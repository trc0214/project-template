# General GitHub Project Template

A technology-neutral starting point for new repositories. It keeps the baseline limited to GitHub-native workflow, essential repository files, and concise AI-agent instructions.

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

Template files encode repository content, not every GitHub repository setting. After creating a repository, configure the native settings that the project actually relies on.

1. Replace this README with project-specific Purpose, Setup, Configuration, and—when applicable—Architecture, Development / Testing, and Deployment.
2. Update `AGENTS.md` with real project commands, protected areas, ownership, generated-code rules, and other project-specific constraints.
3. Adjust `.gitignore` and `.env.example` for the selected stack.
4. Add the ecosystem-standard dependency manifest and lockfile when applicable.
5. Explicitly choose the generated repository's license when it is public or intended for reuse. This generic template does not pre-create a root `LICENSE`, because template files are copied into generated repositories and a template-wide license would silently become part of every new project's starting state.
6. If the project uses formal architecture decisions, enable GitHub Discussions and create an open-ended category named **Architecture** with slug `architecture`, matching `.github/DISCUSSION_TEMPLATE/architecture.yml`.
7. Enable automatic deletion of merged head branches when the repository follows the short-lived task-branch policy.
8. Use branch protection / rulesets when enforcement is needed; for a protected `main`, require pull requests and add required status checks when real CI checks exist.
9. Add project-specific GitHub Actions only when the repository has real repeatable work such as test, lint, type check, build, code generation, or deployment. Do not add empty CI.
10. If the project has meaningful release versions, use Git tags and GitHub Releases. Unless the ecosystem requires another scheme, use `vMAJOR.MINOR.PATCH` tags and Semantic Versioning; do not move or reuse published release tags. Add `CHANGELOG.md` only when a file-based changelog is actually useful.

## GitHub-native workflow

Ordinary implementation work can begin with an Issue. Significant technical changes begin with an Architecture Discussion before implementation:

`Architecture Discussion → Approved decision → Issue → Pull Request → Review / Checks → Merge`

- **Discussion** — significant technical decisions and their final decision record.
- **Issue** — approved or otherwise well-defined implementation work and acceptance criteria.
- **Pull Request** — implementation, review, verification, and merge.
- **README / AGENTS** — stable repository instructions.

Do not create parallel ADR, decision-ledger, AI-review-report, provenance-log, or custom lifecycle files unless the project has a concrete need that GitHub does not cover.

## Research placement

Repository-coupled technical research belongs with the repository:

- unresolved technical investigation or option comparison → GitHub Discussion
- durable codebase-specific knowledge that should evolve with implementation → necessary `docs/`
- reproducible evidence → `tests/`, `benchmarks/`, `scripts/`, or other executable artifacts when practical

Research that remains useful independently of this codebase—such as domain, business, user, course, competition, requirements, or reusable cross-project research—stays in the external project context (Google Drive in this workspace) and is linked from GitHub only when needed. Do not create `docs/research/` by default.

## Included baseline

- `AGENTS.md` — concise AI-agent operating rules, including multi-AI attribution and handoff.
- `.github/DISCUSSION_TEMPLATE/architecture.yml` — structured form for significant technical decisions.
- `.github/ISSUE_TEMPLATE/implementation.yml` — implementation tracking after a decision or for other non-trivial work.
- `.github/pull_request_template.md` — implementation and verification template.
- `.gitignore` — conservative cross-language exclusions.
- `.env.example` — safe configuration placeholders.

This template intentionally does **not** pre-create a root `LICENSE`, language-specific CI, dependency manifests, deployment environments, `CODEOWNERS`, `SECURITY.md`, release branches, package publishing, monitoring, migrations, feature flags, monorepo governance, or a generic research-doc hierarchy. Add them only when the generated project actually needs them.
