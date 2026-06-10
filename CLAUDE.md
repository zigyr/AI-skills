# AI-skills 项目

## 项目定位

本地 skill 管理中心，为 Claude Code 提供统一、标准化的 skill 入口。

## 目录结构

```
AI-skills/
├── skills/
│   ├── normalized/      # 自定义标准化版本（统一入口）
│   │   ├── ppt-system/  # 分层 PPT 生成操作系统
│   │   └── pack-skill/  # Skill 工程打包器
│   ├── moc/             # Map of Content，技能索引/导航
│   └── repos/           # 原始 Git 仓库（只读，用 git clone/pull 管理）
├── runtime/
│   └── ccswitch/        # 打包好的 skill zip 归档
└── prompts/             # 提示词暂存与实验
```

## 治理原则

- `skills/repos/` 只通过 `git clone` / `git pull` 管理，不要手动改
- `skills/normalized/` 是统一入口，内部是 `SKILL.md` + 分层子文件（orchestration/policies/grammars 等）
- `skills/moc/` 按分类索引所有 skill，新增 skill 必须同步更新
- `runtime/ccswitch/` 存放打包好的 zip，可直接部署到 `~/.claude/skills/`

---

## 规则

### 1. 新 Skill 入仓 → 同步更新 MOC

每次有新的 skill 被添加到 `skills/normalized/` 或 `skills/repos/`，**必须**在 `skills/moc/` 中：

- 按实际分类（presentation / tools / ui / writing / cognition 等）找到或创建对应的 moc 文件
- 在该分类的 moc 文件中登记该 skill，内容包括：
  - skill 名称
  - 来源（repos 原始仓库名 或 normalized 标准化名）
  - 一句话定位（做什么的）
  - 核心能力/关键词（3-5 个）
- 如果 skill 跨分类，在主要分类下登记，其他分类下写引用链接

moc 文件命名：`skills/moc/{分类名}.md`（如 `skills/moc/presentation.md`）
