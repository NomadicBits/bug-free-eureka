# Bazzite Setup Playbook

This playbook helps you restore or install your favorite Brew and Flatpak packages on a fresh Bazzite install.

## Prerequisites

1.  **Ansible**: Ensure Ansible is installed.
    ```bash
    brew install ansible
    ```
2.  **Collection**: Install the required `community.general` collection.
    ```bash
    ansible-galaxy collection install -r requirements.yml
    ```

## Usage

Run the playbook using the following command:

```bash
ansible-playbook playbook.yml
```

## Customization

You can modify the list of packages in `vars/packages.yml`. This includes:
- `brew_packages`: Homebrew formulae and casks.
- `flatpak_packages`: Flatpak application IDs.
- `pip_packages`: Python modules to be installed via `pip --user`.

## Testing

This project uses [Molecule](https://molecule.readthedocs.io/) to test the playbook against Bazzite, Fedora CoreOS, and RHCOS containers.

To run tests:
```bash
molecule test
```
Ansible playground for loading up bazzite with software on fresh install
