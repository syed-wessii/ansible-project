# Linux Assignment 1A

## Basic Linux Commands

This assignment covers basic Linux commands for working with directories, files, file contents, and file manipulation.

---

## Assignment Tasks and Commands

### 1. Check Current Working Directory

```bash
pwd
```
<img width="1035" height="169" alt="image" src="https://github.com/user-attachments/assets/d1f1dac3-c70b-4459-845d-12ba78ed46cd" />

### 2. Create `linux` Directory
<img width="1035" height="60" alt="image" src="https://github.com/user-attachments/assets/f642e281-a704-41cc-880b-06d5a55edb80" />

```bash
mkdir linux
```

### 3. Create `Assignment-01` Inside `linux`
<img width="1035" height="156" alt="image" src="https://github.com/user-attachments/assets/3bcdcbdc-b981-4917-bb09-cbfde91bf8ef" />

```bash
mkdir linux/Assignment-01
```

### 4. Create `dir1` Inside `/tmp`
<img width="1035" height="97" alt="image" src="https://github.com/user-attachments/assets/44cd3ef4-1795-4355-8ea5-c8d6f5349a3f" />

```bash
mkdir /tmp/dir1
```

### 5. Create `dir2` and `dir3` Using a Single Command
<img width="1035" height="238" alt="image" src="https://github.com/user-attachments/assets/a19cd179-ed5d-4cd2-8f0c-48646db135a5" />

```bash
mkdir -p /tmp/dir1/dir2/dir3
```

### 6. Delete `dir3`

<img width="1035" height="110" alt="image" src="https://github.com/user-attachments/assets/f18bb4e2-a291-4dc9-b58e-d05df79caeb3" />

```bash
rmdir /tmp/dir1/dir2/dir3
```

### 7. Create an Empty `first-name` File

<img width="1035" height="143" alt="image" src="https://github.com/user-attachments/assets/2b5e2675-4e88-46dd-ae3f-df07ba995d58" />

```bash
touch /tmp/first-name
```

### 8. Add the First Line

<img width="1035" height="74" alt="image" src="https://github.com/user-attachments/assets/cfd7a2a9-5780-4c67-8597-a6d9379bdb1d" />

```bash
echo "This is the first line" > /tmp/first-name
```

### 9. Append Another Line

<img width="1035" height="86" alt="image" src="https://github.com/user-attachments/assets/af6075f2-a218-4668-b99f-0af9ef41223f" />

```bash
echo "this is a additional content" >> /tmp/first-name
```

### 10. Create `last-name` File With Content

<img width="1035" height="86" alt="image" src="https://github.com/user-attachments/assets/2a7a3f8a-0269-42b1-bd05-14dfd3b9e808" />

<img width="1035" height="77" alt="image" src="https://github.com/user-attachments/assets/737a0f01-5add-4e77-8389-e09df6bba6aa" />

```bash
echo "last-name is my last name" > /tmp/last-name
```

### 11. Add a Line at the Beginning

<img width="1035" height="649" alt="image" src="https://github.com/user-attachments/assets/fdb53e71-e2a4-4961-be7f-4b7b5ff26dcd" />

```bash
echo "this is line at the beginning" | cat - /tmp/last-name > /tmp/temp && mv /tmp/temp /tmp/last-name
```

### 12. Add 8–10 More Lines

<img width="662" height="124" alt="image" src="https://github.com/user-attachments/assets/7aaefb16-33b4-44de-9485-0097568a2ef3" />

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

<img width="1035" height="102" alt="image" src="https://github.com/user-attachments/assets/bbd039b2-ca45-4dd7-a547-72306f905d07" />

### Top 5 Lines

```bash
head -5 /tmp/last-name
```

### Bottom 2 Lines

<img width="1035" height="60" alt="image" src="https://github.com/user-attachments/assets/3241674d-7b48-402c-a754-c6eed65ab326" />

```bash
tail -2 /tmp/last-name
```

### Only the 6th Line

<img width="1035" height="191" alt="image" src="https://github.com/user-attachments/assets/4075abff-72a9-4bf9-bcee-a565aafe1127" />

```bash
head -6 /tmp/last-name | tail -1
```

### Lines 3–8

<img width="1035" height="256" alt="image" src="https://github.com/user-attachments/assets/d5a9d004-35b6-4540-a82b-3796bfc85cdb" />

```bash
head -8 /tmp/last-name | tail -6
```

---

## 14. List Contents of `/tmp`

<img width="1035" height="93" alt="image" src="https://github.com/user-attachments/assets/af58d369-745e-49d8-b211-9da7bb3653b6" />

### All Contents Including Hidden Files

```bash
ls -la /tmp
```

### Only Files

```bash
find /tmp -maxdepth 1 -type f
```

### Only Directories

<img width="1035" height="116" alt="image" src="https://github.com/user-attachments/assets/59023900-e3d8-4fdd-8409-15243b9ea814" />

```bash
find /tmp -maxdepth 1 -type d
```

---

## 15. Copy `last-name` to `dir2`

<img width="1035" height="129" alt="image" src="https://github.com/user-attachments/assets/a2f12030-4001-48ea-9d9e-00187ea1e5ea" />

```bash
cp /tmp/last-name /tmp/dir1/dir2/last-name
```

## 16. Copy `last-name` With a Different Name

<img width="1035" height="129" alt="image" src="https://github.com/user-attachments/assets/bf7a5f36-ecd1-4ad1-b83a-fc7b5ebd93bd" />

```bash
cp /tmp/last-name /tmp/dir1/dir2/last-name.copy
```

## 17. Rename `first-name`

<img width="1035" height="129" alt="image" src="https://github.com/user-attachments/assets/1b6a1309-ed95-4e82-9824-18ca58ee6627" />

```bash
mv /tmp/first-name /tmp/first-name-new
```

## 18. Move `last-name` to `dir1`

```bash
mv /tmp/last-name /tmp/dir1/
```

## 19. Clear the Contents of `last-name.copy`

<img width="1035" height="91" alt="image" src="https://github.com/user-attachments/assets/75a9aa97-d204-4700-b02f-f5e20b86e02e" />

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

![Uploading image.png…]()

```bash
rm /tmp/dir1/dir2/last-name.copy
```

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
