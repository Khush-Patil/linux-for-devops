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

# 3. Display Current Shell

## Command

```bash
echo $SHELL
```

## Example Output

```text
/bin/bash
```

---

# 4. Display Current User

## Command

```bash
whoami
```

## Example Output

```text
khushboo
```

---

# 5. Display Running Processes

## Command

```bash
ps
```

## Example Output

```text
    PID TTY          TIME CMD
   2451 pts/0    00:00:00 bash
   3200 pts/0    00:00:00 ps
```

---

# 6. Display All Processes

## Command

```bash
ps -e
```

## Example Output

```text
    PID TTY          TIME CMD
      1 ?        00:00:02 systemd
    850 ?        00:00:05 nginx
   2451 pts/0    00:00:00 bash
```

---

# 7. Display All Processes in Full Format

## Command

```bash
ps -ef
```

## Example Output

```text
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 07:30 ?        00:00:02 /sbin/init
root         850       1  0 07:31 ?        00:00:05 nginx
khushboo    2451    2400  0 07:40 pts/0    00:00:00 bash
```

---

# 8. Display All Processes with User Information

## Command

```bash
ps aux
```

## Example Output

```text
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1  22560 10560 ?        Ss   07:30   0:02 /sbin/init
root         850  0.1  0.5 123456 45678 ?        S    07:31   0:05 nginx
khushboo    2451  0.0  0.1  15000  5000 pts/0  Ss   07:40   0:00 bash
```

---

# 9. Display Processes for Current User

## Command

```bash
ps -u "$USER"
```

## Example Output

```text
    PID TTY          TIME CMD
   2451 pts/0    00:00:00 bash
   3200 pts/0    00:00:00 ps
```

---

# 10. Display Processes for a Specific User

## Command

```bash
ps -u root
```

## Example Output

```text
    PID TTY          TIME CMD
      1 ?        00:00:02 systemd
    850 ?        00:00:05 nginx
```

---

# 🔎 Finding Processes

# 11. Find Process by Name

## Command

```bash
pgrep nginx
```

## Example Output

```text
850
851
852
```

---

# 12. Find Process and Command

## Command

```bash
pgrep -af nginx
```

## Example Output

```text
850 nginx: master process /usr/sbin/nginx
851 nginx: worker process
852 nginx: worker process
```

---

# 13. Find PID Using pidof

## Command

```bash
pidof nginx
```

## Example Output

```text
852 851 850
```

---

# 14. Search Process Using grep

## Command

```bash
ps aux | grep nginx
```

## Example Output

```text
root       850  0.0  0.5 123456 45678 ?       S    07:31   0:05 nginx
root       851  0.0  0.5 123456 45678 ?       S    07:31   0:05 nginx
```

---

# 15. Search Process Without Showing grep

## Command

```bash
ps aux | grep '[n]ginx'
```

## Example Output

```text
root       850  0.0  0.5 123456 45678 ?       S    07:31   0:05 nginx
root       851  0.0  0.5 123456 45678 ?       S    07:31   0:05 nginx
```

---

# 16. Check a Specific Process

## Command

```bash
ps -p 850
```

## Example Output

```text
    PID TTY          TIME CMD
    850 ?        00:00:05 nginx
```

---

# 17. Check Detailed Process Information

## Command

```bash
ps -p 850 -f
```

## Example Output

```text
UID          PID    PPID  C STIME TTY          TIME CMD
root         850       1  0 07:31 ?        00:00:05 nginx
```

---

# 18. Display Selected Process Columns

## Command

```bash
ps -o pid,ppid,user,stat,%cpu,%mem,cmd -p 850
```

## Example Output

```text
    PID    PPID USER       STAT %CPU %MEM CMD
    850       1 root       S     0.1  0.5 nginx
```

---

# 🌳 Process Hierarchy

# 19. Display Process Tree

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
├─nginx
│ ├─nginx
│ └─nginx
└─cron
```

---

# 20. Display Process Tree with PIDs

## Command

```bash
pstree -p
```

## Example Output

```text
systemd(1)
├─sshd(1200)
│ └─bash(2451)
└─nginx(850)─┬─nginx(851)
             └─nginx(852)
```

---

# 21. Display Children of a Process

## Command

```bash
pgrep -P 850
```

## Example Output

```text
851
852
```

`-P` searches for child processes of the specified PID.

---

# 22. Display Parent Process

## Command

```bash
ps -o pid,ppid,cmd -p 850
```

## Example Output

```text
PID  PPID CMD
850    1 nginx
```

---

# 23. Display PID and PPID for All Processes

## Command

```bash
ps -eo pid,ppid,cmd
```

## Example Output

```text
PID    PPID CMD
1         0 /sbin/init
850       1 nginx
2451   2400 bash
```

---

# 📊 Process Monitoring

# 24. Monitor Processes in Real Time

## Command

```bash
top
```

## Example Output

```text
top - 08:15:10 up 10:45, 1 user, load average: 0.12, 0.08, 0.05

Tasks: 150 total, 1 running, 149 sleeping

%Cpu(s): 5.0 us, 2.0 sy, 0.0 ni, 92.0 id

MiB Mem : 7800.0 total, 2100.0 used, 5700.0 free

PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM COMMAND
850 root      20   0  123456  45678  12000 S   5.0  0.5 nginx
```

Press `q` to exit.

---

# 25. Sort top by CPU Usage

## Command

```bash
top
```

Then press:

```text
P
```

## Example Output

```text
Processes are sorted by CPU usage.
```

---

# 26. Sort top by Memory Usage

## Command

```bash
top
```

Then press:

```text
M
```

## Example Output

```text
Processes are sorted by memory usage.
```

---

# 27. Sort top by Process ID

## Command

```bash
top
```

Then press:

```text
N
```

## Example Output

```text
Processes are sorted by process ID.
```

---

# 28. Display Interactive Process Monitor

## Command

```bash
htop
```

## Example Output

```text
CPU[||||||||        ] 15.0%
Mem[|||||||||       ] 35.0%

PID   USER       CPU%  MEM%  COMMAND
850   root        5.0   0.5  nginx
2451  khushboo    0.2   0.1  bash
```

`htop` may need to be installed separately.

---

# 29. Show Processes Sorted by CPU

## Command

```bash
ps aux --sort=-%cpu | head
```

## Example Output

```text
USER       PID %CPU %MEM COMMAND
root      4200 95.5  4.2 python3 app.py
mysql     1500  5.0  8.0 mysqld
```

---

# 30. Show Processes Sorted by Memory

## Command

```bash
ps aux --sort=-%mem | head
```

## Example Output

```text
USER       PID %CPU %MEM COMMAND
mysql     1500  2.0 18.0 mysqld
root      4200  5.0  8.5 python3 app.py
```

---

# 31. Show Top CPU Processes

## Command

```bash
ps -eo pid,user,%cpu,%mem,cmd --sort=-%cpu | head -11
```

## Example Output

```text
PID  USER  %CPU %MEM CMD
4200 root  95.5 4.2 python3 app.py
1500 mysql 5.0  8.0 mysqld
```

---

# 32. Show Top Memory Processes

## Command

```bash
ps -eo pid,user,%cpu,%mem,cmd --sort=-%mem | head -11
```

## Example Output

```text
PID  USER  %CPU %MEM CMD
1500 mysql 2.0 18.0 mysqld
4200 root  5.0  8.5 python3 app.py
```

---

# 33. Monitor a Process Continuously

## Command

```bash
watch -n 2 'ps -p 4200 -o pid,ppid,stat,%cpu,%mem,cmd'
```

## Example Output

```text
Every 2.0s:

PID  PPID STAT %CPU %MEM CMD
4200 1    S     4.5  8.2 python3 app.py
```

Press `Ctrl + C` to exit.

---

# 34. Count Running Processes

## Command

```bash
ps -e --no-headers | wc -l
```

## Example Output

```text
152
```

---

# 35. Count Processes by User

## Command

```bash
ps -eo user= | sort | uniq -c | sort -nr
```

## Example Output

```text
80 root
35 khushboo
20 www-data
10 mysql
```

---

# 🏃 Foreground and Background Processes

# 36. Run a Process in Foreground

## Command

```bash
sleep 60
```

## Example Output

```text
The terminal remains occupied until the command finishes.
```

---

# 37. Run a Process in Background

## Command

```bash
sleep 300 &
```

## Example Output

```text
[1] 4200
```

---

# 38. Display Background Jobs

## Command

```bash
jobs
```

## Example Output

```text
[1]+  Running                 sleep 300 &
```

---

# 39. Display Jobs with PIDs

## Command

```bash
jobs -l
```

## Example Output

```text
[1]+ 4200 Running                 sleep 300 &
```

---

# 40. Bring Background Job to Foreground

## Command

```bash
fg %1
```

## Example Output

```text
sleep 300
```

---

# 41. Send Foreground Process to Background

## Command

```bash
Ctrl + Z
```

## Example Output

```text
^Z
[1]+  Stopped                 sleep 300
```

Then:

## Command

```bash
bg %1
```

## Example Output

```text
[1]+ sleep 300 &
```

---

# 42. Stop Foreground Process

## Command

```bash
Ctrl + C
```

## Example Output

```text
^C
```

Sends `SIGINT`.

---

# 43. Suspend Foreground Process

## Command

```bash
Ctrl + Z
```

## Example Output

```text
^Z
[1]+  Stopped
```

Sends `SIGTSTP`.

---

# 44. Wait for Background Process

## Command

```bash
wait
```

## Example Output

```text
```

---

# 45. Wait for Specific Process

## Command

```bash
wait 4200
```

## Example Output

```text
```

---

# 🔔 Linux Signals

# 46. List Available Signals

## Command

```bash
kill -l
```

## Example Output

```text
1) SIGHUP
2) SIGINT
3) SIGQUIT
9) SIGKILL
15) SIGTERM
18) SIGCONT
19) SIGSTOP
```

---

# 47. Send SIGTERM

## Command

```bash
kill -15 4200
```

## Example Output

```text
Requests graceful process termination.
```

---

# 48. Send SIGTERM by Name

## Command

```bash
pkill -TERM nginx
```

## Example Output

```text
```

---

# 49. Send SIGKILL

## Command

```bash
kill -9 4200
```

## Example Output

```text
Forcefully terminates the process.
```

---

# 50. Send SIGKILL by Name

## Command

```bash
pkill -KILL nginx
```

## Example Output

```text
```

Use carefully because multiple matching processes can be terminated.

---

# 51. Send SIGSTOP

## Command

```bash
kill -STOP 4200
```

## Example Output

```text
Immediately stops the process.
```

---

# 52. Send SIGCONT

## Command

```bash
kill -CONT 4200
```

## Example Output

```text
Continues a stopped process.
```

---

# 53. Send SIGHUP

## Command

```bash
kill -HUP 4200
```

## Example Output

```text
Some applications use SIGHUP to reload configuration.
```

---

# 54. Send SIGINT

## Command

```bash
kill -INT 4200
```

## Example Output

```text
Similar to pressing Ctrl + C.
```

---

# 55. Kill Process by Name

## Command

```bash
pkill nginx
```

## Example Output

```text
```

Use carefully because multiple processes may match.

---

# 56. Kill Exact Process Name

## Command

```bash
pkill -x nginx
```

## Example Output

```text
```

---

# 57. Kill Process by Full Command Pattern

## Command

```bash
pkill -f "python3 app.py"
```

## Example Output

```text
```

`-f` matches against the full command line.

---

# 58. Check Whether Process Exists

## Command

```bash
pgrep nginx
```

## Example Output

```text
850
851
852
```

If nothing is returned, the process may not be running.

---

# 📁 Process Information Using /proc

# 59. View Process Status

## Command

```bash
cat /proc/4200/status
```

## Example Output

```text
Name:   python3
State:  S (sleeping)
Pid:    4200
PPid:   1
Uid:    1000
Gid:    1000
Threads:        8
```

---

# 60. View Process Command

## Command

```bash
cat /proc/4200/cmdline
```

## Example Output

```text
python3app.py
```

`/proc/<PID>/cmdline` contains the command line used to start the process.

---

# 61. View Process Executable

## Command

```bash
readlink -f /proc/4200/exe
```

## Example Output

```text
/usr/bin/python3.12
```

---

# 62. View Process Working Directory

## Command

```bash
readlink -f /proc/4200/cwd
```

## Example Output

```text
/opt/application
```

---

# 63. View Process Root Directory

## Command

```bash
readlink -f /proc/4200/root
```

## Example Output

```text
/
```

---

# 64. View Process Environment

## Command

```bash
sudo tr '\0' '\n' < /proc/4200/environ
```

## Example Output

```text
PATH=/usr/local/bin:/usr/bin
HOME=/root
USER=root
```

Process environments may contain passwords, tokens, or other secrets. Do not expose them in logs or repositories.

---

# 65. View Process Memory Information

## Command

```bash
cat /proc/4200/status | grep -E 'VmSize|VmRSS|VmPeak'
```

## Example Output

```text
VmPeak:  800000 kB
VmSize:  750000 kB
VmRSS:   450000 kB
```

---

# 66. View Process Memory Maps

## Command

```bash
cat /proc/4200/maps
```

## Example Output

```text
7f0000000000-7f0000100000 r-xp /usr/lib/libexample.so
```

---

# 67. View Process File Descriptors

## Command

```bash
ls -l /proc/4200/fd
```

## Example Output

```text
0 -> /dev/null
1 -> /var/log/application.log
2 -> /var/log/application-error.log
3 -> socket:[123456]
```

---

# 68. Count Process File Descriptors

## Command

```bash
ls /proc/4200/fd | wc -l
```

## Example Output

```text
128
```

---

# 69. View Process Limits

## Command

```bash
cat /proc/4200/limits
```

## Example Output

```text
Limit                     Soft Limit Hard Limit Units
Max open files            1024       4096       files
Max processes             15000      15000      processes
Max stack size             8388608    8388608    bytes
```

---

# 70. View Process IO Statistics

## Command

```bash
cat /proc/4200/io
```

## Example Output

```text
rchar: 123456
wchar: 456789
read_bytes: 98765
write_bytes: 12345
```

---

# 71. View Process Scheduling Information

## Command

```bash
cat /proc/4200/sched
```

## Example Output

```text
python3 (4200, #threads: 8)
se.exec_start : 123456789
se.vruntime : 987654
```

---

# 🔗 Open Files and Resources

# 72. Show Files Opened by Process

## Command

```bash
lsof -p 4200
```

## Example Output

```text
COMMAND  PID USER   FD   TYPE DEVICE NAME
python3 4200 root   cwd    DIR  8,1   /opt/application
python3 4200 root   txt    REG  8,1   /usr/bin/python3
```

---

# 73. Find Process Using a File

## Command

```bash
lsof /var/log/application.log
```

## Example Output

```text
COMMAND  PID USER   FD   TYPE NAME
python3 4200 root   1w   REG  /var/log/application.log
```

---

# 74. Find Process Using a Directory

## Command

```bash
lsof +D /var/log
```

## Example Output

```text
python3 4200 root  1w REG /var/log/application.log
```

`+D` recursively searches the directory and may be expensive on large directory trees.

---

# 🌐 Process and Network Ports

# 75. Show Listening Ports

## Command

```bash
sudo ss -lntp
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8000 0.0.0.0:* users:(("python3",pid=4200,fd=5))
```

---

# 76. Find Process Using Port 8000

## Command

```bash
sudo ss -lntp | grep :8000
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8000 0.0.0.0:* users:(("python3",pid=4200,fd=5))
```

---

# 77. Find Process Using Port with lsof

## Command

```bash
sudo lsof -i :8000
```

## Example Output

```text
COMMAND  PID USER   FD   TYPE DEVICE NAME
python3 4200 root   5u   IPv4 12345  TCP *:8000 (LISTEN)
```

---

# 78. Show All Network Connections of Process

## Command

```bash
sudo lsof -Pan -p 4200 -i
```

## Example Output

```text
COMMAND  PID USER   FD TYPE DEVICE NAME
python3 4200 root   5u IPv4      TCP *:8000 (LISTEN)
```

---

# 79. Show Established Connections

## Command

```bash
sudo ss -ntp state established
```

## Example Output

```text
ESTAB 0 0 10.0.0.10:8000 10.0.0.20:53210 users:(("python3",pid=4200,fd=6))
```

---

# ⚡ Process Priority

# 80. Check Process Priority

## Command

```bash
ps -o pid,ni,pri,cmd -p 4200
```

## Example Output

```text
PID   NI PRI CMD
4200   0  20 python3 app.py
```

---

# 81. Start Process with Nice Value

## Command

```bash
nice -n 10 ./application.sh
```

## Example Output

```text
Application started
```

---

# 82. Start Background Process with Nice

## Command

```bash
nice -n 10 ./application.sh &
```

## Example Output

```text
[1] 4200
```

---

# 83. Change Process Priority

## Command

```bash
renice 10 -p 4200
```

## Example Output

```text
4200 (process ID) old priority 0, new priority 10
```

---

# 84. Check Nice Value

## Command

```bash
ps -o pid,ni,cmd -p 4200
```

## Example Output

```text
PID   NI CMD
4200  10 python3 app.py
```

---

# 🧵 Process Threads

# 85. Show Threads of Process

## Command

```bash
ps -T -p 4200
```

## Example Output

```text
PID  SPID TTY      TIME CMD
4200 4200 ?        00:00:20 python3
4200 4201 ?        00:00:10 python3
4200 4202 ?        00:00:05 python3
```

---

# 86. Count Process Threads

## Command

```bash
ps -o nlwp= -p 4200
```

## Example Output

```text
8
```

---

# 87. View Threads in top

## Command

```bash
top -H -p 4200
```

## Example Output

```text
PID   USER      %CPU COMMAND
4200  root       5.0 python3
4201  root      25.0 python3
4202  root       2.0 python3
```

`-H` displays individual threads.

---

# 🧟 Zombie Processes

# 88. Find Zombie Processes

## Command

```bash
ps aux | awk '$8 ~ /^Z/'
```

## Example Output

```text
user 5200 0.0 0.0 0 0 ? Z 08:20 0:00 [worker] <defunct>
```

---

# 89. Find Zombie Processes with ps

## Command

```bash
ps -eo pid,ppid,stat,cmd | grep ' Z'
```

## Example Output

```text
5200 5100 Z [worker] <defunct>
```

---

# 90. Find Defunct Processes

## Command

```bash
ps -ef | grep defunct
```

## Example Output

```text
user 5200 5100 0 08:20 ? 00:00:00 [worker] <defunct>
```

---

# 91. Find Parent of Zombie

## Command

```bash
ps -o pid,ppid,stat,cmd -p 5200
```

## Example Output

```text
PID  PPID STAT CMD
5200 5100 Z    [worker] <defunct>
```

Investigate the parent process rather than trying to kill the zombie itself.

---

# 👻 Orphan Processes

# 92. Find Processes with PID 1 as Parent

## Command

```bash
ps -eo pid,ppid,cmd | awk '$2 == 1'
```

## Example Output

```text
4200 1 python3 worker.py
4300 1 nginx
```

A process with PPID 1 may have been re-parented after its original parent exited. Not every process with PPID 1 is an orphan in the problematic sense.

---

# 🛑 Process Limits

# 93. Display Shell Resource Limits

## Command

```bash
ulimit -a
```

## Example Output

```text
open files                      (-n) 1024
max user processes              (-u) 15000
stack size              (kbytes, -s) 8192
core file size          (blocks, -c) 0
```

---

# 94. Check Maximum User Processes

## Command

```bash
ulimit -u
```

## Example Output

```text
15000
```

---

# 95. Check Maximum Open Files

## Command

```bash
ulimit -n
```

## Example Output

```text
1024
```

---

# 96. Check Kernel PID Limit

## Command

```bash
cat /proc/sys/kernel/pid_max
```

## Example Output

```text
4194304
```

---

# 97. Check Maximum Threads

## Command

```bash
cat /proc/sys/kernel/threads-max
```

## Example Output

```text
123456
```

---

# 💤 nohup and Long-Running Processes

# 98. Run Process with nohup

## Command

```bash
nohup ./application.sh &
```

## Example Output

```text
[1] 5000
nohup: ignoring input and appending output to 'nohup.out'
```

---

# 99. Redirect nohup Output

## Command

```bash
nohup ./application.sh > application.log 2>&1 &
```

## Example Output

```text
[1] 5000
```

---

# 100. Check nohup Process

## Command

```bash
pgrep -af application.sh
```

## Example Output

```text
5000 /bin/bash ./application.sh
```

---

# 🔄 Process State and Runtime

# 101. Display Process State

## Command

```bash
ps -eo pid,ppid,stat,cmd
```

## Example Output

```text
PID  PPID STAT CMD
1      0 Ss   /sbin/init
850    1 S    nginx
4200   1 R    python3 app.py
```

---

# 102. Display Process Runtime

## Command

```bash
ps -eo pid,etime,cmd
```

## Example Output

```text
PID  ELAPSED CMD
850  01:25   nginx
4200 02:15   python3 app.py
```

---

# 103. Display Process Start Time

## Command

```bash
ps -eo pid,lstart,cmd
```

## Example Output

```text
PID  STARTED                  CMD
850  Wed Aug 26 07:31:20 2026 nginx
```

---

# 104. Display CPU Time Used by Process

## Command

```bash
ps -eo pid,time,cmd
```

## Example Output

```text
PID  TIME     CMD
4200 00:05:20 python3 app.py
```

---

# 🧰 systemd Process Management

# 105. Check Service Status

## Command

```bash
systemctl status nginx
```

## Example Output

```text
● nginx.service - A high performance web server
     Loaded: loaded
     Active: active (running)
     Main PID: 850 (nginx)
```

---

# 106. Find Main PID of Service

## Command

```bash
systemctl show nginx -p MainPID
```

## Example Output

```text
MainPID=850
```

---

# 107. Display Service Processes

## Command

```bash
systemctl status nginx
```

## Example Output

```text
Main PID: 850
Tasks: 3
Memory: 20M
CPU: 2s
```

---

# 108. List Running Services

## Command

```bash
systemctl list-units --type=service --state=running
```

## Example Output

```text
UNIT             LOAD   ACTIVE SUB     DESCRIPTION
nginx.service    loaded active running A high performance web server
ssh.service      loaded active running OpenBSD Secure Shell server
```

---

# 109. List Failed Services

## Command

```bash
systemctl --failed
```

## Example Output

```text
UNIT                  LOAD   ACTIVE SUB    DESCRIPTION
application.service   loaded failed failed Application Service
```

---

# 110. View Service Processes

## Command

```bash
systemctl status application
```

## Example Output

```text
Main PID: 4200
Tasks: 8
Memory: 450M
CPU: 2min
```

---

# 111. View Service Logs

## Command

```bash
journalctl -u application
```

## Example Output

```text
Aug 26 08:00:01 server application[4200]: Application started
Aug 26 08:01:10 server application[4200]: Listening on port 8000
```

---

# 112. Follow Service Logs

## Command

```bash
journalctl -u application -f
```

## Example Output

```text
Aug 26 08:15:10 server application[4200]: Request received
Aug 26 08:15:12 server application[4200]: Request completed
```

Press `Ctrl + C` to exit.

---

# 113. Show Recent Service Logs

## Command

```bash
journalctl -u application -n 100
```

## Example Output

```text
Aug 26 08:10:01 server application[4200]: Started
Aug 26 08:11:20 server application[4200]: Request received
```

---

# 🔍 Advanced Process Investigation

# 114. Display Detailed Process Information

## Command

```bash
ps -p 4200 -o pid,ppid,user,group,etime,lstart,stat,%cpu,%mem,rss,vsz,nlwp,cmd
```

## Example Output

```text
PID  PPID USER GROUP ELAPSED STAT %CPU %MEM RSS VSZ NLWP CMD
4200 1 root root 02:15 S 4.5 8.2 450000 800000 8 python3 app.py
```

---

# 115. Find Processes by Command

## Command

```bash
pgrep -af "python3"
```

## Example Output

```text
4200 python3 app.py
4300 python3 worker.py
```

---

# 116. Find Processes by User

## Command

```bash
pgrep -u khushboo
```

## Example Output

```text
2451
2500
2600
```

---

# 117. Find Processes by Parent PID

## Command

```bash
pgrep -P 4200
```

## Example Output

```text
4201
4202
```

---

# 118. Show Process Group ID

## Command

```bash
ps -o pid,ppid,pgid,sid,cmd -p 4200
```

## Example Output

```text
PID  PPID PGID SID CMD
4200 1    4200 4200 python3 app.py
```

---

# 119. Show Session ID

## Command

```bash
ps -o pid,sid,cmd -p 4200
```

## Example Output

```text
PID  SID CMD
4200 4200 python3 app.py
```

---

# 120. Find Process Group

## Command

```bash
ps -eo pid,pgid,cmd
```

## Example Output

```text
PID  PGID CMD
4200 4200 python3 app.py
4201 4200 python3 worker.py
```

---

# 121. Check Process Capabilities

## Command

```bash
sudo cat /proc/4200/status | grep Cap
```

## Example Output

```text
CapInh: 0000000000000000
CapPrm: 0000000000000000
CapEff: 0000000000000000
```

---

# 122. Check Process User and Group IDs

## Command

```bash
grep -E '^(Uid|Gid):' /proc/4200/status
```

## Example Output

```text
Uid: 1000 1000 1000 1000
Gid: 1000 1000 1000 1000
```

---

# 123. Check Process CPU Affinity

## Command

```bash
taskset -cp 4200
```

## Example Output

```text
pid 4200's current affinity list: 0-7
```

---

# 124. Set CPU Affinity

## Command

```bash
sudo taskset -cp 0-3 4200
```

## Example Output

```text
pid 4200's new affinity list: 0-3
```

Use CPU affinity carefully in production environments.

---

# 125. Display Process Scheduling Policy

## Command

```bash
chrt -p 4200
```

## Example Output

```text
pid 4200's current scheduling policy: SCHED_OTHER
pid 4200's current scheduling priority: 0
```

---

# 126. Display Process Resource Usage

## Command

```bash
/usr/bin/time -v sleep 5
```

## Example Output

```text
User time (seconds): 0.00
System time (seconds): 0.00
Maximum resident set size (kbytes): 1500
Exit status: 0
```

---

# 127. Trace Process System Calls

## Command

```bash
sudo strace -p 4200
```

## Example Output

```text
read(5, "data", 4096) = 1024
poll([{fd=5, events=POLLIN}], 1, 1000) = 0
```

`strace` is useful for advanced troubleshooting.

Press `Ctrl + C` to stop tracing.

---

# 128. Trace a New Process

## Command

```bash
strace -f ./application.sh
```

## Example Output

```text
execve("./application.sh", ["./application.sh"], ...) = 0
openat(...)
read(...)
write(...)
```

---

# 129. Check System Calls of a Process

## Command

```bash
sudo strace -p 4200 -f
```

## Example Output

```text
futex(...)
epoll_wait(...)
read(...)
write(...)
```

Use `strace` carefully on production systems because tracing can add overhead.

---

# 🧪 Practical Process Management Labs

# 130. Create a Test Background Process

## Command

```bash
sleep 300 &
```

## Example Output

```text
[1] 5000
```

---

# 131. Find the Test Process

## Command

```bash
pgrep sleep
```

## Example Output

```text
5000
```

---

# 132. Inspect the Test Process

## Command

```bash
ps -p 5000 -f
```

## Example Output

```text
UID       PID  PPID C STIME TTY TIME CMD
khushboo 5000 2451 0 08:30 pts/0 00:00:00 sleep 300
```

---

# 133. Check Process Tree

## Command

```bash
pstree -p 5000
```

## Example Output

```text
sleep(5000)
```

---

# 134. Terminate Test Process

## Command

```bash
kill 5000
```

## Example Output

```text
```

---

# 135. Verify Process Is Gone

## Command

```bash
pgrep sleep
```

## Example Output

```text
```

---

# 🚨 DevOps Troubleshooting Workflow

When an application is not working, use the following process investigation workflow.

# 136. Check Whether Application Is Running

## Command

```bash
pgrep -af application
```

## Example Output

```text
4200 python3 application.py
```

---

# 137. Find PID

## Command

```bash
pidof application
```

## Example Output

```text
4200
```

---

# 138. Inspect Process

## Command

```bash
ps -p 4200 -f
```

## Example Output

```text
UID   PID  PPID C STIME TTY TIME CMD
root 4200    1 0 08:00 ? 00:00:10 application
```

---

# 139. Check CPU

## Command

```bash
ps -p 4200 -o pid,%cpu,%mem,cmd
```

## Example Output

```text
PID  %CPU %MEM CMD
4200 95.5  8.2 application
```

---

# 140. Check Memory

## Command

```bash
ps -p 4200 -o pid,%mem,rss,vsz,cmd
```

## Example Output

```text
PID  %MEM RSS    VSZ    CMD
4200 8.2  450000 800000 application
```

---

# 141. Check Process Tree

## Command

```bash
pstree -p 4200
```

## Example Output

```text
application(4200)─┬─worker(4201)
                  └─worker(4202)
```

---

# 142. Check Open Files

## Command

```bash
sudo lsof -p 4200
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NAME
application 4200 root cwd DIR 8,1 /opt/application
```

---

# 143. Check Network Ports

## Command

```bash
sudo ss -lntp
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8000 0.0.0.0:* users:(("application",pid=4200,fd=5))
```

---

# 144. Check Application Logs

## Command

```bash
journalctl -u application -n 100
```

## Example Output

```text
Aug 26 08:00:01 server application[4200]: Application started
Aug 26 08:01:10 server application[4200]: Listening on port 8000
```

---

# 145. Check Service Status

## Command

```bash
systemctl status application
```

## Example Output

```text
● application.service
     Loaded: loaded
     Active: active (running)
     Main PID: 4200
```

---

# 🔥 Common Production Problems

# 146. Port Already in Use

## Command

```bash
sudo ss -lntp | grep :8000
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8000 users:(("python3",pid=4200,fd=5))
```

Then:

## Command

```bash
sudo lsof -i :8000
```

## Example Output

```text
python3 4200 root 5u TCP *:8000 (LISTEN)
```

Then:

## Command

```bash
ps -p 4200 -f
```

## Example Output

```text
UID PID PPID CMD
root 4200 1 python3 app.py
```

---

# 147. High CPU

## Command

```bash
top
```

## Example Output

```text
PID USER %CPU COMMAND
4200 root 95.5 python3
```

Then:

## Command

```bash
ps aux --sort=-%cpu | head
```

## Example Output

```text
root 4200 95.5 4.2 python3 app.py
```

Then:

## Command

```bash
ps -p 4200 -f
```

## Example Output

```text
UID PID PPID CMD
root 4200 1 python3 app.py
```

---

# 148. High Memory

## Command

```bash
free -h
```

## Example Output

```text
               total        used        free
Mem:           7.8Gi       6.2Gi       1.1Gi
```

Then:

## Command

```bash
ps aux --sort=-%mem | head
```

## Example Output

```text
mysql 1500 2.0 18.0 mysqld
root  4200 5.0  8.5 python3 app.py
```

---

# 149. Service Is Down

## Command

```bash
systemctl status application
```

## Example Output

```text
Active: failed (Result: exit-code)
```

Then:

## Command

```bash
systemctl --failed
```

## Example Output

```text
application.service loaded failed failed Application Service
```

Then:

## Command

```bash
journalctl -u application -n 100
```

## Example Output

```text
Application failed to start
Port 8000 already in use
```

---

# 150. Too Many Processes

## Command

```bash
ps -e --no-headers | wc -l
```

## Example Output

```text
152
```

Then:

## Command

```bash
ps -eo user= | sort | uniq -c | sort -nr
```

## Example Output

```text
80 root
35 khushboo
20 www-data
10 mysql
```

Then:

## Command

```bash
ulimit -u
```

## Example Output

```text
15000
```

---

# 151. Zombie Processes

## Command

```bash
ps -eo pid,ppid,stat,cmd | grep ' Z'
```

## Example Output

```text
5200 5100 Z [worker] <defunct>
```

Find parent:

## Command

```bash
ps -o pid,ppid,stat,cmd -p 5200
```

## Example Output

```text
PID  PPID STAT CMD
5200 5100 Z    [worker] <defunct>
```

Then investigate the parent process.

---

# 📋 Process States

Linux processes can have different states.

# 152. Check Process States

## Command

```bash
ps -eo pid,stat,cmd
```

## Example Output

```text
PID  STAT CMD
1    Ss   systemd
850  S    nginx
4200 R    python3 app.py
5200 Z    [worker] <defunct>
```

## Process State Reference

```text
R  Running
S  Interruptible sleep
D  Uninterruptible sleep
T  Stopped
Z  Zombie
I  Idle kernel thread
```

---

# 📚 Important Process Management Commands

# 153. ps

## Command

```bash
ps
```

## Example Output

```text
PID TTY          TIME CMD
2451 pts/0    00:00:00 bash
```

Purpose: Display processes.

---

# 154. pgrep

## Command

```bash
pgrep nginx
```

## Example Output

```text
850
851
852
```

Purpose: Find processes by name.

---

# 155. pidof

## Command

```bash
pidof nginx
```

## Example Output

```text
852 851 850
```

Purpose: Find PID by program name.

---

# 156. pstree

## Command

```bash
pstree -p
```

## Example Output

```text
systemd(1)
└─nginx(850)─┬─nginx(851)
             └─nginx(852)
```

Purpose: Display process hierarchy.

---

# 157. top

## Command

```bash
top
```

## Example Output

```text
PID USER %CPU %MEM COMMAND
4200 root 95.5 8.2 python3
```

Purpose: Real-time process monitoring.

---

# 158. htop

## Command

```bash
htop
```

## Example Output

```text
PID USER CPU% MEM% COMMAND
4200 root 5.0 8.2 python3
```

Purpose: Interactive process monitoring.

---

# 159. kill

## Command

```bash
kill 4200
```

## Example Output

```text
```

Purpose: Send a signal to a process.

---

# 160. pkill

## Command

```bash
pkill nginx
```

## Example Output

```text
```

Purpose: Kill processes by name or pattern.

---

# 161. jobs

## Command

```bash
jobs
```

## Example Output

```text
[1]+ Running sleep 300 &
```

Purpose: Display shell jobs.

---

# 162. fg

## Command

```bash
fg %1
```

## Example Output

```text
sleep 300
```

Purpose: Bring a background job to the foreground.

---

# 163. bg

## Command

```bash
bg %1
```

## Example Output

```text
[1]+ sleep 300 &
```

Purpose: Send a stopped job to the background.

---

# 164. wait

## Command

```bash
wait 4200
```

## Example Output

```text
```

Purpose: Wait for a process to finish.

---

# 165. nohup

## Command

```bash
nohup ./application.sh &
```

## Example Output

```text
[1] 5000
nohup: ignoring input and appending output to 'nohup.out'
```

Purpose: Keep a process running after logout.

---

# 166. nice

## Command

```bash
nice -n 10 ./application.sh
```

## Example Output

```text
Application started
```

Purpose: Start a process with a specified priority.

---

# 167. renice

## Command

```bash
renice 10 -p 4200
```

## Example Output

```text
4200 (process ID) old priority 0, new priority 10
```

Purpose: Change process priority.

---

# 168. lsof

## Command

```bash
lsof -p 4200
```

## Example Output

```text
python3 4200 root cwd DIR /opt/application
```

Purpose: List open files.

---

# 169. ss

## Command

```bash
sudo ss -lntp
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8000 users:(("python3",pid=4200,fd=5))
```

Purpose: Display sockets and network ports.

---

# 170. watch

## Command

```bash
watch -n 2 'ps -p 4200 -f'
```

## Example Output

```text
Every 2.0s:

PID  PPID CMD
4200 1    python3 app.py
```

Purpose: Repeat a command continuously.

---

# 171. systemctl

## Command

```bash
systemctl status nginx
```

## Example Output

```text
Active: active (running)
Main PID: 850
```

Purpose: Manage systemd services.

---

# 172. journalctl

## Command

```bash
journalctl -u nginx -n 100
```

## Example Output

```text
Aug 26 08:00:01 server nginx[850]: Started
```

Purpose: View service logs.

---

# 173. ulimit

## Command

```bash
ulimit -a
```

## Example Output

```text
open files (-n) 1024
max user processes (-u) 15000
```

Purpose: Display resource limits.

---

# 174. taskset

## Command

```bash
taskset -cp 4200
```

## Example Output

```text
pid 4200's current affinity list: 0-7
```

Purpose: Manage CPU affinity.

---

# 175. chrt

## Command

```bash
chrt -p 4200
```

## Example Output

```text
pid 4200's current scheduling policy: SCHED_OTHER
pid 4200's current scheduling priority: 0
```

Purpose: Manage process scheduling policy.

---

# 176. strace

## Command

```bash
sudo strace -p 4200
```

## Example Output

```text
read(5, "data", 4096) = 1024
poll([{fd=5, events=POLLIN}], 1, 1000) = 0
```

Purpose: Trace system calls.

---

# 177. killall

## Command

```bash
killall nginx
```

## Example Output

```text
```

Purpose: Terminate processes by exact process name. Use carefully.

---

# 178. /proc/PID

## Command

```bash
ls /proc/4200
```

## Example Output

```text
cmdline
cwd
environ
exe
fd
maps
status
limits
io
sched
```

Purpose: Access detailed kernel-provided information about a process.

---

# 🧠 Important Concepts

# 179. PID

## Command

```bash
echo $$
```

## Example Output

```text
4200
```

A **PID** is the Process ID assigned to a running process.

---

# 180. PPID

## Command

```bash
echo $PPID
```

## Example Output

```text
2400
```

A **PPID** is the Parent Process ID.

---

# 181. Foreground Process

## Command

```bash
ping google.com
```

## Example Output

```text
PING google.com ...
64 bytes from ...
```

A foreground process is attached to the current terminal and normally blocks the shell until it finishes.

---

# 182. Background Process

## Command

```bash
ping google.com &
```

## Example Output

```text
[1] 4200
```

A background process runs without blocking the terminal.

---

# 183. Zombie Process

## Command

```bash
ps -eo pid,ppid,stat,cmd | grep ' Z'
```

## Example Output

```text
5200 5100 Z [worker] <defunct>
```

A zombie process has completed but its parent has not collected its exit status.

---

# 184. Orphan Process

## Command

```bash
ps -eo pid,ppid,cmd | awk '$2 == 1'
```

## Example Output

```text
4200 1 python3 worker.py
```

An orphan process is a process whose original parent has exited and which has been re-parented.

---

# 185. Process Priority

## Command

```bash
ps -eo pid,ni,pri,cmd
```

## Example Output

```text
PID  NI PRI CMD
4200 0  20  python3 app.py
```

Process priority controls how the scheduler treats processes relative to each other.

---

# 186. Check Process Priority

## Command

```bash
ps -eo pid,ni,pri,cmd
```

## Example Output

```text
PID  NI PRI CMD
4200 10 30  python3 app.py
```

---

# 187. Complete Process Investigation Example

## Command

```bash
pgrep -af application
pidof application
ps -p 4200 -f
ps -p 4200 -o pid,%cpu,%mem,cmd
pstree -p 4200
sudo lsof -p 4200
sudo ss -lntp
journalctl -u application -n 100
systemctl status application
```

## Example Output

```text
4200 python3 application.py
4200
UID PID PPID CMD
root 4200 1 python3 application.py

PID  %CPU %MEM CMD
4200 4.5  8.2  python3 application.py

application(4200)─┬─worker(4201)
                  └─worker(4202)

python3 4200 root cwd DIR /opt/application

LISTEN 0 128 0.0.0.0:8000 users:(("python3",pid=4200,fd=5))

Application started
Listening on port 8000

Active: active (running)
Main PID: 4200
```

This workflow is useful for DevOps production troubleshooting when an application is slow, consuming high CPU/memory, not listening on the expected port, or failing under systemd.

---
