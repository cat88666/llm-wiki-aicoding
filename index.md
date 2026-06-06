# AI Coding 知识库索引

本仓库围绕“如何让 AI Coding 在真实工程中可靠落地”组织内容。优先阅读 `wiki/` 中已经收敛的知识页；需要课程原文、模板或案例证据时，再进入 `raw/` 与 `artifact/`。

## 推荐阅读路径

```text
AI Coding 工程闭环
  ├── 规格：SDD + 上下文工程与活文档
  ├── 验证：特征测试 + TDD + AI 质量门禁
  ├── 执行：Agent 行为约束 + 小步实施
  └── 复盘：翻车模式与处置 + 30 天落地路线
```

## Concepts

稳定、可复用的核心概念。

- [SDD 规格驱动开发](wiki/concepts/概念-SDD规格驱动开发.md)
- [TDD 红绿循环](wiki/concepts/概念-TDD红绿循环.md)
- [特征测试](wiki/concepts/概念-特征测试.md)
- [上下文工程与活文档](wiki/concepts/概念-上下文工程与活文档.md)
- [Agent 行为约束](wiki/concepts/概念-Agent行为约束.md)
- [AI 质量门禁](wiki/concepts/概念-AI质量门禁.md)

## Summaries

按工程主题组织的学习地图。

- [AI 可靠编程](wiki/summaries/主题-AI可靠编程.md)
- [大项目 AI 安全重构](wiki/summaries/主题-大项目AI安全重构.md)
- [AI 工程化治理](wiki/summaries/主题-AI工程化治理.md)

## Synthesis

跨课程沉淀的执行方法。

- [AI Coding 工程闭环](wiki/synthesis/综合-AICoding工程闭环.md)
- [翻车模式与处置](wiki/synthesis/综合-翻车模式与处置.md)
- [30 天落地路线](wiki/synthesis/综合-30天落地路线.md)

## 原始课程

- [SDD + TDD 驯服 AI 可靠编程课程](raw/01-SDD+TDD驯服AI可靠编程课程/README.md)
- [生产级 AI 安全重构课程](raw/02-生产级AI安全重构课程/README.md)
- [AI 大型项目重构课程视频](raw/03-AI大型项目重构课程视频/README.md)

## 案例与产物

### 失败案例分析

- [生产游戏 AI 重构失败案例分析](artifact/02-失败案例分析/README.md)

### 失败案例

- [生产游戏 AI 重构失败案例：功能拆解](artifact/01-失败案例/01-生产游戏AI重构失败案例/重构功能拆解.md)
- [生产游戏 AI 重构失败案例：进入房间重构设计](artifact/01-失败案例/01-生产游戏AI重构失败案例/具体模块功能重构/01-进入房间-重构设计.md)
- [生产游戏 AI 重构失败案例：进入房间实现计划](artifact/01-失败案例/01-生产游戏AI重构失败案例/具体模块功能重构/01-进入房间-实现计划.md)
- [生产游戏 AI 重构失败案例：进入房间结果审核](artifact/01-失败案例/01-生产游戏AI重构失败案例/具体模块功能重构/01-进入房间-结果审核.md)

### 成功重写

- [生产游戏 AI 重构成功案例](artifact/03-失败案例重写/生产游戏AI重构重写案例/README.md)
- [生产重构总控](artifact/03-失败案例重写/生产游戏AI重构重写案例/00-生产重构总控.md)
- [SDD 规格驱动流程](artifact/03-失败案例重写/生产游戏AI重构重写案例/01-SDD规格驱动流程.md)
- [特征测试与 TDD 流程](artifact/03-失败案例重写/生产游戏AI重构重写案例/02-特征测试与TDD流程.md)
- [小步实施流水线](artifact/03-失败案例重写/生产游戏AI重构重写案例/03-小步实施流水线.md)
- [GitHub 管线与门禁](artifact/03-失败案例重写/生产游戏AI重构重写案例/04-GitHub管线与门禁.md)
- [一次启动自主编排](artifact/03-失败案例重写/生产游戏AI重构重写案例/05-一次启动自主编排.md)
- [生产重构总控 Prompt](artifact/03-失败案例重写/生产游戏AI重构重写案例/prompt/生产重构总控Prompt.md)
