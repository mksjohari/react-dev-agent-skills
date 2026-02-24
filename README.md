# React Developer Agent skills

A collection of agent-optimized skills on React frontend development for AI coding assistants. Curated by [@jasontslxd](https://www.github.com/jasontslxd) for personal use.

## Quickstart

Depending on the agent used, you should clone it into the appropriate locations and rename the folder to the appropriate name.

| Location         | Agent  | Scope         |
| ---------------- | ------ | ------------- |
| .cursor/skills   | Cursor | Project level |
| .claude/skills   | Claude | Project level |
| .codex/skills    | Codex  | Project level |
| ~/.cursor/skills | Cursor | Global level  |
| ~/.claude/skills | Claude | Global level  |
| ~/.codex/skills  | Codex  | Global level  |

E.g. If you are using cursor, and want to install it globally, clone in your root folder `~/`, then rename `~/react-dev-agent-skills` to `~/.cursor`. If the folder already exists, just copy the relevant skills you want into the `skills` folder.

The resulting folder structure should look like this:

```
.cursor/
└── skills/
    └── react-frontend-development/
        └── SKILL.md
```
