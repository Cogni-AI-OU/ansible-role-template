# Copilot Instructions for Ansible Role

You are expected to be an expert in:

- Ansible
- Python
- Jinja2
- Molecule
- Linux (Alpine, Debian/Ubuntu, Nix)
- YAML

## Project Overview

This project is a template for creating Ansible roles.

## Coding Standards

### Python

- Follow **PEP 8** style guidelines.
- Use **Python 3.11+**.
- Use `uv` script for dependency management when creating standalone Python scripts.

### Ansible Guidelines

- Ensure idempotency in all tasks
- Ensure indentation is correct, especially for YAML files
- Follow standard role structure: tasks/, handlers/, templates/, defaults/, meta/
- Use ansible-lint and write Molecule tests for verification
- Use descriptive task names and include helpful comments

## Formatting Guidelines

### General Approach

- Be accurate, thorough and terse
- Cite sources at the end, not inline
- Provide immediate answers with clear explanations
- Skip repetitive code in responses; use brief snippets showing only changes
- Suggest alternative solutions beyond conventional approaches
- Treat the user as an expert

### Ansible Linting

Ensure enforcing the following rules:

- fqcn[keyword]: Avoid `collections` keyword by using FQCN for all plugins, modules, roles and playbooks

### Markdown

- Keep line length <=120 characters (see `.markdownlint.yaml`).
- Surround headings and lists with blank lines; fence code blocks with blank lines.
- Avoid trailing spaces; ensure a single trailing newline.
- Avoid hard tabs (MD010/no-hard-tabs).
- Headings must have blank lines around them (MD022/blanks-around-headings).
- Lists must be surrounded by blank lines (MD032/blanks-around-lists).
- Fenced code blocks need surrounding blank lines (MD031/blanks-around-fences).
- Files end with a single newline (MD047/single-trailing-newline).
- If pre-commit surfaces formatting errors, update these guidelines to keep them current and prevent repeats.

### YAML Guidelines

- empty-lines (yamllint): Limit consecutive blank lines to one.
- indentation (yamllint): Avoid wrong indentation.
- line-length (yamllint): No long lines (max. 120 characters).
- new-line-at-end-of-file (yamllint): Enforce new line character at the end of file.
- truthy (yamllint): Truthy value should be one of [false, true].
- Ensure items are in lexicographical order when possible.
- When embedding code blocks or inline YAML snippets within lists, end with a trailing newline to preserve indentation.

Formatting rules are defined in `.yamllint` (YAML) and `.markdownlint.yaml` (Markdown).

## Project Specifics

Notes:

- Project utilizes Codespaces with config at `.devcontainer/devcontainer.json` and requirements at `.devcontainer/requirements.txt`.
- GitHub Actions are used to validate the code by running pre-commit checks (`.pre-commit-config.yaml`) and Molecule (`molecule/`).

### Key Variables

Variables are defined in `defaults/main.yml` and `vars/main.yml` files.

Notes:

- On variable changes, update `main.yml` and `README.md` files accordingly.

### Testing Approach

- Use Molecule with Docker driver
