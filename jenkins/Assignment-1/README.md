# Jenkins Assignment 6

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

![Git Operations - Part 1](screenshots/part1_git_success_1.png)

The remaining console output confirms the rebase, deletion of the `dev` branch, final branch list, and successful completion.

![Git Operations - Part 1 Final](screenshots/part1_git_success_2.png)

### Final Result

```text
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

![Job 1 Configuration](screenshots/part2_job1_configuration.png)

### Job 1 Build

The build creates `ninja.txt` using the supplied Ninja name.

The generated file contains:

```text
syed from DevOps Ninja
```

The build also archives the file and automatically triggers `Job2_WebServer`.

![Job 1 Console Output](screenshots/part2_job1_console.png)

---

## Job 2 — `Job2_WebServer`

`Job2_WebServer` is configured to run automatically after a successful `Job1_CreateFile` build.

It copies the archived `ninja.txt` artifact from `Job1_CreateFile`, verifies the file, and displays its contents.

![Job 2 Console Output](screenshots/part2_job2_console.png)

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

![Web Server Output](screenshots/part2_web_server.png)

---

# Slack Notifications

Slack notifications were configured for the Jenkins jobs.

## Successful Build Notification

The Slack `#build-status` channel shows successful notifications for both jobs.

![Slack Success Notification](screenshots/part2_slack_success.png)

## Failure Notification

The Slack channel also received failure notifications from `Job2_WebServer` during the earlier artifact-copy permission issue.

![Slack Failure Notification](screenshots/part2_slack_failure.png)

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
