# Learning Claude Code

A guide to getting started with Claude Code, Anthropic's terminal-based AI coding assistant.

> Created by [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)
> Draft

---

## Best Practices Video

[![Claude Code Best Practices](https://img.youtube.com/vi/Ffh9OeJ7yxw/maxresdefault.jpg)](https://youtu.be/Ffh9OeJ7yxw?si=JucaBIBqk6efMWV-)

[Watch: Claude Code Best Practices](https://youtu.be/Ffh9OeJ7yxw?si=JucaBIBqk6efMWV-)

---

## How to Think About Claude Code

Claude Code is the engineer. It writes code, edits files, runs commands, and builds things.

Claude.ai (or ChatGPT or Gemini) is the translator between you and the engineer. It takes your messy thoughts and turns them into clear, precise instructions that the engineer can execute.

Even if you are an engineer yourself, having an AI build robust framing and directions before feeding them to Claude Code is hugely important. The quality of your instructions determines the quality of the output.

**The workflow:**
1. Explain what you want to Claude.ai in plain language
2. Claude.ai helps you refine it into precise instructions
3. Feed those instructions to Claude Code
4. Claude Code executes

Do not skip step 2. The translator makes the engineer better.

---

## The One Constraint That Matters

Most best practices come down to one thing: **Claude's context window fills up fast, and performance degrades as it fills.**

Keep this in mind for everything below.

---

## My Setup

I use two Claudes:

1. **Claude.ai in a browser window** with full project context loaded. This is my thinking partner. I feed it screenshots when I am stuck. It has the big picture and provides Claude Code-friendly language when I need to execute.

2. **Claude Code in VS Code's terminal** with MCP tools connected. This is my hands. It executes, edits files, runs commands, and gets things done.

Claude.ai thinks. Claude Code acts.

**Prompts for this workflow:**
- [Building context at session start](../../prompts/claude/session-workflow/) (start-session-context, start-session-message)
- [Saving context at session end](../../prompts/claude/session-workflow/) (end-of-session-ai, save-session-summary) so you can feed it into the next session

VS Code setup: Claude Code runs in the integrated terminal at the bottom. You see files in the editor, watch changes happen in real time, and keep the conversation visible while reviewing code.

---

## Getting Started

### If You Get Stuck

When in doubt, just explain to Claude.ai what you want to do and your level of understanding. Share screenshots of any errors. It will guide you.

Use this prompt:

```text
I am a complete novice and want to install Claude Code on my computer. I need explicit handholding. I am on [Mac/Windows/Linux]. Please walk me through every step, assuming I have never used the terminal before. Tell me exactly what to type and what I should see after each command.
```

Paste that into Claude.ai, fill in your operating system, and follow along. Send screenshots if something does not look right.

### Prerequisites

**You need:**
- macOS 13.0+, Ubuntu 20.04+, or Windows 10+ (with WSL or Git Bash)
- 4GB+ RAM
- Internet connection
- A Claude Pro, Max, Teams, or Enterprise subscription

**You do not need Node.js** if you use the native installer (recommended).

### Install on Mac

If you do not have Homebrew, install it first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then install Claude Code (pick one method):

**Option 1: Native installer (recommended, auto-updates)**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Option 2: Homebrew (does not auto-update)**
```bash
brew install --cask claude-code
```

### Install on Windows

**Option 1: PowerShell**
```powershell
irm https://claude.ai/install.ps1 | iex
```

**Option 2: With WSL** (install Ubuntu from Microsoft Store, then use the Mac/Linux instructions)

### Install on Linux

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### Verify Installation

```bash
claude doctor
```

This checks your installation and tells you if anything is wrong.

### Authenticate

Run `claude` and follow the prompts to log in with your Claude account.

### Run

```bash
cd your-project
claude
```

That's it. You are now in a conversation with Claude in your terminal.

For troubleshooting, see the [official setup guide](https://code.claude.com/docs/en/setup).

---

## Useful CLI Flags

| Flag | What it does |
|------|-------------|
| `--continue` / `-c` | Resume most recent conversation in this directory |
| `--resume <name>` / `-r` | Resume a specific session by name |
| `--fork-session` | Branch from current history into a new session |
| `--print` / `-p` | One-shot mode: respond and exit (great for scripts) |
| `--add-dir ../other` | Give Claude access to additional directories |

`--continue` does not bloat context. It loads your existing history back in. Claude auto-compacts when context gets full.

**What actually bloats context:**
- MCP servers (each adds tool definitions to every request)
- Large CLAUDE.md files
- Verbose command outputs
- Reading lots of files in one session

---

## Commands Inside Claude

| Command | What it does |
|---------|-------------|
| `/clear` | Clear context, start fresh |
| `/compact` | Summarize and free space |
| `/context` | See what is consuming space |
| `/resume` | List and resume past sessions |

---

## Terminal Shortcuts

Faster than backspacing:

| Shortcut | What it does |
|----------|-------------|
| `Ctrl+U` | Delete entire line |
| `Ctrl+W` | Delete previous word |
| `Ctrl+K` | Delete from cursor to end of line |
| `Ctrl+A` | Jump to beginning of line |
| `Ctrl+E` | Jump to end of line |
| `Option+←` / `Option+→` | Jump word by word (Mac) |

---

## Key Practices

### 1. Never Put Secrets in Code

This is critical. API keys, passwords, tokens, and credentials do not belong in your code. Ever.

**Why:**
- If you commit secrets to git, they are in the history forever (even if you delete them later)
- If your repo is public, your keys are now public
- If your repo is private, anyone with access can see them
- Bots constantly scan GitHub for leaked credentials

**What to do instead:**

Create a `.env` file in your project root:

```text
ANTHROPIC_API_KEY=sk-ant-xxxxx
DATABASE_URL=postgres://user:pass@host:5432/db
STRIPE_SECRET_KEY=sk_live_xxxxx
```

Then add `.env` to your `.gitignore` so it never gets committed:

```text
# .gitignore
.env
.env.local
.env.*.local
```

Your code reads from environment variables instead of hardcoded values. The `.env` file stays on your machine. It never goes to GitHub.

**If you already committed a secret:** Assume it is compromised. Rotate the key immediately. Deleting the file is not enough because git history preserves it.

### 2. Use .gitignore

Every project needs a `.gitignore` file. This tells git which files to never track.

At minimum:

```text
# Secrets
.env
.env.local
.env.*.local

# OS junk
.DS_Store
Thumbs.db

# Editor files
.vscode/
.idea/

# Dependencies
node_modules/
__pycache__/
venv/
```

Create this file before you start coding. It prevents accidents.

### 3. Use CLAUDE.md Files

Create a `CLAUDE.md` file in your project root. This is documentation that Claude reads automatically when you start a session. Put in:

- How the codebase is structured
- Key patterns and conventions
- Things Claude should know before making changes
- Commands to run tests, build, deploy

### 4. Ask Questions First

When onboarding to a new codebase, use Claude Code for learning and exploration before making changes.

```
What does the authentication flow look like in this codebase?
```

```
Where are API endpoints defined?
```

```
How does error handling work here?
```

### 5. Use Multiple Sessions

Context fills up. Start fresh sessions for:

- Different tasks
- Code review (a fresh Claude is not biased toward code it just wrote)
- Exploration vs implementation

**Writer/Reviewer pattern:** Use one session to write code, another to review it.

### 6. Create Custom Commands

Store prompt templates in `.claude/commands/` for repeated workflows:

- Debugging loops
- Log analysis
- Code review checklists
- Deployment procedures

### 7. Use MCP Servers

Claude Code is an MCP client. Connect it to MCP servers to give Claude access to:

- Databases
- APIs
- Documentation systems
- Custom tools

---

## What Claude Code Is Good At

- Navigating large codebases
- Explaining how things work
- Finding relevant files for a task
- Understanding dependencies
- Writing code that matches existing patterns
- Refactoring
- Writing tests

Tasks that would take an hour of searching documentation now take 10-20 minutes.

---

## What to Watch Out For

- **Leaking secrets** (never commit API keys, passwords, or tokens to git)
- Context window filling up (start fresh sessions)
- Sycophancy (see [Anti-Sycophancy Tutorial](../anti-sycophancy/README.md))
- Making changes without understanding existing patterns
- Letting Claude make too many changes at once

---

## Resources

| Resource | What It Is |
|----------|------------|
| [Claude Code Best Practices (Anthropic)](https://www.anthropic.com/engineering/claude-code-best-practices) | Official guide from Anthropic engineering |
| [Claude Code Docs](https://code.claude.com/docs/en/best-practices) | Official documentation |
| [Claude Code in Action (Course)](https://anthropic.skilljar.com/claude-code-in-action) | Official Anthropic training |
| [How Anthropic Teams Use Claude Code (PDF)](https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf) | Internal usage patterns |

---

## Changelog

| Date | Changes |
|------|---------|
| 2026-02-01 | Initial draft |
