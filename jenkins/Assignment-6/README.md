# Jenkins Assignment 6 – Shared Library

## Objective

Create and use a Jenkins Shared Library for an Ansible deployment pipeline.

The pipeline performs the following operations:

1. Read configuration from a configuration file.
2. Clone the project code.
3. Request user approval before deployment.
4. Execute the Ansible playbook.
5. Send deployment notifications through Slack and Email.

---

## Project Structure

```text
ansible-5/
├── Jenkinsfile
├── assignment6.yml
├── config/
│   └── prod.conf
├── vars/
│   └── ansibleDeploy.groovy
├── roles/
│   └── redis/
├── hosts
├── ansible.cfg
└── site.yml
```

---

## Shared Library Configuration

The Jenkins Shared Library was configured with:

- **Library Name:** `ansible-shared-library`
- **Default Version:** `main`
- **SCM:** Git
- **Repository:** `https://github.com/syed-wessii/jenkins-ansible-shared-library.git`
- **Retrieval Method:** Modern SCM

### Screenshot 1 – Jenkins Global Shared Library Configuration

> **Insert screenshot here**

---

## Configuration File

The pipeline receives its required inputs from:

```text
config/prod.conf
```

Configuration used:

```text
SLACK_CHANNEL_NAME=build-status
ENVIRONMENT=prod
CODE_BASE_PATH=.
ACTION_MESSAGE=Redis deployment completed
KEEP_APPROVAL_STAGE=true
EMAIL_RECIPIENT=syedwessi06@gmail.com
```

### Screenshot 2 – Configuration File

> **Insert screenshot here**

---

## Jenkins Pipeline

The `Jenkinsfile` uses the Shared Library:

```groovy
@Library('ansible-shared-library') _
```

The pipeline contains the following stages:

- Read Config
- Clone
- User Approval
- Playbook Execution

A `post` section is used to send notifications after the pipeline execution.

### Screenshot 3 – Jenkinsfile

> **Insert screenshot here**

---

## Shared Library Functions

The Shared Library is implemented in:

```text
vars/ansibleDeploy.groovy
```

It provides functions for:

```text
readConfig()
cloneCode()
userApproval()
executePlaybook()
sendNotification()
```

The library reads the configuration file and uses the configured values during pipeline execution.

---

## Ansible Playbook

The Assignment 6 playbook is:

```text
assignment6.yml
```

The playbook:

1. Verifies that the servers are reachable using the Ansible `ping` module.
2. Creates a deployment marker:

```text
/tmp/assignment6-deployed
```

The playbook is executed through Jenkins using:

```bash
ansible-playbook -i hosts assignment6.yml
```

---

## User Approval

The pipeline checks:

```text
KEEP_APPROVAL_STAGE=true
```

When enabled, Jenkins pauses the pipeline and requests approval before executing the deployment.

Example:

```text
Deploy to prod?
```

The deployment continues after the user selects **Approve**.

---

## Deployment Execution

The Ansible playbook was executed successfully against:

- Ubuntu server
- RHEL server

Both servers returned successful Ansible results.

### Screenshot 4 – Successful Jenkins Console Output

> **Insert screenshot here**

The console output should show:

```text
Read Config
Clone
User Approval
Playbook Execution
ok: [ubuntu-server]
ok: [rhel-server]
Declarative: Post Actions
Finished: SUCCESS
```

---

## Notifications

After the deployment, the Shared Library sends notifications through Slack and Email.

### Slack

Slack notification is sent to:

```text
#build-status
```

### Email

An email notification is sent to the configured recipient.

### Screenshot 5 – Slack Notification

> **Insert screenshot here**

### Screenshot 6 – Email Notification

> **Insert screenshot here**

---

## Complete Pipeline Flow

```text
        Jenkins
           |
           v
   Read Configuration
           |
           v
       Clone Code
           |
           v
     User Approval
           |
           v
    Ansible Playbook
           |
           v
   Ubuntu + RHEL Servers
           |
           v
      Post Actions
        /       \
       v         v
    Slack      Email
```

---

## Result

The Jenkins Shared Library based deployment pipeline was successfully implemented.

The pipeline successfully:

- Loaded configuration from `prod.conf`
- Cloned the project
- Requested user approval
- Executed the Ansible playbook
- Verified Ubuntu and RHEL servers
- Sent Slack notification
- Sent Email notification
- Completed with `Finished: SUCCESS`
