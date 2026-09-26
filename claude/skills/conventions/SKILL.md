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
