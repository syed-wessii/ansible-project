# Assignment 5 --- Terraform Modules & Remote State Management

## Overview

This assignment demonstrates how to organize Terraform infrastructure as
reusable modules and how to configure remote Terraform state management
on AWS.

**Status:** Infrastructure was deployed and verified successfully. AWS
resources created for testing were subsequently destroyed, and the
Assignment 5 S3 state bucket and DynamoDB lock table were removed during
cleanup.

## Objectives

-   Organize infrastructure into reusable Terraform modules.
-   Provision an AWS VPC, subnet, security group, and EC2 instance.
-   Validate and review the Terraform execution plan before deployment.
-   Configure an S3 backend for remote Terraform state.
-   Configure DynamoDB state locking as required by the assignment.
-   Verify the deployment through Terraform CLI, AWS CLI, and the AWS
    Console.

## Tools and Services

-   Terraform
-   AWS CLI
-   Amazon VPC
-   Amazon EC2
-   Amazon S3
-   Amazon DynamoDB
-   Ubuntu 24.04 AMI
-   AWS Region: `ap-south-1` (Asia Pacific --- Mumbai)

## Repository Structure

``` text
assignment-5/
├── main.tf
├── variables.tf
├── outputs.tf
├── providers.tf
├── backend.tf
├── .terraform.lock.hcl
└── modules/
    ├── vpc/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    ├── subnet/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    ├── security_group/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    └── instance/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

> Do not commit credentials, private keys, Terraform state files, or
> other secrets. The `.terraform/` directory and local state files
> should generally be excluded from version control.

## Architecture

``` text
                    Root Terraform Configuration
                               |
               +---------------+---------------+
               |               |               |
           VPC Module     Security Group   Subnet Module
                               |               |
                               +-------+-------+
                                       |
                                  EC2 Module

Remote state configuration (used during the assignment):
Terraform state -> Amazon S3
State-lock configuration -> Amazon DynamoDB
```

## Modules

  -----------------------------------------------------------------------
  Module                              Responsibility
  ----------------------------------- -----------------------------------
  `modules/vpc`                       Creates the VPC and exports its ID
                                      and CIDR block.

  `modules/subnet`                    Creates a subnet in the supplied
                                      VPC and exports its ID and CIDR
                                      block.

  `modules/security_group`            Creates a security group with
                                      configurable ingress rules and
                                      outbound access.

  `modules/instance`                  Creates an EC2 instance using the
                                      supplied AMI, subnet, security
                                      group, instance type, and key pair.
  -----------------------------------------------------------------------

The root `main.tf` calls the modules and passes outputs between them.
For example, the VPC module's `vpc_id` output is passed to the subnet
and security-group modules.

## Deployment and Verification

The following commands were used during implementation:

``` bash
terraform init
terraform validate
terraform plan
terraform apply
terraform state list
terraform output
terraform plan
```

Expected validation result:

``` text
Success! The configuration is valid.
```

Expected final plan after deployment:

``` text
No changes. Your infrastructure matches the configuration.
```

The Terraform state listed four managed resources:

``` text
module.instance.aws_instance.this
module.security_group.aws_security_group.this
module.subnet.aws_subnet.this
module.vpc.aws_vpc.this
```

## Remote State and Locking

The assignment's remote backend was configured with:

-   **S3 bucket:** `assignment-5-terraform-state-702949239113`
-   **State key:** `assignment-5/terraform.tfstate`
-   **Region:** `ap-south-1`
-   **DynamoDB table:** `assignment-5-terraform-lock`
-   **DynamoDB partition key:** `LockID`

The existing local state was migrated to S3, and the state object was
verified using the AWS CLI. The DynamoDB table was also verified in the
AWS Console.

**Cleanup note:** After verification and screenshot capture, the
Assignment 5 infrastructure was destroyed, the S3 state object and
bucket were deleted, and the DynamoDB table was deleted. The backend
configuration is retained in the project as assignment documentation; it
must be recreated or adjusted before using this configuration for a new
deployment.

**Terraform version note:** The installed Terraform version displayed a
deprecation warning for the S3 backend's `dynamodb_table` argument and
recommended `use_lockfile` for S3-native locking. The DynamoDB setting
was retained during this exercise because DynamoDB locking was
explicitly required by the assignment.

## Cleanup

After collecting verification evidence, the infrastructure was removed
with:

``` bash
terraform destroy
```

The output confirmed:

``` text
Destroy complete! Resources: 4 destroyed.
```

The separately created backend resources were then cleaned up manually.
If you redeploy this project, review the backend configuration and
create the required backend resources before running `terraform init`.

## Screenshots

Create a `screenshots/` directory in this repository and add your saved
evidence using the filenames below. The image placeholders can be
replaced with the actual screenshot files before pushing to GitHub.

### 1. Terraform Project Structure

```{=html}
<!-- Add screenshot: screenshots/01-project-structure.png -->
```
![Terraform project structure](screenshots/01-project-structure.png)

### 2. Root Module Configuration

```{=html}
<!-- Add screenshot: screenshots/02-root-main-tf.png -->
```
![Root main.tf calling the modules](screenshots/02-root-main-tf.png)

### 3. Terraform Validation and Plan

```{=html}
<!-- Add screenshot: screenshots/03-terraform-validate-plan.png -->
```
![Terraform validation and
plan](screenshots/03-terraform-validate-plan.png)

### 4. Terraform Apply Result

```{=html}
<!-- Add screenshot: screenshots/04-terraform-apply.png -->
```
![Terraform apply result](screenshots/04-terraform-apply.png)

### 5. Terraform State List and Outputs

```{=html}
<!-- Add screenshot: screenshots/05-state-list-outputs.png -->
```
![Terraform state list and
outputs](screenshots/05-state-list-outputs.png)

### 6. EC2 Instance --- AWS Console

```{=html}
<!-- Add screenshot: screenshots/06-ec2-console.png -->
```
![EC2 instance in the AWS Console](screenshots/06-ec2-console.png)

### 7. S3 Remote State --- AWS Console

```{=html}
<!-- Add screenshot: screenshots/07-s3-remote-state.png -->
```
![Terraform state object in the S3
bucket](screenshots/07-s3-remote-state.png)

### 8. DynamoDB Lock Table --- AWS Console

```{=html}
<!-- Add screenshot: screenshots/08-dynamodb-lock-table.png -->
```
![DynamoDB lock table in the AWS
Console](screenshots/08-dynamodb-lock-table.png)

### 9. AWS CLI Verification

```{=html}
<!-- Add screenshot: screenshots/09-aws-cli-verification.png -->
```
![AWS CLI verification](screenshots/09-aws-cli-verification.png)

## Key Learnings

-   How to separate Terraform resources into reusable modules.
-   How module inputs and outputs connect infrastructure components.
-   How to use `terraform init`, `validate`, `plan`, `apply`, `output`,
    and `state list`.
-   How Terraform remote state is stored in S3.
-   How state-locking configuration helps coordinate Terraform
    operations.
-   Why backend resources need special consideration during cleanup.

------------------------------------------------------------------------

**Assignment:** Implement Infrastructure with Terraform Modules\
**Region:** AWS Mumbai (`ap-south-1`)
