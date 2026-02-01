# Session Workflow Prompts

A set of prompts for maintaining context across Claude.ai conversations. Use these to end sessions cleanly and start new ones with full context.

> Created by [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)

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

## Prompts

### Ending a Session

| Prompt | Tool | What It Does |
|--------|------|--------------|
| [End Session — Claude Code](end-of-session-cc/) | Claude Code | Gets technical snapshot (commits, files, DB changes) |
| [End Session — Claude.ai](end-of-session-ai/) | Claude.ai | Creates downloadable session summary |
| [Save Session Summary](save-session-summary/) | Claude Code | Commits summary to your repo |

### Starting a Session

| Prompt | Tool | What It Does |
|--------|------|--------------|
| [Start Session — Message](start-session-message/) | Claude.ai | Opening message with attachments |
| [Start Session — Context Template](start-session-context/) | Template | Project context file you customize once |

---

## Quick Start

**First time?** Start with [Start Session — Context Template](start-session-context/) to create your project context file.

**Ending a session?**
1. Run [End Session — Claude Code](end-of-session-cc/) in Claude Code
2. Paste output into Claude.ai with [End Session — Claude.ai](end-of-session-ai/)
3. Download the summary file
4. Run [Save Session Summary](save-session-summary/) in Claude Code

**Starting a new session?**
1. Use [Start Session — Message](start-session-message/) with your context file and latest summary attached
