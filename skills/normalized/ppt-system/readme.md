# ppt-system — PPT 生成操作系统

## 定位

ppt-system 是一个**分层的 AI 演示文稿生成系统**。它将演示文稿设计形式化为显式的认知规则、叙事规则和视觉规则，通过分阶段编排产出结构化、叙事连贯、视觉统一的幻灯片。

核心命题：**演示文稿设计可以形式化**——而非依赖 LLM 的隐式审美直觉。

## 系统架构

```
references      设计理论与风格认知
    ↓
policies        全局约束规则（叙事/节奏/视觉一致性）
    ↓
orchestrator    中央调度器（7 阶段认知 pipeline）
    ↓
grammars        页面认知协议（每页的叙事目的与约束）
    ↓
routing         grammar → skill 解耦映射表
    ↓
skills          执行能力单元
```

## 目录与功能

| 文件夹 | 功能 | 说明 |
|--------|------|------|
| [references/](references/readme.md) | 知识参考层 | 设计模式、叙事理论、风格分析——为 orchestrator 注入设计认知 |
| [policies/](policies/readme.md) | 全局策略层 | 叙事流规则、布局决策规则、视觉一致性策略——跨页面全局约束 |
| [orchestration/](orchestration/readme.md) | 编排层 | 7 阶段 pipeline：需求分析 → 叙事规划 → 语法分配 → 布局生成 → 视觉精修 → 一致性检查 → 导出渲染 |
| [grammars/](grammars/readme.md) | 页面语法层 | 标准化可复用幻灯片类型（Comparison / Process / Metrics / Quote-Emphasis / Framework-Model） |
| [routing/](routing/readme.md) | 路由映射层 | grammar 类型 → 外部 skill 的解耦映射 |
| [skills/](skills/readme.md) | 执行能力层 | 引用外部 Claude Code skills，不做重复实现 |

## 运行流程

```
用户："做一个科技风 AI 行业分析 PPT"

1. references 提供风格认知 → 科技风 = 深背景、高对比、大留白
2. policies 施加全局约束 → 信息密度交替、字体层级上限（≤2 字族）、色彩系统（1-2 主色 + 中性色板）
3. orchestrator 规划叙事线 → Problem → Insight → Evidence → Solution → Decision
4. orchestrator 分配页面语法 → P1=Quote/Emphasis, P2=Framework, P3=Comparison, P4=Metrics, ...
5. routing 查表匹配 skills → Comparison → frontend-slides + taste-skill
6. skills 执行生成 → HTML/SVG 产出
7. orchestrator 校验 → 一致性检查 → 导出 PPTX
```

## 调用方式

### 方法一：注册为 Claude Code Skill（推荐）

将 `ppt-system/` 部署到 Claude Code 的 skills 目录：

```bash
# 创建软链接或复制到 Claude Code skills 目录
cp -r skills/normalized/ppt-system ~/.claude/skills/ppt-system
```

之后在任意对话中输入：

```
/ppt-system 做一个科技风 AI 行业分析 PPT
```

Claude Code 会读取 `SKILL.md` 作为入口，按 7 阶段 pipeline 执行。

### 方法二：直接读取 SKILL.md

在对话中直接引用：

```
请按照 skills/normalized/ppt-system/SKILL.md 的流程，帮我做一个 PPT...
```

### 方法三：分阶段手动驱动

也可以手动按阶段推进——每次只告诉 Claude 当前阶段的指令（如"请根据 narrative-policy.md 为以下内容规划叙事线..."）。

---

## 设计原则

- **先叙事，后视觉** — 叙事未稳定前不进入视觉加工
- **语法在策略内运行** — grammar 定义页面行为，policy 限定全局边界
- **认知分层，层间松耦合** — 每层职责正交，通过 orchestrator 串联
- **设计形式化** — 将高价值设计认知显式写入 references 和 policies，不依赖 LLM 隐式知识
- **能力原子化** — skills 专注单一能力维度，复杂能力通过 orchestrator 组合

## 与外部系统的关系

ppt-system 引用但不复制以下 Claude Code skills：

- `ppt-master` — 多角色 SVG→PPTX 完整 pipeline
- `guizang-ppt-skill` — 网页翻页 PPT（杂志风/瑞士风）
- `frontend-slides` — HTML 幻灯片生成
- `taste-skill` / `impeccable` / `frontend-polish` — 视觉质量打磨
- `storytelling-skill` — 叙事结构与节奏设计
