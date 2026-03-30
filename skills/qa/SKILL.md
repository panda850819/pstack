---
name: ps-qa
description: |
  Browser-based QA. Opens real pages, runs user flows, finds bugs.
  Use when UI has changed, or when asked to "test this", "QA",
  or "check the page". Requires browser automation tool.
---

# QA

## Step 1: Load Context

1. Read pstack config from CLAUDE.md.
2. Search `{learnings_dir}` for `type: pitfall` related to UI or the changed components.
3. Read the brief (if exists in `docs/briefs/`) to understand expected behavior.

## Step 2: Determine Flows

From the diff, brief, or user instructions, identify what to test:
- Which pages/URLs changed?
- What are the core user flows affected?
- What are the edge cases? (empty states, error states, loading states)

If unclear, ask the user: "What flows should I test?"

## Step 3: Test

Use the browser automation tool available in your environment to run real user flows:

1. Navigate to the page
2. Perform the core user flow (click, fill, submit)
3. Check for:
   - Console errors
   - Visual regressions (screenshots if supported)
   - Broken interactions (buttons that don't work, forms that don't submit)
   - Missing states (loading, error, empty)
   - Accessibility issues (contrast, keyboard nav)
4. Test edge cases identified in Step 2

For each bug found:
```
[BUG] page/flow — description
  Steps to reproduce: ...
  Expected: ...
  Actual: ...
  Action: AUTO-FIX | ASK
```

## Step 4: Fix

AUTO-FIX bugs that are mechanical (CSS, missing null check, wrong URL).
ASK about bugs that involve design or architecture decisions.

After fixing, re-run the affected flow to verify the fix.

## Step 5: Write Learnings

If a UI pattern or browser-specific pitfall was discovered, write a learning.
Common examples:
- "This component breaks on mobile viewport"
- "Form validation fires before user finishes typing"
- "Loading state missing on slow network"
