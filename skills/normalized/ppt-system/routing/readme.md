# routing/ — 路由映射层

## 定位

`routing/` 维护 grammar → skill 的**解耦映射表**。grammar 不硬编码调用哪个 skill，skill 不假设自己被哪种 grammar 调用。路由层是二者之间的唯一耦合点。

## 核心文件

### grammar-skill-routing.md

定义由 orchestrator 的 Skill Routing Rules 派生出的映射关系：

```
能力需求 → 目标 skill
```

---

## 路由规则表

| 需求 | 目标 Skill | 说明 |
|------|-----------|------|
| 叙事结构设计 | `storytelling-skill` | 规划叙事线、段落节奏、信息展开顺序 |
| 美学判断与优化 | `taste-skill` | 视觉质量评估、风格一致性审查 |
| HTML 幻灯片生成 | `frontend-slides` | 将 grammar 协议渲染为 HTML/SVG 页面 |
| 间距/层级/留白微调 | `frontend-polish` | 对齐精度、字体层级、留白比例打磨 |

---

## 路由逻辑

orchestrator 的执行流程：

```
1. 决定页面 grammar 类型（Comparison / Process / Metrics / Quote-Emphasis / Framework-Model）
2. 识别所需能力维度 → 叙事设计 / HTML生成 / 美学打磨 / 布局精修
3. 查 routing 表 → 获取匹配的 skill
4. 考虑全局 policy 约束
5. 调度 skills 执行生成
```

示例：

```
Comparison 页面 → 需要：并排布局 + 差异可视化 + 对比排版
                → 路由至：frontend-slides（生成）+ taste-skill（打磨）

Process 页面   → 需要：步骤流布局 + 箭头/编号 + 时序叙事
                → 路由至：frontend-slides（生成）+ frontend-polish（精修）

Metrics 页面   → 需要：大数字聚焦 + 指标分组 + 最小文本
                → 路由至：frontend-slides（生成）+ taste-skill（打磨）

Emphasis 页面  → 需要：全屏文本 + 视觉锚点 + 强焦点
                → 路由至：frontend-slides（生成）+ frontend-polish（精修）
```

---

## 设计原则

- **松耦合** — 同一 grammar 可路由到不同 skill 组合，同一 skill 可服务多种 grammar
- **可扩展** — 新增 skill 时只需更新路由表，无需修改 grammar 或 orchestrator
- **优先级排序** — 路由表支持主 skill + 备用 skill 的降级逻辑
