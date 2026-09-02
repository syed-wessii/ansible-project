# Git Assignment 7C

## Git Tag Management Utility

This assignment implements a Bash script to manage Git tags using command-line options.

### Script

```bash
assignment7c.sh
```

## Features

The script supports the following operations:

### 1. Create Tag

```bash
./assignment7c.sh -t <tag_name>
```

Example:

```bash
./assignment7c.sh -t ninja_1.0
./assignment7c.sh -t ninja_1.1
```

Creates tags for the current commit.

### 2. List Tags

```bash
./assignment7c.sh -l
```

Example output:

```text
ninja_1.0
ninja_1.1
```

### 3. Delete Tag

```bash
./assignment7c.sh -d <tag_name>
```

Example:

```bash
./assignment7c.sh -d ninja_1.0
```

Deletes the specified Git tag.

## Usage

First make the script executable:

```bash
chmod +x assignment7c.sh
```

Create tags:

```bash
./assignment7c.sh -t ninja_1.0
./assignment7c.sh -t ninja_1.1
```

List tags:

```bash
./assignment7c.sh -l
```

Delete a tag:

```bash
./assignment7c.sh -d ninja_1.0
```

Verify the remaining tags:

```bash
./assignment7c.sh -l
```

## Result

The utility provides a simple command-line interface for:

* Creating Git tags
* Listing Git tags
* Deleting Git tags
* Checking whether a tag already exists
* Validating tag operations
