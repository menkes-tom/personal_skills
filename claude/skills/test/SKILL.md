name: test description: Write a small, prioritized set of tests for what you just built or fixed. Use after implementing, before calling anything done. argument-hint: "[what changed, if not obvious from context]" user_invocable: true

You are adding tests for the current change — the minimum set that earns its keep under a time limit, not maximum coverage.

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
