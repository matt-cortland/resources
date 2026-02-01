> A resource from [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)
> Free to use and adapt. If you find it useful, I'd love to hear about it.

# Start Session — Opening Message

Kick off a new Claude.ai working session with full context from your last session.

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

This is the first thing you paste into Claude.ai when starting a new working session. It tells Claude you're attaching two files — your project context and your latest session summary — and to wait for two more messages before starting work. This gives Claude the full picture before it writes a single line of code.

---

## The Prompt

Click the **copy button** (top-right of the code block), then **replace `[Your Project Name]` with your project name** before pasting into Claude.ai.

At the same time, **attach two files**:
1. Your `start-session-context.md` (see [Start Session — Project Context](../start-session-context/))
2. Your latest `session-summary-YYYY-MM-DD.md`

```text
I'm continuing work on [Your Project Name]. I've attached two files:

1. start-session-context.md — Project context, tech stack, repos, architecture decisions, and how this conversation will be structured (three messages).
2. session-summary-YYYY-MM-DD.md — Summary from my last working session. This tells you what was built, what's pending, and what to work on next. If it includes a transcript path, you can read that for additional detail.

Read both files completely. Do not respond yet — I have two more messages to send (project docs and my Claude Code instructions). Wait until you've received all three messages before starting.
```

---

## What Happens Next

- Claude reads both attachments and waits
- **Message 2:** Upload any architecture or reference docs Claude needs for today's work
- **Message 3:** Paste your Claude Code instructions (your technical level, formatting preferences, how file handoffs work)
- Claude confirms what it understands and you start building

---

## Changelog

| Date | Changes |
|------|---------|
| 2025-02-01 | Initial version |
