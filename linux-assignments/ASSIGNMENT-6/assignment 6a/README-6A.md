# Assignment 6A – Process Management Utility

## Objective
Create a Bash utility for common Linux process-management operations.

## Script
`assignment6a.sh`


Then GitHub will still give you the nice code box and copy button, but **without Bash-specific syntax coloring**.

### So I recommend:

Keep it as:

```markdown
## Supported Operations

```text
./assignment6a.sh topProcess 5 memory
<img width="1035" height="227" alt="image" src="https://github.com/user-attachments/assets/f6e44229-d23a-4a61-9f05-b50c3d3fe156" />

./assignment6a.sh topProcess 10 cpu
<img width="1035" height="411" alt="image" src="https://github.com/user-attachments/assets/a29537cb-2098-4f47-ac3c-42f2dbdbc26b" />

./assignment6a.sh killLeastPriorityProcess
<img width="1035" height="57" alt="image" src="https://github.com/user-attachments/assets/6d390238-2355-492e-b12a-167917edcc6f" />

./assignment6a.sh RunningDurationProcess <processName>/<processID>
<img width="1035" height="102" alt="image" src="https://github.com/user-attachments/assets/0aa0a802-1fa0-4cac-ba1b-990a938fe982" />

./assignment6a.sh listOrphanProcess
<img width="1035" height="597" alt="image" src="https://github.com/user-attachments/assets/a94a92f5-76cb-4baa-85f2-efece5c9adf7" />

./assignment6a.sh listZombieProcess
<img width="1035" height="94" alt="image" src="https://github.com/user-attachments/assets/e9399ec3-9750-4b79-b74d-aa7cbbc4469d" />

./assignment6a.sh killProcess <processName>/<processID>
<img width="1035" height="215" alt="image" src="https://github.com/user-attachments/assets/3b75998f-2c65-48dd-ac45-5370e1257625" />

./assignment6a.sh ListWaitingProcess
<img width="1035" height="99" alt="image" src="https://github.com/user-attachments/assets/d26e8f1e-8300-4d37-98f8-176fc06e8f35" />

```

## Features
- Find top processes by memory usage.
- Find top processes by CPU usage.
- Kill a lowest-priority process.
- Check process running duration by name or PID.
- List orphan processes.
- List zombie processes.
- Kill a process by name or PID.
- List processes waiting in uninterruptible sleep (`D` state).

## Usage

```bash
chmod +x assignment6a.sh
./assignment6a.sh topProcess 5 memory
./assignment6a.sh topProcess 10 cpu
```

## Verification
All supported operations were tested using Linux process-management commands and terminal output.

## Author
Linux Assignment – 6A
