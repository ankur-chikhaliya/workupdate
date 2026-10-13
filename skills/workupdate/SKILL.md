---
name: workupdate
description: >
  Writes a daily work update (standup note) from git commits, uncommitted
  changes, and the current session, in the Yesterday / Today / Blockers format.
  Use when the user says "workupdate", "work update", "daily update", "standup",
  "what did I do today", or asks for a status message to send to their team.
---

# workupdate

Paste-ready daily standup note. Format adapted from marketplace skill
`team-collaboration-standup-notes` (agentic-awesome-skills).

## Steps

1. Collect evidence (skip git silently if not a repo):
   - `git log --since="yesterday 00:00" --author="$(git config user.name)" --pretty='%h %ad %s' --date=short`
   - `git status --short`, `git diff --stat` for uncommitted work.
   - Anything done earlier in this session. User args ("this week", ticket ids) override defaults.
2. Merge related commits into one bullet. Write delivered value, not activity ("Shipped auth" not "Worked on auth").
3. Link PR / ticket when known. Add % or milestone for ongoing work.

## Format

```
# Standup - YYYY-MM-DD

## Yesterday / Last Update
• <outcome> - <PR / ticket link if known>

## Today / Next
• <planned work> - <target: end of day / milestone>

## Blockers / Notes
• <blocker> - **Needs:** <specific help> - **From:** <person/team>
• <dependency> - **ETA:** <date>
```

## Rules

- Bullets, 1-2 lines each. Bold blockers. Max 8 bullets total.
- Plain language. Include impact only if known. Never invent work, metrics, or links.
- Section with no evidence → omit (Blockers: write "None" only if user said so).
- Zero evidence at all → ask what user worked on.
- Print only. Do not send or post.
