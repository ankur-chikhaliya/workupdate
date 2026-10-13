# workupdate

Two Claude Code skills that write your work update from git history and the current session. No API keys, nothing is sent anywhere. Output is a draft to paste.

| Skill | Output |
|---|---|
| `workupdate` | Daily standup: Yesterday / Today / Blockers |
| `workupdate-weekly` | Weekly 3P update: Progress / Plans / Problems |

Formats adapted from `team-collaboration-standup-notes` and `internal-comms` in [agentic-awesome-skills](https://github.com/sickn33/agentic-awesome-skills).

## Install

As a plugin:

```
/plugin marketplace add ankur-chikhaliya/workupdate
/plugin install workupdate@workupdate
```

Or as plain skills (any agent that reads SKILL.md):

```
cp -r skills/* ~/.claude/skills/    # Claude Code
cp -r skills/* ~/.agents/skills/    # other agents
```

## Use

```
/workupdate
/workupdate since monday
/workupdate-weekly my-team
```

Run inside a git repo. Without git, it asks what you worked on.

## License

MIT
