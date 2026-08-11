# General GitHub Project Template

This repository is a technology-neutral starting point for new GitHub projects. It standardizes repository governance, AI-agent collaboration, Git and pull-request workflows, commit conventions, handoffs, and secrets hygiene without assuming a particular language or framework.

## Create a project

After this repository is marked as a GitHub Template Repository, use GitHub's **Use this template** button or the GitHub CLI:

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

## Included baseline

- `AGENTS.md`: operational governance for AI agents.
- `CONTRIBUTING.md`: contributor workflow for humans.
- `.github/pull_request_template.md`: consistent PR context and quality checks.
- `.gitignore`: conservative cross-language exclusions.
- `.env.example`: a safe configuration placeholder.

This template deliberately includes no dependency manifest, CI workflow, or language-specific test command. Add those only after the generated project selects its ecosystem.
