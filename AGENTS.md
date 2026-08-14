# AI Agent Repository Guidelines

## Scope and precedence

Apply instructions in this order:

1. User instructions for the current task.
2. This repository's `AGENTS.md` and more specific in-repo rules.
3. Governing workspace development rules, when available.
4. Tool defaults.

Keep project-specific commands, protected areas, ownership, architecture constraints, and deployment rules here. Do not copy general GitHub documentation into this file.

## Governance layers

Put a rule or template at the narrowest durable layer that owns it:

- **Account-wide `trc0214/.github` defaults**: generic Discussion category forms, Issue/PR templates, and supported community-health files that should apply across repositories unless locally overridden.
- **Repository scaffold**: files that must exist in each generated repository and evolve with it, including `README.md`, `AGENTS.md`, `.gitignore`, `.env.example`, `.editorconfig`, and `.gitattributes`.
- **Project-specific configuration**: dependency manifests/lockfiles, CI/CD, `LICENSE`, `CODEOWNERS`, dependency automation, security tooling, deployment, release configuration, and ecosystem-specific rules when applicable.

GitHub account-wide community defaults do not replace repository-specific instructions. A repository-local supported file overrides the account-wide default for that repository. Do not maintain two editable copies of the same universal template after account-wide inheritance has been verified.

The public `trc0214/.github` repository provides the shared Discussion/Issue/PR templates and contribution guidance. Inheritance was verified in a repository without local overrides. Add a repository-local supported file only when the project needs a justified override.

## Repository workflow

GitHub is the canonical source for source code, branches, commits, Discussions, Issues, pull requests, checks, Releases, repository-coupled technical research/documentation, and implementation state. Chat history must not be the only project record.

- Keep `main` stable and do not perform feature development directly on it.
- Use one short-lived branch per task. AI branches use `ai/<agent>/<task>`; general work may use `feature/`, `fix/`, `docs/`, `refactor/`, `test/`, or `chore/`.
- One implementation task should have one primary owner at a time. Other agents may review, research, test, document, or own clearly separated subtasks.
- Before editing, read `README.md`, relevant repository instructions, and the related Discussion / Issue / PR. Check the current branch, scope, existing changes, and available test or build commands.
- Keep changes focused. Do not perform unrelated refactors because a different architecture is preferred.

## GitHub-native responsibilities

Use GitHub's native objects instead of parallel tracking documents:

- **Ideas Discussion**: proposals to change or improve the project. Significant technical decisions are reviewed and finalized here before implementation.
- **Bug Issue**: reproducible incorrect behavior or regression with evidence and impact.
- **Implementation Issue**: approved or otherwise well-defined implementation scope, acceptance criteria, dependencies, and completion state.
- **Pull Request**: actual code changes, review, checks, and merge decision.

Use the repository's native `Ideas` category rather than creating a separate `Architecture` category solely for governance. Do not create ADR, decision-ledger, AI-review-report, or custom lifecycle documents unless this project has a concrete need that GitHub does not cover.

### Significant technical proposal minimum

For a significant technical change, the Ideas Discussion must give reviewers enough evidence to reconstruct both the current state and the proposed target. At minimum cover:

- decision status
- proposal type
- problem / context
- current architecture or current state
- decision drivers / constraints
- proposed direction
- credible alternatives
- material impact / risks
- evidence and unresolved questions
- required approver

When repository, package, module, service, component boundaries, or data flow materially change, also show the target file/module structure or target data flow. These details are optional for small feature ideas where they do not affect the decision. Do not substitute a preferred architecture pattern for repository evidence.

Significant changes include public API breaking changes, core architecture or runtime migrations, destructive schema migrations, authentication / authorization model changes, deployment-topology changes, and large cross-cutting refactors. Do not implement these without the required maintainer or user approval recorded in the Ideas Discussion.

## AI attribution and provenance

When multiple humans or AI tools operate through the same GitHub account, GitHub's author identity records the operator account, not necessarily the actual contributor. Record AI identity only where native GitHub authorship cannot distinguish a material contributor; do not create a separate provenance log.

- **Ideas Discussion initial draft**: fill `Drafted By` with the human or AI agent/model that produced the initial proposal.
- **Issue initial draft**: fill the account-wide Issue Form's `Drafted By` with the human or AI agent/model that produced the initial Issue content. Treat this as immutable provenance; do not overwrite it during handoff, revision, or implementation.
- **Non-Form Issue creation**: if Blank issue, GitHub CLI, API, or automation creates an Issue without the standard Issue Form, put `Drafted By: <human-or-agent/model>` at the top of the Issue body before creation. Never create an Issue without initial attribution.
- **Discussion revision or synthesis**: if another AI materially rewrites the proposal or synthesizes multiple reviews, leave a concise comment beginning with `AI-Contributor: <agent/model>` and `Role: Revision` or `Role: Synthesis`. State what materially changed. Do not overwrite the original `Drafted By` merely to replace provenance.
- **Discussion review**: an AI review comment must begin with `AI-Reviewer: <agent/model>`. Add `Review-Focus: <area>` only when the review has a specialized scope.
- **Issue planning**: when a different AI materially changes scope, acceptance criteria, reproduction, impact, dependencies, or other Issue-defining content through a shared GitHub account, leave one concise `AI-Contributor: <agent/model>` comment with `Role: Planning`, `Role: Revision`, or `Role: Synthesis`. Routine wording edits do not require attribution comments.
- **Pull Request review**: when an AI submits a PR review or review comment through a shared GitHub account, begin the review body with `AI-Reviewer: <agent/model>`.
- **Decision authority**: `Approved By` or equivalent approval text must identify the actual user or maintainer with decision authority. AI drafting, synthesis, review, or implementation never implies approval authority.
- **Implementation branch**: `ai/<agent>/<task>` identifies the agent that created or initially owned the branch. Do not rename a branch solely to rewrite provenance after a handoff.
- **AI handoff**: if the primary implementation agent changes while the same task continues, add one concise handoff update to the linked Issue or PR identifying `<from> → <to>` together with remaining work and verification state. Create a new branch only when the task boundary or implementation ownership genuinely splits.
- **Issue / PR body**: do not duplicate `Implemented By` or other AI identity fields when branch history and the linked handoff already make implementation ownership clear.

Do not infer the AI model from the GitHub username, commit author, writing style, or branch history when explicit attribution exists.

## Research and documentation placement

- Use GitHub Discussion for repository-specific technical investigation or option comparison while the technical direction is still unresolved; use the native Ideas category when the discussion is proposing a project change.
- Keep durable knowledge that is tightly coupled to this codebase in `docs/` only when future maintainers need it and it should evolve with the implementation.
- Prefer reproducible evidence in `tests/`, `benchmarks/`, `scripts/`, or other executable artifacts over a static research report when practical.
- Keep domain, business, user, course, competition, requirements, and other research that remains useful independently of this repository in the external project context; link the source instead of copying it into the repository.

Do not create a generic `docs/research/` directory merely because research occurred.

## Pull requests and checks

Merge task branches through focused pull requests. Before merge, confirm that applicable tests, lint, type checks, builds, and other required checks pass, and that the diff contains no secrets, debug artifacts, unexpected files, or out-of-scope changes.

A PR implementing a significant technical decision must link the approved Ideas Discussion. Do not hide an unapproved architecture or other major direction change inside an ordinary feature or bug-fix PR.

If GitHub Actions workflows exist, treat their required checks as the primary automated verification. Do not bypass failing checks without an explicit project-specific reason.

## Cross-project engineering baseline

Use established specifications and native controls instead of inventing local equivalents:

- Keep `.editorconfig` technology-neutral unless the selected language requires explicit indentation or formatting overrides.
- Keep `.gitattributes` responsible for repository text normalization and explicit binary handling; extend it only for real file types or custom diff/merge behavior.
- Prefer Conventional Commits for commit messages. Use `feat` for features, `fix` for fixes, and other descriptive types such as `docs`, `refactor`, `test`, `chore`, `ci`, and `build` where useful. Breaking changes must be explicit.
- Use Semantic Versioning only when the repository has a meaningful versioned public interface and no higher-priority ecosystem versioning rule.
- Use ecosystem-standard dependency manifests and lockfiles when applicable.
- Add dependency automation, CI tests, security policy, SAST, workflow token restrictions, release signing, or similar supply-chain controls when project exposure and lifecycle justify them. Do not create empty generic workflows or placeholder security machinery merely to satisfy a checklist.

## Releases

When this repository uses a release lifecycle and its ecosystem does not require another scheme, use Semantic Versioning tags in the form `vMAJOR.MINOR.PATCH`. Use prerelease tags such as `v1.0.0-alpha.1`, `v1.0.0-beta.1`, and `v1.0.0-rc.1`. Published release tags are immutable: do not move or reuse them; publish a new version for corrections.

## Commits and handoff

Prefer Conventional Commits and keep each commit understandable on its own.

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
