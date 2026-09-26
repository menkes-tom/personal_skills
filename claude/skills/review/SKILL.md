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
