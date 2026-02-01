> A resource from [Matt Cortland](https://mattcortland.com) / [Prime Directive AI](https://primedirective.ai)
> Free to use and adapt. If you find it useful, I'd love to hear about it.

# Save Session Summary to Repo

Save your downloaded session summary into your project's code repository so it's version controlled and accessible to Claude Code in future sessions.

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

After you've downloaded a session summary from Claude.ai (using the [End of Session — Claude.ai Summary](../end-of-session-ai/) prompt), this prompt tells Claude Code to copy that file from your Downloads folder into your project repo. This means your session summaries are version controlled alongside your code — you can look back at them anytime, and Claude Code can read them in future sessions.

---

## The Prompt

Click the **copy button** (top-right of the code block), then **replace `YYYY-MM-DD` with today's date** and **replace `your-repo-name` with your actual repo name** before pasting into Claude Code.

```text
Copy ~/Downloads/session-summary-YYYY-MM-DD.md to the your-repo-name repo at docs/session-summaries/session-summary-YYYY-MM-DD.md. Create the session-summaries folder if it doesn't exist. Then commit with message "Add session summary YYYY-MM-DD" and push.
```

Don't worry if you forget to replace the date or repo name — Claude Code will ask you to clarify.

---

## What Happens Next

- Claude Code copies the file into your repo at `docs/session-summaries/`
- It commits the file and pushes to GitHub
- Your session summary is now saved permanently with your project
- You can find past summaries anytime in that folder

---

## Changelog

| Date | Changes |
|------|---------|
| 2025-02-01 | Initial version |
