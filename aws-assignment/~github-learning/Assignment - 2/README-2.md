# Assignment 2: Deployment Strategies with AWS

## Overview

This assignment explores deployment strategies on AWS and demonstrates how application versions can be deployed, verified, and promoted using EC2, Auto Scaling Groups, Application Load Balancers, and Amazon S3.

The application used for this assignment is **Spring3HibernateApp**.

## Objectives

- Understand Recreate, Rolling, Blue-Green, Canary, and A/B deployment strategies.
- Deploy an application manually on an EC2 instance and create an AMI.
- Store deployment artifacts and static assets in Amazon S3.
- Perform a Rolling Deployment using an Auto Scaling Group and Launch Templates.
- Demonstrate Blue-Green traffic switching with an Application Load Balancer (ALB).
- Demonstrate weighted traffic routing for a Canary-style rollout.
- Verify application versions through HTTP requests.

## AWS Services Used

- Amazon EC2
- Amazon Machine Images (AMI)
- EC2 Auto Scaling Groups (ASG)
- EC2 Launch Templates
- Application Load Balancer (ALB)
- ALB Target Groups and weighted forwarding
- Amazon S3
- AWS IAM instance roles
- AWS CLI

## Application and Artifact Versions

| Version | S3 artifact | Displayed verification text |
|---|---|---|
| v1 | `artifacts/Spring3HibernateApp.war` | `Assignment 2 - Static Asset Test` |
| v2 | `artifacts/Spring3HibernateApp-v2.war` | `Assignment 2 - Version 2` |

> The AWS resources used during the exercise have been cleaned up. The names and configuration below document the implementation; the resources are not expected to exist now.

---

## 1. Recreate Deployment

### Implementation

1. Launched an EC2 instance named `Assignment2-Recreate-v1`.
2. Installed/configured the application and Apache Tomcat.
3. Created an AMI named `Assignment2-Recreate-v1-AMI`.
4. Stored a static asset (`version.txt`) in an S3 bucket.
5. Retrieved the asset from S3 and included it in the application package so the application could serve it.
6. Verified the application in a browser or with `curl`.

### Verification result

The application returned:

```text
Assignment 2 - Static Asset Test
```

### Screenshots

<!-- Add screenshots to the screenshots/ directory and replace the placeholders below. -->

**1.1 EC2 instance and application deployment**

![Recreate EC2 deployment](screenshots/recreate-ec2.png)

**1.2 AMI available**

![Recreate AMI](screenshots/recreate-ami.png)

**1.3 S3 static asset**

![S3 static asset](screenshots/s3-static-asset.png)

**1.4 Application response**

![Recreate application response](screenshots/recreate-app-response.png)

---

## 2. Rolling Deployment

### Implementation

1. Stored v1 and v2 WAR artifacts in S3.
2. Created Launch Templates for the initial and updated application versions:
   - `Assignment2-Rolling-v1`
   - `Assignment2-Rolling-v2`
3. Created an Auto Scaling Group named `Assignment2-Rolling-ASG`.
4. Configured the ASG with:
   - Minimum capacity: `1`
   - Desired capacity: `2`
   - Maximum capacity: `2`
5. Updated the ASG to use the v2 Launch Template.
6. Started an Instance Refresh to replace the old instances with new instances.
7. Confirmed that the Instance Refresh completed successfully and that the v2 application responded.

### Verification result

The application returned:

```text
Assignment 2 - Version 2
```

### Screenshots

![Rolling ASG configuration](screenshots/rolling-asg.png)

![Rolling Launch Templates](screenshots/rolling-launch-templates.png)

![Rolling Instance Refresh successful](screenshots/rolling-instance-refresh.png)

![Rolling v2 application response](screenshots/rolling-v2-response.png)

---

## 3. Blue-Green Deployment

### Concept

Blue-Green deployment maintains two separate environments. One environment serves the current version while the other receives the updated version. Traffic can be switched between the environments through a load balancer.

### Implementation

- **Blue environment:** v1
- **Green environment:** v2
- Created separate target groups:
  - `Assignment2-Blue-TG`
  - `Assignment2-Green-TG`
- Created an Application Load Balancer named `Assignment2-BlueGreen-ALB`.
- Registered each environment in its target group.
- Changed the ALB listener's default forwarding target to demonstrate switching traffic between Blue and Green.
- Verified the response through the ALB DNS name.

### Verification results

Blue returned:

```text
Assignment 2 - Static Asset Test
```

Green returned:

```text
Assignment 2 - Version 2
```

The ALB was ultimately configured to send 100% of traffic to Green before cleanup.

### Screenshots

![Blue and Green environments](screenshots/blue-green-instances.png)

![Blue target group](screenshots/blue-target-group.png)

![Green target group healthy](screenshots/green-target-group.png)

![ALB listener traffic switch](screenshots/blue-green-alb-switch.png)

![ALB serving Green v2](screenshots/blue-green-v2-response.png)

---

## 4. Canary Deployment

### Concept

Canary deployment sends a small percentage of traffic to a selected version while most traffic continues to use the stable version. The deployment can be evaluated before increasing traffic to the selected version.

### Implementation

Used the ALB's weighted forwarding action to split traffic between the two target groups:

| Target group | Version | Weight |
|---|---|---:|
| `Assignment2-Green-TG` | v2 | 90 |
| `Assignment2-Blue-TG` | v1 | 10 |

Sent 20 HTTP requests through the ALB and observed responses from both versions. The sample returned 19 v2 responses and 1 v1 response. Weighted routing is probabilistic, so a small sample is not expected to match the configured percentage exactly.

After the test, traffic was returned to **100% Green (v2)**.

> Scope note: this exercise demonstrated weighted routing and functional HTTP verification. A full CloudWatch-based performance monitoring and log/metric export pipeline to S3 was not implemented.

### Screenshots

![Canary weighted routing 90/10](screenshots/canary-weighted-routing.png)

![Canary repeated HTTP requests](screenshots/canary-http-test.png)

![Canary final Green 100 percent](screenshots/canary-final-green.png)

---

## 5. A/B Deployment — Research

A/B deployment runs two variants and directs different users or user groups to each variant to compare outcomes such as engagement, conversion, error rate, or performance.

### A/B vs. Canary

| A/B deployment | Canary deployment |
|---|---|
| Focuses on comparing outcomes between variants | Focuses on reducing risk while rolling out a version |
| Traffic/user groups are selected for comparison | A small traffic share is directed to the candidate version |
| May keep both variants active during evaluation | Traffic typically increases to the candidate version after successful evaluation |

The assignment listed A/B as a strategy to explore but did not provide a separate detailed implementation checklist. This section documents the research; a dedicated A/B experiment was not implemented.

---

## 6. S3 Artifact and Static Asset Management

The S3 bucket used during the exercise was:

`spring3hibernate-deployment-syed`

It contained the following objects:

```text
artifacts/
├── Spring3HibernateApp.war
└── Spring3HibernateApp-v2.war

assets/
└── version.txt
```

The EC2 instance role `spring3-ec2-ssm-role` was used to provide AWS access without storing long-lived access keys on the instance.

The bucket was versioned during the exercise. **The bucket has since been deleted as part of cleanup**, so the paths above document the original layout and are not currently available.

### Screenshots

![S3 artifacts](screenshots/s3-artifacts.png)

![S3 assets](screenshots/s3-assets.png)

![EC2 IAM role access to S3](screenshots/ec2-s3-access.png)

---

## 7. Cleanup

After capturing evidence, the following Assignment 2 resources were cleaned up:

- EC2 instances: terminated
- Auto Scaling Group: deleted
- Application Load Balancer: deleted
- Blue and Green target groups: deleted
- Rolling Launch Templates: deleted
- AMI: deregistered
- S3 bucket: deleted

This cleanup was performed to avoid leaving unnecessary AWS resources running and incurring ongoing charges.

---

## 8. Summary

| Strategy / requirement | Result |
|---|---|
| Recreate deployment | Implemented and verified |
| Rolling deployment | Implemented and verified using ASG Instance Refresh |
| Blue-Green deployment | Implemented and verified using ALB target groups |
| Canary deployment | Demonstrated with 90/10 weighted routing |
| A/B deployment | Researched and documented; not separately implemented |
| S3 deployment artifacts | Demonstrated; bucket later deleted |
| S3 static asset integration | Demonstrated; bucket later deleted |
| AWS cleanup | Completed |

## Screenshots Directory

Create a `screenshots/` folder in the repository and save your captured screenshots using the filenames referenced above. If a screenshot is not available, remove its image line or replace it with the correct filename.

Suggested repository layout:

```text
assignment-2/
├── README.md
└── screenshots/
    ├── recreate-ec2.png
    ├── recreate-ami.png
    ├── s3-static-asset.png
    ├── recreate-app-response.png
    ├── rolling-asg.png
    ├── rolling-launch-templates.png
    ├── rolling-instance-refresh.png
    ├── rolling-v2-response.png
    ├── blue-green-instances.png
    ├── blue-target-group.png
    ├── green-target-group.png
    ├── blue-green-alb-switch.png
    ├── blue-green-v2-response.png
    ├── canary-weighted-routing.png
    ├── canary-http-test.png
    ├── canary-final-green.png
    ├── s3-artifacts.png
    ├── s3-assets.png
    └── ec2-s3-access.png
```
