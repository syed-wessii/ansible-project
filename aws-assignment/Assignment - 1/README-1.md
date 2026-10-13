# AWS High Availability Web Application Deployment

## Overview

This project deploys the **Spring3Hibernate** Java web application on
AWS using an internet-facing Application Load Balancer (ALB), an Auto
Scaling Group (ASG), private EC2 instances, and a VPC with public and
private subnets.

The infrastructure was configured and tested in **US East (N. Virginia)
--- `us-east-1`**. The application was successfully accessible through
the ALB DNS name. After testing, the assignment resources were deleted
to avoid ongoing AWS charges.

> **Repository:** `https://github.com/opstree/spring3hibernate`

## Objectives

-   Build and deploy a Java WAR application.
-   Place application instances in private subnets.
-   Route public HTTP traffic through an internet-facing ALB.
-   Distribute requests across instances registered with a target group.
-   Use an ASG to maintain the desired number of application instances
    across two Availability Zones.
-   Validate the deployment and clean up billable resources after
    testing.

## Architecture

The intended request flow is:

``` text
Client / Browser
       |
       | HTTP :80
       v
Internet-facing Application Load Balancer
       |
       v
ALB Target Group (HTTP :8080)
       |
       +--------------------+
       |                    |
       v                    v
Private EC2 Instance 1   Private EC2 Instance 2
(AZ us-east-1a)          (AZ us-east-1b)
       |                    |
       +---------+----------+
                 |
       Spring3Hibernate application
       Tomcat 9 + Java 11
       Local MariaDB on each instance
```

The ALB was configured in two public subnets. The Auto Scaling Group
used two private subnets across two Availability Zones. A NAT Gateway
provided outbound internet access for private instances during package
installation and application setup.


## AWS Resources and Configuration

  -----------------------------------------------------------------------
  Component                           Configuration
  ----------------------------------- -----------------------------------
  AWS Region                          `us-east-1`

  VPC                                 `spring3-vpc`, CIDR `10.0.0.0/16`

  Public subnets                      Two public subnets across
                                      `us-east-1a` and `us-east-1b`

  Private subnets                     Two private subnets across
                                      `us-east-1a` and `us-east-1b`

  Internet Gateway                    `spring3-igw`

  NAT Gateway                         `spring3-nat-1`

  Application Load Balancer           `spring3-alb`, internet-facing,
                                      HTTP port 80

  Target Group                        `spring3-tg`, HTTP port 8080,
                                      health check path `/`

  Auto Scaling Group                  `spring3-asg`, minimum 2, desired
                                      2, maximum 4

  Launch Template                     `spring3-launch-template`;
                                      corrected configuration used
                                      version 5

  EC2 instance type                   `t3.micro`

  Operating system                    Ubuntu 24.04 LTS

  Java                                OpenJDK 11

  Application server                  Apache Tomcat 9

  Database                            MariaDB

  Application                         Spring3Hibernate WAR
  -----------------------------------------------------------------------

## Network and Security

-   The VPC used the CIDR block `10.0.0.0/16`.
-   Public subnets used a route to the Internet Gateway.
-   Private subnets used a default route through the NAT Gateway for
    outbound access.
-   The ALB security group allowed inbound HTTP traffic on port `80`.
-   The EC2 security group allowed application traffic on port `8080`
    from the ALB security group.
-   SSH access was restricted to the configured client IP where
    applicable.
-   The application instances did not require public IPv4 addresses.

## Application Deployment

The EC2 launch template User Data automated the setup process on new
instances:

1.  Updated the package index and installed Git, Maven, OpenJDK 11,
    MariaDB, and `wget`.
2.  Started MariaDB and created the `employeedb` database.
3.  Cloned the Spring3Hibernate repository.
4.  Updated the application's database URL to use local MariaDB.
5.  Updated the Maven compiler source and target settings from Java 6 to
    Java 8 compatibility so the legacy project could build on the
    installed Java 11 JDK.
6.  Built the WAR file with Maven, skipping tests.
7.  Installed Apache Tomcat 9.
8.  Deployed `Spring3HibernateApp.war` as `ROOT.war`.
9.  Configured Tomcat as a systemd service and started it.

The application was verified through the ALB DNS name and displayed the
**Sample WebApp CRUD Example for CI** page with links for listing
employees, adding an employee, uploading a file, and listing images.

## Load Balancer and Auto Scaling Validation

-   The ALB was active and accepted HTTP requests.
-   The target group used HTTP port `8080` and the `/` health-check
    path.
-   The ASG was configured across two Availability Zones.
-   The corrected launch-template configuration was used to replace
    older instances through an instance refresh.
-   The ASG reached its desired capacity with **2 of 2 instances
    healthy**.
-   The ALB successfully routed requests to the deployed application.

### Screenshot Evidence

Add screenshots to the `screenshots/` folder and update the filenames
below as needed.

#### 1. VPC and Subnets

```{=html}
<!-- Screenshot: VPC details showing CIDR and subnets in two AZs. -->
```
<img width="1919" height="660" alt="image" src="https://github.com/user-attachments/assets/634624e2-3a89-4074-9651-b379d55f795a" />

<img width="1919" height="660" alt="image" src="https://github.com/user-attachments/assets/fdd4e03f-d127-4f6a-8e31-36aef81d09e9" />



#### 2. Route Tables and Gateways

```{=html}
<!-- Screenshot: Public route to IGW and private route to NAT Gateway. -->
```
<img width="1919" height="427" alt="image" src="https://github.com/user-attachments/assets/dfbaaec1-b546-4a83-8275-5b79f21b761a" />

<img width="1919" height="640" alt="image" src="https://github.com/user-attachments/assets/60807e29-2321-4050-b058-f2f9c6d7b34b" />



#### 3. Security Groups

```{=html}
<!-- Screenshot: ALB inbound HTTP rule and EC2 port 8080 rule sourced from the ALB security group. -->
```
<img width="1918" height="715" alt="image" src="https://github.com/user-attachments/assets/59709cd9-6805-4ff0-9ceb-8ec664c9b941" />


#### 4. Application Load Balancer

```{=html}
<!-- Screenshot: ALB showing Active state and Internet-facing scheme. -->
```
<img width="1919" height="883" alt="image" src="https://github.com/user-attachments/assets/99ead9a5-3de7-439f-b40c-8c1f258302fe" />

#### 5. Target Group Health

```{=html}
<!-- Screenshot: Target group showing healthy registered targets. -->
```
<img width="1526" height="569" alt="image" src="https://github.com/user-attachments/assets/b8cc1d9c-18ec-43e3-b328-d914f4098714" />


#### 6. Launch Template

```{=html}
<!-- Screenshot: Launch template details and the User Data configuration. -->
```
<img width="1919" height="756" alt="image" src="https://github.com/user-attachments/assets/2afbdd0a-6321-4d12-9bea-9beedaa0f531" />


#### 7. Auto Scaling Group

```{=html}
<!-- Screenshot: ASG showing desired capacity 2 and 2/2 healthy instances. -->
```
<img width="1916" height="714" alt="image" src="https://github.com/user-attachments/assets/855cdf5d-91ab-4e35-baa6-527bc5aaa13b" />



#### 8. Application in Browser

```{=html}
<!-- Screenshot: Application homepage opened using the ALB DNS name. -->
```
![Application Homepage](screenshots/application-homepage.png)

<img width="1919" height="519" alt="image" src="https://github.com/user-attachments/assets/cc0b6659-0329-4ea7-bf7d-c79ce702c12a" />


## Challenges and Resolutions

### 1. Legacy Maven compiler settings

**Issue:** The original project configured Java source and target
version `1.6`, which is not supported by the Java 11 compiler.

**Resolution:** Updated the Maven compiler settings to source and target
`1.8`.

### 2. Invalid dependency version

**Issue:** Maven could not resolve `commons-collections:3.4.0` from
Maven Central.

**Resolution:** Changed the dependency version to `3.2.1`, which
resolved successfully.

### 3. Launch-time application setup

**Issue:** Instances launched from the earlier User Data configuration
did not finish application setup because the Maven build failed.

**Resolution:** Corrected the build configuration in the launch
template, created a new version, and used an ASG instance refresh to
replace the older instances.

## Cleanup and Cost Management

After validating the application, the Auto Scaling Group and related
assignment resources were removed. The custom VPC deletion confirmation
reported that `spring3-vpc` and 10 associated resources had been
deleted.

The default AWS VPC was left intact.

**Important:** The infrastructure is documented here as the completed
deployment design; the assignment resources were cleaned up afterward
and are not currently running. Screenshots should be captured from
existing evidence where available. Do not recreate billable resources
just to obtain screenshots.

## Key Learnings

-   VPC design with public and private subnets across multiple
    Availability Zones.
-   Internet Gateway and NAT Gateway routing.
-   Security-group-based traffic control between the ALB and private
    instances.
-   ALB listeners, target groups, and health checks.
-   Launch Templates, User Data, and Auto Scaling Groups.
-   Rolling replacement using an ASG instance refresh.
-   Troubleshooting legacy Maven builds on a modern JDK.
-   Verifying application availability through an ALB DNS endpoint.
-   Cleaning up AWS resources to control costs.

## Suggested Repository Structure

``` text
.
├── README.md
└── screenshots/
    ├── architecture.png
    ├── vpc-subnets.png
    ├── routes-gateways.png
    ├── security-groups.png
    ├── alb.png
    ├── target-group-health.png
    ├── launch-template.png
    ├── asg-healthy.png
    ├── instance-refresh.png
    ├── application-homepage.png
    └── cleanup-confirmation.png
```

Create the `screenshots/` directory in your GitHub repository and add
your screenshots using the filenames above. If a screenshot is not
available, remove that image line or leave the placeholder comment until
you add it.
