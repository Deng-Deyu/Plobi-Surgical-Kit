# Antigravity Adapter for Plobi

## Setup

1. Copy the relevant prompt files from `prompts/` to your Antigravity workspace
2. Reference them in your Antigravity conversations as needed

## Usage

Antigravity doesn't have a built-in rules file or skill system. Use these approaches:

### Option A: System Prompt
If Antigravity supports custom system prompts, paste the contents of `../cursor/.cursorrules` or `../vscode-copilot/copilot-instructions.md` as your system prompt.

### Option B: Reference Files
Store Plobi prompts in your workspace and reference them:

```
[Reference: plobi-principles.md]
[Reference: plobi-freeze.md]

Implement slice #2 with TDD.
```

### Option C: Conversation Starter
Begin each session with a brief Plobi context:

```
We're using the Plobi workflow. Key rules:
- Vertical slices only (end-to-end features)
- Tests first (red-green-refactor)
- Frozen decisions in CONTEXT.md
- Structured bug reports with [Location][Action][Expected][Actual][Impact]

Current phase: [X]. Next task: [Y].
```

## Document Templates

Use templates from `../../templates/`.

## Limitations

| Feature | Antigravity | Notes |
|---|---|---|
| Guard | Not available | Manual discipline |
| Persistent rules | Depends on setup | May need per-session context |
| Skill commands | Not available | Inline reference |

## Recommended Workflow

1. Set up Plobi principles in Antigravity's system prompt (if supported)
2. Create `docs/` folder with templates
3. Reference skill prompts at start of each task
4. Maintain `TASK.md` and `HANDOFF.md` manually
