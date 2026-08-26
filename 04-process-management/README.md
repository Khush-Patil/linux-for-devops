---
# 1. Check Running Processes

## Command

```bash
ps

```
##Example Output

```text

    PID TTY          TIME CMD
   2451 pts/0    00:00:00 bash
   3821 pts/0    00:00:00 ps

```
ps shows processes associated with the current terminal/session.

---

# 2. Show All Processes

## Command

```bash

ps aux

```
##Example Output

```text

USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1  22560 10560 ?        Ss   07:30   0:02 /sbin/init
root         850  0.1  0.5 123456 45678 ?       S    07:31   0:05 nginx
khushboo    2451  0.0  0.1  15000  5000 pts/0  Ss   07:40   0:00 bash

```
ps aux is one of the most commonly used commands for process troubleshooting.

---

3. Show Processes in Full Format
Command
ps -ef
Example Output
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 07:30 ?        00:00:02 /sbin/init
root         850       1  0 07:31 ?        00:00:05 nginx
khushboo    2451    2400  0 07:40 pts/0    00:00:00 bash

-e displays all processes and -f displays full information.

4. Check a Specific Process
Command
ps -p 850
Example Output
    PID TTY          TIME CMD
    850 ?        00:00:05 nginx

Replace 850 with the actual PID you want to inspect.

5. Check Detailed Information About a Process
Command
ps -p 850 -f
Example Output
UID          PID    PPID  C STIME TTY          TIME CMD
root         850       1  0 07:31 ?        00:00:05 nginx
