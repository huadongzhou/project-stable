# project-stable

项目五文档基建技能（Claude Code Agent Skill）：为全新项目或接入 Vibe Coding 的旧项目，初始化 / 更新 / 同步仓库根目录的五份上下文文档，让任意代码助手进入项目即拥有一致的认知基础。

| 文档 | 定位 |
|---|---|
| `AGENTS.md` | 默认上下文，最简单清晰的项目指引 |
| `PRODUCT.md` | 产品指示：模块/关联/顺序/引用、增删改查关联、关系图 |
| `DESIGN.md` | 产品设计：设计令牌 / UX / UI 基准 |
| `TODO.md` | 待办：场景→功能→点 目录树 + todo 状态 |
| `PROMPT.md` | 常用提示词：BDD 场景 + 可执行提示词 |

## 安装

```bash
# 用户级（所有项目可用，推荐——新项目搭建时技能必须先于项目存在）
git clone https://github.com/huadongzhou/project-stable.git ~/.claude/skills/project-stable

# 或项目级（仅当前仓库可用）
git clone https://github.com/huadongzhou/project-stable.git <repo>/.claude/skills/project-stable
```

Windows 用户级路径：`C:\Users\<用户名>\.claude\skills\project-stable`。

## 使用

在 Claude Code 中自然语言触发即可，例如：

- 「用 project-stable 初始化本项目文档」——为缺失的文档执行 **初始化**（读模板 → 解读项目 → 生成文档；已存在的不覆盖）；
- 「更新项目五文档」——执行 **更新**（最小变更：补缺失章节、修正过期事实；项目自行长出的章节保留）；
- 「把项目文档结构反哺回模板」——执行 **同步**（项目文档 → 模板单向反哺：提取模板缺少的标题+结构，项目特性值改写为生成提示）。

三个操作的完整行为契约（Gherkin 场景 + 规则）见 [SKILL.md](SKILL.md)。

## 仓库结构

```text
project-stable/
├── SKILL.md              # 技能入口：管辖范围、模板机制、初始化/更新/同步 三操作
└── templates/            # 五份模板：公共内容原样保留 + <!-- 生成提示 --> 挖空点 + {{占位符}}
    ├── AGENTS.md
    ├── PRODUCT.md
    ├── DESIGN.md
    ├── TODO.md
    └── PROMPT.md
```

## 设计约束

- 仅管理与 `templates/` 同名一一对应的五份根目录文档；其余文档（README、CLAUDE.md、docs/ 等）只作只读信息来源，不创建、不修改。
- 所有产出基于可验证的项目事实：解读不到的内容写「待补充：<缺什么、去哪找>」，不编造、不推定。
- 模板演进走「同步」操作：从真实项目文档提取通用结构反哺模板，项目特性值永不写入模板。

## License

[MIT](LICENSE)
