# Claude Code Cheat Sheet

Quick reference for running the interview session smoothly. Keep this open in a second window.

Reminder: two-hour live test — use these to stay fast and unstuck, not to add ceremony. If a command isn't saving you time right now, skip it.

## Starting a session

| Do this | Command |
|---|---|
| Start fresh in the current folder | `claude` |
| Continue the most recent conversation here | `claude -c` (or `--continue`) |
| Pick a past session to resume | `claude -r` (or `--resume`) |
| Start with a one-off prompt | `claude "fix the failing test in foo.py"` |

## Mid-session controls

| Do this | How |
|---|---|
| Interrupt a response that's going the wrong way | `Esc` once |
| Rewind to an earlier point / edit a previous message | `Esc` twice (double-tap) |
| Clear conversation history but keep project files (CLAUDE.md etc.) | `/clear` |
| Force a manual context summarization (before it auto-triggers) | `/compact` |
| Quit | `Ctrl+C` twice |

Use `/clear` between unrelated sub-tasks in the same 2-hour block if the conversation is getting long and noisy — it's cheaper than starting a whole new `claude` process. Because state lives in `LIVING.md` (see below), `/clear` and auto-compaction stop being risky — the next message just re-reads the file and picks up where things stopped.

## Adding info / memory

| Do this | How |
|---|---|
| Quick one-off note to project memory | Start a message with `#` — it gets appended to `CLAUDE.md` directly, no need to open the file |
| Bigger charter/convention changes | Edit `CLAUDE.md` / `AGENTS.md` directly (or ask Claude to) |
| Scaffold a new CLAUDE.md from scratch | `/init` |
| Give it a one-off doc/log/error to read | Just paste it in chat, or point at the file path — no special command needed |

## Branching / isolating work

Two different meanings of "branch" — pick the one you mean:

- **Git branch** (normal source control): just ask Claude to `git checkout -b <name>`, or do it yourself in another terminal. This is what you want most of the time in a single 2-hour task.
- **Worktree** (parallel isolated copy, e.g. to let Claude try an approach without touching your main working tree): explicitly say "work in a worktree" — Claude creates an isolated git worktree under `.claude/worktrees/`, switches into it, and you can come back out later with keep/remove. Only reach for this if you genuinely need two things happening at once; for a single scoped interview task it's usually overkill.

## Cross-session memory: LIVING.md

This scaffold keeps one file, `LIVING.md`, as the persistent source of truth for the current task — the plan, any clarifying answers you gave, the decisions log, and current status. It's created/resumed by the `plan` skill and updated by `wrap-up`.

- Every new session reads it first (see `CLAUDE.md` step 0) — you never have to re-explain where things stand.
- If you're about to run low on context or want a clean break, ask Claude to run `wrap-up` early — it checkpoints `LIVING.md` before anything gets lost to compaction.
- To resume later: just start a new `claude` session (or `/clear`) in the same folder and say "continue" — it'll read `LIVING.md` on its own per the entry-point instructions.
- If you ever want to see exactly where things stand without asking the agent, just open `LIVING.md` yourself.

## Other useful commands

| Command | Does |
|---|---|
| `/agents` | Manage/inspect subagents |
| `/model` | Switch model |
| `/permissions` | Review/change tool permission settings |
| `/help` | List available commands |

## For this interview specifically

- Session order to follow: `plan → conventions → implement → verify → test → review → wrap-up` (see `CLAUDE.md`).
- Don't let the clock pressure skip `plan` or `review` — that's the whole point of this scaffold.
- If scope changes mid-task, re-run the `plan` skill rather than silently drifting — cheap to do, and it's visible proof to the interviewer that you're managing scope deliberately.
- `#` quick-notes are a good way to capture an interviewer's clarifying answer mid-task without breaking flow.
