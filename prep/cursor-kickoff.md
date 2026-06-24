# Cursor kickoff — paste this to start a build session

Cursor automatically loads the project context from `.cursor/rules/project.mdc`, so you don't have to explain the stack or deploy flow. Use the message below to start a working session, then drive it step by step with `live-build-prompt-sequence.md`.

---

## Opening message (paste into Cursor chat)

> I'm working on Traveler Supply Exchange, the static prototype in `index.html`. It's a single self-contained HTML file with inline CSS/JS, no framework, no build step. Keep it that way.
>
> For this session I want to work on the "I need it tonight" hero flow only. Make changes directly in `index.html`, in small reviewable steps, and tell me what you're about to change before you change it. Don't add new screens, frameworks, or dependencies unless I ask. No em-dashes in any copy.
>
> Start by reading `index.html` and giving me a quick map of the screens and how `go(id)` switches between them. Then wait for my next instruction.

---

## When you're ready to ship a change

Ask Cursor to hand you the commands, then run them yourself one line at a time:

```
git add -A
```
```
git commit -m "describe the change"
```
```
git push
```

Vercel auto-deploys to https://travelers-supply-exchange.vercel.app within a minute.

---

## Reminders for showing tool fluency (interview)
- Prompt small, one screen or one decision at a time.
- Say what you expect before running a prompt; react to what you got after.
- When Cursor overreaches, cut it back out loud: "that's more than I asked for."
- You're the editor, the tool is the intern. The detailed step-by-step is in `live-build-prompt-sequence.md`.
