# pack-skill — Skill 工程打包器

## 定位

将 `skills/normalized/<name>/` 下的多文件 skill 工程打包为可部署的 `.zip` 归档，输出到 `runtime/ccswitch/`。

属于 AI-skills 项目的**基础设施工具**，不是面向最终用户的功能 skill。

## 触发方式

在任意 skill 工程目录下说：
- "将这个skill工程变成skill"
- "封装成skill"
- "打包这个skill"
- "pack this skill"
- "ccswitch"

## 执行流程

1. **发现目标** — 从用户指令或上下文确定要打包的 skill
2. **结构校验** — 检查 SKILL.md 存在性及 frontmatter 完整性
3. **元数据提取** — 读取 name、description
4. **打包** — `zip -r runtime/ccswitch/<name>.zip <name>/`（排除 .git/__pycache__/.DS_Store）
5. **验证** — 检查 zip 内容结构
6. **MOC 更新** — 确认或创建 MOC 索引条目
7. **输出部署指令** — 告知用户如何部署到 `~/.claude/skills/`

## 依赖

- `skills/normalized/<name>/SKILL.md` — 必须有合法的 YAML frontmatter（name + description）
- `runtime/ccswitch/` — 输出目录

## 打包产物

```
runtime/ccswitch/
└── <skill-name>.zip    # 可直接 unzip 到 ~/.claude/skills/ 部署
```
