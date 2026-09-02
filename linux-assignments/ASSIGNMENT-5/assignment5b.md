# Linux Assignment 5B – Text Editor Utility

## Objective

Create a Bash-based text editor utility that can perform different text and file editing operations from the command line.

## Script

```bash
assignment5b.sh
```

## Syntax

```bash
./assignment5b.sh <command> <file> [arguments]
```


## Usage Examples

### Add Line at Top

```bash
./assignment5b.sh addLineTop test.txt "First line"
```

### Add Line at Bottom

```bash
./assignment5b.sh addLineBottom test.txt "Last line"
```

### Add Line at Specific Position

```bash
./assignment5b.sh addLineAt test.txt 3 "Inserted line"
```

### Update First Word

```bash
./assignment5b.sh updateFirstWord test.txt Linux Ubuntu
```

### Update All Words

```bash
./assignment5b.sh updateAllWords test.txt Linux Unix
```

### Insert Word

```bash
./assignment5b.sh insertWord test.txt Bash is very
```

This changes:

```text
Bash is powerful
```

to:

```text
Bash very is powerful
```

### Delete Line

```bash
./assignment5b.sh deleteLine test.txt 3
```

### Delete Lines Containing a Word

```bash
./assignment5b.sh deleteLineWord test.txt Docker
```

## Custom Features

### Backup File

Creates a backup of the target file.

```bash
./assignment5b.sh backupFile test.txt
```

Creates:

```text
test.txt.bak
```

### Empty File

Removes all contents from the file without deleting the file.

```bash
./assignment5b.sh emptyFile test.txt
```

## Verification

Make the script executable:

```bash
chmod +x assignment5b.sh
```

Create a test file:

```bash
cat > test.txt <<'EOF'
Linux is powerful
Linux is flexible
Bash is powerful
Docker is useful
Linux and Bash are important
EOF
```

Verify:

```bash
cat -n test.txt
```

Each command can then be tested using the examples above.

## Technologies Used

* Linux
* Bash Shell
* `sed`
* `cp`
* Shell scripting

## Author

Linux Assignment – 5B
