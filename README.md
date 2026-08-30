# General GitHub Project Template

A technology-neutral starting point for new repositories. It keeps the copied baseline limited to files that belong inside each repository, while GitHub account-wide defaults handle shared contribution and collaboration templates when available.

## Governance layers

Use the narrowest durable layer that owns the concern:

1. **Account-wide `trc0214/.github` defaults** — shared Discussion category forms, Issue/PR templates, and generic community-health guidance. Repository-local files override these defaults when a project needs different behavior.
2. **`trc0214/project-template` scaffold** — files that should actually be copied into each new repository, such as `README.md`, `AGENTS.md`, `.gitignore`, `.env.example`, `.editorconfig`, and `.gitattributes`.
3. **Project-specific configuration** — dependency manifests and lockfiles, CI/CD, `LICENSE`, `CODEOWNERS`, dependency automation, security tooling, deployment, release configuration, and other ecosystem-specific controls only when applicable.

The public `trc0214/.github` repository provides the shared Discussion, Issue, pull request, and contribution defaults. Their inheritance was verified in a repository without local overrides before the duplicate copies were removed from this template.

## Create a project

Use GitHub's **Use this template** button or:

```bash
gh repo create my-project \
  --private \
  --template trc0214/project-template \
  --clone
```

Choose the appropriate visibility for the project.

## Customize after creation

Template files encode repository content, not every GitHub repository setting. After creating a repository:

1. Replace this README with project-specific Purpose, Setup, Configuration, and—when applicable—Architecture, Development / Testing, and Deployment.
2. Update `AGENTS.md` with real project commands, protected areas, ownership, generated-code rules, and other project-specific constraints.
3. Adjust `.gitignore`, `.env.example`, `.editorconfig`, and `.gitattributes` only where the selected stack requires different behavior.
4. Add the ecosystem-standard dependency manifest and lockfile when applicable.
5. Explicitly choose the generated repository's license when it is public or intended for reuse. This generic template does not pre-create a root `LICENSE`.
6. Enable GitHub Discussions when the project uses proposal or decision discussions. Use GitHub's native **Ideas** category for project-change proposals.
7. Enable automatic deletion of merged head branches when the repository follows the short-lived task-branch policy.
8. Use branch protection / rulesets when enforcement is needed; for a protected `main`, require pull requests and add required status checks only when real CI checks exist. Disable force-push on `main`; consider disabling force-push on shared `task/*` branches when the repository relies on multi-agent handoff history.
9. Add project-specific GitHub Actions only when the repository has real repeatable work such as test, lint, type check, build, code generation, or deployment. Do not add empty CI.
10. If the project has meaningful release versions, use Git tags and GitHub Releases. Unless the ecosystem requires another scheme, use `vMAJOR.MINOR.PATCH` tags and Semantic Versioning; do not move or reuse published release tags.
11. When multi-AI tasks rely on per-commit provenance and diagnostic history, enable merge commits and use them by default for `task/*` pull requests unless the project explicitly chooses another strategy.

## GitHub-native workflow

Ordinary implementation work begins with an Issue. Reproducible defects use a Bug Report Issue Form. Proposals to change or improve the project belong in the native **Ideas** Discussion category. Significant technical changes require an approved Ideas Discussion before implementation:

`Ideas Discussion → Approved decision → Issue → task branch → Pull Request → Review / Checks → Merge`

All standard Issue Forms require `Drafted By` for the actual human or AI agent/model that produced the initial Issue content. Preserve that value as immutable provenance; later AI revisions use `AI-Contributor: <agent/model>` comments instead of overwriting the original attribution. If Blank issue, GitHub CLI, API, or automation creates an Issue without the standard Form, put `Drafted By: <human-or-agent/model>` at the top of the Issue body before creation.

- **Ideas Discussion** — feature, architecture, refactor, migration, security, performance, or other project-change proposals; significant decisions and their final decision record remain in the same Discussion.
- **Bug Issue** — reproducible incorrect behavior or regression with evidence and impact.
- **Implementation Issue** — approved or otherwise well-defined work, scope, acceptance criteria, dependencies, and verification.
- **Task branch** — the working line for one Issue/task; it represents the work, not the current agent.
- **Pull Request** — implementation, review, verification, aggregate provenance, and merge.
- **README / AGENTS** — stable repository-specific instructions.

Do not create parallel ADR, decision-ledger, AI-review-report, provenance-log, custom Architecture category, or custom lifecycle files unless the project has a concrete need that GitHub does not cover.

## Multi-agent implementation workflow

Keep normal multi-agent work linear and low-overhead:

1. Create one short-lived task branch. When an Issue exists, prefer `task/<issue-number>-<short-name>`.
2. Keep one active writer on that task branch at a time.
3. If work is expected to span sessions or agents, open a Draft PR early so diff, checks, comments, provenance, and handoff context stay in one durable place.
4. When one agent stops and another takes over, commit and push meaningful work when possible, leave a concise handoff, and continue on the **same task branch**.
5. Use commit SHAs as exact recovery points. If current HEAD is unverified or broken, record the last verified SHA in the handoff instead of creating a checkpoint branch or custom commit state.
6. Every material AI commit records `AI-Agent: <agent/model>` in the commit footer. The PR body records aggregate `Implemented By` provenance for all material contributors.
7. Treat published shared task history as durable. Do not force-push or rebase it by default; revert bad published commits when history preservation is safer.
8. Use a temporary `experiment/<agent>/<task>` branch only for deliberately isolated risky or alternative work. Successful pieces may be merged or cherry-picked; unsuccessful experiments can be discarded without making experiment branches part of every task.
9. Before final merge, run applicable checks and review the full diff. For multi-AI task branches, default to a merge commit so original commit SHAs, AI trailers, and `git bisect` granularity survive in `main`.
10. Merge the PR, close the linked Issue with the PR when appropriate, and delete the task branch.

If a task can be split into genuinely independent parallel work, prefer separate Issues/task branches rather than concurrent writers on one branch.

## Cross-project engineering conventions

- **EditorConfig** provides a minimal cross-editor baseline: UTF-8, LF, final newline, and trailing-whitespace handling. Language-specific indentation belongs in project-specific overrides.
- **Git attributes** normalize text handling and explicitly mark common binary formats; project-specific binary/diff/merge rules may extend the baseline.
- **Conventional Commits** are preferred for readable, machine-processable history. Keep commits as understandable logical changes so review, revert, blame, and `git bisect` remain useful.
- **AI commit provenance** uses the `AI-Agent: <agent/model>` trailer for material AI commits when multiple agents may share one Git identity or task branch.
- **Semantic Versioning** is used only when the project has a meaningful versioned public interface and no higher-priority ecosystem rule.
- **OpenSSF-aligned controls** such as branch protection, code review, dependency update tooling, CI tests, pinned dependencies, security policy, SAST, minimal workflow token permissions, and signed releases are added when the repository's exposure and lifecycle justify them. They are not represented by empty generic files.

## Research placement

Repository-coupled technical research belongs with the repository:

- unresolved technical investigation or option comparison → GitHub Discussion; use Ideas when it is a proposal to change the project
- durable codebase-specific knowledge that should evolve with implementation → necessary `docs/`
- reproducible evidence → `tests/`, `benchmarks/`, `scripts/`, or other executable artifacts when practical

Research that remains useful independently of this codebase—such as domain, business, user, course, competition, requirements, or reusable cross-project research—stays in the external project context and is linked from GitHub only when needed. Do not create `docs/research/` by default.

## Included baseline

- `AGENTS.md` — concise AI-agent operating rules, including multi-AI attribution and handoff.
- `.editorconfig` — cross-editor text consistency without language-specific indentation assumptions.
- `.gitattributes` — Git text normalization and common binary handling.
- `.gitignore` — conservative cross-language exclusions.
- `.env.example` — safe configuration placeholders.

Shared Discussion, Issue, and pull request templates are intentionally not copied into generated repositories. They are inherited from `trc0214/.github` unless a repository has a justified local override.

This template intentionally does **not** pre-create a root `LICENSE`, language-specific CI, dependency manifests, deployment environments, `CODEOWNERS`, `SECURITY.md`, release branches, package publishing, monitoring, migrations, feature flags, monorepo governance, a custom Architecture Discussion category, or a generic research-doc hierarchy. Add or inherit them only when the generated project actually needs them.
