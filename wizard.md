# Claude Code Workspace Wizard

The prompt that builds your personal Claude Code workspace from scratch. Designed for knowledge workers — no technical knowledge required.

**Paste everything inside the code block into a new Claude Code session:**

```
You are setting up a personal Claude Code workspace for me. This is not a coding project. Follow each step in order. Do not skip ahead.

IMPORTANT: At the start of each step, briefly explain what we're doing and why it matters — in plain language, as if talking to someone who's never configured software before. No jargon. No file paths. Just "here's what we're doing and why it'll help you."

---

STEP 0 — QUICK CHECK

Explain: "Before we start, I just need to check that everything's in place. This takes two seconds — you don't need to do anything."

Silently verify:
1. git is installed (run: git --version)
2. We are inside a Claude Code Workspace (check for CLAUDE.md and .claude/ directory)

If everything is fine, say: "All good — we're ready to go."
If anything is missing, explain what's wrong in simple terms and tell the user exactly what to do — one step at a time. Do not continue until everything checks out.

---

STEP 1 — WELCOME

Say this:

"Hey — I'm going to ask you a few questions about how you work, then build a workspace that remembers everything. Takes about 10 minutes.

Here's the idea: right now, every time you start a conversation with Claude, it has no idea who you are. You have to explain your role, your projects, your preferences — every single time. After this setup, Claude will already know all of that. Every session just picks up where you left off.

Ready?"

Wait for confirmation before continuing.

---

STEP 2 — UNDERSTAND MY WORLD

Explain: "I'm going to ask you 5 questions about your work. There are no right or wrong answers — I just need to understand what your days actually look like so I can set things up properly."

Ask these questions one at a time. Wait for the full answer before asking the next one. Do not rush.

1. What's your role, and what does a typical work week actually look like?
2. What are the 2–3 projects or responsibilities that take most of your time right now?
3. Who are the most important people in your work — manager, key stakeholders, clients, direct reports?
4. What's the one type of task you do repeatedly that always takes longer than it should?
5. How do you like to communicate? Tone, length, level of formality.

Do not move on until you have a clear picture of how I actually work.

---

STEP 3 — SHOW ME WHAT'S POSSIBLE FOR SOMEONE LIKE ME

Explain: "Now that I know how you work, let me show you what I can actually do for someone in your position. These aren't generic features — they're based on what you just told me."

Based only on what I just told you, give me 5 concrete things you could do for me that I probably haven't considered. Make them specific to my role and situation. Make them feel immediately useful. After each one, ask: does that resonate?

---

STEP 4 — BUILD MY WORK MODES

Explain: "Now we're going to set up your 'modes.' Think of modes like different hats you wear at work. When you start a session, you'll pick which hat you're wearing, and Claude will adjust its behaviour accordingly — the way it talks to you, what it focuses on, what it already knows.

For example, you might have a mode for your main work, one for emails, one for a specific project. Each mode remembers its own context."

Suggest 2–4 work modes based on my answers. Not generic categories — modes shaped around my specific projects and responsibilities. For each one, explain why you're suggesting it. Let me adjust or remove any. For each confirmed mode, generate a context file that captures:
- Who I am in this mode
- What tasks it covers
- How I want you to communicate with me
- What background you should always have loaded

Show me each file before saving. Let me edit. Ask which should be my default. Save confirmed files to .claude/modes/{name}.md

---

STEP 5 — BUILD MY MEMORY LAYER

Explain: "Next, we're going to build your memory — the things Claude should always know about you, no matter which mode you're in. Things like the people you work with, the terms you use, decisions that have already been made.

This way you'll never have to re-explain context. Claude just knows."

Create the following files, asking me for the content of each. For each one, explain what it's for in one sentence before asking. If I say "skip", create the file with the template content and move on — don't ask again.

- People — "Who are the key people in your work? I'll remember their names, roles, and how you work with them."
- Glossary — "Any terms, acronyms, or project names that have a specific meaning in your world? I'll learn your language."
- Decisions — "Anything that's already been decided and shouldn't be reopened? I'll respect those."
- Rules — "Things I should always do, or never do? Like 'always be direct' or 'never use jargon.'"
- Style — based on how I've written in this conversation, describe my communication style back to me and ask me to correct it. "I'm going to describe how you communicate based on this conversation, and you tell me if I got it right."
- Memory — create this empty with the header: "# Session memory — updated automatically". Tell the user: "This one fills itself in. At the end of every session, I'll write a short summary of what we did. Over time, this becomes a log of everything we've worked on together."

Save to .claude/people.md, .claude/glossary.md, .claude/decisions.md, .claude/rules.md, .claude/style.md, .claude/memory.md

---

STEP 6 — BUILD MY SHORTCUTS

Explain: "You mentioned tasks that take too long or come up a lot. Let's turn those into shortcuts — step-by-step recipes that I can run for you instantly every time.

For example, if you write a lot of status update emails, I can have a shortcut where you give me 3 bullet points and I give you a ready-to-send email."

Based on the recurring task I mentioned and anything else that came up, suggest 2–3 shortcuts that would save me real time. For each one I confirm, ask how I currently do it and what good looks like, then generate a file in .claude/skills/.

---

STEP 7 — BUILD MY OUTPUT FORMATS

Explain: "Last thing before we save — let's set up some output formats. These are standard structures for things you write regularly, so you get consistent results every time.

For example, if you often write updates, I can have a format that always includes the right sections in the right order."

Based on the work I described, suggest 2–3 output formats — standard structures I'll use repeatedly. Keep examples relevant to what the user described (don't suggest bug reports to a designer, for instance).

For each one I confirm, generate a template file in .claude/templates/. These templates tell Claude exactly what format to use when producing that type of output.

---

STEP 8 — SET UP MY PROJECTS

Explain: "Remember the projects you mentioned earlier? Let's create folders for them. This is where your actual work will live — PRDs, briefs, stories, whatever you produce. One folder per project, and the contents grow naturally as you work."

Based on the projects and responsibilities the user described in Step 2, suggest project folders. For each one the user confirms, create a folder in projects/{project-name}/. Use lowercase kebab-case for folder names.

If the user doesn't have clear projects yet, just create the projects/ directory and say: "No worries — folders will be created automatically as you start working on things."

---

STEP 9 — SAVE EVERYTHING

Explain: "We're done with the questions. Now I'm going to save everything we just built into your workspace. This happens automatically — you don't need to do anything."

Now:
1. Write all the files we just created into the correct locations in this repo
2. Update CLAUDE.md to reference the memory layer, skills, and templates
3. Commit everything locally with message: "init: my Claude Code Workspace v1.0.0"

Then say: "Everything's saved. Your workspace is set up and ready."

Then ask: "One optional thing — want me to back this up online so you don't lose it? This creates a private copy on GitHub that only you can see. (If you're not sure, just say no — you can do this later.)"

If yes:
  - Check if gh is installed and authenticated. If not, walk me through installing it step by step.
  - Ask me what to name the backup
  - Remove the template remote: git remote remove origin
  - Create my private repo: gh repo create {name} --private --source=. --remote=origin --push
  - Tell me the repo URL and explain: "This is your private backup. Nobody else can see it."

If no:
  - Remove the template remote: git remote remove origin
  - Tell me: "No problem. Your workspace is saved on your computer. If you ever want to back it up, just let me know."

---

STEP 10 — MAKE IT EASY TO COME BACK

Explain: "Your workspace lives in this folder. Every time you want to use it, you need to open Claude Code from here. Let me set up a shortcut so you can do that with one word."

"Want me to add a shortcut so you can start Claude with your workspace by just typing `claude-work` in your terminal?"

If yes:
  - Detect the user's shell (bash or zsh)
  - Add this line to their shell profile (~/.bashrc, ~/.zshrc, or equivalent):
    alias claude-work="cd {workspace-path} && claude"
  - Tell them: "Done. From now on, just open your terminal and type `claude-work`. That's it."

If no:
  - Tell them: "No worries. Whenever you want to use your workspace, just open your terminal and run: cd {workspace-path} && claude"

---

STEP 11 — YOU'RE READY

Explain: "That's it — your workspace is built. From now on, every time you open Claude here, I'll already know who you are, what you're working on, and how you like to communicate."

Tell me the 3 most useful things I can now ask you that I couldn't before — specific to what I told you about my work. Then say:

"A few things you can say anytime during a session:
- **'switch mode'** — change what you're working on without starting over
- **'status'** — see what mode you're in and what we've been working on recently
- **'reset'** — start the setup from scratch if your work changes significantly
- **'export'** — create a version you can share with colleagues
- **'update'** — get the latest improvements to the workspace template"

Then automatically load the default mode: read the default mode file from .claude/modes/, acknowledge it in one sentence, and ask the kick-off question from that mode. The user is now in their first real session.
```

## What the wizard produces

```
your-workspace/
  CLAUDE.md                     ← loads your context every session
  projects/                     ← your work output, one folder per project
  .claude/
    modes/                      ← your personalised work modes
    people.md                   ← your key relationships
    glossary.md                 ← your language and terminology
    decisions.md                ← closed questions
    rules.md                    ← your hard constraints
    style.md                    ← your communication voice
    memory.md                   ← updated automatically each session
    skills/                     ← your saved shortcuts
    templates/                  ← your output formats
  config.json
```

Every future Claude Code session starts already knowing you.
