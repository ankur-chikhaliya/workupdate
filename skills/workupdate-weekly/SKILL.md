---
name: workupdate-weekly
description: >
  Writes a weekly work update as 5-7 plain bullets of finished work, after
  reviewing the last 7 days of commits for bugs and issues. Use when the user
  says "weekly update", "weekly report", "workupdate weekly", "what did I ship
  this week", or asks for a week-in-review for their manager.
---

# workupdate-weekly

Output: 5-7 bullets, past tense, outcome-first. No headers, no sections. Same style as `workupdate`, wider window, coarser grain.

## Steps

1. Gather commits (skip silently if not a git repo):
   - `git log --since="7 days ago" --author="$(git config user.name)" --pretty='%h %ad %s' --date=short`
   - `git log --since="7 days ago" --author="$(git config user.name)" --shortstat` for size.
   - User range ("this sprint", "last 2 weeks") overrides. Also read `git status --short` and session work.
2. Review before writing. Read `git show --stat` per commit and the diff of non-trivial ones. Look for: bugs, fixes of earlier work in the same week, reverts, missing error handling, env or config assumptions, untested paths, TODOs.
3. Cluster commits by theme, not one bullet per commit. Write from what the code does, not commit titles.

## Bullet shape

One sentence each, starts with a past-tense verb. Group by theme, in this order, skipping empty ones:

1. **Delivered / Implemented** - features shipped, with scope in one clause.
2. **Enhanced** - improvements to existing flows.
3. **Fixed** - bugs, listed together in one bullet when small.
4. **Completed / Verified** - testing, checks, docs, findings and recommended fixes.

Style sample (shape only, not content):

```
Delivered a comparison of the web and mobile feature sets and implemented parity across billing, contacts, reports and documents.
Enhanced the order flow with automatic status updates, free-slot detection and live refresh of lists and counts.
Fixed branch-switching data issues, stale calendar refresh, truncated text and incorrect relative timestamps.
Completed responsive testing across key screens and verified the main flows end to end; documented gaps with recommended fixes.
```

## Rules

- 5-7 bullets. Fewer only if there is truly less work; never pad.
- Larger window = less granular: themes and outcomes, not file names.
- Numbers only from git (commits, files changed) or the user. Never guess impact.
- Real issues found in review go in a final bullet: "Identified <issue>; recommended <fix>". Only issues seen in the diff.
- Never invent work. State if build/tests were not run.
- Print only. Do not send or post.
