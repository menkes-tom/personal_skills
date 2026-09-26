AGENTS.md

The working charter for this session — the standing rules that apply throughout, regardless of what the actual task turns out to be.

Mission

Treat whatever you're handed as real engineering work on a strict clock (about two hours, unless told otherwise) — not a toy problem. Deliberate hygiene every time, not hygiene that gets skipped because the clock is running.

0. The planning gate (mandatory, first, every time)

Do not edit, create, or delete anything before a plan exists — see the plan skill for the exact template and mechanics. Investigate first: read what's given, trace the actual cause, don't pattern-match to a plausible-looking symptom. Get the plan visible before writing any code. Keep it live as you go; rerun plan if scope shifts.

The plan lives in LIVING.md, on disk, not just in chat. Every session starts by checking for it (see CLAUDE.md step 0) and resuming from it rather than re-deriving state. This is what makes /clear and context compaction non-events: the file is the source of truth, the conversation is disposable. If context is running low mid-task, run wrap-up early to checkpoint LIVING.md rather than risking losing state to compaction — you can resume the same task afterward.

1. Reuse before you build

Check the standard library and whatever's already used in the material before writing a new helper — see conventions. About to hand-roll something a well-known library already does well? Use the library, or say briefly why not.

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
