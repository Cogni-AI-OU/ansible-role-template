# Copilot Instructions for ... Ops

## Project Overview

TBC

## Coding Standards

### Python

- Use **Python 3.11+**.
- Use `uv` script headers for dependency management:

  ```python
  #!/usr/bin/env -S uv run --script
  # /// script
  # requires-python = ">=3.11"
  # dependencies = [
  #     "xero-python",
  #     "PyYAML",
  # ]
  # ///
  ```

- Follow **PEP 8** style guidelines.
- Use `argparse` for CLI argument parsing.
- Handle `BrokenPipeError` for CLI tools that might be piped to `head` or `grep`.

### TBC API

- Use the TBC SDK.
- Handle API rate limits and errors gracefully.

## Formatting Guidelines

### Markdown

Follow the Markdown rules in `.github/instructions/markdown.instructions.md`, which mirror the repository markdownlint configuration.

To test locally, run via `pre-commit run markdownlint -a` or use the VS Code Markdownlint extension.

### YAML

Follow the YAML rules in `./.github/instructions/yaml.instructions.md`, which mirror the repository `.yamllint` configuration.

Notes:

- Project utilizes Codespaces with config at `.devcontainer/devcontainer.json` and requirements at `.devcontainer/requirements.txt`.
- GitHub Actions run pre-commit checks (`.pre-commit-config.yaml`).
- To verify locally, run `pre-commit run yamllint -a` from the repo root.

## Project Structure

TBC

## Troubleshooting

If Copilot or automated checks behave unexpectedly:

- Re-run `pre-commit run -a` locally to surface formatting or linting issues.
- Verify `.markdownlint.yaml` and `.yamllint` have not been modified incorrectly.
- If problems persist, open an issue with details of the command run and any error output.

## Copilot Agent

- If you encounter firewall issues when using the GitHub Copilot Agent,
  refer to <https://gh.io/copilot/firewall-config> for configuration details.
  If you need to allowlist additional hosts, update your firewall configuration accordingly
  and keep the list of allowed hosts in `.github/agents/FIREWALL.md` up to date.

## Common Tasks

TBC
