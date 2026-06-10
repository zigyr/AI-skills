# policies/ — 全局策略层

## 定位

`policies/` 定义跨页面的**全局约束规则**。grammar 控制单页行为，policy 控制多页之间的协调关系。

policy 对 orchestrator 具有约束力——任何页面生成必须在 policy 限定的边界内运行。

## 目录

```
policies/
├── narrative-policy.md      (待编写)
├── rhythm-policy.md         (待编写)
└── visual-policy.md         (待编写)
```

---

## 三大策略维度

### 1. 叙事策略（Narrative Policy）

控制演示文稿的**故事线**，对应 orchestrator 定义的叙事流规则：

- **渐进式叙事** — 保持故事推进，避免静态重复
- **幻灯片类型交替** — 交替使用不同类型以产生认知变化
- **自然过渡** — 确保每张幻灯片自然导向下一张
- **推荐叙事弧结构** — Problem → Insight → Evidence → Solution → Decision
- **受众适配** — 根据受众类型调整证据密度和语言风格

### 2. 节奏策略（Rhythm Policy）

控制页面间的**信息密度交替**：

- 连续高密度页面上限
- 呼吸页插入频率（引用页 / 过渡页 / 全屏视觉页）
- 章节级视觉断点规则
- 认知动量管理 — 逐步收窄模糊度，随时间增加清晰度

### 3. 视觉策略（Visual Policy）

控制全局**视觉一致性**，对应 orchestrator 的 Visual Consistency Policy：

- **字体约束** — 每个演示文稿最多使用 2 个字体系列
- **色彩约束** — 1–2 个主色 + 中性色板
- **对齐约束** — 严格的网格系统
- **间距约束** — 一致的页边距和节奏
- **图表约束** — 所有可视化元素统一风格配置

一致性降低认知负荷，提升可读性。

---

## Policy 与 Grammar 的区别

| | Grammar | Policy |
|------|---------|--------|
| 作用域 | 单页 | 跨页 |
| 定义内容 | 页面类型的认知协议 | 多页协调的约束规则 |
| 触发时机 | orchestrator 分配页面语法后 | 全程持续生效 |
| 内容来源 | Slide Grammar Library | Narrative Flow Rules + Visual Consistency Policy |

Policy 是 grammar 的上层约束——grammar 在 policy 限定的边界内定义页面行为。
