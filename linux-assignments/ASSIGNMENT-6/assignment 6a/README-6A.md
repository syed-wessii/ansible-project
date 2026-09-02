# Assignment 6A – Process Management Utility

## Objective
Create a Bash utility for common Linux process-management operations.

## Script
`assignment6a.sh`

## Supported Operations

```bash
./assignment6a.sh topProcess 5 memory
<img width="1035" height="227" alt="image" src="https://github.com/user-attachments/assets/7b299116-8e91-4f6c-8dc4-213bc12ab902" />

./assignment6a.sh topProcess 10 cpu
<img width="1035" height="411" alt="image" src="https://github.com/user-attachments/assets/f0a420bc-6b24-48d6-8bb3-3f1fb04e7f58" />

./assignment6a.sh killLeastPriorityProcess
<img width="1035" height="57" alt="image" src="https://github.com/user-attachments/assets/8db6155b-459c-48e8-8900-da1c961d532b" />

./assignment6a.sh RunningDurationProcess <processName>/<processID>
<img width="1035" height="102" alt="image" src="https://github.com/user-attachments/assets/044a58d6-f6fa-486c-93ac-c06f3c71c8fc" />

./assignment6a.sh listOrphanProcess
<img width="1035" height="597" alt="image" src="https://github.com/user-attachments/assets/4d681995-33d4-405a-b483-07b7a0fa041c" />

./assignment6a.sh listZoombieProcess
<img width="1035" height="94" alt="image" src="https://github.com/user-attachments/assets/2cb76f84-e56a-46b5-894e-8c706a076744" />

./assignment6a.sh killProcess <processName>/<processID>
<img width="1035" height="215" alt="image" src="https://github.com/user-attachments/assets/487f2cbe-d5ea-40ed-aaff-1adb2962ff1d" />

./assignment6a.sh ListWaitingProcess
<img width="1035" height="99" alt="image" src="https://github.com/user-attachments/assets/f5f80ab4-8ea1-4e42-acc2-c7c11c3c5a71" />

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
