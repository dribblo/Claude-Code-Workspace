# claude-context Wizard

The prompt that builds your personal Claude Code workspace from scratch. Designed for knowledge workers — no technical knowledge required.

**Paste everything inside the code block into a new Claude Code session:**

```
You are setting up a personal Claude Code workspace for me. This is not a coding project. Follow each step in order. Do not skip ahead.

---

STEP 1 — UNDERSTAND MY WORLD

Ask me the following questions one at a time. Wait for my full answer before asking the next one. Do not rush.

1. What's your role, and what does a typical work week actually look like?
2. What are the 2–3 projects or responsibilities that take most of your time right now?
3. Who are the most important people in your work — manager, key stakeholders, clients, direct reports?
4. What's the one type of task you do repeatedly that always takes longer than it should?
5. How do you like to communicate? Tone, length, level of formality.

Do not move on until you have a clear picture of how I actually work.

---

STEP 2 — SHOW ME WHAT'S POSSIBLE FOR SOMEONE LIKE ME

Based only on what I just told you — not generic features — give me 5 concrete things you could do for me that I probably haven't considered. Make them specific to my role and situation. Make them feel immediately useful. After each one, ask: does that resonate?

---

STEP 3 — BUILD MY WORK MODES

Based on my answers, suggest 2–4 work modes that reflect how I actually operate. Not generic categories — modes shaped around my specific projects and responsibilities. For each one, explain why you're suggesting it. Let me adjust or remove any. For each confirmed mode, generate a context file that captures:
- Who I am in this mode
- What tasks it covers
- How I want you to communicate with me
- What background you should always have loaded

Show me each file before saving. Let me edit. Ask which should be my default. Save confirmed files to .claude/modes/{name}.md

---

STEP 4 — BUILD MY MEMORY LAYER

Create the following files, asking me for the content of each:

- .claude/people.md — the people I mentioned: name, role, how we work together
- .claude/glossary.md — terms, project names, acronyms, internal language I use
- .claude/decisions.md — things already decided that you should never reopen
- .claude/rules.md — things you must always do, and things you must never do
- .claude/style.md — based on how I've written in this conversation, describe my communication style back to me and ask me to correct it
- .claude/memory.md — create this empty with the header: "# Session memory — updated automatically"

---

STEP 5 — BUILD MY WORKFLOW LIBRARY

Based on the recurring task I mentioned and anything else that came up, suggest 2–3 workflows that would save me real time. For each one I confirm, ask how I currently do it and what good looks like, then generate a workflow file in .claude/skills/.

---

STEP 6 — SAVE THE WORKSPACE

Now:
1. Write all the files we just created into the correct locations in this repo
2. Update CLAUDE.md to reference the memory layer and skills
3. Commit everything locally with message: "init: my claude-context workspace v1.0.0"

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

STEP 7 — CLOSE WITH WHAT'S NEXT

Tell me the 3 most useful things I can now ask you that I couldn't before — specific to what I told you about my work. Then ask: what's the first thing you'd like to tackle?
```

## What the wizard produces

```
your-private-repo/
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
  config.json
```

Every future Claude Code session starts already knowing you.
