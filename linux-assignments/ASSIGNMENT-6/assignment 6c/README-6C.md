# Assignment 6C – Process Experiments

## Objective

Experiment with a running Linux process by:

1. Clearing its log file.
2. Deleting its log file while it is running and observing the effect.
3. Elevating its process priority.

## Script

`assignment6c.sh`

## Test Log

The script continuously writes timestamped messages to:

```text
~/assignment6c.log
```

## 1. Start and Verify Process

```bash
chmod +x assignment6c.sh
./assignment6c.sh &
PID=$!
echo "PID: $PID"
sleep 3
ps -p $PID -o pid,ni,stat,comm
cat ~/assignment6c.log
```

## 2. Clear the Log

```bash
ls -lh ~/assignment6c.log
cat ~/assignment6c.log
: > ~/assignment6c.log
ls -lh ~/assignment6c.log
sleep 3
cat ~/assignment6c.log
```

The file contents are cleared, but the running process continues writing new entries.

## 3. Delete the Log

```bash
ps -p $PID -o pid,ni,stat,comm
rm ~/assignment6c.log
ls -l ~/assignment6c.log
ps -p $PID -o pid,ni,stat,comm
```

The process continues running even though the log filename has been deleted.

## 4. Observe the Deleted File

```bash
ls -l /proc/$PID/fd | grep deleted
```

A result containing:

```text
assignment6c.log (deleted)
```

shows that the running process still has the deleted file open.

## 5. Elevate Process Priority

Check the current priority:

```bash
ps -p $PID -o pid,ni,stat,comm
```

Elevate it:

```bash
sudo renice -n -5 -p $PID
```

Verify:

```bash
ps -p $PID -o pid,ni,stat,comm
```

The nice value changes from `0` to `-5`, indicating higher process priority.

## Cleanup

```bash
kill $PID
```

## Concepts Demonstrated

- Background processes
- Process IDs
- Log files
- File descriptors
- Deleted files held open by processes
- Process priority
- Nice values
- `renice`
- `/proc` filesystem

## Author

Linux Assignment – 6C
