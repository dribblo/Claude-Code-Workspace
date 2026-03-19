# Claude Code Workspace

> Stop chatting with AI. Start building with it.

Most people use AI the same way every time: open a chat, explain who they are, explain what they need, get a generic answer, close the tab. Next day, repeat.

This project is for people who are done with that.

Claude Code Workspace is a file structure that makes Claude Code context-aware from the first message — every session. It knows your role, your team, your domain, your communication style, and your standards. No plugin, no extension, no code. Just structured markdown files and a 10-minute setup.

**The result:** You stop explaining yourself and start doing real work. A rough idea becomes a structured PRD. A product decision becomes a stakeholder update tailored to the right person. A messy brain dump becomes execution-ready output — in your format, in your voice, with your context already loaded.

**Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code)** — Anthropic's coding agent, available in the terminal or the Claude desktop app.

---

## See it in action

[Claude-Code-for-PM](https://github.com/dribblo/Claude-Code-for-PM) is a working example — a Product Manager's workspace built from this template. It has real modes (product, launch, alignment, review), real skills (idea-to-PRD, PRD-to-stories), and real templates (PRDs, founder updates, launch assessments).

In one session, the PM went from *"I need a PRD for insurance integration via API"* to a full, execution-ready PRD with workflow breakdowns, functional requirements, edge cases, and user stories — because the workspace already knew the domain, the team, the personas, and the output format.

That's the difference between chatting and building.

---

## How it works

Claude Code automatically reads a file called `CLAUDE.md` when it starts. This is a built-in feature — not something this project adds.

What this project does is give you a structured `CLAUDE.md` and a set of files that make Claude context-aware across sessions. Everything here is prompt engineering — structured markdown that tells Claude how to behave.

```
Your workspace/
  CLAUDE.md            ← auto-read by Claude Code at session start
  wizard.md            ← interactive setup (runs once)
  projects/            ← where your actual work output lives
    insurance-api/     ← one folder per project
    onboarding/
  .claude/
    config.json        ← your name, default mode
    modes/
      work.md          ← context for work tasks
      my-project.md    ← context for a specific project
    people.md          ← key people and relationships
    glossary.md        ← domain terms and language
    decisions.md       ← settled decisions (not reopened)
    rules.md           ← hard constraints for every session
    style.md           ← your communication style
    memory.md          ← session log (auto-updated)
    skills/            ← reusable workflow shortcuts
    templates/         ← output formats you use repeatedly
```

Every session starts like this:

```
Claude: Hey Daniel. What's this about?
  1. product  (default)
  2. launch
  3. alignment
  4. review

You: 1

Claude: Product mode. What are we working on today —
        a new feature, refining something existing, or making a decision?
```

No re-explaining. No setup. Just work.

---

## Quickstart

**1. Clone this repo and open Claude Code inside it:**

```
git clone https://github.com/dribblo/Claude-Code-Workspace.git
cd Claude-Code-Workspace
```

**2. Open Claude Code and say "let's go".**

Claude reads `CLAUDE.md`, sees it's your first time, and starts a setup wizard — about 10 minutes of questions about your work, your people, your recurring tasks, and how you communicate. No technical knowledge needed.

**3. That's it.**

Every future session in this folder starts with your modes, your context, and your standards already loaded. The workspace grows with you — Claude suggests additions to your glossary, people, and decisions as you work.

---

## What you get

### Modes
Contexts you switch between. Each one tells Claude who you are, what you're doing, how to behave, and what to ask first.

| Example mode | Use case |
|---|---|
| `work.md` | Day-to-day tasks, documents, communication |
| `strategy.md` | Research, analysis, one-pagers |
| `alignment.md` | Adapting the same thinking for different audiences |
| `review.md` | Pressure-testing logic and flows before they ship |
| `learning.md` | Studying, understanding new topics deeply |

### Memory layer
Persistent context that applies across all modes — people, glossary, decisions, rules, communication style, and a session log that grows automatically.

### Skills
Reusable shortcuts for recurring work. Example: "idea-to-PRD" takes a rough idea and produces a structured PRD with requirements, edge cases, and user stories — following your template, in your format.

### Templates
Output formats you use repeatedly — PRDs, stakeholder updates, user stories, assessments. Claude uses the right template automatically when producing output.

---

## Commands

These work because `CLAUDE.md` instructs Claude to respond to them. They're prompt engineering, not native features — reliable in practice, but not guaranteed.

| Phrase | What it does |
|---|---|
| `switch mode` | Change to a different mode mid-session |
| `status` | See your current mode and recent session history |
| `reset` | Re-run the wizard from scratch (backs up first) |
| `update` | Pull latest improvements from the template repo |
| `export` | Create a shareable, anonymised version of your setup |

---

## Who this is for

Anyone who uses Claude Code regularly and is tired of starting from zero. The wizard is designed for non-technical users — no coding, no config files, no terminal knowledge required beyond opening Claude Code.

Examples of what people build:

| Role | Modes they create | Skills they use |
|---|---|---|
| **Product Manager** | product, launch, alignment, review | idea-to-PRD, PRD-to-stories, reformat-for-audience |
| **Founder** | strategy, ops, investor-updates | pitch-deck-section, metrics-summary |
| **Consultant** | client-work, proposals, research | brief-to-proposal, meeting-notes-to-actions |
| **Designer** | design-critique, research, specs | user-flow-review, design-brief |
| **Writer** | drafting, editing, pitching | outline-to-draft, rewrite-for-audience |

---

## How it's built

There's no code. The entire system is markdown files that work with Claude Code's built-in behavior of reading `CLAUDE.md` at startup. The architecture:

1. **`CLAUDE.md`** — session loader. Reads config, loads context, presents modes, starts the session.
2. **`wizard.md`** — one-time setup. Asks questions, builds personalized modes/skills/templates.
3. **`.claude/`** — your workspace. Modes, memory, skills, templates — all growing over time.

This means it works with stock Claude Code. No dependencies, no installs, no updates to wait for.

---

## Contributing

Contributions welcome — especially **mode templates for specific roles**. If you're a lawyer, designer, teacher, researcher, consultant, or chief-of-staff and you've built a workspace that works, share the structure so others can start from it.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

---

## License

MIT — use it, fork it, build on it.
