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

## 2. Create Directory

<img width="1035" height="207" alt="image" src="https://github.com/user-attachments/assets/d12499e8-0d48-4841-bd00-4e77efa3019f" />


<img width="1035" height="207" alt="image" src="https://github.com/user-attachments/assets/fc190a45-fe45-41ef-9b31-d1fcfe2b3558" />


<img width="1035" height="207" alt="image" src="https://github.com/user-attachments/assets/fcf892f3-834d-4a82-8868-cb91457018bc" />



Creates a directory at the specified location.

### Example

```bash
./assignment1b.sh addDir /tmp dir1
./assignment1b.sh addDir /tmp dir2
./assignment1b.sh addDir /tmp dir3
```


## 3. List Files

<img width="1035" height="126" alt="image" src="https://github.com/user-attachments/assets/44acbb87-49ab-499c-8bf4-1946e7863d9e" />

```bash
./assignment1b.sh listFiles /tmp
```

### Verification

```bash
find /tmp -maxdepth 1 -type f
```

## 4. List Directories

<img width="1035" height="306" alt="image" src="https://github.com/user-attachments/assets/28386e17-c7cc-4042-a8ef-958b8949e29e" />

```bash
./assignment1b.sh listDirs /tmp
```

### Verification

```bash
find /tmp -mindepth 1 -maxdepth 1 -type d
```

## 5. List All Contents

<img width="1035" height="284" alt="image" src="https://github.com/user-attachments/assets/320a733f-5265-406e-b17c-d61136358804" />

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

<img width="1035" height="137" alt="image" src="https://github.com/user-attachments/assets/30ae0bdc-b563-40c1-9096-10486ac38142" />

```bash
./assignment1b.sh addFile /tmp/dir1 file1.txt
```

### Verification

```bash
ls -l /tmp/dir1/file1.txt
```

## 7. Create File With Initial Content

<img width="1035" height="83" alt="image" src="https://github.com/user-attachments/assets/0e969971-9df6-432e-bc89-eba03981be11" />

```bash
./assignment1b.sh addFile /tmp/dir1 file1.txt "Initial Content"
```

### Verification

```bash
cat /tmp/dir1/file1.txt
```

## 8. Add Content to File

<img width="1035" height="131" alt="image" src="https://github.com/user-attachments/assets/e2d40fb4-478c-489d-b585-1ee26420f456" />

Adds content to the end of the file.

```bash
./assignment1b.sh addContentToFile /tmp/dir1 file1.txt "Additional Content"
```

### Verification

```bash
cat /tmp/dir1/file1.txt
```

## 9. Add Content at Beginning of File

<img width="1035" height="127" alt="image" src="https://github.com/user-attachments/assets/98c27ea8-30ea-4de0-af36-46741f56c444" />

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

<img width="1035" height="174" alt="image" src="https://github.com/user-attachments/assets/d974ee19-9f61-4d81-99e5-b40380ff3f6b" />

```bash
./assignment1b.sh showFileBeginingContent /tmp/dir1 file1.txt 5
```

### Verification

```bash
head -n 5 /tmp/dir1/file1.txt
```

## 11. Show Last N Lines

<img width="1035" height="178" alt="image" src="https://github.com/user-attachments/assets/eb3458f0-4f03-423b-b23c-0991852d6622" />

```bash
./assignment1b.sh showFileEndContent /tmp/dir1 file1.txt 5
```

### Verification

```bash
tail -n 5 /tmp/dir1/file1.txt
```

## 12. Show Content of Specific Line

<img width="1035" height="93" alt="image" src="https://github.com/user-attachments/assets/9079cc35-e37b-4a9b-be37-d86850814b82" />

```bash
./assignment1b.sh showFileContentAtLine /tmp/dir1 file1.txt 10
```

### Verification

```bash
head -n 10 /tmp/dir1/file1.txt | tail -n 1
```

## 13. Show Content of Line Range

<img width="1035" height="201" alt="image" src="https://github.com/user-attachments/assets/5018dc3b-7a62-4348-8d4d-9ee43d1aeed1" />

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

<img width="1035" height="107" alt="image" src="https://github.com/user-attachments/assets/d997433c-a2b6-4151-bfd8-0f31c4600f1b" />

```bash
./assignment1b.sh moveFile /tmp/dir1/file1.txt /tmp/dir1/file2.txt
```

### Verification

```bash
ls -l /tmp/dir1
```

## 15. Move File to Another Directory

<img width="1035" height="124" alt="image" src="https://github.com/user-attachments/assets/f2a0faf6-3862-4d98-bedc-d7822745542b" />

```bash
./assignment1b.sh moveFile /tmp/dir1/file2.txt /tmp/dir2/
```

### Verification

```bash
ls -l /tmp/dir2
```

## 16. Copy File

<img width="1035" height="118" alt="image" src="https://github.com/user-attachments/assets/ca3517e5-f058-4c0a-9a8a-65304b63f971" />

```bash
./assignment1b.sh copyFile /tmp/dir2/file2.txt /tmp/dir1/
```

### Verification

```bash
ls -l /tmp/dir1 /tmp/dir2
```

## 17. Copy File With New Name

<img width="1035" height="146" alt="image" src="https://github.com/user-attachments/assets/eccd7692-1a50-4e27-8cb8-a4bff177ef70" />

```bash
./assignment1b.sh copyFile /tmp/dir1/file2.txt /tmp/dir1/file3.txt
```

### Verification

```bash
ls -l /tmp/dir1
```

## 18. Clear File Content

<img width="1035" height="101" alt="image" src="https://github.com/user-attachments/assets/c897a53c-930d-4f0e-b120-661a7bdbe221" />

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

<img width="1035" height="78" alt="image" src="https://github.com/user-attachments/assets/138e8e64-b47a-46ab-8839-3678ac262847" />


<img width="1035" height="154" alt="image" src="https://github.com/user-attachments/assets/68b62ea5-9f8c-4162-a8fc-2d42bc61ff0b" />


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
