# 04-GitHub 管线与门禁

> 目标：让 AI 产出进入团队工程秩序。可信度不来自“AI 说完成了”，而来自 spec、测试、Git、workflow、PR、人审组成的系统。

---

## 1. 标准流转

```text
Issue
  └── spec PR
        └── test PR
              └── refactor PR
                    └── CI
                          └── review
                                └── merge
                                      └── gray release
                                            └── observe
```

---

## 2. PR 类型

| PR 类型 | 内容 | 禁止 |
|---|---|---|
| spec PR | 只改 spec、行为矩阵、验收标准 | 不改代码 |
| test PR | 只补特征测试、测试工具、mock | 不重构 |
| refactor PR | 只做等价重构 | 不修业务 bug |
| bugfix PR | 只修明确 bug | 不夹带结构重构 |
| observe PR | 只补日志、指标、灰度开关 | 不改业务语义 |

---

## 3. Required Checks

| Check | 拦截目标 |
|---|---|
| 编译 | 语法、依赖、签名错误 |
| 单元测试 | 规则、validator、assembler |
| 特征测试 | 旧行为等价 |
| 集成测试 | 协议、钱包、MQ、Redis |
| lint / style | 低级格式和静态问题 |
| DTO 兼容检查 | 请求、响应、通知字段破坏 |
| 变更记录检查 | PR 是否关联功能、R 项、回滚方式 |

### 没有自动化环境时

没有编译和测试环境时，PR 状态只能是 `BLOCKED`。允许提交纯文档、测试草案和环境修复；禁止提交未经验证的生产代码。

---

## 4. PR 审核清单

```text
审核
├── spec 是否已通过
├── 是否有已运行通过的特征测试
├── 协议号 / DTO / 通知是否 0 破坏
├── 是否只改当前功能
├── 是否只实现当前 R 项
├── 缓存 / RPC / MQ / 通知副作用是否一致
├── 并发 / 幂等是否考虑
├── 是否有回滚方式
└── 是否更新变更记录
```

---

## 5. 分支策略

| 分支 | 用途 |
|---|---|
| `dev` | 生产等价对比基线 |
| `junk/spec/{功能}` | spec 和验收标准 |
| `junk/test/{功能}` | 特征测试 |
| `junk/refactor/{功能}-{R项}` | 小步重构 |
| `junk/bugfix/{功能}-{问题}` | 明确 bugfix |

---

## 6. Commit 规范

```text
junk(02-sitdown): add characterization test for occupy-to-sitdown
junk(02-sitdown): R-01 keep occupy state transition equivalent
junk(03-bringin): R-02 add wallet null guard without DTO change
junk(09-billing): R-03 extract billing snapshot assembler
```

### commit 禁止项

| 禁止 | 原因 |
|---|---|
| `优化重构` | 无法追溯 |
| `fix` | 不知道修什么 |
| 一个 commit 改多个功能 | 无法回滚 |
| 自动格式化全仓 | diff 污染 |
| 混入旧资料整理 | 影响审核焦点 |

---

## 7. 上线门禁

| 门禁 | 要求 |
|---|---|
| 发布范围 | 功能、空间类型、俱乐部、桌子、代理维度可控 |
| 灰度开关 | 高风险链路必须支持旧 flow 或快速回滚 |
| 指标 | 成功率、错误码、耗时、NPE、MQ 失败、钱包失败 |
| 日志 | tableId、userId、proto、R 项标识，不打大对象 |
| 回滚 | revert 步骤、配置开关、数据补偿方式 |
| 观察期 | P0/P1 至少灰度观察后再扩大 |

## 8. 自动提交边界

AI 可以自动执行：

- 创建任务分支、运行验证、提交原子 commit、更新状态表。
- 为独立且验证通过的 R 项创建 PR 草稿。
- 修复由测试明确定位的局部问题。

AI 必须阻塞并等待人工：

- 合并主干、发布、修改生产数据、执行不可逆操作。
- 决定产品语义、协议废弃、资金口径、风控策略。
- 绕过 required check 或接受失败测试。
