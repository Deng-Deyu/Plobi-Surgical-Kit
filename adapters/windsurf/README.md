# Windsurf Adapter for Plobi

## Setup

1. Copy `.windsurfrules` to your project root
2. Copy `prompts/` contents to a `.plobi-prompts/` folder in your project

## Usage

### Global Rules
Windsurf Cascade automatically reads `.windsurfrules` on every interaction.

### Skill Prompts
In Cascade Chat, reference individual skill prompts with `@`:

```
@.plobi-prompts/grill.md
@.plobi-prompts/freeze.md
@.plobi-prompts/explore.md
```

### Document Templates
Use templates from `../../docs/`:
- `RESEARCH.md`, `CONTEXT.md`, `PRODUCT.md`, `DESIGN.md` → `docs/`
- `TASK.md`, `HANDOFF.md` → project root

## Limitations vs Claude Code

| Feature | Windsurf | Notes |
|---|---|---|
| Guard (git interception) | Not available | Manual discipline or hooks |
| `/command` skills | Not available | Use `@prompt` references |
| Auto skill selection | Manual | You choose prompt |

## Recommended Workflow

Same as Cursor: paste rules, create docs folder, `@prompt` skills as needed.
