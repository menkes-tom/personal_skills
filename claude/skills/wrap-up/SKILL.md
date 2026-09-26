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
