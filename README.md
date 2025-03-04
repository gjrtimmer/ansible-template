# Ansible Template

This project provides a devcontainer template for Ansible, ready to be used for yhour next Ansible project.

## Requirements

- docker
- Editor with Dev Container support (e.g. VS Code)

When you are using VS Code the following extension is required to enable Dev Container Support: [ms-vscode-remote.remote-containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Quick Start

- Clone repository
- Open in VS Code
- Start Dev Container
- Enjoy !

## Cross-Platform

This is a cross-platform development container project, which means it is designed to work out-of-the-box on the following platforms.

| Platform       | Tested             |
| -------------- | ------------------ |
| Darwin (MacOS) | :white_check_mark: |
| Linux          | :white_check_mark: |
| Windows        | :white_check_mark: |

## Restart/Rebuild Container

The devcontainer can be restarted by opening the Command Pallete of VS Code with CMD + SHIFT + P (MacOS) or CTRL + SHIFT + P (Windows/Linux) and then choose the option `Dev Containers: Rebuild Container`.

## Working Directory

The working directory in the devcontainer is `/work`.

## Home Directory

The home directory `~` in the devcontainer is `/home/vscode`.

## SSH

To protect existing SSH keys against overwriting, the user's .ssh directory is mounted as READONLY, which the exception of the SSH Config in `.ssh/config` and known hosts configuration in `.ssh/known_hosts`. Furthermore, a new directory `.ssh/ansible` is created which is mounted READWRITE to allow the user of this project to store new SSH keys in regards to this project. All the mounts regarding SSH are mounted in the devcontainer in the home directory of the `vscode` user `~` at `/home/vscode/.ssh` which ensures that all ssh commands and ansible commands works as expected.

If the user desires to change this the following files require updates:

- .devcontainer/devcontainer.json
- .devcontainer/scripts/initialize
- .devcontainer/scripts/initialize.cmd

## Ansible Vault

During container startup an Ansible Vault Password file is written to the user host at `${HOME}/.ansible_vault_pass` this file is empty.
This file is then mounted in the devcontainer at `~/.ansible_vault_pass`
Use the following command to set the Ansible Vault Password.

```shell
echo 'password' > ~/.ansible_vault_pass
```

If you want to secure a value within this project after you have set the password, it is as simple as selecting the value, then opening the VS Code Command Pallet with `Command + Shift + P` (MacOS) or `Ctrl + Shift + P` (Linux/Windows) and selecting `Ansible Vault: Encrypt/Decrypt via 'ansible-vault'`. You can use this option
to either decrypt or encrypt.

## Ansible Galaxy

Ansible Galaxy collections and/or roles can be added into the `requirements.yml` configuration. After updating restarting the container through VSCode is enough to trigger the installation of the requested collections/roles. The collections/roles are installed into the project folder at `.ansible`. The provided Ansible configuration (`ansible.cfg`) is configured to make use of these directories. The installation commands are provided by the `.devcontainer/scripts/postStartCommand.sh` script.

If manual installation is required the following commands can be used.

### Collections

```shell
ansible-galaxy collection install --force --collections-path .ansible/collections -r requirements.yml
```

### Roles

```shell
ansible-galaxy role install --force --roles-path .ansible/roles -r requirements.yml
```

## Ansible Reference Information

If you require something more complex please see the following [Ansible Documentation](https://docs.ansible.com/ansible/latest/tips_tricks/sample_setup.html) about sample project setups and modify this repository after cloning to your own requirements.
