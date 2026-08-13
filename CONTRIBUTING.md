# Contributing

Keep changes focused, reviewable, and traceable in GitHub. AI agents must also follow `AGENTS.md`.

## Workflow

1. Start from an up-to-date `main` branch.
2. Create a task branch: `feature/<task>`, `fix/<task>`, `docs/<task>`, `refactor/<task>`, `test/<task>`, or `chore/<task>`. AI agents use `ai/<agent>/<task>`.
3. Work from a GitHub Issue when the task is non-trivial or part of an approved architecture change.
4. Make one coherent change and avoid unrelated cleanup.
5. Run the project's documented tests, lint, type checks, and build commands when available.
6. Open a single-purpose pull request using the repository template.

Do not develop features directly on `main`.

## Joining ongoing work

Before changing an established codebase, review repository instructions, relevant Discussions, active Issues and PRs, recent commits, current ownership, and existing verification status. Establish a baseline when reasonably possible and distinguish pre-existing failures from regressions introduced by your change.

Do not use intake as an excuse for unrelated refactoring.

## Significant architecture changes

Use the GitHub-native workflow defined in `AGENTS.md`:

`Architecture Discussion → Approved Decision in Discussion → Implementation Issue(s) → Pull Request`

Use the open-ended **Architecture** Discussion category for problem framing, alternatives, AI/human review, and the final decision. Reviewers should inspect repository evidence independently and reply in the Discussion rather than creating separate review reports.

After approval, create implementation Issues with scope and acceptance criteria. Pull requests should link the relevant Issue and Architecture Discussion when applicable.

Do not create a separate ADR or decision document unless this project explicitly requires one.

## Commits

Use Conventional Commits with an appropriate type: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, or `build`. Prefer meaningful checkpoints over many tiny commits.

## Issues and pull requests

Keep executable work in Issues. Use closing keywords only when a completed PR should actually close the Issue after merge.

Use GitHub's native reviewers, review comments, Checks, Files changed view, labels, Projects, milestones, and linked Issues where useful rather than duplicating those functions in custom documents.

## Secrets

Never commit credentials, tokens, private keys, production configuration, or real `.env` files. Use safe placeholders in `.env.example`. If a secret reaches Git history, rotate it immediately and assess whether history must be cleaned.
