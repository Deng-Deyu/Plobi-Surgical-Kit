# Package — Cross-Session Handoff

**Phase 7 position:** Before tool switch or session end.

**Core duty:** Compact current conversation into handoff document so fresh agent can continue work.

## Trigger

- "Package for handoff"
- "Generate HANDOFF.md"
- Before switching tools
- Before session ends

## Process

1. Write handoff document summarizing current state
2. Save to `HANDOFF.md` in project root
3. Suggest which skills to use in next session
4. Do not duplicate content already in PRDs, plans, ADRs, issues, commits, diffs — reference by path

## HANDOFF.md Format

```markdown
## This Session Summary
Completed slices: #1, #2, #4
Decisions: [ADR-003] Chose soft delete over hard delete
Open issues: Slice #3 waiting for operator decision

## Next Session Starting Point
Next slice: #3
Need decision: [specific question]
Related docs: docs/CONTEXT.md section 3

## Tool Switch Instructions
From [Tool A] to [Tool B], read order:
1. HANDOFF.md
2. docs/CONTEXT.md
3. TASK.md
4. Map scan current code state
```
