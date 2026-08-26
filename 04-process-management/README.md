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
$$ represents the PID of the current shell.

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

$PPID represents the parent process ID.

---

3. Display Current Shell
Command
echo $SHELL
Example Output
/bin/bash
4. Display Current User
Command
whoami
Example Output
khushboo
5. Display Running Processes
Command
ps
Example Output
    PID TTY          TIME CMD
   2451 pts/0    00:00:00 bash
   3200 pts/0    00:00:00 ps
6. Display All Processes
Command
ps -e
Example Output
    PID TTY          TIME CMD
      1 ?        00:00:02 systemd
    850 ?        00:00:05 nginx
   2451 pts/0    00:00:00 bash
7. Display All Processes in Full Format
Command
ps -ef
Example Output
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 07:30 ?        00:00:02 /sbin/init
root         850       1  0 07:31 ?        00:00:05 nginx
khushboo    2451    2400  0 07:40 pts/0    00:00:00 bash
8. Display All Processes with User Information
Command
ps aux
Example Output
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1  22560 10560 ?        Ss   07:30   0:02 /sbin/init
root         850  0.1  0.5 123456 45678 ?       S    07:31   0:05 nginx
khushboo    2451  0.0  0.1  15000  5000 pts/0  Ss   07:40   0:00 bash
9. Display Processes for Current User
Command
ps -u "$USER"
Example Output
    PID TTY          TIME CMD
   2451 pts/0    00:00:00 bash
   3200 pts/0    00:00:00 ps
10. Display Processes for a Specific User
Command
ps -u root
Example Output
    PID TTY          TIME CMD
      1 ?        00:00:02 systemd
    850 ?        00:00:05 nginx
🔎 Finding Processes
11. Find Process by Name
Command
pgrep nginx
Example Output
850
851
852
12. Find Process and Command
Command
pgrep -af nginx
Example Output
850 nginx: master process /usr/sbin/nginx
851 nginx: worker process
852 nginx: worker process
13. Find PID Using pidof
Command
pidof nginx
Example Output
852 851 850
14. Search Process Using grep
Command
ps aux | grep nginx
Example Output
root       850  0.0  0.5 123456 45678 ?       S    07:31   0:05 nginx
root       851  0.0  0.5 123456 45678 ?       S    07:31   0:05 nginx
15. Search Process Without Showing grep
Command
ps aux | grep '[n]ginx'
Example Output
root       850  0.0  0.5 123456 45678 ?       S    07:31   0:05 nginx
16. Check a Specific Process
Command
ps -p 850
Example Output
    PID TTY          TIME CMD
    850 ?        00:00:05 nginx
17. Check Detailed Process Information
Command
ps -p 850 -f
Example Output
UID          PID    PPID  C STIME TTY          TIME CMD
root         850       1  0 07:31 ?        00:00:05 nginx
18. Display Selected Process Columns
Command
ps -o pid,ppid,user,stat,%cpu,%mem,cmd -p 850
Example Output
    PID    PPID USER       STAT %CPU %MEM CMD
    850       1 root       S     0.1  0.5 nginx
🌳 Process Hierarchy
19. Display Process Tree
Command
pstree
Example Output
systemd
├─sshd
│ └─bash
│   └─pstree
├─nginx
│ ├─nginx
│ └─nginx
└─cron
20. Display Process Tree with PIDs
Command
pstree -p
Example Output
systemd(1)
├─sshd(1200)
│ └─bash(2451)
└─nginx(850)─┬─nginx(851)
             └─nginx(852)
21. Display Children of a Process
Command
pgrep -P 850
Example Output
851
852

-P searches for child processes of the specified PID.

22. Display Parent Process
Command
ps -o pid,ppid,cmd -p 850
Example Output
PID  PPID CMD
850    1 nginx
23. Display PID and PPID for All Processes
Command
ps -eo pid,ppid,cmd
Example Output
PID    PPID CMD
1         0 /sbin/init
850       1 nginx
2451   2400 bash
📊 Process Monitoring
24. Monitor Processes in Real Time
Command
top
Example Output
top - 08:15:10 up 10:45, 1 user, load average: 0.12, 0.08, 0.05

Tasks: 150 total, 1 running, 149 sleeping

%Cpu(s): 5.0 us, 2.0 sy, 0.0 ni, 92.0 id

MiB Mem : 7800.0 total, 2100.0 used, 5700.0 free

PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM COMMAND
850 root      20   0  123456  45678  12000 S   5.0  0.5 nginx

Press q to exit.

25. Sort top by CPU Usage
Command
top

Then press:

P

Processes are sorted by CPU usage.

26. Sort top by Memory Usage
Command
top

Then press:

M

Processes are sorted by memory usage.

27. Sort top by Process ID
Command
top

Then press:

N
28. Display Interactive Process Monitor
Command
htop
Example Output
CPU[||||||||        ] 15.0%
Mem[|||||||||       ] 35.0%

PID   USER       CPU%  MEM%  COMMAND
850   root        5.0   0.5  nginx
2451  khushboo    0.2   0.1  bash

htop may need to be installed separately.

29. Show Processes Sorted by CPU
Command
ps aux --sort=-%cpu | head
Example Output
USER       PID %CPU %MEM COMMAND
root      4200 95.5  4.2 python3 app.py
mysql     1500  5.0  8.0 mysqld
30. Show Processes Sorted by Memory
Command
ps aux --sort=-%mem | head
Example Output
USER       PID %CPU %MEM COMMAND
mysql     1500  2.0 18.0 mysqld
root      4200  5.0  8.5 python3 app.py
31. Show Top CPU Processes
Command
ps -eo pid,user,%cpu,%mem,cmd --sort=-%cpu | head -11
Example Output
PID  USER  %CPU %MEM CMD
4200 root  95.5 4.2 python3 app.py
1500 mysql 5.0  8.0 mysqld
32. Show Top Memory Processes
Command
ps -eo pid,user,%cpu,%mem,cmd --sort=-%mem | head -11
Example Output
PID  USER  %CPU %MEM CMD
1500 mysql 2.0 18.0 mysqld
4200 root  5.0  8.5 python3 app.py
33. Monitor a Process Continuously
Command
watch -n 2 'ps -p 4200 -o pid,ppid,stat,%cpu,%mem,cmd'
Example Output
Every 2.0s:

PID  PPID STAT %CPU %MEM CMD
4200 1    S     4.5  8.2 python3 app.py

Press Ctrl + C to exit.

34. Count Running Processes
Command
ps -e --no-headers | wc -l
Example Output
152
35. Count Processes by User
Command
ps -eo user= | sort | uniq -c | sort -nr
Example Output
80 root
35 khushboo
20 www-data
10 mysql
🏃 Foreground and Background Processes
36. Run a Process in Foreground
Command
sleep 60
Example Output

The terminal remains occupied until the command finishes.

37. Run a Process in Background
Command
sleep 300 &
Example Output
[1] 4200
38. Display Background Jobs
Command
jobs
Example Output
[1]+  Running                 sleep 300 &
39. Display Jobs with PIDs
Command
jobs -l
Example Output
[1]+ 4200 Running                 sleep 300 &
40. Bring Background Job to Foreground
Command
fg %1
Example Output
sleep 300
41. Send Foreground Process to Background

First press:

Ctrl + Z

Example:

^Z
[1]+  Stopped sleep 300

Then:

bg %1
Example Output
[1]+ sleep 300 &
42. Stop Foreground Process
Command
Ctrl + C
Example Output
^C

Sends SIGINT.

43. Suspend Foreground Process
Command
Ctrl + Z
Example Output
^Z
[1]+  Stopped

Sends SIGTSTP.

44. Wait for Background Process
Command
wait
Example Output
45. Wait for Specific Process
Command
wait 4200
Example Output
🔔 Linux Signals
46. List Available Signals
Command
kill -l
Example Output
1) SIGHUP
2) SIGINT
3) SIGQUIT
9) SIGKILL
15) SIGTERM
18) SIGCONT
19) SIGSTOP
47. Send SIGTERM
Command
kill -15 4200
Example Output

Requests graceful process termination.

48. Send SIGTERM by Name
Command
pkill -TERM nginx
Example Output
49. Send SIGKILL
Command
kill -9 4200
Example Output

Forcefully terminates the process.

50. Send SIGKILL by Name
Command
pkill -KILL nginx
Example Output

Use carefully because multiple matching processes can be terminated.

51. Send SIGSTOP
Command
kill -STOP 4200
Example Output

Immediately stops the process.

52. Send SIGCONT
Command
kill -CONT 4200
Example Output

Continues a stopped process.

53. Send SIGHUP
Command
kill -HUP 4200
Example Output

Some applications use SIGHUP to reload configuration.

54. Send SIGINT
Command
kill -INT 4200
Example Output

Similar to pressing Ctrl + C.

55. Kill Process by Name
Command
pkill nginx
Example Output

Use carefully because multiple processes may match.

56. Kill Exact Process Name
Command
pkill -x nginx
Example Output
57. Kill Process by Full Command Pattern
Command
pkill -f "python3 app.py"
Example Output

-f matches against the full command line.

58. Check Whether Process Exists
Command
pgrep nginx
Example Output
850
851
852

If nothing is returned:

The process may not be running.

📁 Process Information Using /proc
59. View Process Status
Command
cat /proc/4200/status
Example Output
Name:   python3
State:  S (sleeping)
Pid:    4200
PPid:   1
Uid:    1000
Gid:    1000
Threads:        8
60. View Process Command
Command
cat /proc/4200/cmdline
Example Output
python3app.py

/proc/<PID>/cmdline contains the command line used to start the process.

61. View Process Executable
Command
readlink -f /proc/4200/exe
Example Output
/usr/bin/python3.12
62. View Process Working Directory
Command
readlink -f /proc/4200/cwd
Example Output
/opt/application
63. View Process Root Directory
Command
readlink -f /proc/4200/root
Example Output
/
64. View Process Environment
Command
sudo tr '\0' '\n' < /proc/4200/environ
Example Output
PATH=/usr/local/bin:/usr/bin
HOME=/root
USER=root

Process environments may contain passwords, tokens, or other secrets. Do not expose them in logs or repositories.

65. View Process Memory Information
Command
cat /proc/4200/status | grep -E 'VmSize|VmRSS|VmPeak'
Example Output
VmPeak:  800000 kB
VmSize:  750000 kB
VmRSS:   450000 kB
66. View Process Memory Maps
Command
cat /proc/4200/maps
Example Output
7f0000000000-7f0000100000 r-xp /usr/lib/libexample.so
67. View Process File Descriptors
Command
ls -l /proc/4200/fd
Example Output
0 -> /dev/null
1 -> /var/log/application.log
2 -> /var/log/application-error.log
3 -> socket:[123456]
68. Count Process File Descriptors
Command
ls /proc/4200/fd | wc -l
Example Output
128
69. View Process Limits
Command
cat /proc/4200/limits
Example Output
Limit                     Soft Limit Hard Limit Units
Max open files            1024       4096       files
Max processes             15000      15000      processes
Max stack size             8388608    8388608    bytes
70. View Process IO Statistics
Command
cat /proc/4200/io
Example Output
rchar: 123456
wchar: 456789
read_bytes: 98765
write_bytes: 12345
71. View Process Scheduling Information
Command
cat /proc/4200/sched
Example Output
python3 (4200, #threads: 8)
se.exec_start : 123456789
se.vruntime : 987654
🔗 Open Files and Resources
72. Show Files Opened by Process
Command
lsof -p 4200
Example Output
COMMAND  PID USER   FD   TYPE DEVICE NAME
python3 4200 root  cwd    DIR  8,1   /opt/application
python3 4200 root  txt    REG  8,1   /usr/bin/python3
73. Find Process Using a File
Command
lsof /var/log/application.log
Example Output
COMMAND  PID USER   FD   TYPE NAME
python3 4200 root    1w  REG  /var/log/application.log
74. Find Process Using a Directory
Command
lsof +D /var/log
Example Output
python3 4200 root  1w REG /var/log/application.log

+D recursively searches the directory and may be expensive on large directory trees.

🌐 Process and Network Ports
75. Show Listening Ports
Command
sudo ss -lntp
Example Output
LISTEN 0 128 0.0.0.0:8000 0.0.0.0:* users:(("python3",pid=4200,fd=5))
76. Find Process Using Port 8000
Command
sudo ss -lntp | grep :8000
Example Output
LISTEN 0 128 0.0.0.0:8000 0.0.0.0:* users:(("python3",pid=4200,fd=5))
77. Find Process Using Port with lsof
Command
sudo lsof -i :8000
Example Output
COMMAND  PID USER   FD   TYPE DEVICE NAME
python3 4200 root    5u  IPv4 12345  TCP *:8000 (LISTEN)
78. Show All Network Connections of Process
Command
sudo lsof -Pan -p 4200 -i
Example Output
COMMAND  PID USER   FD TYPE DEVICE NAME
python3 4200 root    5u IPv4      TCP *:8000 (LISTEN)
79. Show Established Connections
Command
sudo ss -ntp state established
Example Output
ESTAB 0 0 10.0.0.10:8000 10.0.0.20:53210 users:(("python3",pid=4200,fd=6))
⚡ Process Priority
80. Check Process Priority
Command
ps -o pid,ni,pri,cmd -p 4200
Example Output
PID   NI PRI CMD
4200   0  20 python3 app.py
81. Start Process with Nice Value
Command
nice -n 10 ./application.sh
Example Output
Application started
82. Start Background Process with Nice
Command
nice -n 10 ./application.sh &
Example Output
[1] 4200
83. Change Process Priority
Command
renice 10 -p 4200
Example Output
4200 (process ID) old priority 0, new priority 10
84. Check Nice Value
Command
ps -o pid,ni,cmd -p 4200
Example Output
PID   NI CMD
4200  10 python3 app.py
🧵 Process Threads
85. Show Threads of Process
Command
ps -T -p 4200
Example Output
PID  SPID TTY      TIME CMD
4200 4200 ?        00:00:20 python3
4200 4201 ?        00:00:10 python3
4200 4202 ?        00:00:05 python3
86. Count Process Threads
Command
ps -o nlwp= -p 4200
Example Output
8
87. View Threads in top
Command
top -H -p 4200
Example Output
PID   USER      %CPU COMMAND
4200  root       5.0 python3
4201  root      25.0 python3
4202  root       2.0 python3

-H displays individual threads.

🧟 Zombie Processes
88. Find Zombie Processes
Command
ps aux | awk '$8 ~ /^Z/'
Example Output
user 5200 0.0 0.0 0 0 ? Z 08:20 0:00 [worker] <defunct>
89. Find Zombie Processes with ps
Command
ps -eo pid,ppid,stat,cmd | grep ' Z'
Example Output
5200 5100 Z [worker] <defunct>
90. Find Defunct Processes
Command
ps -ef | grep defunct
Example Output
user 5200 5100 0 08:20 ? 00:00:00 [worker] <defunct>
91. Find Parent of Zombie
Command
ps -o pid,ppid,stat,cmd -p 5200
Example Output
PID  PPID STAT CMD
5200 5100 Z    [worker] <defunct>

Investigate the parent process rather than trying to kill the zombie itself.

👻 Orphan Processes
92. Find Processes with PID 1 as Parent
Command
ps -eo pid,ppid,cmd | awk '$2 == 1'
Example Output
4200 1 python3 worker.py
4300 1 nginx

A process with PPID 1 may have been re-parented after its original parent exited. Not every process with PPID 1 is an orphan in the problematic sense.

🛑 Process Limits
93. Display Shell Resource Limits
Command
ulimit -a
Example Output
open files                      (-n) 1024
max user processes              (-u) 15000
stack size              (kbytes, -s) 8192
core file size          (blocks, -c) 0
94. Check Maximum User Processes
Command
ulimit -u
Example Output
15000
95. Check Maximum Open Files
Command
ulimit -n
Example Output
1024
96. Check Kernel PID Limit
Command
cat /proc/sys/kernel/pid_max
Example Output
4194304
97. Check Maximum Threads
Command
cat /proc/sys/kernel/threads-max
Example Output
123456
💤 nohup and Long-Running Processes
98. Run Process with nohup
Command
nohup ./application.sh &
Example Output
[1] 5000
nohup: ignoring input and appending output to 'nohup.out'
99. Redirect nohup Output
Command
nohup ./application.sh > application.log 2>&1 &
Example Output
[1] 5000
100. Check nohup Process
Command
pgrep -af application.sh
Example Output
5000 /bin/bash ./application.sh
🔄 Process State and Runtime
101. Display Process State
Command
ps -eo pid,ppid,stat,cmd
Example Output
PID  PPID STAT CMD
1      0 Ss   /sbin/init
850    1 S    nginx
4200   1 R    python3 app.py
102. Display Process Runtime
Command
ps -eo pid,etime,cmd
Example Output
PID  ELAPSED CMD
850  01:25   nginx
4200 02:15   python3 app.py
103. Display Process Start Time
Command
ps -eo pid,lstart,cmd
Example Output
PID  STARTED                  CMD
850  Wed Aug 26 07:31:20 2026 nginx
104. Display CPU Time Used by Process
Command
ps -eo pid,time,cmd
Example Output
PID  TIME     CMD
4200 00:05:20 python3 app.py
🧰 systemd Process Management
105. Check Service Status
Command
systemctl status nginx
Example Output
● nginx.service - A high performance web server
     Loaded: loaded
     Active: active (running)
     Main PID: 850 (nginx)
106. Find Main PID of Service
Command
systemctl show nginx -p MainPID
Example Output
MainPID=850
107. Display Service Processes
Command
systemctl status nginx
108. List Running Services
Command
systemctl list-units --type=service --state=running
Example Output
UNIT             LOAD   ACTIVE SUB     DESCRIPTION
nginx.service    loaded active running A high performance web server
ssh.service      loaded active running OpenBSD Secure Shell server
109. List Failed Services
Command
systemctl --failed
Example Output
UNIT                  LOAD   ACTIVE SUB    DESCRIPTION
application.service   loaded failed failed Application Service
110. View Service Processes
Command
systemctl status application
Example Output
Main PID: 4200
Tasks: 8
Memory: 450M
CPU: 2min
111. View Service Logs
Command
journalctl -u application
Example Output
Aug 26 08:00:01 server application[4200]: Application started
Aug 26 08:01:10 server application[4200]: Listening on port 8000
112. Follow Service Logs
Command
journalctl -u application -f
Example Output
Aug 26 08:15:10 server application[4200]: Request received
Aug 26 08:15:12 server application[4200]: Request completed

Press Ctrl + C to exit.

113. Show Recent Service Logs
Command
journalctl -u application -n 100
Example Output
Aug 26 08:10:01 server application[4200]: Started
Aug 26 08:11:20 server application[4200]: Request received
🔍 Advanced Process Investigation
114. Display Detailed Process Information
Command
ps -p 4200 -o pid,ppid,user,group,etime,lstart,stat,%cpu,%mem,rss,vsz,nlwp,cmd
Example Output
PID  PPID USER GROUP ELAPSED STAT %CPU %MEM RSS VSZ NLWP CMD
4200 1 root root 02:15 S 4.5 8.2 450000 800000 8 python3 app.py
115. Find Processes by Command
Command
pgrep -af "python3"
Example Output
4200 python3 app.py
4300 python3 worker.py
116. Find Processes by User
Command
pgrep -u khushboo
Example Output
2451
2500
2600
117. Find Processes by Parent PID
Command
pgrep -P 4200
Example Output
4201
4202
118. Show Process Group ID
Command
ps -o pid,ppid,pgid,sid,cmd -p 4200
Example Output
PID  PPID PGID SID CMD
4200 1    4200 4200 python3 app.py
119. Show Session ID
Command
ps -o pid,sid,cmd -p 4200
Example Output
PID  SID CMD
4200 4200 python3 app.py
120. Find Process Group
Command
ps -eo pid,pgid,cmd
Example Output
PID  PGID CMD
4200 4200 python3 app.py
4201 4200 python3 worker.py
121. Check Process Capabilities
Command
sudo cat /proc/4200/status | grep Cap
Example Output
CapInh: 0000000000000000
CapPrm: 0000000000000000
CapEff: 0000000000000000
122. Check Process User and Group IDs
Command
grep -E '^(Uid|Gid):' /proc/4200/status
Example Output
Uid: 1000 1000 1000 1000
Gid: 1000 1000 1000 1000
123. Check Process CPU Affinity
Command
taskset -cp 4200
Example Output
pid 4200's current affinity list: 0-7
124. Set CPU Affinity
Command
sudo taskset -cp 0-3 4200
Example Output
pid 4200's new affinity list: 0-3

Use CPU affinity carefully in production environments.

125. Display Process Scheduling Policy
Command
chrt -p 4200
Example Output
pid 4200's current scheduling policy: SCHED_OTHER
pid 4200's current scheduling priority: 0
126. Display Process Resource Usage
Command
/usr/bin/time -v sleep 5
Example Output
User time (seconds): 0.00
System time (seconds): 0.00
Maximum resident set size (kbytes): 1500
Exit status: 0
127. Trace Process System Calls
Command
sudo strace -p 4200
Example Output
read(5, "data", 4096) = 1024
poll([{fd=5, events=POLLIN}], 1, 1000) = 0

strace is useful for advanced troubleshooting.

Press Ctrl + C to stop tracing.

128. Trace a New Process
Command
strace -f ./application.sh
Example Output
execve("./application.sh", ["./application.sh"], ...) = 0
openat(...)
read(...)
write(...)
129. Check System Calls of a Process
Command
sudo strace -p 4200 -f
Example Output
futex(...)
epoll_wait(...)
read(...)
write(...)

Use strace carefully on production systems because tracing can add overhead.

🧪 Practical Process Management Labs
130. Create a Test Background Process
Command
sleep 300 &
Example Output
[1] 5000
131. Find the Test Process
Command
pgrep sleep
Example Output
5000
132. Inspect the Test Process
Command
ps -p 5000 -f
Example Output
UID       PID  PPID C STIME TTY TIME CMD
khushboo 5000 2451 0 08:30 pts/0 00:00:00 sleep 300
133. Check Process Tree
Command
pstree -p 5000
Example Output
sleep(5000)
134. Terminate Test Process
Command
kill 5000
Example Output
135. Verify Process Is Gone
Command
pgrep sleep
Example Output
🚨 DevOps Troubleshooting Workflow

When an application is not working, use the following process investigation workflow.

Step 1 - Check Whether Application Is Running
pgrep -af application
Step 2 - Find PID
pidof application
Step 3 - Inspect Process
ps -p PID -f
Step 4 - Check CPU
ps -p PID -o pid,%cpu,%mem,cmd
Step 5 - Check Memory
ps -p PID -o pid,%mem,rss,vsz,cmd
Step 6 - Check Process Tree
pstree -p PID
Step 7 - Check Open Files
sudo lsof -p PID
Step 8 - Check Network Ports
sudo ss -lntp
Step 9 - Check Application Logs
journalctl -u application -n 100
Step 10 - Check Service Status
systemctl status application
🔥 Common Production Problems
Problem 1 - Port Already in Use

Check:

sudo ss -lntp | grep :8000

Then:

sudo lsof -i :8000

Then:

ps -p PID -f
Problem 2 - High CPU

Check:

top

Then:

ps aux --sort=-%cpu | head

Then:

ps -p PID -f
Problem 3 - High Memory

Check:

free -h

Then:

ps aux --sort=-%mem | head
Problem 4 - Service Is Down

Check:

systemctl status application

Then:

systemctl --failed

Then:

journalctl -u application -n 100
Problem 5 - Too Many Processes

Check:

ps -e --no-headers | wc -l

Then:

ps -eo user= | sort | uniq -c | sort -nr

Then:

ulimit -u
Problem 6 - Zombie Processes

Check:

ps -eo pid,ppid,stat,cmd | grep ' Z'

Find parent:

ps -o pid,ppid,stat,cmd -p PID

Then investigate the parent process.

📋 Process States

Linux processes can have different states.

R  Running
S  Interruptible sleep
D  Uninterruptible sleep
T  Stopped
Z  Zombie
I  Idle kernel thread

Check:

ps -eo pid,stat,cmd

Example:

PID  STAT CMD
1    Ss   systemd
850  S    nginx
4200 R    python3 app.py
5200 Z    [worker] <defunct>
📚 Important Process Management Commands
Command	Purpose
ps	Display processes
ps aux	Display all processes
ps -ef	Full process listing
pgrep	Find process by name
pidof	Find PID by program
pstree	Display process hierarchy
top	Real-time process monitoring
htop	Interactive process monitoring
kill	Send signal to process
pkill	Kill processes by name
jobs	Display shell jobs
fg	Bring job to foreground
bg	Send job to background
wait	Wait for process
nohup	Keep process running after logout
nice	Start process with priority
renice	Change process priority
lsof	List open files
ss	Display sockets
watch	Repeat command
systemctl	Manage services
journalctl	View service logs
ulimit	Display resource limits
taskset	Manage CPU affinity
chrt	Manage scheduling policy
strace	Trace system calls
killall	Kill processes by name
/proc/PID	Process information
🧠 Important Concepts
PID

Process ID.

4200
PPID

Parent Process ID.

PID  = 4200
PPID = 1
Foreground Process

A process attached to the current terminal.

ping google.com
Background Process

A process running without blocking the terminal.

ping google.com &
Zombie Process

A process that has completed but whose parent has not collected its exit status.

[worker] <defunct>
Orphan Process

A process whose original parent has exited and which has been re-parented.

Process Priority

Controls how the scheduler treats processes relative to each other.

Check:

ps -eo pid,ni,pri,cmd
