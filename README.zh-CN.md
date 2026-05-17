# Plobi — 工程主权工作流

**人类掌握主权，AI 执行冲刺，物理文档对抗幻觉。**

[English](README.md) | [简体中文](README.zh-CN.md)

---

Plobi 是一个结构化软件开发工作流，专为人类与 AI 协作设计。它让你（人类）对"做什么"拥有战略控制权，同时让 AI 在明确边界内处理战术实现细节。

## 快速开始

### 1. 选择你的工具

| 工具 | 设置方式 | 说明 |
|------|---------|------|
| **Claude Code** | 复制 `adapters/claude-code/` skills | [README](adapters/claude-code/README.md) |
| **Cursor** | 复制 `.cursorrules` 到项目根目录 | [README](adapters/cursor/README.md) |
| **Windsurf** | 复制 `.windsurfrules` 到项目根目录 | [README](adapters/windsurf/README.md) |
| **VSCode + Copilot** | 复制 `copilot-instructions.md` 到 `.github/` | [README](adapters/vscode-copilot/README.md) |
| **Antigravity** | 内联引用 prompts | [README](adapters/antigravity/README.md) |
| **其他 AI 工具** | 直接使用 `prompts/` | 参考 `core/principles.md` + `prompts/[skill].md` |

### 2. 初始化项目

```text
Phase 0: 初始化
  1. Guard  — 防止危险 git 操作
  2. Scaffold — 创建 docs/ 文件夹和模板
  3. Compress — 启用极简模式（可选）
```

### 3. 运行 8 阶段工作流

```text
Phase 1: 探索与调研    → 发散，发现真实需求
Phase 2: 方案设计      → UI 规范、PRD、任务切片
Phase 3: 开发编码      → TDD 垂直切片
Phase 4: 测试验证      → 人工测试，结构化反馈
Phase 5: Bug 修复      → 系统性诊断
Phase 6: 功能扩展      → 重复 1-5 添加新功能
Phase 7: 部署上线      → 审查，手动推送
Phase 8: 持续优化      → 架构扫描
```

完整工作流文档：[`core/workflow.md`](core/workflow.md)

## 仓库结构

```text
plobi/
├── core/                          # 工具无关核心
│   ├── principles.md              # 核心原则
│   ├── glossary.md                # 领域术语
│   └── workflow.md                # 完整 8 阶段工作流
├── prompts/                       # 工具无关 skill prompt
│   ├── compress.md
│   ├── explore.md
│   ├── recon.md
│   ├── grill.md
│   ├── design.md
│   ├── synthesize.md
│   ├── slice.md
│   ├── freeze.md
│   ├── dissect.md
│   ├── fuse.md
│   ├── map.md
│   ├── package.md
│   ├── tidy.md
│   ├── scaffold.md
│   └── forge.md
├── docs/                          # 文档模板
│   ├── RESEARCH.md
│   ├── CONTEXT.md
│   ├── PRODUCT.md
│   └── DESIGN.md
├── decisions/                     # 决策记录（已采纳 + 已否决）
├── TASK.md                        # 实时任务跟踪（根目录方便查阅）
├── HANDOFF.md                     # 跨会话交接（根目录方便查阅）
│   ├── adr/                       # 架构决策记录
│   └── veto/                      # 被否决的决策
├── adapters/                      # 工具特定实现
│   ├── claude-code/               # 原生 skill 系统
│   ├── cursor/                    # .cursorrules + @prompts
│   ├── windsurf/                  # .windsurfrules
│   ├── vscode-copilot/            # copilot-instructions.md
│   └── antigravity/               # 内联 prompt 引用
└── examples/                      # 示例项目配置
```

## 17 个 Skill

| Skill | 阶段 | 用途 |
|-------|------|------|
| **guard** | 0 | 拦截危险 git 操作 |
| **scaffold** | 0 | 创建项目结构和模板 |
| **compress** | 全阶段 | 极简通信模式 |
| **explore** | 1 | 发散需求探索 |
| **recon** | 1 | 市场与技术调研 |
| **grill** | 1, 2, 6 | 审讯式追问直至收敛 |
| **design** | 2 | UI/UX 设计规范 |
| **synthesize** | 2 | 从上下文生成 PRD |
| **slice** | 2 | 将 PRD 拆成垂直切片 |
| **freeze** | 3, 4, 5 | TDD 红绿重构 |
| **dissect** | 5 | 六阶段 Bug 诊断 |
| **fuse** | 3, 8 | 架构改进扫描 |
| **map** | 6, 任意 | 代码库模块地图 |
| **tidy** | 任意 | 强制结构整洁和命名规范 |
| **package** | 7, 任意 | 跨会话交接 |
| **forge** | 元 | 创建新 skill |

## 核心概念

### 垂直切片
每个任务都是一个端到端、可演示的功能（数据库 + API + UI + 测试）—— 不是水平分层。

### 冻结线
决策一旦写入 `CONTEXT.md` 或 `TASK.md` 即进入冻结状态。只能追加，不能修改。如需更改：迷你 grill + ADR 说明原因。

### 否决
被否决的决策被永久记录。后续会话在重新讨论前必须先检查。

### 反馈格式
结构化 Bug 报告防止"修好一个，坏掉两个"：

```text
[位置] 哪个页面/功能
[操作] 我做了什么
[期望] 我以为会发生什么
[实际] 实际发生了什么
[影响] 严重程度（影响使用 / 体验不好 / 小细节）
```

## 设计哲学

1. **你决定做什么。** AI 决定怎么做。
2. **物理文档优于记忆。** 所有上下文存在于文件中。会话结束，文档永存。
3. **测试即反馈环。** 没有通过/失败信号就没有进展。
4. **一次一个切片。** 完成并验证后再继续。

## 贡献

Plobi 是一个从真实项目中演化而来的个人工作流。要贡献：

1. 在真实项目中使用它
2. 识别摩擦点
3. 通过工作流本身提出变更（explore → grill → synthesize → slice → freeze）

## 许可证

MIT — 自由使用、修改、分享。注明出处即感激。
