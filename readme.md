# Ansible Assignment 5 — Redis Role

## Objective

Create an Ansible role to install and configure **Redis** with the following requirements:

- Install a specific Redis version.
- Support multiple operating systems.
- Variableize Redis configuration.
- Use Jinja2 templates for configuration and service files.
- Use separate Ansible handlers.
- Allow execution on Ubuntu, RHEL/CentOS, or both operating systems together.

## Assignment Requirements

| Requirement | Implementation |
|---|---|
| Version-specific Redis installation | `redis_version` variable |
| OS independent | Debian/Ubuntu and RedHat/RHEL task conditions |
| Variableized configuration | Variables in `defaults/main.yml` |
| Jinja2 templates | `redis.conf.j2` and `redis.service.j2` |
| Dynamic configuration values | Jinja2 variables |
| Separate handlers | `handlers/main.yml` |
| Ubuntu execution | `-l ubuntu` |
| RHEL/CentOS execution | `-l rhel` |
| Both operating systems | `hosts: all` |

## Project Structure

```text
ansible-5/
├── ansible.cfg
├── hosts
├── roles/
│   └── redis/
│       ├── defaults/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       ├── meta/
│       │   └── main.yml
│       ├── tasks/
│       │   └── main.yml
│       └── templates/
│           ├── redis.conf.j2
│           └── redis.service.j2
└── site.yml
```
<img width="951" height="214" alt="2026-09-07 07_55_26-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/e551fb98-07e1-464c-aafd-0ac19693a42c" />

## Role Components

### Version-Specific Installation

The Redis version is defined as a variable:

```yaml
redis_version: "8.10.0"
```

The download URL uses:

```text
https://download.redis.io/releases/redis-{{ redis_version }}.tar.gz
```

This allows the version to be changed centrally.

### OS Independence

The role uses Ansible OS facts to install the required build dependencies.

For Debian/Ubuntu:

```yaml
when: ansible_os_family == "Debian"
```

For RHEL/RedHat:

```yaml
when: ansible_os_family == "RedHat"
```

### Variableized Configuration

Configuration variables are maintained in:

```text
roles/redis/defaults/main.yml
```

Examples include:

```yaml
redis_version: "8.10.0"
redis_port: 6379
redis_bind: "127.0.0.1"
redis_user: "redis"
redis_group: "redis"
redis_config_dir: "/etc/redis"
redis_data_dir: "/var/lib/redis"
redis_log_dir: "/var/log/redis"
redis_maxmemory: "256mb"
redis_maxmemory_policy: "noeviction"
redis_appendonly: "yes"
redis_protected_mode: "yes"
```

### Jinja2 Templates

`redis.conf.j2` uses variables such as:

```jinja2
bind {{ redis_bind }}
port {{ redis_port }}
maxmemory {{ redis_maxmemory }}
maxmemory-policy {{ redis_maxmemory_policy }}
appendonly {{ redis_appendonly }}
protected-mode {{ redis_protected_mode }}
```

The systemd service is also generated from:

```text
roles/redis/templates/redis.service.j2
```

### Handlers

Handlers are kept separately in:

```text
roles/redis/handlers/main.yml
```

The role includes handlers to:

- Reload systemd.
- Restart Redis when configuration or service files change.

# Execution

## 1. Ubuntu

```bash
ansible-playbook site.yml -l ubuntu
```

### Screenshot — Ubuntu Playbook Execution

<img width="949" height="434" alt="2026-09-07 07_58_03-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/cf848ed7-c921-4183-a785-a5b8f6276c51" />

<br><br><br><br>

## 2. RHEL/CentOS

```bash
ansible-playbook site.yml -l rhel
```

### Screenshot — RHEL Playbook Execution

<img width="949" height="452" alt="2026-09-07 07_58_54-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/7ab81bc6-d0a1-4194-a745-f556517d7a74" />


<br><br><br><br>

## 3. Both Ubuntu and RHEL

```bash
ansible-playbook site.yml
```

### Screenshot — Both Operating Systems

<img width="947" height="488" alt="2026-09-07 07_59_55-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/da267cf4-7366-41ea-af22-e3c965382d2d" />


<br><br><br><br>

# Verification

## 1. Ansible Connectivity

```bash
ansible all -m ping
```

### Screenshot — Ansible Connectivity
<img width="940" height="198" alt="2026-09-07 07_56_57-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/14d161f1-d794-49be-9f1b-8d368995ac2d" />


<br><br><br><br>

## 2. Ubuntu Redis Version

```bash
ansible ubuntu -m command -a "redis-server --version"
```

Expected version:

```text
Redis server v=8.10.0
```

### Screenshot — Ubuntu Redis Version

<img width="946" height="68" alt="2026-09-07 08_00_26-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/fb957b9b-a267-4dfd-a1d3-7793366aad33" />


<br><br><br><br>

## 3. RHEL Redis Version

```bash
ansible rhel -m command -a "redis-server --version"
```

Expected version:

```text
Redis server v=8.10.0
```

### Screenshot — RHEL Redis Version

<img width="949" height="69" alt="2026-09-07 08_00_48-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/666ca156-50a5-4349-824d-6ef0b4810aa9" />


<br><br><br><br>

## 4. Ubuntu Redis Functionality

```bash
ansible ubuntu -m command -a "redis-cli ping"
```

Expected result:

```text
PONG
```

### Screenshot — Ubuntu Redis PONG

<img width="944" height="57" alt="2026-09-07 08_01_13-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/d5470c31-ef9e-4cc1-91f9-b52820e93963" />


<br><br><br><br>

## 5. RHEL Redis Functionality

```bash
ansible rhel -m command -a "redis-cli ping"
```

Expected result:

```text
PONG
```

### Screenshot — RHEL Redis PONG

<img width="941" height="54" alt="2026-09-07 08_01_38-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/c8e39f79-4bd4-4173-a632-ea252d996908" />


<br><br><br><br>

## 6. Redis Service Active

```bash
ansible all -m command -a "systemctl is-active redis"
```

### Screenshot — Redis Service Active

<img width="948" height="100" alt="2026-09-07 08_02_02-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/6fbf1026-6e2d-4eaf-a7e4-caa3b507a4d4" />


<br><br><br><br>

## 7. Redis Service Enabled

```bash
ansible all -m command -a "systemctl is-enabled redis"
```

### Screenshot — Redis Service Enabled

<img width="949" height="99" alt="2026-09-07 08_02_25-_Ansible Assignment-5 - Notepad" src="https://github.com/user-attachments/assets/2981b0e9-960f-47df-b083-cfacef238f72" />


<br><br><br><br>

## 8. Idempotency

The playbook was executed again against both nodes. The final recap showed:

```text
changed=0
failed=0
```

This demonstrates that the role does not make unnecessary changes when the desired state is already present.

### Screenshot — Idempotency / Final Play Recap

<img width="479" height="40" alt="2026-09-07 08_21_40-2026-09-07 07_59_55-_Ansible Assignment-5 - Notepad png" src="https://github.com/user-attachments/assets/a1b181e3-da04-408f-a9f6-03c8b3ebac11" />


<br><br><br><br>

# Final Result

The Redis Ansible role successfully:

- Installs Redis **8.10.0**.
- Supports Ubuntu/Debian and RHEL/RedHat systems.
- Uses variables for Redis version and configuration.
- Uses Jinja2 templates for Redis configuration and the systemd service.
- Uses separate handlers for systemd reload and Redis restart.
- Can be executed on Ubuntu only.
- Can be executed on RHEL/CentOS only.
- Can be executed on both operating systems together.
- Starts and enables the Redis service.
- Successfully responds to `redis-cli ping` with `PONG`.
- Demonstrates idempotent behavior with `changed=0`.

## Conclusion

The Ansible Redis role fulfills the requirements of **Ansible Assignment 5** and provides a reusable, variable-driven, OS-independent method for installing and configuring Redis.
