# Linux Assignment 5A – Template Engine

## Objective

Create a Bash Template Engine that reads a template file and replaces placeholders with values provided as `key=value` arguments.

## Script

```bash
assignment5a.sh
```

## Syntax

```bash
./assignment5a.sh <template-file> key1=value1 key2=value2 ...
```

## Example Template

**trainer.template**

```text
{{fname}} is trainer of {{topic}}
```

## Execution

```bash
./assignment5a.sh trainer.template fname=sandeep topic=linux
```

## Expected Output

```text
sandeep is trainer of linux
```

## Features

* Accepts a template file as the first argument.
* Accepts multiple `key=value` arguments.
* Replaces `{{key}}` placeholders with corresponding values.
* Replaces all occurrences of a placeholder.
* Checks whether the template file exists.
* Displays an error when the template file is missing.

## Verification

### 1. Make the script executable

```bash
chmod +x assignment5a.sh
```

### 2. Verify the template
<img width="1035" height="168" alt="image" src="https://github.com/user-attachments/assets/6a870da8-ff98-4019-83b9-290885fd5a7b" />

```bash
cat trainer.template
```

### 3. Test basic replacement
<img width="953" height="43" alt="image" src="https://github.com/user-attachments/assets/fda7d6af-a8c8-4539-b32d-91d87eb96854" />

```bash
./assignment5a.sh trainer.template fname=sandeep topic=linux
```

### 4. Test multiple variables
<img width="953" height="130" alt="image" src="https://github.com/user-attachments/assets/d28875c5-d17f-4af6-89e1-61c8766f79d0" />

```bash
./assignment5a.sh trainer2.template fname=Rahul topic=Linux tool=Bash
```

### 5. Test invalid template file
<img width="953" height="42" alt="image" src="https://github.com/user-attachments/assets/62211849-e2f4-452e-9861-f3435e38976a" />

<img width="1035" height="41" alt="image" src="https://github.com/user-attachments/assets/7efd7249-1935-46d8-a2b9-951441856cb8" />


```bash
./assignment5a.sh missing.template fname=sandeep topic=linux
```

## Technologies Used

* Linux
* Bash Shell
* `sed`
* Shell scripting

## Author

Linux Assignment – 5A
