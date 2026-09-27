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

<img width="1919" height="164" alt="image" src="https://github.com/user-attachments/assets/f5053953-dffd-496b-86eb-462028fd2ca3" />


### Screenshot

<!-- Add screenshots/00-dashboard.png here -->

---

# 2. Python CI — Attendance API

### Jenkins Job

`CI-Attendance-Python`

<img width="1917" height="827" alt="image" src="https://github.com/user-attachments/assets/c5573064-da2e-470d-bfa5-2a3da57de2d2" />


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

<img width="1919" height="985" alt="image" src="https://github.com/user-attachments/assets/ef8a5516-653c-41af-94a6-06f4eabb51c7" />


### CI Checks

<img width="1919" height="923" alt="image" src="https://github.com/user-attachments/assets/1f5b8a53-573f-48b4-a03c-1c9b90709d37" />


### Coverage Report

<img width="1919" height="437" alt="image" src="https://github.com/user-attachments/assets/97454a60-3ffc-42e2-8bf7-327d732f0d6a" />


### Archived Artifacts

<img width="1919" height="872" alt="image" src="https://github.com/user-attachments/assets/8f224bbd-3667-4e5f-9519-76ad7967078b" />


<img width="1918" height="1023" alt="image" src="https://github.com/user-attachments/assets/bee1d913-2529-47ac-bfb8-9d71defefe0c" />


---

# 3. Go CI — Employee API

### Jenkins Job

`CI-Employee-Go`

### CI Checks Performed

<img width="1919" height="1077" alt="image" src="https://github.com/user-attachments/assets/e9746009-7c12-4b51-ad0c-9fb6986fe0b0" />


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

<img width="1918" height="814" alt="image" src="https://github.com/user-attachments/assets/deaaee30-f0f8-4939-8df0-93e4e5a503f2" />


### CI Checks

<img width="1919" height="1077" alt="image" src="https://github.com/user-attachments/assets/42727128-8683-4d0a-9c49-2fce3e6f84b6" />



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

<img width="1916" height="598" alt="image" src="https://github.com/user-attachments/assets/5e8d8aab-a98c-484f-b93b-c40e137f1d14" />


### CI Checks

<img width="1919" height="245" alt="image" src="https://github.com/user-attachments/assets/3ff4c860-ffc6-4208-b1e3-babe182655de" />


### Artifacts

No Java artifacts were configured for the Java Jenkins job.

---

# 5. Email Notifications

Email notifications were configured using Jenkins **Editable Email Notification**.

<img width="1919" height="1060" alt="image" src="https://github.com/user-attachments/assets/ce4ed0f1-ba8e-40f4-a11a-7100e8e6f76c" />


### Configuration

The **Failure - Any** trigger was configured.

<!-- Add screenshots/notifications/01-email-config.png here -->

### Email Notification Test

A Jenkins success notification was received successfully.

<img width="1919" height="673" alt="image" src="https://github.com/user-attachments/assets/cf4d74a8-3f6f-40fd-ba11-8d64c73db2f8" />



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
