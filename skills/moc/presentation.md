# Presentation — MOC

Presentation 分类下的技能索引。

---

## ppt-system

- **来源**: `normalized/ppt-system`
- **定位**: 分层 AI PPT 生成操作系统——将演示文稿设计形式化为显式的认知、叙事和视觉规则
- **核心能力**: 分阶段编排 / 页面语法协议 / 全局策略约束 / 设计知识注入 / 多 skill 路由调度
- **入口**: [`SKILL.md`](../normalized/ppt-system/SKILL.md) — Claude Code 可直接调用的 skill 入口
- **文档**: [`readme.md`](../normalized/ppt-system/readme.md) — 系统架构说明
- **部署**: 复制或软链接到 `~/.claude/skills/ppt-system/` 即可通过 `/ppt-system` 调用
- **打包**: [`runtime/ccswitch/ppt-system.zip`](../../runtime/ccswitch/ppt-system.zip) — 可直接 unzip 部署

### 子系统

| 子系统 | 路径 | 功能 |
|--------|------|------|
| Orchestrator | [orchestration/](../normalized/ppt-system/orchestration/readme.md) | 7 阶段中央调度器 |
| Policies | [policies/](../normalized/ppt-system/policies/readme.md) | 叙事/节奏/视觉全局约束 |
| Grammars | [grammars/](../normalized/ppt-system/grammars/readme.md) | 5 类页面认知协议 |
| Routing | [routing/](../normalized/ppt-system/routing/readme.md) | grammar → skill 解耦映射 |
| Skills | [skills/](../normalized/ppt-system/skills/readme.md) | 外部 skill 引用层 |
| References | [references/](../normalized/ppt-system/references/readme.md) | 设计理论与风格知识库 |

---

## 关联 Skills（外部）

ppt-system 引用但不复制以下独立 skill：

| Skill | 在 ppt-system 中的角色 |
|-------|----------------------|
| `ppt-master` | 多角色 SVG→PPTX pipeline |
| `guizang-ppt-skill` | 网页翻页 PPT（杂志风/瑞士风） |
| `frontend-slides` | HTML 幻灯片生成 |
| `taste-skill` | 美学判断与视觉优化 |
| `frontend-polish` | 间距/层级/留白微调 |
| `storytelling-skill` | 叙事结构与节奏设计 |
| `impeccable` | 前端界面审查与打磨 |
