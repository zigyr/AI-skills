# AI-skills — 本地 Skill 管理中心

为 Claude Code 提供统一、标准化的 skill 入口。管理原始仓库、标准化版本、运行时工具和分发打包。

---

## 目录结构

```
AI-skills/
├── skills/
│   ├── normalized/          # 自定义标准化版本（统一入口）
│   │   ├── ppt-system/      # 分层 PPT 生成操作系统
│   │   └── pack-skill/      # Skill 工程打包器
│   ├── moc/                 # Map of Content，技能索引/导航
│   │   ├── presentation.md
│   │   └── tools.md
│   └── repos/               # 原始 Git 仓库（只读，git clone/pull 管理）
├── runtime/
│   └── ccswitch/            # 打包好的 skill zip，可直接部署到 ~/.claude/skills/
├── prompts/                 # 提示词暂存与实验
└── readme.md
```

---

## 治理原则

- `skills/repos/` — 只通过 `git clone` / `git pull` 管理，**严禁手动修改**
- `skills/normalized/` — 统一标准化入口，内部是 `SKILL.md` + 分层子文件
- `skills/moc/` — 每次新增或变更 skill，**必须**同步更新 MOC 索引
- `runtime/ccswitch/` — 打包分发的 zip 归档，每个 zip 以 skill 名称命名
- `prompts/` — 临时提示词、实验性 prompt 草稿，非结构化暂存区

---

## Skill 工程化 SOP

> 以下为在 `skills/normalized/` 下从零构建一个多文件 skill 系统的标准方法论。以 `ppt-system` 为参考实现。

### 何时使用多文件架构

满足以下任一条件时，应使用多文件分层架构而非单一 `SKILL.md`：

- Skill 包含**多阶段工作流**（≥3 个阶段）
- Skill 需要**独立的策略/约束层**（规则在生成前、中、后持续生效）
- Skill 需要**可复用的知识库**（设计模式、风格参考、叙事理论等）
- Skill 涉及**多个子能力的编排调度**（路由映射表）

单一文件 SKILL.md 适用于：单阶段任务、无状态工具类 skill、简单 prompt 包装。

---

### 阶段 1：定义核心哲学

**产物**：`orchestration/<name>-orchestrator.md`

定义该 skill 的：
- **Mission** — 一句话使命宣言
- **核心哲学** — 3-5 条基础原则（不可妥协的设计公理）
- **规则体系** — 显式的分类法（如幻灯片的 7 种责任类型、5 种语法类型）
- **最终目标** — 这个 skill 希望把什么东西形式化

**检查点**：这份文档描述了"为什么这么设计"，任何新加入的规则必须能从这里推导出来。

---

### 阶段 2：构建知识参考层

**产物**：`references/*.md`

将 LLM 隐式具备但不稳定的**设计知识显式化**：
- 风格模式分析（如 Apple Keynote、McKinsey 咨询风）
- 叙事理论（如 tension→reveal→validation→resolution）
- 最佳实践库（如怎么做数据页、怎么做对比页）

**原则**：
- References 不直接控制生成——它们是参考，不是规则
- 按风格/主题分类沉淀，不要混入编排逻辑
- 目标是形成"设计 RAG"：稳定的高质量参考，替代 LLM 的不稳定隐式知识

---

### 阶段 3：定义全局策略层

**产物**：`policies/*.md`

将 orchestrator 中的规则细化成**可执行的约束文件**：
- **叙事策略** — 叙事弧结构、受众适配表、过渡规则
- **节奏策略** — 密度交替规则、呼吸页频率、认知动量管理
- **视觉策略** — 字体预算、色彩预算、网格系统、图表统一规则

**原则**：
- Policy 是**硬约束**——对 orchestrator 具有强制力
- Policy 作用于**跨页面**（区别于 grammar 的单页面作用域）
- 每个 policy 文件必须标注"Implementation"段落——说明 orchestrator 在哪个阶段读取它

---

### 阶段 4：定义页面语法层

**产物**：`grammars/*.md`

将 orchestrator 的类型分类法展开为**完整的认知协议文件**：
- 每个 grammar 类型一个独立文件
- 四维定义：Use Case / Layout Pattern / Content Constraints / Visual Expectations
- 附加：Narrative Role / Information Density / Cognitive Goal / Avoid / Recommended Skills

**原则**：
- Grammar 定义"做什么"（认知目标），不定义"怎么做"（视觉实现）
- Grammar 的类型集合必须与 orchestrator 的 Slide Grammar Library 完全对齐
- 每页只分配一个 grammar 类型

---

### 阶段 5：构建路由映射层

**产物**：`routing/<name>-routing.md`

将 grammar 类型与服务 skill 之间建立**解耦映射**：
- Grammar → 所需能力 → 推荐 skill 列表
- 每个映射包含：能力维度 + 目标 skill + 调度优先级

**原则**：
- Grammar 不硬编码调用哪个 skill
- Skill 不假设自己被哪种 grammar 调用
- 新增/替换 skill 只需更新路由表，不改 grammar 或 orchestrator

---

### 阶段 6：注册外部能力层

**产物**：`skills/readme.md`

声明该 skill 系统引用的外部 Claude Code skills：
- 核心引用（路由表直接使用的 skill）
- 扩展引用（可选替代方案）

**原则**：
- 不重复实现已有 skill 的功能
- 能力原子化——每个外部 skill 专注一个维度
- 复杂能力通过 orchestrator 组合多个 skill

---

### 阶段 7：编写运行时入口

**产物**：`SKILL.md`（放在 skill 根目录）

这是整个系统的**可执行入口**。内容：
1. **YAML frontmatter** — `name` + `description`（含触发条件）
2. **何时激活** — 触发词列表
3. **执行约束（硬规则）** — 从 orchestrator 提取的最高优先级规则
4. **分阶段工作流** — 每阶段：目标 + 动作（读取哪些子文件、产出什么）+ 阻塞点
5. **快速模式**（可选）— 轻量级执行路径
6. **文件索引** — 所有子文件 + 在哪个阶段读取

**关键**：SKILL.md 是"运行时指令"而非"文档"。它告诉 Claude **如何执行**，而非**系统如何设计**。

---

### 阶段 8：编写各层 readme.md

**产物**：每个子目录下的 `readme.md`

每个 readme 说明该层的：
- 定位与职责
- 与其他层的关系
- 文件清单
- 被 orchestrator 调用的时机

---

### 阶段 9：更新 MOC 索引

**产物**：`skills/moc/<分类>.md`

按分类登记该 skill：
- skill 名称 + 来源
- 一句话定位
- 核心能力关键词（3-5 个）
- 子系统入口链接
- 关联的外部 skill 引用

---

### 阶段 10：打包分发

**产物**：`runtime/ccswitch/<skill-name>.zip`

```bash
cd skills/normalized/
zip -r ../../runtime/ccswitch/<skill-name>.zip <skill-name>/ \
  -x "*.git*"
```

打包后的 zip 可直接解压到 `~/.claude/skills/` 完成部署。

---

## 从 Skill 工程到可调用 Skill

将 `skills/normalized/<name>/` 部署为 Claude Code 可调用 skill：

### 方式一：自动打包（推荐）

说 **"将这个 skill 工程变成 skill"** 或 **"封装成 skill"**，触发自动打包流程：
1. 校验工程结构（必须包含 SKILL.md）
2. 打包为 `<name>.zip`
3. 输出到 `runtime/ccswitch/`

### 方式二：手动部署

```bash
# 从 zip 部署
unzip runtime/ccswitch/<name>.zip -d ~/.claude/skills/

# 或直接复制源码
cp -r skills/normalized/<name> ~/.claude/skills/<name>
```

### 方式三：开发模式（软链接）

```bash
# Windows (管理员 PowerShell)
New-Item -ItemType Junction -Path "$env:USERPROFILE\.claude\skills\<name>" -Target "<absolute-path-to-skills-normalized>\<name>"

# macOS / Linux
ln -s "$(pwd)/skills/normalized/<name>" ~/.claude/skills/<name>
```

---

## 已有 Skill

| Skill | 分类 | 定位 | 入口 |
|-------|------|------|------|
| ppt-system | presentation | 分层 AI PPT 生成操作系统 | [SKILL.md](skills/normalized/ppt-system/SKILL.md) |
| pack-skill | tools | Skill 工程打包器 | [SKILL.md](skills/normalized/pack-skill/SKILL.md) |

详见 [skills/moc/](skills/moc/) 下的各分类索引。
