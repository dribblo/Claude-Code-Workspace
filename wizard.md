# Claude Code Workspace Wizard

The prompt that builds your personal Claude Code workspace from scratch. Designed for knowledge workers — no technical knowledge required.

**Paste everything inside the code block into a new Claude Code session:**

```
You are setting up a personal Claude Code workspace for me. This is not a coding project. Follow each step in order. Do not skip ahead.

---

STEP 0 — PREREQUISITES CHECK

Before anything else, verify:
1. git is installed (run: git --version)
2. We are inside a Claude Code Workspace (check for CLAUDE.md and .claude/ directory)

If anything is missing, tell me exactly what to do to fix it — one command at a time. Do not continue until everything checks out.

---

STEP 1 — WELCOME

Say this:

"Hey — I'm going to ask you a few questions about how you work, then build a workspace that remembers everything. Takes about 10 minutes. After that, every Claude session starts already knowing you. Ready?"

Wait for confirmation before continuing.

---

STEP 2 — UNDERSTAND MY WORLD

Ask me the following questions one at a time. Wait for my full answer before asking the next one. Do not rush.

1. What's your role, and what does a typical work week actually look like?
2. What are the 2–3 projects or responsibilities that take most of your time right now?
3. Who are the most important people in your work — manager, key stakeholders, clients, direct reports?
4. What's the one type of task you do repeatedly that always takes longer than it should?
5. How do you like to communicate? Tone, length, level of formality.

Do not move on until you have a clear picture of how I actually work.

---

STEP 3 — SHOW ME WHAT'S POSSIBLE FOR SOMEONE LIKE ME

Based only on what I just told you — not generic features — give me 5 concrete things you could do for me that I probably haven't considered. Make them specific to my role and situation. Make them feel immediately useful. After each one, ask: does that resonate?

---

STEP 4 — BUILD MY WORK MODES

Suggest 2–4 work modes based on my answers. Not generic categories — modes shaped around my specific projects and responsibilities. For each one, explain why you're suggesting it. Let me adjust or remove any. For each confirmed mode, generate a context file that captures:
- Who I am in this mode
- What tasks it covers
- How I want you to communicate with me
- What background you should always have loaded

Show me each file before saving. Let me edit. Ask which should be my default. Save confirmed files to .claude/modes/{name}.md

---

STEP 5 — BUILD MY MEMORY LAYER

Create the following files, asking me for the content of each. If I say "skip", create the file with the template content and move on — don't ask again.

- .claude/people.md — the people I mentioned: name, role, how we work together
- .claude/glossary.md — terms, project names, acronyms, internal language I use
- .claude/decisions.md — things already decided that you should never reopen
- .claude/rules.md — things you must always do, and things you must never do
- .claude/style.md — based on how I've written in this conversation, describe my communication style back to me and ask me to correct it
- .claude/memory.md — create this empty with the header: "# Session memory — updated automatically"

---

STEP 6 — BUILD MY WORKFLOW LIBRARY

Based on the recurring task I mentioned and anything else that came up, suggest 2–3 workflows that would save me real time. For each one I confirm, ask how I currently do it and what good looks like, then generate a workflow file in .claude/skills/.

---

STEP 7 — BUILD MY OUTPUT TEMPLATES

Based on the work I described, suggest 2–3 output templates — standard formats I'll use repeatedly. Examples:
- A bug report template
- An email format
- A user story structure
- A meeting brief layout

For each one I confirm, generate a template file in .claude/templates/. These templates tell Claude exactly what format to use when producing that type of output.

---

STEP 8 — SAVE THE WORKSPACE

Now:
1. Write all the files we just created into the correct locations in this repo
2. Update CLAUDE.md to reference the memory layer, skills, and templates
3. Commit everything locally with message: "init: my Claude Code Workspace v1.0.0"

Then ask: "Want me to back this up to a private GitHub repo? (requires GitHub CLI — say no if you're not sure)"

If yes:
  - Check if gh is installed and authenticated. If not, walk me through installing it.
  - Ask me what to name the repo
  - Remove the template remote: git remote remove origin
  - Create my private repo: gh repo create {name} --private --source=. --remote=origin --push
  - Tell me the repo URL

If no:
  - Remove the template remote: git remote remove origin
  - Tell me: "Your workspace is saved locally. You can back it up to GitHub anytime by running: gh repo create {name} --private --source=. --remote=origin --push"

This folder is now my personal workspace. Every time I open Claude Code here, it loads my context.

---

STEP 9 — MAKE IT EASY TO START

Claude Code loads your workspace based on the folder you open it from. To make sure you always start in the right place, offer to create a shortcut:

"Want me to add a shortcut so you can start Claude with your workspace by just typing `claude-work` in your terminal?"

If yes:
  - Detect the user's shell (bash or zsh)
  - Add this line to their shell profile (~/.bashrc, ~/.zshrc, or equivalent):
    alias claude-work="cd {workspace-path} && claude"
  - Tell them: "Done. From now on, just open your terminal and type claude-work."

If no:
  - Tell them: "To start a session, open your terminal and run: cd {workspace-path} && claude"

---

STEP 10 — CLOSE WITH WHAT'S NEXT

Tell me the 3 most useful things I can now ask you that I couldn't before — specific to what I told you about my work. Then tell me about these commands I can use anytime:

- **"switch mode"** — change to a different mode mid-session
- **"status"** — see your current mode, session history, and workspace health
- **"reset"** — re-run the wizard from scratch
- **"export"** — create a shareable, anonymised version of your workspace setup
- **"update"** — pull the latest improvements from the Claude Code Workspace template

Then automatically load the default mode: read the default mode file from .claude/modes/, acknowledge it in one sentence, and ask the kick-off question from that mode. The user is now in their first real session.
```

## What the wizard produces

```
your-workspace/
  CLAUDE.md                     ← loads your context every session
  .claude/
    modes/                      ← your personalised work modes
    people.md                   ← your key relationships
    glossary.md                 ← your language and terminology
    decisions.md                ← closed questions
    rules.md                    ← your hard constraints
    style.md                    ← your communication voice
    memory.md                   ← updated automatically each session
    skills/                     ← your saved workflows
    templates/                  ← your output formats
  config.json
```

Every future Claude Code session starts already knowing you.
