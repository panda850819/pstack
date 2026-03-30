---
name: ps-review
description: |
  Code review with learning integration. Searches past learnings
  before reviewing, writes new learnings after. Use when asked to
  "review", "check my code", or before creating a PR.
---

# Code Review

## Step 1: Scope

1. Read pstack config from CLAUDE.md.
2. Run `git branch --show-current`. If on the main branch, stop: "Nothing to review — you're on main."
3. Run `git diff origin/{main} --stat`. If no diff, stop.
4. Get the full diff: `git diff origin/{main}`

## Step 2: Load Learnings

Search `{learnings_dir}` for learnings related to the changed files:

```bash
# Search by file paths mentioned in the diff
grep -rl "relevant-file-path" {learnings_dir}/ 2>/dev/null

# Search by keywords from the diff (function names, patterns)
grep -rl "keyword" {learnings_dir}/ 2>/dev/null
```

Read matching files. For each match, note:
"Prior learning: [key] (confidence N/10, from [date])"

Apply confidence decay per `lib/confidence.md` rules. Skip learnings with effective confidence < 3.

## Step 3: Review

Use the eng agent's judgment to review the diff. Focus on:
- Bugs that pass CI but break production
- Race conditions, N+1 queries, stale reads
- Security issues (injection, auth bypass)
- Missing error handling at system boundaries
- Test gaps for changed code paths

Output format per finding:
```
[P0-P3] (confidence: N/10) file:line — description
  Fix: what to do
  Action: AUTO-FIX | ASK
```

**AUTO-FIX**: mechanical fixes (typos, missing null checks, obvious bugs). Apply directly.
**ASK**: judgment calls (architecture, design trade-offs). Batch all ASK items into one AskUserQuestion.

If no issues found: "Review clean. No issues found."

## Step 4: Write Learnings

After review completes, evaluate whether any non-obvious pattern was discovered.

Test: "Would this save time in a future session on this codebase?"

If yes, check `{learnings_dir}` for existing learnings with similar key.
- If match exists: update `last_seen` and add new context.
- If no match: write new file to `{learnings_dir}/{category}/{slug}.md`

Use the format from `lib/learning-format.md`.

If nothing worth recording: skip silently. Not every review produces learnings.
