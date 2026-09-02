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

```bash
cat trainer.template
```

### 3. Test basic replacement

```bash
./assignment5a.sh trainer.template fname=sandeep topic=linux
```

### 4. Test multiple variables

```bash
./assignment5a.sh trainer2.template fname=Rahul topic=Linux tool=Bash
```

### 5. Test invalid template file

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
