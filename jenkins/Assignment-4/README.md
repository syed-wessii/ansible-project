# Jenkins Assignment 4 -- Declarative CI Pipeline

## Overview

This assignment implements a **Declarative CI Pipeline in Jenkins** for
the `Spring3Hibernate` Java project.

The pipeline performs source-code checkout, parallel CI checks,
SonarQube code-quality analysis, code-coverage analysis, report
generation, artifact creation, approval, artifact publication, and email
notifications.

## Project Repository

-   **GitHub Repository:**
    `https://github.com/opstree/spring3hibernate.git`
-   **Branch:** `master`
-   **Jenkins Job:** `Assignment4-Spring3Hibernate`
-   **Application:** Spring3Hibernate

------------------------------------------------------------------------

## Pipeline Flow

``` text
Code Checkout
      |
      v
 CI Checks
      |
      +-------------------+-------------------+
      |                   |                   |
      v                   v                   v
Code Stability      Code Quality       Code Coverage
      |                   |                   |
      +-------------------+-------------------+
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
                    +-----+-----+
                    |           |
                  Approve      Deny
                    |
                    v
              Publish Artifact
                    |
                    v
             Email Notification
```

------------------------------------------------------------------------

## Technologies Used

-   Jenkins
-   Git / GitHub
-   Maven
-   Java 11
-   SonarQube
-   JaCoCo
-   Jenkins Coverage Plugin
-   Email Extension Plugin
-   Jenkins Pipeline

------------------------------------------------------------------------

# Pipeline Stages

## 1. Code Checkout

The pipeline checks out the `master` branch from the Spring3Hibernate
GitHub repository.

The source code is then made available to the subsequent CI stages.

### Screenshot

> Add screenshot here.

`![Code Checkout](screenshots/01-code-checkout.png)`

------------------------------------------------------------------------

## 2. CI Checks

The CI checks run in parallel to reduce overall pipeline execution time.

### Code Stability

Runs the project's tests using Maven:

``` bash
mvn clean test
```

### Code Quality

The pipeline:

-   Compiles the project.
-   Performs SonarQube analysis.
-   Uses the SonarQube project key `spring3hibernate`.

SonarQube analysis is performed using:

``` bash
mvn org.sonarsource.scanner.maven:sonar-maven-plugin:5.8.0.7211:sonar
```

### Code Coverage

JaCoCo is used to generate code-coverage data:

``` bash
mvn clean org.jacoco:jacoco-maven-plugin:0.8.13:prepare-agent test org.jacoco:jacoco-maven-plugin:0.8.13:report
```

The generated JaCoCo XML report is published through the Jenkins
Coverage Plugin.

### Screenshot

> Add screenshot of the parallel CI configuration here.

`![Parallel CI Checks](screenshots/02-parallel-ci-checks.png)`

------------------------------------------------------------------------

# 3. Generate Reports

The pipeline generates and publishes the available CI analysis and
coverage reports.

The JaCoCo report is recorded by Jenkins using the coverage parser.

### Screenshot

> Add screenshot here.

`![Generate Reports](screenshots/03-generate-reports.png)`

------------------------------------------------------------------------

# 4. Build Artifact

The Java application is packaged as a WAR file using Maven:

``` bash
mvn clean package -DskipTests
```

The generated WAR file is:

``` text
Spring3HibernateApp.war
```

### Screenshot

> Add screenshot here.

`![Build Artifact](screenshots/04-build-artifact.png)`

------------------------------------------------------------------------

# 5. Approval Stage

Before publishing the artifact, Jenkins pauses the pipeline and requests
manual approval.

The user can:

-   **APPROVE** the publication
-   **DENY** the publication

The successful pipeline execution used the approval option before
publishing the artifact.

### Screenshot

> Add screenshot of the approval step here.

`![Approval Stage](screenshots/05-approval.png)`

------------------------------------------------------------------------

# 6. Publish Artifacts

After approval, Jenkins archives the generated WAR artifact.

Artifact pattern:

``` text
artifact/target/*.war
```

The artifact is fingerprinted for tracking.

The pipeline displays:

``` text
Artifact published successfully
```

### Screenshot

> Add screenshot here.

`![Publish Artifact](screenshots/06-publish-artifact.png)`

------------------------------------------------------------------------

# 7. SonarQube Analysis

SonarQube is integrated with Jenkins for static code-quality analysis.

The SonarQube project is:

``` text
spring3hibernate
```

The analysis completed successfully and the project Quality Gate was
reported as **Passed**.

### Screenshot

> Add SonarQube dashboard screenshot here.

`![SonarQube Dashboard](screenshots/07-sonarqube.png)`

------------------------------------------------------------------------

# 8. Email Notification

The pipeline uses the Jenkins Email Extension Plugin (`emailext`) to
send notifications after the pipeline execution.

Notifications are configured for successful and unsuccessful/aborted
executions.

### Screenshot

> Add screenshot of the email notification configuration here.

`![Email Notification](screenshots/08-email-notification.png)`

------------------------------------------------------------------------

# 9. Final Pipeline Verification

The completed Jenkins build successfully executed all major stages:

-   Code Checkout
-   CI Checks
-   Code Stability
-   Code Quality
-   Code Coverage
-   Generate Reports
-   Build Artifact
-   Approval
-   Publish Artifacts
-   Post Actions

The final build result was:

``` text
Finished: SUCCESS
```

### Screenshot

> Add the Jenkins Stage View screenshot showing the successful pipeline
> here.

`![Jenkins Stage View](screenshots/09-stage-view.png)`

------------------------------------------------------------------------

# Build Verification

The successful build generated the WAR artifact:

``` text
artifact/target/Spring3HibernateApp.war
```

The artifact was archived by Jenkins after manual approval.

### Screenshot

> Optional: Add the Jenkins archived-artifact screenshot here.

`![Archived Artifact](screenshots/10-archived-artifact.png)`

------------------------------------------------------------------------

# Notes

-   The original project uses an older Maven compiler configuration
    targeting Java 6.
-   For the Jenkins build, the pipeline temporarily adjusts the local
    `pom.xml` compiler source and target to Java 8 so that the legacy
    project can be compiled with the configured JDK.
-   This modification is performed in the Jenkins workspace and does
    **not** modify the GitHub repository.
-   The old OWASP Dependency-Check configuration in the project was not
    used as a blocking verification step because its legacy NVD feed
    configuration caused dependency-feed errors during the build.
-   Slack notification was not included in the final implementation.

------------------------------------------------------------------------

# Result

The Jenkins Declarative CI pipeline was successfully implemented and
verified.

The final successful Jenkins execution demonstrated:

``` text
Checkout
   ↓
Parallel CI Checks
   ↓
Reports
   ↓
WAR Build
   ↓
Manual Approval
   ↓
Artifact Publication
   ↓
Email Notification
   ↓
SUCCESS
```
