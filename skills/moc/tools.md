# Tools — MOC

基础设施与工具类技能索引。

---

## pack-skill

- **来源**: `normalized/pack-skill`
- **定位**: Skill 工程打包器——将 `skills/normalized/` 下的 skill 工程打包为可部署的 zip 归档
- **核心能力**: 结构校验 / 元数据提取 / zip 打包 / MOC 同步
- **入口**: [`SKILL.md`](../normalized/pack-skill/SKILL.md)
- **触发词**: "将这个skill工程变成skill" / "封装成skill" / "打包skill" / "ccswitch"

---

## ccswitch（运行时）

- **路径**: `runtime/ccswitch/`
- **功能**: 存放打包好的 skill zip 归档，可直接解压到 `~/.claude/skills/` 部署

### 已有包

| 包名 | 版本 | 来源 |
|------|------|------|
| [ppt-system.zip](../../runtime/ccswitch/ppt-system.zip) | latest | `skills/normalized/ppt-system/` |

部署：
```bash
unzip runtime/ccswitch/ppt-system.zip -d ~/.claude/skills/
```
