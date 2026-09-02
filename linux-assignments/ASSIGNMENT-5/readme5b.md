# Linux Assignment 5B – Text Editor Utility

## Objective
Create a Bash-based text editor utility that performs text and file editing operations from the command line.

## Script Used
```bash
assignment5b.sh
```

## Syntax
```bash
./assignment5b.sh <command> <file> [arguments]
```

## Supported Commands

| Command | Description |
|---|---|
| `addLineTop` | Adds a line at the top |
| `addLineBottom` | Adds a line at the bottom |
| `addLineAt` | Adds a line at a specific line number |
| `updateFirstWord` | Replaces the first occurrence of a word |
| `updateAllWords` | Replaces all occurrences of a word |
| `insertWord` | Inserts a word between two words |
| `deleteLine` | Deletes a specific line |
| `deleteLineWord` | Deletes lines containing a word |
| `backupFile` | Creates a backup copy |
| `emptyFile` | Removes file contents |

---

# Test File

Create:
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

---

# Verification

---

## 2. Add Line at Top
```bash
./assignment5b.sh addLineTop test.txt "This is the first line"
cat -n test.txt
```
### Screenshot
<img width="953" height="173" alt="image" src="https://github.com/user-attachments/assets/791d9f1e-1187-4a5a-ab37-b11af72497df" />


---

## 3. Add Line at Bottom
```bash
./assignment5b.sh addLineBottom test.txt "This is the last line"
cat -n test.txt
```
### Screenshot
<img width="953" height="193" alt="image" src="https://github.com/user-attachments/assets/cede6725-8207-4a5a-9ca9-150d72a2191e" />


---

## 4. Add Line at Specific Line Number
```bash
./assignment5b.sh addLineAt test.txt 3 "This line was inserted at line 3"
cat -n test.txt
```
### Screenshot
<img width="953" height="198" alt="image" src="https://github.com/user-attachments/assets/266daee5-c6cb-484f-9d40-32732959e796" />


---

## 5. Update First Word
```bash
./assignment5b.sh updateFirstWord test.txt Linux Ubuntu
cat -n test.txt
```
### Screenshot
<img width="953" height="234" alt="image" src="https://github.com/user-attachments/assets/9e2eb39f-2f2e-48e7-8e3a-40d732efb7eb" />


---

## 6. Update All Words
```bash
./assignment5b.sh updateAllWords test.txt Linux Unix
cat -n test.txt
```
### Screenshot
<img width="953" height="243" alt="image" src="https://github.com/user-attachments/assets/dbdef95c-5363-4ee2-b500-806682867bb3" />


---

## 7. Insert Word
```bash
./assignment5b.sh insertWord test.txt Bash is very
cat -n test.txt
```

Example:
```text
Bash is powerful
```
becomes:
```text
Bash very is powerful
```

### Screenshot
<img width="953" height="249" alt="image" src="https://github.com/user-attachments/assets/236658d3-be38-4f7a-bd65-53e81cda66b9" />


---

## 8. Delete Line
```bash
./assignment5b.sh deleteLine test.txt 3
cat -n test.txt
```
### Screenshot
<img width="953" height="265" alt="image" src="https://github.com/user-attachments/assets/d2881ce6-a651-47e4-8ce3-331365c7fb4d" />

---

## 9. Delete Lines Containing a Word
```bash
./assignment5b.sh deleteLineWord test.txt Docker
cat -n test.txt
```
### Screenshot
<img width="953" height="214" alt="image" src="https://github.com/user-attachments/assets/b81440f7-774c-4254-a258-e13e576c4129" />


---

# Custom Features

## 10. Backup File
```bash
./assignment5b.sh backupFile test.txt
ls -l test.txt test.txt.bak
cat test.txt.bak
```

### Screenshot
<img width="953" height="326" alt="image" src="https://github.com/user-attachments/assets/4110919b-2e6b-4859-9414-cde35cf5db8d" />


---

## 11. Empty File
```bash
cat test.txt
./assignment5b.sh emptyFile test.txt
ls -l test.txt
cat test.txt
```

### Screenshot
<img width="953" height="142" alt="image" src="https://github.com/user-attachments/assets/50e1dc51-a1de-433d-82d4-954d0c03f1f4" />


---

# Features

### Required Features
- Add line at top.
- Add line at bottom.
- Add line at a specific line number.
- Replace first occurrence of a word.
- Replace all occurrences of a word.
- Insert a word between two words.
- Delete a specific line.
- Delete lines containing a specified word.

### Additional Features
- `backupFile` creates a `.bak` backup.
- `emptyFile` clears the file without deleting it.
- Error handling for a missing target file.
- Success and error messages.

# Technologies Used
- Linux
- Bash Shell Scripting
- `sed`
- `cp`
- Shell redirection

# Assignment Submission
All verification screenshots are included above as evidence of successful execution.
