# About

This repository contains the Ansible playbooks to reset a machine after a cohort ends.
The playbooks are divided into two parts. The first part is `setup1.yml` and the second part is `setup2.yml`.

## Directory structure

```sh
.
├── README.md
├── ansible.cfg
├── gnome-terminal-settings.dconf   # Terminal settings
├── inventory.ini                   # Contains the target machines
├── setup1.yml                      # Run this playbook first
├── setup2.yml                      # Run this playbook second
├── ssh-keys                        # Contains all the ssh keys
│   ├── id_gh_daa
│   └── id_gh_daa.pub
└── tasks                           # Contains all the tasks
    ├── account.yml
    ├── background.yml
    ├── chrome.js
    ├── chrome.yml
    ├── directories.yml
    ├── firefox.yml
    ├── install-zsh.yml
    ├── node.yml
    ├── os.yml
    ├── ssh.yml
    └── vscode.yml
```

## Install

1. Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

## Setup hosts

1. Populate the `inventory.ini` file with the target machines.

```ini
[auckland]
eda@192.168.1.xxx

[auckland:vars]
; populate the necessary variables here, such as ansible_user, ansible_ssh_pass, etc.
```

## SSH keys

This step is necessary to configure the ssh keys for github and `git iam` to work.

1. Generate new ssh keys by following the instructions from your wiki
2. Copy both files to the `ssh-keys` directory

## Run

1. Run `ansible-playbook -i inventory.ini setup1.yml` to run the first part of the playbook.
1. Reboot all machines.
1. Open chrome and open a new tab.
1. Click on the `+` icon to create a new bookmark and enter any dummy name in the `Name` and `URL` fields.
1. Close the browser.
1. Run `ansible-playbook -i inventory.ini setup2.yml` to run the second part of the playbook. This playbook will setup the pinned bookmarts to the homepage in chrome.

## Verify

1. Go to the cohort org and verify that all machines have successfully committed by checking the README.md file.
