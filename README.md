# Ansible Assignment 4 --- System Manager Role

## Objective

Create a reusable Ansible role named **`system_manager`** that can
manage common system-level configuration on Linux virtual machines.

The assignment requires the role to provide these capabilities:

1.  **Software Management** --- manage software/packages that need to be
    installed.
2.  **User Management** --- manage users on the system.
3.  **Git Repository Management** --- manage Git repositories.
4.  **Directory Structure Management** --- ensure required folder
    structures exist on a VM.
5.  **Additional System-Specific Setting** --- manage another useful
    system setting.

The implementation is variable-driven so that the resources being
managed can be changed from the role defaults without rewriting the task
logic.

------------------------------------------------------------------------

## Environment

### Control Node

The Ansible control node is the local Linux/WSL environment.

### Managed Nodes

The role was executed against three managed Ubuntu nodes:

``` text
control_node_1
control_node_2
control_node_4
```

The inventory contains the connection details for these nodes.

------------------------------------------------------------------------

## Project Structure

The project uses a standard Ansible Galaxy role structure:

``` text
ansible-4/
├── ansible.cfg
├── hosts
├── site.yml
└── roles/
    └── system_manager/
        ├── README.md
        ├── defaults/
        │   └── main.yml
        ├── files/
        ├── handlers/
        │   └── main.yml
        ├── meta/
        │   └── main.yml
        ├── tasks/
        │   └── main.yml
        ├── templates/
        ├── tests/
        │   ├── inventory
        │   └── test.yml
        └── vars/
            └── main.yml
```

The role was initialized using:

``` bash
ansible-galaxy init roles/system_manager
```

------------------------------------------------------------------------

# 1. Ansible Configuration and Connectivity

The project contains a local `ansible.cfg` and `hosts` inventory file.

The managed nodes were tested using:

``` bash
ansible managed_nodes -m ping
```

All three managed nodes returned a successful `pong` response.

### Screenshot --- Connectivity Verification

<img width="940" height="469" alt="2026-08-25 20_39_37-_Ansible Assignment 4 - Notepad" src="https://github.com/user-attachments/assets/63e75223-4af3-4e25-9cb0-73a0c33164fe" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# 2. System Manager Role

The main role is:

``` text
roles/system_manager/
```

The two important implementation files are:

``` text
roles/system_manager/defaults/main.yml
roles/system_manager/tasks/main.yml
```

### `defaults/main.yml`

This file contains the resources that should be managed.

### `tasks/main.yml`

This file contains the Ansible tasks that enforce the required
configuration.

This separation makes the role reusable because the resource lists can
be changed without rewriting the task logic.

------------------------------------------------------------------------

# Task 1 --- Software Management

## Requirement

The System Manager role should be able to manage software that needs to
be installed.

The implementation manages:

``` text
git
curl
vim
unzip
```

## Variables

The package list is defined in:

``` text
roles/system_manager/defaults/main.yml
```

``` yaml
system_manager_packages:
  - git
  - curl
  - vim
  - unzip
```

## Task

The role uses:

``` text
ansible.builtin.apt
```

to ensure that the configured packages are installed.

Important parameters include:

-   `name` --- receives the package list.
-   `state: present` --- ensures packages are installed.
-   `update_cache: true` --- updates the APT package cache.
-   `cache_valid_time: 3600` --- keeps the cache valid for one hour.
-   `become: true` --- provides the required administrative privileges.

## Verification

The installed software was verified using:

``` bash
ansible managed_nodes -b -m shell -a 'git --version && curl --version | head -1 && vim --version | head -1 && unzip -v | head -1'
```

### Screenshot --- Software Management

<img width="946" height="440" alt="2026-08-25 20_40_00-_Ansible Assignment 4 - Notepad" src="https://github.com/user-attachments/assets/8e98cf0a-8e1b-4949-ad90-e3562c8e9ed1" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# Task 2 --- User Management

## Requirement

The System Manager role should be able to manage users on the system.

The current implementation manages:

``` text
ansibleuser
```

with:

``` text
Shell: /bin/bash
Home directory: created
```

## Variables

The user configuration is defined in:

``` text
roles/system_manager/defaults/main.yml
```

``` yaml
system_manager_users:
  - name: ansibleuser
    shell: /bin/bash
    create_home: true
```

The variable is a list, so additional users can be added without
changing the task logic.

## Task

The role uses:

``` text
ansible.builtin.user
```

with a loop over:

``` yaml
system_manager_users
```

Important parameters include:

-   `name` --- username.
-   `shell` --- login shell.
-   `create_home` --- controls creation of the home directory.
-   `state: present` --- ensures the user exists.
-   `loop` --- allows multiple users to be managed.

## Verification

The user was verified using:

``` bash
ansible managed_nodes -b -m shell -a 'id ansibleuser && getent passwd ansibleuser'
```

### Screenshot --- User Management

<img width="945" height="270" alt="2026-08-25 20_43_52-WhatsApp" src="https://github.com/user-attachments/assets/a2b6f379-790f-4d1d-8e7f-91684f5bc5d5" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# Task 3 --- Git Repository Management

## Requirement

The System Manager role should be able to manage various Git
repositories.

The current implementation manages:

``` text
Repository:
https://github.com/ansible/ansible-examples.git

Destination:
/opt/ansible-examples

Version:
master
```

## Variables

The Git configuration is defined in:

``` text
roles/system_manager/defaults/main.yml
```

``` yaml
system_manager_git_repositories:
  - repo: https://github.com/ansible/ansible-examples.git
    dest: /opt/ansible-examples
    version: master
```

The variable is a list, allowing additional repositories to be added
without changing the task logic.

## Task

The role uses:

``` text
ansible.builtin.git
```

Important parameters include:

-   `repo` --- source repository.
-   `dest` --- destination directory.
-   `version` --- required branch/version.
-   `update: true` --- allows the repository to be updated.
-   `loop` --- allows multiple repositories to be managed.

## Verification

The repository was verified using:

``` bash
ansible managed_nodes -b -m shell -a 'ls -ld /opt/ansible-examples && git -C /opt/ansible-examples status --short --branch'
```

### Screenshot --- Git Repository Management

<img width="956" height="287" alt="2026-08-25 20_45_13-" src="https://github.com/user-attachments/assets/f02ed95b-e711-4ec1-ae83-ec26c4df4253" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# Task 4 --- Directory Structure Management

## Requirement

Various folder structures should exist on a VM.

The role ensures that the following structure exists:

``` text
/opt/system_manager
├── bin
├── config
├── data
├── logs
└── tmp
```

## Variables

The directory list is defined in:

``` text
roles/system_manager/defaults/main.yml
```

``` yaml
system_manager_directories:
  - /opt/system_manager
  - /opt/system_manager/bin
  - /opt/system_manager/config
  - /opt/system_manager/data
  - /opt/system_manager/logs
  - /opt/system_manager/tmp
```

## Task

The role uses:

``` text
ansible.builtin.file
```

to create and maintain the directories.

The directories are configured with:

``` text
owner: root
group: root
mode: 0755
```

A loop allows the complete directory list to be managed by one task.

## Verification

The directory structure was verified using:

``` bash
ansible managed_nodes -b -m shell -a 'find /opt/system_manager -type d | sort'
```

### Screenshot --- Directory Structure Management

<img width="960" height="437" alt="2026-08-25 20_45_46-" src="https://github.com/user-attachments/assets/d750501b-de73-43d4-9148-97655dde13d1" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# Task 5 --- Additional System-Specific Setting

The assignment also asks for other system-specific settings that should
be managed.

For this implementation, the **Message of the Day (MOTD)** was selected.

## What is MOTD?

MOTD means **Message of the Day**. It is a message displayed when a user
logs into a Linux system.

The configured message is:

``` text
System managed by Ansible
```

## Variable

The setting is defined in:

``` text
roles/system_manager/defaults/main.yml
```

``` yaml
system_manager_motd: "System managed by Ansible"
```

## Task

The role uses:

``` text
ansible.builtin.copy
```

to manage:

``` text
/etc/motd
```

## Verification

The MOTD was verified using:

``` bash
ansible managed_nodes -b -m shell -a 'cat /etc/motd'
```

All managed nodes returned:

``` text
System managed by Ansible
```

### Screenshot --- MOTD Verification

<img width="952" height="228" alt="2026-08-25 20_46_05-WhatsApp" src="https://github.com/user-attachments/assets/613ebdee-4778-41d9-9ce2-f518dd284085" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# 6. Main Playbook

The main playbook is:

``` text
site.yml
```

Its purpose is to apply the `system_manager` role to the managed nodes.

``` yaml
---
- name: Configure systems using system_manager role
  hosts: managed_nodes
  become: true

  roles:
    - system_manager
```

The playbook is executed using:

``` bash
ansible-playbook site.yml
```

------------------------------------------------------------------------

# 7. Syntax Validation

The playbook syntax was checked using:

``` bash
ansible-playbook site.yml --syntax-check
```

Successful validation returns:

``` text
playbook: site.yml
```

### Screenshot --- Syntax Validation

<img width="649" height="46" alt="2026-08-25 20_47_25-WhatsApp" src="https://github.com/user-attachments/assets/befe5b41-b766-44c6-b936-9201e0084295" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# 8. Complete Role Execution

The complete role was executed against all three managed nodes using:

``` bash
ansible-playbook site.yml
```

The playbook successfully applied the configured software, users, Git
repository, directory structure, and MOTD settings.

### Screenshot --- Complete Playbook Execution

<img width="942" height="278" alt="2026-08-25 20_46_26-WhatsApp" src="https://github.com/user-attachments/assets/3a5f2cad-db24-4e57-9e7a-4999e13b8c3e" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# 9. Idempotency Verification

The playbook was executed a second time after the desired configuration
had already been applied:

``` bash
ansible-playbook site.yml
```

The second execution produced:

``` text
control_node_1 : changed=0
control_node_2 : changed=0
control_node_4 : changed=0
```

with:

``` text
failed=0
unreachable=0
```

This demonstrates Ansible's **idempotent behavior**: when the systems
are already in the desired state, the role does not make unnecessary
changes.

### Screenshot --- Idempotency Verification

<img width="956" height="79" alt="2026-08-25 20_46_49-" src="https://github.com/user-attachments/assets/a2d981ae-00d7-46f9-90e3-2e60b90aeaa1" />


`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

# 10. Verification Summary

  ------------------------------------------------------------------------
  Requirement             Implementation           Result
  ----------------------- ------------------------ -----------------------
  System Manager role     `roles/system_manager`   ✅ Completed

  Software management     `ansible.builtin.apt`    ✅ Completed

  User management         `ansible.builtin.user`   ✅ Completed

  Git repository          `ansible.builtin.git`    ✅ Completed
  management                                       

  Directory structure     `ansible.builtin.file`   ✅ Completed
  management                                       

  Additional system       MOTD using               ✅ Completed
  setting                 `ansible.builtin.copy`   

  Variable-driven         `defaults/main.yml`      ✅ Completed
  configuration                                    

  Multi-node execution    3 managed nodes          ✅ Completed

  Idempotent execution    Second run with          ✅ Completed
                          `changed=0`              
  ------------------------------------------------------------------------

------------------------------------------------------------------------

# 11. Ansible Modules Used

``` text
ansible.builtin.apt
        ↓
Software management

ansible.builtin.user
        ↓
User management

ansible.builtin.git
        ↓
Git repository management

ansible.builtin.file
        ↓
Directory structure management

ansible.builtin.copy
        ↓
MOTD/system-specific setting
```

------------------------------------------------------------------------

# 12. Conclusion

Assignment 4 implements a reusable **`system_manager` Ansible role** for
managing common Linux system configuration.

The role can manage:

``` text
Software
   ↓
Users
   ↓
Git Repositories
   ↓
Directory Structures
   ↓
System-Specific Settings
```

The implementation is variable-driven, reusable, multi-node capable, and
idempotent.
