# Contributing

Thank you for contributing. Keep changes focused, reviewable, and traceable in GitHub. AI agents must also follow `AGENTS.md`.

## Workflow

1. Start from an up-to-date `main` branch.
2. Create a task branch: `feature/<task>`, `fix/<task>`, `docs/<task>`, `refactor/<task>`, `test/<task>`, or `chore/<task>`. AI agents use `ai/<agent>/<task>`.
3. Make one coherent change and avoid unrelated cleanup.
4. Run the project's documented tests, lint, type checks, and build commands when available.
5. Open a single-purpose pull request using the repository template.

Do not develop features directly on `main`.

## Commits

Use Conventional Commits with an appropriate type: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, or `build`. Write a concise message that explains the intent. Prefer meaningful checkpoints over many tiny commits.

## Issues and pull requests

Link relevant issues and explain the change, scope, verification, risks, and follow-up work. Use a closing keyword only when the completed PR should close the issue after merge; partial or unreviewed work must not close issues.

Reviewers should check behavior, scope, tests, security, maintainability, and documentation. Authors should respond to feedback or explain design tradeoffs before merge.

## Secrets

Never commit credentials, tokens, private keys, production configuration, or real `.env` files. Use safe placeholders in `.env.example`. If a secret reaches Git history, rotate it immediately and assess whether history must be cleaned.
