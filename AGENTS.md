# AI Agent Repository Guidelines

## Scope and precedence

Apply instructions in this order:

1. User instructions for the current task.
2. This repository's `AGENTS.md` and more specific in-repo rules.
3. Governing workspace development rules, when available.
4. Tool defaults.

Keep project-specific commands, protected areas, ownership, architecture constraints, and deployment rules here. Do not copy general GitHub documentation into this file.

## Repository workflow

GitHub is the canonical source for source code, branches, commits, Discussions, Issues, pull requests, checks, Releases, and implementation state. Chat history must not be the only project record.

- Keep `main` stable and do not perform feature development directly on it.
- Use one short-lived branch per task. AI branches use `ai/<agent>/<task>`; general work may use `feature/`, `fix/`, `docs/`, `refactor/`, `test/`, or `chore/`.
- One implementation task should have one primary owner at a time. Other agents may review, research, test, document, or own clearly separated subtasks.
- Before editing, read `README.md`, relevant repository instructions, and the related Discussion / Issue / PR. Check the current branch, `git status`, scope, and available test or build commands.
- Keep changes focused. Do not perform unrelated refactors because a different architecture is preferred.

## GitHub-native responsibilities

Use GitHub's native objects instead of parallel tracking documents:

- **Discussion**: significant technical decisions before implementation; keep the final decision in the same Discussion.
- **Issue**: approved implementation scope, acceptance criteria, dependencies, and completion state.
- **Pull Request**: actual code changes, review, checks, and merge decision.

Do not create ADR, decision-ledger, AI-review-report, or custom lifecycle documents unless this project has a concrete need that GitHub does not cover.

Significant changes include public API breaking changes, core architecture or runtime migrations, destructive schema migrations, authentication / authorization model changes, deployment-topology changes, and large cross-cutting refactors. Do not implement these without the required maintainer or user approval.

## Pull requests and checks

Merge task branches through focused pull requests. Before merge, confirm that applicable tests, lint, type checks, builds, and other required checks pass, and that the diff contains no secrets, debug artifacts, unexpected files, or out-of-scope changes.

If GitHub Actions workflows exist, treat their required checks as the primary automated verification. Do not bypass failing checks without an explicit project-specific reason.

## Commits and handoff

Prefer Conventional Commits: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `build`.

Commits record repository history; Issues and PRs record lifecycle state. Do not invent custom commit-state metadata.

When work is incomplete, leave enough durable context in the linked Issue or PR for another agent to continue: goal, completed work, remaining work, verification, known risks, and next step. The receiving agent must verify repository state rather than rely only on the handoff summary.

## Dependencies, secrets, and generated content

Use the ecosystem-standard dependency manifest and lockfile when applicable. Do not invent package or build commands; use the project's documented commands.

Never commit API keys, passwords, access tokens, private keys, service-account credentials, production secrets, or a real `.env`. `.env.example` may contain safe placeholders only. If a secret enters Git history, treat it as compromised and rotate it.

Generated code or synced artifacts must have a clear canonical source. Do not manually maintain two editable copies of the same source artifact.

## Project-specific rules

Replace or extend this section only when the project has concrete requirements such as:

- test / lint / type-check / build commands
- protected files or directories
- required reviewers or ownership boundaries
- generated-code commands
- deployment or migration procedures
- project-specific architecture constraints
