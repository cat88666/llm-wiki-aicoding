> ⚠️ **已废弃 / 历史中间副本**：本文件是 01 进入房间设计的早期草稿。正式版见 [`../../Junk-游戏准备重构/01-进入房间-重构设计.md`](../../具体模块功能重构/01-进入房间-重构设计.md)。保留仅作追溯，**请勿据此开发**。

# 进入房间重构设计文档

> 对应分析文档：`docs/Junk-游戏准备重构/01-进入房间.md`
> 设计日期：2026-06-03
> 工程：dx-game-frame + dx-game-guandan
> 分支：20260615/junk

## 1. 背景与目标

当前进房流程所有逻辑堆在 `EnterBaseTableHandlerDefault.handleData()`，存在：
- P0：私人房人数计数"校验即递增"，失败路径不补偿，可能错误判满
- P0：多处直接读取缓存对象无空保护，异常重连时系统异常
- P1：PLAYER 线程写 WATCH_USER 与 TABLE 线程并发不安全
- P1：后置事件吞异常，异常带出（资金）不可靠
- P2：大量 `GsonUtils.toJson(context)` info 日志，高峰 CPU 放大

目标：消除所有 P0/P1 问题，结构性拆分编排、校验、状态写入、快照组装四个关注点，保持协议和 DTO 完全兼容。

## 2. 决策记录

| 决策项 | 结论 |
|--------|------|
| 主导方案 | Frame 主导（方案 A）：EnterRoomFlowService 放 frame，guandan 提供 contributor 扩展 |
| 字段重命名 | `isNewRoomUser` 全量重命名为 `alreadyInRoom`（直接重命名，全量搜索引用） |
| 灰度开关 | 不做开关，直接替换，依赖测试覆盖 |
| 线程模型 | 保留 PLAYER 线程入口，`EnterRoomStateService` 内用表级 `ReentrantLock` 串行化状态写入 |
| 后置事件 | 异常带出从事件监听剥离，改为 `after()` 中直接同步调用 |

## 3. 整体架构

### 改造前

```
EnterTableCommand (PLAYER线程)
  └─ EnterBaseTableHandlerDefault
       ├─ initContext()        — 读缓存、设 isNewRoomUser
       ├─ check()              — 7个静态校验散落
       ├─ handleData()         — 7类动作串联（含NPE风险、日志大量序列化）
       └─ after()              — 事件+响应+通知+异常带出混在一起
```

### 改造后

```
EnterTableCommand (PLAYER线程)
  └─ EnterBaseTableHandlerDefault
       ├─ initContext()        — 保留，isNewRoomUser → alreadyInRoom
       ├─ check()              — 委托 EnterRoomValidatorChain
       ├─ handleData()         — 委托 EnterRoomFlowService.execute(context)
       └─ after()              — 异常带出直接调用，事件只保留轨迹/活动

EnterRoomFlowService (frame, Spring Bean)
  ├─ EnterRoomValidatorChain     — 内置校验 + IEnterRoomValidationExtension 扩展
  ├─ EnterRoomStateService       — 表级锁 + GdReconnectStateService
  └─ EnterRoomSnapshotAssembler  — DTO组装 + IEnterRoomHandAssembler 扩展

dx-game-guandan 扩展：
  ├─ GdEnterRoomValidationExtension  — 账号锁定、代理风控、私人房人数（R-01修复）
  ├─ GdReconnectStateService          — 取消托管、清预退出/预站起
  └─ GdEnterRoomHandAssembler         — 手牌/贡还贡/转蛋/结算重连快照
```

**兼容性原则**：
- 协议号 1000、`EnterRoomReqDto`、`EnterRoomRespDtoV2` 字段不变
- `EnterBaseTableHandlerDefault` 所有 public 方法签名保留
- Handler 路由（`HandlerSpaceService`）、`@ThreadModel(PLAYER)` 不变

## 4. 安全改造（R-01 / R-02 / R-03）

### R-01：私人房人数计数修复

**文件**：`BaseTableCheckService.checkPrivateTableUserUpperLimit()`

改法：去掉 `incrementAndGet`，改用 WATCH_USER + PLAYER_USER 实际集合大小判断：

```java
public static void checkPrivateTableUserUpperLimit(Long tableId, Boolean alreadyInRoom) {
    if (alreadyInRoom) return;
    BaseTableInfo tableInfo = BaseTableInfoCache.getTableInfo(tableId);
    int currentCount = BaseTableUserCache.fetchTableUserIds(tableId, TableUserCacheEnum.WATCH_USER).size()
                     + BaseTableUserCache.fetchTableUserIds(tableId, TableUserCacheEnum.PLAYER_USER).size();
    if (currentCount >= tableInfo.getPrivateUpperLimit()) {
        log.info("房间{}人数已达上限{}，禁止进入，当前:{}", tableId, tableInfo.getPrivateUpperLimit(), currentCount);
        throw BusinessException.createException(BusinessExceptionTypeEnums.PRIVATE_ENT_ROOM_EXCEEDS_LIMIT);
    }
}
```

`BaseTable.enterRoomUserCount` 字段保留（不删，避免序列化问题），不再 increment。

### R-02：空值保护

| 位置 | 保护方式 |
|------|----------|
| `buildEnterRoomUserInfo` wallet 读取 | `wallet != null` 才取 nextBringIn/Out，否则置 0 |
| `GdEnterRoomHandAssembler` tableHand 读取 | `tableHand != null` 才组装手牌快照，否则返回空 DTO |
| `TableUserHandBootstrap` raceGlobalConfig 读取 | `getRaceGlobalConfig() != null` 才读 playingCardTime |

### R-03：日志收敛

`EnterBaseTableHandlerDefault` 所有 `GsonUtils.toJson(context)` / `toJson(enterRoomResp)` / `toJson(userList)` 的 info 日志降为 **debug**。

只保留两条 info：
```java
log.info("进入房间 tableId:{} userId:{} alreadyInRoom:{}", tableId, userId, context.isAlreadyInRoom());
log.info("进入房间成功 tableId:{} userId:{} handCode:{}", tableId, userId, handCode);
```

`TableUserHandBootstrap` 手牌 Map 日志同理降为 debug。

## 5. 新增组件详细设计

### 5.1 `EnterRoomFlowService`（frame）

**包**：`com.dx.game.frame.service.biz.enterroom`

```java
@Component
public class EnterRoomFlowService {
    @Resource EnterRoomValidatorChain    validatorChain;
    @Resource EnterRoomStateService      stateService;
    @Resource EnterRoomSnapshotAssembler snapshotAssembler;

    public void execute(EnterRoomContextV2 context) {
        validatorChain.validate(context);
        stateService.applyState(context);
        snapshotAssembler.assemble(context);
        UserRiskCache.initRiskDataEnterRoom(context.getRequest());
    }
}
```

### 5.2 `EnterRoomValidatorChain`（frame）

**包**：`com.dx.game.frame.service.biz.enterroom`

内置 frame 原有 8 个校验（device / table / currency / watchUserLimit / pwd / kick / lockClub / club），然后按序调用所有 `IEnterRoomValidationExtension`：

```java
@Component
public class EnterRoomValidatorChain {
    @Resource List<IEnterRoomValidationExtension> contributors;

    public void validate(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId  = context.getRequest().getUserId();
        Boolean alreadyInRoom = context.isAlreadyInRoom();

        BaseTableCheckService.checkDevice(tableId, context.getRequest().getDeviceType());
        BaseTableCheckService.checkTable(tableId);
        BaseTableCheckService.checkCurrency(tableId, userId);
        BaseTableCheckService.checkTableWatchUserLimit(tableId, alreadyInRoom);
        BaseUserCheckAuthService.checkUserPwd(tableId, userId, context.getRequest().getTableEntryPassword());
        BaseUserCheckAuthService.checkUserKick(tableId, userId);
        BaseUserCheckAuthService.checkUserLockClub(userId, alreadyInRoom);
        BaseUserCheckAuthService.checkUserClub(tableId, userId, alreadyInRoom);

        SpaceTypeEnum spaceType = context.getSpaceType();
        contributors.stream()
            .filter(c -> c.supports(spaceType))
            .forEach(c -> c.validate(context));
    }
}
```

**接口**（frame）：
```java
public interface IEnterRoomValidationExtension {
    void validate(EnterRoomContextV2 context);
    default boolean supports(SpaceTypeEnum spaceType) { return true; }
}
```

**`GdEnterRoomValidationExtension`**（guandan）：
```java
@Component
public class GdEnterRoomValidationExtension implements IEnterRoomValidationExtension {
    public void validate(EnterRoomContextV2 context) {
        Long tableId      = context.getTableId();
        Long userId       = context.getRequest().getUserId();
        Boolean alreadyInRoom = context.isAlreadyInRoom();
        // 私人房人数上限（R-01 新实现）
        BaseTableCheckService.checkPrivateTableUserUpperLimit(tableId, alreadyInRoom);
        // 账号锁定（私人房）
        BaseUserCheckAuthService.checkUserLockPrivate(userId, alreadyInRoom);
        // 代理风控锁定
        // userBaseInfo.getTopProxyWindCtlStatus() 校验
    }
    @Override
    public boolean supports(SpaceTypeEnum spaceType) {
        return spaceType == SpaceTypeEnum.PRIVATE || spaceType == SpaceTypeEnum.CLUB;
    }
}
```

### 5.3 `EnterRoomStateService`（frame）

**包**：`com.dx.game.frame.service.biz.enterroom`

```java
@Component
public class EnterRoomStateService {
    @Resource(required = false) GdReconnectStateService gdReconnectStateService;

    private final ConcurrentHashMap<Long, ReentrantLock> tableLocks = new ConcurrentHashMap<>();

    public void applyState(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        ReentrantLock lock = tableLocks.computeIfAbsent(tableId, k -> new ReentrantLock());
        lock.lock();
        try {
            if (context.isAlreadyInRoom()) {
                if (gdReconnectStateService != null) {
                    gdReconnectStateService.recover(context);
                }
            } else {
                GameUserBootStrapService.handUserItem(context);
            }
        } finally {
            lock.unlock();
        }
    }

    public void releaseTableLock(Long tableId) {
        tableLocks.remove(tableId);
    }
}
```

**`GdReconnectStateService`**（guandan）：
```java
@Component
public class GdReconnectStateService {
    @Resource GdGameUserBootstrap gdGameUserBootstrap;

    public void recover(EnterRoomContextV2 context) {
        gdGameUserBootstrap.restartLoadHand(context.getTableId(), context.getRequest().getUserId());
    }
}
```

### 5.4 `EnterRoomSnapshotAssembler`（frame）

**包**：`com.dx.game.frame.service.biz.enterroom`

> **循环依赖说明**：`EnterBaseTableHandlerDefault` → `EnterRoomFlowService` → `EnterRoomSnapshotAssembler`，如果 Assembler 再注入 Handler 就形成循环。因此 Assembler **直接持有**组装所需的底层依赖，不注入 Handler。`EnterBaseTableHandlerDefault` 中原有的 `buildXxx()` protected 方法保留为 deprecated stub（其他游戏子类若有覆盖仍可兼容），新流程不再调用它们。

```java
@Component
public class EnterRoomSnapshotAssembler {
    @Resource(required = false) IEnterRoomHandAssembler handAssembler;
    // 直接注入组装所需底层依赖（来自原 buildXxx 方法的依赖）
    @Resource BaseUserWalletService      baseUserWalletService;
    @Resource BaseSystemParamsConfig     baseSystemParamsConfig;
    @Resource BaseAnonymousService       baseAnonymousService;
    @Resource GameUserHandBootstrapService gameUserHandBootstrapService;

    public void assemble(EnterRoomContextV2 context) {
        assembleUserGameConfig(context);   // 含 R-02 wallet 空值保护
        assembleUserList(context);
        if (handAssembler != null) {
            handAssembler.assembleHand(context);  // 含 R-02 tableHand 空值保护
        } else {
            assembleTableHand(context);           // frame fallback
        }
        assembleTableInfo(context);        // 含 R-02 raceGlobalConfig 保护
        assembleUserConfig(context);
    }

    private void assembleUserGameConfig(EnterRoomContextV2 context) {
        // 迁移自 EnterBaseTableHandlerDefault.buildEnterRoomUserInfo()
        // R-02：wallet 空值保护
        TableUserWallet wallet = TableUserWalletCache.getWallet(tableId, userId, WalletConstant.walletType);
        if (wallet != null) {
            userGameConfig.setNextBringInChipScore(wallet.getNextBringInChipScore());
            userGameConfig.setNextBringOutChipScore(wallet.getNextBringOutChipScore());
        }
        // ... 其余字段照搬
    }

    private void assembleTableInfo(EnterRoomContextV2 context) {
        // 迁移自 buildTableInfoData，raceGlobalConfig 空值保护由 GameUserHandBootstrapService 内部处理
        context.getEnterRoomRespDtoV2().setTableInfoDto(
            GameUserHandBootstrapService.buildTableInfo(context.getTableId()));
    }

    // assembleUserList / assembleTableHand / assembleUserConfig 类似迁移
}
```

**接口**（frame）：
```java
public interface IEnterRoomHandAssembler {
    void assembleHand(EnterRoomContextV2 context);
}
```

**`GdEnterRoomHandAssembler`**（guandan）：
```java
@Component
public class GdEnterRoomHandAssembler implements IEnterRoomHandAssembler {
    @Resource TableUserHandBootstrap tableUserHandBootstrap;

    public void assembleHand(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId  = context.getRequest().getUserId();
        // tableHand 空值保护
        BaseTableHand tableHand = BaseTableHandCache.getTableHand(tableId);
        if (tableHand == null) {
            log.warn("assembleHand tableHand 为空, tableId:{} userId:{}", tableId, userId);
            return;
        }
        BaseTableHandDto handDto = tableUserHandBootstrap.buildTableHandInfo(tableId, userId);
        context.getEnterRoomRespDtoV2().setTableHandDto(handDto);
        Map<Integer, BaseTableUserHandDto> userHandMap = tableUserHandBootstrap.buildTableUserHand(tableId, userId);
        context.getEnterRoomRespDtoV2().setTableUserHandMap(userHandMap);
    }
}
```

## 6. R-08：后置事件拆分

**`after()` 改造**（`EnterBaseTableHandlerDefault`）：

```java
protected void after(EnterRoomContextV2 context) {
    Long tableId = context.getTableId();
    Long userId  = context.getUserBaseInfo().getUserId();
    BaseTableHand tableHand = BaseTableHandCache.getTableHand(tableId);

    // 1. 异常带出：直接同步调用，仅对新用户（重连跳过），不能静默丢失
    //    对应原 BaseUserEnterRoomFinishListener 中 !isNewRoomUser 分支
    if (!context.isAlreadyInRoom()) {
        userTrackService.pushTableEntryExitRecord(userId, tableId,
            UserEntryExitTypeEnums.ENTER_ROOM, UserEntryExitReasonEnums.DEFAULT,
            KickerReasonEnum.DEFAULT.getDescribe());
        TableUserWallet wallet = TableUserWalletCache.getWallet(tableId, userId, WalletConstant.walletType);
        if (wallet != null && !BaseTableUserCache.hasQuitUser(tableId, userId)
                && wallet.getBalance().compareTo(BigDecimal.ZERO) > 0) {
            log.info("进入房间-处理异常未带出筹码 tableId:{} userId:{}", tableId, userId);
            UserBringOutBootstrapService.bringOutByQuit(tableId, userId);
        }
    }

    // 2. 轨迹/活动事件（可失败，监听器内 catch 打日志）
    applicationEventPublisher.publishEvent(
        new UserEnterRoomFinishEventV2(context, tableHand != null ? tableHand.getHandCode() : null));

    // 3. 发送响应
    EnterRoomRespDtoV2 enterRoomResp = context.getEnterRoomRespDtoV2();
    log.info("进入房间成功 tableId:{} userId:{}", tableId, userId);
    NetResponseBody netResponseBody = NetResponseBuilder.buildResponse(
        CommonProto.ENTER_ROOM, NoticeEncryptUtils.encrypt(enterRoomResp, tableId, userId), context.getRequest());
    SendUtil.send(netResponseBody);

    // 4. 清理、私人房、广播（保持不变）
    baseUserOnlineService.clearOfflineStartTime(tableId, userId);
    BaseTableInfo tableInfo = BaseTableInfoCache.getTableInfo(tableId);
    if (tableInfo.isPrivateTable()) {
        retryPrivateTableRedisService.joinPrivateTable(userId, tableId);
    }
    enterRoomNotice.sendNotice(tableId, userId, context.isAlreadyInRoom());
}
```

`BaseUserEnterRoomFinishListener` 移除 `异常带出` 分支，只保留轨迹和活动逻辑。

## 7. 字段重命名：`isNewRoomUser` → `alreadyInRoom`

搜索范围：dx-game-frame + dx-game-guandan 全量

| 位置 | 变更 |
|------|------|
| `EnterRoomContextV2.java` | 字段 `isNewRoomUser` → `alreadyInRoom`，getter `getIsNewRoomUser()` → `isAlreadyInRoom()` |
| `EnterBaseTableHandlerDefault.java` | 所有引用替换 |
| `BaseUserEnterRoomFinishListener.java` | `!context.getIsNewRoomUser()` → `!context.isAlreadyInRoom()` |
| `EnterRoomNotice.java` | 参数替换 |
| dx-game-guandan 所有引用处 | 全量替换 |

## 8. 新增文件清单

### dx-game-frame

| 文件 | 包 |
|------|-----|
| `EnterRoomFlowService.java` | `com.dx.game.frame.service.biz.enterroom` |
| `EnterRoomValidatorChain.java` | `com.dx.game.frame.service.biz.enterroom` |
| `IEnterRoomValidationExtension.java` | `com.dx.game.frame.service.biz.enterroom` |
| `EnterRoomStateService.java` | `com.dx.game.frame.service.biz.enterroom` |
| `EnterRoomSnapshotAssembler.java` | `com.dx.game.frame.service.biz.enterroom` |
| `IEnterRoomHandAssembler.java` | `com.dx.game.frame.service.biz.enterroom` |

### dx-game-guandan

| 文件 | 包 |
|------|-----|
| `GdEnterRoomValidationExtension.java` | `com.dx.game.guandan.service.bootstrap.enterroom` |
| `GdReconnectStateService.java` | `com.dx.game.guandan.service.bootstrap.enterroom` |
| `GdEnterRoomHandAssembler.java` | `com.dx.game.guandan.service.bootstrap.enterroom` |

## 9. 修改文件清单

| 文件 | 变更内容 |
|------|----------|
| `EnterRoomContextV2.java` | 重命名 `isNewRoomUser` → `alreadyInRoom` |
| `EnterBaseTableHandlerDefault.java` | handleData 委托 FlowService；after 剥离异常带出；日志降级(R-03) |
| `BaseTableCheckService.java` | checkPrivateTableUserUpperLimit 改为集合计数(R-01)；wallet空值保护(R-02) |
| `BaseUserEnterRoomFinishListener.java` | 移除异常带出分支 |
| `TableUserHandBootstrap.java` | raceGlobalConfig/tableHand 空值保护(R-02)；日志降级(R-03) |
| 所有引用 `isNewRoomUser` 的文件 | 全量重命名 |

## 10. 协议兼容确认

| 协议 | 变更 | 兼容性 |
|------|------|--------|
| 1000 请求 `EnterRoomReqDto` | 不变 | 完全兼容 |
| 1000 响应 `EnterRoomRespDtoV2` | 不变 | 完全兼容 |
| 14015 通知 `NewUserMsgDto` | 不变 | 完全兼容 |

## 11. 验收关键场景

1. 私人房重复进房：同一 userId 并发请求，WATCH_USER 只出现一次，人数上限不重复增加
2. 游戏中重连：有 `TableUserHand` 且 systemType=1，重连后取消托管、发取消托管通知
3. 缓存缺失容错：钱包、TableHand、raceGlobalConfig 任一缺失时返回明确业务异常，不抛系统异常
4. 异常带出：进房成功后异常带出逻辑执行，失败时有错误日志和指标，不静默丢失
