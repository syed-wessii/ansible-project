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
<img width="900" height="130" alt="image" src="https://github.com/user-attachments/assets/15dd46e3-60b5-4dc4-8740-0cf5146348dc" />


```bash
./assignment7b.sh -l
```

Lists all branches in the current Git repository.

### 2. Create Branch
<img width="900" height="47" alt="image" src="https://github.com/user-attachments/assets/88058c97-4cf5-46ef-b179-4e9959d2c657" />


```bash
./assignment7b.sh -b <branch_name>
```

Example:

```bash
./assignment7b.sh -b testbranch
```

Creates a new Git branch.

### 3. Delete Branch
<img width="900" height="70" alt="image" src="https://github.com/user-attachments/assets/93326d95-bcd7-43bd-9316-65a04279a2a4" />


```bash
./assignment7b.sh -d <branch_name>
```

Example:

```bash
./assignment7b.sh -d testbranch
```

Deletes an existing branch.

### 4. Merge Two Branches
<img width="900" height="187" alt="image" src="https://github.com/user-attachments/assets/240e057e-cb51-4e8a-88d5-a4b730a94da2" />


```bash
./assignment7b.sh -m -1 <branch_name1> -2 <branch_name2>
```

Example:

```bash
./assignment7b.sh -m -1 ninja -2 master
```

This switches to `master` and merges the `ninja` branch into it.

### 5. Rebase Two Branches
<img width="900" height="183" alt="image" src="https://github.com/user-attachments/assets/49444bbb-5996-46b7-aceb-72ba5380a6d7" />


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
