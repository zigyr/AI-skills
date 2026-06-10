---
name: pack-skill
description: >
  Pack a skill project under skills/normalized/ into a deployable zip archive
  in runtime/ccswitch/. Validates the project structure, creates the zip, and
  updates the MOC index. Triggered by "将这个skill工程变成skill", "封装成skill",
  "打包skill", "pack this skill", "ccswitch".
---

# Pack Skill — Skill 工程打包器

> 将 `skills/normalized/<name>/` 下的 skill 工程打包为可部署的 zip 归档，放入 `runtime/ccswitch/`。

## 触发条件

用户说以下任意短语时激活：
- "将这个skill工程变成skill"
- "把这个封装成skill"
- "打包这个skill"
- "pack this skill"
- "ccswitch"
- "导出为skill包"

## 执行流程

### Step 1: 发现目标 Skill

确定要打包的 skill：

1. **若用户指定了路径**（如"把 ppt-system 打包"），直接使用 `skills/normalized/<name>/`
2. **若用户在 skill 目录下操作**（IDE 打开了该目录下的文件），从上下文推断目标 skill
3. **若无法推断**，列出 `skills/normalized/` 下所有可用 skill，让用户选择

### Step 2: 结构校验

验证目标目录必须包含：

| 检查项 | 必需 | 说明 |
|--------|------|------|
| `SKILL.md` | ✅ 必需 | Skill 运行时入口文件 |
| `SKILL.md` frontmatter 含 `name` | ✅ 必需 | Skill 名称 |
| `SKILL.md` frontmatter 含 `description` | ✅ 必需 | Skill 描述 |
| `readme.md` | 推荐 | 工程文档 |

**校验失败** → 报告缺失项，停止打包。给出修复建议。

### Step 3: 读取 Skill 元数据

从 `SKILL.md` 的 YAML frontmatter 提取：
- `name` — 作为 zip 文件名的基础
- `description` — 用于更新 MOC 索引

### Step 4: 打包

```bash
cd skills/normalized/
zip -r ../../runtime/ccswitch/<name>.zip <name>/ \
  -x "*.git*" "__pycache__/*" "*.pyc" ".DS_Store"
```

**命名规则**：`<name>.zip` — 与 SKILL.md 中的 `name` 字段一致。

### Step 5: 验证打包结果

```bash
# 检查 zip 内容结构
unzip -l runtime/ccswitch/<name>.zip | head -30
```

确认：
- `SKILL.md` 在 zip 根目录下（路径为 `<name>/SKILL.md`）
- 所有子文件完整

### Step 6: 更新 MOC 索引

在 `skills/moc/` 中检查该 skill 是否已登记：
- **已登记** → 更新"打包状态"为 `runtime/ccswitch/<name>.zip`
- **未登记** → 根据 skill 分类（从 SKILL.md 内容推断或询问用户），在对应 moc 文件中登记

### Step 7: 输出部署指令

```
✅ 打包完成: runtime/ccswitch/<name>.zip

部署方式:
  unzip runtime/ccswitch/<name>.zip -d ~/.claude/skills/

或开发模式 (macOS/Linux):
  ln -s "$(pwd)/skills/normalized/<name>" ~/.claude/skills/<name>
```

---

## 注意事项

- 打包前确保所有待提交的修改已保存（git status 检查）
- zip 自动排除 `.git`、`__pycache__`、`.pyc`、`.DS_Store`
- 同一 skill 重复打包会覆盖旧 zip
- 打包完成后可以 `git add runtime/ccswitch/<name>.zip` 将其纳入版本管理（可选）
