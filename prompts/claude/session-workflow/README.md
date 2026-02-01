# Session Workflow Prompts

End Claude.ai sessions cleanly so new conversations can pick up exactly where you left off.

> Created by [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)
> Free to use and adapt. If you find it useful, I'd love to hear about it.

---

## Tools Used

`Claude.ai` `Claude Code` `VS Code` `GitHub`

---

## The Problem

Claude.ai conversations have a context limit. The longer you work, the more Claude "forgets" from earlier in the conversation. Eventually you'll see signs:

- Claude starts asking about things you already discussed
- It contradicts decisions you made earlier
- Responses get slower or less accurate
- You get a warning that context is running low

When this happens, you need to start a fresh conversation. But a new Claude has zero memory of what you built, what decisions you made, or what's next on your list.

**The fix:** Before your session ends, capture everything into a summary file. When you start a new conversation, attach that summary. The new Claude reads it and picks up exactly where the old one left off.

This guide shows you how to end sessions (that's why it's first) and then how to start new ones with full context.

---

## When to Act

### Checking Your Context Usage

You can ask Claude how much context it has used. Paste this:

```text
What percentage of your context window have I used?
```

Claude will tell you something like "approximately 45% of my context window."

**Recommendation:** Start the session ending workflow when you hit around 90%. This gives you room to generate the summary without running out of space.

### What Context Compression Looks Like

When conversations get very long, Claude.ai automatically compresses earlier parts to make room for new messages. You'll see a message like:

> "I've compressed earlier parts of our conversation to continue. I still have context about our main topics and recent work..."

This happens automatically — you don't trigger it.

### What Compression Means for Memory

When Claude compresses:
- **Recent messages:** Fully remembered, word for word
- **Middle of conversation:** Summarized — key decisions and outcomes kept, exact wording lost
- **Early messages:** Heavily compressed — only major themes and conclusions retained

This is why Claude starts "forgetting" specific details, file paths, or exact decisions you made early on. The information isn't gone — it's been compressed into a summary that loses granularity.

**Important:** Compression is not the same as running out of context. You can keep working after compression. But each compression loses more detail from earlier work, so the earlier you create a proper session summary, the more accurate it will be.

---

## My Setup

These prompts assume the following setup:

| Tool | How It's Used |
|------|---------------|
| **Claude.ai** | Browser-based chat for planning and building |
| **Claude Code** | Running in VS Code's terminal panel |
| **VS Code** | Code editor with Claude Code extension installed |
| **GitHub** | Linked to VS Code, authenticated and signed in |

**Note:** This is written for Claude.ai, but you can adapt it for ChatGPT or Gemini. I recommend Claude.ai because it pairs naturally with Claude Code.

---

## The Workflow

```
End of Session                          Start of Session
─────────────────                       ─────────────────
1. End Session CC    ──┐
   (Claude Code)       │                1. Start Message
                       ├── creates ──►     (Claude.ai)
2. End Session AI    ──┘  summary          + attach context
   (Claude.ai)                             + attach summary
       │
       ▼
3. Save Summary
   (Claude Code)
```

---

# Ending a Session

Run these prompts when Claude is running low on context, or when you're done working for the day.

## Step 1: Get Technical Summary from Claude Code

Paste this into **Claude Code**. It outputs a technical snapshot of your project state.

```text
Generate a technical session summary I can paste into my Claude.ai conversation before it generates its own session summary. Include:

1. Session Date — Today's date

2. What We Did — Bullet list of completed work this session (commits, files created, configs changed, migrations run, functions deployed)

3. Current Repo State — For each repo we touched:
   - Latest commit hash and message
   - Branch we're on
   - Any uncommitted or unstaged changes
   - Key folder structure (just the parts relevant to today's work)

4. Key Files Changed — Full paths of files created, modified, or deleted — grouped by repo

5. Database State — Any tables created/modified, policies added, seeds run. Include the SQL if it was meaningful. (Skip this section if we didn't touch the database.)

6. Environment / Config — Any secrets added, env vars set, DNS changes, domain configurations. (Skip if none.)

7. What's Working — Features or flows that are confirmed functional right now

8. What's Broken or Incomplete — Anything that errored, wasn't finished, or needs follow-up. Include error messages if relevant.

9. Outstanding Commands — Any commands I was given by Claude.ai that I haven't run yet, or that failed and need retry

10. Next Steps — What to work on next, in priority order

11. Context Docs to Load — Which project docs should I upload to the new Claude.ai conversation based on what we were working on

Format as markdown. Don't create a file — just output it in chat so I can copy-paste it into my Claude.ai conversation.
```

**After:** Copy the output. You'll paste it into Claude.ai in the next step.

---

## Step 2: Generate Session Summary in Claude.ai

Paste this into **Claude.ai**. If you have output from Step 1, paste it after the last line.

```text
We're running low on context. I need you to create a session summary file so I can hand it off to the next conversation.

CRITICAL: Create the file FIRST

Do NOT display the summary in chat. Do NOT ask me to confirm anything. Do NOT show me a preview.

Create a downloadable markdown file called session-summary-YYYY-MM-DD.md (using today's date) and give me the download link. Put ALL of the summary content in the file, not in chat. Your chat message should just be a brief sentence and the download — nothing else.

Check for transcript

Before writing the summary, check if a conversation transcript exists at /mnt/transcripts/. When Claude.ai conversations get very long, earlier parts get compressed to save space — but a full transcript is automatically saved at this path. If a transcript exists:
- Read it (incrementally if large) to make sure you capture everything from the full conversation, including anything that may have been compressed out of your current context.
- In the summary file, include the full transcript file path at the top so the next session can read it for details beyond what the summary covers.
- Note the conversation start time from the first transcript entry.

Claude Code technical summary

I may paste a technical summary from Claude Code after this prompt (either below the marker at the bottom, or as a separate follow-up message). If present, incorporate it into your session summary — it contains verified repo state, commit hashes, file paths, and database changes that are ground-truth from the actual codebase. Merge it with the conversation context you have (architecture decisions, reasoning, discussions) to create one unified summary.

If no Claude Code summary is provided, generate the summary from conversation context alone.

What to include in the file:

1. Session Header
- Date, approximate duration, what project(s) were worked on
- Transcript path (if found)
- One-paragraph plain English summary of the session

2. What We Accomplished
Everything we built, configured, decided, or changed. Be specific — include file names, function names, repo names, table names, and any other identifiers. Group by topic if we worked on multiple things.

3. What Changed From Previous State
If we modified existing architecture, schema, docs, or code — document what changed and why.

4. What Still Needs To Be Done
Three categories:
- Immediate (next session) — things we were about to do, said we'd do next, or left half-finished
- Short-term — things that came up but weren't urgent
- Medium-term — bigger features or changes mentioned but not started

5. Known Bugs and Issues
Anything broken, partially working, or behaving unexpectedly.

6. Architecture Decisions Made
Decisions about how things should work — naming conventions, patterns, approaches, trade-offs. These are easy to forget between sessions.

7. Key Files, Repos, and IDs
Tables of all repos, database projects, important file paths, and any API keys or project IDs mentioned (names only, not values).

8. Challenges and Solutions
Problems we hit, how we solved them (or didn't), and any workarounds in place.

9. Effective Prompts
Any particularly effective prompts used during the session — include them verbatim so they can be reused.

10. Diagrams and Visualizations
Any structures, flows, or diagrams discussed — include the ASCII visualizations.

11. Commands Not Yet Run
Any commands generated but not yet pasted — list them with exact text.

12. Docs to Load Next Session
Which project docs should be uploaded to the next conversation, in priority order.

Format rules:
- Markdown with headers and tables for scanning
- Code blocks for commands, config, or anything copy-pasteable
- Comprehensive enough that a completely new Claude session with zero prior context can pick up exactly where we left off
- When in doubt, include it — too much context is better than too little

Output: One downloadable markdown file. Brief chat message with the download link. That's it.

---

CLAUDE CODE TECHNICAL SUMMARY (if available, paste below):

```

**After:** Download the file Claude creates.

---

## Step 3: Save Summary to Your Repo

Paste this into **Claude Code**. Replace `YYYY-MM-DD` with today's date and `your-repo-name` with your repo.

```text
Copy ~/Downloads/session-summary-YYYY-MM-DD.md to the your-repo-name repo at docs/session-summaries/session-summary-YYYY-MM-DD.md. Create the session-summaries folder if it doesn't exist. Then commit with message "Add session summary YYYY-MM-DD" and push.
```

**After:** Your summary is now version controlled in your repo.

---

# Starting a Session

Use these when starting a fresh Claude.ai conversation.

## Step 1: Create Your Project Context (One-Time Setup)

Copy this template, fill in your project details, and save as `start-session-context.md`. You only do this once per project.

```text
# Project Context

## What This Is

This file contains the standing context for this project. It is uploaded at the start of every new Claude.ai conversation alongside the latest session summary. Read this file and the session summary before responding.

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

## Step 2: Start a New Session

Paste this into **Claude.ai** when starting a new conversation.

**Attach two files:**
1. Your `start-session-context.md`
2. Your latest `session-summary-YYYY-MM-DD.md`

```text
I'm continuing work on this project. I've attached two files:

1. start-session-context.md — Project context, tech stack, repos, architecture decisions, and how this conversation will be structured (three messages).
2. session-summary-YYYY-MM-DD.md — Summary from my last working session. This tells you what was built, what's pending, and what to work on next. If it includes a transcript path, you can read that for additional detail.

Read both files completely. Do not respond yet — I have two more messages to send (project docs and my Claude Code instructions). Wait until you've received all three messages before starting.
```

**After:**
- Message 2: Upload any architecture or reference docs Claude needs
- Message 3: Paste your Claude Code instructions
- Claude confirms what it understands and you start building

---

## Changelog

| Date | Changes |
|------|---------|
| 2025-02-01 | Initial version |
