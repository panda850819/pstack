---
name: ps-ship
description: |
  Test, commit, and create PR. One command from "code done" to
  "PR open". Use when asked to "ship", "create PR", or "we're done".
---

# Ship

## Step 0: Read Config

Read pstack config from CLAUDE.md for: test command, tag format, release preference.

## Step 1: Pre-flight

1. Run the project's test command. If tests fail, stop and report.
2. Run `git diff --stat` to see uncommitted changes.
3. Run `git log origin/{main}..HEAD --oneline` for commit history.

## Step 2: Load Learnings

Search `{learnings_dir}` for `type: pitfall` related to the changed files.
If any match, do a quick sanity check against the diff before proceeding.

## Step 3: Commit

If there are uncommitted changes:
1. Analyze the diff
2. Generate a conventional commit message (`type(scope): description`)
3. Stage relevant files (never `git add -A`)
4. Commit (don't amend, don't skip hooks)

## Step 4: Tag (if configured)

If pstack config has `tag: semver`:
1. Read current version from package.json, VERSION, or latest git tag
2. Determine bump type from commits (feat = minor, fix = patch)
3. Create tag: `git tag v{version}`

If `tag: none`: skip.

## Step 5: Push + PR

1. Push the branch (and tags if created)
2. Create PR with:
   - Title: short, under 70 chars
   - Body: what changed, why, how to test
   - If learnings were written this session, mention in PR body

## Step 6: Release (if configured)

If pstack config has `release: true`:
- Create GitHub Release from the tag
- Auto-generate release notes from commits

If `release: false`: skip.

## Step 7: Write Learnings (if applicable)

If the ship process itself revealed something useful:
- A test that caught a subtle bug
- A deploy pattern worth remembering
- A CI configuration gotcha

Write a learning to `{learnings_dir}/pitfalls/` or `{learnings_dir}/patterns/`.
