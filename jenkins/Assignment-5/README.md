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

<img width="1919" height="225" alt="image" src="https://github.com/user-attachments/assets/2d9a72d0-ccdf-46a9-b6f2-2d0fb82e81b0" />


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

<img width="1919" height="291" alt="image" src="https://github.com/user-attachments/assets/ff18b0a4-aa26-4f50-8a0e-2de499af22d0" />


#### Code Stability

<img width="1918" height="1054" alt="image" src="https://github.com/user-attachments/assets/47ebde12-ab1f-4430-9b56-db790bfbd563" />


Runs the Maven test/compilation checks required for code stability.

#### Code Quality

<img width="1910" height="1065" alt="image" src="https://github.com/user-attachments/assets/2f1b57c5-495b-47b3-aad4-b24d55ee97df" />


Uses **SonarQube** for static code-quality analysis.

#### Code Coverage

Uses **JaCoCo** to execute tests and generate the code-coverage report.

**Verification Screenshot:**

<img width="1919" height="1057" alt="image" src="https://github.com/user-attachments/assets/8015200f-1a19-436f-af0f-1ba87ef27edb" />


```{=html}
<!-- Insert screenshot here -->
```
`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 3. Generate Reports

The pipeline generates the required reports after the CI checks are
completed.



> **Screenshot 3 -- Generate Reports**

```{=html}
<img width="1914" height="339" alt="image" src="https://github.com/user-attachments/assets/d511f386-0e00-4aeb-8fc6-89d176c78338" />

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
<img width="1891" height="1051" alt="image" src="https://github.com/user-attachments/assets/c75f4548-0979-4f95-8dfd-1a0719f0fbdb" />

`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 5. Approval

A manual approval step is included before publishing the artifacts.

The pipeline pauses and waits for interactive input before continuing.

**Verification Screenshot:**

> **Screenshot 5 -- Manual Approval**

```{=html}
<img width="1912" height="417" alt="image" src="https://github.com/user-attachments/assets/174b1046-23a9-4549-8552-d45916d0c89e" />

`<br>`{=html}`<br>`{=html}`<br>`{=html}

------------------------------------------------------------------------

### 6. Publish Artifacts

The generated artifacts are archived and published by Jenkins.

The pipeline also records fingerprints for the archived artifacts.

**Verification Screenshot:**

> **Screenshot 6 -- Publish / Archive Artifacts**

```{=html}
<img width="1910" height="441" alt="image" src="https://github.com/user-attachments/assets/29bf02ef-5b26-4212-90e2-035accb6be57" />

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
<img width="1910" height="504" alt="image" src="https://github.com/user-attachments/assets/a7a00b42-597b-49b5-b1ea-1164a59044f4" />

<img width="1642" height="346" alt="image" src="https://github.com/user-attachments/assets/f3593250-78fb-49a5-9abf-794311cb9ff4" />

<img width="1919" height="752" alt="image" src="https://github.com/user-attachments/assets/a340358b-6d69-4575-b309-7254e9907cea" />



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

<img width="1911" height="457" alt="image" src="https://github.com/user-attachments/assets/4c555d75-163b-4335-b5a2-28667a9f8fc3" />

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
