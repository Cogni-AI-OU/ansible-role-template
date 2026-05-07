# GitHub Workflows and Actions

This directory contains GitHub Actions workflows, agent prompts, and related configuration.

## Workflows

### Check Workflow

The `check.yml` workflow runs on pull requests, pushes, and weekly schedule to
ensure code quality and correctness.

Jobs:

- **actionlint**: Validates GitHub Actions workflow files
- **link-checker**: Checks for broken links in Markdown files using Lychee
- **pre-commit**: Runs pre-commit hooks for code formatting and linting

### Test Workflow

The `test.yml` workflow runs tests on pull requests and pushes to ensure code
correctness.

### Molecule Workflow

The `molecule.yml` workflow runs Molecule tests for Ansible roles to verify
cross-platform compatibility.

### DevContainer CI Workflow

The `devcontainer-ci.yml` workflow builds and validates the dev container
environment and ensures all required tools and Python packages are present.

### Cogni AI Agent Workflow

The `cogni-ai-agent.yml` workflow provides event-driven automation for issues,
pull requests, discussions, and manual dispatches.

### OpenCode Workflow

The `opencode.yml` workflow allows for manual and event-driven invocation of
OpenCode agents via slash commands or manual triggers.

### OpenCode Review Workflow

The `opencode-review.yml` workflow provides automated PR reviews using OpenCode.

#### Link Checker

The link checker job uses [Lychee](https://github.com/lycheeverse/lychee) to
scan all Markdown files for broken links. It includes caching to avoid rate
limits and can be configured via `.lycheeignore` at the repository root to
exclude specific URLs or patterns.

**Local Testing**: You can test links locally with the configured
`markdown-link-check` pre-commit hook:

```bash
# Install from requirements.txt
pip install -r .devcontainer/requirements.txt

# Check a single file
pre-commit run markdown-link-check --files path/to/file.md

# Check all Markdown files
pre-commit run markdown-link-check -a
```

The hook uses `.markdown-link-check.json` and checks both local file references
and remote URLs before you push changes.

## Workflow Templates

The `workflow-templates/` directory contains reference workflows that are not
actively executed but are preserved for future use or copying to other
repositories. These templates can be customized and moved to the `workflows/`
directory when needed.

## Agent Prompts

The `prompts/` directory contains ready-to-use prompts for AI agents to perform
common repository management tasks. For agent-loading guidance and catalog, see
[prompts/AGENTS.md](prompts/AGENTS.md). For human-oriented details, see
[prompts/README.md](prompts/README.md).

## Problem Matchers

GitHub Actions problem matchers automatically annotate files with errors and
warnings in pull requests, making it easier to identify and fix issues.

### Available Matchers

- **actionlint-matcher.json**: Captures errors from actionlint workflow linting
- **pre-commit-matcher.json**: Captures errors from pre-commit hooks

### Pre-commit Problem Matcher

The pre-commit problem matcher supports two output formats:

1. **Generic format** (`file:line:col: message`): Used by flake8, actionlint,
   and other tools that provide column information
2. **No-column format** (`file:line message`): Used by markdownlint and other
   tools that only provide line numbers

Note: Some hooks like yamllint and ansible-lint already output GitHub Actions
annotations directly and don't need the problem matcher.

### Configuration

Problem matchers are registered in the `.github/workflows/check.yml` workflow
before running the corresponding tools.

## Security

### OpenCode Workflow Git Access

The OpenCode workflow (`opencode.yml`) grants intentionally broad git access
via `Bash(git:*)` to enable autonomous code changes. This permission is necessary
for OpenCode to commit and push changes, but requires proper safeguards.

#### Security Controls

**Access Control:**

- Only trusted users can trigger OpenCode (OWNER, MEMBER, COLLABORATOR, CONTRIBUTOR)
- PR/issue authors can only trigger on their own content
- External contributors (FIRST_TIME_CONTRIBUTOR, NONE) are explicitly blocked

**Required Repository Protections:**

To safely use OpenCode with git access, repository administrators must configure:

1. **Branch Protection Rules** on main/protected branches:
   - Require pull request reviews before merging
   - Require status checks to pass (e.g., linting, tests)
   - Require conversation resolution before merging
   - Do not allow bypassing the above settings

2. **GitHub Audit Logs** (organization-level):
   - Enable and regularly review audit logs
   - Monitor commits made by `github-actions[bot]` (OpenCode's identity)
   - Set up alerts for suspicious patterns (rapid commits, deleted branches, etc.)

3. **Protected Branch Policies**:
   - Restrict who can push to protected branches
   - Consider requiring deployment approvals for production branches
   - Use CODEOWNERS to require specific reviewer approval for sensitive files

#### Best Practices

- Review OpenCode's commits before merging PRs
- Use draft PRs for OpenCode's work to require explicit promotion
- Regularly audit OpenCode's tool usage and permissions
- Rotate `OPENCODE_API_KEY` periodically
- Monitor workflow run logs for unexpected behavior

### OpenCode Review (opencode-review.yml) — no git access

The OpenCode Review workflow (`opencode-review.yml`) does not grant git access
and relies solely on `gh` API commands and pre-commit hooks to perform its
duties. Because it does not write to the repository, it does not require the
strict git-specific controls outlined above.

### Cogni AI Agent (cogni-ai-agent.yml) — git access

The Cogni AI Agent workflow (`cogni-ai-agent.yml`) grants broad git access via
allowlisted `git` commands to enable autonomous operations. Like OpenCode, it
requires strict access controls and repository protections to ensure security.

#### Security Controls

The security controls for Cogni AI Agent are identical to those of OpenCode (see
above).
