# Git Assignment 7D

## Git Commit Report Utility

This assignment implements a Bash script to generate a commit report for a Git repository.

### Script

```bash
assignment7d.sh
```

## Features

The script accepts:

* Git repository URL
* Number of days for which the commit report should be generated

It generates the report in **CSV format**.

The report contains:

* Commit ID
* Author Name
* Author Email
* Commit Message
* Changed Files
* Valid

## Usage

Make the script executable:

```bash
chmod +x assignment7d.sh
```

Run the script using:

```bash
./assignment7d.sh -u <repo_url> -d <days>
```

Example:

```bash
./assignment7d.sh -u https://github.com/opstree/spring3hibernate.git -d 1500
```

## Output

The script generates:

```text
git_commit_report.csv
```

View the report using:

```bash
cat git_commit_report.csv
```

For easier terminal viewing:

```bash
column -s ',' -t < git_commit_report.csv
```

## Valid Commit Check

The script also checks whether a commit message follows the required Jira format:

```text
JIRA-XXXX:
```

Example of a valid commit message:

```text
JIRA-1234: Fix login issue
```

Such commits are marked:

```text
Yes
```

Commits that do not follow the pattern are marked:

```text
No
```

## Example Report

```text
Commit ID,Author Name,Author Email,Commit Message,Changed Files,Valid
82d59771...,Sandeep,sandeep@opstree.com,Updated path to correct value,terraform/network_skeleton/terraform.tfvars,No
```

## Result

The utility successfully clones the specified repository and generates a CSV commit report containing commit details, author information, changed files, and commit-message validity.
