# Linux Assignment 1A

## Basic Linux Commands

This assignment covers basic Linux commands for working with directories, files, file contents, and file manipulation.

---

## Assignment Tasks and Commands

### 1. Check Current Working Directory

```bash
pwd
```

### 2. Create `linux` Directory

```bash
mkdir linux
```

### 3. Create `Assignment-01` Inside `linux`

```bash
mkdir linux/Assignment-01
```

### 4. Create `dir1` Inside `/tmp`

```bash
mkdir /tmp/dir1
```

### 5. Create `dir2` and `dir3` Using a Single Command

```bash
mkdir -p /tmp/dir1/dir2/dir3
```

### 6. Delete `dir3`

```bash
rmdir /tmp/dir1/dir2/dir3
```

### 7. Create an Empty `first-name` File

```bash
touch /tmp/first-name
```

### 8. Add the First Line

```bash
echo "This is the first line" > /tmp/first-name
```

### 9. Append Another Line

```bash
echo "this is a additional content" >> /tmp/first-name
```

### 10. Create `last-name` File With Content

```bash
echo "last-name is my last name" > /tmp/last-name
```

### 11. Add a Line at the Beginning

```bash
echo "this is line at the beginning" | cat - /tmp/last-name > /tmp/temp && mv /tmp/temp /tmp/last-name
```

### 12. Add 8–10 More Lines

```bash
cat <<EOF >> /tmp/last-name
Line 3
Line 4
Line 5
Line 6
Line 7
Line 8
Line 9
Line 10
Line 11
EOF
```

---

## 13. Display Specific Lines

### Top 5 Lines

```bash
head -5 /tmp/last-name
```

### Bottom 2 Lines

```bash
tail -2 /tmp/last-name
```

### Only the 6th Line

```bash
head -6 /tmp/last-name | tail -1
```

### Lines 3–8

```bash
head -8 /tmp/last-name | tail -6
```

---

## 14. List Contents of `/tmp`

### All Contents Including Hidden Files

```bash
ls -la /tmp
```

### Only Files

```bash
find /tmp -maxdepth 1 -type f
```

### Only Directories

```bash
find /tmp -maxdepth 1 -type d
```

---

## 15. Copy `last-name` to `dir2`

```bash
cp /tmp/last-name /tmp/dir1/dir2/last-name
```

## 16. Copy `last-name` With a Different Name

```bash
cp /tmp/last-name /tmp/dir1/dir2/last-name.copy
```

## 17. Rename `first-name`

```bash
mv /tmp/first-name /tmp/first-name-new
```

## 18. Move `last-name` to `dir1`

```bash
mv /tmp/last-name /tmp/dir1/
```

## 19. Clear the Contents of `last-name.copy`

```bash
> /tmp/dir1/dir2/last-name.copy
```

### Verify That the File Is Empty

```bash
wc -c /tmp/dir1/dir2/last-name.copy
```

Expected output:

```text
0 /tmp/dir1/dir2/last-name.copy
```

## 20. Delete `last-name.copy`

```bash
rm /tmp/dir1/dir2/last-name.copy
```

---

## Additional Practice

### Delete a Specific Line

For example, delete line 6:

```bash
sed -i '6d' /tmp/last-name
```

### Delete Lines 3–8

```bash
sed -i '3,8d' /tmp/last-name
```

### Delete the First Line

```bash
sed -i '1d' /tmp/last-name
```

### Delete the Last Line

```bash
sed -i '$d' /tmp/last-name
```

### Delete the Last 10 Lines

```bash
head -n -10 /tmp/last-name > /tmp/temp && mv /tmp/temp /tmp/last-name
```

---

## Directory Structure

The required directory structure is:

```text
/tmp
└── dir1
    └── dir2
        └── dir3
```

---

## Verification

Commands such as the following can be used to verify the results:

```bash
ls -d /tmp/dir1
ls -R /tmp/dir1
cat /tmp/first-name
cat /tmp/last-name
wc -l /tmp/last-name
ls -la /tmp
```

---

## Learning Outcomes

Through this assignment, I practiced:

* Checking the current working directory
* Creating and removing directories
* Creating empty files
* Writing and appending file content
* Adding content at the beginning of a file
* Viewing specific portions of a file
* Listing files and directories
* Copying files
* Renaming and moving files
* Clearing file contents
* Deleting files
