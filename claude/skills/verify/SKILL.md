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
