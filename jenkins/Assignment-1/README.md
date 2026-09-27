# Jenkins Assignment 1

## Overview

This assignment demonstrates Jenkins automation for Git operations, parameterized builds, artifact transfer, web-server publishing, and Slack notifications.

---

# Part 1 — Git Operations

A Jenkins job was created to automate the following Git operations:

1. Create a branch
2. List all branches
3. Make changes on branches
4. Merge `dev` into `master`
5. Create `rebase-branch`
6. Rebase `rebase-branch` onto `master`
7. Delete the `dev` branch
8. Display the final branch list
9. Send notifications when the job succeeds or fails

## Successful Git Operations

The Jenkins console output confirms successful branch creation, branch listing, changes, merge, and rebase.

<img width="262" height="212" alt="image" src="https://github.com/user-attachments/assets/830807e8-7fca-4619-b5ef-aacedba46f97" />


The remaining console output confirms the rebase, deletion of the `dev` branch, final branch list, and successful completion.

<img width="688" height="945" alt="image" src="https://github.com/user-attachments/assets/2082c633-3e44-4296-be2f-3e6e9b36d8aa" />

<img width="613" height="986" alt="image" src="https://github.com/user-attachments/assets/8b96fc74-cf5c-48f3-99e4-2c8f12520b99" />



### Final Result

```textq
FINAL BRANCH LIST
* master
  rebase-branch

ALL GIT OPERATIONS COMPLETED SUCCESSFULLY
Finished: SUCCESS
```

---

# Part 2 — Parameterized File Creation and Web Server

## Job 1 — `Job1_CreateFile`

`Job1_CreateFile` is configured as a parameterized Jenkins job.

The job accepts a string parameter named `NINJA_NAME` and allows `Job2_WebServer` to copy its archived artifacts.

<img width="1913" height="1026" alt="image" src="https://github.com/user-attachments/assets/a5b673f2-bd78-4065-bf34-1f0c12d1449a" />


### Job 1 Build

The build creates `ninja.txt` using the supplied Ninja name.

The generated file contains:

```text
syed from DevOps Ninja
```

The build also archives the file and automatically triggers `Job2_WebServer`.

<img width="1919" height="887" alt="image" src="https://github.com/user-attachments/assets/827ab0e8-8631-4437-8053-0ff414c5908e" />


---

## Job 2 — `Job2_WebServer`

`Job2_WebServer` is configured to run automatically after a successful `Job1_CreateFile` build.

It copies the archived `ninja.txt` artifact from `Job1_CreateFile`, verifies the file, and displays its contents.

<img width="1919" height="962" alt="image" src="https://github.com/user-attachments/assets/e348256d-b969-4f29-a70b-388cd6904de9" />


The console output confirms:

```text
Started by upstream project "Job1_CreateFile"
Copied 1 artifact from "Job1_CreateFile"
File found successfully.
File content:
syed from DevOps Ninja
Finished: SUCCESS
```

---

## Web Server Verification

The generated `ninja.txt` file is published through the web server and is accessible at:

```text
http://localhost:8000/ninja.txt
```

<img width="1919" height="262" alt="image" src="https://github.com/user-attachments/assets/e77c8285-89dd-4071-8391-52630925c583" />

---

# Slack Notifications

Slack notifications were configured for the Jenkins jobs.

## Successful Build Notification

The Slack `#build-status` channel shows successful notifications for both jobs.

<img width="1912" height="334" alt="image" src="https://github.com/user-attachments/assets/025b5c07-a8d3-4ec8-9ed1-fb61e75df216" />


## Failure Notification

The Slack channel also received failure notifications from `Job2_WebServer` during the earlier artifact-copy permission issue.

<img width="1644" height="324" alt="image" src="https://github.com/user-attachments/assets/2f8a445d-f09c-4e03-b593-426acfacf82a" />


This verifies that failure notifications are being sent when a Jenkins build fails.

---

# Final Verification

| Requirement | Status |
|---|---|
| Create Git branch | ✅ |
| List Git branches | ✅ |
| Merge branches | ✅ |
| Rebase branch | ✅ |
| Delete branch | ✅ |
| Job 1 accepts `NINJA_NAME` | ✅ |
| Job 1 creates `ninja.txt` | ✅ |
| Artifact archived by Job 1 | ✅ |
| Job 2 automatically triggered | ✅ |
| Job 2 copies artifact | ✅ |
| Web server publishes `ninja.txt` | ✅ |
| Slack success notification | ✅ |
| Slack failure notification | ✅ |

## Conclusion

The Jenkins assignment was completed successfully. The implementation demonstrates Git automation, parameterized Jenkins jobs, artifact sharing between jobs, downstream job triggering, web-server publishing, and Slack build notifications.
