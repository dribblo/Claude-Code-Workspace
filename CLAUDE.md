# claude-context

You are operating in a structured workspace that follows the claude-context standard.

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

### Step 2 — List modes
Read all `.md` files in `.claude/modes/`.

### Step 3 — Ask the user
Present the mode list. If a default mode is set, offer it as the Enter shortcut:

```
Which mode today?
  1. work  (default)
  2. my-project
  3. learning

Press Enter for "work", or type a number:
```

### Step 4 — Load mode
Read the full content of the chosen mode file. This is your active context for the session.

### Step 5 — Acknowledge
In one sentence, confirm the active mode and greet the user by name.

### Step 6 — Ask kick-off question
Ask the kick-off question from the mode file. Wait for the response before doing anything else.

## Rules for this session

* Do not skip the startup sequence, even if the user starts with a task
* Stay in the active mode context for the full session
* If the user says "switch mode", restart from step 3
* If the user asks to update or create a mode, edit the file and commit the change

---

*claude-context spec v1.0.0*
