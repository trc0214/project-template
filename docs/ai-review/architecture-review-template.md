# Architecture Review Template

Use this format when reviewing a significant technical or architecture Discussion. Review the repository evidence independently before responding. Do not modify the implementation unless you are explicitly assigned implementation ownership.

## Reviewer / Model

`<agent / model>`

## Review Focus

`Architecture | Migration | Failure Modes | Testing | Security | Simplicity | Other`

## Position

`Support | Support with Changes | Oppose | Need More Evidence`

## Verified Repository Facts

List facts directly supported by repository code, configuration, tests, commits, issues, PRs, or documentation.

## Blocking Concerns

List concerns that must be resolved before approval or implementation. Use `None` when there are no blocking concerns.

For each concern include:

- Severity: Blocking
- Evidence
- Impact
- Recommended Action

## Major Concerns

List important but non-blocking risks, design weaknesses, compatibility problems, or missing evidence.

For each concern include:

- Severity: Major
- Evidence
- Impact
- Recommended Action

## Alternative

Describe a materially different alternative only when it is credible and relevant. Do not redesign unrelated parts of the system.

## Evidence Gaps / Open Questions

Identify missing benchmarks, tests, production evidence, migration information, or architectural facts needed to reach a stronger conclusion.

## Recommendation

Give the recommended next action and identify what must be resolved before the decision proceeds.

## Review Discipline

- Separate verified repository facts from inference and architectural preference.
- Do not treat another AI's summary as source evidence.
- Do not use model count or majority opinion as decision authority.
- Do not broaden the scope into unrelated refactoring.
- Do not implement during the deliberation phase unless explicitly assigned.
