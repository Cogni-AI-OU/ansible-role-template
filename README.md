# Ansible Role: Template

[![PR Reviews][pr-reviews-image]][pr-reviews-link]
[![License][license-image]][license-link]

This is a template role.
Use it as starting point to create your own role.

## Getting Started

🗺️ **New to this repository?** Take the [**CodeTour**](.tours/getting-started.tour) to explore the project structure!

To view the tour:

1. Install the [CodeTour extension](https://marketplace.visualstudio.com/items?itemName=vsls-contrib.codetour) in VS Code
2. Open the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`)
3. Run "CodeTour: Start Tour"

Or simply open this repository in a devcontainer - the extension is pre-configured!

## Requirements

This role requires:

- Ansible
- Python
- Administrative/root access on target hosts
- One of the following operating systems:
  - Alpine Linux
  - Debian/Ubuntu
  - NixOS or systems with Nix package manager

## Install

To install this role, you can use the following terminal command:

```shell
ansible-galaxy install git+https://github.com/Cogni-AI-OU/ansible-role-template.git
```

## Role Variables

For available variables,
check [`defaults/main.yml`](defaults/main.yml).

## Testing

### Docker

Steps to test role on Docker containers.

1. Install the current role by running the following commands in shell:

    ```shell
    ansible-galaxy install -r requirements.yml
    jinja2 requirements-local.yml.j2 -D "pwd=$PWD" -o requirements-local.yml
    ansible-galaxy install -r requirements-local.yml
    ```

    Alternatively, for development purposes, you can consider using symbolic link, e.g.

    ```shell
    ln -vs "$PWD" ~/.ansible/roles/cogni-ai.template
    ```

2. Ensure Docker service (e.g. Docker Desktop) is running.
3. Run playbook from `tests/`:

    ```shell
    ansible-playbook -i tests/inventory/docker-containers.yml tests/playbooks/docker-containers.yml
    ```

4. Run the verify-tag playbook (stops containers after verification):

  ```shell
  ansible-playbook -i tests/inventory/docker-containers.yml tests/playbooks/tags/verify.yml --tags verify
  ```

### Molecule

To test using Molecule, run:

```shell
molecule test
```

<!-- Named links -->

[pr-reviews-image]: https://img.shields.io/github/issues-pr/Cogni-AI-OU/ansible-role-template?label=PR+Reviews&logo=github
[pr-reviews-link]: https://github.com/Cogni-AI-OU/ansible-role-template/pulls
[license-image]: https://img.shields.io/badge/License-MIT-blue.svg
[license-link]: LICENSE
