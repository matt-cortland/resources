> A resource from [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)
> Free to use and adapt. If you find it useful, I'd love to hear about it.

# End of Session — Claude Code Summary

Get a technical snapshot of your project's current state at the end of a working session.

---

## Tools Used

`Claude Code` `VS Code` `GitHub`

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

When you paste this into Claude Code, it scans your project and outputs a technical summary of everything that changed during your session — commits, file paths, database changes, what's working, what's broken, and what to do next. You then copy this output and paste it into Claude.ai alongside the [End of Session — Claude.ai Summary](../end-of-session-ai/) prompt to generate a complete session summary file.

---

## The Prompt

Click the **copy button** (top-right of the code block), then paste into Claude Code.

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

---

## What Happens Next

- Claude Code outputs the summary in your terminal
- **Copy the entire output**
- Paste it into Claude.ai along with the [End of Session — Claude.ai Summary](../end-of-session-ai/) prompt
- Claude.ai will merge it with your conversation context to create a complete session summary

---

## Changelog

| Date | Changes |
|------|---------|
| 2025-02-01 | Initial version |
