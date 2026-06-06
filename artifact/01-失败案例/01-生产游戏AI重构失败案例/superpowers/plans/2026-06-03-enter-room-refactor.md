> ⚠️ **已废弃 / 历史中间副本**：本文件是 01 进入房间实现计划的早期草稿。正式版见 [`../../Junk-游戏准备重构/01-进入房间-实现计划.md`](../../Junk-游戏准备重构/01-进入房间-实现计划.md)。保留仅作追溯，**请勿据此开发**。

# 进入房间重构 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 实现进入房间重构 R-01~R-08，消除私人房计数 P0 bug、空指针风险、线程并发问题、日志膨胀，并将编排/校验/状态/快照四个关注点结构性分离。

**Architecture:** Frame 主导。新增 `EnterRoomValidatorChain`（校验）、`EnterRoomStateService`（状态+锁）、`EnterRoomSnapshotAssembler`（快照组装）、`EnterRoomFlowService`（编排后三者）。Guandan 提供三个扩展实现：`GdEnterRoomValidationExtension`、`GdReconnectStateService`、`GdEnterRoomHandAssembler`。`EnterBaseTableHandlerDefault.handleData()` 委托 FlowService，`check()` 委托 ValidatorChain。

**Tech Stack:** Java 11, Spring Boot, Lombok，无外部新依赖。

---

## 路径常量（本计划全局使用）

```
FRAME_SVC  = dx-game-frame/dx-game-frame-service/src/main/java/com/dx/game/frame/service
FRAME_MODEL = dx-game-frame/dx-game-frame-model/src/main/java/com/dx/game/frame/model
GD_SVC     = dx-game-guandan/dx-game-guandan-service/src/main/java/com/dx/game/guandan/service
```

---

## Task 1：重命名 `isNewRoomUser` → `alreadyInRoom`（EnterRoomContextV2）

**Files:**
- Modify: `FRAME_MODEL/context/EnterRoomContextV2.java`
- Modify: `FRAME_SVC/biz/bootstrap/command/enterRoom/EnterBaseTableHandlerDefault.java`（所有引用）
- Modify: `FRAME_SVC/biz/bootstrap/command/enterRoom/EnterPrivateTableHandlerDefault.java`
- Modify: `FRAME_SVC/listener/BaseUserEnterRoomFinishListener.java`

- [ ] **Step 1: 修改 EnterRoomContextV2.java**

完整替换文件（Lombok `@Data` 自动生成 getter/setter，字段名改了 getter 跟着改）：

```java
package com.dx.game.frame.model.context;

import com.dx.game.frame.model.cache.UserBaseInfo;
import com.dx.game.frame.model.dto.enterroom.EnterRoomReqDto;
import com.dx.game.frame.model.dto.enterroom.EnterRoomRespDtoV2;
import lombok.Data;
import lombok.EqualsAndHashCode;

@EqualsAndHashCode(callSuper = true)
@Data
public class EnterRoomContextV2 extends CommandContext<EnterRoomReqDto> {
    public EnterRoomContextV2(EnterRoomReqDto request) {
        super(request);
    }

    /** true = 用户已在房间（重连），false = 新用户首次进入 */
    private Boolean alreadyInRoom = Boolean.FALSE;

    private UserBaseInfo userBaseInfo;

    private EnterRoomRespDtoV2 enterRoomRespDtoV2 = new EnterRoomRespDtoV2();
}
```

- [ ] **Step 2: 批量替换 EnterBaseTableHandlerDefault.java 中的引用**

在 `EnterBaseTableHandlerDefault.java` 中执行以下替换（共 4 处）：

| 旧字符串 | 新字符串 |
|---------|---------|
| `context.getIsNewRoomUser()` | `context.getAlreadyInRoom()` |
| `context.setIsNewRoomUser(` | `context.setAlreadyInRoom(` |

具体位置：
- `initContext()` L78：`context.setAlreadyInRoom(BaseUserCheckService.checkUserIsInRoom(tableId, userId));`
- `check()` L97：`Boolean inRoomUser = context.getAlreadyInRoom();`
- `buildEnterRoomUserInfo()` L253：`if (context.getAlreadyInRoom()) {`
- `after()` L173：`enterRoomNotice.sendNotice(tableId, userId, context.getAlreadyInRoom());`

- [ ] **Step 3: 修改 EnterPrivateTableHandlerDefault.java**

将 `check()` 方法 L43 的：
```java
Boolean inRoomUser = context.getIsNewRoomUser();
```
改为：
```java
Boolean inRoomUser = context.getAlreadyInRoom();
```

- [ ] **Step 4: 修改 BaseUserEnterRoomFinishListener.java L52**

```java
// 旧
if (!context.getIsNewRoomUser()) {
// 新
if (!context.getAlreadyInRoom()) {
```

- [ ] **Step 5: 确认无遗漏引用**

```bash
grep -rn "getIsNewRoomUser\|setIsNewRoomUser\|isNewRoomUser" \
  dx-game-frame/dx-game-frame-model/src/main/java/ \
  dx-game-frame/dx-game-frame-service/src/main/java/ \
  dx-game-guandan/dx-game-guandan-service/src/main/java/ \
  --include="*.java"
```

预期：只剩 `EnterRoomContext.java`（旧版 context，非 V2，保留不动）。

- [ ] **Step 6: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "refactor: rename isNewRoomUser to alreadyInRoom in EnterRoomContextV2"
```

---

## Task 2：R-01 私人房人数计数修复（BaseTableCheckService）

**Files:**
- Modify: `FRAME_SVC/biz/base/BaseTableCheckService.java`

- [ ] **Step 1: 替换 checkPrivateTableUserUpperLimit 方法（L67-79）**

```java
public static void checkPrivateTableUserUpperLimit(Long tableId, Boolean alreadyInRoom) {
    if (alreadyInRoom) {
        return;
    }
    BaseTableInfo tableInfo = BaseTableInfoCache.getTableInfo(tableId);
    int currentCount = BaseTableUserCache.fetchTableUserIds(tableId, TableUserCacheEnum.WATCH_USER).size()
                     + BaseTableUserCache.fetchTableUserIds(tableId, TableUserCacheEnum.PLAYER_USER).size();
    if (currentCount >= tableInfo.getPrivateUpperLimit()) {
        log.info("私人房人数已达上限，禁止进入 tableId:{} limit:{} current:{}",
                tableId, tableInfo.getPrivateUpperLimit(), currentCount);
        throw BusinessException.createException(BusinessExceptionTypeEnums.PRIVATE_ENT_ROOM_EXCEEDS_LIMIT);
    }
}
```

> 注：`BaseTable.enterRoomUserCount` 字段保留（不删，防止反序列化问题），不再被本方法 increment。

- [ ] **Step 2: 确认调用方签名兼容**

```bash
grep -rn "checkPrivateTableUserUpperLimit" \
  dx-game-frame/dx-game-frame-service/src/main/java/ --include="*.java"
```

预期输出仅 `EnterPrivateTableHandlerDefault.java:66` 和 `BaseTableCheckService.java`。参数签名不变（Long tableId, Boolean alreadyInRoom）。

- [ ] **Step 3: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "fix(R-01): 私人房人数上限改用WATCH+PLAYER实际集合计数"
```

---

## Task 3：R-02 空值保护 + R-03 日志收敛（EnterBaseTableHandlerDefault）

**Files:**
- Modify: `FRAME_SVC/biz/bootstrap/command/enterRoom/EnterBaseTableHandlerDefault.java`

- [ ] **Step 1: buildEnterRoomUserInfo 中 wallet 空值保护（L266-268）**

将：
```java
TableUserWallet wallet = TableUserWalletCache.getWallet(tableId, userId, WalletConstant.walletType);
userGameConfig.setNextBringInChipScore(wallet.getNextBringInChipScore());
userGameConfig.setNextBringOutChipScore(wallet.getNextBringOutChipScore());
```
改为：
```java
TableUserWallet wallet = TableUserWalletCache.getWallet(tableId, userId, WalletConstant.walletType);
if (wallet != null) {
    userGameConfig.setNextBringInChipScore(wallet.getNextBringInChipScore());
    userGameConfig.setNextBringOutChipScore(wallet.getNextBringOutChipScore());
} else {
    log.warn("进入房间-钱包缓存为空 tableId:{} userId:{}", tableId, userId);
}
```

- [ ] **Step 2: R-03 日志收敛 - 将 info 级 GsonUtils.toJson 改为 debug**

在 `EnterBaseTableHandlerDefault.java` 中，将以下日志从 `log.info` 改为 `log.debug`：

```java
// initContext() L84
log.debug("进入房间-初始化完成 tableId:{} userId:{}", tableId, userId);

// check() L92 和 L115 — 删除或 debug
// 保留：
log.info("进入房间 tableId:{} userId:{} alreadyInRoom:{}", tableId, userId, context.getAlreadyInRoom());

// check() L115 GsonUtils.toJson(context) → 删除整行

// buildUserData() L238 和 L240 → debug
log.debug("进入房间-buildUserData tableId:{} userId:{} count:{}", userId, tableId, tableUsers.size());

// buildTableHandData() L207 和 L210 → debug
log.debug("进入房间-buildTableHandData tableId:{} userId:{}", userId, tableId);

// handleData() L140
log.info("进入房间成功 tableId:{} userId:{}", tableId, userId);
```

- [ ] **Step 3: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "fix(R-02/R-03): wallet空值保护，收敛进入房间info日志"
```

---

## Task 4：R-02 空值保护 + R-03 日志收敛（TableUserHandBootstrap）

**Files:**
- Modify: `GD_SVC/bootstrap/TableUserHandBootstrap.java`

- [ ] **Step 1: buildTableInfo 中 raceGlobalConfig 空值保护（L819）**

将：
```java
tableInfoEnterRoomDto.setRaceGlobalConfig(tableInfo.getRaceGlobalConfig());
tableInfoEnterRoomDto.setPlayingCardTime(tableInfo.getRaceGlobalConfig().getPlayingCardTime());
```
改为：
```java
tableInfoEnterRoomDto.setRaceGlobalConfig(tableInfo.getRaceGlobalConfig());
if (tableInfo.getRaceGlobalConfig() != null) {
    tableInfoEnterRoomDto.setPlayingCardTime(tableInfo.getRaceGlobalConfig().getPlayingCardTime());
}
```

- [ ] **Step 2: buildTableUserHand 中 L89 手牌 Map 日志改为 debug**

```java
// 将
log.info("进入牌桌,tableId={}, userId={}, 当前牌桌手牌数据{}", tableId, userId, GsonUtils.toJson(tableUserHandMap));
// 改为
log.debug("进入牌桌,tableId={}, userId={}, 当前牌桌手牌数据{}", tableId, userId, GsonUtils.toJson(tableUserHandMap));
```

- [ ] **Step 3: Commit**

```bash
git -C dx-game-guandan add -A && git -C dx-game-guandan commit -m "fix(R-02/R-03): raceGlobalConfig空值保护，手牌日志改debug"
```

---

## Task 5：创建 frame 接口文件

**Files:**
- Create: `FRAME_SVC/biz/enterroom/IEnterRoomValidationExtension.java`
- Create: `FRAME_SVC/biz/enterroom/IEnterRoomHandAssembler.java`

- [ ] **Step 1: 创建 IEnterRoomValidationExtension.java**

```java
package com.dx.game.frame.service.biz.enterroom;

import com.dx.game.frame.model.context.EnterRoomContextV2;

/**
 * 进入房间校验扩展点，游戏侧实现并注册为 Spring Bean，框架自动发现并按序调用。
 */
public interface IEnterRoomValidationExtension {

    /**
     * 执行校验，失败时抛 BusinessException。
     */
    void validate(EnterRoomContextV2 context);
}
```

- [ ] **Step 2: 创建 IEnterRoomHandAssembler.java**

```java
package com.dx.game.frame.service.biz.enterroom;

import com.dx.game.frame.model.context.EnterRoomContextV2;

/**
 * 进入房间手牌快照组装扩展点，游戏侧实现并注册为 Spring Bean，Assembler 自动注入并调用。
 */
public interface IEnterRoomHandAssembler {

    /**
     * 组装 tableHandDto 和 tableUserHandMap 并写入 context.enterRoomRespDtoV2。
     */
    void assembleHand(EnterRoomContextV2 context);
}
```

- [ ] **Step 3: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "feat: 新增 IEnterRoomValidationExtension/IEnterRoomHandAssembler 接口"
```

---

## Task 6：创建 EnterRoomValidatorChain（frame）

**Files:**
- Create: `FRAME_SVC/biz/enterroom/EnterRoomValidatorChain.java`

- [ ] **Step 1: 创建文件**

```java
package com.dx.game.frame.service.biz.enterroom;

import com.dx.game.frame.model.cache.BaseTableInfo;
import com.dx.game.frame.model.context.EnterRoomContextV2;
import com.dx.game.frame.repository.local.cache.BaseTableInfoCache;
import com.dx.game.frame.service.biz.base.BaseTableCheckService;
import com.dx.game.frame.service.biz.base.BaseUserCheckAuthService;
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;
import java.util.List;

/**
 * 进入房间统一校验链。
 * 公共校验内置，私人房 vs 俱乐部/大厅/比赛 分支处理，游戏侧通过 IEnterRoomValidationExtension 扩展。
 */
@Slf4j
@Component
public class EnterRoomValidatorChain {

    @Resource
    private List<IEnterRoomValidationExtension> contributors;

    public void validate(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId = context.getRequest().getUserId();
        Boolean alreadyInRoom = context.getAlreadyInRoom();
        String password = context.getRequest().getTableEntryPassword();
        Integer deviceType = context.getRequest().getDeviceType();
        BaseTableInfo tableInfo = BaseTableInfoCache.getTableInfo(tableId);

        // 公共校验（所有空间类型）
        BaseTableCheckService.checkDevice(tableId, deviceType);
        BaseTableCheckService.checkTable(tableId);
        BaseTableCheckService.checkCurrency(tableId, userId);
        BaseTableCheckService.checkTableWatchUserLimit(tableId, alreadyInRoom);
        BaseUserCheckAuthService.checkUserKick(tableId, userId);

        if (tableInfo.isPrivateTable()) {
            // 私人房校验
            BaseUserCheckAuthService.checkUserLockPrivate(userId, alreadyInRoom);
            BaseUserCheckAuthService.checkTableAuth(tableId, userId, deviceType);
            BaseUserCheckAuthService.checkUserPrivate(tableId, userId, alreadyInRoom);
            BaseUserCheckAuthService.checkTouristStatus(tableId, userId);
            BaseTableCheckService.checkPrivateTableUserUpperLimit(tableId, alreadyInRoom);
        } else {
            // 俱乐部 / 大厅 / 比赛校验
            BaseUserCheckAuthService.checkUserPwd(tableId, userId, password);
            BaseUserCheckAuthService.checkUserLockClub(userId, alreadyInRoom);
            BaseUserCheckAuthService.checkUserClub(tableId, userId, alreadyInRoom);
        }

        // 游戏侧扩展校验
        for (IEnterRoomValidationExtension contributor : contributors) {
            contributor.validate(context);
        }
    }
}
```

- [ ] **Step 2: 修改 EnterBaseTableHandlerDefault.check() 使用 ValidatorChain**

在 `EnterBaseTableHandlerDefault` 中增加注入并替换 check() 实现：

```java
// 新增 @Resource 注入（放在已有 @Resource 列表末尾）
@Resource
EnterRoomValidatorChain enterRoomValidatorChain;
```

将 `check()` 方法体替换为：
```java
public void check(EnterRoomContextV2 context) {
    log.info("进入房间-校验开始 tableId:{} userId:{}",
            context.getTableId(), context.getRequest().getUserId());
    enterRoomValidatorChain.validate(context);
    log.info("进入房间-校验通过 tableId:{} userId:{}",
            context.getTableId(), context.getRequest().getUserId());
}
```

- [ ] **Step 3: 修改 EnterPrivateTableHandlerDefault.check() 使用 ValidatorChain**

在 `EnterPrivateTableHandlerDefault` 增加注入：

```java
// 在类顶部 @Resource 注入
@Resource
private EnterRoomValidatorChain enterRoomValidatorChain;
```

将 `check()` 方法体替换为：
```java
public void check(EnterRoomContextV2 context) {
    log.info("私人房-进入房间-校验开始 tableId:{} userId:{}",
            context.getTableId(), context.getRequest().getUserId());
    enterRoomValidatorChain.validate(context);
    log.info("私人房-进入房间-校验通过 tableId:{} userId:{}",
            context.getTableId(), context.getRequest().getUserId());
}
```

- [ ] **Step 4: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "feat(R-05): 新增 EnterRoomValidatorChain，check() 委托校验链"
```

---

## Task 7：创建 EnterRoomStateService（R-07，frame）

**Files:**
- Create: `FRAME_SVC/biz/enterroom/EnterRoomStateService.java`

- [ ] **Step 1: 创建文件**

```java
package com.dx.game.frame.service.biz.enterroom;

import com.dx.game.frame.model.context.EnterRoomContextV2;
import com.dx.game.frame.service.biz.bootstrap.GameUserBootStrapService;
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.locks.ReentrantLock;

/**
 * 进入房间状态写入服务。
 * 用表级 ReentrantLock 保证同桌 WATCH_USER 写入与 TABLE 线程操作线性化，解决 PLAYER 线程并发风险（P-03）。
 */
@Slf4j
@Component
public class EnterRoomStateService {

    /**
     * 游戏侧可选注入：重连状态恢复（如取消托管、清预退出标记）。
     * 无游戏侧实现时走 frame 默认路径。
     */
    @Resource(required = false)
    private IReconnectStateHandler reconnectStateHandler;

    private final ConcurrentHashMap<Long, ReentrantLock> tableLocks = new ConcurrentHashMap<>();

    public void applyState(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId = context.getRequest().getUserId();
        ReentrantLock lock = tableLocks.computeIfAbsent(tableId, k -> new ReentrantLock());
        lock.lock();
        try {
            if (context.getAlreadyInRoom()) {
                log.info("进入房间-重连路径 tableId:{} userId:{}", tableId, userId);
                if (reconnectStateHandler != null) {
                    reconnectStateHandler.recover(context);
                }
            } else {
                log.info("进入房间-新用户路径 tableId:{} userId:{}", tableId, userId);
                GameUserBootStrapService.handUserItem(context);
            }
        } finally {
            lock.unlock();
        }
    }

    /** 桌解散时调用，释放锁对象防止内存泄漏。 */
    public void releaseTableLock(Long tableId) {
        tableLocks.remove(tableId);
    }
}
```

- [ ] **Step 2: 创建 IReconnectStateHandler 接口**

```java
// FRAME_SVC/biz/enterroom/IReconnectStateHandler.java
package com.dx.game.frame.service.biz.enterroom;

import com.dx.game.frame.model.context.EnterRoomContextV2;

/**
 * 重连状态恢复扩展点（如取消托管、清预退出/预站起标记）。
 */
public interface IReconnectStateHandler {
    void recover(EnterRoomContextV2 context);
}
```

- [ ] **Step 3: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "feat(R-07): 新增 EnterRoomStateService，表级锁保护WATCH_USER写入"
```

---

## Task 8：创建 EnterRoomSnapshotAssembler（frame）

**Files:**
- Create: `FRAME_SVC/biz/enterroom/EnterRoomSnapshotAssembler.java`

- [ ] **Step 1: 创建文件**

注意：Assembler 直接持有底层依赖，不注入 `EnterBaseTableHandlerDefault`（避免循环依赖）。代码来自原 `buildXxx` 方法，含 R-02 空值保护。

```java
package com.dx.game.frame.service.biz.enterroom;

import cn.hutool.json.JSONUtil;
import com.dx.facade.account.change.WalletType;
import com.dx.game.frame.common.config.BaseSystemParamsConfig;
import com.dx.game.frame.common.constant.WalletConstant;
import com.dx.game.frame.model.cache.*;
import com.dx.game.frame.model.context.EnterRoomContextV2;
import com.dx.game.frame.model.dto.base.BaseTableHandDto;
import com.dx.game.frame.model.dto.base.BaseTableUserHandDto;
import com.dx.game.frame.model.dto.user.UserGameConfig;
import com.dx.game.frame.model.dto.user.UserItemDto;
import com.dx.game.frame.model.dto.userfriend.UserFriendRemarkDto;
import com.dx.game.frame.model.dto.userconfig.UserConfigQueryRespDto;
import com.dx.game.frame.constant.constant.CommonConstant;
import com.dx.game.frame.constant.enums.table.TableUserCacheEnum;
import com.dx.game.frame.repository.local.cache.*;
import com.dx.game.frame.service.biz.base.*;
import com.dx.game.frame.service.biz.bootstrap.GameUserBootStrapService;
import com.dx.game.frame.service.biz.bootstrap.GameUserHandBootstrapService;
import com.dx.game.frame.service.convert.BaseTableConvert;
import lombok.extern.slf4j.Slf4j;
import org.apache.commons.collections.CollectionUtils;
import org.springframework.beans.BeanUtils;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;
import java.util.*;
import java.util.stream.Collectors;

/**
 * 进入房间响应 DTO 组装器。
 * 不注入 EnterBaseTableHandlerDefault（避免循环依赖），直接持有底层依赖。
 * 游戏侧通过 IEnterRoomHandAssembler 扩展手牌快照组装。
 */
@Slf4j
@Component
public class EnterRoomSnapshotAssembler {

    @Resource(required = false)
    private IEnterRoomHandAssembler handAssembler;

    @Resource
    private BaseUserWalletService baseUserWalletService;
    @Resource
    private BaseSystemParamsConfig baseSystemParamsConfig;
    @Resource
    private BaseAnonymousService baseAnonymousService;

    public void assemble(EnterRoomContextV2 context) {
        assembleUserGameConfig(context);
        assembleUserList(context);
        assembleHand(context);
        assembleTableInfo(context);
        assembleUserConfig(context);
    }

    private void assembleUserGameConfig(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId = context.getUserBaseInfo().getUserId();
        UserGameConfig userGameConfig = context.getEnterRoomRespDtoV2().getUserGameConfig();

        if (context.getAlreadyInRoom()) {
            Optional<UserTableItem> optional = UserTableItemCache.getAllUserTableItem(tableId).values().stream()
                    .filter(x -> x.getUserId().equals(userId)).findAny();
            userGameConfig.setFirstSitDown(optional.map(UserTableItem::isFirstSitDown).orElse(true));
        } else {
            userGameConfig.setFirstSitDown(true);
        }
        userGameConfig.setLockStandTime(baseSystemParamsConfig.getLockStandTime());
        if (baseSystemParamsConfig.isEnterRoomBalance()) {
            userGameConfig.setBalance(baseUserWalletService.getUserCashWalletBalance(userId, WalletType.cash));
        }
        userGameConfig.setMemberCurrency(UserBaseInfoCache.getUserBaseInfo(userId).getCurrency());

        // R-02: wallet 空值保护
        TableUserWallet wallet = TableUserWalletCache.getWallet(tableId, userId, WalletConstant.walletType);
        if (wallet != null) {
            userGameConfig.setNextBringInChipScore(wallet.getNextBringInChipScore());
            userGameConfig.setNextBringOutChipScore(wallet.getNextBringOutChipScore());
        } else {
            log.warn("assembleUserGameConfig-钱包缓存为空 tableId:{} userId:{}", tableId, userId);
        }

        userGameConfig.setTencentUserSign(BaseUserCheckService.getUserTencentUserSign(userId));
        userGameConfig.setAnonName(BaseAnonymousService.getAnonymousName(tableId, userId));
        UserTableItem userTableItem = UserTableItemCache.getUserTableItem(tableId, userId);
        userGameConfig.setOnlineStatus(userTableItem.getOnlineStatus());

        BaseTableInfo tableInfo = BaseTableInfoCache.getTableInfo(tableId);
        if (tableInfo.isPrivateTable()) {
            assembleButtonDataPrivate(context, tableInfo, userGameConfig);
        } else {
            assembleButtonData(context, tableInfo, userGameConfig);
        }
    }

    private void assembleButtonData(EnterRoomContextV2 context, BaseTableInfo tableInfo, UserGameConfig userGameConfig) {
        Long userId = context.getUserBaseInfo().getUserId();
        Long tableId = context.getTableId();
        UserBaseInfo memberInfo = context.getUserBaseInfo();

        BaseUserItem newUser = BaseTableUserCache.getUser(tableId, userId);
        userGameConfig.setStageId(newUser.getStageId());
        userGameConfig.setHolderId(tableInfo.getHolderId());
        userGameConfig.setBusinessModel(memberInfo.getBusinessModel());
        userGameConfig.setProxyEntryAuthority(memberInfo.getProxyEntryAuthority());

        if (Objects.equals(CommonConstant.ONE, memberInfo.getProxyEntryAuthority())) {
            userGameConfig.setIsProxy(true);
            if (Objects.equals(memberInfo.getClubId(), tableInfo.getClubId())) {
                userGameConfig.setShowStart(true);
            }
            if (Objects.equals(memberInfo.getClubId(), tableInfo.getClubId())
                    && memberInfo.getTopProxyId().longValue() == userId.longValue()) {
                userGameConfig.setTopProxy(true);
                userGameConfig.setShowDisband(true);
            }
            if (Objects.equals(memberInfo.getClubId(), tableInfo.getClubId())
                    && tableInfo.getHolderId().longValue() == userId.longValue()) {
                userGameConfig.setShowDisband(true);
            }
        }
        if (userGameConfig.getTopProxy() || userGameConfig.getShowDisband()) {
            userGameConfig.setForceKick(true);
            userGameConfig.setForceStand(true);
            userGameConfig.setAllowedEnterRoom(true);
        }
    }

    private void assembleButtonDataPrivate(EnterRoomContextV2 context, BaseTableInfo tableInfo, UserGameConfig userGameConfig) {
        Long userId = context.getUserBaseInfo().getUserId();
        Long tableId = context.getTableId();
        UserBaseInfo memberInfo = context.getUserBaseInfo();

        BaseUserItem newUser = BaseTableUserCache.getUser(tableId, userId);
        userGameConfig.setStageId(newUser.getStageId());
        userGameConfig.setBusinessModel(memberInfo.getBusinessModel());
        userGameConfig.setHolderId(tableInfo.getHolderId());

        if (Objects.equals(CommonConstant.ONE, memberInfo.getProxyEntryAuthority())) {
            if (Objects.equals(memberInfo.getClubId(), tableInfo.getClubId())
                    && memberInfo.getTopProxyId().longValue() == userId.longValue()) {
                userGameConfig.setTopProxy(true);
            }
        }
        if (tableInfo.getHolderId().longValue() == userId.longValue()) {
            userGameConfig.setShowStart(true);
            userGameConfig.setShowDisband(true);
        }
        if (userGameConfig.getShowDisband()) {
            userGameConfig.setForceKick(true);
            userGameConfig.setForceStand(true);
            userGameConfig.setAllowedEnterRoom(true);
        }
        userGameConfig.setTouristFlag(memberInfo.getTouristFlag());
        userGameConfig.setTouristType(memberInfo.getTouristType());
    }

    private void assembleUserList(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId = context.getUserBaseInfo().getUserId();
        List<UserItemDto> userList = context.getEnterRoomRespDtoV2().getTableUserList();
        List<BaseUserItem> tableUsers = BaseTableUserCache.fetchTableUsers(tableId, TableUserCacheEnum.PLAYER_USER);
        userList.addAll(buildUserItemDtoList(tableId, userId, tableUsers));
    }

    private List<UserItemDto> buildUserItemDtoList(Long tableId, Long userId, List<BaseUserItem> userItemList) {
        if (CollectionUtils.isEmpty(userItemList)) {
            return new ArrayList<>();
        }
        Set<Long> remarkUserIds = userItemList.stream().distinct().map(BaseUserItem::getUserId).collect(Collectors.toSet());
        Map<Long, UserFriendRemarkDto> friendRemarkMap = UserFriendCache.getFriendRemarkCache(userId, remarkUserIds);
        List<UserItemDto> userList = BaseTableConvert.INSTANCE.userItemListToUserItemDtoList(userItemList);
        userList.forEach(u -> {
            UserBaseInfo userBaseInfo = UserBaseInfoCache.getUserBaseInfo(u.getUserId());
            BeanUtils.copyProperties(userBaseInfo, u);
            if (!userId.equals(u.getUserId())) {
                u.setUserNameRemark(friendRemarkMap.getOrDefault(u.getUserId(), new UserFriendRemarkDto()).getUserNameRemark());
                u.setUserRemark(friendRemarkMap.getOrDefault(u.getUserId(), new UserFriendRemarkDto()).getUserRemark());
            }
            UserTableItem userTableItem = UserTableItemCache.getUserTableItem(tableId, u.getUserId());
            u.setOnlineStatus(userTableItem.getOnlineStatus());
            u.setFirstSitDown(userTableItem.isFirstSitDown());
            u.setChipScore(TableUserWalletCache.getChipScore(tableId, u.getUserId()));
            GameUserBootStrapService.fillUserItem(tableId, u);
        });
        BaseAnonymousService.batchGetAnonymousName(tableId, userList);
        return userList;
    }

    private void assembleHand(EnterRoomContextV2 context) {
        if (handAssembler != null) {
            handAssembler.assembleHand(context);
        } else {
            // frame 默认：使用 GameUserHandBootstrapService 静态代理
            Long tableId = context.getTableId();
            Long userId = context.getUserBaseInfo().getUserId();
            BaseTableHandDto handDto = GameUserHandBootstrapService.buildTableHandInfo(tableId, userId);
            context.getEnterRoomRespDtoV2().setTableHandDto(handDto);
            Map<Integer, BaseTableUserHandDto> userHandMap = GameUserHandBootstrapService.buildTableUserHand(tableId, userId);
            context.getEnterRoomRespDtoV2().setTableUserHandMap(userHandMap);
        }
    }

    private void assembleTableInfo(EnterRoomContextV2 context) {
        context.getEnterRoomRespDtoV2().setTableInfoDto(
                GameUserHandBootstrapService.buildTableInfo(context.getTableId()));
    }

    private void assembleUserConfig(EnterRoomContextV2 context) {
        Long userId = context.getRequest().getUserId();
        UserConfig userConfig = UserConfigCache.getUserCfgCache(userId);
        if (userConfig == null) {
            log.warn("查询玩家配置失败 userId:{}", userId);
            return;
        }
        UserConfigQueryRespDto respDto = new UserConfigQueryRespDto();
        BeanUtils.copyProperties(userConfig, respDto);
        baseAnonymousService.checkButton(respDto, context.getTableId());
        respDto.setUserId(userId);
        context.getEnterRoomRespDtoV2().setUserConfigQueryResp(respDto);
    }
}
```

- [ ] **Step 2: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "feat(R-06): 新增 EnterRoomSnapshotAssembler，含 R-02 wallet 空值保护"
```

---

## Task 9：创建 EnterRoomFlowService（frame）

**Files:**
- Create: `FRAME_SVC/biz/enterroom/EnterRoomFlowService.java`

- [ ] **Step 1: 创建文件**

```java
package com.dx.game.frame.service.biz.enterroom;

import com.dx.game.frame.model.cache.UserRiskCache;
import com.dx.game.frame.model.context.EnterRoomContextV2;
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;

/**
 * 进入房间编排服务：状态写入 → 快照组装 → 风控初始化。
 * 不包含校验（校验由 EnterRoomValidatorChain 在 check() 中完成）。
 */
@Slf4j
@Component
public class EnterRoomFlowService {

    @Resource
    private EnterRoomStateService      stateService;
    @Resource
    private EnterRoomSnapshotAssembler snapshotAssembler;

    public void execute(EnterRoomContextV2 context) {
        stateService.applyState(context);
        snapshotAssembler.assemble(context);
        UserRiskCache.initRiskDataEnterRoom(context.getRequest());
    }
}
```

- [ ] **Step 2: 修改 EnterBaseTableHandlerDefault.handleData() 委托 FlowService**

在 `EnterBaseTableHandlerDefault` 中新增 @Resource：
```java
@Resource
EnterRoomFlowService enterRoomFlowService;
```

将 `handleData()` 方法体替换为：
```java
public void handleData(EnterRoomContextV2 context) {
    enterRoomFlowService.execute(context);
    log.info("进入房间成功 tableId:{} userId:{}",
            context.getTableId(), context.getRequest().getUserId());
    after(context);
}
```

> 原有的 `buildEnterRoomUserInfo`、`buildUserData`、`buildTableHandData`、`buildTableInfoData`、`buildUserConfig` 方法保留为 `@Deprecated protected` 方法，供子类兼容调用（标注 `@Deprecated` 即可，不删除）。

- [ ] **Step 3: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "feat(R-04): 新增 EnterRoomFlowService，handleData 委托 Flow 编排"
```

---

## Task 10：创建 guandan 三个扩展实现

**Files:**
- Create: `GD_SVC/bootstrap/enterroom/GdReconnectStateService.java`
- Create: `GD_SVC/bootstrap/enterroom/GdEnterRoomHandAssembler.java`
- Create: `GD_SVC/bootstrap/enterroom/GdEnterRoomValidationExtension.java`

- [ ] **Step 1: 创建 GdReconnectStateService.java**

```java
package com.dx.game.guandan.service.bootstrap.enterroom;

import com.dx.game.frame.model.context.EnterRoomContextV2;
import com.dx.game.frame.service.biz.enterroom.IReconnectStateHandler;
import com.dx.game.guandan.service.bootstrap.GdGameUserBootstrap;
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;

/**
 * 掼蛋重连状态恢复：取消托管、清理预退出/预站起标记。
 */
@Slf4j
@Component
public class GdReconnectStateService implements IReconnectStateHandler {

    @Resource
    private GdGameUserBootstrap gdGameUserBootstrap;

    @Override
    public void recover(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId = context.getRequest().getUserId();
        log.info("掼蛋重连状态恢复 tableId:{} userId:{}", tableId, userId);
        gdGameUserBootstrap.restartLoadHand(tableId, userId);
    }
}
```

- [ ] **Step 2: 创建 GdEnterRoomHandAssembler.java**

```java
package com.dx.game.guandan.service.bootstrap.enterroom;

import com.dx.game.frame.model.cache.BaseTableHand;
import com.dx.game.frame.model.context.EnterRoomContextV2;
import com.dx.game.frame.model.dto.base.BaseTableHandDto;
import com.dx.game.frame.model.dto.base.BaseTableUserHandDto;
import com.dx.game.frame.repository.local.cache.BaseTableHandCache;
import com.dx.game.frame.service.biz.enterroom.IEnterRoomHandAssembler;
import com.dx.game.guandan.service.bootstrap.TableUserHandBootstrap;
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;
import java.util.Map;

/**
 * 掼蛋手牌/贡还贡/转蛋/结算重连快照组装。
 * 含 R-02 tableHand 空值保护。
 */
@Slf4j
@Component
public class GdEnterRoomHandAssembler implements IEnterRoomHandAssembler {

    @Resource
    private TableUserHandBootstrap tableUserHandBootstrap;

    @Override
    public void assembleHand(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId = context.getRequest().getUserId();

        // R-02: tableHand 空值保护
        BaseTableHand tableHand = BaseTableHandCache.getTableHand(tableId);
        if (tableHand == null) {
            log.warn("assembleHand-tableHand缓存为空，跳过手牌组装 tableId:{} userId:{}", tableId, userId);
            return;
        }

        BaseTableHandDto handDto = tableUserHandBootstrap.buildTableHandInfo(tableId, userId);
        context.getEnterRoomRespDtoV2().setTableHandDto(handDto);

        Map<Integer, BaseTableUserHandDto> userHandMap = tableUserHandBootstrap.buildTableUserHand(tableId, userId);
        context.getEnterRoomRespDtoV2().setTableUserHandMap(userHandMap);
        log.debug("assembleHand 完成 tableId:{} userId:{}", tableId, userId);
    }
}
```

- [ ] **Step 3: 创建 GdEnterRoomValidationExtension.java**

```java
package com.dx.game.guandan.service.bootstrap.enterroom;

import com.dx.game.frame.constant.constant.CommonConstant;
import com.dx.game.frame.constant.enums.BusinessExceptionTypeEnums;
import com.dx.game.frame.constant.exception.BusinessException;
import com.dx.game.frame.model.cache.BaseTableInfo;
import com.dx.game.frame.model.cache.UserBaseInfo;
import com.dx.game.frame.model.context.EnterRoomContextV2;
import com.dx.game.frame.repository.local.cache.BaseTableInfoCache;
import com.dx.game.frame.repository.local.cache.UserBaseInfoCache;
import com.dx.game.frame.service.biz.enterroom.IEnterRoomValidationExtension;
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Component;

import java.util.Objects;

/**
 * 掼蛋进入房间校验扩展：俱乐部掼蛋游戏开关（ClubGuandanGameSwitch）。
 * 私人房路径不调用（by supports 逻辑内置到 validate 中判断）。
 */
@Slf4j
@Component
public class GdEnterRoomValidationExtension implements IEnterRoomValidationExtension {

    @Override
    public void validate(EnterRoomContextV2 context) {
        Long tableId = context.getTableId();
        Long userId = context.getRequest().getUserId();
        Boolean alreadyInRoom = context.getAlreadyInRoom();

        if (alreadyInRoom) {
            return;
        }

        BaseTableInfo tableInfo = BaseTableInfoCache.getTableInfo(tableId);
        if (!tableInfo.isClubTable()) {
            // 仅俱乐部桌需要掼蛋开关校验
            return;
        }

        UserBaseInfo userBaseInfo = UserBaseInfoCache.getUserBaseInfo(userId);
        if (Objects.equals(CommonConstant.ONE, userBaseInfo.getClubGuandanGameSwitch())) {
            log.warn("玩家账号被禁止入局俱乐部掼蛋游戏 userId:{} ClubGuandanGameSwitch:{}",
                    userId, userBaseInfo.getClubGuandanGameSwitch());
            throw BusinessException.createException(BusinessExceptionTypeEnums.USER_JOIN_GAME_LOCK_STATUS);
        }
    }
}
```

- [ ] **Step 4: Commit**

```bash
git -C dx-game-guandan add -A && git -C dx-game-guandan commit -m "feat: 新增 Gd 三个进入房间扩展实现（Reconnect/HandAssembler/ValidatorContributor）"
```

---

## Task 11：R-08 后置事件拆分

**Files:**
- Modify: `FRAME_SVC/biz/bootstrap/command/enterRoom/EnterBaseTableHandlerDefault.java`（after() 方法）
- Modify: `FRAME_SVC/listener/BaseUserEnterRoomFinishListener.java`

- [ ] **Step 1: 在 EnterBaseTableHandlerDefault 注入新依赖**

```java
@Resource
BaseUserTrackService baseUserTrackService;

@Resource
TableUserWalletCache tableUserWalletCache;   // 如果是静态调用则不需要注入
```

> 注：`TableUserWalletCache` 使用静态方法，不需要注入；`UserBringOutBootstrapService` 也是静态调用。

- [ ] **Step 2: 替换 after() 方法**

将整个 `after()` 方法替换为：

```java
protected void after(EnterRoomContextV2 context) {
    Long tableId = context.getTableId();
    Long userId = context.getUserBaseInfo().getUserId();
    BaseTableHand tableHand = BaseTableHandCache.getTableHand(context.getTableId());
    EnterRoomRespDtoV2 enterRoomResp = context.getEnterRoomRespDtoV2();

    // R-08: 异常带出直接同步调用（仅新用户，重连跳过），不可静默丢失
    if (!context.getAlreadyInRoom()) {
        baseUserTrackService.pushTableEntryExitRecord(userId, tableId,
                UserEntryExitTypeEnums.ENTER_ROOM, UserEntryExitReasonEnums.DEFAULT,
                KickerReasonEnum.DEFAULT.getDescribe());
        TableUserWallet wallet = TableUserWalletCache.getWallet(tableId, userId, WalletConstant.walletType);
        if (wallet != null && !BaseTableUserCache.hasQuitUser(tableId, userId)
                && wallet.getBalance().compareTo(BigDecimal.ZERO) > 0) {
            log.info("进入房间-处理异常未带出筹码 tableId:{} userId:{}", tableId, userId);
            UserBringOutBootstrapService.bringOutByQuit(tableId, userId);
        }
    }

    // 轨迹/活动事件（可失败，监听器内 catch 打日志）
    applicationEventPublisher.publishEvent(
            new UserEnterRoomFinishEventV2(context, tableHand != null ? tableHand.getHandCode() : null));

    log.info("进入房间-响应发送 tableId:{} userId:{}", tableId, userId);
    NetResponseBody netResponseBody = NetResponseBuilder.buildResponse(
            CommonProto.ENTER_ROOM, NoticeEncryptUtils.encrypt(enterRoomResp, tableId, userId), context.getRequest());
    SendUtil.send(netResponseBody);

    baseUserOnlineService.clearOfflineStartTime(tableId, userId);

    BaseTableInfo tableInfo = BaseTableInfoCache.getTableInfo(tableId);
    if (tableInfo.isPrivateTable()) {
        retryPrivateTableRedisService.joinPrivateTable(userId, tableId);
    }
    enterRoomNotice.sendNotice(tableId, userId, context.getAlreadyInRoom());
}
```

需要新增 import：
```java
import com.dx.facade.enums.UserEntryExitReasonEnums;
import com.dx.facade.enums.UserEntryExitTypeEnums;
import com.dx.game.frame.constant.enums.userspecify.KickerReasonEnum;
import com.dx.game.frame.service.biz.base.BaseUserTrackService;
import com.dx.game.frame.service.biz.bootstrap.UserBringOutBootstrapService;
import java.math.BigDecimal;
```

- [ ] **Step 3: 修改 BaseUserEnterRoomFinishListener，移除异常带出分支**

将 `onEvent()` 方法替换为（只保留轨迹和活动，移除 `if (!context.getAlreadyInRoom())` 分支）：

```java
@EventListener
public void onEvent(UserEnterRoomFinishEventV2 event) {
    EnterRoomContextV2 context = (EnterRoomContextV2) event.getSource();
    try {
        Long userId = context.getRequest().getUserId();
        Long tableId = context.getRequest().getTableId();
        BaseTableHand tableHand = BaseTableHandCache.getTableHand(tableId);
        BaseUserItem userItem = BaseTableUserCache.getUser(tableId, userId);

        userTrackService.push(userId, tableId, TrackTypeEnum.ENTER_ROOM);
        memberActivityPushService.userOprSendMessage(tableHand, userItem, UserActionEnum.ENTERED_ROOM);

        log.info("进入房间完成事件处理完毕 tableId:{} userId:{} handCode:{}", tableId, userId, event.getHandCode());
    } catch (Exception e) {
        log.error("进入房间完成事件处理异常 tableId:{} userId:{}", 
                context.getRequest().getTableId(), context.getRequest().getUserId(), e);
    }
}
```

- [ ] **Step 4: Commit**

```bash
git -C dx-game-frame add -A && git -C dx-game-frame commit -m "feat(R-08): 异常带出从事件监听剥离，after()直接同步调用"
```

---

## Task 12：自检与推送

- [ ] **Step 1: 确认无编译错误（grep 关键符号）**

```bash
# 确认旧字段引用已全部替换
grep -rn "getIsNewRoomUser\|isNewRoomUser" \
  dx-game-frame/dx-game-frame-service/src/main/java/ \
  dx-game-guandan/dx-game-guandan-service/src/main/java/ \
  --include="*.java"
# 预期：0 行

# 确认新接口都有实现类
grep -rn "implements IEnterRoomValidationExtension\|implements IEnterRoomHandAssembler\|implements IReconnectStateHandler" \
  dx-game-guandan/dx-game-guandan-service/src/main/java/ --include="*.java"
# 预期：3 行，各一个实现
```

- [ ] **Step 2: 确认 R-01 fix 生效**

```bash
grep -n "incrementAndGet\|enterRoomUserCount" \
  dx-game-frame/dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/base/BaseTableCheckService.java
# 预期：checkPrivateTableUserUpperLimit 中不再有 incrementAndGet
```

- [ ] **Step 3: 推送两个工程到远程**

```bash
TOKEN="[REDACTED_GITLAB_TOKEN]"

git -C dx-game-frame push \
  "https://junk:${TOKEN}@gitlab.ak12.cc/dx-b-server/dx-game-frame.git" \
  20260615/junk

git -C dx-game-guandan push \
  "https://junk:${TOKEN}@gitlab.ak12.cc/dx-b-server/dx-game-guandan.git" \
  20260615/junk
```

---

## 验收检查清单

- [ ] 私人房重复进房：WATCH_USER 只出现一次，人数上限不多增
- [ ] 重连场景：tableHand、raceGlobalConfig 为空时不抛系统异常
- [ ] 进房成功日志：只有两条 info（开始、成功），无 GsonUtils.toJson 大对象输出
- [ ] 异常带出：新用户进房后若有未带出筹码，同步执行 bringOutByQuit，有明确日志
- [ ] 并发进房：表级锁保证同桌同时进房的用户按序写入 WATCH_USER
