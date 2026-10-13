# Assignment 4 --- Terraform Infrastructure as Code (IaC)

## Objective

Provision AWS infrastructure using Terraform, manage Terraform state
remotely in Amazon S3, and verify that an application is reachable
through an Application Load Balancer (ALB).

## Architecture

The infrastructure was provisioned in the AWS `ap-south-1` (Mumbai)
region.

``` text
Internet
   |
Application Load Balancer (public subnets)
   |
Target Group + HTTP Listener
   |
Auto Scaling Group
   |
EC2 instances in private subnets
   |
Apache HTTP Server
```

Networking includes a VPC, public and private subnets, an Internet
Gateway, route tables, a NAT Gateway, and security groups.

## AWS Resources

-   VPC and subnets
-   Internet Gateway and NAT Gateway
-   Public and private route tables and subnet associations
-   Security groups for the ALB and EC2 instances
-   Application Load Balancer
-   Target group and HTTP listener
-   EC2 launch template using Amazon Linux 2023
-   Auto Scaling Group (`min: 2`, `desired: 2`, `max: 4`)
-   Amazon S3 bucket for Terraform remote state
-   S3 bucket versioning
-   S3-native Terraform state locking using `use_lockfile = true`

The EC2 launch template installs Apache (`httpd`) and serves the page:

`Assignment 4 - Terraform`

## Terraform Files

  -----------------------------------------------------------------------
  File                                Purpose
  ----------------------------------- -----------------------------------
  `provider.tf`                       AWS provider version, region, and
                                      S3 backend configuration

  `vpc.tf`                            VPC, subnets, gateways, and routing

  `security.tf`                       ALB and EC2 security groups

  `alb.tf`                            ALB, target group, and HTTP
                                      listener

  `asg.tf`                            Launch template and Auto Scaling
                                      Group

  `variables.tf`                      Input variables

  `outputs.tf`                        ALB DNS output
  -----------------------------------------------------------------------

Terraform's dependency lock file, `.terraform.lock.hcl`, records the
selected provider version. Commit this file to GitHub.

## Prerequisites

-   Terraform CLI
-   AWS CLI
-   An AWS account and IAM credentials with permissions required to
    manage the resources
-   Git

Configure AWS credentials locally; **never commit credentials or secret
keys**.

``` bash
aws configure
aws sts get-caller-identity
```

## Deployment

Run these commands from the `assignment-4` directory.

``` bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
```

After applying, retrieve the ALB DNS name:

``` bash
terraform output alb_dns_name
```

Open the resulting address using HTTP:

``` text
http://<alb_dns_name>
```

The expected page content is:

``` text
Assignment 4 - Terraform
```

## Remote State

The Terraform backend stores the state file in an S3 bucket with
versioning enabled. S3-native state locking is configured through
`use_lockfile = true`.

Example verification command:

``` bash
aws s3 ls s3://<your-state-bucket>/<your-state-key-prefix>/
```

Do not commit `terraform.tfstate`, state backups, AWS credentials, or
`.terraform/` to the repository.

## Validation Results

-   `terraform fmt` completed.
-   `terraform validate` succeeded.
-   `terraform plan` reported no changes after deployment.
-   The application was verified through the ALB DNS name.
-   The Terraform state file was verified in S3.
-   `terraform destroy` completed successfully and reported **21
    resources destroyed**.

**Current status:** The billable application infrastructure has been
destroyed to avoid ongoing charges. The Terraform code remains available
locally. The S3 state bucket was intentionally retained; S3 storage may
still incur a small charge.

## Screenshots

Add your evidence images to the `screenshots/` directory and update the
paths below if you use different filenames.

### 1. Application accessible through the ALB

Shows the ALB DNS in the browser and the `Assignment 4 - Terraform`
page.

<img width="1914" height="604" alt="image" src="https://github.com/user-attachments/assets/e3577715-1910-4a2d-8df1-ec518bac552f" />

### 2. Terraform plan --- no changes

Shows Terraform confirming that the deployed infrastructure matched the
configuration.

<img width="1710" height="839" alt="image" src="https://github.com/user-attachments/assets/a329a399-fccf-42b8-9115-5233124f3ce8" />


### 3. Terraform state stored in S3

Shows `terraform.tfstate` listed in the S3 backend path.

<img width="1708" height="102" alt="image" src="https://github.com/user-attachments/assets/4c4e1655-cdbe-484d-8049-eef9fa3ad720" />

### 4. Terraform destroy completed

Shows the final cleanup result:
`Destroy complete! Resources: 21 destroyed.`

<img width="1856" height="1041" alt="image" src="https://github.com/user-attachments/assets/0dc071fe-228d-4475-b024-e2466e5f757f" />

## Repository Structure

``` text
assignment-4/
├── alb.tf
├── asg.tf
├── outputs.tf
├── provider.tf
├── security.tf
├── variables.tf
├── vpc.tf
├── .terraform.lock.hcl
├── README.md
└── screenshots/
    ├── 01-application-alb.png
    ├── 02-terraform-plan.png
    ├── 03-s3-terraform-state.png
    └── 04-terraform-destroy.png
```

Keep the screenshot filenames consistent with the Markdown links above.
Do not upload credentials, private keys, or Terraform state files to
GitHub.
