# GitHub Actions Workflows (Agent Catalog)

Authoritative, agent-facing catalog of workflows in this repository. Use this when loading or modifying
workflows and keep it in sync with the files in this directory.

For a human-readable overview, see [README.md](README.md).

## Workflow catalog

| Workflow | Purpose | Key triggers / notes |
| -------- | ------- | -------------------- |
| [check.yml](check.yml) | Linting and quality gates via actionlint and pre-commit | push, pull_request, schedule; reusable via `workflow_call` |
| [claude-review.yml](claude-review.yml) | Automated PR review with Claude | pull_request (non-bot), `workflow_call` with `pr_number` |
| [claude.yml](claude.yml) | Interactive Claude mentions on issues/PRs | issue_comment, pull_request_review_comment, workflow_dispatch, `workflow_call` |
| [cogni-ai-agent.yml](cogni-ai-agent.yml) | Cogni AI agent automation | discussions, issues, PRs, comments, workflow_dispatch |
| [devcontainer-ci.yml](devcontainer-ci.yml) | Build/test devcontainer and required tools/packages | push/pull_request touching .devcontainer or workflow; schedule; `workflow_call` |
| [opencode-review.yml](opencode-review.yml) | OpenCode PR review | pull_request_target (trusted authors), `/review` comment by OWNER/MEMBER/COLLABORATOR, workflow_dispatch, `workflow_call` |
| [opencode.yml](opencode.yml) | OpenCode agent invocation via comments or manual triggers | issue_comment, pull_request_review_comment with `/oc` or `/opencode`, workflow_dispatch, `workflow_call` |

## Details

### check.yml

- Purpose: run actionlint and pre-commit to enforce workflow and repo standards.
- Reusable: `uses: Cogni-AI-OU/.github/.github/workflows/check.yml@main`.
- Jobs: `actionlint`, `pre-commit`.

### opencode.yml

- Purpose: invoke OpenCode agents via slash commands or manual triggers.
- Inputs: `agent` (default `cogni-ai`), `model` (default `opencode/gemini-3.1-pro`), `prompt` (optional override).
- Triggers: `workflow_dispatch`, `workflow_call`, or issue comments and PR review comments with `/oc` or
  `/opencode` from trusted collaborators.
- Concurrency: one run per branch/PR context via workflow-level `concurrency` group to avoid competing pushes.
- Reusable: `uses: Cogni-AI-OU/.github/.github/workflows/opencode.yml@main`.

### opencode-review.yml

- Purpose: OpenCode-driven PR review.
- Inputs: `agent` (default `cogni-ai`), `model` (default `opencode/gpt-5.3-codex`), `pr_number`,
  `prompt` (default `pr-review`), `additional_prompt`.
- Triggers: `pull_request_target`, `/review` comments from trusted collaborators, `workflow_dispatch`,
  `workflow_call`.
- Reusable: `uses: Cogni-AI-OU/.github/.github/workflows/opencode-review.yml@main`.

### claude-review.yml

- Purpose: AI code review that comments on PRs.
- Inputs: `pr_number` (required for `workflow_call`), `model` (default `claude-opus-4-5`),
  `additional_prompt` (optional extra review instructions).
- Trigger: pull_request (skips bot authors) and `workflow_call`.
- Reusable: `uses: Cogni-AI-OU/.github/.github/workflows/claude-review.yml@main`.

### claude.yml

- Purpose: respond to `@claude` mentions for interactive assistance.
- Input: `model` (default `claude-opus-4-5`).
- Triggers: issue_comment, pull_request_review_comment, workflow_dispatch, `workflow_call`.
- Reusable: `uses: Cogni-AI-OU/.github/.github/workflows/claude.yml@main`.
- Access: restricted to OWNER, MEMBER, COLLABORATOR, CONTRIBUTOR associations.

### cogni-ai-agent.yml

- Purpose: run the Cogni AI hosted agent on issues, pull requests, discussions, and manual dispatches.
- Inputs: `agent` (default `cogni-ai-architect`), `model` (default `opencode/gemini-3-flash`),
  `prompt` (optional override for workflow dispatch).
- Triggers: discussion, discussion_comment, issue_comment, issues, pull_request,
  pull_request_review_comment, workflow_dispatch.
- Jobs: `cogni-ai-agent`, `summary`.

### devcontainer-ci.yml

- Purpose: build and validate the dev container; ensure required tools and Python packages exist.
- Inputs: `required_commands` (defaults to common CLI tools), `required_python_packages`
  (defaults to ansible, ansible-lint, docker, molecule, pre-commit, uv).
- Triggers: pull_request/push affecting `.devcontainer/` or this workflow; weekly schedule;
  `workflow_call`.
- Permissions: callers must grant `packages: write` when pushing images to GHCR.
- Reusable: `uses: Cogni-AI-OU/.github/.github/workflows/devcontainer-ci.yml@main`.

## Model selection

### OpenCode workflows

- `opencode/claude-haiku-4-5`: fastest, best for quick tasks.
- `opencode/gemini-3.1-pro`: default for `opencode.yml`.
- `opencode/gpt-5.3-codex`: default for `opencode-review.yml`.
- Provide `model` input when calling `opencode.yml` or `opencode-review.yml`; defaults to
  workflow-level defaults when not explicitly provided.

### Claude workflows

- `claude-haiku-4-5`: fastest, best for quick tasks.
- `claude-opus-4-5`: default balance.
- `claude-sonnet-4-5`: most capable.
- Provide `model` input when calling `claude.yml` or `claude-review.yml`; defaults to `claude-opus-4-5`.

### Cogni AI workflow

- `opencode/gemini-3-flash`: default for `cogni-ai-agent.yml`.
- The workflow also exposes higher-capability OpenCode and xAI model choices for manual dispatches.

## Notes

- Keep workflow keys and environment variables alphabetized when practical.
- Validate workflow changes with `pre-commit run -a` so `yamllint`, `yamlfix`, and `actionlint` run together.
- Keep this catalog updated when workflows are added, removed, or renamed.
