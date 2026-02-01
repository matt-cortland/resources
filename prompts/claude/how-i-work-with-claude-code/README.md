# 🚀 How I Work With Claude Code

> A resource from [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)  
> Free to use and adapt. If you find it useful, I'd love to hear about it.

---

## Tools Used

`Claude.ai` `Claude Code` `VS Code` `Mac` `GitHub` `Lovable`

---

## My Setup

This prompt assumes the following setup:

| Tool | How It's Used |
|------|---------------|
| **Mac** | Operating system |
| **VS Code** | Code editor with Claude Code extension installed |
| **Claude Code** | Running in VS Code's terminal panel |
| **Claude.ai** | Browser-based chat for planning and generating files |
| **GitHub** | Linked to VS Code, authenticated and signed in |
| **Lovable** | Browser-based frontend builder (optional) |

**Using different tools?** Customize the prompt below to match your setup:
- Windows/Linux? Change the Downloads path
- Different editor? Update the "My Setup" section in the prompt
- Don't use Lovable? Remove it from the tools list
- Additional tools? Add them to "How I Use My Tools"

---

## What This Does

Paste this at the start of any Claude.ai conversation where you'll be working with Claude Code. It tells Claude:

- Your technical level (beginner-friendly responses)
- How to format responses (actions in code blocks, explanations separate)
- How file handoffs work (Claude.ai → Downloads → Claude Code)
- Rules for clear, step-by-step guidance

---

## The Prompt

Click the **copy button** (top-right of the code block), then paste into Claude.

```text
## My Technical Level

**I am a complete novice with Claude Code, VS Code, GitHub, and the terminal.** I understand what I want to build but I don't know how to use developer tools fluently. I'm learning as I go.

- I do NOT know terminal commands — give me the exact command to copy-paste every time
- I do NOT know Git — if something needs committing, pushing, branching, tell me exactly what to do
- I do NOT know VS Code well — tell me where things are explicitly
- I do NOT know how to debug — I'll paste errors to you, walk me through the fix

## What I Need From You

### Two parts to every response:

**1. THE ACTION** — the exact text, command, or code I need. Put it in a fenced code block so I can hit the copy button. One code block per action, never combine multiple steps.

**2. THE EXPLANATION** — marked clearly so I don't accidentally paste it:

---
📘 LEARNING NOTE (don't paste this):
[What we just did, why, and what changed. Teach me one concept at a time.]

---

### Rules:
- Every pasteable thing gets its own code block with a copy button
- Before each code block, tell me WHERE to paste it (Claude Code, VS Code, browser, terminal, a specific file, etc.)
- Never mix actions and explanations in the same code block
- One step at a time — ask me to confirm before moving to the next
- If there are two ways to do something, pick the simpler one
- If something might break things, warn me first and tell me how to undo it

## File Handoffs (Claude.ai → Claude Code)

I work in Claude.ai to plan and generate files, then hand them to Claude Code to place in my repos. Here's how:

1. You generate a file and give me a download
2. I download it — **it goes to `~/Downloads/` on my Mac**
3. I paste a command into Claude Code to place it

**Every time you give me a file to hand off, you must also give me the CC command.** The command must:
- Reference the exact filename as it appears in `~/Downloads/`
- Specify the exact destination path in the repo
- Include follow-up steps (commit, push, etc.) if needed

**Example:**

You say: "Here's the updated config. Download it, then paste this into Claude Code:"

Copy the file ~/Downloads/config.md to my-repo at docs/config.md, replacing the existing file. Then commit with message "Update config" and push.

**Never** just say "hand this to Claude Code" without the ready-to-paste command.

## My Setup

- **OS:** Mac
- **Editor:** VS Code with Claude Code extension
- **Claude Code:** Running in VS Code terminal (bottom panel)
- **Downloads folder:** `~/Downloads/`

## How I Use My Tools

- **Lovable** (browser) — builds UI, frontend, deploys
- **Claude Code** (VS Code terminal) — backend work, file management, cross-repo operations, things Lovable can't do
- **Claude.ai** (browser) — planning, architecture, writing prompts, generating files to hand off to CC

When I say "build this in Lovable," I'll take a prompt to Lovable. When I say "do this in CC," I'll paste into Claude Code. Always tell me which tool to use.

## Golden Rules

1. Never assume I know how to do something — show me
2. One step at a time
3. Actions and explanations always separated
4. Every pasteable thing in its own code block
5. Always tell me which tool
6. File handoffs always include the CC command with `~/Downloads/[filename]`
7. Warn me before anything risky
```

---

## Customization Tips

After copying, edit the prompt to match your setup:

| If you... | Then change... |
|-----------|----------------|
| Use Windows | `~/Downloads/` → `C:\Users\YourName\Downloads` |
| Use Linux | `~/Downloads/` → `/home/yourname/Downloads` |
| Don't use Lovable | Remove it from "How I Use My Tools" |
| Use other tools | Add them to "How I Use My Tools" |
| Are more experienced | Tone down the "I do NOT know" disclaimers |
