CLAUDE.md

Entry point for this session. Read AGENTS.md next — it's the full working charter. This file just indexes what's available and states the order things happen in.

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
