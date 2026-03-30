# pstack

Agent-driven development with a learning loop.

## Available Skills

- `/ps-init` — one-time project setup
- `/ps-brief` — structured requirement gathering
- `/ps-review` — code review with learnings integration
- `/ps-qa` — browser-based QA
- `/ps-ship` — test + commit + PR
- `/ps-compound` — extract learnings from solved problems
- `/ps-learn` — search and manage learnings
- `/ps-retro` — weekly retrospective

## Available Commands

- `/ps-sprint` — full flow: brief → build → review → qa → ship → compound
- `/ps-design` — design-driven flow
- `/ps-fix` — debug + fix + review + ship + compound
- `/ps-quick` — small change: review + ship

## Agent Personas

Read from `agents/` directory. Use their Iron Laws and judgment, not generic prompts.

## Learnings

Stored at the path configured in the project's CLAUDE.md under `## pstack > learnings`.
Default: `docs/learnings/`. Format: see `lib/learning-format.md`.
