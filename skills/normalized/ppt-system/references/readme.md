# references/ — 知识参考层

## 定位

`references/` 是 ppt-system 的设计知识库。它**不直接控制生成**，而是为 orchestrator 提供参考认知——让 AI 具备稳定的设计判断力，而非在每次生成时从零推导。

## 与其他层级的区别

| 层级 | 性质 | 作用 |
|------|------|------|
| `references/` | 知识参考 | 设计理论与风格经验——注入设计认知 |
| `policies/` | 全局规则 | 强制约束——限制生成边界 |
| `grammars/` | 认知协议 | 页面契约——定义页面类型行为 |
| `routing/` | 映射表 | 解耦层——连接 grammar 与 skill |
| `skills/` | 执行单元 | 生成能力——产出实际页面 |

---

## 目录结构

```
references/
├── slide-patterns.md         # 优秀幻灯片模式分析
├── storytelling-notes.md     # 叙事节奏与认知动线理论
└── styles/                   # 按风格分类的设计参考（可扩展）
    ├── consulting/           # McKinsey 等咨询风格
    ├── apple/                # Apple Keynote 风格
    ├── startup/              # 创业融资风格
    ├── futuristic/           # 科技/未来感风格
    ├── minimalism/           # 极简风格
    └── dashboard/            # 数据仪表盘风格
```

---

## 风格参考

### Apple Keynote 风格

- **特征** — 极简文本、情感化图像、强排版、每页一核心
- **适用** — 产品发布、主题演讲
- **启发** — 使用全屏图像 + 大字体语句，营造情绪冲击

### McKinsey 咨询风格

- **特征** — 洞察驱动标题、证据链结构、信息密集但有序
- **适用** — 咨询报告、战略文档
- **启发** — 标题即结论，页面内容为结论提供证据支撑

### 科技/未来感风格

- **特征** — 深色背景、高对比、几何装饰、大量留白
- **适用** — 科技产品发布、AI/Web3 主题演讲
- **启发** — 冷色调 + 细线几何 + 低信息密度

### 极简风格

- **特征** — 单一焦点、克制用色、大量留白、字体层级清晰
- **适用** — 学术报告、设计审查、高端品牌
- **启发** — 删减到只剩必要元素，用留白替代分割线

---

## 运行机制

当 orchestrator 接收任务时：

```
用户需求："做一个科技风 AI 行业分析 PPT"
    ↓
references 提供风格认知 → 科技风 = 深背景、高对比、冷色调、大留白
    ↓
policies 施加约束 → 色彩：深色底 + 1-2 冷色主色 + 白色文本
    ↓
grammars 分配页面类型 → P1=Emphasis, P2=Framework, P3=Comparison, ...
    ↓
routing + skills 执行生成 → frontend-slides + taste-skill
```

---

## 设计原则

references 存在的核心目的：**给 AI 注入稳定的设计感**。

LLM 具备广泛的视觉知识但输出不稳定。将高价值设计认知显式写入 references，形成稳定的设计知识检索（Design RAG）：

```
references 风格认知 + policies 规则约束 + grammars 页面协议 + skills 生成执行
```

不同风格的叙事语法各有不同，应在 references 中按风格分类沉淀，而非混入 orchestrator 逻辑。
