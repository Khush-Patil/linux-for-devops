# 📌 Process Management Basics

# 1. Display Current Shell PID

## Command

```bash
echo $$
```

## Example Output

```text
2451
```

`$$` represents the PID of the current shell.

---

# 2. Display Parent Process ID

## Command

```bash
echo $PPID
```

## Example Output

```text
2400
```

`$PPID` represents the parent process ID.

---

# 3. Display Current Shell Process

## Command

```bash
ps
```

## Example Output

```text
    PID TTY          TIME CMD
   2451 pts/0    00:00:00 bash
   3182 pts/0    00:00:00 ps
```

---

# 4. Display All Running Processes

## Command

```bash
ps aux
```

## Example Output

```text
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1  22000 14000 ?        Ss   08:00   0:01 /sbin/init
root        1245  0.0  0.2  50000 18000 ?        Ss   08:10   0:00 sshd
khushboo    2451  0.0  0.1  12000  5000 pts/0    Ss   08:30   0:00 bash
```

---

# 5. Display Processes in Full Format

## Command

```bash
ps -ef
```

## Example Output

```text
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 08:00 ?        00:00:01 /sbin/init
root        1245       1  0 08:10 ?        00:00:00 /usr/sbin/sshd
khushboo    2451    2400  0 08:30 pts/0    00:00:00 bash
```

---

# 6. Display Process Tree

## Command

```bash
pstree
```

## Example Output

```text
systemd
├─sshd
│ └─bash
│   └─pstree
├─cron
└─docker
```

---

# 7. Display Process Tree with PIDs

## Command

```bash
pstree -p
```

## Example Output

```text
systemd(1)
├─sshd(1245)
│ └─bash(2451)
│   └─pstree(3200)
├─cron(850)
└─dockerd(1100)
```

---

# 8. Find Process by Name

## Command

```bash
pgrep nginx
```

## Example Output

```text
1520
1521
```

---

# 9. Find Process Name and PID

## Command

```bash
pgrep -a nginx
```

## Example Output

```text
1520 nginx: master process /usr/sbin/nginx
1521 nginx: worker process
```

---

# 10. Find Process Using PID

## Command

```bash
ps -p 1520
```

## Example Output

```text
    PID TTY          TIME CMD
   1520 ?        00:00:00 nginx
```

---

# 11. Display Process Details

## Command

```bash
ps -p 1520 -o pid,ppid,user,%cpu,%mem,stat,cmd
```

## Example Output

```text
    PID    PPID USER     %CPU %MEM STAT CMD
   1520       1 root      0.0  0.2 S    nginx: master process
```

---

# 12. Find Process Using grep

## Command

```bash
ps aux | grep nginx
```

## Example Output

```text
root      1520  0.0  0.2  nginx: master process
www-data  1521  0.0  0.1  nginx: worker process
```

---

# 13. Avoid grep Matching Itself

## Command

```bash
ps aux | grep '[n]ginx'
```

## Example Output

```text
root      1520  0.0  0.2  nginx: master process
www-data  1521  0.0  0.1  nginx: worker process
```

---

# 14. Display Top CPU Consuming Processes

## Command

```bash
ps aux --sort=-%cpu | head
```

## Example Output

```text
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
khushboo  3120 45.2  2.1 500000 80000 ?       R    10:20   2:15 python3 app.py
root      1520 10.5  0.2  50000 12000 ?       S    09:10   0:30 nginx
```

---

# 15. Display Top Memory Consuming Processes

## Command

```bash
ps aux --sort=-%mem | head
```

## Example Output

```text
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
mysql     2100  5.2 12.5 900000 500000 ?       S    08:10   5:20 mysqld
root      1100  3.1  8.2 700000 320000 ?       S    08:00   3:10 dockerd
```

---

# 16. Display Process Statistics

## Command

```bash
ps -eo pid,ppid,user,%cpu,%mem,stat,cmd
```

## Example Output

```text
PID   PPID USER      %CPU %MEM STAT CMD
1       0 root        0.0  0.1 Ss   /sbin/init
1520    1 root        0.0  0.2 S    nginx
2451 2400 khushboo    0.1  0.5 Ss   bash
```

---

# 17. Monitor Processes in Real Time

## Command

```bash
top
```

## Example Output

```text
top - 10:30:00 up 2 days,  3:20,  2 users
Tasks: 250 total, 1 running, 249 sleeping
%Cpu(s): 5.2 us, 2.1 sy, 92.7 id
MiB Mem :  7800 total,  2100 free
```

Press `q` to exit `top`.

---

# 18. Run Top in Batch Mode

## Command

```bash
top -b -n 1
```

## Example Output

```text
PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM COMMAND
3120 khushboo  20   0  500000  80000  12000 R  45.2  2.1 python3
1520 root      20   0   50000  12000   5000 S  10.5  0.2 nginx
```

---

# 19. Display First 10 Processes by CPU

## Command

```bash
ps -eo pid,ppid,user,%cpu,%mem,cmd --sort=-%cpu | head -11
```

## Example Output

```text
PID   PPID USER      %CPU %MEM CMD
3120  2400 khushboo  45.2  2.1 python3 app.py
1520     1 root      10.5  0.2 nginx
2100     1 mysql      5.2 12.5 mysqld
```

---

# 20. Display First 10 Processes by Memory

## Command

```bash
ps -eo pid,ppid,user,%cpu,%mem,cmd --sort=-%mem | head -11
```

## Example Output

```text
PID   PPID USER      %CPU %MEM CMD
2100     1 mysql      5.2 12.5 mysqld
1100     1 root       3.1  8.2 dockerd
3120  2400 khushboo  45.2  2.1 python3 app.py
```

---

# 21. Check Process Open Files

## Command

```bash
lsof -p 1520
```

## Example Output

```text
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
nginx   1520 root  cwd    DIR  253,0     4096    2 /
nginx   1520 root  txt    REG  253,0   123456 1234 /usr/sbin/nginx
nginx   1520 root    3u  IPv4  12345      0t0  TCP *:80 (LISTEN)
```

---

# 22. Find Process Using a Port

## Command

```bash
sudo lsof -i :8080
```

## Example Output

```text
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
python3 2451 khushboo 3u IPv4 12345 0t0 TCP *:8080 (LISTEN)
```

---

# 23. Find Process Using Port with ss

## Command

```bash
sudo ss -lntp | grep :8080
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8080 0.0.0.0:* users:(("python3",pid=2451,fd=3))
```

---

# 24. Send SIGTERM to a Process

## Command

```bash
kill 2451
```

## Example Output

```text
```

`kill PID` sends SIGTERM by default.

---

# 25. Force Kill a Process

## Command

```bash
kill -9 2451
```

## Example Output

```text
```

> Use `SIGKILL` carefully because the process cannot clean up before termination.

---

# 26. Kill Process by Name

## Command

```bash
pkill nginx
```

## Example Output

```text
```

---

# 27. Force Kill Process by Name

## Command

```bash
pkill -9 nginx
```

## Example Output

```text
```

---

# 28. Check Process Exit Status

## Command

```bash
echo $?
```

## Example Output

```text
0
```

`0` generally indicates that the previous command completed successfully.

---

# 29. Run Process in Background

## Command

```bash
sleep 300 &
```

## Example Output

```text
[1] 3200
```

---

# 30. Display Background Jobs

## Command

```bash
jobs
```

## Example Output

```text
[1]+  Running                 sleep 300 &
```

---

# 31. Bring Background Job to Foreground

## Command

```bash
fg %1
```

## Example Output

```text
sleep 300
```

---

# 32. Suspend a Running Process

## Command

```bash
Ctrl+Z
```

## Example Output

```text
[1]+  Stopped                 sleep 300
```

---

# 33. Resume Process in Background

## Command

```bash
bg %1
```

## Example Output

```text
[1]+ sleep 300 &
```

---

# 34. Run Process with nohup

## Command

```bash
nohup python3 app.py > app.log 2>&1 &
```

## Example Output

```text
[1] 3500
nohup: ignoring input and redirecting stderr to stdout
```

---

# 35. Check nohup Process

## Command

```bash
ps aux | grep '[a]pp.py'
```

## Example Output

```text
khushboo 3500  0.2  1.5 250000 60000 ? S 10:40 0:02 python3 app.py
```

---

# 36. Check Process Priority

## Command

```bash
ps -eo pid,ni,pri,cmd
```

## Example Output

```text
PID   NI PRI CMD
1      0  19 /sbin/init
1520   0  19 nginx
3500   0  19 python3 app.py
```

---

# 37. Start Process with Lower Priority

## Command

```bash
nice -n 10 python3 app.py
```

## Example Output

```text
Application started
```

---

# 38. Check Nice Value

## Command

```bash
ps -o pid,ni,cmd -p 3500
```

## Example Output

```text
PID   NI CMD
3500  10 python3 app.py
```

---

# 39. Change Process Priority

## Command

```bash
renice 5 -p 3500
```

## Example Output

```text
3500 (process ID) old priority 10, new priority 5
```

---

# 40. Display Process Threads

## Command

```bash
ps -eLf
```

## Example Output

```text
UID      PID  PPID   LWP  C NLWP STIME TTY      TIME CMD
root    1520     1  1520  0    4 09:10 ?        00:00:00 nginx
root    1520     1  1521  0    4 09:10 ?        00:00:00 nginx
```

---

# 41. Display Threads of a Process

## Command

```bash
ps -T -p 1520
```

## Example Output

```text
PID   SPID TTY      TIME CMD
1520  1520 ?        00:00:00 nginx
1520  1521 ?        00:00:00 nginx
```

---

# 42. Check Process Status from /proc

## Command

```bash
cat /proc/1520/status
```

## Example Output

```text
Name:   nginx
State:  S (sleeping)
Pid:    1520
PPid:   1
Threads: 4
```

---

# 43. Check Process Command

## Command

```bash
cat /proc/1520/cmdline
```

## Example Output

```text
nginx: master process /usr/sbin/nginx
```

---

# 44. Check Process Working Directory

## Command

```bash
readlink -f /proc/1520/cwd
```

## Example Output

```text
/
```

---

# 45. Check Process Executable

## Command

```bash
readlink -f /proc/1520/exe
```

## Example Output

```text
/usr/sbin/nginx
```

---

# 46. Check Process Environment

## Command

```bash
sudo tr '\0' '\n' < /proc/1520/environ
```

## Example Output

```text
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
LANG=C.UTF-8
HOME=/root
```

---

# 47. Check Process File Descriptors

## Command

```bash
ls -l /proc/1520/fd
```

## Example Output

```text
lrwx------ 1 root root 64 Aug 27 10:00 0 -> /dev/null
lrwx------ 1 root root 64 Aug 27 10:00 1 -> /var/log/nginx.log
lrwx------ 1 root root 64 Aug 27 10:00 3 -> socket:[12345]
```

---

# 48. Check Process Memory

## Command

```bash
pmap 1520
```

## Example Output

```text
1520: nginx
0000555555554000    120K r-x-- nginx
0000555555573000     20K r---- nginx
total             15000K
```

---

# 49. Check Process Resource Limits

## Command

```bash
cat /proc/1520/limits
```

## Example Output

```text
Limit                     Soft Limit   Hard Limit
Max open files             1024         4096
Max processes              31000        31000
Max stack size             8388608      unlimited
```

---

# 50. Monitor a Specific Process

## Command

```bash
top -p 1520
```

## Example Output

```text
PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM COMMAND
1520 root      20   0   50000  12000   5000 S   0.0  0.2 nginx
```

---

# 51. Monitor Multiple Processes

## Command

```bash
top -p 1520,2451,3500
```

## Example Output

```text
PID  USER      %CPU %MEM COMMAND
1520 root       0.0  0.2 nginx
2451 khushboo   2.5  1.2 python3
3500 khushboo   1.1  0.8 python3
```

---

# 52. Check Process Start Time

## Command

```bash
ps -p 1520 -o pid,lstart,cmd
```

## Example Output

```text
PID  STARTED                     CMD
1520 Thu Aug 27 09:10:01 2026   nginx: master process
```

---

# 53. Check Process Runtime

## Command

```bash
ps -p 1520 -o pid,etime,cmd
```

## Example Output

```text
PID  ELAPSED CMD
1520 01:25:30 nginx: master process
```

---

# 54. Check Process CPU Time

## Command

```bash
ps -p 1520 -o pid,time,cmd
```

## Example Output

```text
PID      TIME CMD
1520 00:00:03 nginx
```

---

# 55. Check Parent Process

## Command

```bash
ps -o pid,ppid,cmd -p 1520
```

## Example Output

```text
PID   PPID CMD
1520     1 nginx: master process
```

---

# 56. Display Child Processes

## Command

```bash
pgrep -P 1520
```

## Example Output

```text
1521
1522
1523
```

---

# 57. Display Process Children

## Command

```bash
pstree -p 1520
```

## Example Output

```text
nginx(1520)─┬─nginx(1521)
            ├─nginx(1522)
            └─nginx(1523)
```

---

# 58. Check Process State

## Command

```bash
ps -p 1520 -o pid,stat,cmd
```

## Example Output

```text
PID   STAT CMD
1520  Ss   nginx: master process
```

Common process states include:

```text
R = Running
S = Sleeping
D = Uninterruptible sleep
T = Stopped
Z = Zombie
```

---

# 59. Find Zombie Processes

## Command

```bash
ps aux | awk '$8 ~ /Z/ {print}'
```

## Example Output

```text
user  4200  0.0  0.0  0  0 ?  Z  10:20  0:00 [process] <defunct>
```

---

# 60. Find Orphan Processes

## Command

```bash
ps -eo pid,ppid,cmd | awk '$2 == 1'
```

## Example Output

```text
PID   PPID CMD
1520     1 nginx
2100     1 mysqld
```

---

# 61. Check Process Count

## Command

```bash
ps -e --no-headers | wc -l
```

## Example Output

```text
250
```

---

# 62. Check Processes for Current User

## Command

```bash
ps -u "$USER"
```

## Example Output

```text
PID TTY          TIME CMD
2451 pts/0    00:00:00 bash
3500 ?        00:00:02 python3
```

---

# 63. Count Processes for Current User

## Command

```bash
pgrep -u "$USER" | wc -l
```

## Example Output

```text
15
```

---

# 64. Find Process by User

## Command

```bash
pgrep -u khushboo
```

## Example Output

```text
2451
3500
3600
```

---

# 65. Check Process Tree with pstree

## Command

```bash
pstree -ap
```

## Example Output

```text
systemd,1
  ├─sshd,1245
  │   └─bash,2451
  └─dockerd,1100
```

---

# 66. Check Process Using a File

## Command

```bash
sudo lsof /var/log/syslog
```

## Example Output

```text
COMMAND  PID USER   FD   TYPE DEVICE NAME
rsyslogd 900 syslog 5w   REG  253,0  /var/log/syslog
```

---

# 67. Check Process Using a Directory

## Command

```bash
sudo lsof +D /var/log
```

## Example Output

```text
COMMAND  PID USER   FD   TYPE NAME
rsyslogd 900 syslog  cwd  DIR  /var/log
```

---

# 68. Check Network Connections of a Process

## Command

```bash
sudo lsof -p 1520 -i
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NODE NAME
nginx 1520 root 3u IPv4 12345 TCP *:80 (LISTEN)
```

---

# 69. Trace a Running Process

## Command

```bash
sudo strace -p 1520
```

## Example Output

```text
epoll_wait(5, [], 512, -1)
accept4(3, ...)
```

Press `Ctrl+C` to stop tracing.

---

# 70. Trace Process System Calls

## Command

```bash
sudo strace -f -p 1520
```

## Example Output

```text
epoll_wait(...)
accept4(...)
read(...)
write(...)
```

---

# 71. Check Process CPU Affinity

## Command

```bash
taskset -cp 1520
```

## Example Output

```text
pid 1520's current affinity list: 0-7
```

---

# 72. Set Process CPU Affinity

## Command

```bash
sudo taskset -cp 0 1520
```

## Example Output

```text
pid 1520's current affinity list: 0-7
pid 1520's new affinity list: 0
```

---

# 73. Check Number of Threads

## Command

```bash
ps -p 1520 -o nlwp
```

## Example Output

```text
NLWP
4
```

---

# 74. Display Processes Sorted by PID

## Command

```bash
ps -eo pid,ppid,user,cmd --sort=pid
```

## Example Output

```text
PID PPID USER CMD
1   0   root /sbin/init
900 1   syslog rsyslogd
1520 1  root nginx
```

---

# 75. Display Processes Sorted by Memory

## Command

```bash
ps -eo pid,user,%mem,%cpu,cmd --sort=-%mem | head
```

## Example Output

```text
PID USER      %MEM %CPU CMD
2100 mysql     12.5 5.2 mysqld
1100 root       8.2 3.1 dockerd
3500 khushboo   2.1 4.5 python3 app.py
```

---

# 76. Display Processes Sorted by CPU

## Command

```bash
ps -eo pid,user,%cpu,%mem,cmd --sort=-%cpu | head
```

## Example Output

```text
PID USER      %CPU %MEM CMD
3500 khushboo  45.2 2.1 python3 app.py
1520 root      10.5 0.2 nginx
2100 mysql      5.2 12.5 mysqld
```

---

# 77. Monitor Process Every 2 Seconds

## Command

```bash
watch -n 2 'ps -eo pid,ppid,%cpu,%mem,cmd --sort=-%cpu | head'
```

## Example Output

```text
Every 2.0s: ps -eo pid,ppid,%cpu,%mem,cmd

PID   PPID %CPU %MEM CMD
3500  2400 45.2  2.1 python3 app.py
1520     1 10.5  0.2 nginx
```

Press `Ctrl+C` to exit.

---

# 78. Check Process Information Using pidof

## Command

```bash
pidof nginx
```

## Example Output

```text
1521 1520
```

---

# 79. Check Process Command Using pidof

## Command

```bash
pidof -x nginx
```

## Example Output

```text
1521 1520
```

---

# 80. Check Process Resource Usage

## Command

```bash
/usr/bin/time -v sleep 2
```

## Example Output

```text
User time (seconds): 0.00
System time (seconds): 0.00
Elapsed (wall clock) time: 0:02.00
Maximum resident set size: 1500
```

---

# 🧪 Practical Process Management Lab

## Command

```bash
mkdir process-lab
cd process-lab
```

## Example Output

```text
```

---

# 81. Start a Background Process

## Command

```bash
sleep 300 &
```

## Example Output

```text
[1] 5000
```

---

# 82. Find the Background Process

## Command

```bash
pgrep -a sleep
```

## Example Output

```text
5000 sleep 300
```

---

# 83. Check the Process

## Command

```bash
ps -p 5000 -o pid,ppid,stat,etime,cmd
```

## Example Output

```text
PID  PPID STAT ELAPSED CMD
5000 2451 S    00:10   sleep 300
```

---

# 84. Check Process Open Files

## Command

```bash
lsof -p 5000
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NAME
sleep   5000 khushboo cwd DIR 253,0 /home/khushboo/process-lab
```

---

# 85. Terminate the Process

## Command

```bash
kill 5000
```

## Example Output

```text
```

---

# 86. Verify Process Terminated

## Command

```bash
ps -p 5000
```

## Example Output

```text
PID TTY          TIME CMD
```

---

# 87. Check Process Does Not Exist

## Command

```bash
pgrep sleep
```

## Example Output

```text
```

---

# 88. Remove Lab Directory

## Command

```bash
cd ..
rmdir process-lab
```

## Example Output

```text
```

---

# 📚 Process Management Commands Summary

## Command

```bash
echo $$
echo $PPID
ps
ps aux
ps -ef
pstree
pstree -p
pgrep
pgrep -a
pidof
top
top -b -n 1
lsof
ss
kill
kill -9
pkill
ps --sort
nice
renice
jobs
fg
bg
nohup
ps -T
pmap
strace
taskset
watch
/proc
```

## Example Output

```text
Process identification
Process monitoring
CPU monitoring
Memory monitoring
Process termination
Process priority management
Background process management
Process tree analysis
Open file analysis
Network process analysis
System call tracing
CPU affinity management
```

---

# 🎯 DevOps Skills Practiced

## Command

```bash
ps aux
top
pgrep
lsof
ss
kill
pkill
journalctl
systemctl
strace
```

## Example Output

```text
Process Monitoring
Resource Monitoring
Application Troubleshooting
CPU Investigation
Memory Investigation
Port Investigation
Process Termination
Production Troubleshooting
```

---

# ✅ Learning Outcome

## Command

```bash
ps aux
top
pgrep
lsof
kill
strace
```

## Example Output

```text
By completing this topic, you should be able to:

- Identify running processes
- Understand PID and PPID
- Monitor CPU and memory usage
- Find processes by name
- Find processes using ports
- Analyze process trees
- Manage background processes
- Terminate processes safely
- Change process priority
- Inspect /proc information
- Investigate zombie processes
- Analyze open files
- Trace system calls
- Troubleshoot production processes
```
