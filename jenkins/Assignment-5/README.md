# Jenkins Assignment 5 -- Scripted Pipeline

## Overview

This assignment demonstrates a **Scripted Jenkins Pipeline**
implementing a complete CI/CD workflow with parallel CI checks,
reporting, artifact creation, manual approval, artifact publishing, and
notifications.

## Pipeline Flow

``` text
Code Checkout
      |
      v
   CI Checks
   /   |   \
  /    |    \
Code  Code  Code
Stability Quality Coverage
      |
      v
Generate Reports
      |
      v
Build Artifact
      |
      v
Approval
      |
      v
Publish Artifacts
      |
      v
Notifications
```

------------------------------------------------------------------------

## Technologies Used

-   Jenkins
-   Git / GitHub
-   Maven
-   Java
-   SonarQube
-   JaCoCo
-   Jenkins Scripted Pipeline
-   Email Notification
-   Slack Notification

------------------------------------------------------------------------

## Pipeline Stages

### 1. Code Checkout

The pipeline checks out the source code from the configured Git
repository.

**Verification Screenshot:**

> **Screenshot 1 -- Code Checkout**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 2. CI Checks

The CI Checks stage runs three checks in parallel:

-   **Code Stability**
-   **Code Quality**
-   **Code Coverage**

#### Code Stability

Runs the Maven test/compilation checks required for code stability.

#### Code Quality

Uses **SonarQube** for static code-quality analysis.

#### Code Coverage

Uses **JaCoCo** to execute tests and generate the code-coverage report.

**Verification Screenshot:**

> **Screenshot 2 -- CI Checks (Parallel Execution)**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 3. Generate Reports

The pipeline generates the required reports after the CI checks are
completed.

**Verification Screenshot:**

> **Screenshot 3 -- Generate Reports**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 4. Build Artifact

The pipeline builds the application artifact using Maven.

The build uses:

``` bash
mvn clean package -DskipTests
```

**Verification Screenshot:**

> **Screenshot 4 -- Build Artifact**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 5. Approval

A manual approval step is included before publishing the artifacts.

The pipeline pauses and waits for interactive input before continuing.

**Verification Screenshot:**

> **Screenshot 5 -- Manual Approval**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 6. Publish Artifacts

The generated artifacts are archived and published by Jenkins.

The pipeline also records fingerprints for the archived artifacts.

**Verification Screenshot:**

> **Screenshot 6 -- Publish / Archive Artifacts**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 7. Notifications

The pipeline sends notifications after completion.

Configured notifications:

-   Extended Email
-   Slack message

The Slack notification is configured for the `#build-status` channel.

**Verification Screenshot:**

> **Screenshot 7 -- Email and Slack Notifications**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

## Code Coverage Report

The Jenkins Coverage report provides an overview of:

-   Instruction Coverage
-   Branch Coverage
-   Line Coverage
-   Method Coverage
-   Class Coverage
-   File Coverage
-   Package Coverage
-   Coverage Trend

**Verification Screenshot:**

> **Screenshot 8 -- Coverage Report**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

## Overall Pipeline Verification

The Jenkins Pipeline Overview confirms the complete execution flow:

-   Code Checkout
-   CI Checks
    -   Code Stability
    -   Code Quality
    -   Code Coverage
-   Generate Reports
-   Build Artifact
-   Approval
-   Publish Artifacts
-   Notifications

All stages completed successfully in the verified build.

**Verification Screenshot:**

> **Screenshot 9 -- Complete Pipeline Overview**

```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

## Build Verification

**Jenkins Job:** `Assignment-5-Scripted`

**Verified Build:** `#9`

**Build Status:** `SUCCESS`

The pipeline completed the complete workflow successfully, including CI
checks, report generation, artifact creation, manual approval, artifact
publishing, and notifications.

------------------------------------------------------------------------

## Conclusion

This assignment demonstrates how a **Scripted Jenkins Pipeline** can
automate a complete CI workflow while supporting:

-   Parallel CI checks
-   SonarQube code-quality analysis
-   JaCoCo code-coverage reporting
-   Maven artifact creation
-   Manual approval
-   Artifact archiving and publishing
-   Email and Slack notifications
