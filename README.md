# Claude Code Workspace

> The standard for Claude Code workspaces.

`Claude Code Workspace` is an open convention for making Claude Code context-aware from the first message of every session. Instead of re-explaining who you are and what you're working on every time, Claude Code reads your workspace and asks which mode to start in.

**Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code)** — available in the terminal or inside the Claude desktop app.

<!-- TODO: Add demo GIF showing the wizard and mode selector in action -->
<!-- ![Claude Code Workspace demo](demo.gif) -->

---

## How it works

Claude Code automatically reads `CLAUDE.md` at the start of every session. `Claude Code Workspace` defines what that file should contain — and how to structure the rest of your workspace — so Claude always starts informed, focused, and in the right mode.

```
Your repo/
  CLAUDE.md          ← auto-loaded by Claude Code. This is the plugin.
  .claude/
    modes/
      work.md        ← context for work tasks
      my-project.md  ← context for a specific project
      learning.md    ← context for study sessions
    templates/       ← output formats (bug reports, stories, briefs)
    skills/          ← reusable workflows
    config.json      ← your name, default mode, preferences
```

Every session starts like this:

```
Claude: Which mode today?
  1. work
  2. my-project
  3. learning

You: 1

Claude: Work mode. What's the task?
```

That's it. No re-explaining. No setup. Just work.

---

## Quickstart

Open Claude Code and run:

```bash
git clone https://github.com/dribblo/Claude-Code-workspace.git
cd Claude-Code-workspace
```

The wizard starts automatically. It will interview you about your work, build your personalised mode files, and set up your entire workspace in a single conversation.

---

## Modes

A mode is a Markdown file that tells Claude:

- **Who you are** in this context
- **What this mode is for**
- **How you want Claude to behave**
- **Background knowledge** it should always have
- **A kick-off question** to open every session

| Mode | Use case |
|---|---|
| `work.md` | Emails, documents, meetings, professional communication |
| `personal.md` | Life admin, decisions, planning, personal projects |
| `learning.md` | Understanding topics deeply, studying, research |
| `creative.md` | Writing, brainstorming, ideation, creative projects |
| `project-template.md` | Blank template for any specific project |

---

## Commands

Say any of these during a session:

| Command | What it does |
|---|---|
| `switch mode` | Change to a different mode mid-session |
| `status` | See your current mode, session history, and workspace health |
| `reset` | Re-run the wizard from scratch (backs up your files first) |
| `update` | Pull the latest improvements from the template repo |
| `export` | Create a shareable, anonymised version of your setup |

---

## Features

- **Auto-save** — changes to your workspace are committed automatically
- **Session memory** — Claude writes a summary at the end of every session
- **Smart enrichment** — Claude suggests adding new terms, people, and decisions it notices during your session
- **Output templates** — standardised formats for bugs, stories, emails, meeting briefs
- **Workflow skills** — reusable workflows for recurring tasks

---

## Why this exists

Claude Code is powerful out of the box — but blank. Every session starts the same way: you explain who you are, what you're working on, how you like to communicate. Again. And again.

`Claude Code Workspace` solves this with a simple convention: a structured workspace that Claude Code understands from the first word. It's not a plugin, an extension, or a wrapper. It's a file structure and a spec. It works today, with the Claude Code you already have, with no installs.

---

## Contributing

Contributions welcome — especially new mode templates. See `CONTRIBUTING.md`.

---

## License

MIT — use it, fork it, build on it.
