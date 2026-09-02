# Assignment 1B - FileManager.sh

## Objective

Create a Linux shell utility named `FileManager.sh` that performs basic file and directory management operations using Linux commands.

> **Note:** The `sed` command is not used in this assignment, as required.

---


---

## How to Run

Give execute permission to the script:

```bash
chmod +x FileManager.sh
```

Run the utility using:

```bash
./assignment1b.sh <operation> <arguments>
```

---

# Directory Operations

## 1. Create Directory

Creates a directory at the specified location.

### Example

```bash
./assignment1b.sh addDir /tmp dir1
./assignment1b.sh addDir /tmp dir2
./assignment1b.sh addDir /tmp dir3
```

### Verification

```bash
ls -ld /tmp/dir1 /tmp/dir2 /tmp/dir3
```

## 2. Delete Directory

```bash
./assignment1b.sh deleteDir /tmp dir3
```

### Verification

```bash
ls -ld /tmp/dir3
```

## 3. List Files

```bash
./assignment1b.sh listFiles /tmp
```

### Verification

```bash
find /tmp -maxdepth 1 -type f
```

## 4. List Directories

```bash
./assignment1b.sh listDirs /tmp
```

### Verification

```bash
find /tmp -mindepth 1 -maxdepth 1 -type d
```

## 5. List All Contents

```bash
./assignment1b.sh listAll /tmp
```

### Verification

```bash
ls -la /tmp
```

---

# File Operations

## 6. Create File

```bash
./assignment1b.sh addFile /tmp/dir1 file1.txt
```

### Verification

```bash
ls -l /tmp/dir1/file1.txt
```

## 7. Create File With Initial Content

```bash
./assignment1b.sh addFile /tmp/dir1 file1.txt "Initial Content"
```

### Verification

```bash
cat /tmp/dir1/file1.txt
```

## 8. Add Content to File

Adds content to the end of the file.

```bash
./assignment1b.sh addContentToFile /tmp/dir1 file1.txt "Additional Content"
```

### Verification

```bash
cat /tmp/dir1/file1.txt
```

## 9. Add Content at Beginning of File

```bash
./assignment1b.sh addContentToFileBegining /tmp/dir1 file1.txt "Beginning Content"
```

### Verification

```bash
cat /tmp/dir1/file1.txt
```

---

# Display File Content

## 10. Show First N Lines

```bash
./assignment1b.sh showFileBeginingContent /tmp/dir1 file1.txt 5
```

### Verification

```bash
head -n 5 /tmp/dir1/file1.txt
```

## 11. Show Last N Lines

```bash
./assignment1b.sh showFileEndContent /tmp/dir1 file1.txt 5
```

### Verification

```bash
tail -n 5 /tmp/dir1/file1.txt
```

## 12. Show Content of Specific Line

```bash
./assignment1b.sh showFileContentAtLine /tmp/dir1 file1.txt 10
```

### Verification

```bash
head -n 10 /tmp/dir1/file1.txt | tail -n 1
```

## 13. Show Content of Line Range

```bash
./assignment1b.sh showFileContentForLineRange /tmp/dir1 file1.txt 5 10
```

### Verification

```bash
head -n 10 /tmp/dir1/file1.txt | tail -n 6
```

This displays lines **5 through 10**.

---

# File Management

## 14. Move/Rename File

```bash
./assignment1b.sh moveFile /tmp/dir1/file1.txt /tmp/dir1/file2.txt
```

### Verification

```bash
ls -l /tmp/dir1
```

## 15. Move File to Another Directory

```bash
./assignment1b.sh moveFile /tmp/dir1/file2.txt /tmp/dir2/
```

### Verification

```bash
ls -l /tmp/dir2
```

## 16. Copy File

```bash
./assignment1b.sh copyFile /tmp/dir2/file2.txt /tmp/dir1/
```

### Verification

```bash
ls -l /tmp/dir1 /tmp/dir2
```

## 17. Copy File With New Name

```bash
./assignment1b.sh copyFile /tmp/dir1/file2.txt /tmp/dir1/file3.txt
```

### Verification

```bash
ls -l /tmp/dir1
```

## 18. Clear File Content

```bash
./assignment1b.sh clearFileContent /tmp/dir1 file3.txt
```

### Verification

```bash
cat /tmp/dir1/file3.txt
ls -l /tmp/dir1/file3.txt
```

The file should still exist but contain no content.

## 19. Delete File

```bash
./assignment1b.sh deleteFile /tmp/dir1 file2.txt
```

### Verification

```bash
ls -l /tmp/dir1
```

---

# Commands Used

The utility uses basic Linux commands:

```text
mkdir
rm
find
ls
touch
echo
cat
head
tail
mv
cp
```

The `sed` command is **not used**.

---

# Complete Example

```bash
chmod +x FileManager.sh

./assignment1b.sh addDir /tmp dir1
./assignment1b.sh addDir /tmp dir2
./assignment1b.sh addDir /tmp dir3

./assignment1b.sh listFiles /tmp
./assignment1b.sh listDirs /tmp
./assignment1b.sh listAll /tmp

./assignment1b.sh addFile /tmp/dir1 file1.txt "Initial Content"

./assignment1b.sh addContentToFile /tmp/dir1 file1.txt "Additional Content"

./assignment1b.sh addContentToFileBegining /tmp/dir1 file1.txt "Beginning Content"

./assignment1b.sh showFileBeginingContent /tmp/dir1 file1.txt 5

./assignment1b.sh showFileEndContent /tmp/dir1 file1.txt 5

./assignment1b.sh showFileContentAtLine /tmp/dir1 file1.txt 10

./assignment1b.sh showFileContentForLineRange /tmp/dir1 file1.txt 5 10

./assignment1b.sh moveFile /tmp/dir1/file1.txt /tmp/dir1/file2.txt

./assignment1b.sh moveFile /tmp/dir1/file2.txt /tmp/dir2/

./assignment1b.sh copyFile /tmp/dir2/file2.txt /tmp/dir1/

./assignment1b.sh copyFile /tmp/dir1/file2.txt /tmp/dir1/file3.txt

./assignment1b.sh clearFileContent /tmp/dir1 file3.txt

./assignment1b.sh deleteFile /tmp/dir1 file2.txt

./assignment1b.sh deleteDir /tmp dir3
```

---

# Result

The `FileManager.sh` utility performs the required directory and file operations using basic Linux commands without using `sed`.
