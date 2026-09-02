# Git Assignment 7B

## Git Branch Management Utility

This assignment implements a Bash script to manage Git branches using command-line options.

### Script

```bash
assignment7b.sh
```

## Features

The script supports the following operations:

### 1. List Branches

```bash
./assignment7b.sh -l
```

Lists all branches in the current Git repository.

### 2. Create Branch

```bash
./assignment7b.sh -b <branch_name>
```

Example:

```bash
./assignment7b.sh -b testbranch
```

Creates a new Git branch.

### 3. Delete Branch

```bash
./assignment7b.sh -d <branch_name>
```

Example:

```bash
./assignment7b.sh -d testbranch
```

Deletes an existing branch.

### 4. Merge Two Branches

```bash
./assignment7b.sh -m -1 <branch_name1> -2 <branch_name2>
```

Example:

```bash
./assignment7b.sh -m -1 ninja -2 master
```

This switches to `master` and merges the `ninja` branch into it.

### 5. Rebase Two Branches

```bash
./assignment7b.sh -r -1 <branch_name1> -2 <branch_name2>
```

Example:

```bash
./assignment7b.sh -r -1 ninja -2 master
```

This switches to `ninja` and rebases it onto `master`.

## Usage

First make the script executable:

```bash
chmod +x assignment7b.sh
```

Then run the required Git branch operation using the supported options.

## Result

The utility provides a simple command-line interface for:

* Listing branches
* Creating branches
* Deleting branches
* Merging branches
* Rebasing branches
