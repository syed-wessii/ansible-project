# Assignment 6B – Process Manager Utility

## Objective
Create a Bash Process Manager utility that can register, start, monitor, stop, prioritize, and list services using aliases.

## Script
`assignment6b.sh`

## Operations

### 1. Register Service

```text
./assignment6b.sh -o register -s <path> -a <alias>
```

**Screenshot:**

<img width="1050" height="117" alt="image" src="https://github.com/user-attachments/assets/8d6f9531-1102-4d35-a62f-64e3e370b131" />


### 2. Start Service

```text
./assignment6b.sh -o start -a <alias>
```

**Screenshot:**

<img width="1050" height="93" alt="image" src="https://github.com/user-attachments/assets/eb1b6e15-10b0-45a0-964e-57f86ed6d932" />



### 3. Check Service Status

```text
./assignment6b.sh -o status -a <alias>
```

**Screenshot:**

<img width="1050" height="60" alt="image" src="https://github.com/user-attachments/assets/f85c5f76-82a8-4d3e-8915-2fd6588abdbf" />


### 4. Kill Service

```text
./assignment6b.sh -o kill -a <alias>
```

**Screenshot:**

<img width="1050" height="67" alt="image" src="https://github.com/user-attachments/assets/0b48405a-9dfb-416e-a9c8-18112bfd9cf4" />


### 5. Change Service Priority

```text
./assignment6b.sh -o priority -p <low/med/high> -a <alias>
```

<img width="1050" height="131" alt="image" src="https://github.com/user-attachments/assets/418d8c22-2dcb-481a-8d4b-dfd6e7f08426" />

<i<img width="1050" height="156" alt="image" src="https://github.com/user-attachments/assets/9de549ad-3a8a-4b8e-89d7-2d7274e245dc" />


### 6. List Registered Services

```text
./assignment6b.sh -o list
```

**Screenshot:**

<img width="1050" height="111" alt="image" src="https://github.com/user-attachments/assets/9b640bc5-a728-495c-bf53-6c1b62f6778d" />


### 7. Display Top Processes

```text
./assignment6b.sh -o top
```

**Screenshot:**

<img src="YOUR_TOP_SCREENSHOT_URL" />

### 8. Display Top Processes for a Specific Service

```text
./assignment6b.sh -o top -a <alias>
```

**Screenshot:**
<img width="1050" height="127" alt="image" src="https://github.com/user-attachments/assets/df177ea8-2259-4b50-b404-3d7cba2d0c22" />

```

## Features
- Register a script with an alias.
- Store alias, script path, and PID information.
- Start registered services in the background.
- Check service status.
- Stop services by alias.
- Change process priority using `renice`.
- List registered services.
- Display alias, PID, state, priority, and script path.

## Database

The utility stores service information in:

```text
~/.process_manager.db
```

Database format:

```text
alias|script_path|PID
```

## Example

```bash
./assignment6b.sh -o register -s /home/syed/opstree/testservice.sh -a service1
./assignment6b.sh -o start -a service1
./assignment6b.sh -o status -a service1
./assignment6b.sh -o top -a service1
./assignment6b.sh -o priority -p low -a service1
./assignment6b.sh -o kill -a service1
```

## Verification
The utility was verified for registration, startup, status, process details, priority changes, termination, service listing, and restart.

## Author
Linux Assignment – 6B
