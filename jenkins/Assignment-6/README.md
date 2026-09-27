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

<img width="1919" height="758" alt="Screenshot 2026-09-26 111958" src="https://github.com/user-attachments/assets/34a8992a-54fb-4be6-90a3-14e3f5771912" />


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

<img width="819" height="895" alt="Screenshot 2026-09-26 113259" src="https://github.com/user-attachments/assets/5294e2dc-89f8-4b29-b927-1a638fabee9f" />

<img width="960" height="372" alt="2026-09-26 15_38_12-_git token for Jenkins - Notepad" src="https://github.com/user-attachments/assets/4f8958fa-a19c-4bc9-9a36-a920355f06a6" />

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

<img width="953" height="478" alt="2026-09-26 15_39_56-_git token for Jenkins - Notepad" src="https://github.com/user-attachments/assets/95ffe082-63f7-4d79-99c6-86c7dbd65387" />

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
<img width="960" height="388" alt="2026-09-26 15_35_02-_git token for Jenkins - Notepad" src="https://github.com/user-attachments/assets/3f236f7a-77b1-4d12-8af2-868435793eb7" />

<img width="953" height="478" alt="2026-09-26 15_39_56-_git token for Jenkins - Notepad" src="https://github.com/user-attachments/assets/ff7a29ca-19b6-4544-8358-5ecc8120df68" />

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
<img width="946" height="466" alt="2026-09-26 15_53_55-Greenshot" src="https://github.com/user-attachments/assets/0bfcaf87-d158-46e5-858d-df9b2c441957" />

---

## User Approval

The pipeline checks:

```text
KEEP_APPROVAL_STAGE=true
```
<img width="1917" height="241" alt="image" src="https://github.com/user-attachments/assets/a55b6986-72b1-49bd-b3f9-15ff5c76a926" />


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

<img width="1919" height="791" alt="image" src="https://github.com/user-attachments/assets/4842aae9-72f1-46be-aa31-0db3fe8a442c" />


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

<img width="1896" height="189" alt="image" src="https://github.com/user-attachments/assets/724c81aa-a5f8-442d-9361-7da85178b939" />


### Screenshot 6 – Email Notification

<img width="1905" height="628" alt="image" src="https://github.com/user-attachments/assets/e5d0097b-5471-4550-ad4e-5d1ac5b6b06f" />


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
