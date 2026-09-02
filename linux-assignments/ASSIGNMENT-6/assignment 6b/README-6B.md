# Assignment 6B – Process Manager Utility

## Objective
Create a Bash Process Manager utility that can register, start, monitor, stop, prioritize, and list services using aliases.

## Script
`assignment6b.sh`

## Operations

```bash
./assignment6b.sh -o register -s <path> -a <alias>
./assignment6b.sh -o start -a <alias>
./assignment6b.sh -o status -a <alias>
./assignment6b.sh -o kill -a <alias>
./assignment6b.sh -o priority -p <low/med/high> -a <alias>
./assignment6b.sh -o list
./assignment6b.sh -o top
./assignment6b.sh -o top -a <alias>
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
