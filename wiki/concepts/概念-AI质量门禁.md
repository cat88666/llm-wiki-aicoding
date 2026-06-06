# 概念：AI 质量门禁

## 一、定义

AI 质量门禁是把 AI 产出放进确定性的工程轨道：

```
issue → branch → commit → PR → CI → required check → 人审 → merge
```

它解决的不是“AI 会不会犯错”，而是“犯错能不能被拦住、定位、回退”。

## 二、门禁分层

| 层级 | 门禁 | 拦截目标 |
|---|---|---|
| 本地 | lint、类型检查、局部测试 | 低级错误和本次改动行为 |
| CI | 全量测试、特征测试、构建 | 主干回归 |
| PR | 模板、diff、人审 | 范围失控、语义错误、兼容风险 |
| 仓库保护 | required check、branch protection | 红灯合并 |
| 发布 | stage、冒烟、回滚方案 | 线上风险 |

## 三、为什么 workflow 比口头规范强

| 口头规范 | workflow |
|---|---|
| “最好跑测试” | 测试不通过不能合 |
| “PR 不要太大” | 模板要求范围和回退说明 |
| “AI review 过了” | deterministic check 过了才进入人审 |
| “之后补文档” | PR 检查 spec 是否回写 |

AI review 的标准会随模型漂移；lint、测试、required check 是稳定裁判。

## 四、质量飞轮

```
AI 生成
  └── 测试 / lint / workflow 验证
        └── 失败信息结构化回喂
              └── AI 修正
                    └── 人审裁决
                          └── 规则沉淀进 spec / AGENTS / workflow
```

每次失败都应该转成一条规则、测试或模板项。

## 五、最小闭环

```
最小 AI 工程门禁
├── PR 模板
├── lint
├── test
├── required check
├── 人审
└── 回退方式
```

先有硬闸门，再逐步加安全扫描、性能测试、stage 验证。

## 六、一句话

```
AI 代码必须和人写代码走同一条门禁，没有豁免权。
```
