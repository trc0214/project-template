# Contributing

Thank you for contributing. Keep changes focused, reviewable, and traceable in GitHub. AI agents must also follow `AGENTS.md`.

## Workflow

1. Start from an up-to-date `main` branch.
2. Create a task branch: `feature/<task>`, `fix/<task>`, `docs/<task>`, `refactor/<task>`, `test/<task>`, or `chore/<task>`. AI agents use `ai/<agent>/<task>`.
3. Make one coherent change and avoid unrelated cleanup.
4. Run the project's documented tests, lint, type checks, and build commands when available.
5. Open a single-purpose pull request using the repository template.

Do not develop features directly on `main`.

## Joining an existing project

Before changing an established codebase, review the repository instructions, active issues and PRs, recent relevant commits, architecture and decision records, current ownership, and existing verification status. Establish a baseline with the project's documented checks when reasonably possible and distinguish pre-existing failures from regressions introduced by your change.

Do not use project intake as an excuse for unrelated refactoring. If you discover a broader architecture problem outside the task scope, document it separately and follow the significant-change process in `AGENTS.md`.

## Significant technical or architecture changes

Changes that materially affect public contracts, schema or data integrity, authentication or security, framework/runtime choice, storage strategy, deployment topology, canonical-source boundaries, or core module/service architecture require a documented decision before implementation.

The decision record should describe the current state, problem, alternatives, recommendation, blast radius, migration strategy, rollback strategy, and verification plan. Record who owns the decision and whether approval has been granted. AI agents must not self-approve high-impact or irreversible architecture changes.

Prefer keeping significant architecture changes separate from ordinary feature or bug-fix PRs. If they cannot be separated, clearly identify the architecture portion and link the approved ADR, decision record, issue, or proposal.

## Commits

Use Conventional Commits with an appropriate type: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, or `build`. Write a concise message that explains the intent. Prefer meaningful checkpoints over many tiny commits.

## Issues and pull requests

Link relevant issues and explain the change, scope, verification, risks, and follow-up work. Use a closing keyword only when the completed PR should close the issue after merge; partial or unreviewed work must not close issues.

Reviewers should check behavior, scope, tests, security, maintainability, documentation, and whether any significant technical decision has the required decision record and approval. Authors should respond to feedback or explain design tradeoffs before merge.

## Secrets

Never commit credentials, tokens, private keys, production configuration, or real `.env` files. Use safe placeholders in `.env.example`. If a secret reaches Git history, rotate it immediately and assess whether history must be cleaned.
