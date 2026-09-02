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
<img width="1035" height="642" alt="image" src="https://github.com/user-attachments/assets/efa2c711-75b2-4602-9d3f-67dedc188781" />


## 2. Clear the Log

```bash
ls -lh ~/assignment6c.log
cat ~/assignment6c.log
: > ~/assignment6c.log
ls -lh ~/assignment6c.log
sleep 3
cat ~/assignment6c.log
```
<img width="1035" height="295" alt="image" src="https://github.com/user-attachments/assets/a3ce18e2-ecce-42c8-a560-74ae5cdcd240" />


The file contents are cleared, but the running process continues writing new entries.

## 3. Delete the Log

```bash
ps -p $PID -o pid,ni,stat,comm
rm ~/assignment6c.log
ls -l ~/assignment6c.log
ps -p $PID -o pid,ni,stat,comm
```
<img width="1035" height="295" alt="image" src="https://github.com/user-attachments/assets/61bbfdee-5dd4-4eee-bd7f-7ef641a3aeb5" />


The process continues running even though the log filename has been deleted.

## 4. Observe the Deleted File

```bash
ls -l /proc/$PID/fd | grep deleted
```
<img width="1035" height="158" alt="image" src="https://github.com/user-attachments/assets/af07612e-e099-4dfa-ac24-715a9524f8cc" />


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
<img width="1035" height="325" alt="image" src="https://github.com/user-attachments/assets/000d2886-e068-4918-ac74-565ad474b4e3" />
<img width="1035" height="99" alt="image" src="https://github.com/user-attachments/assets/0ede17b1-1758-43d8-94a2-47ad38d27497" />


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
