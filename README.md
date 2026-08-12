# General GitHub Project Template

This repository is a technology-neutral starting point for new GitHub projects. It standardizes repository governance, AI-agent collaboration, Git and pull-request workflows, project intake, architecture deliberation, decision control, commit conventions, handoffs, and secrets hygiene without assuming a particular language or framework.

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
6. Define who can approve significant architecture changes and where project-specific ADRs or decision records live.

GitHub Discussion category forms are repository files under `.github/DISCUSSION_TEMPLATE/`; the form filename must match the category slug. This template therefore assumes an `Architecture` category with slug `architecture`.

## Development lifecycle baseline

The template expects this lifecycle for non-trivial work:

1. **Project initialization** — establish project-specific README, agent rules, dependencies, checks, and canonical-source boundaries.
2. **Existing project intake** — when joining ongoing work, reconstruct the current state from repository evidence before editing code.
3. **Task start** — confirm branch, scope, ownership, acceptance criteria, and prohibited areas.
4. **Development** — make focused changes and maintain meaningful checkpoints.
5. **Architecture Discussion** — for significant changes, compare alternatives and collect independent AI/human review before approval.
6. **Decision / ADR** — record the approved decision and rationale after deliberation.
7. **Issue planning** — break the approved decision into executable work.
8. **Verification and PR integration** — run applicable checks, disclose risks, and keep the PR single-purpose.
9. **Handoff / continuation** — preserve durable state when work is incomplete or another agent takes over.

## Significant architecture changes

For breaking contracts, destructive schema changes, security-model changes, framework/runtime migrations, storage or canonical-source changes, deployment-topology changes, core architecture replacement, or other high-impact changes, use this lifecycle:

`Significant Change Detected → Architecture Discussion → Multi-AI / Human Review → Discussion Synthesis → Required Approval → ADR / Decision Record → Implementation Issues → Implementation PR → Verification → Close Discussion`

The layers have distinct responsibilities:

- **Discussion**: deliberation, alternatives, review, open questions, and synthesis.
- **ADR / Decision Record**: the final approved or rejected decision and rationale.
- **Issue**: implementation tracking after a decision exists.
- **Pull Request**: implementation and verification.

Multi-AI review is advisory, not a vote. AI agents may propose, compare, validate, and implement approved options, but they must not silently self-approve high-impact or irreversible architecture changes.

## Included baseline

- `AGENTS.md`: operational governance for AI agents, including existing-project intake, Architecture Discussions, multi-AI review, and architecture-change control.
- `CONTRIBUTING.md`: contributor workflow for humans.
- `.github/DISCUSSION_TEMPLATE/architecture.yml`: structured Architecture Discussion form.
- `docs/ai-review/architecture-review-template.md`: standard response format for AI architecture reviewers.
- `.github/ISSUE_TEMPLATE/architecture-change.md`: post-decision implementation-tracking template.
- `.github/pull_request_template.md`: consistent PR context, intake, verification, and decision-link checks.
- `docs/adr/0000-template.md`: reusable ADR structure for the final decision record.
- `.gitignore`: conservative cross-language exclusions.
- `.env.example`: a safe configuration placeholder.

This template deliberately includes no dependency manifest, CI workflow, or language-specific test command. Add those only after the generated project selects its ecosystem.
