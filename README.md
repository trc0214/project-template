# General GitHub Project Template

This repository is a technology-neutral starting point for new GitHub projects. It standardizes repository governance, AI-agent collaboration, project intake, GitHub-native architecture decisions, Issues, pull requests, handoffs, and secrets hygiene without assuming a particular language or framework.

## Create a project

Use GitHub's **Use this template** button or the GitHub CLI:

```bash
gh repo create my-project \
  --private \
  --template trc0214/project-template \
  --clone
```

Choose the visibility that is appropriate for the new project.

## Customize immediately

Every generated project should promptly:

1. Replace this README with project-specific purpose, setup, configuration, development, architecture, and deployment information as applicable.
2. Update `AGENTS.md` with real test, lint, type-check, build, deployment, ownership, protected-file, architecture, and scope rules.
3. Adjust `.gitignore` for the selected technology stack without hiding source artifacts unintentionally.
4. Replace `.env.example` placeholders with the project's safe configuration names—never real credentials.
5. Enable GitHub Discussions when the project will use formal architecture deliberation, and create an open-ended category named **Architecture** so `.github/DISCUSSION_TEMPLATE/architecture.yml` is active.
6. Define who may approve significant architecture changes.

GitHub Discussion category forms live under `.github/DISCUSSION_TEMPLATE/`; the form filename must match the category slug. This template assumes an `Architecture` category with slug `architecture`.

## Governance model

Use GitHub's native objects for their native responsibilities:

- **Discussion** — significant architecture deliberation, independent AI/human review, and the final decision summary.
- **Issue** — approved implementation work, scope, acceptance criteria, sequencing, risks, and verification expectations.
- **Pull Request** — actual implementation, code review, checks, and merge decision.
- **README / AGENTS / CONTRIBUTING** — stable repository instructions only.

Do not add a separate ADR, decision ledger, AI review report, or custom workflow document unless the project has a concrete need that GitHub's native objects do not cover.

## Development lifecycle baseline

1. **Project initialization** — establish project-specific README, agent rules, dependencies, checks, and canonical-source boundaries.
2. **Existing project intake** — reconstruct current state from repository evidence before editing ongoing work.
3. **Task start** — confirm branch, Issue, scope, ownership, acceptance criteria, and prohibited areas.
4. **Architecture Discussion when needed** — for Significant Change, compare alternatives and obtain required approval in GitHub Discussions.
5. **Implementation Issues** — split the approved direction into executable work.
6. **Development and checkpoints** — implement focused changes on task branches.
7. **Pull Request / review / checks** — verify the change and merge through GitHub's native PR workflow.
8. **Handoff / continuation** — preserve durable state in the relevant Issue or PR when work is incomplete.

For Significant Change, use:

`Architecture Discussion → Approved Decision in Discussion → Implementation Issue(s) → Pull Request → Review / Checks → Merge / Close`

## Included baseline

- `AGENTS.md`: AI-agent operating rules, project intake, ownership, handoff, and GitHub-native architecture governance.
- `CONTRIBUTING.md`: concise contributor workflow.
- `.github/DISCUSSION_TEMPLATE/architecture.yml`: structured Architecture Discussion form.
- `.github/ISSUE_TEMPLATE/architecture-implementation.yml`: native Issue Form for approved architecture implementation work.
- `.github/pull_request_template.md`: concise implementation and verification template.
- `.gitignore`: conservative cross-language exclusions.
- `.env.example`: safe configuration placeholders.

This template deliberately includes no dependency manifest, CI workflow, ADR system, or language-specific test command. Add project-specific infrastructure only after the generated project actually needs it.
