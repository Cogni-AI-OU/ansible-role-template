# GitHub Actions Workflows

Reusable and repository workflows that automate checks, reviews, and AI-powered tasks.

- For the agent-facing workflow catalog, see [AGENTS.md](AGENTS.md).
- For editing guidelines, keep keys and environment variables alphabetized when practical.
- Validate workflow changes with `pre-commit run -a`.

## Using these workflows

- Reference a workflow from another repo with `uses: Cogni-AI-OU/.github/.github/workflows/<file>@main`.
- Consult the catalog in [AGENTS.md](AGENTS.md) for inputs, triggers, and job details, including the Cogni AI workflow.
- Keep branch protection and required checks enabled when consuming workflows that can push commits.
