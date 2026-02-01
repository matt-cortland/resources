> A resource from [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)
> Free to use and adapt. If you find it useful, I'd love to hear about it.

# Start Session — Project Context Template

A template for the project context file you attach at the start of every new Claude.ai conversation.

---

## Tools Used

`Claude.ai` `Claude Code` `VS Code` `GitHub`

---

## My Setup

This prompt assumes the following setup:

| Tool | How It's Used |
|------|---------------|
| **Claude.ai** | Browser-based chat for planning and building |
| **Claude Code** | Running in VS Code's terminal panel |
| **VS Code** | Code editor with Claude Code extension installed |
| **GitHub** | Linked to VS Code, authenticated and signed in |

**Note on Claude.ai:** This is written for Claude.ai, but you can adapt it for ChatGPT or Gemini. I recommend Claude.ai because it pairs naturally with Claude Code.

**Using different tools?** Customize the prompt to match your setup.

---

## What This Does

This template gives you the structure for a project context file. You fill it in once with your project's details — name, tech stack, repos, key decisions — then attach it at the start of every new session alongside your latest session summary. It's the standing context that doesn't change between sessions.

---

## The Template

Click the **copy button** (top-right of the code block), paste into a new file, and replace everything in `[brackets]` with your actual project details. Save it as `start-session-context.md`.

```text
# [Your Project Name] — Project Context

## What This Is

This file contains the standing context for [Your Project Name]. It is uploaded at the start of every new Claude.ai conversation alongside the latest session summary. Read this file and the session summary before responding.

## How This Conversation Will Be Structured

### Message 1 (already sent)
A short message with this file and a session summary attached. The session summary tells you what was built, what's pending, and what to work on next. If it includes a transcript path from a previous conversation, you can read that transcript for additional detail beyond what the summary covers.

### Message 2 (coming next)
Architecture and reference docs for this project. (Delete this section if you keep all your context in this file instead of separate docs.)

### Message 3 (coming last)
My Claude Code instructions. This tells you my technical level, how to format responses, and how file handoffs work between Claude.ai and Claude Code. Follow those instructions for the rest of the conversation.

Do not start working until you've received all three messages. After my third message, confirm what you understand and ask if there's anything else before we begin.

---

## Project Overview

[What are you building? Who is it for? What stage is it at? Write 2-3 sentences.]

---

## Tech Stack

| Tool | Role |
|------|------|
| [e.g., Lovable] | [e.g., Frontend builder] |
| [e.g., Supabase] | [e.g., Database, auth, storage] |
| [e.g., GitHub] | [e.g., Code repos] |

---

## Key Repos

| Repo | Purpose |
|------|---------|
| [your-username/repo-name] | [What this repo contains] |

---

## Database Projects

(Delete this section if you don't use a hosted database.)

| Project | Purpose | ID |
|---------|---------|-----|
| [project-name] | [What it's for] | [Project ID from your dashboard] |

---

## Key Architecture Decisions Already Made

(These are decisions you don't want Claude to revisit or contradict.)

- [e.g., All auth handled by Supabase, no custom auth]
- [e.g., Single codebase deployed to multiple domains]
- [Add your own]

---

## Docs Index

(If you have separate documentation files, list them here. Delete this section if all your context is above.)

Core docs (always uploaded):

| File | What It Tells You |
|------|-------------------|
| [filename.md] | [What it covers] |

Situational docs (uploaded when relevant):

| File | What It Tells You | When To Include |
|------|-------------------|-----------------|
| [filename.md] | [What it covers] | [When you'd upload this] |
```

---

## What Happens Next

- Save the filled-in file as `start-session-context.md`
- Attach it every time you start a new session using the [Start Session — Opening Message](../start-session-message/) prompt
- Update it whenever your project's fundamentals change (new repos, new tools, new architecture decisions)

---

## Changelog

| Date | Changes |
|------|---------|
| 2025-02-01 | Initial version |
