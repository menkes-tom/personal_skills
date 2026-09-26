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
Approach: <the intended design; name anything existing you'll reuse>

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
