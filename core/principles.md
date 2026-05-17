# Plobi Core Principles

## Human Sovereignty, AI Execution

The operator holds strategic sovereignty — what to build, how it should look, how it should feel. The AI executes tactical sprints within boundaries the operator defines. Physical documents defend against AI hallucination: rules are written into files, not left to AI self-discipline.

## The 8 Phases

1. **Init** — Guardrails, scaffold, templates
2. **Explore & Research** — Diverge, then converge
3. **Design** — UI/UX spec, PRD, sliced tasks
4. **Develop** — TDD vertical slices
5. **Verify** — Human testing with structured feedback
6. **Fix** — Disciplined diagnosis
7. **Extend** — Repeat phases 1-6
8. **Optimize** — Architecture scans, test freezes

## Key Mechanics

### Vertical Slices
Each slice is an end-to-end, demoable feature (database + API + UI + tests). Not horizontal layers.

### Freeze Line
Once a decision is written into `CONTEXT.md` or `TASK.md`, it is frozen. Can only append, never modify. To change: mini-grill + ADR explaining why.

### Veto
Rejected decisions are recorded permanently. Future sessions check veto files before re-opening closed branches.

### Feedback Loop
No progress without a pass/fail signal. Tests first. Always.

### Physical Documents
All context lives in files, not in AI memory. Session ends, memory resets, documents persist.
