# claude-context Specification

**Version:** 1.0.0
**Status:** Draft
**License:** MIT

---

## Overview

`claude-context` defines a workspace convention for Claude Code that enables persistent, mode-aware sessions. It is a file structure, a set of naming conventions, and a `CLAUDE.md` contract — not a library, plugin, or binary.

---

## 1. File structure

A compliant workspace MUST include the following:

```
CLAUDE.md        (required) session loader
.claude/         (required) context directory
  modes/         (required) context mode files
    {mode-name}.md  (at least one required)
  config.json    (required) workspace settings
```

Additional files and directories inside `.claude/` are permitted and ignored by this spec.

---

## 2. CLAUDE.md

`CLAUDE.md` MUST be placed in the root of the workspace. It is the session loader — the file Claude Code reads automatically at the start of every session.

### 2.1 Required behaviour

`CLAUDE.md` MUST instruct Claude Code to perform the following steps, in order, at the start of every session:

1. **Read config** — load `.claude/config.json`
2. **List modes** — read all `.md` files in `.claude/modes/`
3. **Ask the user** — present the mode list and ask which one to use
4. **Load mode** — read the chosen mode file into active context
5. **Acknowledge** — confirm the active mode in one sentence
6. **Ask kick-off question** — use the question defined in the mode file

### 2.2 Default mode

If `config.json` defines a `defaultMode`, CLAUDE.md SHOULD offer it as the default option.

### 2.3 Reference implementation

See `CLAUDE.md` in this repo.

---

## 3. Mode files

Mode files are Markdown documents in `.claude/modes/`. Each defines a context mode.

### 3.1 Naming

- Lowercase letters, numbers, and hyphens only
- Extension must be `.md`

### 3.2 Required sections

```
Mode: {name}
Who I am
What this mode is for
How I want Claude to behave
Relevant context
Kick-off question
```

### 3.3 Kick-off question

Must be the last section. Format:

```
Kick-off question
Start by asking: "{Your question here}"
```

---

## 4. config.json

```json
{
  "userName": "string (required)",
  "defaultMode": "string (optional)",
  "version": "string (optional)",
  "createdAt": "string (optional — ISO 8601)"
}
```

## 5. Versioning

Follows semantic versioning. Workspaces MAY declare target spec version in config.json.

## 6. Contributing to the spec

Changes require an open issue before a PR is accepted.
