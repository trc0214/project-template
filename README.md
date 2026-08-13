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

1. Replace this README with project-specific Purpose, Setup, Configuration, and—when applicable—Architecture, Development / Testing, and Deployment.
2. Update `AGENTS.md` with real project commands, protected areas, ownership, generated-code rules, and other project-specific constraints.
3. Adjust `.gitignore` and `.env.example` for the selected stack.
4. Add the ecosystem-standard dependency manifest and lockfile when applicable.
5. For a public or reusable repository, explicitly choose and add a `LICENSE`.
6. Add project-specific GitHub Actions only when the repository has real repeatable work such as test, lint, type check, build, code generation, or deployment. Do not add empty CI.
7. Use branch protection / rulesets when enforcement is needed.
8. If the project has meaningful release versions, use Git tags and GitHub Releases. Unless the ecosystem requires another scheme, use `vMAJOR.MINOR.PATCH` tags and Semantic Versioning; do not move or reuse published release tags. Add `CHANGELOG.md` only when a file-based changelog is actually useful.

## GitHub-native workflow

Use each GitHub object for one responsibility:

`Discussion → Issue → Pull Request → Review / Checks → Merge`

- **Discussion** — significant technical decisions and their final decision record.
- **Issue** — approved implementation work and acceptance criteria.
- **Pull Request** — implementation, review, verification, and merge.
- **README / AGENTS** — stable repository instructions.

Do not create parallel ADR, decision-ledger, AI-review-report, or custom lifecycle files unless the project has a concrete need that GitHub does not cover.

## Included baseline

- `AGENTS.md` — concise AI-agent operating rules.
- `.github/DISCUSSION_TEMPLATE/architecture.yml` — lightweight form for significant technical decisions.
- `.github/ISSUE_TEMPLATE/implementation.yml` — implementation tracking after a decision or for other non-trivial work.
- `.github/pull_request_template.md` — implementation and verification template.
- `.gitignore` — conservative cross-language exclusions.
- `.env.example` — safe configuration placeholders.

This template intentionally does **not** pre-create language-specific CI, dependency manifests, deployment environments, `CODEOWNERS`, `SECURITY.md`, release branches, package publishing, monitoring, migrations, feature flags, or monorepo governance. Add them only when the generated project actually needs them.
