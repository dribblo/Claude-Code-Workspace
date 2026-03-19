# Claude Code Workspace

You are operating in a structured workspace that follows the Claude Code Workspace standard.

At the start of this session, before doing anything else, follow these steps exactly:

## First-time setup detection

Check if `.claude/modes/` contains any `.md` files (ignore `.gitkeep`).

- **If no mode files exist** → this is a first-time setup. Read `wizard.md` and follow the wizard instructions inside the code block. Do not ask the user to paste anything — just run the wizard directly.
- **If mode files exist** → this is a returning user. Skip to the **Session startup sequence** below.

---

## Session startup sequence

Only run this if mode files already exist in `.claude/modes/`.

### Step 1 — Read config
Read `.claude/config.json`. Note the user's name and default mode.

### Step 2 — Read context
Read all files in `.claude/` — modes, people, glossary, decisions, rules, style, memory, templates. This is your full context.

### Step 3 — List modes
Read all `.md` files in `.claude/modes/`.

### Step 4 — Ask the user
Present the mode list. If a default mode is set, offer it as the Enter shortcut:

```
Hey {name}. What's this about?
  1. work  (default)
  2. my-project
  3. learning

Press Enter for "work", or type a number:
```

### Step 5 — Load mode
Read the full content of the chosen mode file. This is your active context for the session.

### Step 6 — Acknowledge
In one sentence, confirm the active mode and greet the user by name.

### Step 7 — Ask kick-off question
Ask the kick-off question from the mode file. Wait for the response before doing anything else.

---

## Commands

The user can say any of these at any time during a session:

### "switch mode"
Restart from step 4 of the startup sequence. Load the new mode and its kick-off question.

### "status"
Show:
- Current active mode
- Number of sessions logged in memory.md
- Last 3 session summaries from memory.md
- Number of modes, skills, and templates configured
- Whether a remote is configured (backed up to GitHub or local only)

### "reset"
Re-run the wizard from scratch. Ask: "This will rebuild your workspace from the beginning. Your current files will be backed up to .claude/backup/ first. Continue?" If yes, copy all current .claude/ files to .claude/backup/{timestamp}/, then run the wizard.

### "update"
Pull the latest template improvements from the upstream Claude Code Workspace repo. Steps:
1. Check if the upstream remote exists. If not, add it: git remote add upstream https://github.com/dribblo/Claude-Code-Workspace.git
2. Fetch upstream: git fetch upstream
3. Show what's new (compare SPEC.md, wizard.md, modes/ templates, CONTRIBUTING.md)
4. Ask the user which updates to apply
5. Merge selected changes, preserving all user files in .claude/

Never overwrite the user's personalised files (.claude/modes/, .claude/people.md, etc.)

### "export"
Create a shareable version of the workspace setup:
1. Copy the workspace structure to a temporary directory
2. Strip all personal information from .claude/ files (names, people, specific context)
3. Keep the mode structure, rules format, and template formats intact
4. Replace personal content with placeholder text like the original templates
5. Save to .claude/exports/ or show the anonymised files
6. Tell the user: "Share this with anyone who has a similar role — they can use it as a starting point."

---

## Workspace contents

### Projects
- `projects/` — where actual work output lives. One subfolder per project.
- When producing documents (PRDs, briefs, stories, etc.), save them into `projects/{project-name}/`.
- Create project folders as needed. Do not pre-structure them — let the contents be organic.

### Memory layer
- `.claude/people.md` — key people, roles, and relationships
- `.claude/glossary.md` — domain terms, personas, and internal language
- `.claude/decisions.md` — settled decisions that should not be reopened
- `.claude/rules.md` — hard constraints for every session
- `.claude/style.md` — communication style preferences
- `.claude/memory.md` — session log, updated automatically

### Skills (shortcuts)
- `.claude/skills/` — reusable workflow shortcuts (created by the wizard)

### Templates (output formats)
- `.claude/templates/` — standard output formats (created by the wizard)

---

## Rules for this session

* Do not skip the startup sequence, even if the user starts with a task
* Stay in the active mode context for the full session
* If the user asks to update or create a mode, edit the file and commit the change
* When producing output (PRDs, briefs, stories, etc.), save to `projects/{project-name}/` and check .claude/templates/ for a matching template and use that format
* When a skill shortcut is invoked, read the corresponding file from .claude/skills/ and follow its process

## Auto-save

Whenever you create or edit any file inside `.claude/` (modes, people, glossary, decisions, rules, style, skills, templates, config), automatically commit the change. If a remote is configured, push as well. Use a short commit message describing what changed (e.g. "update glossary", "add email mode"). Do not ask the user for permission — just save silently.

## Session memory

At the end of every session, before the user leaves:

1. Write a 3-bullet summary of what was done this session to `.claude/memory.md` — append it under a date heading
2. Review the session for anything worth adding to the workspace:
   - New terms mentioned → suggest adding to glossary
   - New people mentioned → suggest adding to people.md
   - Decisions made → suggest adding to decisions.md
   - New recurring patterns → suggest a new skill or template
3. Ask: "Before we wrap up, I noticed [suggestions]. Want me to add any of these to your workspace?"
4. Commit with message: "memory: session update" — push if a remote is configured

---

*Claude Code Workspace spec v1.0.0*
