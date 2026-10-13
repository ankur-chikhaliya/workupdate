---
name: workupdate
description: >
  Writes a work update as 5-7 plain bullets of finished work, after reviewing
  the commits for bugs and issues. Use when the user says "workupdate", "work
  update", "daily update", "standup", "what did I do today", or asks for a
  status message to send to their team.
---

# workupdate

Output: 5-7 bullets, past tense, outcome-first. No headers, no sections.

## Steps

1. Gather commits (skip silently if not a git repo):
   - Today: `git log --since=midnight --author="$(git config user.name)" --pretty='%h %s'`
   - None today → use the most recent commit day and say so in one line.
   - User range ("since monday") overrides. Also read `git status --short` and session work.
2. Review before writing. For each commit read `git show <hash> --stat` and the diff of non-trivial ones. Look for: bugs, fixes that fix earlier work, missing error handling, config or env assumptions, untested paths, TODOs.
3. Write the bullets from what the code actually does, not just commit titles.

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
- Name concrete things (screens, endpoints, modules), not "various improvements".
- Real issues found in review go in a final bullet: "Identified <issue>; recommended <fix>". Only issues seen in the diff.
- Never invent work, metrics, or fixes. State if build/tests were not run.
- Print only. Do not send or post.
