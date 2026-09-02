# Assignment 6A – Process Management Utility

## Objective
Create a Bash utility for common Linux process-management operations.

## Script
`assignment6a.sh`

## Supported Operations

```bash
./assignment6a.sh topProcess 5 memory
./assignment6a.sh topProcess 10 cpu
./assignment6a.sh killLeastPriorityProcess
./assignment6a.sh RunningDurationProcess <processName>/<processID>
./assignment6a.sh listOrphanProcess
./assignment6a.sh listZoombieProcess
./assignment6a.sh killProcess <processName>/<processID>
./assignment6a.sh ListWaitingProcess
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
