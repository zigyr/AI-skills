---
name: ppt-system
description: >
  分层 AI PPT 生成操作系统。将演示文稿设计形式化为显式的认知、叙事和视觉规则，
  通过 7 阶段编排产出结构化、叙事连贯、视觉统一的幻灯片。
  Use when user asks to "create PPT", "make presentation", "生成PPT", "做PPT", 
  "制作演示文稿", "设计幻灯片", or provides content to turn into a slide deck.
---

# PPT System — 分层 PPT 生成操作系统

> **核心命题：演示文稿设计可以形式化。** 不依赖 LLM 的隐式审美直觉，而是通过显式的认知分层、叙事规则和视觉策略，产出结构化、可信赖的演示文稿。

## 何时激活

- 用户要求创建 PPT / 演示文稿 / 幻灯片
- 用户提供了内容（文字/文档/数据），需要转化为 slide deck
- 用户要求分析或改进现有演示文稿的结构
- 用户提到"ppt-system"

## 与其他 PPT Skill 的关系

| Skill | 定位 | 与本系统的关系 |
|-------|------|--------------|
| `ppt-master` | 多角色 SVG→PPTX 完整 pipeline（含 Python 脚本） | 重武器——适合有明确源文档、需精确控制每页像素的场景 |
| `guizang-ppt-skill` | 网页翻页 PPT（杂志风/瑞士风） | 轻量级——适合快速出稿、网页展示 |
| **`ppt-system`** (本系统) | **认知编排层** | **中量级——适合需要叙事设计、结构严谨、视觉一致的专业演示** |

`ppt-system` 不绑定特定渲染技术。它通过路由层调度 `frontend-slides` / `taste-skill` / `frontend-polish` 等外部 skill 完成实际生成。

---

## 执行约束（硬规则）

> **以下规则优先级最高。违反任何一条即为执行失败。**

1. **先叙事，后视觉** — 叙事未稳定前，禁止进入视觉加工
2. **先语法，后布局** — 页面 grammar 类型未分配前，禁止布局生成
3. **全程维护视觉一致性** — 字体 ≤2 字族、色彩 1-2 主色+中性色板、严格网格
4. **一页一核心** — 每张幻灯片只传达一个信息
5. **禁止段落文本** — 幻灯片不是文档，不接受密集段落

---

## 工作流（7 阶段 Pipeline）

### 阶段 1：需求分析
**目标**：解析用户意图、受众、风格偏好、场景

**动作**：
1. 从用户输入中提取：主题、受众类型（高管/技术/投资/通用）、风格关键词、页数期望
2. 读取 `references/slide-patterns.md` 获取风格认知——将用户的关键词映射到具体的设计参考（如"科技风"→深背景+高对比+大留白）
3. 读取 `references/storytelling-notes.md` 获取叙事理论基础
4. 输出：**一页需求简报**（受众 / 风格方向 / 页数预估 / 叙事弧类型）

**⛔ 阻塞点**：如用户需求模糊（无主题、无受众、无风格），向用户确认后再继续。

---

### 阶段 2：叙事规划
**目标**：确定叙事弧和页面序列

**动作**：
1. 读取 `policies/narrative-policy.md` — 获取叙事流规则和受众适配表
2. 读取 `policies/rhythm-policy.md` — 获取密度交替和呼吸页规则
3. 规划叙事弧：**Problem → Insight → Evidence → Solution → Decision**（或根据演示类型调整变体）
4. 确定页面序列：每页标注叙事角色（Introduction / Explanation / Comparison / Persuasion / Transition / Summary / Emphasis）
5. 验证：检查密度交替（连续 Medium+ ≤2）、呼吸页频率（每 4 页至少 1 个）、叙事推进性（无静态重复）

**输出**：**页面序列大纲**（每页的叙事角色 + 核心信息 + 密度级别）

---

### 阶段 3：语法分配
**目标**：为每页匹配 grammar 类型

**动作**：
1. 读取 `grammars/readme.md` — 了解 5 种 grammar 类型概览
2. 根据每页的叙事角色，从 Slide Grammar Library 中匹配类型：

| 叙事角色 | 推荐 Grammar |
|---------|-------------|
| Introduction / Emphasis | → `grammars/quote-emphasis-slide.md` |
| Comparison | → `grammars/comparison-slide.md` |
| Explanation / Process | → `grammars/process-slide.md` |
| Persuasion / Evidence | → `grammars/metrics-slide.md` |
| Explanation / Model | → `grammars/framework-model-slide.md` |

3. 对每页，读取对应的 grammar 文件，提取：Use Case / Layout Pattern / Content Constraints / Visual Expectations / Avoid
4. 验证：检查 grammar 类型交替（最多连续 2 页同类型）

**输出**：**每页的 grammar 分配表**（页码 + grammar 类型 + 核心约束摘要）

---

### 阶段 4：布局生成
**目标**：将每页的 grammar 协议转化为实际幻灯片

**动作**：
1. 读取 `policies/visual-policy.md` — 获取字体、色彩、对齐、间距的全局约束
2. 读取 `routing/grammar-skill-routing.md` — 查表确定每页应调度的 skill
3. 按页面顺序，逐页生成：
   a. 调用 `frontend-slides` 生成 HTML/SVG 骨架
   b. 应用 grammar 的 Layout Pattern（如 50/50 并排、步骤流、大数字聚焦）
   c. 应用 visual-policy 的约束（字体层级、色彩预算、网格对齐）
4. 生成过程中保持 policy 约束——字体不超过 2 个家族，色彩在预算内，间距遵循限定比例

**输出**：**所有页面的 HTML/SVG 初稿**

---

### 阶段 5：视觉精修
**目标**：美学打磨，确保视觉质量

**动作**：
1. 调用 `taste-skill` 逐页审查视觉质量
2. 调用 `frontend-polish` 微调间距、层级、留白
3. 重点检查：
   - Quote/Emphasis 页：焦点是否绝对清晰？是否有干扰元素？
   - Metrics 页：数字是否秒级可读？视觉层级是否正确？
   - Comparison 页：两侧是否视觉平衡？差异是否直观？
   - Process 页：方向感是否明确？步骤间关系是否清晰？
   - Framework/Model 页：结构是否可瞬间辨识？关系连线是否干净？

**输出**：**精修后的所有页面**

---

### 阶段 6：一致性检查
**目标**：跨页校验，确保整份演示文稿视觉统一

**动作**：
1. 读取 `policies/visual-policy.md` 逐条对照检查：
   - 字体：所有页面使用同一套字体层级？（标题同字号、正文同字号）
   - 色彩：所有页面使用同一套色彩？无越界色值？
   - 对齐：所有页面使用同一套边距和网格？
   - 间距：所有页面使用同一套间距比例？
   - 图表：所有数据可视化的样式统一？
2. 检查 grammar 约束：每页是否遵守了其 grammar 的 Content Constraints 和 Avoid 规则？
3. 检查叙事一致性：页面间过渡是否自然？叙事线是否完整？
4. 违规项 → 回到阶段 4 或 5 修复

**输出**：**一致性检查报告 + 修复确认**

---

### 阶段 7：导出渲染
**目标**：输出最终交付格式

**动作**：
1. 确定目标格式（PPTX / PDF / HTML / 图片序列）
2. 如需要 PPTX：调用 `ppt-master` 的导出能力，或直接使用生成的 SVG/HTML 组装
3. 如需要网页展示：直接使用 `frontend-slides` 的输出
4. 确认所有页面可导出（无缺失资源、无格式冲突）

**输出**：**最终演示文稿文件**

---

## 快速模式

当用户只需快速草稿（非正式演示）时，可启用快速模式：

1. 跳过阶段 5 的 taste-skill 审查
2. 阶段 6 仅检查关键一致性（字体、色彩），跳过间距和图表细节
3. 不读取完整的 grammar 文件——仅使用 readme 中的摘要信息

**触发**：用户说"快速出稿" / "先出个草稿" / "quick draft"

---

## 文件索引

| 层 | 路径 | 何时读取 |
|----|------|---------|
| 编排器 | `orchestration/ppt-orchestrator.md` | 阶段 1（了解完整哲学） |
| 策略 | `policies/narrative-policy.md` | 阶段 2 |
| 策略 | `policies/rhythm-policy.md` | 阶段 2 |
| 策略 | `policies/visual-policy.md` | 阶段 4、6 |
| 语法 | `grammars/comparison-slide.md` | 阶段 3（按需） |
| 语法 | `grammars/process-slide.md` | 阶段 3（按需） |
| 语法 | `grammars/metrics-slide.md` | 阶段 3（按需） |
| 语法 | `grammars/quote-emphasis-slide.md` | 阶段 3（按需） |
| 语法 | `grammars/framework-model-slide.md` | 阶段 3（按需） |
| 路由 | `routing/grammar-skill-routing.md` | 阶段 4 |
| 参考 | `references/slide-patterns.md` | 阶段 1 |
| 参考 | `references/storytelling-notes.md` | 阶段 1、2 |

---

## 设计原则

- **认知分层，层间松耦合** — 每层职责正交，通过 orchestrator 串联
- **设计形式化** — 将高价值设计认知显式写入 references 和 policies
- **能力原子化** — 每个 skill 专注单一能力维度，通过 routing 组合
- **约束优先于生成** — policy 和 grammar 限定边界，skill 在边界内自由发挥
