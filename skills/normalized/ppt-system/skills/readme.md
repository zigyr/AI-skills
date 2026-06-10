# skills/ — 执行能力层

## 定位

`skills/` 是实际执行生成的能力单元。它接收 orchestrator 的调度指令，在 grammar 协议和 policy 约束下，产出具体页面。

ppt-system 的 skills 层**不重新实现**生成能力，而是引用和编排外部已注册的 Claude Code skills。

## 目录

```
skills/          (当前为空，待注册子 skill)
```

---

## 外部 Skill 引用

以下为 orchestrator 路由表直接引用的 skill：

| 外部 Skill | 在 ppt-system 中的角色 | 路由触发条件 |
|------------|----------------------|-------------|
| `storytelling-skill` | 叙事结构与节奏设计 | 需要叙事线规划时 |
| `frontend-slides` | HTML/SVG 幻灯片生成 | 需要从 grammar 协议渲染页面时 |
| `taste-skill` | 美学判断与视觉优化 | 需要风格一致性审查和视觉质量评估时 |
| `frontend-polish` | 间距/层级/留白微调 | 需要对齐精度和字体层级打磨时 |

## 扩展 Skill 池

以下 skill 虽未直接列于 orchestrator 路由表，但可被 routing 层按需引用：

| 外部 Skill | 潜在角色 |
|------------|---------|
| `ppt-master` | 多角色 SVG→PPTX 完整 pipeline（替代方案） |
| `guizang-ppt-skill` | 网页翻页 PPT（杂志风/瑞士风） |
| `impeccable` | 前端界面审查与打磨（taste-skill 的替代/补充） |

---

## 注册新 Skill

当新的外部 skill 要接入 ppt-system：

1. 在 [routing/](routing/readme.md) 层添加需求 → skill 映射
2. 在此目录下创建 `{skill-name}.md`，记录：
   - skill 来源与版本
   - 接入方式（直接调用 / 适配器包装）
   - 适用 grammar 类型
   - 输入/输出约定
3. 更新 MOC 索引

---

## 设计原则

- **能力原子化** — 每个 skill 专注一个能力维度，复杂任务通过 orchestrator 组合多个 skill
- **不重复实现** — 优先引用外部成熟 skill，不做功能重复
- **通过路由解耦** — skill 不直接绑定 grammar，新增/替换 skill 只需更新 routing 表
