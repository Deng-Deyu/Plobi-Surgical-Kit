# Plobi Workflow

## Document System

| Document | Purpose | Written By | Created |
|---|---|---|---|
| `docs/RESEARCH.md` | Tech research, competitive analysis, API summaries | AI (recon) | Phase 1 |
| `docs/CONTEXT.md` | Aligned definitions, glossary, product boundaries | AI (grill) | Phase 1 |
| `docs/PRODUCT.md` | Final PRD: feature list, acceptance criteria, priorities | AI (synthesize) | Phase 2 |
| `docs/DESIGN.md` | UI visual style, interaction spec, component conventions | AI (design) | Phase 2 |
| `decisions/adr/ADR-XXX.md` | Every major decision: what, why, what was rejected | AI (grill) | Phase 1-6 |
| `decisions/veto/*.md` | Permanently rejected decisions | AI (grill) | Phase 1-6 |
| `TASK.md` | Real-time task tracking: status per slice | AI (auto-update) | Phase 3 |
| `HANDOFF.md` | Cross-tool / cross-session handoff document | AI (package) | Every switch |

**Naming rule:** ALL_CAPS, underscores, in `docs/` (except `TASK.md` and `HANDOFF.md` at root for quick access). Decisions live in `decisions/adr/` and `decisions/veto/`.

---

## Skills Overview

| Skill | One-line Duty | Trigger |
|---|---|---|
| **guard** | Install physical locks blocking dangerous git operations | First step of every project |
| **scaffold** | Auto-create folder structure and all document templates | After guard |
| **compress** | Enable caveman mode: minimal tokens, full accuracy | Say "caveman mode" |
| **explore** | Divergent exploration: ask + recommend missing features | "Explore this idea" |
| **recon** | Market/tech research, results written to `RESEARCH.md` | "Research X" |
| **map** | Scan unfamiliar code, output module map | "Map this codebase" |
| **grill** | Relentless interrogation: disambiguate, stress-test, write ADR | "Grill me" |
| **design** | UI/UX design spec: visual style, interaction rules | "Design the UI" |
| **synthesize** | Generate PRD from confirmed context | "Write the PRD" |
| **slice** | Break PRD into vertical slice tasks | "Slice the work" |
| **freeze** | TDD loop: fail test first, minimal implementation, repeat | "Write tests" / "Start coding" |
| **fuse** | Architecture scan: find rot, propose fixes | "Architecture scan" |
| **dissect** | Bug diagnosis 6 phases: systematic root cause | "Diagnose this" |
| **package** | Generate `HANDOFF.md` for tool/session switching | "Package for handoff" |
| **tidy** | Enforce structure hygiene and naming conventions | "Tidy up" / "Clean up structure" |
| **forge** | Create a new Plobi skill | "Forge a new skill" |

**17 skills total.**

---

## Phase 0 — Init

**Operator does:** Answer scaffold's three questions. Everything else is AI.

**Execution order (sequential, no skipping):**

```
Step 1 → guard    (install git locks)
Step 2 → scaffold (create folders and doc templates)
Step 3 → compress (enable caveman mode)
```

### Guard
Writes scripts to intercept dangerous git commands at the OS level:
- `git push` (prevents AI from publishing)
- `git reset --hard` (prevents history wipe)
- `git clean -fd` (prevents file deletion)
- `git branch -D` (prevents branch deletion)

**Your push is unaffected.** The hook only intercepts AI-issued commands.

### Scaffold
Auto-creates:

```
your-project/
├── docs/
│   ├── RESEARCH.md
│   ├── CONTEXT.md
│   ├── PRODUCT.md
│   └── DESIGN.md
├── decisions/
│   ├── adr/
│   └── veto/
├── TASK.md
└── HANDOFF.md
```

### Scaffold's Three Questions

1. Which issue tracker? (GitHub Issues / Notion / Local markdown)
2. Which triage labels? (Keep: `ready` / `in-progress` / `blocked` / `done`)
3. Project codename? (For ADR prefix, e.g. `TASK-001`)

> **Iron rule:** No requirements discussion before Phase 0 completes. Locks and skeleton must be in place first.

---

## Phase 1 — Explore & Research

**Operator does:** Input initial ideas, answer AI questions, make choices.

### Two paths

```
Path A: I have an idea but not sure what to build
         → explore (divergent)

Path B: I know what's missing, need validation
         → recon (market/tech)

Both paths converge at grill
```

### Explore
**Input:** Say anything. Example: "I want a tool to help designers manage client feedback."

**AI does:**
1. Persistent questions to uncover real needs
2. Proactively recommend features you might have missed
3. Each recommendation: keep / drop / later

**Output:** Feature candidate list (in chat, for later grill convergence).

> Tip: Explore is divergent. Don't reject features too early. Let AI lay them out, cut later in grill.

### Recon
**Input:** Describe research target. Example: "Research feedback tools for designers."

**AI does:** Web search → organize → **mandatory write to `docs/RESEARCH.md`** (never just tell verbally).

`RESEARCH.md` contains: Competitor feature comparison, tech stack comparison, recommendation, reference links.

> **Iron rule:** AI must not only report recon results in chat. All recon output must persist to `RESEARCH.md`.

### Grill
After explore or recon, execute grill. **This is the step from "idea" to "contract."**

**Grill does:**
1. Disambiguate every fuzzy term ("nice" = what? "smooth" = what standard?)
2. Stress-test your plan — AI plays devil's advocate ("What if user uploads >100MB file?")
3. Write aligned definitions and decisions to `docs/CONTEXT.md` and `decisions/adr/`

**"Stress test" feeling:** AI asks "what if" questions to surface edge cases you haven't thought of. Not hostile, just thorough.

> **Freeze line (iron rule):**
> - Content confirmed and written into `CONTEXT.md` enters **frozen state**
> - Can only **append**, never **modify** existing entries
> - If change needed: mini-grill + ADR explaining why
> - AI has no authority to override frozen content, even if it thinks old decision is "obviously wrong"

**Caveman mode auto-rules:**
- Grill triggers: caveman mode **auto-pauses** (full natural language for conversation)
- After grill, requirements written: caveman mode **auto-resumes**

---

## Phase 2 — Design

**Operator does:** Review feature descriptions (no code needed), say "yes" or "no" in natural language.

### Execution order

```
Step 1 → design     (UI/UX design spec)
Step 2 → synthesize (generate PRD)
Step 3 → slice      (break into tasks)
Step 4 → grill      (stress-test the design)
```

### Design
**Input:** Describe desired style however you want:
- Screenshot: "I want this app's style"
- Reference: "Like Linear's clean feel"
- Keywords: "Dark theme, big radius, smooth animations"

**AI does:**
1. Ask about visual preferences (colors, fonts, radius, animation)
2. Ask about interaction preferences (gestures, click feedback, loading)
3. Recommend style if no reference given
4. Write confirmed design spec to `docs/DESIGN.md`

`DESIGN.md` contains:
- Primary colors and palette
- Font spec
- Spacing and radius spec
- Core interaction rules (button feedback, page transitions)
- Component conventions (which card/button/form for which scene)

> **Iron rule:** All Phase 3 UI implementation must reference `DESIGN.md`. AI must not self-determine visual style.

### Synthesize
**"Context" means:** `RESEARCH.md` + `CONTEXT.md` + your explore/grill chat history.

**Output:** `docs/PRODUCT.md` (PRD) containing:
- Feature list (each feature from grill confirmation)
- Acceptance criteria per feature (natural language, not code)
- Feature priority (P0 must-have / P1 important / P2 later)

### Slice
AI breaks PRD into vertical slice tasks, writes to `TASK.md`.

**Vertical slice:** Each slice = one end-to-end runnable complete feature (database to UI to tests).

**Correct example:**
> Slice #1: User can create a Todo (includes database + API + UI + tests)

**Your review** (no tech knowledge needed): Just read slice descriptions in `TASK.md`:
- Does this feature match my need?
- Any missing features?
- Is order correct? (Login before core feature?)

**AI also labels each slice:**
- **AFK:** AI completes autonomously
- **HITL:** Pauses for your decision

### Stress-test (grill round 2)
Stress-test design and slice division:
- "If user has poor network, how does slice 3 behave?"
- "Will slice #2 and #5 conflict?"

> **Interface contract lock (iron rule):**
> - Phase 2 ends with each slice's "description + acceptance criteria" in `TASK.md`
> - Confirmed by you, enters frozen state
> - Phase 3 AI can only implement, cannot change feature definitions
> - If AI says "I need to modify this feature" in Phase 3: pause, return to grill

---

## Phase 3 — Develop

**Operator does:** Check `TASK.md` for progress, make decisions on HITL slices, do functional acceptance (no code review needed).

### Only document you need: `TASK.md`

Format:

```markdown
## Current Progress

| Slice | Description | Status | Type | Notes |
|---|---|---|---|---|
| #1 | User can create Todo | Done | AFK | |
| #2 | User can delete Todo | In Progress | AFK | |
| #3 | Multi-user permissions | Waiting for you | HITL | Need your decision: everyone can delete, or only creator? |
| #4 | Soft delete (recycle bin) | Not started | AFK | |

## This Session Progress
Start: ...   Completed: #1   Next: #2
```

**Regular task:** Open `TASK.md`, check status. Respond to HITL.

### AFK Slice Execution Loop

AI inside each AFK slice runs TDD:

```
freeze →
  RED: Write failing test (prove feature not implemented)
  GREEN: Write minimal code to pass
  Next behavior → Repeat
```

You don't need to understand this loop technically. Its purpose: AI has verifiable signal at every step, won't write blindly.

### HITL Slice Handling

When hitting HITL slice, AI will:
1. Pause, mark "waiting for decision" in `TASK.md`
2. Trigger grill, ask decision in natural language
3. Your answer → AI writes decision to ADR → continues coding

### Code Review Gate (per slice completion)

**Layer 1 (auto, no action needed):**
AI's built-in scanner checks: hardcoded passwords, accidentally deleted files, spec violations. Auto-passes if clean, self-fixes if not.

**Layer 2 (you do, no code needed):**
AI gives functional acceptance checklist:
```
Slice #2 complete, confirm:
- Click "Delete" button, Todo disappears from list
- After delete, page doesn't refresh or error
- If Todo doesn't exist, show friendly error
Confirm? Type pass to continue, or tell me what's wrong.
```

Just **launch the app, click through yourself**, then say `pass` or describe the issue.

> **Bug escalation rule:**
> - Small reproducible bug: AI fixes immediately
>> - Unstable or unclear bug: mandatory Phase 5 diagnosis, no guessing allowed

---

## Phase 4 — Test

**Operator does:** Launch app, test as real user, report issues in standard format.

### Your testing

No test code needed. Your job: **use the app like a real user**, find:
- Wrong functionality
- Bad experience (lag, weird animation, confusing button)
- Anything not matching your expectation

### Feedback format (mandatory)

```
[Location] Which page/feature
[Action] What I did
[Expected] What I thought would happen
[Actual] What actually happened
[Impact] Severity (blocks usage / bad experience / minor detail)
```

**Example:**
```
[Location] Todo list page
[Action] Clicked "Delete" button
[Expected] Todo disappears, list updates
[Actual] Todo disappeared, but page blanked for one second before refresh
[Impact] Bad experience
```

**Why format matters:** Structured feedback lets AI modify only relevant code, drastically reducing "fix one, break two" risk.

> **Iron rule:** No fuzzy bug reports like "this is wrong" or "feels off". AI will ask you to complete the format before fixing.

---

## Phase 5 — Bug Fix

**Operator does:** Provide feedback, supplement background knowledge AI doesn't have.

### Dissect 6 Phases

| Phase | AI Doing | You Doing |
|---|---|---|
| ① Build feedback loop | Write stable repro test | If AI says "can't reproduce", give more detailed steps |
| ② Minimize repro | Reduce to simplest path | — |
| ③ Hypothesize | List 3-5 possible causes, ranked | Reorder based on your background knowledge |
| ④ Single-variable verify | Change one thing at a time, observe | — |
| ⑤ Fix + regression | Fix, test turns green, write regression test | Confirm with format again |
| ⑥ Post-mortem | Write root cause in commit message | — |

> **Iron rule:** AI must not "read code and guess". If AI says "I think it's XXX" without first writing a repro test, stop it and make it complete Phase ① first.

---

## Phase 6 — Extend

**Operator does:** Same as Phase 1 — input new ideas, answer questions.

### Execution order

```
Step 1 → map        (rescan code, architecture may have changed)
Step 2 → explore    (if new direction, diverge)
Step 3 → recon      (if entering new tech area, research first)
Step 4 → grill      (converge, check against existing decisions)
Step 5 → synthesize → slice → freeze
```

### Veto prevents re-litigation

Before grill questions, AI checks ADR for similar already-rejected solutions. If new request resembles a vetoed one, AI cites the ADR and blocks. You can explicitly say "I want to reconsider" to reopen, but AI won't spontaneously re-litigate.

> **Iron rule:** After each extension slice completes, rerun all existing tests to confirm extension didn't break existing functionality.

---

## Phase 7 — Deploy

**Operator does:** Check `TASK.md`, manually execute push.

### Execution order

```
Step 1 → package    (generate HANDOFF.md handoff doc)
Step 2 → You check TASK.md    (confirm all slices at satisfactory state)
Step 3 → You manually git push (guard ensures AI can't push for you)
Step 4 → You verify core paths in production
```

### HANDOFF.md

Each generated `HANDOFF.md` contains:

```markdown
## This Session Summary
Completed slices: #1, #2, #4
Decisions: [ADR-003] Chose soft delete over hard delete
Open issues: Slice #3 (multi-user permissions) waiting for your decision

## Next Session Starting Point
Next slice: #3
Need your decision: Can all users delete others' Todos, or only creator?
Related docs: docs/CONTEXT.md section 3

## Tool Switch Instructions
From [Tool A] to [Tool B], read order:
1. HANDOFF.md (this file)
2. docs/CONTEXT.md
3. TASK.md
4. map scan current code state
```

### Pre-deploy Checklist

- [ ] Open `TASK.md`, confirm all P0 slices show "Done"
- [ ] Each completed slice, actually click through (per acceptance criteria)
- [ ] Confirm `HANDOFF.md` "open issues" has no critical items
- [ ] Manually execute `git push`

> **Iron rule:** `git push` is always manual. AI has no push authority — guard's physical guarantee, not a trust issue.

---

## Phase 8 — Optimize

(Enable after entering stable iteration phase. Currently just understand triggers.)

### Three Auto-triggers

| Trigger Type | Condition | After Trigger |
|---|---|---|
| Milestone | All slices in a phase complete | Mandatory fuse full-repo architecture scan |
| Threshold | 5+ implemented features you haven't accepted | Halt new features, clear backlog first |
| Manual | You say "do architecture scan" | Immediate execution |

---

## Cross-tool / Cross-session Protocol

Frequent tool switches risk context loss. This protocol prevents fracture.

### Before Switch (in current tool)

```
1. package → generate HANDOFF.md
2. Confirm HANDOFF.md written to root (physical file)
3. Commit a WIP commit (even if code incomplete)
```

### After Switch (in new tool)

```
1. Read HANDOFF.md → Read docs/CONTEXT.md → Read TASK.md
2. map → scan current code state
3. Continue from "next slice" in TASK.md
4. Do not re-discuss frozen decisions
```

> **Iron rule:** New session AI must not rely on its own "memory". All context must come from physical documents. AI memory resets after session ends; physical documents don't.

---

## Seven Iron Rules (Quick Reference)

Stop AI immediately when you see:

| # | Iron Rule | Signal to Stop |
|---|---|---|
| 1 | **No feedback loop, no progress** | AI says "I think it's..." without writing a test to verify |
| 2 | **Tests first, always** | AI says "I'll write code first, tests later" |
| 3 | **You define features, AI writes implementation** | AI in Phase 3 says "I think this feature should change to..." |
| 4 | **Vertical slices, reject horizontal layers** | AI says "I'll build all database tables first" |
| 5 | **Freeze line** | AI in Phase 3 modifies TASK.md feature descriptions on its own |
| 6 | **Veto prevents re-litigation** | AI re-discusses already-rejected solution |
| 7 | **Physical interception of dangerous ops** | AI attempts git push / reset --hard |

---

## Complete Flow Overview

```
Phase 0  Init
  guard → scaffold → compress
  Output: All doc templates in place, git locks installed

Phase 1  Explore & Research
  explore (diverge) → recon (market/tech) → grill (converge + freeze)
  Output: RESEARCH.md + CONTEXT.md + ADR

Phase 2  Design
  design (UI spec) → synthesize (PRD) → slice (break down) → grill (stress-test)
  Output: DESIGN.md + PRODUCT.md + TASK.md

Phase 3  Develop
  freeze (TDD loop) → fuse (architecture check) → package (slice handoff)
  Continuous update: TASK.md + HANDOFF.md

Phase 4  Test
  Your format feedback → freeze (add tests) → dissect (diagnosis)

Phase 5  Bug Fix
  dissect 6 phases → fix → regression verify

Phase 6  Extend
  map → explore/recon → grill → synthesize → slice → freeze → fuse

Phase 7  Deploy
  package → you check TASK.md → you manually push → production verify

Phase 8  Optimize (enable after stable)
  fuse (architecture scan) → freeze (characterization tests) → dissect (perf diagnosis)
```

---

*Plobi Engineering Sovereignty Manual · Human Sovereignty, AI Execution, Physical Documents Against Hallucination.*
