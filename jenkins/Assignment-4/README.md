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

<img width="1914" height="1004" alt="image" src="https://github.com/user-attachments/assets/a2804d68-12cb-4fa4-95b0-d5240fd076c0" />


------------------------------------------------------------------------

## 2. CI Checks

The CI checks run in parallel to reduce overall pipeline execution time.

<img width="1201" height="801" alt="image" src="https://github.com/user-attachments/assets/d1ce7eb3-1053-4872-a3d7-abc3123ae9e5" />

<img width="1217" height="837" alt="image" src="https://github.com/user-attachments/assets/25297e18-20a5-433f-ac99-05b79ceb2f2e" />

<img width="1234" height="943" alt="image" src="https://github.com/user-attachments/assets/b0694e0b-fd9f-4376-91d9-9f3380070301" />


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

<img width="1914" height="993" alt="image" src="https://github.com/user-attachments/assets/efa35c25-927c-4884-9bb4-426f926838d9" />


------------------------------------------------------------------------

# 3. Generate Reports

The pipeline generates and publishes the available CI analysis and
coverage reports.

The JaCoCo report is recorded by Jenkins using the coverage parser.



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

<img width="1919" height="469" alt="image" src="https://github.com/user-attachments/assets/bd27cd90-ecc6-4a3c-9a6b-756d0cb20586" />


------------------------------------------------------------------------

# 5. Approval Stage

Before publishing the artifact, Jenkins pauses the pipeline and requests
manual approval.

The user can:

-   **APPROVE** the publication
-   **DENY** the publication

The successful pipeline execution used the approval option before
publishing the artifact.



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

<img width="1128" height="377" alt="image" src="https://github.com/user-attachments/assets/ed6f5e92-89c0-4297-824d-7dd86a264c17" />


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

<img width="1919" height="716" alt="image" src="https://github.com/user-attachments/assets/2d494d2d-537e-4563-9b2e-59094fca59f0" />


------------------------------------------------------------------------

# 8. Email Notification

The pipeline uses the Jenkins Email Extension Plugin (`emailext`) to
send notifications after the pipeline execution.

Notifications are configured for successful and unsuccessful/aborted
executions.


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

<img width="1766" height="276" alt="image" src="https://github.com/user-attachments/assets/baac95ca-a4b3-4685-8665-7ed328d2f3bb" />

<img width="1057" height="204" alt="image" src="https://github.com/user-attachments/assets/1c4bfbc1-5b9e-4c50-ba22-07560d44deb6" />


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
