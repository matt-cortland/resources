> A resource from [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)
> Free to use and adapt. If you find it useful, I'd love to hear about it.

# End of Session — Claude.ai Summary

Generate a downloadable session summary that captures everything from your current working session.

---

## Tools Used

`Claude.ai`

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

When you paste this into Claude.ai at the end of a working session, it generates a downloadable markdown file called `session-summary-YYYY-MM-DD.md` that captures everything you discussed and built. The summary is comprehensive enough that a brand new Claude conversation can pick up exactly where you left off.

**Optional but recommended:** Before using this prompt, run the [End of Session — Claude Code Summary](../end-of-session-cc/) prompt first. That gives you a technical snapshot you can paste at the bottom of this prompt, making the final summary even more accurate.

---

## The Prompt

Click the **copy button** (top-right of the code block), then paste into Claude.ai. If you have output from the Claude Code end-of-session prompt, paste that after the last line.

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

---

## What Happens Next

- Claude creates a file called `session-summary-YYYY-MM-DD.md` and gives you a download link
- **Download the file** — you'll attach it when starting your next session
- To save it into your project repo, use the [Save Session Summary](../save-session-summary/) prompt

---

## Changelog

| Date | Changes |
|------|---------|
| 2025-02-01 | Initial version |
