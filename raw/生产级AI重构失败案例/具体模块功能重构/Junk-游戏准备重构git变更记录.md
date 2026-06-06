# Junk-游戏准备重构 git 变更记录

> 本文档用于记录 `Junk-游戏准备重构` 范围内的每次 git 变更。每条记录必须可追溯、可审核、可回退。

## 一、记录目标

- 可追溯：能从任务、文档、分支、commit 追到具体改动。
- 可审核：能看到变更范围、核心改动、验证结果和审核状态。
- 可回退：能明确知道如何撤回本次变更，以及回退会影响哪些功能。

## 二、填写时机

- 代码变更提交前：先补充 `待提交` 记录，明确任务、范围、验证和回退方案。
- 代码变更提交后：补充 commit hash、MR 地址、审核状态和最终验证结果。
- 代码变更被回退后：追加回退记录，不直接删除原记录。
- 发现未知问题后：更新对应记录的 `未知问题`，并在后续记录中闭环。

## 三、变更记录索引

| 记录编号 | 日期 | 任务序号 / 功能 | git 分支 | commit / MR | 审核状态 | 回退状态 |
|---|---|---|---|---|---|---|
| GIT-20260603-001 | 2026-06-03 | 1-21 / 游戏准备全量扫描 | 20260615/junk | `186a4093ea08937cae002139c5d4b112e588efa3` | 未审核 | 未回退 |
| GIT-20260603-002 | 2026-06-03 | 3-21 / 游戏准备扫描重做 | 20260615/junk | `69025f57c8a537833018bf0cf117df850e9067c2` | 未审核 | 未回退 |
| GIT-20260603-003 | 2026-06-03 | 1 / 进入房间 | 20260615/junk | `f4ae71bea2f4a07b34eb33111e58b966392666ba` | 未审核 | 未回退 |
| GIT-20260603-004 | 2026-06-03 | 1 / 进入房间 | 20260615/junk | `2bb60c536fd2535b162558664d404f9328cea7d1` | 未审核 | 未回退 |
| GIT-20260603-005 | 2026-06-03 | 1 / 进入房间 | 20260615/junk | `64dad4554de1df0f100904a77cddee2aff04c8a7` | 未审核 | 未回退 |
| GIT-20260603-006 | 2026-06-03 | 1 / 进入房间 | 20260615/junk | `70a5f3c4f110f16830f63151b23bfd2643078c46` | 未审核 | 未回退 |
| GIT-20260603-007 | 2026-06-03 | 1 / 进入房间 | 20260615/junk | `de3c0db7ecc2dce21c298d0ff95daa1e1cb54104` | 未审核 | 未回退 |
| GIT-20260603-008 | 2026-06-03 | 1 / 进入房间 | 20260615/junk | `b12b3d607cf4df6758a81f587c698350258cb425` | 未审核 | 未回退 |
| GIT-20260604-001 | 2026-06-04 | 2 / 入座 | 20260615/junk | `2f24178549fce14f552d8decfcc7667d19cab91e` | 未审核 | 未回退 |
| GIT-20260604-002 | 2026-06-04 | 2 / 入座 | 20260615/junk | `30945906162519627ec4c3ef100ff86a460e68e8` | 未审核 | 未回退 |
| GIT-20260604-003 | 2026-06-04 | 2 / 入座 | 20260615/junk | `da6e9dfad370118e6da12eb105394c47e54614d4` | 未审核 | 未回退 |
| GIT-20260604-004 | 2026-06-04 | 18、21 / 预站起留座离桌、用户配置查询修改 | 20260615/junk | `fa43de8369b2daf620faaf8f08292fba2dddd2bb` | 未审核 | 未回退 |
| GIT-20260604-005 | 2026-06-04 | 19、20 / 风控数据上报、好友备注 | 20260615/junk | `8668585005a9b69b8f766491c90821f8adc6669c` | 未审核 | 未回退 |
| GIT-20260604-006 | 2026-06-04 | 2 / 入座 | 20260615/junk | `8b5a0f57ea169a35e8b471e254c931187efb31d7` | 未审核 | 未回退 |
| GIT-20260604-007 | 2026-06-04 | 总入口 / 指导与记录 | 20260615/junk | `ba463fa46a4f33570ecc1c343c152d9843010250` | 未审核 | 未回退 |
| GIT-20260604-008 | 2026-06-04 | 总入口 / 指导与记录 | 20260615/junk | `000a355e5685bb53050e31098e939a54784b5f3c` | 未审核 | 未回退 |
| GIT-20260604-009 | 2026-06-04 | 19 / 风控数据上报 | dx-game-frame 20260615/junk | `0483c93e8cd3b7764c22ab14a81b976ea4f8aea9` | 未审核 | 未回退 |
| GIT-20260604-010 | 2026-06-04 | 19 / 风控数据上报 | dx-game-frame 20260615/junk | `f78ef4e4203dc6c3bffcc4dfd535dd02fd6acbf6` | 未审核 | 未回退 |
| GIT-20260604-011 | 2026-06-04 | 19 / 风控数据上报 | dx-game-frame 20260615/junk | `2d745acd95dfac7502ce8534b28feaafc2e086a2` | 未审核 | 未回退 |
| GIT-20260604-012 | 2026-06-04 | 19 / 风控数据上报 | dx-game-frame 20260615/junk | `6ac8c6ab9e4d2ee7f7773fb40fb283a4b032a6fd` | 未审核 | 未回退 |
| GIT-20260604-013 | 2026-06-04 | 8 / 风控 | dx-game-frame 20260615/junk | `f688d8c538895f5ee5eee3958e4a1406b5ba0a8a` | 未审核 | 未回退 |
| GIT-20260604-014 | 2026-06-04 | 8 / 风控 | dx-game-frame 20260615/junk | `1e5aa3c34c2930a717d1b83f49adefb039be7d87` | 未审核 | 未回退 |
| GIT-20260604-015 | 2026-06-04 | 8 / 风控 | dx-game-frame 20260615/junk | `026684b40411fa2c58e073a587ad74156dc282a6` | 未审核 | 未回退 |
| GIT-20260604-016 | 2026-06-04 | 8 / 风控 | dx-game-frame 20260615/junk | `5c3ce0d2f0f1a966f3d0e55d0de7b20eeeef2ed3` | 未审核 | 未回退 |
| GIT-20260604-017 | 2026-06-04 | 4 / 站起 | dx-game-frame 20260615/junk | `726710eacb342c44eb98196a827013084f796332` | 未审核 | 未回退 |
| GIT-20260604-018 | 2026-06-04 | 4 / 站起 | dx-game-frame 20260615/junk | `12045248dcd3f65839a16862fa93897ef87c986f` | 未审核 | 未回退 |
| GIT-20260604-019 | 2026-06-04 | 4 / 站起 | dx-game-frame 20260615/junk | `38e58122f600067f6aa50c94bfd49a61819961a1` | 未审核 | 未回退 |
| GIT-20260604-020 | 2026-06-04 | 6 / 退出 | dx-game-frame 20260615/junk | `f6c046554c84810c1263eca7e758489ba5bd4203` | 未审核 | 未回退 |
| GIT-20260604-021 | 2026-06-04 | 6 / 退出 | dx-game-frame 20260615/junk | `101409a0a4f5a241c2293dc7be74a54022d7ef46` | 未审核 | 未回退 |
| GIT-20260604-022 | 2026-06-04 | 6 / 退出 | dx-game-frame 20260615/junk | `8681ca4526de0118d7199b9d69c45e8c30ccf658` | 未审核 | 未回退 |
| GIT-20260604-023 | 2026-06-04 | 7 / 离开状态检查 | dx-game-frame 20260615/junk | `cc72065eeabb53051b637697c3f74a7d288cfaa5` | 未审核 | 未回退 |
| GIT-20260604-024 | 2026-06-04 | 7 / 离开状态检查 | dx-game-frame 20260615/junk | `a9c8efc5dada1c09d7c51b0e4a225bed65643a4a` | 未审核 | 未回退 |
| GIT-20260604-025 | 2026-06-04 | 7 / 离开状态检查 | dx-game-frame 20260615/junk | `e8e6c7a6132d2df709267186f27ebbe47f8ce12c` | 未审核 | 未回退 |
| GIT-20260604-026 | 2026-06-04 | 7 / 离开状态检查 | dx-game-frame 20260615/junk | `bc009d0fe9408cf1624a3d36cb6ce27d89ba928c` | 未审核 | 未回退 |
| GIT-20260604-027 | 2026-06-04 | 12 / 进入房间前校验 | dx-game-frame 20260615/junk | `d8443cab242cd2f08296201919fcf514d642477b` | 未审核 | 未回退 |
| GIT-20260604-028 | 2026-06-04 | 12 / 进入房间前校验 | dx-game-frame 20260615/junk | `e9b9c699378c528348f7d71fcc545886580fce3d` | 未审核 | 未回退 |
| GIT-20260604-029 | 2026-06-04 | 12 / 进入房间前校验 | dx-game-frame 20260615/junk | `904efde88a42991613b5dae07a78c036e5d22167` | 未审核 | 未回退 |
| GIT-20260604-030 | 2026-06-04 | 13 / 牌桌状态查询 | dx-game-frame 20260615/junk | `1a3f8ea2080cb7aadcd5042d79dd66816c07cd9d` | 未审核 | 未回退 |
| GIT-20260604-031 | 2026-06-04 | 13 / 牌桌状态查询 | dx-game-frame 20260615/junk | `d7829de7bbf9c07f9bcc01d7c49283f4631ea656` | 未审核 | 未回退 |
| GIT-20260604-032 | 2026-06-04 | 18 / 预站起留座离桌（与 20 混合 commit） | dx-game-frame 20260615/junk | `036cfd439d224c1a3e4a92823f4ecffe5df63f99` | 未审核 | 未回退 |
| GIT-20260604-033 | 2026-06-04 | 18 / 预站起留座离桌 | dx-game-frame 20260615/junk | `27a889dc6f0bf3843da6d17ca288fd9b19e31916` | 未审核 | 未回退 |
| GIT-20260604-034 | 2026-06-04 | 18 / 预站起留座离桌 | dx-game-frame 20260615/junk | `0e238679cf9454a3ebb9e4959cc78a7dd379cd21` | 未审核 | 未回退 |
| GIT-20260604-035 | 2026-06-04 | 18 / 预站起留座离桌 | dx-game-frame 20260615/junk | `877114fba991e432519563978c90aa870533b518` | 未审核 | 未回退 |
| GIT-20260604-036 | 2026-06-04 | 21 / 用户配置查询修改 | dx-game-frame 20260615/junk | `d385a35aff989dbfad1742cf25bf22fc151a4a5d` | 未审核 | 未回退 |
| GIT-20260604-037 | 2026-06-04 | 21 / 用户配置查询修改 | dx-game-frame 20260615/junk | `70006efe50873e9e605e56d60ed0d554e99004a8` | 未审核 | 未回退 |
| GIT-20260604-038 | 2026-06-04 | 20 / 好友备注（与 18 R-01 混合 commit） | dx-game-frame 20260615/junk | `036cfd439d224c1a3e4a92823f4ecffe5df63f99` | 未审核 | 未回退 |
| GIT-20260604-039 | 2026-06-04 | 20 / 好友备注 | dx-game-frame 20260615/junk | `3c2cc4355ef99f486787735edeb9874282957dfe` | 未审核 | 未回退 |
| GIT-20260604-040 | 2026-06-04 | 20 / 好友备注 | dx-game-frame 20260615/junk | `f5ade75227cef25ef1d1334e1506521e25e9c300` | 未审核 | 未回退 |
| GIT-20260604-041 | 2026-06-04 | 20 / 好友备注 | dx-game-frame 20260615/junk | `15624810b4bf66be38e865c8a6a918535ca5d482` | 未审核 | 未回退 |
| GIT-20260604-042 | 2026-06-04 | 20 / 好友备注 | dx-game-frame 20260615/junk | `6de0a6f3f4848c03d3c34245cfbf984ab0729857` | 未审核 | 未回退 |
| GIT-20260604-043 | 2026-06-04 | 20 / 好友备注 | dx-game-frame 20260615/junk | `cea312807c809975f15de0ba65a26a6469105d04` | 未审核 | 未回退 |
| GIT-20260604-044 | 2026-06-04 | 20 / 好友备注 | dx-game-frame 20260615/junk | `e50608bff69adb7b8d332eac111f34577448ae43` | 未审核 | 未回退 |
| GIT-20260604-045 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `ee320d64214f5a8ce841657060b497be8735ebf1` | 未审核 | 未回退 |
| GIT-20260604-046 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `5298ccaf6c9fd5657e5005c8ea5a7fce8585309e` | 未审核 | 未回退 |
| GIT-20260604-047 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `48fa28c1256104dd0ce7a3400974913a497947eb` | 未审核 | 未回退 |
| GIT-20260604-048 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `4195f89ba5c1a9d85fd767ecfba81c470aa23784` | 未审核 | 未回退 |
| GIT-20260604-049 | 2026-06-04 | 2 / 入座（重复登记，已并入 GIT-20260604-001） | dx-game-guandan 20260615/junk | `2f24178549fce14f552d8decfcc7667d19cab91e` | 未审核 | 未回退 |
| GIT-20260604-050 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `4b826a230fc5b32e195a6dbc7752b859429cefa4` | 未审核 | 未回退 |
| GIT-20260604-051 | 2026-06-04 | 2 / 入座（重复登记，已并入 GIT-20260604-003） | dx-game-guandan 20260615/junk | `da6e9dfad370118e6da12eb105394c47e54614d4` | 未审核 | 未回退 |
| GIT-20260604-052 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `8f8ba8d249f72fb7e97d0d1f74b126d47953bea5` | 未审核 | 未回退 |
| GIT-20260604-053 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `de520423e02e57c0f05517e0d3069f955d863241` | 未审核 | 未回退 |
| GIT-20260604-054 | 2026-06-04 | 2 / 入座 | dx-game-guandan 20260615/junk | `8b5a0f57ea169a35e8b471e254c931187efb31d7` | 未审核 | 未回退 |
| GIT-20260604-055 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `d5132f2122ec41df4aee5790b814b47aec278449` | 未审核 | 未回退 |
| GIT-20260604-056 | 2026-06-04 | 2 / 入座 | dx-game-frame 20260615/junk | `3d007014392ba20f51a2fdca42d062be4e662c5a` | 未审核 | 未回退 |
| GIT-20260604-057 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `b83e425e2c5dd03ad8976947c212be5b8555dd2e` | 未审核 | 未回退 |
| GIT-20260604-058 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `77e0a7e8ce6ec66c3a6e2291e4f2c5d12cc87ca1` | 未审核 | 未回退 |
| GIT-20260604-059 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `e3c8dd6664b741b6331a2820136c969b38cb50a1` | 未审核 | 未回退 |
| GIT-20260604-060 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `2ac8bcb0d56aed80e6a416b8ae5051e6fde021c2` | 未审核 | 未回退 |
| GIT-20260604-061 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `7d8999dd1f7a74d65e9202e787ce3d74bbdce0f7` | 未审核 | 未回退 |
| GIT-20260604-062 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `6556c6ccf608b961876eddd04440da8a7ad723e0` | 未审核 | 未回退 |
| GIT-20260604-063 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `d5902b225ff494c3a6612f7a29e15fcf28b7ba0c` | 未审核 | 未回退 |
| GIT-20260604-064 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `57f4d02a3b16ca1d11d14603f247d4b6047cd94c` | 未审核 | 未回退 |
| GIT-20260604-065 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `ba7fe6d43e69ea4a365ff65c9124c05f2ad151b7` | 未审核 | 未回退 |
| GIT-20260604-066 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `43a732700ed336c8212c8c0ae0618f04ec33862d` | 未审核 | 未回退 |
| GIT-20260604-067 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `4a98023b2404e94862e585a8a1587c53ba51c067` | 未审核 | 未回退 |
| GIT-20260604-068 | 2026-06-04 | 1 / 进入房间 | dx-game-frame 20260615/junk | `506f2952ae9f1fdb3910b7419b0fdf37498a2117` | 未审核 | 未回退 |

## 四、实际变更记录

### GIT-20260603-001：新增游戏准备 21 个功能扫描报告

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-001 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 1-21 / 游戏准备全量扫描 |
| 关联文档 | `01-进入房间.md` 至 `21-用户配置查询修改.md` |
| git 分支 | 20260615/junk |
| commit / MR | `186a4093ea08937cae002139c5d4b112e588efa3` |
| 变更范围 | `docs/Junk-游戏准备重构/01-进入房间.md` 至 `21-用户配置查询修改.md` |
| 核心变更 | 1. 新增或更新 21 个游戏准备功能扫描文档<br>2. 按功能拆分进入房间、入座、带入、站起、带出、退出、风控、账单、私人房、重连、配置等范围<br>3. 为后续重构设计和实现计划提供问题扫描入口 |
| 验证结果 | 文档变更，未运行代码测试；git 记录未体现额外文档审核结果 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 186a4093ea08937cae002139c5d4b112e588efa3`，或恢复上述 21 个扫描文档到提交前版本 |
| 回退影响 | 回退后 21 个功能扫描入口会恢复到提交前状态，后续设计文档的前置依据可能缺失 |
| 未知问题 | 扫描结论是否全部覆盖 `dx-game-guandan` 与 `dx-game-frame` 真实代码路径，仍需逐功能评审确认 |

### GIT-20260603-002：重做 3-21 号游戏准备扫描文档

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-002 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 3-21 / 游戏准备扫描重做 |
| 关联文档 | `03-带入.md` 至 `21-用户配置查询修改.md` |
| git 分支 | 20260615/junk |
| commit / MR | `69025f57c8a537833018bf0cf117df850e9067c2` |
| 变更范围 | `docs/Junk-游戏准备重构/03-带入.md` 至 `21-用户配置查询修改.md` |
| 核心变更 | 1. 重做带入到用户配置查询/修改共 19 个扫描文档<br>2. 覆盖资金、状态、风控、实时账单、私人房审核、重连、在线状态恢复等后续任务输入<br>3. 将非 01/02 的功能扫描重新归档到 Junk 游戏准备范围 |
| 验证结果 | 文档变更，未运行代码测试；git 记录未体现额外文档审核结果 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 69025f57c8a537833018bf0cf117df850e9067c2`，或恢复 03-21 号扫描文档到提交前版本 |
| 回退影响 | 回退后 03-21 号任务的扫描内容会恢复到旧版本，后续设计拆分依据可能变化 |
| 未知问题 | 重做后的扫描内容是否覆盖全部协议分支、异常分支和跨工程依赖，仍需逐项确认 |

### GIT-20260603-003：新增进入房间重构设计草案到 superpowers specs

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-003 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 1 / 进入房间 |
| 关联文档 | `docs/superpowers/specs/2026-06-03-enter-room-refactor-design.md` |
| git 分支 | 20260615/junk |
| commit / MR | `f4ae71bea2f4a07b34eb33111e58b966392666ba` |
| 变更范围 | `docs/superpowers/specs/2026-06-03-enter-room-refactor-design.md` |
| 核心变更 | 1. 新增进入房间 R-01 至 R-08 的重构设计草案<br>2. 将进入房间设计先落到 superpowers specs 路径<br>3. 为后续落地到 `docs/Junk-游戏准备重构` 提供设计来源 |
| 验证结果 | 文档变更，未运行代码测试；git 记录未体现额外文档审核结果 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert f4ae71bea2f4a07b34eb33111e58b966392666ba`，或删除该 specs 文档 |
| 回退影响 | 回退后 superpowers specs 中进入房间设计草案缺失，但不直接影响代码运行 |
| 未知问题 | specs 草案与最终 Junk 目录设计文档是否完全一致，需以后续落地文档为准 |

### GIT-20260603-004：进入房间重构设计落地到 Junk 目录

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-004 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 1 / 进入房间 |
| 关联文档 | `01-进入房间.md`<br>`01-进入房间-重构设计.md` |
| git 分支 | 20260615/junk |
| commit / MR | `2bb60c536fd2535b162558664d404f9328cea7d1` |
| 变更范围 | `docs/Junk-游戏准备重构/01-进入房间-重构设计.md` |
| 核心变更 | 1. 新增进入房间重构设计文档<br>2. 将 R-01 至 R-08 设计从草案路径落地到 Junk 任务目录<br>3. 明确进入房间后续实现计划的正式设计依据 |
| 验证结果 | 文档变更，未运行代码测试；git 记录未体现额外文档审核结果 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 2bb60c536fd2535b162558664d404f9328cea7d1`，或删除 `01-进入房间-重构设计.md` |
| 回退影响 | 回退后进入房间任务缺少正式设计产物，任务清单中的设计完成度需要同步调整 |
| 未知问题 | 设计文档中的 Frame/Guandan 职责边界是否已被实现完整遵循，需结合后续代码提交审核 |

### GIT-20260603-005：新增进入房间重构实现计划

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-005 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 1 / 进入房间 |
| 关联文档 | `01-进入房间.md`<br>`01-进入房间-重构设计.md`<br>`01-进入房间-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `64dad4554de1df0f100904a77cddee2aff04c8a7` |
| 变更范围 | `docs/Junk-游戏准备重构/01-进入房间-实现计划.md`<br>`docs/superpowers/plans/2026-06-03-enter-room-refactor.md` |
| 核心变更 | 1. 新增进入房间重构实现计划<br>2. 将 R-01 至 R-08 拆成可执行步骤<br>3. 同步新增 superpowers plans 路径下的执行计划 |
| 验证结果 | 文档变更，未运行代码测试；git 记录未体现额外计划审核结果 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 64dad4554de1df0f100904a77cddee2aff04c8a7`，或删除两个实现计划文档 |
| 回退影响 | 回退后进入房间缺少可执行计划，后续代码变更难以追溯到具体 R 项 |
| 未知问题 | 实现计划中的步骤是否全部被后续代码提交完成，需按代码提交逐条核对 |

### GIT-20260603-006：进入房间 R-02/R-03 空值保护与日志降级

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-006 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 1 / 进入房间 |
| 关联文档 | `01-进入房间.md`<br>`01-进入房间-重构设计.md`<br>`01-进入房间-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `70a5f3c4f110f16830f63151b23bfd2643078c46` |
| 变更范围 | `dx-game-guandan-service/src/main/java/com/dx/game/guandan/service/bootstrap/TableUserHandBootstrap.java` |
| 核心变更 | 1. 对 `raceGlobalConfig` 增加空值保护<br>2. 将手牌相关日志从高频输出降为 `debug`<br>3. 对应进入房间 R-02/R-03 的稳定性和日志膨胀治理 |
| 验证结果 | git 记录未体现编译、单测或协议回归结果；需要补充 `TableUserHandBootstrap` 相关回归 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 70a5f3c4f110f16830f63151b23bfd2643078c46`，或恢复 `TableUserHandBootstrap.java` 到提交前版本 |
| 回退影响 | 回退后 `raceGlobalConfig` 空值风险和手牌日志膨胀风险可能重新出现 |
| 未知问题 | 空值保护是否覆盖所有进入房间手牌初始化分支，日志降级是否影响排障能力，仍需验证 |

### GIT-20260603-007：新增 Guandan 进入房间三个扩展实现

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-007 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 1 / 进入房间 |
| 关联文档 | `01-进入房间.md`<br>`01-进入房间-重构设计.md`<br>`01-进入房间-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `de3c0db7ecc2dce21c298d0ff95daa1e1cb54104` |
| 变更范围 | `GdEnterRoomHandAssembler.java`<br>`GdEnterRoomValidatorContributor.java`<br>`GdReconnectStateService.java` |
| 核心变更 | 1. 新增 Guandan 进入房间手牌装配扩展<br>2. 新增 Guandan 进入房间校验扩展<br>3. 新增 Guandan 重连状态服务扩展 |
| 验证结果 | git 记录未体现编译、单测或协议回归结果；需补充进入房间、重连、手牌快照回归 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert de3c0db7ecc2dce21c298d0ff95daa1e1cb54104`，或删除新增三个扩展实现并恢复注入关系 |
| 回退影响 | 回退后 Guandan 侧无法通过新增扩展实现承接 Frame 进入房间重构链路 |
| 未知问题 | 三个扩展是否已被 Frame 侧正确调用、是否覆盖所有场景，仍需结合依赖工程和运行验证确认 |

### GIT-20260603-008：进入房间优化并重命名校验扩展

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260603-008 |
| 日期 | 2026-06-03 |
| 任务序号 / 功能 | 1 / 进入房间 |
| 关联文档 | `01-进入房间-重构设计.md`<br>`01-进入房间-实现计划.md`<br>`docs/superpowers/specs/2026-06-03-enter-room-refactor-design.md`<br>`docs/superpowers/plans/2026-06-03-enter-room-refactor.md` |
| git 分支 | 20260615/junk |
| commit / MR | `b12b3d607cf4df6758a81f587c698350258cb425` |
| 变更范围 | 进入房间设计/计划文档；`GdEnterRoomValidatorContributor.java` 重命名为 `GdEnterRoomValidationExtension.java` |
| 核心变更 | 1. 更新进入房间设计和实现计划文档<br>2. 同步更新 superpowers specs/plans 文档<br>3. 将 Guandan 进入房间校验扩展命名从 Contributor 调整为 ValidationExtension |
| 验证结果 | git 记录未体现编译、单测或协议回归结果；重命名类需要确认 Spring 注入和 Frame 侧引用是否一致 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert b12b3d607cf4df6758a81f587c698350258cb425`，或恢复文档和类名到提交前状态 |
| 回退影响 | 回退后进入房间设计/计划回到旧版本，校验扩展命名也回退为 Contributor |
| 未知问题 | 重命名是否与 Frame 侧接口命名完全匹配，需编译和启动验证 |

### GIT-20260604-001：新增 Guandan 入座校验扩展点

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-001 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 2 / 入座 |
| 关联文档 | `02-入座.md` |
| git 分支 | 20260615/junk |
| commit / MR | `2f24178549fce14f552d8decfcc7667d19cab91e` |
| 变更范围 | `dx-game-guandan-service/src/main/java/com/dx/game/guandan/service/bootstrap/sitdown/GdSitDownValidatorContributor.java` |
| 核心变更 | 1. 新增 Guandan 入座校验扩展点<br>2. 为 Frame 入座校验链提供 Guandan 侧业务校验接入<br>3. 支撑入座重构中校验职责从 Handler 拆出的设计方向 |
| 验证结果 | git 记录未体现编译、单测或协议回归结果；需补充入座协议和校验失败场景回归 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 2f24178549fce14f552d8decfcc7667d19cab91e`，或删除该扩展类并恢复旧校验路径 |
| 回退影响 | 回退后 Guandan 入座校验无法通过新增扩展点接入重构链路 |
| 未知问题 | 扩展点是否覆盖俱乐部、私人房、赛事等入座分支，仍需验证 |

### GIT-20260604-002：新增入座重构设计文档与实现计划

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-002 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 2 / 入座 |
| 关联文档 | `02-入座.md`<br>`02-入座-重构设计.md`<br>`02-入座-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `30945906162519627ec4c3ef100ff86a460e68e8` |
| 变更范围 | `docs/Junk-游戏准备重构/02-入座-重构设计.md`<br>`docs/Junk-游戏准备重构/02-入座-实现计划.md` |
| 核心变更 | 1. 新增入座重构设计文档<br>2. 新增入座 R-01 至 R-06 实现计划<br>3. 明确入座重构对进入房间校验链和表级锁框架的复用关系 |
| 验证结果 | 文档变更，未运行代码测试；git 记录未体现额外文档审核结果 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 30945906162519627ec4c3ef100ff86a460e68e8`，或删除两个入座产物文档 |
| 回退影响 | 回退后入座任务缺少正式设计和实现计划，任务清单完成度需要同步调整 |
| 未知问题 | 入座设计中复用进入房间框架的边界是否实际成立，需结合后续实现审核 |

### GIT-20260604-003：占座转入座调用点改走 SitDownStateService 表级锁

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-003 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 2 / 入座 |
| 关联文档 | `02-入座.md`<br>`02-入座-重构设计.md`<br>`02-入座-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `da6e9dfad370118e6da12eb105394c47e54614d4` |
| 变更范围 | `UserSitDownBootstrap.java`<br>`UserSitDownFinishListener.java` |
| 核心变更 | 1. 将占座转入座调用点改为走 `SitDownStateService`<br>2. 将关键状态迁移纳入表级锁路径<br>3. 降低 WATCH 到 PLAYER 迁移的并发风险 |
| 验证结果 | git 记录未体现编译、单测或协议回归结果；需补充占座转入座并发和通知链路回归 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert da6e9dfad370118e6da12eb105394c47e54614d4`，或恢复两个文件中的旧调用路径 |
| 回退影响 | 回退后占座转入座可能不再通过 `SitDownStateService` 表级锁保护，并发风险可能恢复 |
| 未知问题 | 表级锁路径是否覆盖全部占座转入座入口，以及 listener 顺序是否稳定，仍需验证 |

### GIT-20260604-004：预站起留座离桌与用户配置文档/代码补充

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-004 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 18、21 / 预站起留座离桌、用户配置查询修改 |
| 关联文档 | `18-预站起留座离桌.md`<br>`18-预站起留座离桌-重构设计.md`<br>`18-预站起留座离桌-实现计划.md`<br>`21-用户配置查询修改.md`<br>`21-用户配置查询修改-重构设计.md`<br>`21-用户配置查询修改-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `fa43de8369b2daf620faaf8f08292fba2dddd2bb` |
| 变更范围 | 新增 18、21 号设计/计划文档；修改 `GdUserConfigQueryCommand.java`、`GdUserConfigUpdateCommand.java` |
| 核心变更 | 1. 新增预站起/留座离桌重构设计和实现计划<br>2. 新增用户配置查询/修改重构设计和实现计划<br>3. 修改 Guandan 用户配置查询和更新命令 |
| 验证结果 | git 记录未体现编译、单测或协议回归结果；用户配置命令改动需补充 3018/3019 或相关协议回归 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert fa43de8369b2daf620faaf8f08292fba2dddd2bb`，或删除新增 18/21 文档并恢复两个命令类 |
| 回退影响 | 回退后 18/21 号任务缺少设计/计划产物，用户配置命令行为恢复到提交前 |
| 未知问题 | 此提交同时涉及两个任务和代码改动，用户配置命令的具体行为变化需要单独代码审核确认 |

### GIT-20260604-005：风控数据上报与好友备注设计/计划补充

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-005 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 19、20 / 风控数据上报、好友备注 |
| 关联文档 | `19-风控数据上报.md`<br>`19-风控数据上报-重构设计.md`<br>`19-风控数据上报-实现计划.md`<br>`20-好友备注.md`<br>`20-好友备注-重构设计.md`<br>`20-好友备注-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `8668585005a9b69b8f766491c90821f8adc6669c` |
| 变更范围 | `19-风控数据上报-重构设计.md`<br>`19-风控数据上报-实现计划.md`<br>`20-好友备注-重构设计.md`<br>`20-好友备注-实现计划.md` |
| 核心变更 | 1. 新增风控数据上报重构设计和实现计划<br>2. 新增好友备注重构设计和实现计划<br>3. 将两个独立任务的核心产物补齐到 Junk 目录 |
| 验证结果 | 文档变更，未运行代码测试；git 记录未体现额外文档审核结果 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 8668585005a9b69b8f766491c90821f8adc6669c`，或删除新增 19/20 设计和计划文档 |
| 回退影响 | 回退后 19/20 号任务缺少设计/计划产物，任务清单完成度需要同步调整 |
| 未知问题 | 两个任务的实现是否已经按设计落地，需后续代码提交和验证记录闭环 |

### GIT-20260604-006：新增 GdSitDownStateService 并调整占座转入座表级锁路径

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-006 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 2 / 入座 |
| 关联文档 | `02-入座.md`<br>`02-入座-重构设计.md`<br>`02-入座-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | `8b5a0f57ea169a35e8b471e254c931187efb31d7` |
| 变更范围 | `GdSitDownStateService.java`<br>`UserSitDownBootstrap.java`<br>`UserSitDownFinishListener.java` |
| 核心变更 | 1. 新增 Guandan 入座状态服务 `GdSitDownStateService`<br>2. 调整占座转入座调用点走 `IOccupyResitHandler` 表级锁路径<br>3. 更新入座完成监听链路中的状态迁移调用 |
| 验证结果 | git 记录未体现编译、单测或协议回归结果；需补充占座转入座、入座完成监听和并发场景回归 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 8b5a0f57ea169a35e8b471e254c931187efb31d7`，或删除 `GdSitDownStateService` 并恢复两个调用文件 |
| 回退影响 | 回退后入座状态迁移不再使用新增 Guandan 状态服务和 `IOccupyResitHandler` 表级锁路径 |
| 未知问题 | 此提交与 `da6e9dfad` 均修改占座转入座路径，二者关系和最终有效实现需要代码 diff 审核确认 |

### GIT-20260604-007：README 改名为指导文档并新增 git 变更记录文件

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-007 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 总入口 / 指导与记录 |
| 关联文档 | `Junk-游戏准备重构指导.md`<br>`Junk-游戏准备重构git变更记录.md` |
| git 分支 | 20260615/junk |
| commit / MR | `ba463fa46a4f33570ecc1c343c152d9843010250` |
| 变更范围 | 新增 `Junk-游戏准备重构指导.md`、`Junk-游戏准备重构git变更记录.md`；删除 `README.md` |
| 核心变更 | 1. 将原目录入口从 `README.md` 改为更明确的指导文档<br>2. 新增 git 变更记录文档<br>3. 为任务清单和变更追溯建立总入口 |
| 验证结果 | 文档变更，未运行代码测试；已通过 git 记录确认文件新增/删除范围 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert ba463fa46a4f33570ecc1c343c152d9843010250`，或恢复 `README.md` 并删除两个新文档 |
| 回退影响 | 回退后目录入口恢复为 README，git 变更记录入口会消失 |
| 未知问题 | 文档名称变更是否影响外部引用 README 的入口链接，需检查外部文档或索引 |

### GIT-20260604-008：补充指导文档和 git 变更记录维护要求

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-008 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 总入口 / 指导与记录 |
| 关联文档 | `Junk-游戏准备重构指导.md`<br>`Junk-游戏准备重构git变更记录.md` |
| git 分支 | 20260615/junk |
| commit / MR | `000a355e5685bb53050e31098e939a54784b5f3c` |
| 变更范围 | `Junk-游戏准备重构指导.md`<br>`Junk-游戏准备重构git变更记录.md` |
| 核心变更 | 1. 补充指导文档中的 git 变更记录章节<br>2. 补充 git 变更记录模板、索引和示例<br>3. 明确每次变更必须可追溯、可审核、可回退 |
| 验证结果 | 文档变更，未运行代码测试；已通过 git 记录确认两个文档被修改 |
| 审核状态 | 未审核 |
| 回退方式 | 执行 `git revert 000a355e5685bb53050e31098e939a54784b5f3c`，或恢复两个文档到提交前版本 |
| 回退影响 | 回退后 git 变更记录的格式要求和指导文档中的追溯要求会减少或消失 |
| 未知问题 | 2026-06-03 至 2026-06-04 的历史提交当时未按模板登记，本记录为后补，仍需人工确认审核状态 |

### GIT-20260604-009：风控数据上报 R-01 UserRiskCache 加入 table 维度

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-009 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 19 / 风控数据上报 |
| 关联文档 | `19-风控数据上报.md`<br>`19-风控数据上报-重构设计.md` §4 R-01<br>`19-风控数据上报-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `0483c93e8cd3b7764c22ab14a81b976ea4f8aea9` |
| 变更范围 | `dx-game-frame-repository/src/main/java/com/dx/game/frame/repository/local/cache/UserRiskCache.java` |
| 核心变更 | 1. `USER_RISK_DATA_CACHE` 内部 key 由 `Long userId` 升级为嵌套静态类 `RiskDataCacheKey(tableId, userId)`，消除跨桌 IP/GPS/设备数据串用 P0<br>2. `initRiskDataEnterRoom` / `refreshRiskData` / `getUserRiskData` 全部按 `(tableId, userId)` 读写；对外方法签名 100% 保持不变<br>3. `getUserRiskData` 增加 `tableInfo` 和 `gpsImposeSwitch` 空值保护，GPS 超时刷新不再 NPE<br>4. `getTableRiskData` / `getGpsRiskData` / `getIPRiskData` 含 IP/GPS payload 的 info 日志降级为 debug |
| 验证结果 | 未验证：仅完成代码改造；尚未跑单测、跨桌冒烟和 1040/1041 协议回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 0483c93e8cd3b7764c22ab14a81b976ea4f8aea9`，或将 `UserRiskCache.java` 恢复到提交前版本（key 退回 `Long`） |
| 回退影响 | 回退后 cache 复用回 userId 单维度，会重新出现跨桌串用 P0；08-风控/02-入座/04-站起 在切换桌场景下风险数据不准确 |
| 未知问题 | 旧 `Long` key 在 cache 中的残留条目通过 3h TTL 自然过期；过渡期是否存在读到旧 userId-only 条目导致行为差异，尚未做线上观测 |

### GIT-20260604-010：风控数据上报 R-02 抽出 RiskDataRedisSyncService 解耦 1040 与 Redis 同步

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-010 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 19 / 风控数据上报 |
| 关联文档 | `19-风控数据上报.md`<br>`19-风控数据上报-重构设计.md` §4 R-02<br>`19-风控数据上报-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `f78ef4e4203dc6c3bffcc4dfd535dd02fd6acbf6` |
| 变更范围 | 新增 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/risk/RiskDataRedisSyncService.java`<br>修改 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/risk/RiskDataCollectionCommandDefault.java`<br>修改 `dx-game-frame-cmd/src/main/java/com/dx/game/frame/cmd/command/riskdatacollection/RiskDataCollectionCommand.java` |
| 核心变更 | 1. 新增 `RiskDataRedisSyncService.syncSafely(tableId, userId, riskData)`，包含 `tableInfo` / `riskData` 空值短路 + try/catch 隔离<br>2. `RiskDataCollectionCommandDefault.handleCommand` 委托新服务，移除内部 `syncRiskDataToRedis` 私有方法<br>3. Redis 同步异常不再上抛主流程，仅 warn；1040 主响应与 Redis 同步彻底解耦<br>4. 1040 入口 info 日志收敛为 `tableId+userId` 元数据，req/resp toJson 全部降级 debug |
| 验证结果 | 未验证：仅完成代码改造；缺 mock `HallTableUserSeatRedisService.syncRiskData` 抛异常时主响应仍 200 的回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert f78ef4e4203dc6c3bffcc4dfd535dd02fd6acbf6`，或恢复 `RiskDataCollectionCommandDefault` 旧版本并删除 `RiskDataRedisSyncService` |
| 回退影响 | 回退后 Redis 同步异常会再次导致 1040 返回系统错误；客户端可能收到 SYSTEM_EXCEPTION 而本地 cache 已刷新，与服务端不一致 |
| 未知问题 | `RiskDataRedisSyncService` 内尚未接入指标埋点（注释里留有 TODO），线上 Redis 同步失败率目前只能从日志侧推断 |

### GIT-20260604-011：风控数据上报 R-04 UserRiskInfoDto 新增可选 riskTypeList

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-011 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 19 / 风控数据上报 |
| 关联文档 | `19-风控数据上报.md`<br>`19-风控数据上报-重构设计.md` §6 R-04<br>`19-风控数据上报-实现计划.md` Task 3 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `2d745acd95dfac7502ce8534b28feaafc2e086a2` |
| 变更范围 | `dx-game-frame-model/src/main/java/com/dx/game/frame/model/dto/riskdatagraph/UserRiskInfoDto.java` |
| 核心变更 | 1. `UserRiskInfoDto` 新增可选字段 `List<Integer> riskTypeList`，承载 `BaseTableRiskService.checkRiskData` 全规则用户级风险（设备/视频/GPS未开/GPS相近/IP相同）<br>2. 字段默认 `null`，老客户端 JSON 反序列化忽略，新客户端可在头像/座位上展示节点级风险<br>3. 1041 协议响应向后兼容；不删/不改任何已有字段 |
| 验证结果 | 未验证：仅完成 DTO 改造；尚未与客户端联调新字段，也未验证旧客户端忽略未知字段的反序列化行为 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 2d745acd95dfac7502ce8534b28feaafc2e086a2`，或删除 `UserRiskInfoDto.riskTypeList` 字段 |
| 回退影响 | 回退后 1041 响应只暴露旧 `riskGraphList`（IP/GPS 两两关系），客户端无法展示设备/视频等用户级风险节点；与 08-风控 实时通知展示不一致 |
| 未知问题 | 客户端是否已支持解析 `riskTypeList`、UI 渲染方案是否对齐，需要与客户端 / 产品确认 |

### GIT-20260604-012：风控数据上报 R-03/R-04 新增 RiskGraphAssembler 统一 1041 风险规则

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-012 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 19 / 风控数据上报 |
| 关联文档 | `19-风控数据上报.md`<br>`19-风控数据上报-重构设计.md` §4 R-03、§6 R-04<br>`19-风控数据上报-实现计划.md` Task 4 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `6ac8c6ab9e4d2ee7f7773fb40fb283a4b032a6fd` |
| 变更范围 | 新增 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/risk/RiskGraphAssembler.java`<br>修改 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/risk/RiskDataGraphCommandDefault.java`<br>修改 `dx-game-frame-cmd/src/main/java/com/dx/game/frame/cmd/command/riskdatagraph/RiskDataGraphCommand.java` |
| 核心变更 | 1. 新增 `RiskGraphAssembler.assemble(tableId, currentUserId)`：复用 `BaseTableRiskService.checkRiskData` 覆盖 IP/GPS/GPS未开/设备/视频 全 5 规则<br>2. 用户级风险类型写入 `UserRiskInfoDto.riskTypeList`，弥补旧 1041 只显示 IP/GPS 的覆盖缺口<br>3. pairwise 边构造 `buildPairwiseEdges` 对 latitude/longitude/gpsImposeSwitch/ipImposeSwitch/limitToLessThan 全部加空值短路，避免 GPS 缺失 NPE<br>4. `RiskDataGraphCommandDefault` 瘦身委托新装配器，删除内部 `getUserRiskGraph` / `isNearby` 私有方法<br>5. 1041 入口与处理层 info 日志收敛为 `tableId+userId+playerCount` 元数据；payload 全部降级 debug |
| 验证结果 | 未验证：仅完成代码改造；尚未跑 GPS 空值场景、非 iOS 设备风险展示、1041 协议字段回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 6ac8c6ab9e4d2ee7f7773fb40fb283a4b032a6fd`，或恢复 `RiskDataGraphCommandDefault` 旧版本并删除 `RiskGraphAssembler` |
| 回退影响 | 回退后 1041 重新走旧版本：GPS 空值可能 NPE 被吞导致空关系图；`riskTypeList` 不会写入，客户端无法看到设备/视频/GPS未开等用户级风险节点 |
| 未知问题 | 1041 复用 `BaseTableRiskService.checkRiskData` 是否在大牌桌（玩家数较多）下带来明显额外耗时，尚未做性能 benchmark；08-风控 重构后规则签名若变更需同步审视本依赖 |

### GIT-20260604-013：风控 R-01 新增 RiskCheckResult / RuleFailure DTO

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-013 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 8 / 风控 |
| 关联文档 | `08-风控.md`<br>`08-风控-重构设计.md` §4 R-01<br>`08-风控-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `f688d8c538895f5ee5eee3958e4a1406b5ba0a8a` |
| 变更范围 | 新增 `dx-game-frame-model/src/main/java/com/dx/game/frame/model/dto/risk/RiskCheckResult.java`<br>新增 `dx-game-frame-model/src/main/java/com/dx/game/frame/model/dto/risk/RuleFailure.java` |
| 核心变更 | 1. 新增 `RiskCheckResult { riskMap, success, failedRules }`：承载一次风控规则计算的完整结果<br>2. 新增 `RuleFailure { rule, message }`：单条规则失败记录，不带 throwable 避免日志膨胀<br>3. 提供静态工厂 `empty()`、判定方法 `hasRisk() / hasFailure()` |
| 验证结果 | 未验证：仅新增 DTO；后续随 BaseTableRiskService 改造一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert f688d8c538895f5ee5eee3958e4a1406b5ba0a8a` 或删除两个新文件 |
| 回退影响 | 单独回退此提交会导致后续 GIT-20260604-016 编译失败；需同时回退 016 |
| 未知问题 | 是否需要带入 stackTrace 字段帮助排障？本期取舍偏简洁，待运营反馈 |

### GIT-20260604-014：风控 R-02 新增 RiskTableSnapshot 纯 DTO

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-014 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 8 / 风控 |
| 关联文档 | `08-风控.md`<br>`08-风控-重构设计.md` §4 R-02<br>`08-风控-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `1e5aa3c34c2930a717d1b83f49adefb039be7d87` |
| 变更范围 | 新增 `dx-game-frame-model/src/main/java/com/dx/game/frame/model/dto/risk/RiskTableSnapshot.java` |
| 核心变更 | 1. 新增 `RiskTableSnapshot` 纯 DTO，承载风控实时检测一次执行的快照<br>2. 字段：`tableId / tableInfo / riskData / playerUserIds / activePlayerUserIds / allUserIds / handStarted / capturedAt`<br>3. 用 `@Builder` 暴露构造；装配逻辑放在 service 层避免 model → repository 反向依赖 |
| 验证结果 | 未验证：仅新增 DTO；后续随 BaseTableRiskService 改造一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 1e5aa3c34c2930a717d1b83f49adefb039be7d87` 或删除该文件 |
| 回退影响 | 单独回退会导致 GIT-20260604-016 中 `captureSnapshot/computeNeedStandUserIds/sendCheckRiskNotice` 编译失败；需同时回退 016 |
| 未知问题 | snapshot 内 riskData 直接持有 cache 返回的 list 不深拷贝，依赖 TableLoopTask 单线程串行；后续如风控引入并发要重新评估 |

### GIT-20260604-015：风控 R-03 新增 RiskPolicyRegistry

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-015 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 8 / 风控 |
| 关联文档 | `08-风控.md`<br>`08-风控-重构设计.md` §4 R-03、§5.4<br>`08-风控-实现计划.md` Task 3 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `026684b40411fa2c58e073a587ad74156dc282a6` |
| 变更范围 | 新增 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/risk/RiskPolicyRegistry.java` |
| 核心变更 | 1. 新增 `RiskPolicyRegistry` Spring `@Component`<br>2. `getPriorityOrder()` 取代 `BaseTableRiskService.RISK_PRIORITY_ORDER` 私有常量<br>3. `getKickerReason(RiskTypeEnum)` 取代 `getRiskReason` 中 hardcode if-else<br>4. `getStandType(RiskTypeEnum)` 取代 `realtimeCheckRisk` 内 hardcode 三目<br>5. `getSeatError(RiskTypeEnum)` 暴露 SeatError 兜底查询 |
| 验证结果 | 未验证：仅新增类；后续随 BaseTableRiskService 改造一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 026684b40411fa2c58e073a587ad74156dc282a6` 或删除该文件 |
| 回退影响 | 单独回退会导致 GIT-20260604-016 中 `policy()` 调用编译失败；需同时回退 016 |
| 未知问题 | `REALTIME_VOICE_RISK` 是否纳入 `PRIORITY_ORDER` 尚未决策；当前保持改造前一致（不在列表内） |

### GIT-20260604-016：风控 R-01/R-02/R-03/R-04 BaseTableRiskService 重构

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-016 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 8 / 风控 |
| 关联文档 | `08-风控.md`<br>`08-风控-重构设计.md` §4 全部<br>`08-风控-实现计划.md` Task 4 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `5c3ce0d2f0f1a966f3d0e55d0de7b20eeeef2ed3` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/base/BaseTableRiskService.java` |
| 核心变更 | 1. **R-01**：新增 `checkRiskDataResult(tableId, riskData) → RiskCheckResult`；5 条规则各自 `safeRule` try/catch；旧 `checkRiskData` 标记 `@Deprecated` 并委托新方法；`checkRiskSitDown` 对 `result.success=false` 保守拦截抛 `TABLE_RISK_ERROR` —— 消除"风控异常被静默成无风险"的 P0 安全漏洞<br>2. **R-02**：`realtimeCheckRisk` 一次 `captureSnapshot()` 后全程基于 snapshot；`computeNeedStandUserIds / sendCheckRiskNotice` 改成接 snapshot 参数；二次确认仍基于 snapshot.riskData，避免"刚站起 → 重新拉 cache → 看到新上报"导致重复处理 —— 消除"风控计算/站起筛选/通知接收人不是同一时刻"的 P0<br>3. **R-03**：`RISK_PRIORITY_ORDER` 私有常量删除；`getUserRiskType / getRiskReason` 委托 `RiskPolicyRegistry`；方法签名 100% 保持兼容<br>4. **R-04**：IP/GPS/全 riskMap payload 日志全部降级 debug；info 只保留 `tableId / userId / riskTypeEnum / recipientCount / standCount / riskTypeCount` 元数据 |
| 验证结果 | 未验证：仅完成代码改造；尚未跑单测、规则失败注入冒烟、并发用户进出场景回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 5c3ce0d2f0f1a966f3d0e55d0de7b20eeeef2ed3`，或恢复 `BaseTableRiskService.java` 到 6ac8c6ab9 时的版本 |
| 回退影响 | 回退后风控异常重新静默为无风险（P0 重现）；`realtimeCheckRisk` 重新多次独立读 cache（快照不一致 P0 重现）；旧调用方 `RiskStandLeaveUserVisitor` / `GdUserCheckCommandBootstrap` / `GdUserLeaveBootstrapService` / `RiskGraphAssembler` 行为完全不变（旧 `checkRiskData` API 保留） |
| 未知问题 | 1) 入座规则失败保守拦截是否符合产品预期，08 §13 待确认；2) 实时检测二次确认是否要从 cache 重读 riskData，本期保持改造前"看同一份"的行为；3) `RiskActionPlanner` 统一动作规划本期未做，留给 04 站起 / 18 预站起 一起做 |

### GIT-20260604-017：站起 R-01 修正 UserStandCommandDefault 任务 event key

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-017 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 4 / 站起 |
| 关联文档 | `04-站起.md` §5 P0-2<br>`04-站起-重构设计.md` §4 R-01<br>`04-站起-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `726710eacb342c44eb98196a827013084f796332` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/user/UserStandCommandDefault.java` 一行 |
| 核心变更 | 1. `handle()` 中 `EventUtils.getKey(OnceEventTypeEnum.USER_QUIT_TASK, ...)` 改为 `OnceEventTypeEnum.USER_STAND_TASK`<br>2. `USER_STAND_TASK("TABLE_USER_STAND_%s_UID_%s", "玩家站起")` 枚举常量已存在但从未被使用<br>3. 消除"同一用户并发 1007/1006 时 event key 互相覆盖"P0 |
| 验证结果 | 未验证：仅完成代码改造；尚未通过 EventManager 实际并发场景冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 726710eacb342c44eb98196a827013084f796332`，或把第 87 行 enum 值改回 `USER_QUIT_TASK` |
| 回退影响 | 回退后站起任务与退出任务复用同一 event key prefix；并发场景重新出现 P0 互相覆盖 |
| 未知问题 | EventManager 内现有残留 `TABLE_USER_QUIT_...` 站起任务是否需要主动清理？目前选择不清理，等自然超时；如有 stuck 风险需要补操作 |

### GIT-20260604-018：站起 R-02 + R-03 UserStandNotice 钱包兜底 + 整理 imports + 日志收敛

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-018 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 4 / 站起 |
| 关联文档 | `04-站起.md` §5 P1-2、P2 日志<br>`04-站起-重构设计.md` §4 R-02、R-03<br>`04-站起-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `12045248dcd3f65839a16862fa93897ef87c986f` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/notice/UserStandNotice.java` 整体重写 |
| 核心变更 | 1. 新增 `safeFetchChipScore(tableId, userId) → BigDecimal`：`TableUserWalletCache.getChipScore` 抛任何异常时返回 `BigDecimal.ZERO` + warn 日志<br>2. `notice(...)` 中 `setChipScore` 改走兜底方法，站起主流程已完成不再被钱包缓存阻断<br>3. 整段 `context / userStandNoticeDto` toJson info 日志降级 debug；info 仅保留 tableId/userId/standType/kickerReason/chairId 元数据<br>4. 顺便整理被压在 1 行的 imports 为标准格式（不影响行为） |
| 验证结果 | 未验证：仅完成代码改造；尚未模拟钱包缺失场景的 1007/14007 回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 12045248dcd3f65839a16862fa93897ef87c986f`，或恢复 `UserStandNotice.java` 到提交前版本 |
| 回退影响 | 回退后 1007 链路对钱包缓存缺失再次敏感（站起主流程成功但 14007 不发送）；info 日志重新含敏感 payload；imports 退回 1 行格式 |
| 未知问题 | 兜底返回 `BigDecimal.ZERO` 是否符合客户端展示预期？04 §13 待确认项："`UserStandNotice` 金额字段失败时前端是否接受 null/0 兜底" |

### GIT-20260604-019：站起 R-03 收敛 UserStandCommandDefault / UserStandTask 日志

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-019 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 4 / 站起 |
| 关联文档 | `04-站起.md` §5 D12 日志<br>`04-站起-重构设计.md` §4 R-03<br>`04-站起-实现计划.md` Task 3 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `38e58122f600067f6aa50c94bfd49a61819961a1` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/user/UserStandCommandDefault.java`<br>`dx-game-frame-service/src/main/java/com/dx/game/frame/service/task/once/UserStandTask.java` |
| 核心变更 | 1. `UserStandCommandDefault.handleCommand` / handle 用户不在 PLAYER_USER 分支：req/context/uidList toJson info → debug；info 只保留 tableId/userId/standType<br>2. `UserStandTask.run` 任务 toJson info → debug<br>3. catch 块的 warn/error 日志去掉 req/context JSON 体，仅保留 tableId/userId + 异常栈 |
| 验证结果 | 未验证：日志收敛属于"零行为变更"改造，理论上不影响功能；尚未通过 grep 之外的实际运行验证 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 38e58122f600067f6aa50c94bfd49a61819961a1`，或恢复两个文件到提交前版本 |
| 回退影响 | 回退后 1007 链路 info 日志重新含 req/context/uidList JSON 体，CPU + 隐私风险重现 |
| 未知问题 | 1007 高峰是否真的需要 debug 级保留完整 payload？如果排障频率极低，后续可考虑直接删除 debug 日志 |

### GIT-20260604-020：退出 R-01/R-02/R-03 UserQuitNotice userItem 空值保护 + 钱包兜底 + 日志收敛

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-020 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 6 / 退出 |
| 关联文档 | `06-退出.md` §5 P0 NPE / P1 钱包<br>`06-退出-重构设计.md` §4 R-01/R-02/R-03<br>`06-退出-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `f6c046554c84810c1263eca7e758489ba5bd4203` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/notice/UserQuitNotice.java` 整体重写 |
| 核心变更 | 1. **R-01 (P0)**：`BaseTableUserCache.getUser` 返回 null 时不再 NPE；`chairId / status` 兜底为 null，保持"不在房间的用户 1005 仍返回成功"的现有幂等语义；消除 `UserQuitCommandDefault.handle` 在用户不在 uidList 时调用 `notice` 立即栈崩的 P0<br>2. **R-02 (P1)**：新增 `safeFetchChipScore(tableId, userId) → BigDecimal`，`TableUserWalletCache.getChipScore` 抛任何异常时返回 `BigDecimal.ZERO` + warn 日志（与 04 R-02 同模式）<br>3. **R-03 (P2)**：`userItem / context / bringOutResult / userQuitNoticeDto` toJson info 日志全部降级 debug；info 只保留 `tableId/userId/quitType/kickerReason/chairId/userItemPresent` 元数据 |
| 验证结果 | 未验证：仅完成代码改造；尚未通过 mock `getUser` 返回 null / mock `getChipScore` 抛 NPE 的回归冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert f6c046554c84810c1263eca7e758489ba5bd4203`，或恢复 `UserQuitNotice.java` 到提交前版本 |
| 回退影响 | 回退后 1005 在 userItem 缺失场景再次 NPE；钱包缓存缺失重新阻断 14008；info 日志重新含敏感 payload |
| 未知问题 | 客户端是否能正确处理 `UserQuitNoticeDto.chairId=null / status=null / chipScore=0` 的"未知"语义？06 §13 待客户端确认 |

### GIT-20260604-021：退出 R-03 UserQuitCommandDefault 1005 入口日志收敛

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-021 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 6 / 退出 |
| 关联文档 | `06-退出.md` §5 P2 日志<br>`06-退出-重构设计.md` §4 R-03<br>`06-退出-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `101409a0a4f5a241c2293dc7be74a54022d7ef46` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/user/UserQuitCommandDefault.java` |
| 核心变更 | 1. `handleCommand` 头部 req toJson info → debug；info 仅 `tableId/userId/handType`<br>2. catch BusinessException / Exception 两个分支的 warn 日志去掉 req JSON 体，保留 `tableId/userId` + 异常栈<br>3. `handle` "不在 uidList" 分支 context/uidList toJson info → debug；info 仅 `tableId/userId/quitType` |
| 验证结果 | 未验证：日志收敛属于"零行为变更"改造，理论上不影响功能 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 101409a0a4f5a241c2293dc7be74a54022d7ef46`，或恢复 `UserQuitCommandDefault.java` 到提交前版本 |
| 回退影响 | 回退后 1005 入口 info 日志重新含 req/context/uidList JSON 体，CPU + 隐私风险重现 |
| 未知问题 | 无 |

### GIT-20260604-022：退出 R-03 UserQuitTask 退出任务日志收敛

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-022 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 6 / 退出 |
| 关联文档 | `06-退出.md` §5 P2 日志<br>`06-退出-重构设计.md` §4 R-03<br>`06-退出-实现计划.md` Task 3 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `8681ca4526de0118d7199b9d69c45e8c30ccf658` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/task/once/UserQuitTask.java` |
| 核心变更 | 1. `run()` 头 context toJson info → debug；info 仅 `tableId/userId/quitType`<br>2. catch BusinessException warn / Exception error 两个分支去掉 context JSON 体，保留 `tableId/userId` + 异常栈 |
| 验证结果 | 未验证：日志收敛属于"零行为变更"改造 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 8681ca4526de0118d7199b9d69c45e8c30ccf658`，或恢复 `UserQuitTask.java` 到提交前版本 |
| 回退影响 | 回退后退出任务 info 日志重新含 context JSON 体 |
| 未知问题 | 无 |

### GIT-20260604-023：离开状态检查 R-02 新增 LeaveIntent 和 UserArea 枚举

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-023 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 7 / 离开状态检查 |
| 关联文档 | `07-离开状态检查.md` §5 P0-1 / §7 改造建议<br>`07-离开状态检查-重构设计.md` §4 R-02<br>`07-离开状态检查-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `cc72065eeabb53051b637697c3f74a7d288cfaa5` |
| 变更范围 | 新增 `dx-game-frame-constant/src/main/java/com/dx/game/frame/constant/enums/user/LeaveIntent.java`<br>新增 `dx-game-frame-constant/src/main/java/com/dx/game/frame/constant/enums/user/UserArea.java` |
| 核心变更 | 1. `LeaveIntent` 枚举：`STAND / QUIT / BREAK_LINK / PREP_STAND` 四类离开意图<br>2. `UserArea` 枚举：`DISBAND / WATCH / QUIT / OCCUPY / SIT_DOWN_WAITING / PLAYER / UNKNOWN` 七种用户当前所在区域<br>3. 为后续 `LeaveDecision` 结构化 API + LeaveRuleChain 大改打基础 |
| 验证结果 | 未验证：仅新增枚举常量；后续随 LeaveDecisionService 一起测试 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert cc72065eeabb53051b637697c3f74a7d288cfaa5`，或删除两个枚举文件 |
| 回退影响 | 单独回退会导致 GIT-20260604-024、GIT-20260604-025 编译失败；需同时回退 |
| 未知问题 | 无 |

### GIT-20260604-024：离开状态检查 R-02 新增 LeaveDecision DTO

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-024 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 7 / 离开状态检查 |
| 关联文档 | `07-离开状态检查.md` §5 P0-1<br>`07-离开状态检查-重构设计.md` §4 R-02<br>`07-离开状态检查-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `a9c8efc5dada1c09d7c51b0e4a225bed65643a4a` |
| 变更范围 | 新增 `dx-game-frame-model/src/main/java/com/dx/game/frame/model/dto/leave/LeaveDecision.java` |
| 核心变更 | 1. `LeaveDecision` 不可变 DTO，承载结构化离开决策结果<br>2. 字段：`intent / allowed / errorCode / currentArea / evidence`<br>3. `@Builder @AllArgsConstructor` 方便测试和未来扩展 |
| 验证结果 | 未验证：仅新增 DTO |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert a9c8efc5dada1c09d7c51b0e4a225bed65643a4a`，或删除该文件 |
| 回退影响 | 单独回退会导致 GIT-20260604-025 编译失败；需同时回退 |
| 未知问题 | `evidence` 字段是否需要结构化为 `List<RuleEvaluation>`？本期保留 String 简单实现；未来 LeaveRuleChain 时改 |

### GIT-20260604-025：离开状态检查 R-03 新增 LeaveDecisionService

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-025 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 7 / 离开状态检查 |
| 关联文档 | `07-离开状态检查.md` §7 改造建议<br>`07-离开状态检查-重构设计.md` §4 R-03、§5.4<br>`07-离开状态检查-实现计划.md` Task 3 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `e8e6c7a6132d2df709267186f27ebbe47f8ce12c` |
| 变更范围 | 新增 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/leave/LeaveDecisionService.java` |
| 核心变更 | 1. `LeaveDecisionService.evaluate(LeaveIntent, tableId, userId) → LeaveDecision`<br>2. `detectArea(...)` 一次性快照计算用户当前所在区域；顺序与 `UserLeaveDefault.commonCheckUserLeave` 完全一致<br>3. `invokeUnderlyingCheck` 根据 intent 委托 `commonCheckUserLeave` 或 `commonCheckUserBreakLink`，行为 100% 等价<br>4. evidence 字段仅 debug 级使用<br>5. 老调用方完全不变；新调用方可 opt-in 走此 API |
| 验证结果 | 未验证：仅完成新 API；尚未将 04/06/02/18 等现有调用方迁移到此 API |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert e8e6c7a6132d2df709267186f27ebbe47f8ce12c`，或删除该文件 |
| 回退影响 | 回退后失去结构化 API 雏形；老 `commonCheckUserLeave` 完全不变，不影响功能 |
| 未知问题 | 1) 是否需要在本期就推送 04/06 老调用方迁移？本期保持 opt-in，不强推；2) 未来 LeaveRuleChain 专项是否要把 `evaluate` 内部完全替换为 `LeaveRule` 链？设计上预留了空间 |

### GIT-20260604-026：离开状态检查 R-01/R-04 UserLeaveDefault 系统站起 event key 修复 + 日志收敛

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-026 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 7 / 离开状态检查 |
| 关联文档 | `07-离开状态检查.md` §5 P2 日志<br>`07-离开状态检查-重构设计.md` §4 R-01、R-04<br>`07-离开状态检查-实现计划.md` Task 4<br>关联 04 R-01（GIT-20260604-017） |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `bc009d0fe9408cf1624a3d36cb6ce27d89ba928c` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/def/UserLeaveDefault.java` |
| 核心变更 | 1. **R-01 (P0 sibling)**：`userStand(...)` 系统站起入口的 event key 从 `OnceEventTypeEnum.USER_QUIT_TASK` 改为 `OnceEventTypeEnum.USER_STAND_TASK`；这是 04 R-01（GIT-20260604-017）在 frame 系统站起入口侧的姊妹 bug。影响所有系统站起入口：08 风控 `realtimeCheckRisk` / 17 补码失败 / 房主强制 / 旁观上限退出等<br>2. **R-04 (P2)**：`commonCheckUserLeave` 5 处分支 info → debug；`userStand` 2 处早返回分支 info → debug；`pushQuitTask` 中 `quitContext` toJson info → debug<br>3. info 仅保留 `tableId/userId/standType/quitType/kickerReason/messageId` 元数据 |
| 验证结果 | 未验证：尚未通过 08 风控触发系统站起 + 客户端 1006 并发的实际冒烟回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert bc009d0fe9408cf1624a3d36cb6ce27d89ba928c`，或恢复 `UserLeaveDefault.java` 到提交前版本 |
| 回退影响 | 回退后系统站起 event key 重新与退出冲突，并发场景 P0 复发；info 日志重新含 quitContext JSON 体 |
| 未知问题 | 系统站起入口与客户端 1006 并发的真实场景频率有多高？建议线上加一个针对 `userStand` event key 的日志埋点观测 1~2 周 |

### GIT-20260604-027：进入房间前校验 R-01 GameHandleFactory 新增 getEnterRoomBeforeHandler

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-027 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 12 / 进入房间前校验 |
| 关联文档 | `12-进入房间前校验.md` §5 P0-1<br>`12-进入房间前校验-重构设计.md` §4 R-01<br>`12-进入房间前校验-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `d8443cab242cd2f08296201919fcf514d642477b` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/factory/GameHandleFactory.java`（additive） |
| 核心变更 | 1. 新增 `getEnterRoomBeforeHandler(Long tableId) → IEnterRoomBeforeHandler`<br>2. 复用既有 private `findHandler(gameSpaceType, protoType)`<br>3. 不走 `getTypedHandle` 的 `requireNonNull`，无匹配/tableInfo 缺失时返回 null<br>4. 既有 `getEnterRoomHandler` / `getUserSitDownHandler` / `getTypedHandle` / `findHandler` 完全不动 |
| 验证结果 | 未验证：仅 additive 新增方法；后续随 EnterRoomBeforeCommandDefault 一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert d8443cab242cd2f08296201919fcf514d642477b`，或删除新增方法 + import |
| 回退影响 | 单独回退会导致 GIT-20260604-029 编译失败；需同时回退 |
| 未知问题 | `GameSpaceTypeEnums` 是否还有 CLUB/HALL/RACE/PRIVATE 之外的空间类型？目前 fallback 到 CLUB 兜底；新增空间需要补 handler 或在 fallback 中处理 |

### GIT-20260604-028：进入房间前校验 R-02/R-05 PrivatedEnterRoomBeforeHandler 补密码基线 + 文案修正

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-028 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 12 / 进入房间前校验 |
| 关联文档 | `12-进入房间前校验.md` §5 P0-1（私人房禁入漏拦）/ §5 P2 命名误导<br>`12-进入房间前校验-重构设计.md` §4 R-02/R-05<br>`12-进入房间前校验-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `e9b9c699378c528348f7d71fcc545886580fce3d` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/handler/enterroombefore/PrivatedEnterRoomBeforeHandler.java`（整体重写） |
| 核心变更 | 1. **R-02 (P0 配套)**：`handle()` 首行补 `super.check(req)` 密码校验基线<br>   改造前 `EnterRoomBeforeCommandDefault.check` 对所有房统一调 `checkUserPwd`；改造后 1032 走 handler 分发，Private 必须显式补密码校验，否则私人房会跳过密码<br>2. **R-02 配套 null 保护**：`userBaseInfo == null` 时不抛 NPE，跳过禁入校验<br>3. **R-05 (P2)**：日志文案「私人房德州游戏」→「私人房」，掼蛋工程不再误导<br>4. 异常码 `USER_JOIN_GAME_LOCK_STATUS` 行为不变 |
| 验证结果 | 未验证：仅完成 handler 内部改造；后续随 Command 默认入口 commit 一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert e9b9c699378c528348f7d71fcc545886580fce3d`，或恢复 `PrivatedEnterRoomBeforeHandler.java` 到提交前版本 |
| 回退影响 | 单独回退会让 R-02 P0 修复失效：1032 走 handler 分发后私人房会跳过密码校验（**重大回归**），需同时回退 029 |
| 未知问题 | 私人房禁入校验「由失效转生效」是否有灰度依赖？修复后 `privateMajongStatus=1` 玩家将被 1032 拦截，需产品/风控确认无依赖旧（漏拦）行为 |

### GIT-20260604-029：进入房间前校验 R-02/R-03/R-04 EnterRoomBeforeCommandDefault check() 改走 handler 分发 + 日志收敛 + 整理 1 行格式

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-029 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 12 / 进入房间前校验 |
| 关联文档 | `12-进入房间前校验.md` §5 P0-1/P1-1/P2<br>`12-进入房间前校验-重构设计.md` §4 R-02/R-03/R-04<br>`12-进入房间前校验-实现计划.md` Task 3 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `904efde88a42991613b5dae07a78c036e5d22167` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/enterRoom/EnterRoomBeforeCommandDefault.java`（整体重写） |
| 核心变更 | 1. **R-02 (P0)**：`check()` 改为通过 `GameHandleFactory.getEnterRoomBeforeHandler(tableId)` 分发到 Club/Hall/Private 空间 handler；handler==null 时兜底走 `BaseUserCheckAuthService.checkUserPwd`（等价改造前）；让原本游离未被调用的空间 handler 真正生效（修复 P0 死代码 + 私人房禁入漏拦）<br>2. **R-03 (P1)**：`needPwd` 内部上下文字段保留计算；class Javadoc 明确 1032 成功仅代表「密码校验通过且空间禁入校验通过」<br>3. **R-04 (P2)**：handleCommand / initContext / catch 中 req/context toJson info → debug；info 仅保留 `tableId/userId/inRoom` 元数据<br>4. 顺便整理原本压在 1 行的 imports 为标准格式（不影响行为，与 04 R-02 整理 UserStandNotice 同模式） |
| 验证结果 | 未验证：尚未通过 CLUB/PRIVATE/HALL 三类空间真实场景冒烟回归；尚未模拟 `tableInfo == null` 走兜底密码校验 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 904efde88a42991613b5dae07a78c036e5d22167`，或恢复 `EnterRoomBeforeCommandDefault.java` 到提交前版本 |
| 回退影响 | 回退后 1032 重新走 hard-coded `checkUserPwd`，空间 handler 重回游离状态；私人房禁入 P0 重新漏拦；info 日志重新含 context JSON 体 |
| 未知问题 | 1) 私人房禁入「由失效转生效」是否有灰度依赖（同 028 未知问题）；2) `roomNo` 是否仍被客户端使用？本期保留字段不强制校验；3) `needPwd` 是否需要新增 `isNeedPwd` 响应字段？产品待确认 |

### GIT-20260604-030：牌桌状态查询 R-02 TableStatusContext 新增 disbanded 字段

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-030 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 13 / 牌桌状态查询 |
| 关联文档 | `13-牌桌状态查询.md` §5 P0-1<br>`13-牌桌状态查询-重构设计.md` §4 R-02<br>`13-牌桌状态查询-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `1a3f8ea2080cb7aadcd5042d79dd66816c07cd9d` |
| 变更范围 | `dx-game-frame-model/src/main/java/com/dx/game/frame/model/context/TableStatusContext.java` |
| 核心变更 | 1. 新增内部字段 `private boolean disbanded = false`<br>2. 承载"牌桌是否已解散"的标记，供下游 check/refreshUser/after 短路判断使用<br>3. 顺便修正注释错字「牌桌装」→「牌桌状态」<br>4. 本字段不进协议；`TableStatusRespDto` 不变 |
| 验证结果 | 未验证：仅新增内部字段；后续随 TableStatusCommandDefault 一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 1a3f8ea2080cb7aadcd5042d79dd66816c07cd9d`，或删除新增字段 |
| 回退影响 | 单独回退会导致 GIT-20260604-031 编译失败；需同时回退 |
| 未知问题 | 无 |

### GIT-20260604-031：牌桌状态查询 R-01/R-02/R-03/R-04 TableStatusCommandDefault 重写

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-031 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 13 / 牌桌状态查询 |
| 关联文档 | `13-牌桌状态查询.md` §5 P0/P1<br>`13-牌桌状态查询-重构设计.md` §4 R-01/R-02/R-03/R-04<br>`13-牌桌状态查询-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `d7829de7bbf9c07f9bcc01d7c49283f4631ea656` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/enterRoom/TableStatusCommandDefault.java`（整体重写） |
| 核心变更 | 1. **R-01 (P0 逻辑 bug)**：`check()` 改为 `if/else if/else` 互斥分支：HALL → Hall校验；PRIVATE → Private校验；CLUB/RACE/兜底 → Club校验。修复 HALL 桌错误同时跑 Hall+Club 两份校验的 P0；RACE 桌走 Club 行为同改造前。增加 `tableInfo == null` 早返回 + warn 日志<br>2. **R-02 (P0 NPE)**：`initContext` disband 路径下 `setDisbanded(true)` + `setTableStatus(GAME_END)`；`check/refreshUser/after` 全部对 `disbanded=true` 短路；`after` 解散桌只回 `status=GAME_END(2)` + 空 `TableSimpleCfgDto` + `isPassword=false`，不再读已清理的 cache 而 NPE<br>3. **R-03 (P1)**：`after()` 对 `tableInfo == null` 用空 `TableSimpleCfgDto` 兜底 + warn 日志<br>4. **R-04 (P2)**：`handleCommand` / `initContext` / `after` / `catch` 中 context/req/respDto toJson info → debug；info 仅保留 `tableId/userId/status/disbanded` 元数据<br>5. 顺便删除原文件中已注释的旧 `check` 方法（200+ 字符 dead code）<br>6. 协议 1025 请求/响应字段全部不变 |
| 验证结果 | 未验证：尚未通过 HALL/PRIVATE/CLUB/RACE 四类空间冒烟；尚未通过 mock `checkDisbandTable=true` 验证 disband 桌返回 `status=GAME_END` 而不是 SYSTEM_EXCEPTION；尚未通过 mock `getTableInfo=null` 验证 after 走兜底 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert d7829de7bbf9c07f9bcc01d7c49283f4631ea656`，或恢复 `TableStatusCommandDefault.java` 到提交前版本 |
| 回退影响 | 回退后 HALL 桌重新同时跑两份权限校验（性能/行为意外）、RACE 桌错走 Club 校验（保持回退后不变）；解散桌 1025 重新抛 NPE → SYSTEM_EXCEPTION；info 日志重新含 toJson payload |
| 未知问题 | 1) 解散桌从「SYSTEM_EXCEPTION」改为「`status=GAME_END(2)` + 空配置」是否符合客户端期望？老客户端可能将 SYSTEM_EXCEPTION 当作"未知/重试"，新行为是明确"已结束"。需要客户端确认<br>2) RACE 桌当前走 Club 校验是否符合产品预期？设计文档已标注待确认<br>3) `GameTableBootstrapService.init` 在查询接口的副作用是否应保留？设计文档已标注转交单独立项 |

### GIT-20260604-032：预站起留座离桌 R-01 新增 UserStandPrepBootstrapServiceImpl（与 20 S-02 混合 commit）

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-032 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 18 / 预站起留座离桌（与 20 / 好友备注 S-02 混合 commit） |
| 关联文档 | `18-预站起留座离桌.md` §5 P0-1<br>`18-预站起留座离桌-重构设计.md` §4 R-01<br>`18-预站起留座离桌-实现计划.md` Task 1<br>同一 commit 含 20 S-02 影响范围另行记录于 GIT-20260604-038 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `036cfd439d224c1a3e4a92823f4ecffe5df63f99` |
| 变更范围 | 18 部分：`dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/impl/UserStandPrepBootstrapServiceImpl.java` |
| 核心变更 | 1. **R-01 (P0-1)**：新增 `UserStandPrepBootstrapServiceImpl` 实现 `UserStandPrepBootstrapService` 接口<br>2. `prepStand(tableId, userId, prepStandStatusEnum)`：把预站起意图写入 `BaseUserItem.prepStandStatus`<br>3. 真正离开动作由 `PrepStandLeaveUserVisitor` 在本手/本轮结束时扫描生成<br>4. 立即站起（STAND=1）不在此协议范围，仍走 1004/1007 协议<br>5. 解决"1045 协议存在但 service 实现缺失导致系统异常"的 P0 |
| 验证结果 | 未验证：仅有代码改造；尚未通过 1045 端到端冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 036cfd439d224c1a3e4a92823f4ecffe5df63f99`（注意同时回退 20 S-02 部分），或单独删除 `UserStandPrepBootstrapServiceImpl.java` |
| 回退影响 | 18 部分回退后 1045 重新抛"无 Bean 实现"系统异常；P0-1 复发 |
| 未知问题 | 1) commit message 标注为 "feat(S-02)"（20 范围），实际包含 18 R-01 实现；属于"多功能混合提交"，按指导文档 §六 要求拆成 032/038 两条记录；2) 本登记由后补完成，原作者非本人，登记内容由 commit message + plan + diff 对照推断，准确性请原作者复核 |

### GIT-20260604-033：预站起留座离桌 R-02 新增 1034 UserHoldSeatCommand 占位

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-033 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 18 / 预站起留座离桌 |
| 关联文档 | `18-预站起留座离桌.md` §5 P0-2<br>`18-预站起留座离桌-重构设计.md` §4 R-02<br>`18-预站起留座离桌-实现计划.md` Task 2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `27a889dc6f0bf3843da6d17ca288fd9b19e31916` |
| 变更范围 | `dx-game-frame-cmd/src/main/java/com/dx/game/frame/cmd/command/userholdseat/UserHoldSeatCommand.java` |
| 核心变更 | 1. **R-02 (P0-2)**：新增 1034 `UserHoldSeatCommand` 占位 Command 类<br>2. 实现 `RequestCommand<...>`、`getType()` 返回 `CommonProto.USER_HOLD_SEAT`<br>3. `handleCommand` 抛 `NOT_SUPPORT_OPERATION`，明确告知客户端"功能未支持"<br>4. 修复"1034 协议号存在但无 Command 注册导致请求被静默丢包"的 P0 |
| 验证结果 | 未验证：仅有代码改造；尚未通过 1034 请求端到端冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 27a889dc6f0bf3843da6d17ca288fd9b19e31916`，或删除该文件 |
| 回退影响 | 回退后 1034 重新静默丢包；客户端无任何感知 |
| 未知问题 | 1) 1034 协议号是否仍被客户端使用？如果不再使用应清理协议号定义<br>2) 本登记由后补完成，原作者非本人，登记内容由 commit message + plan + diff 对照推断，准确性请原作者复核 |

### GIT-20260604-034：预站起留座离桌 R-03 修正 UserPrepStandReqDto.standType 与 PrepStandStatusEnum 注释

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-034 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 18 / 预站起留座离桌 |
| 关联文档 | `18-预站起留座离桌.md` §5 P1<br>`18-预站起留座离桌-重构设计.md` §4 R-03<br>`18-预站起留座离桌-实现计划.md` Task 3 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `0e238679cf9454a3ebb9e4959cc78a7dd379cd21` |
| 变更范围 | `dx-game-frame-constant/src/main/java/com/dx/game/frame/constant/enums/userleave/PrepStandStatusEnum.java`<br>`dx-game-frame-model/src/main/java/com/dx/game/frame/model/dto/userstand/UserPrepStandReqDto.java` |
| 核心变更 | 1. **R-03 (P1)**：修正 `UserPrepStandReqDto.standType` 字段注释<br>2. 修正 `PrepStandStatusEnum` 枚举注释<br>3. 仅注释文案，不改代码行为；纯文档级修复语义混乱 |
| 验证结果 | 文档变更，未运行代码测试；语义混乱被修复后阅读门槛降低 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 0e238679cf9454a3ebb9e4959cc78a7dd379cd21`，或恢复两个文件到提交前注释 |
| 回退影响 | 回退后注释回到改造前语义混乱状态，但代码行为不变 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-035：预站起留座离桌 R-04/R-05/R-06 1045 补 respDto.userId + 收敛日志 + 服务接口 Javadoc

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-035 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 18 / 预站起留座离桌 |
| 关联文档 | `18-预站起留座离桌.md` §5 P1/P2<br>`18-预站起留座离桌-重构设计.md` §4 R-04/R-05/R-06<br>`18-预站起留座离桌-实现计划.md` Task 4/5/6 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `877114fba991e432519563978c90aa870533b518` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/UserStandPrepBootstrapService.java`<br>`dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/user/UserPrepStandCommandDefault.java`<br>`dx-game-frame-service/src/main/java/com/dx/game/frame/service/visitor/userleavevisitor/PrepStandLeaveUserVisitor.java` |
| 核心变更 | 1. **R-04 (P1)**：1045 响应 `UserPrepStandRespDto.userId` 补设值（之前 userId 缺失）<br>2. **R-05 (P2)**：`UserPrepStandCommandDefault` / `PrepStandLeaveUserVisitor` 含 context/req toJson 的 info 日志降级 debug；info 仅保留 tableId/userId/standType 元数据<br>3. **R-06**：`UserStandPrepBootstrapService` 接口补 Javadoc，明确"立即站起走 1007/1004，本协议只写 prepStandStatus" |
| 验证结果 | 未验证：仅有代码改造；尚未通过 1045 协议字段回归 + 客户端联调 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 877114fba991e432519563978c90aa870533b518`，或恢复三个文件到提交前 |
| 回退影响 | 1045 响应 userId 重新缺失；info 日志重新含敏感 payload |
| 未知问题 | 1) 1034/1045 协议字段客户端兼容需要联调；2) 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-036：用户配置查询修改 R-01/R-04 新增 AutoComplementConfigService + UserConfigCacheService

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-036 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 21 / 用户配置查询修改 |
| 关联文档 | `21-用户配置查询修改.md` §5<br>`21-用户配置查询修改-重构设计.md` §4 R-01/R-04<br>`21-用户配置查询修改-实现计划.md` Task 1/2 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `d385a35aff989dbfad1742cf25bf22fc151a4a5d` |
| 变更范围 | 新增 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/userconfig/AutoComplementConfigService.java`<br>新增 `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/userconfig/UserConfigCacheService.java` |
| 核心变更 | 1. **R-01**：新增 `AutoComplementConfigService` 统一 1029/3019 自动补码目标值口径（正整数 + 桌范围夹取 + configMap 兼容）<br>2. **R-04**：新增 `UserConfigCacheService` 提供 `get/refresh/prewriteAutoComplement` 三组操作<br>3. `refresh` 返回显式 `boolean`，异常吞掉但记录 debug，让调用方显式判断刷新结果<br>4. 老 `UserConfigCache` 静态门面保留供其它链路使用，不破坏既有 API |
| 验证结果 | 未验证：仅新增 service 类；后续随 1028/1029 切换 commit 一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert d385a35aff989dbfad1742cf25bf22fc151a4a5d`，或删除两个新增 service 文件 |
| 回退影响 | 单独回退会导致 GIT-20260604-037 编译失败；需同时回退 037 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-037：用户配置查询修改 R-01/R-04/R-05 1028/1029 切到 UserConfigCacheService / AutoComplementConfigService + 日志收敛

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-037 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 21 / 用户配置查询修改 |
| 关联文档 | `21-用户配置查询修改.md` §5<br>`21-用户配置查询修改-重构设计.md` §4 R-01/R-04/R-05<br>`21-用户配置查询修改-实现计划.md` Task 3/4/5 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `70006efe50873e9e605e56d60ed0d554e99004a8` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/userconfig/UserConfigQueryCommandDefault.java`（1028）<br>`dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/bootstrap/command/userconfig/UserConfigUpdateCommandDefault.java`（1029）<br>`dx-game-frame-repository/src/main/java/com/dx/game/frame/repository/local/cache/UserFriendCache.java`（顺带改动） |
| 核心变更 | 1. **R-01 1028**：用 `UserConfigCacheService.get` 取代静态门面 `UserConfigCache.getUserCfgCache`<br>2. **R-01 1029**：删除三个私有方法（saveAutoBringChipScoreIfNecessary / isValidAutoBringRange / isPositive），改为委托 `AutoComplementConfigService.saveIfPresent(requireInteger=true)`<br>3. **R-04 1029**：缓存读取与刷新走 `UserConfigCacheService`；`refresh` 返回 boolean 显式判断；大厅匿名比较仅在 refresh 成功且 newConfig 非空时执行，避免 NPE<br>4. **R-05**：异常日志错码字符串笔误修正 1041 → 1029<br>5. **R-05**：收敛 `GsonUtils.toJson(req/resp)` info → debug<br>6. info 仅保留 tableId/userId 元数据 |
| 验证结果 | 未验证：尚未通过 1028/1029 协议字段回归 + 自动补码端到端冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 70006efe50873e9e605e56d60ed0d554e99004a8`，或恢复三个文件到提交前 |
| 回退影响 | 1028/1029 重新走老静态门面 + 私有方法；NPE 风险重现；info 日志重新含敏感 payload |
| 未知问题 | 1) 21 设计文档 R-02 / R-03（3018/3019 协议改造）在已 push 的 commit 中**未找到明确的 R-02/R-03 范围**：本次 02-04 号 commit 仅覆盖 1028/1029，对 3018/3019 是否已改造需要原作者确认；2) `UserFriendCache.java` 出现在本 commit 文件列表中，与 21 用户配置语义无关，疑似顺带改动，需原作者解释；3) 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-038：好友备注 S-02 新增 FriendRemarkCommandService（与 18 R-01 混合 commit）

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-038 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 20 / 好友备注（与 18 R-01 混合 commit） |
| 关联文档 | `20-好友备注.md` §5<br>`20-好友备注-重构设计.md` §4 S-02<br>`20-好友备注-实现计划.md` Task 关于 FriendRemarkCommandService<br>同一 commit 含 18 R-01 影响范围另行记录于 GIT-20260604-032 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `036cfd439d224c1a3e4a92823f4ecffe5df63f99` |
| 变更范围 | 20 部分：`dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/friendremark/FriendRemarkCommandService.java` |
| 核心变更 | 1. **S-02**：新增 `FriendRemarkCommandService` 接管 1033 协议业务流程<br>2. 把原本散落在 `FriendRemarkCommand` 内部的 RPC 调用 + 缓存写入 + 响应组装编排剥离到 service 层<br>3. `FriendRemarkCommand` 后续仅做协议接入、异常翻译、响应发送（在 GIT-20260604-043 中切换委托） |
| 验证结果 | 未验证：仅新增 service 类；后续随 1033 切换 commit 一起冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 036cfd439d224c1a3e4a92823f4ecffe5df63f99`（注意同时回退 18 R-01 部分），或单独删除 `FriendRemarkCommandService.java` |
| 回退影响 | 20 部分回退会导致 GIT-20260604-043 编译失败；需同时回退 |
| 未知问题 | 1) commit 标签 feat(S-02) 准确描述 20 范围，但同一 commit 还包含 18 R-01 文件；按指导文档 §六 拆为 032/038 两条记录；2) 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-039：好友备注 S-01 第一步 新增 FriendRemarkCacheEntry

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-039 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 20 / 好友备注 |
| 关联文档 | `20-好友备注.md` §5<br>`20-好友备注-重构设计.md` §4 S-01<br>`20-好友备注-实现计划.md` Task 关于 FriendRemarkCacheEntry |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `3c2cc4355ef99f486787735edeb9874282957dfe` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/friendremark/FriendRemarkCacheEntry.java`（注：后由 GIT-20260604-041 搬迁到 repository 模块） |
| 核心变更 | 1. **S-01 第一步**：新增 `FriendRemarkCacheEntry` 承载缓存条目（含 hit/miss 区分、TTL 等元数据）<br>2. 这是缓存重构的基础类型，本身不含逻辑<br>3. 后续 GIT-20260604-040 在 `FriendRemarkCacheService` 中使用此类型 |
| 验证结果 | 未验证：仅新增数据类型 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 3c2cc4355ef99f486787735edeb9874282957dfe`，或删除该文件 |
| 回退影响 | 单独回退会导致 GIT-20260604-040 编译失败；需同时回退 040/041/043/044 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-040：好友备注 F-02/F-03 新增 FriendRemarkCacheService

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-040 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 20 / 好友备注 |
| 关联文档 | `20-好友备注.md` §5 F-02/F-03<br>`20-好友备注-重构设计.md` §4 F-02/F-03<br>`20-好友备注-实现计划.md` Task 关于 FriendRemarkCacheService |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `f5ade75227cef25ef1d1334e1506521e25e9c300` |
| 变更范围 | `dx-game-frame-service/src/main/java/com/dx/game/frame/service/biz/friendremark/FriendRemarkCacheService.java`（注：后由 GIT-20260604-041 搬迁到 repository 模块） |
| 核心变更 | 1. **F-02**：负缓存独立短 TTL —— 区分"未查到"和"RPC 异常"两类缓存条目，避免负结果用普通 TTL 长时间错误命中<br>2. **F-03**：RPC 异常不再静默吞 —— 异常路径显式记录到缓存 entry，调用方可判断是真的没好友还是查询失败<br>3. 缓存逻辑收敛到独立 service，老 `UserFriendCache` 静态门面保留供旧调用方使用 |
| 验证结果 | 未验证：仅新增 service 类；后续随 UserFriendCache 切换冒烟 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert f5ade75227cef25ef1d1334e1506521e25e9c300`，或删除该文件 |
| 回退影响 | 负缓存与异常吞噬两个 P1 问题重现；需同时回退 041 才能保持后续 commit 编译通过 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-041：好友备注 模块依赖修复 把 FriendRemarkCacheEntry/Service 从 service 移到 repository

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-041 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 20 / 好友备注 |
| 关联文档 | `20-好友备注-实现计划.md` 模块依赖说明<br>`20-好友备注-重构设计.md` §模块边界 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `15624810b4bf66be38e865c8a6a918535ca5d482` |
| 变更范围 | 删除 `dx-game-frame-service/.../friendremark/FriendRemarkCacheEntry.java`<br>删除 `dx-game-frame-service/.../friendremark/FriendRemarkCacheService.java`<br>新增 `dx-game-frame-repository/src/main/java/com/dx/game/frame/repository/local/cache/friendremark/FriendRemarkCacheEntry.java`<br>新增 `dx-game-frame-repository/src/main/java/com/dx/game/frame/repository/local/cache/friendremark/FriendRemarkCacheService.java` |
| 核心变更 | 1. **模块依赖修复**：原本 cache 类放在 service 模块，但静态门面 `UserFriendCache` 在 repository 模块要引用它，违反 repository 不依赖 service 的分层约束<br>2. 把 FriendRemarkCacheEntry / FriendRemarkCacheService 搬到 `dx-game-frame-repository/local/cache/friendremark/`，让 `UserFriendCache` 能 import<br>3. 仅类位置变更，行为不变 |
| 验证结果 | 未验证：编译需通过（搬迁后包路径变化）；功能行为未变 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 15624810b4bf66be38e865c8a6a918535ca5d482`，或恢复 service 模块下的两个类位置 |
| 回退影响 | 回退后 `UserFriendCache` 静态门面要引用 service 模块类，会触发跨模块编译循环依赖 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-042：好友备注 F-01/F-04/F-05 笔误修复 + PII + map 日志

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-042 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 20 / 好友备注 |
| 关联文档 | `20-好友备注.md` §5 F-01/F-04/F-05<br>`20-好友备注-重构设计.md` §4 F-01/F-04/F-05<br>`20-好友备注-实现计划.md` Task 1 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `6de0a6f3f4848c03d3c34245cfbf984ab0729857` |
| 变更范围 | `dx-game-frame-cmd/src/main/java/com/dx/game/frame/cmd/command/friend/FriendRemarkCommand.java`<br>`dx-game-frame-repository/src/main/java/com/dx/game/frame/repository/local/cache/UserFriendCache.java` |
| 核心变更 | 1. **F-01 (P0 笔误)**：`FriendRemarkCommand.handleCommand` 中 `BeanUtils.copyProperties(req, addReq)` + `addReq.setRemarkUserId(...)` 笔误，全部改为显式 setter，避免字段误覆盖<br>2. **F-04 (P1 PII)**：req/resp 不再 `GsonUtils.toJson` 全量打印（含手机/昵称/备注文本等 PII）；info 仅输出 `userId/remarkUserId/字段长度`<br>3. **F-05 (P2)**：`UserFriendCache.updateFriendRemarkCache` 不再 `JSON.toJSONString` 整份 map；debug 仅打 remarkUserId |
| 验证结果 | 未验证：仅完成代码改造；尚未通过 1033 协议字段回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert 6de0a6f3f4848c03d3c34245cfbf984ab0729857`，或恢复两个文件到提交前 |
| 回退影响 | F-01 笔误 P0 复发；info 日志重新含 PII 与 map 全量 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-043：好友备注 FriendRemarkCommand 委托 FriendRemarkCommandService

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-043 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 20 / 好友备注 |
| 关联文档 | `20-好友备注-重构设计.md` §4 S-02 配套<br>`20-好友备注-实现计划.md` Task 关于 Command 切换委托 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `cea312807c809975f15de0ba65a26a6469105d04` |
| 变更范围 | `dx-game-frame-cmd/src/main/java/com/dx/game/frame/cmd/command/friend/FriendRemarkCommand.java` |
| 核心变更 | 1. **S-02 配套**：`FriendRemarkCommand` 内部业务编排剥离，改为委托 `FriendRemarkCommandService`（GIT-20260604-038 已引入）<br>2. Command 类瘦身，仅做协议接入 + 异常翻译 + 响应发送<br>3. 与 19/04/06/07/08/13 中 Command → CommandService 委托模式一致 |
| 验证结果 | 未验证：尚未通过 1033 协议字段回归 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert cea312807c809975f15de0ba65a26a6469105d04`，或恢复 `FriendRemarkCommand.java` 到提交前 |
| 回退影响 | Command 内部重新包含完整业务编排；与 service 层职责重叠 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

### GIT-20260604-044：好友备注 死代码清理 删除 redis/cache/UserFriendCache

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-044 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 20 / 好友备注 |
| 关联文档 | `20-好友备注.md` §死代码清理<br>`20-好友备注-重构设计.md` §死代码清理 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `e50608bff69adb7b8d332eac111f34577448ae43` |
| 变更范围 | 删除 `dx-game-frame-repository/src/main/java/com/dx/game/frame/repository/redis/cache/UserFriendCache.java` |
| 核心变更 | 1. **死代码清理**：`redis/cache/UserFriendCache` 与 `local/cache/UserFriendCache` 重名，且逻辑全部已注释掉<br>2. 删除该冗余文件，避免阅读时混淆<br>3. 保留 `local/cache/UserFriendCache`（真正使用的静态门面） |
| 验证结果 | 未验证：死代码清理理论上不影响行为；需确认无 import 引用残留 |
| 审核状态 | 未审核 |
| 回退方式 | `git -C dx-game-frame revert e50608bff69adb7b8d332eac111f34577448ae43`，或恢复该文件 |
| 回退影响 | 回退后两个同名冗余文件并存，阅读时易混淆，但功能无影响 |
| 未知问题 | 本登记由后补完成，原作者非本人，准确性请原作者复核 |

> **后补登记说明（GIT-20260604-045 ~ 056，02 入座共 12 条）**：
> 入座任务（02）由另一 agent 完成大型结构化重构（含 SitDownValidatorChain / SitDownStateService / SitDownFlowService + Validator 规则链 + IOccupyResitHandler 表级锁），跨 dx-game-frame + dx-game-guandan 两工程共 12 个 commit。
> 因本批次登记内容多、原作者非本人，每条记录采用**精简格式**：仅保留必要字段（commit/范围/核心变更/未知问题）。
> 未知问题统一标注：「本登记由后补完成，原作者非本人，登记内容由 commit message + 实现计划 + diff 对照推断，准确性请原作者复核；02-入座-重构设计.md 与 02-入座-实现计划.md 中 R/S 编号与本批次 commit 的对应关系建议原作者补充」。

### GIT-20260604-045：入座 R-01/R-05 占座入座 wallet 空值保护 + 收敛入座 info 日志

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-045 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `ee320d64214f5a8ce841657060b497be8735ebf1` |
| 关联文档 | `02-入座-重构设计.md` §4 R-01/R-05；`02-入座-实现计划.md` |
| 变更范围 | `UserSitDownDefault.java` |
| 核心变更 | R-01 占座入座 wallet 空值保护；R-05 收敛入座 info 日志 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert ee320d642`，或恢复 `UserSitDownDefault.java` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-046：入座 R-02 HALL/RACE 空入座 handler 改为显式抛 NOT_SUPPORT_OPERATION

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-046 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `5298ccaf6c9fd5657e5005c8ea5a7fce8585309e` |
| 关联文档 | `02-入座-重构设计.md` §4 R-02 |
| 变更范围 | `BusinessExceptionTypeEnums.java`（新增 `NOT_SUPPORT_OPERATION`）、`HallUserSitDownDefault.java`、`RaceUserSitDownDefault.java` |
| 核心变更 | HALL/RACE 空入座 handler 不再静默 no-op，显式抛业务异常告知客户端"功能不支持" |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 5298ccaf6`；注意 `BusinessExceptionTypeEnums.NOT_SUPPORT_OPERATION` 可能被其它任务依赖 |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-047：入座 R-03 占座超时任务先注册,通知失败不再卡 OCCUPY

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-047 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `48fa28c1256104dd0ce7a3400974913a497947eb` |
| 关联文档 | `02-入座-重构设计.md` §4 R-03 |
| 变更范围 | `BaseOccupyUserService.java` |
| 核心变更 | 占座超时任务先注册再发通知；通知失败不再让用户卡在 OCCUPY 状态，避免占座僵尸 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 48fa28c12` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-048：入座 S-01 新增 SitDownValidatorChain / SitDownStateService / SitDownFlowService 与扩展接口

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-048 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `4195f89ba5c1a9d85fd767ecfba81c470aa23784` |
| 关联文档 | `02-入座-重构设计.md` §4 S-01；`02-入座-实现计划.md` Task 关于 Validator/State/Flow Service |
| 变更范围 | 新增 4 个文件：`ISitDownValidatorContributor.java`、`SitDownFlowService.java`、`SitDownStateService.java`、`SitDownValidatorChain.java` |
| 核心变更 | 入座结构性重构基础：校验链 + 状态服务 + 编排服务 + 扩展接口；与 01 EnterRoomFlowService 模式平行 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 4195f89ba`；注意级联回退 049/050/051/052/053/054/055/056 |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-049：入座 新增 GdSitDownValidatorContributor 作为掼蛋入座校验扩展点

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-049 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-guandan 20260615/junk |
| commit / MR | `2f24178549fce14f552d8decfcc7667d19cab91e` |
| 关联文档 | `02-入座-重构设计.md` §4 S-01 配套 |
| 变更范围 | 新增 `dx-game-guandan-service/.../sitdown/GdSitDownValidatorContributor.java` |
| 核心变更 | 掼蛋侧通过 `ISitDownValidatorContributor` 扩展点向 frame 入座校验链注入掼蛋特有规则；与 01 GdEnterRoomValidatorContributor 模式平行 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git -C dx-game-guandan revert 2f2417854` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-050：入座 R-04 Club/Private 入座 Handler 委托 SitDownFlowService + 限流顺序调整

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-050 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `4b826a230fc5b32e195a6dbc7752b859429cefa4` |
| 关联文档 | `02-入座-重构设计.md` §4 R-04 |
| 变更范围 | `ClubUserSitDownDefault.java`、`PrivateUserSitDownDefault.java` |
| 核心变更 | 俱乐部/私人房入座 Handler 改走 `SitDownFlowService` 编排；R-04 限流顺序调整（具体顺序见 commit diff） |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 4b826a230` |
| 未知问题 | 后补登记，原作者复核；限流顺序调整具体语义需原作者补充 |

### GIT-20260604-051：入座 R-09 占座转入座调用点改走 SitDownStateService 表级锁（guandan）

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-051 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-guandan 20260615/junk |
| commit / MR | `da6e9dfad370118e6da12eb105394c47e54614d4` |
| 关联文档 | `02-入座-重构设计.md` §4 R-09 |
| 变更范围 | `UserSitDownBootstrap.java`、`UserSitDownFinishListener.java` |
| 核心变更 | 掼蛋"占座转入座"调用点统一走 `SitDownStateService` 提供的表级锁路径，消除占座 → 入座的并发竞争 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git -C dx-game-guandan revert da6e9dfad`；注意与 054 (GdSitDownStateService) 是先后两步 |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-052：入座 R-05/R-06/S-11 BaseUserSitDownHandler/onlyCheck 标注 @Deprecated + 收敛入座日志

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-052 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `8f8ba8d249f72fb7e97d0d1f74b126d47953bea5` |
| 关联文档 | `02-入座-重构设计.md` §4 R-05/R-06/S-11 |
| 变更范围 | `UserSitDownCommand.java`、`UserSitDownReqDto.java`、`BaseUserSitDownCheckService.java`、`BaseUserSitDownDefault.java`、`BaseUserSitDownHandler.java` |
| 核心变更 | R-05/R-06：`BaseUserSitDownHandler` 与 `onlyCheck` 标注 `@Deprecated`，引导调用方迁移；S-11：收敛入座链路 info 日志 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 8f8ba8d24` |
| 未知问题 | 后补登记，原作者复核；`@Deprecated` 调用方迁移时机需原作者补充 |

### GIT-20260604-053：入座 新增 IOccupyResitHandler + SitDownStateService 提供 occupyToSitDown 表级锁入口

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-053 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `de520423e02e57c0f05517e0d3069f955d863241` |
| 关联文档 | `02-入座-重构设计.md` §占座转入座 |
| 变更范围 | 新增 `IOccupyResitHandler.java`；扩展 `SitDownStateService.java`（`occupyToSitDown` 表级锁入口） |
| 核心变更 | 提供"占座转入座"统一锁入口；后续 054 由 guandan 侧实现 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert de520423e`；注意级联回退 054 |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-054：入座 新增 GdSitDownStateService + 占座转入座调用点改走 IOccupyResitHandler 表级锁路径（guandan）

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-054 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-guandan 20260615/junk |
| commit / MR | `8b5a0f57ea169a35e8b471e254c931187efb31d7` |
| 关联文档 | `02-入座-重构设计.md` §占座转入座 |
| 变更范围 | 新增 `dx-game-guandan-service/.../sitdown/GdSitDownStateService.java`；修改 `UserSitDownBootstrap.java`、`UserSitDownFinishListener.java` |
| 核心变更 | 掼蛋侧实现 `IOccupyResitHandler`；占座 → 入座调用统一走 `SitDownStateService` 表级锁路径 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git -C dx-game-guandan revert 8b5a0f57e` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-055：入座 优化重构入座（含 RaceUserSitDownDefault 等多文件细化 / 老 Handler 标注 @Deprecated）

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-055 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `d5132f2122ec41df4aee5790b814b47aec278449` |
| 关联文档 | `02-入座-重构设计.md` 全部 |
| 变更范围 | 21 个文件（涉及 `RaceUserSitDownDefault`、所有 Handler 接口/实现、`GameHandleFactory`、`SitDownFlowService/StateService/ValidatorChain` 等） |
| 核心变更 | 大型整合 commit：把前面 R/S 各步骤的接口与实现整合到一起，并对老 Handler 系列做 `@Deprecated` 收敛；commit message 仅写「fix: 优化重构入座」，具体范围需查 diff |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert d5132f212`；改动面广，回退需谨慎 |
| 未知问题 | 后补登记，原作者复核；commit message 过于笼统，建议补充本次具体改造点（与 R/S 编号对应关系） |

### GIT-20260604-056：入座 优化重构入座（新增 SitDownValidator chain 规则细化）

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-056 |
| 任务序号 / 功能 | 2 / 入座 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `3d007014392ba20f51a2fdca42d062be4e662c5a` |
| 关联文档 | `02-入座-重构设计.md` §SitDownValidator 链 |
| 变更范围 | 新增 7 个文件：`chain/SitDownValidatorChain.java`、`validator/ISitDownValidationExtension.java`、`validator/ISitDownValidationRule.java`、`validator/RiskSitDownValidator.java`、`validator/SeatSitDownValidator.java`、`validator/SpecifyKickSitDownValidator.java`、`validator/TableAuthSitDownValidator.java` |
| 核心变更 | 入座校验链规则化：把 specifyKick/seat/tableAuth/risk 4 类校验拆为独立 `ISitDownValidationRule` 实现，便于单独测试与扩展 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 3d0070143`；删除 7 个 validator/chain 文件 |
| 未知问题 | 后补登记，原作者复核；规则链 4 条规则是否对应 02 §设计的具体 R 编号需要原作者补充 |

### GIT-20260604-057~068：进入房间 R-01~R-08 落地（12 条精简登记）

> **后补登记说明（GIT-20260604-057 ~ 068，01 进入房间共 12 条新增；与已有 GIT-20260603-003~008 共同覆盖 01 全部 commit）**：
> 01 进入房间是本批次中规模最大的重构任务，覆盖 R-01 ~ R-08 + 4 个细化 follow-up commit。已有 GIT-20260603-003~008 已登记了 5 个 frame/guandan commit（含设计/计划/Gd 三扩展/进入房间优化等）；本批次补登记 frame 侧 12 个**结构性核心 commit**（不再重复登记 003~008 中已登记的）。
> 因 01 commit message 已较规整且与实现计划任务编号对齐，每条记录采用**精简表格**。
> 未知问题统一标注：「本登记由后补完成，原作者非本人，登记内容由 commit message + 实现计划 + diff 对照推断；准确性请原作者复核」。

### GIT-20260604-057：进入房间 Task 1 字段重命名 isNewRoomUser → alreadyInRoom

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-057 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `b83e425e2c5dd03ad8976947c212be5b8555dd2e` |
| 关联文档 | `01-进入房间-重构设计.md` §7；`01-进入房间-实现计划.md` Task 1 |
| 变更范围 | `EnterRoomContextV2.java`、`EnterBaseTableHandlerDefault.java`、`EnterPrivateTableHandlerDefault.java`、`BaseUserEnterRoomFinishListener.java`、相关 guandan 引用 |
| 核心变更 | `EnterRoomContextV2.isNewRoomUser` 字段全量重命名为 `alreadyInRoom`（含义与命名对齐）；所有引用点同步替换 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert b83e425e2` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-058：进入房间 R-02/R-03 wallet 空值保护 + 收敛进入房间 info 日志

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-058 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `77e0a7e8ce6ec66c3a6e2291e4f2c5d12cc87ca1` |
| 关联文档 | `01-进入房间-重构设计.md` §4 R-02/R-03；`01-进入房间-实现计划.md` Task 3 |
| 变更范围 | `EnterBaseTableHandlerDefault.java` 等 |
| 核心变更 | R-02：`TableUserWallet` / `TableHand` / `raceGlobalConfig` 空值保护；R-03：进入房间 info 日志全部降级 debug |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 77e0a7e8c` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-059：进入房间 Task 5 新增 IEnterRoomValidatorContributor / IEnterRoomHandAssembler 接口

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-059 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `e3c8dd6664b741b6331a2820136c969b38cb50a1` |
| 关联文档 | `01-进入房间-实现计划.md` Task 5 |
| 变更范围 | 新增 `IEnterRoomValidatorContributor.java`、`IEnterRoomHandAssembler.java` |
| 核心变更 | 提供 frame → guandan 扩展点接口，让掼蛋侧能注入校验贡献与手牌装配逻辑 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert e3c8dd666`；注意 064 等 commit 依赖这些接口 |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-060：进入房间 R-07 新增 EnterRoomStateService 表级锁保护 WATCH_USER 写入

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-060 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `2ac8bcb0d56aed80e6a416b8ae5051e6fde021c2` |
| 关联文档 | `01-进入房间-重构设计.md` §4 R-07；`01-进入房间-实现计划.md` Task 7 |
| 变更范围 | 新增 `EnterRoomStateService.java` |
| 核心变更 | 表级锁封装 WATCH_USER 写入路径；与 02 SitDownStateService、08 RiskTableSnapshot 配套构成完整桌级状态收敛 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 2ac8bcb0d` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-061：进入房间 R-05 新增 EnterRoomValidatorChain + check() 委托校验链

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-061 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `7d8999dd1f7a74d65e9202e787ce3d74bbdce0f7` |
| 关联文档 | `01-进入房间-重构设计.md` §4 R-05；`01-进入房间-实现计划.md` Task 6 |
| 变更范围 | 新增 `EnterRoomValidatorChain.java`；修改 `EnterBaseTableHandlerDefault.check()` |
| 核心变更 | 进入房间 5 类校验抽出为可扩展校验链；通过 `IEnterRoomValidatorContributor` 允许掼蛋扩展校验 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 7d8999dd1` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-062：进入房间 R-06 新增 EnterRoomSnapshotAssembler 含 R-02 wallet 空值保护

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-062 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `6556c6ccf608b961876eddd04440da8a7ad723e0` |
| 关联文档 | `01-进入房间-重构设计.md` §4 R-06；`01-进入房间-实现计划.md` Task 8 |
| 变更范围 | 新增 `EnterRoomSnapshotAssembler.java` |
| 核心变更 | 进入房间响应快照装配抽出独立 Assembler；wallet 等空值保护内置 |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 6556c6ccf` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-063：进入房间 R-04 新增 EnterRoomFlowService + handleData 委托 Flow 编排

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-063 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `d5902b225ff494c3a6612f7a29e15fcf28b7ba0c` |
| 关联文档 | `01-进入房间-重构设计.md` §4 R-04；`01-进入房间-实现计划.md` Task 9 |
| 变更范围 | 新增 `EnterRoomFlowService.java`；修改 `EnterBaseTableHandlerDefault.handleData()` |
| 核心变更 | 进入房间编排服务：组合 StateService + Snapshot + 风控初始化等步骤；Handler 委托 FlowService |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert d5902b225` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-064：进入房间 R-08 异常带出从事件监听剥离 after() 直接同步调用

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-20260604-064 |
| 任务序号 / 功能 | 1 / 进入房间 |
| git 分支 | dx-game-frame 20260615/junk |
| commit / MR | `57f4d02a3b16ca1d11d14603f247d4b6047cd94c` |
| 关联文档 | `01-进入房间-重构设计.md` §6 R-08；`01-进入房间-实现计划.md` Task 11 |
| 变更范围 | `EnterBaseTableHandlerDefault.after()`、`BaseUserEnterRoomFinishListener.java` |
| 核心变更 | R-08：异常带出从 listener 剥离，after() 中直接同步调用（避免 Spring Event 异步吞异常导致带出失败静默） |
| 验证结果 | 未验证 / 审核状态：未审核 |
| 回退方式 | `git revert 57f4d02a3` |
| 未知问题 | 后补登记，原作者复核 |

### GIT-20260604-065 ~ 068：进入房间 4 个 "优化重构入座" follow-up commit

| 记录编号 | commit | 备注 |
|---|---|---|
| GIT-20260604-065 | `ba7fe6d43e69ea4a365ff65c9124c05f2ad151b7` | "重构：进入房间优化" follow-up #1 |
| GIT-20260604-066 | `43a732700ed336c8212c8c0ae0618f04ec33862d` | "重构：进入房间优化" follow-up #2 |
| GIT-20260604-067 | `4a98023b2404e94862e585a8a1587c53ba51c067` | "重构：进入房间优化" follow-up #3 |
| GIT-20260604-068 | `506f2952ae9f1fdb3910b7419b0fdf37498a2117` | "重构：进入房间优化" follow-up #4 |

> 这 4 个 commit 的 message 笼统（仅"重构：进入房间优化"），具体改造点需查 diff 推断；属于 R-01~R-08 核心 commit 之后的细化与 polish。回退方式：`git revert <hash>`；改动面广建议链式回退。统一未知问题：commit message 过于笼统、原作者非本人、需原作者补充对应 R 编号或具体 polish 内容。

## 五、变更记录模板

### GIT-YYYYMMDD-001：变更标题

| 字段 | 内容 |
|---|---|
| 记录编号 | GIT-YYYYMMDD-001 |
| 日期 | YYYY-MM-DD |
| 任务序号 / 功能 | 例如：1 / 进入房间 |
| 关联文档 | `xx-功能.md`<br>`xx-功能-重构设计.md`<br>`xx-功能-实现计划.md` |
| git 分支 | 待补充 |
| commit / MR | 待提交 / commit hash / MR 地址 |
| 变更范围 | 待补充涉及模块、类、接口、配置、测试 |
| 核心变更 | 1. 待补充<br>2. 待补充<br>3. 待补充 |
| 验证结果 | 待补充编译、单测、回归、日志、人工验证结果 |
| 审核状态 | 未审核 |
| 回退方式 | 待补充 revert commit、回滚文件、关闭开关或恢复旧实现 |
| 回退影响 | 待补充回退后会影响的功能、协议、状态或数据 |
| 未知问题 | 待补充尚未确认、尚未验证、依赖外部条件的问题 |

## 六、记录要求

- 不允许只写“优化”“重构”“修复问题”这类无法审核的描述。
- `核心变更` 必须写清楚实际代码行为变化，不能只写文件名。
- `验证结果` 必须写明执行过什么验证；未验证必须写 `未验证` 和原因。
- `回退方式` 必须能被执行，不能只写“回滚代码”。
- `未知问题` 必须保留，后续关闭时要补充关闭依据。
- 如果一个 commit 涉及多个任务，必须拆成多条记录分别描述影响范围。

## 七、示例

### 示例：进入房间编排服务拆分（不入索引）

| 字段 | 内容 |
|---|---|
| 记录编号 | 示例，不作为正式记录 |
| 日期 | 2026-06-04 |
| 任务序号 / 功能 | 1 / 进入房间 |
| 关联文档 | `01-进入房间.md`<br>`01-进入房间-重构设计.md`<br>`01-进入房间-实现计划.md` |
| git 分支 | 20260615/junk |
| commit / MR | 待提交 |
| 变更范围 | `dx-game-frame` 进入房间默认处理链路；`dx-game-guandan` 进入房间扩展实现 |
| 核心变更 | 1. 将进入房间主流程从 Handler 拆到 FlowService<br>2. 将校验逻辑收敛到 ValidatorChain<br>3. 将状态写入和快照装配拆成独立服务 |
| 验证结果 | 未验证，等待实现完成后补充编译、单测和协议回归 |
| 审核状态 | 未审核 |
| 回退方式 | revert 对应 commit；恢复 Handler 直接编排旧流程；删除新增 FlowService / ValidatorChain / SnapshotAssembler 注入点 |
| 回退影响 | 回退后进入房间重构能力失效，但协议行为应恢复到改造前 |
| 未知问题 | 是否完全覆盖私人房、俱乐部、赛事、重连等所有入口，需回归确认 |

## 八、Phase 3 B 组实施编码变更记录（2026-06-05）

> 本批为 B 组(及修复 A 组遗留)的实施编码。统一说明：**验证结果**=未编译验证（本环境无 java/maven），静态评审 + 对 origin/20260615/dev 基线核对 + 与调用点签名核对，待 IDE 编译/回归；**审核状态**=未审核；**回退方式**=`git revert <commit>` 或删除新增类/恢复旧调用。

| 记录编号 | 任务序号/功能 | 工程 | commit | 核心变更 | 类型 |
|---|---|---|---|---|---|
| GIT-20260605-001 | 02 入座 R-09(P0编译修复) | frame | `480366d57` | 补建缺失 `SitDownStateService`(表级 ReentrantLock + 回调 IOccupySitDownHandler)，修占座转入座编译断裂 | 缺类修复 |
| GIT-20260605-002 | 02 入座 审核补正 | guandan(doc) | `1bc07da05` | 02 结果审核补 R-6（记录上述 P0 及修复） | 文档 |
| GIT-20260605-003 | 09 实时账单 R-01/04/05 | guandan | `e38368151` | 3005 主块失败抛出走错误响应 + playAttributes 空值兜底 + 旁观/踢人附加块各自兜底 + 请求日志降 debug | 安全修复 |
| GIT-20260605-004 | 03 带入 R-02 | frame | `8a631b459` | UserBringInDefault 占座转入座(:677)改走 SitDownStateService 表级锁 + @Resource protected 字段 | 并发修复 |
| GIT-20260605-005 | 03 带入 R-02 | guandan | `0476ad641` | UserBringInBootstrap 占座转入座(审核PASS/普通带入 2 处)改走表级锁 | 并发修复 |
| GIT-20260605-006 | 03 带入 R-04 | frame | `7224609aa` | 新增 `ReviewWalletAmount` 审核单钱包金额内部视图(bringInAmount→GUANDAN/bringInSquidAmount→GD_BONUS) | additive 视图 |
| GIT-20260605-007 | 05 带出 R-02 | frame | `525947e0b` | UserBringOutDefault tableHand 空值兜底修入口链式 NPE(:52-54/:83) | NPE 修复 |
| GIT-20260605-008 | 15 在线状态恢复 R-01 | guandan | `23cb2619d` | GdUserOnlineStatusQueryCommand UserTableItem 空值兜底(当前用户默认在线/遍历缺失跳过) | NPE 修复 |
| GIT-20260605-009 | 16 固定带入审核 R-02(P0) | guandan | `32d7c033f` | 恢复 `needAmountApply \|\| hasPendingTransferAudit` keep 判断，修待审核用户被补码超时强制站起 | 行为修复 |
| GIT-20260605-010 | 10 私人房申请审核 R-01 | frame | `5f82992b6` | AmountApplyDefault.check 加 tableInfo/userItem 空值资格守卫，防 NPE/脏审核单 | 安全修复 |
| GIT-20260605-011 | 收尾 / 待确认清单 | guandan(doc) | `53361ed58` | 新增全量待确认清单(BLK-1~6 阻塞型 + 产品/客户端/技术 + 潜在 bug) | 文档 |

### 协议影响

以上代码变更**均保持协议号/请求/响应/通知 DTO 字段 0 改动**（19 的 riskTypeList 为既有 A 组改动，不在本批）；行为变化项（09 主块失败→错误响应、16 keep 判断扩大、02 入座限流/HALL拒绝、05/15 兜底值）均已在 [待确认清单](Junk-游戏准备重构-待确认清单.md) 登记，待产品/客户端确认。

### 剩余未编码（结构性第二波，待编译环境+产品拍板）

03 R-01 BringInScene / R-03 审核 Redis CAS；10 建单失败补偿+calc；11 BringInAudit 全服务族；16 PrivateFixedBringInAuditPolicy；14 ReconnectIntentResolver；17 GiveUpTransferCommand(1042 阻塞)。详见各 `xx-实现计划.md` 与待确认清单。
