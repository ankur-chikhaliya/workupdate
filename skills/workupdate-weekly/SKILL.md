---
name: workupdate-weekly
description: >
  Writes a weekly work update in the 3P format (Progress, Plans, Problems) from
  the last 7 days of git history and the current session. Use when the user
  says "weekly update", "weekly report", "3P update", "workupdate weekly",
  "what did I ship this week", or asks for a week-in-review for their manager.
---

# workupdate-weekly

Paste-ready 3P update, readable in 30-60 seconds. Format adapted from
marketplace skill `internal-comms` (`examples/3p-updates.md`, agentic-awesome-skills).

## Steps

1. Ask team/project name only if not given and not inferable from repo name.
2. Collect evidence (skip git silently if not a repo):
   - Progress: `git log --since="7 days ago" --author="$(git config user.name)" --pretty='%h %ad %s' --date=short` and `--shortstat` for size.
   - Plans: `git status --short`, open branches, anything user or session said is next.
   - Problems: blockers from session or commits (reverts, "wip", "fix" loops).
3. Cluster by theme, not commit. Larger scope = less granular. Metrics only if from git or user.

## Format

```
<emoji matching the work> <Team/Project> (<Mon DD – Mon DD>)
Progress: <1-3 sentences: shipped, milestones, with numbers where known>
Plans: <1-3 sentences: top priorities next week>
Problems: <1-3 sentences: what slows the work; "None" if none>
```

## Rules

- Each section max 3 sentences. Matter-of-fact, data-driven, not prose-heavy.
- Audience has some but not much context: no jargon, no commit hashes.
- Never invent work or metrics. Unknown = leave out.
- Draft only. Do not send or post.
