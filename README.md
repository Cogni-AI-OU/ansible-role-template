# Ansible Role: Template

[![CodeRabbit PR Reviews](https://img.shields.io/coderabbit/prs/github/Cogni-AI-OU/ansible-role-template?utm_source=oss&labelColor=171717&color=FF570A&link=https%3A%2F%2Fcoderabbit.ai&label=CodeRabbit+PR+Reviews)](https://github.com/Cogni-AI-OU/ansible-role-template/pulls)
[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](LICENSE)

This is a template role.
Use it as starting point to create your own role.

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

## License

GNU GPL v3

See: [LICENSE](./LICENSE)

<!-- Named links -->
