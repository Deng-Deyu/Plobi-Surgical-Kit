# Plobi Domain Glossary

## Baseline
A pristine git commit state with zero uncommitted changes. The absolute, immutable starting point before surgery.
_Avoid_: dirty tree, loose changes.

## Surgical Dissection
The process of isolating a regression or defect by freezing a 2-second deterministic fail-to-pass feedback loop before executing implementation fixes.
_Avoid_: loose debugging, vibe guessing.

## Deep Fusion
The architectural practice of collapsing scattered shallow components into high-leverage modules with minimal interface footprints to save cognitive load.
_Avoid_: shallow abstraction, boilerplate pass-through.

## Freeze
Test-driven development with a red-green-refactor loop. Write one failing test, write minimal code to pass, repeat. Never refactor while RED.

## Veto
A permanently recorded rejection of a feature request or design direction. Prevents repeated re-litigation across sessions.

## Vertical Slice
An end-to-end, independently demoable feature that cuts through all layers (schema, API, UI, tests). Preferred over horizontal layer-by-layer implementation.

## HITL vs AFK
- **HITL** (Human In The Loop): Requires human decision before proceeding.
- **AFK** (Away From Keyboard): AI can complete autonomously.

## Guard
Physical interception of dangerous operations (git push, reset --hard, clean, branch -D) at the tool level, not the policy level.

## Compression
Ultra-terse communication mode that drops filler while preserving full technical accuracy. Used to conserve token budget during implementation phases.

## Package
Cross-session handoff document that allows a fresh agent to continue work without context loss.
