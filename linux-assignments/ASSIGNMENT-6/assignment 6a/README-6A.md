# Assignment 6A – Process Management Utility

## Objective
Create a Bash utility for common Linux process-management operations.

## Script
`assignment6a.sh`

## Supported Operations

```bash
assignment6a.sh topProcess 5 memory
<img width="1035" height="227" alt="image" src="https://github.com/user-attachments/assets/314ee1cc-9ff4-4440-b264-bb3a123a97e5" />

assignment6a.sh topProcess 10 cpu
<img width="1035" height="411" alt="image" src="https://github.com/user-attachments/assets/624f33e0-c8d5-4e42-a672-af64a1b6dd11" />

assignment6a.sh killLeastPriorityProcess
<img width="1035" height="57" alt="image" src="https://github.com/user-attachments/assets/3e25addd-c359-41d6-b35f-71016aa72b6f" />

assignment6a.sh RunningDurationProcess <processName>/<processID>
<img width="1035" height="102" alt="image" src="https://github.com/user-attachments/assets/419403e0-dda8-46d0-831c-2075d13f25a0" />

assignment6a.sh listOrphanProcess
<img width="1035" height="597" alt="image" src="https://github.com/user-attachments/assets/f119c38d-22ce-402b-8baa-e56f099d83b6" />

assignment6a.sh listZoombieProcess
<img width="1035" height="94" alt="image" src="https://github.com/user-attachments/assets/91c782a7-7845-4b5f-b13c-f58e23edebf2" />

assignment6a.sh killProcess <processName>/<processID>
<img width="1035" height="215" alt="image" src="https://github.com/user-attachments/assets/2cfbabe5-983e-4e91-a9d8-161ab05827a3" />

assignment6a.sh ListWaitingProcess
<img width="1035" height="99" alt="image" src="https://github.com/user-attachments/assets/8adde405-7b7a-41d9-a926-14dbd9b2ff20" />

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
