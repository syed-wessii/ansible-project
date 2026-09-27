# Jenkins Assignment 03 — CI Checks

## Overview

This assignment implements Continuous Integration (CI) checks for three repositories using Jenkins Freestyle Jobs.

The Jenkins jobs perform CI checks, generate reports, archive artifacts, and configure email notifications.

---

## Repositories

| Language | Repository | Jenkins Job |
|---|---|---|
| Python | `OT-MICROSERVICES/attendance-api` | `CI-Attendance-Python` |
| Go | `OT-MICROSERVICES/employee-api` | `CI-Employee-Go` |
| Java | `syed-wessii/spring3hibernate` | `CI-Spring3Hibernate` |

---

# 1. Jenkins Dashboard

All three CI jobs completed successfully.

### Screenshot

<!-- Add screenshots/00-dashboard.png here -->

---

# 2. Python CI — Attendance API

### Jenkins Job

`CI-Attendance-Python`

### CI Checks Performed

- Gitleaks credential scanning
- Dependency security check
- Python version verification
- Poetry dependency management
- Unit testing
- Code coverage
- HTML coverage report generation
- Artifact archiving
- Email notification

### Results

- **Unit Tests:** 15 passed
- **Code Coverage:** 95%
- **Dependency Scan:** No known vulnerabilities
- **Build Status:** SUCCESS

### Job Success

<!-- Add screenshots/python/01-job-success.png here -->

### CI Checks

<!-- Add screenshots/python/02-ci-checks.png here -->

### Coverage Report

<!-- Add screenshots/python/03-coverage.png here -->

### Archived Artifacts

<!-- Add screenshots/python/04-artifacts.png here -->

---

# 3. Go CI — Employee API

### Jenkins Job

`CI-Employee-Go`

### CI Checks Performed

- Gitleaks credential scanning
- Go dependency management
- Vulnerability scanning
- `go vet`
- Unit testing
- Code coverage
- HTML coverage report generation
- Application build
- Artifact archiving
- Email notification

### Results

- **Code Coverage:** 41.2%
- **Application Build:** Successful
- **CI Checks:** Passed successfully
- **Build Status:** SUCCESS

### Job Success

<!-- Add screenshots/go/01-job-success.png here -->

### CI Checks

<!-- Add screenshots/go/02-ci-checks.png here -->

### Coverage Report

<!-- Add screenshots/go/03-coverage.png here -->

### Archived Artifacts

<!-- Add screenshots/go/04-artifacts.png here -->

---

# 4. Java CI — Spring3Hibernate

### Jenkins Job

`CI-Spring3Hibernate`

### CI Checks Performed

- Maven compilation
- Maven unit testing
- Java compatibility configuration
- Maven Surefire test execution
- Email notification

### Results

- **Tests:** 3
- **Failures:** 0
- **Errors:** 0
- **Skipped:** 0
- **Build:** SUCCESS

### Job Success

<!-- Add screenshots/java/01-job-success.png here -->

### CI Checks

<!-- Add screenshots/java/02-ci-checks.png here -->

### Artifacts

No Java artifacts were configured for the Java Jenkins job.

---

# 5. Email Notifications

Email notifications were configured using Jenkins **Editable Email Notification**.

### Configuration

The **Failure - Any** trigger was configured.

<!-- Add screenshots/notifications/01-email-config.png here -->

### Email Notification Test

A Jenkins success notification was received successfully.

<!-- Add screenshots/notifications/02-success-email.png here -->

> Note: A failure email was not retained, so no failure-email screenshot is included.

---

# 6. Artifacts and Reports

### Python

Archived artifacts include:

- HTML coverage report
- Pytest HTML reports
- Static report files

### Go

Archived artifacts include:

- `coverage.html`
- `coverage.out`
- `employee-api`

### Java

No artifacts were configured for the Java Jenkins job.

---

# 7. Jenkins Jobs Summary

| Job | Language | Tests / Checks | Coverage | Status |
|---|---|---|---:|---|
| `CI-Attendance-Python` | Python | Unit tests, Gitleaks, dependency scan | 95% | SUCCESS |
| `CI-Employee-Go` | Go | Tests, Gitleaks, vulnerability scan, vet, build | 41.2% | SUCCESS |
| `CI-Spring3Hibernate` | Java | Maven compilation and unit tests | — | SUCCESS |

---

# 8. Assignment Requirements

- [x] Three separate Jenkins Freestyle Jobs
- [x] GitHub repository integration
- [x] Generic CI checks
- [x] Credential scanning
- [x] Dependency/vulnerability checks
- [x] Unit testing
- [x] Code coverage
- [x] Reports generated
- [x] Jenkins artifact storage
- [x] Email notifications
- [x] Successful CI execution verification

---

## Screenshot Directory

```text
screenshots/
├── 00-dashboard.png
├── python/
│   ├── 01-job-success.png
│   ├── 02-ci-checks.png
│   ├── 03-coverage.png
│   └── 04-artifacts.png
├── go/
│   ├── 01-job-success.png
│   ├── 02-ci-checks.png
│   ├── 03-coverage.png
│   └── 04-artifacts.png
├── java/
│   ├── 01-job-success.png
│   └── 02-ci-checks.png
└── notifications/
    ├── 01-email-config.png
    └── 02-success-email.png
```

---

## Conclusion

Jenkins Freestyle Jobs were created for Python, Go, and Java repositories to perform CI validation, testing, coverage analysis, security checks, report generation, artifact management, and email notifications.

All three Jenkins jobs completed successfully.
