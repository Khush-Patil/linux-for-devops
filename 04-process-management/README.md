# ⚙️ Linux Process Management

Process management is a fundamental Linux skill for DevOps engineers.

This topic covers how to:

- Understand Linux processes
- Find running processes
- Check process IDs
- Understand parent and child processes
- Monitor CPU and memory usage
- Run processes in foreground and background
- Stop and terminate processes
- Understand Linux signals
- Change process priority
- Find processes consuming CPU or memory
- Find processes using ports
- Identify zombie and orphan processes
- Troubleshoot application processes
- Monitor processes in real-world DevOps scenarios

---

# 1. Check Running Processes

## Command

```bash
ps

##Example Output

    PID TTY          TIME CMD
   2451 pts/0    00:00:00 bash
   3821 pts/0    00:00:00 ps

ps shows processes associated with the current terminal/session.

# 2. Show All Processes

## Command

```bash
ps aux

##Example Output

USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1  22560 10560 ?        Ss   07:30   0:02 /sbin/init
root         850  0.1  0.5 123456 45678 ?       S    07:31   0:05 nginx
khushboo    2451  0.0  0.1  15000  5000 pts/0  Ss   07:40   0:00 bash

ps aux is one of the most commonly used commands for process troubleshooting.

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
