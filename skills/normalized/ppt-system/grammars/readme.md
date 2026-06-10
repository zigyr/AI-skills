# grammars/ — 页面认知协议层

## 定位

`grammars/` 定义每种幻灯片类型的**认知协议**——不规定具体视觉布局，而是描述该页面的叙事目的、信息密度上限、认知目标和约束条件。

grammar 是 orchestrator 与 skills 之间的契约：orchestrator 指定页面语法类型，skills 在语法约束下执行生成。

## 目录

```
grammars/
├── comparison-slide.md          # 对比页
├── process-slide.md             # 流程页（含 timeline 变体）
├── metrics-slide.md             # 数据页
├── quote-emphasis-slide.md      # 引用/强调页（含 hero 变体）
├── framework-model-slide.md     # 框架/模型页
├── hero-slide.md                → 已迁移至 quote-emphasis-slide.md
├── timeline-slide.md            → 已迁移至 process-slide.md
└── readme.md
```

---

## Slide Grammar Library（语法库）

来源于 orchestrator 定义的标准化可复用幻灯片类型：

---

## Grammar 模板结构

每个 grammar 定义四个维度：

| 维度 | 说明 |
|------|------|
| Use Case | 使用场景——该页面类型解决什么问题 |
| Layout Pattern | 布局模式——自然的布局倾向 |
| Content Constraints | 内容约束——信息密度上限和内容形式限制 |
| Visual Expectations | 视觉期望——该页面类型应达成的视觉效果 |

---

## 已定义 Grammar

### 1. Comparison（对比页）

- **Use Case** — 对比两种方案、产品、数据或观点
- **Layout Pattern** — 50/50 并排布局，每侧项目数最小化
- **Content Constraints** — 对比维度 3–5 个，每侧等量
- **Visual Expectations** — 清晰的视觉分割，差异一目了然

### 2. Process（流程页）

- **Use Case** — 展示顺序步骤、操作流程或阶段推进
- **Layout Pattern** — 步骤流布局，箭头 / 编号 / 时间轴
- **Content Constraints** — 每步 1 个核心动作 + 精简说明
- **Visual Expectations** — 方向感明确，步骤间关系清晰

### 3. Metrics（数据页）

- **Use Case** — 呈现关键指标、量化证据或业绩数据
- **Layout Pattern** — 大数字聚焦布局，单一主导 KPI
- **Content Constraints** — 最多 3 个核心指标，数字突出，文本最小化
- **Visual Expectations** — 数字成为视觉主角，秒级可读

### 4. Quote / Emphasis（引用/强调页）

- **Use Case** — 突出单一关键陈述、引用或核心观点
- **Layout Pattern** — 全屏文本或图像叠加布局
- **Content Constraints** — 1 条核心语句，可选 1 个背景视觉辅助
- **Visual Expectations** — 强焦点，无干扰，情绪锚定

### 5. Framework / Model（框架/模型页）

- **Use Case** — 呈现概念模型、分析框架或理论结构
- **Layout Pattern** — 层级图示布局
- **Content Constraints** — 框架节点 3–5 个，关系明确
- **Visual Expectations** — 结构清晰，层次分明

---

## Grammar 与 Skill 的关系

grammar 不直接调用 skill，而是通过 [routing/grammar-skill-routing.md](../routing/readme.md) 查表将 grammar 类型映射到具体执行 skill。

```
grammar → routing 查表 → skill 执行
```

## 设计原则

- **定义"做什么"，不定义"怎么做"** — grammar 描述认知目标，skill 负责视觉实现
- **一页一类型** — 每张幻灯片只分配一个 grammar 类型
- **在 policy 边界内运行** — grammar 的布局倾向受 policies 的全局视觉策略约束
