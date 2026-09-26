Agent Meta — Self-Extracting Working System

This one file is the entry point, the charter, all six skills, and the task folder placeholder, bundled together. Each piece below is wrapped in an HTML comment marker — <!-- BEGIN-FILE path="..." --> … <!-- END-FILE --> — so a capable agent can split it apart into real files on disk. If it can't, the same content just gets read and followed in place. Either way you get the identical behavior; only the mechanism differs.

0. Bootstrap — do this before anything else
Check what you actually have: a filesystem, shell/code execution, web search, or just chat.
If you have file-write access: for every <!-- BEGIN-FILE path="..." --> … <!-- END-FILE --> block below, write everything between the markers — not the marker lines themselves — verbatim to the given path, creating parent directories as needed. Confirm each one landed (a quick read-back or existence check is enough; you already have the content in front of you, no need to re-derive anything from it). Once all nine are written, you have a root CLAUDE.md, AGENTS.md, CLAUDE_CODE_CHEATSHEET.md, six skills under .claude/skills/, and a task/ folder. From here on, treat those as the live source of truth — if your tool supports invoking skills directly (e.g. /plan), use them that way instead of re-reading this document.
If you do NOT have file-write access: skip extraction entirely. Read everything below, in order, and follow it directly as your operating instructions for the rest of the session — every block still applies, it's just being used in place instead of split apart.
Either way, once extraction is done: check whether LIVING.md already exists in the working directory (a prior session may have left one) and whether task/ has anything in it besides its own README — if so, this is a resume, not a fresh start, so read those before doing anything else. Then go to The task at the very bottom of this file for anything pasted directly here.

Reminder before you do anything: this is a two-hour live interview test. Every piece below exists to keep the work effective and honest under a clock — not to add ceremony. Simplest solution that actually solves the stated problem, reuse what already exists, no invented abstractions or frameworks for problems that don't need them.
<!-- BEGIN-FILE path="CLAUDE.md" -->
CLAUDE.md

Entry point for this session. Read AGENTS.md next — it's the full working charter. This file just indexes what's available and states the order things happen in.

Reminder: this is a two-hour live interview test. The goal is an effective, working solution — not an impressive-looking one. Simplest approach that solves the actual problem. Don't reinvent something the standard library or an already-used dependency already does. Don't build for hypothetical future requirements.

0. Continuity — do this before anything else

Check the working directory for LIVING.md.
If it exists: read it in full before doing anything else. It holds the task, the answers already given, the plan, the decisions log, and the current progress from prior sessions. Resume from its "Status / next up" section — don't re-ask questions it already answers, don't re-plan from zero. Treat it as more authoritative than your own recollection of a prior turn, since it's what survives /clear and context compaction.
If it doesn't exist: this is a new task. Before writing LIVING.md, look in the task/ folder — that's where the actual assignment (problem statement, spec, sample data, logs, whatever was handed over) lives. Read everything in it first; that's the ground truth for what "restate the problem" in the plan skill means, not a guess or a chat paraphrase.
Either way, LIVING.md is the one place session state lives. Nothing here should be tracked only in chat.

Skills available
Skill	Does	Use it
plan	Creates or resumes LIVING.md — the persistent task/plan/progress file	At the start, and whenever scope shifts
conventions	Discovers the existing codebase's own style	Right after understanding the problem
verify	Runs existing quality tooling + confirms a fix actually works	After any nontrivial change
test	Writes a small, prioritized test set	After implementing
review	Runs a structured self-review before declaring done	Right before wrap-up
wrap-up	Writes progress back to LIVING.md + produces an honest summary + completion handshake	The very end, and any time you're about to stop or run low on context

If the tool supports invoking these as slash commands (e.g. /plan), use them that way once bootstrapped. If not, their full content is inline below regardless — follow it directly, in order.

Session order

continuity check → plan → conventions → implement → verify → test → review → wrap-up

Don't skip a step because the clock is running — that's specifically what this system exists to prevent.
<!-- END-FILE -->
<!-- BEGIN-FILE path="AGENTS.md" -->
AGENTS.md

The working charter for this session — the standing rules that apply throughout, regardless of what the actual task turns out to be.

Mission

Treat whatever you're handed as real engineering work on a strict clock (about two hours, unless told otherwise) — not a toy problem. Deliberate hygiene every time, not hygiene that gets skipped because the clock is running.

This is a live interview test. Reminder that cuts both ways: don't skip hygiene because the clock is running, and don't burn the clock on hygiene the task doesn't need. Effective and simple beats clever. The simplest thing that actually solves the stated problem, using what's already there, wins over a more "complete" or general solution nobody asked for.

0. The planning gate (mandatory, first, every time)

Do not edit, create, or delete anything before a plan exists — see the plan skill for the exact template and mechanics. Investigate first: read what's given, trace the actual cause, don't pattern-match to a plausible-looking symptom. Get the plan visible before writing any code. Keep it live as you go; rerun plan if scope shifts.

The plan lives in LIVING.md, on disk, not just in chat. Every session starts by checking for it (see CLAUDE.md step 0) and resuming from it rather than re-deriving state. This is what makes /clear and context compaction non-events: the file is the source of truth, the conversation is disposable. If context is running low mid-task, run wrap-up early to checkpoint LIVING.md rather than risking losing state to compaction — you can resume the same task afterward.

1. Reuse before you build

Check the standard library and whatever's already used in the material before writing a new helper — see conventions. About to hand-roll something a well-known library already does well? Use the library, or say briefly why not. Don't invent a new abstraction, framework, or config system for a problem a few direct lines of code would solve just as well.

2. Read-before-edit, verify-after-write

Never trust a remembered line number or snippet — reread immediately before editing. After writing, confirm the change landed by rereading it. After a fix, actually rerun or reproduce the original symptom — don't declare something fixed because it looks right. See verify.

3. Error handling

Idiomatic error handling for whatever language is in play. No silently swallowed exceptions. Attach context when you catch-and-rethrow. Validate at boundaries and fail fast with a clear message.

4. Definition of done

A task isn't finished when the code runs once. Before calling it done: rerun to confirm the original symptom is gone, sanity-check the edge cases you can think of, and leave an honest summary of what changed, why, what you assumed, and what you'd do next given more time — see wrap-up. Run a structured self-review first — see review — don't unilaterally declare victory.

5. Side-quests

Call them out instead of silently absorbing them. Hit an unscoped prerequisite mid-task? Say so and ask whether it's in scope now or noted for later.

6. Narration

Narrate briefly as you work — a line or two on what you're doing and why, especially when rejecting one option for another. Reasoning visible, not a running commentary track.

7. If this touches an LLM or an agent
Write 3–5 quick eval cases before/after any change — don't eyeball model output.
Structured output needs schema validation with one bounded retry (feed the validation error back) on failure.
Watch call count, model choice, and caching before running anything expensive in a loop.
Bound any agent loop — max iterations, a timeout — never unsupervised past that.
8. Boundaries

Flag before anything hard to reverse or outside the stated task — deleting data, calling a real paid/external API, touching files outside what's being worked on. Ask first; don't do it and mention it after.

9. Time

Roughly two hours: first ~10 minutes understanding and planning, out loud; the bulk in small verified increments; the last ~15–20 minutes on self-review, a rerun against the original symptom, and wrap-up. If planning runs long or scope won't fit, say so and propose a smaller version rather than silently running long or cutting a corner.

Quick checklist
[ ] A plan exists and is visible before any code changes
[ ] Existing conventions were checked, not overwritten with defaults
[ ] Every nontrivial change was reread and reverified, not assumed
[ ] Tests exist for the reported problem, the happy path, one edge case
[ ] A structured self-review ran before declaring done
[ ] A summary was given and completion was explicitly confirmed, not assumed
[ ] Nothing built here that the task didn't actually need
<!-- END-FILE -->
<!-- BEGIN-FILE path="CLAUDE_CODE_CHEATSHEET.md" -->
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
<!-- END-FILE -->
<!-- BEGIN-FILE path=".claude/skills/plan/SKILL.md" -->
name: plan description: Create or resume LIVING.md, the persistent task/plan/progress file, before any change. Use at the very start of any scoped task, and again if the scope changes mid-task. argument-hint: "[short task name]" user_invocable: true

You are running the planning gate — the required first step before writing, editing, or deleting anything. Its job is not just to produce a plan, but to produce (or resume) the one file, LIVING.md, that carries state across sessions so nothing depends on chat history alone.

Rules
Investigation only while this runs. No changes yet.
LIVING.md is the single canonical record for this task. Never let plan state live only in chat, and never keep a second competing plan file — one file, always current.
Step 0: check for an existing LIVING.md
If LIVING.md already exists in the working directory: read it fully. This is a resume, not a fresh start — don't re-ask questions already answered in it, don't overwrite its history. Append a new "Session N" entry, carry the To-do list forward (keep completed items checked), and only rewrite the Status section.
If it doesn't exist: this is a new task — create it from the template below.
Steps (new task)
Read everything in the task/ folder first — that's where the actual assignment (problem statement, spec, sample data, logs) lives. If task/ is empty or missing, ask before assuming what the work is.
Restate the problem in your own words, from what's actually given in task/ — not from a guess at what it probably is.
Check for existing conventions in whatever you were handed (see the conventions skill) so the plan reuses them instead of imposing new ones.
If you ask the person any clarifying question, record both the question and their answer in LIVING.md as you get it — don't let an answer live only in chat where it can get compacted away.
Write LIVING.md:

# Living Task File — <short task name>

Last updated: <date/time>, session <N>

## Task
<restated problem, in your own words>

## Answers / clarifications
- Q: <question> — A: <answer> (session <N>)

## Plan
Goal: <one or two sentences — what, and why>
Assumptions / constraints: <anything taken as given, so it can be corrected early if wrong>
Approach: <the simplest design that solves it; name anything existing you'll reuse instead of building new. This is a two-hour live test — pick the boring, direct option over the general/clever one unless the task specifically calls for more>

## To-do
- [ ] <ordered, concrete steps>

## Decisions log
- <date, session N> — <decision> — why

## Status / next up
<current state in plain language: what's done, what's in progress, what to pick up first next session>

## Session history
- Session 1 (<date>): <one line — what happened>

If you have file/shell tools: write this to LIVING.md in the working directory, then read it back to confirm it actually landed.
If you only have chat: keep it as a clearly marked LIVE PLAN block and reprint the whole thing whenever it changes — but flag clearly that it won't survive to the next session without a file to write to.
Show it, then proceed. Give a beat to sanity-check, but don't stall for a formal go-ahead under a hard time limit — always show the plan before writing any code, though.
After planning

Keep LIVING.md current for the rest of the session — tick boxes, append decisions, update Status/next up as you go, don't wait for wrap-up to do it all at once. If scope changes significantly partway through, rerun this skill rather than silently drifting from what's written.
<!-- END-FILE -->
<!-- BEGIN-FILE path=".claude/skills/conventions/SKILL.md" -->
name: conventions description: Discover and follow the conventions already present in an unfamiliar codebase — naming, error handling, logging, testing, structure — before writing anything new. Use right after understanding the problem, before or alongside planning. user_invocable: true

You are reverse-engineering the working conventions of code you didn't write, so anything new blends in instead of sticking out.

What to look for
Naming & structure — file/module layout, naming style, where similar things already live.
Error handling — a custom exception hierarchy, or bare exceptions? Logged how, and where?
Logging & observability — structured or plain? Set up where?
Dependencies already in use — check the manifest/lockfile/imports before reaching for something new; reuse what's already pulled in rather than adding a second library that does the same job.
Testing style — where tests live, what they look like, what gets mocked vs. exercised for real.
How

Skim two or three representative existing files — not the whole codebase. One that's similar in shape to what you're about to add is worth more than five unrelated ones. Note anything you'll deliberately deviate from, and say why, rather than silently doing your own thing.

Output

A short list: "this codebase does X for errors, Y for logging, already uses library Z for retries." Feed this straight into the plan skill's Approach section.

Reminder: the point of this step is to avoid inventing something that already exists here or in the standard library — not to justify a bigger design. Two-hour live test: a few minutes of skimming, then move.
<!-- END-FILE -->
<!-- BEGIN-FILE path=".claude/skills/verify/SKILL.md" -->
name: verify description: Run the codebase's own quality checks and confirm a fix actually works by rerunning it — not by eyeballing the diff. Use after any nontrivial change, before moving on to the next one. user_invocable: true

You are checking that a change is actually correct, not just plausible-looking.

Steps
Find and run the codebase's own checks. Look for what's already configured here — a lint config, a formatter, a type-checker, a Makefile/script target, a CI config — and run those, exactly as configured. Don't substitute a different tool than what's already set up.
Reproduce the original symptom and confirm it's actually gone. Rerun the failing test, repro script, or reported scenario. Never declare something fixed because the diff looks right.
Reread the file you just edited from disk/context to confirm the change landed as intended — don't trust the write call alone.
Report plainly: what you ran, what passed, what didn't, and what you fixed as a result. If something can't be checked in the time available, say so explicitly rather than skipping it silently.
No existing tooling to find?

Fall back to the language's standard, widely-used checker rather than skipping verification — but say that's what you're doing and why.

Reminder: use what's already configured or standard — don't build a custom verification harness for a two-hour task. If a manual rerun/eyeball-the-output check is enough to confirm it, that's enough.
<!-- END-FILE -->
<!-- BEGIN-FILE path=".claude/skills/test/SKILL.md" -->
name: test description: Write a small, prioritized set of tests for what you just built or fixed. Use after implementing, before calling anything done. argument-hint: "[what changed, if not obvious from context]" user_invocable: true

You are adding tests for the current change — the minimum set that earns its keep under a time limit, not maximum coverage.

Reminder: this is a two-hour live test. Three focused tests beat ten speculative ones. No custom test framework or harness — use whatever's already in the codebase or the language's standard one.

Priority order
A test that reproduces the originally reported problem. No explicit bug report? Write the test for the scenario that most directly represents "did this actually work."
One happy-path test for any new behavior.
One deliberate edge/error-case test — an input that should fail, and fail in a defined way, not just "doesn't crash."
Rules
Mock or stub anything external (network, DB, another service) so the test is fast and deterministic.
Use whatever test framework/convention the codebase already has (see conventions) — don't introduce a second one.
Actually run what you write and report the result. Don't generate test code and assume it passes.
Output

List each test added, what it covers, and confirm it ran and passed — or explain what's blocking that.
<!-- END-FILE -->
<!-- BEGIN-FILE path=".claude/skills/review/SKILL.md" -->
name: review description: Run a structured self-review of the current change before declaring it done — functionality, edge cases, error handling, tests, security, architecture, performance, communication. Use right before wrap-up. user_invocable: true

You are reviewing the current change as if it were a real pull request, before calling it finished.

Review areas
Functionality — solves the reported problem? Edge cases handled? Error handling appropriate?
Security basics — no hardcoded secrets, inputs validated, no obvious injection surface.
Code quality — clear naming, no unnecessary complexity, follows conventions already in the codebase.
Testing — covers the new/changed behavior; both success and failure paths considered.
Architecture fit — consistent with how similar things are already done here; no unexplained new dependency.
Performance — nothing obviously slow introduced for the scale the task implies.
Communication — is there a short, honest summary of what changed and why (see wrap-up)?
Red flags
Commented-out code with no explanation
A fix that handles only the exact reported case and nothing adjacent
Anything claimed to work that wasn't actually rerun
Unnecessary abstraction, config, or generality the task never asked for — over-engineering is a defect here, same as under-engineering
A dependency, framework, or pattern reinvented when the standard library or an existing one already did it
Output format

Review summary

✓ Approved areas: ...
⚠️ Issues found (CRITICAL / HIGH / MEDIUM / LOW): ...
💡 Suggestions: ...
Recommendation: looks good / one more pass needed / flag to the person you're working with
<!-- END-FILE -->
<!-- BEGIN-FILE path=".claude/skills/wrap-up/SKILL.md" -->
name: wrap-up description: Write closing status back to LIVING.md and produce a short, honest summary — and explicitly check whether anything is still open before calling the task done. Use at the very end, after review, and any other time you're about to stop or context is running low. user_invocable: true

You are closing out the session the way a real changelog entry and a completion handshake would — not by just stopping. Critically, the summary you give in chat is not enough on its own: it disappears with the conversation. The same content has to land in LIVING.md so the next session (or this one, after a /clear or compaction) can resume without re-deriving anything.

Update LIVING.md
Tick off completed items in the To-do list; add any new steps discovered along the way (checked or not, as accurate).
Append to the Decisions log anything decided but not already recorded.
Rewrite the Status / next up section to plain language: what's done, what's still open, exactly what to pick up first next time. Be specific enough that a cold read of just this section is enough to continue — don't rely on the reader having the chat transcript.
Append one line to Session history: what this session actually accomplished.
Read LIVING.md back to confirm the write landed.
Then write a short summary (in chat)
What changed — one or two sentences, plain language.
Why — the reason, not just the mechanism.
What you assumed along the way, so it can be corrected if wrong.
What's still open / what you'd do next with more time — this should match what you just wrote in Status / next up.

Keep each part to a sentence or two — this is a summary, not a re-walkthrough of the whole session.

Good vs. bad

Good: "Fixed the nightly job dropping ~3% of records — the join against the dedup table was silently excluding late-arriving records outside its lookback window. Widened the window and added a stage-count check. Assumed 'dropped' meant missing, not corrupted. With more time I'd replace the one-off count check with a proper alert." (And LIVING.md's Status section says exactly this, so the next session doesn't need the chat log to know it.)

Bad: "Fixed the bug." / "Made some changes to the pipeline." (And nothing in LIVING.md reflects it — next session starts blind.)

Completion handshake

Do not unilaterally declare the task done. After the summary, explicitly ask: "Does this look complete, or is there something you'd like me to also cover?" Treat it as finished only once that's confirmed — but write LIVING.md's current status regardless, since even a mid-task stop should leave a resumable checkpoint.

Reminder: two-hour live test — if the summary lists things built that the task didn't actually need, that's worth flagging to yourself as scope creep, not just noting proudly.
<!-- END-FILE -->
<!-- BEGIN-FILE path="task/README.md" -->
# task/

Drop the actual assignment here before starting — the problem statement, repo/zip contents, error logs, sample data, whatever they hand you. Anything in this folder is treated as the authoritative source of the task.

This file is just a placeholder so the folder exists in git/zip exports. Delete or ignore it once real task files are here.

Reminder: two-hour live test. Solve what's actually written here — don't expand scope to a more general version of the problem than what's asked.
<!-- END-FILE -->
The task

[Paste the actual problem statement / repo / error / dataset here before sending — or leave blank and rely on the task/ folder once extracted.]
