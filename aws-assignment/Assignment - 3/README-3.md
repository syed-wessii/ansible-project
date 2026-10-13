# Assignment 3: Nginx High Availability, Auto Scaling, and Disaster Recovery on AWS

## Overview

This project demonstrates an AWS-based Nginx middleware architecture designed to improve application availability, handle traffic spikes, support version changes, and provide a foundation for disaster recovery.

The implementation covers Nginx AMI versioning, an Application Load Balancer (ALB), an Auto Scaling Group (ASG), scaling policies, S3-based website assets, IAM access controls, path-based routing, and CloudFront content delivery.

## Objectives

- Configure Nginx as a reverse-proxy/web-serving middleware layer.
- Create versioned Amazon Machine Images (AMIs) for Nginx.
- Distribute traffic through an Application Load Balancer.
- Configure an Auto Scaling Group to maintain the desired EC2 capacity.
- Configure scaling policies based on CPU utilization, network traffic, and ALB request count per target.
- Practice version upgrades, rolling deployments, and rollback to a previous AMI.
- Host a webpage using Nginx and serve image assets from Amazon S3.
- Validate instance replacement and self-healing behavior.
- Route requests to different Nginx servers using ALB path-based listener rules.
- Apply IAM and S3 bucket policies to control access to production and non-production objects.
- Use CloudFront to deliver website images through a CDN.

## Architecture

```text
                         Clients
                            |
                       Application
                      Load Balancer
                            |
               +------------+------------+
               |                         |
          Target Group 1            Target Group 2
               |                         |
       Private Nginx EC2-1       Private Nginx EC2-2
         Path: /ninja1             Path: /ninja2
               |                         |
               +------------+------------+
                            |
                    Amazon S3 Assets
                            |
                       CloudFront
```

For the high-availability deployment, the ALB distributes requests to targets managed by an ASG. The ASG uses a launch template that references a versioned Nginx AMI and maintains the configured desired capacity across Availability Zones. A bastion host provides controlled administrative access to private instances.

## AWS Services Used

- Amazon EC2
- Amazon Machine Images (AMIs)
- Application Load Balancer (ALB)
- Target Groups and Listener Rules
- Auto Scaling Groups and Launch Templates
- CloudWatch metrics and scaling policies
- Amazon VPC, public/private subnets, and security groups
- Bastion host
- Amazon S3 and AWS CLI
- AWS IAM users, roles, and policies
- Amazon CloudFront
- Git-based version control

## Implementation Summary

### Day 1 — Nginx AMIs, High Availability, and Auto Scaling

- Installed and configured Nginx on an EC2 instance.
- Created versioned AMIs for Nginx V1 and V2.
- Launched instances from the versioned AMIs.
- Configured an ALB and connected it to the application targets.
- Configured an ASG using a launch template, with desired capacity and scaling limits.
- Added scaling policies based on:
  - Average CPU utilization
  - Network traffic
  - ALB request count per target
- Planned and validated version deployment and rollback using the previous AMI.
- Used CloudWatch metrics to observe instance health and scaling behavior.

### Day 2 — Website Hosting and S3 Assets

- Retrieved website content from a Git repository on an EC2 instance.
- Uploaded image assets to an S3 bucket using the AWS CLI.
- Configured Nginx to serve a webpage containing images hosted in S3.
- Used an EC2 IAM role for AWS access rather than embedding access keys or secret keys.

### Day 3 — Auto Scaling Self-Healing

- Tested the behavior of an unhealthy or failed instance.
- Verified that the ASG can replace unhealthy instances and work toward maintaining the configured desired capacity.
- Reviewed instance health and ASG activity during recovery.

### Day 4 — Bastion Host and Path-Based Routing

- Used a bastion host in a public subnet for controlled SSH access.
- Placed Nginx application instances in private subnets.
- Restricted SSH access to the bastion host and limited HTTP access to the ALB.
- Configured separate target groups for the two Nginx servers.
- Configured ALB listener rules:
  - `/ninja1` routes to the first Nginx server and displays Image-1.
  - `/ninja2` routes to the second Nginx server and displays Image-2.
- Uploaded updated website images to designated S3 folders from an EC2 instance.

### Day 5 — IAM and S3 Access Restrictions

- Created an S3 bucket with `prod` and `nonprod` prefixes.
- Uploaded different image assets to each prefix.
- Configured an IAM role for the required S3 access.
- Applied IAM and bucket policies to control access to the bucket and its objects.
- Restricted the IAM user's access to production objects while allowing access to non-production objects.
- Kept access limited to the intended principals.

### Day 6 — CloudFront and IAM Trust Relationships

- Configured CloudFront to deliver website images through a CDN.
- Set up the required relationship between the CloudFront service and the IAM role/policy configuration.
- Reused the intended role and permissions without unnecessarily broadening access.
- Applied least-privilege IAM permissions for administrative tasks.

## Screenshots

Add your screenshots to the repository (for example, in a folder named `screenshots/`) and replace the placeholders below with the corresponding image paths.

### 1. EC2 Instances and Nginx Setup

<img width="1772" height="887" alt="image" src="https://github.com/user-attachments/assets/a3c98e64-afdf-4b01-b21b-7399ae45b010" />


### 2. Nginx AMI — V1

<img width="1773" height="887" alt="image" src="https://github.com/user-attachments/assets/5f1b6270-81e0-4b0e-bbe2-2dde69494036" />

### 3. Nginx AMI — V2

<img width="1773" height="887" alt="image" src="https://github.com/user-attachments/assets/c0581722-6e2e-454e-9784-a8878b148b39" />

### 4. Application Load Balancer

![Application Load Balancer](screenshots/04-alb.png)

### 5. Auto Scaling Group and Healthy Instances

<img width="1773" height="887" alt="image" src="https://github.com/user-attachments/assets/7def027d-52d7-4bbe-bb4d-b5bda11d4bdf" />

### 6. Auto Scaling Policies

<img width="1768" height="890" alt="image" src="https://github.com/user-attachments/assets/105696dc-3351-4ad1-ba36-48e92e516b54" />

![Network scaling policy](screenshots/07-scaling-policy-network.png)

![ALB request-count scaling policy](screenshots/08-scaling-policy-alb-requests.png)

### 7. Load Test and CloudWatch Metrics

![Load test and CloudWatch metrics](screenshots/09-load-test-cloudwatch.png)

### 8. V1/V2 Deployment and Rollback

<img width="1773" height="887" alt="image" src="https://github.com/user-attachments/assets/231e4d1f-8fe9-418a-9e39-8d0e0f815285" />

<img width="1771" height="888" alt="image" src="https://github.com/user-attachments/assets/756cbb07-69c8-407f-aa05-42f9a92dd180" />



## Validation Checklist

- [ ] Nginx V1 and V2 AMIs are available.
- [ ] ALB routes requests to healthy targets.
- [ ] ASG maintains the configured desired capacity.
- [ ] CPU, network, and ALB request-count scaling policies are configured and tested.
- [ ] Version upgrade and rollback are validated.
- [ ] Website content is retrieved from Git and image assets are uploaded to S3.
- [ ] Website displays images from S3/CloudFront.
- [ ] ASG replaces unhealthy instances.
- [ ] SSH and HTTP access are restricted using security groups.
- [ ] `/ninja1` and `/ninja2` route to their respective target groups.
- [ ] IAM and S3 policies enforce the required `prod`/`nonprod` access restrictions.
- [ ] CloudFront serves the intended image assets.
- [ ] Temporary AWS resources are reviewed and cleaned up when no longer needed.

## Security Notes

- Do not commit AWS access keys, secret keys, private keys, or credentials to Git.
- Prefer IAM roles and temporary credentials for EC2-based AWS CLI operations.
- Restrict SSH access to the administrator's public IP on the bastion host.
- Permit SSH to private Nginx instances only from the bastion security group.
- Allow application HTTP traffic to Nginx instances only from the ALB security group.
- Apply least-privilege IAM policies and validate both allowed and denied S3 access.
- Review AWS resources after testing to avoid unexpected charges.

## Cleanup

After capturing the required evidence, review and remove temporary resources that are no longer required, including test EC2 instances, Auto Scaling Groups, load balancers, target groups, CloudFront distributions, and NAT Gateways where applicable. Retain any AMIs or S3 objects needed for submission.

## Author

**Syed**
