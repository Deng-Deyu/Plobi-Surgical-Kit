# Plobi — Engineering Sovereignty Workflow

**Human sovereignty, AI execution, physical documents against hallucination.**

[English](README.md) | [简体中文](README.zh-CN.md)

---

Plobi is a structured software development workflow designed for human-AI collaboration. It gives you (the human) strategic control over what gets built while letting AI handle tactical implementation within clearly defined boundaries.

## Quick Start

### 1. Pick Your Tool

| Tool | Setup | Instructions |
|------|-------|-------------|
| **Claude Code** | Copy `adapters/claude-code/` skills | [README](adapters/claude-code/README.md) |
| **Cursor** | Copy `.cursorrules` to project root | [README](adapters/cursor/README.md) |
| **Windsurf** | Copy `.windsurfrules` to project root | [README](adapters/windsurf/README.md) |
| **VSCode + Copilot** | Copy `copilot-instructions.md` to `.github/` | [README](adapters/vscode-copilot/README.md) |
| **Antigravity** | Reference prompts inline | [README](adapters/antigravity/README.md) |
| **Any other AI tool** | Use `prompts/` directly | Reference `core/principles.md` + `prompts/[skill].md` |

### 2. Initialize Your Project

```text
Phase 0: Init
  1. Guard  — protect against dangerous git operations
  2. Scaffold — create docs/ folder with templates
  3. Compress — enable terse mode (optional)
```

### 3. Run the 8-Phase Workflow

```text
Phase 1: Explore & Research    → diverge, discover real needs
Phase 2: Design                → UI spec, PRD, task slices
Phase 3: Develop               → TDD vertical slices
Phase 4: Verify                → human testing, structured feedback
Phase 5: Fix                   → disciplined diagnosis
Phase 6: Extend                → repeat 1-5 for new features
Phase 7: Deploy                → review, manual push
Phase 8: Optimize              → architecture scans
```

Full workflow documentation: [`core/workflow.md`](core/workflow.md)

## Repository Structure

```text
plobi/
├── core/                          # Tool-agnostic core
│   ├── principles.md              # Core principles
│   ├── glossary.md                # Domain terminology
│   └── workflow.md                # Complete 8-phase workflow
├── prompts/                       # Tool-agnostic skill prompts
│   ├── compress.md
│   ├── explore.md
│   ├── grill.md
│   ├── design.md
│   ├── synthesize.md
│   ├── slice.md
│   ├── freeze.md
│   ├── dissect.md
│   ├── fuse.md
│   ├── map.md
│   ├── package.md
│   ├── scaffold.md
│   └── forge.md
├── docs/                          # Document templates
│   ├── RESEARCH.md
│   ├── CONTEXT.md
│   ├── PRODUCT.md
│   ├── DESIGN.md
│   ├── TASK.md
│   └── HANDOFF.md
├── decisions/                     # Decision records (adopted + vetoed)
│   ├── adr/                       # Architecture Decision Records
│   └── veto/                      # Rejected decisions
├── adapters/                      # Tool-specific implementations
│   ├── claude-code/               # Native skill system
│   ├── cursor/                    # .cursorrules + @prompts
│   ├── windsurf/                  # .windsurfrules
│   ├── vscode-copilot/            # copilot-instructions.md
│   └── antigravity/               # Inline prompt references
└── examples/                      # Example project setups
```

## 15 Skills

| Skill | Phase | Purpose |
|-------|-------|---------|
| **guard** | 0 | Block dangerous git operations |
| **scaffold** | 0 | Create project structure and templates |
| **compress** | All | Ultra-terse communication mode |
| **explore** | 1 | Divergent requirement discovery |
| **recon** | 1 | Market and technology research |
| **grill** | 1, 2, 6 | Relentless interrogation until convergence |
| **design** | 2 | UI/UX design specification |
| **synthesize** | 2 | Generate PRD from context |
| **slice** | 2 | Break PRD into vertical slices |
| **freeze** | 3, 4, 5 | TDD red-green-refactor |
| **dissect** | 5 | 6-phase bug diagnosis |
| **fuse** | 3, 8 | Architecture improvement scans |
| **map** | 6, Any | Codebase module mapping |
| **package** | 7, Any | Cross-session handoff |
| **forge** | Meta | Create new skills |

## Key Concepts

### Vertical Slices
Each task is an end-to-end, demoable feature (database + API + UI + tests) — not a horizontal layer.

### Freeze Line
Once a decision is written to `CONTEXT.md` or `TASK.md`, it's frozen. Can only append, never modify. To change: mini-grill + ADR explaining why.

### Veto
Rejected decisions are permanently recorded. Future sessions check before re-litigating.

### Feedback Format

Structured bug reports prevent "fix one, break two":

```text
[Location] Which page/feature
[Action] What I did
[Expected] What I thought would happen
[Actual] What actually happened
[Impact] Severity (blocks usage / bad experience / minor)
```

## Philosophy

1. **You decide what to build.** AI decides how to implement.
2. **Physical documents over memory.** All context lives in files. Sessions end; documents persist.
3. **Tests are the feedback loop.** No progress without a pass/fail signal.
4. **One slice at a time.** Complete and verify before moving on.

## Contributing

Plobi is a personal workflow evolved through real project use. To contribute:

1. Use it on a real project
2. Identify friction points
3. Propose changes via the workflow itself (explore → grill → synthesize → slice → freeze)

## License

MIT — Use, modify, share freely. Attribution appreciated.
