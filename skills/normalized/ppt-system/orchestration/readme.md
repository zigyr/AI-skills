# orchestration/ — 编排层

## 定位

`orchestration/` 是 ppt-system 的中央调度器。它不执行具体页面生成，而是协调完整的 7 阶段认知 pipeline：从需求分析到最终导出。

## 核心文件

### ppt-orchestrator.md

定义完整编排系统，包含以下模块：

---

## 演示文稿哲学

编排器内置四条基础原则，所有阶段均在此框架下运行：

1. **幻灯片不是文档** — 幻灯片是现场沟通的视觉辅助，应支撑演讲者而非替代演讲者
2. **一页一核心** — 每张幻灯片只传达一个信息，多信息则拆分
3. **视觉层级引导注意力** — 字体、对比度、间距和对齐引导认知焦点，留白是功能性设计元素
4. **简洁降低认知负荷** — 避免密集段落，偏好简洁陈述和结构化片段，每张幻灯片应可在 ~1 分钟内被理解

---

## 7 阶段工作流

| 阶段 | 内容 | 说明 |
|------|------|------|
| 1. Requirement Analysis | 需求分析 | 解析用户意图、受众、风格、场景 |
| 2. Narrative Planning | 叙事规划 | 确定叙事线（Problem → Insight → Evidence → Solution → Decision） |
| 3. Slide Grammar Assignment | 语法分配 | 为每页匹配 grammar 类型（Comparison / Process / Metrics / Quote-Emphasis / Framework-Model） |
| 4. Layout Generation | 布局生成 | 根据 grammar 类型决定布局模式，调度 frontend-slides 生成 |
| 5. Visual Refinement | 视觉精修 | 调用 taste-skill / frontend-polish 进行美学打磨 |
| 6. Consistency Checking | 一致性检查 | 跨页色彩/字体/间距/图表风格校验 |
| 7. Export Rendering | 导出渲染 | SVG/HTML → PPTX 或其他目标格式 |

---

## 幻灯片责任系统

每张幻灯片必须承担一个主要功能：

- **Introduction** — 上下文或主题框架
- **Comparison** — 元素间的对比
- **Explanation** — 概念、模型或流程说明
- **Persuasion** — 论点或建议
- **Transition** — 章节间桥梁
- **Summary** — 洞察整合
- **Emphasis** — 突出单一关键陈述

---

## 布局决策规则

| 页面目的 | 布局模式 |
|----------|----------|
| Comparison | 50/50 并排布局 |
| Process | 时间轴 / 步骤流布局 |
| Metrics | 大数字聚焦布局 |
| Emphasis | 全屏文本或图像叠加 |
| Frameworks | 层级图示布局 |

---

## 执行约束（硬规则）

编排器强制执行以下约束，按阶段门控：

1. **叙事未稳定 → 禁止视觉加工**
2. **语法未分配 → 禁止布局生成**
3. **全程维护跨页视觉一致性**
4. **先结构，后设计** — 结构方案确定后才进入视觉阶段

这些约束防止过早优化和生成过程中的风格漂移。
