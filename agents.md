# Agent Instructions for bug-free-eureka

This repository contains an Ansible playbook designed to automate the setup of extra packages on a fresh Bazzite (Fedora-based) installation.

## Repository Structure

- `playbook.yml`: The main entry point for the Ansible automation.
- `tasks/main.yml`: Contains the actual installation logic.
- `vars/packages.yml`: The source of truth for package lists.
- `molecule/`: Contains Molecule tests for Bazzite, Fedora CoreOS, and RHCOS.
- `inventory.ini`: Configured for `localhost` execution.
- `ansible.cfg`: Local Ansible configuration.
- `requirements.yml`: Lists required Ansible collections.

## Testing with Molecule

The repository includes Molecule tests to verify the playbook across different platforms.

```bash
molecule test
```

This will spin up Podman containers for:
- Bazzite
- Fedora CoreOS (via Fedora image)
- RHCOS (via UBI image)

## Package Management Policy

1.  **Flatpaks**: Prefer Flatpaks for GUI applications. Use the application ID (e.g., `com.google.Chrome`).
2.  **Homebrew**: Use for CLI tools and developers utilities not available as Flatpaks.
3.  **Pip**: Use for Python modules. Always install with the `--user` flag (handled by the playbook) to avoid interfering with the immutable system.

## Workflow for Future Agents

When asked to add new software:
1.  Identify the correct package manager (Flatpak, Brew, or Pip).
2.  Add the package name/ID to the corresponding list in `vars/packages.yml`.
3.  Ensure the `playbook.yml` remains generic and doesn't hardcode specific package names.
