# 📌 Linux Logging & Log Management
---

# 1. List Log Directory

## Command

```bash
ls -lh /var/log
```

## Example Output

```text
total 12M
-rw-r----- 1 syslog adm  25K Aug 27 10:00 auth.log
-rw-r----- 1 syslog adm 150K Aug 27 10:00 syslog
-rw-r----- 1 syslog adm  80K Aug 27 10:00 kern.log
drwxr-xr-x 2 root   root 4.0K Aug 27 09:00 nginx
```

`/var/log` contains many system and application log files.

---

# 2. Display System Log

## Command

```bash
cat /var/log/syslog
```

## Example Output

```text
Aug 27 10:00:01 devops-server systemd[1]: Started Session.
Aug 27 10:01:10 devops-server sshd[1234]: Accepted publickey.
```

---

# 3. Display Authentication Logs

## Command

```bash
sudo cat /var/log/auth.log
```

## Example Output

```text
Aug 27 10:10:01 devops-server sshd[1234]: Accepted publickey
Aug 27 10:11:20 devops-server sudo: devops : TTY=pts/0
```

---

# 4. Display Kernel Logs

## Command

```bash
sudo cat /var/log/kern.log
```

## Example Output

```text
Aug 27 10:00:00 devops-server kernel: Linux version 6.8.0
Aug 27 10:02:00 devops-server kernel: eth0: Link is Up
```

---

# 5. Read Log File Using less

## Command

```bash
less /var/log/syslog
```

## Example Output

```text
Aug 27 10:00:01 devops-server systemd[1]: Started service.
Aug 27 10:01:01 devops-server CRON[1234]: CMD (/usr/bin/test)
```

Press `q` to exit.

---

# 6. Display Last 10 Log Lines

## Command

```bash
tail /var/log/syslog
```

## Example Output

```text
Aug 27 10:09:01 devops-server systemd[1]: Started service.
Aug 27 10:10:01 devops-server systemd[1]: Service running.
```

---

# 7. Display Last 50 Log Lines

## Command

```bash
tail -n 50 /var/log/syslog
```

## Example Output

```text
Aug 27 10:00:01 systemd: Started service.
Aug 27 10:01:01 systemd: Service running.
...
Aug 27 10:10:01 systemd: Service stopped.
```

---

# 8. Display First 10 Log Lines

## Command

```bash
head /var/log/syslog
```

## Example Output

```text
Aug 27 00:00:01 devops-server systemd[1]: Started system.
Aug 27 00:01:01 devops-server systemd[1]: Started cron.
```

---

# 9. Display First 50 Log Lines

## Command

```bash
head -n 50 /var/log/syslog
```

## Example Output

```text
Aug 27 00:00:01 systemd: Started service.
Aug 27 00:01:01 systemd: Started cron.
```

---

# 10. Monitor Log File in Real Time

## Command

```bash
tail -f /var/log/syslog
```

## Example Output

```text
Aug 27 10:20:01 devops-server systemd[1]: Started service.
Aug 27 10:20:02 devops-server nginx[1234]: 200 GET /
Aug 27 10:20:03 devops-server sshd[5678]: Accepted publickey
```

Press `Ctrl+C` to stop.

---

# 11. Monitor Last 100 Lines and Follow

## Command

```bash
tail -n 100 -f /var/log/syslog
```

## Example Output

```text
Aug 27 10:20:01 systemd: Started service.
Aug 27 10:20:02 nginx: GET / 200
```

---

# 12. Follow Multiple Log Files

## Command

```bash
tail -f /var/log/syslog /var/log/auth.log
```

## Example Output

```text
==> /var/log/syslog <==
Aug 27 10:20:01 systemd: Started service.

==> /var/log/auth.log <==
Aug 27 10:20:02 sshd: Accepted publickey
```

---

# 13. Search for Errors in Logs

## Command

```bash
grep -i "error" /var/log/syslog
```

## Example Output

```text
Aug 27 10:30:01 application: ERROR database connection failed
Aug 27 10:31:02 nginx: error connecting to upstream
```

---

# 14. Search for Warnings

## Command

```bash
grep -i "warning" /var/log/syslog
```

## Example Output

```text
Aug 27 10:32:01 kernel: WARNING: memory pressure detected
```

---

# 15. Search for Failed Messages

## Command

```bash
grep -i "failed" /var/log/auth.log
```

## Example Output

```text
Aug 27 10:35:01 sshd[1234]: Failed password for user devops
Aug 27 10:36:02 sudo: authentication failure
```

---

# 16. Search for Successful Messages

## Command

```bash
grep -i "accepted" /var/log/auth.log
```

## Example Output

```text
Aug 27 10:40:01 sshd[1234]: Accepted publickey for devops
```

---

# 17. Count Errors in Log

## Command

```bash
grep -ic "error" /var/log/syslog
```

## Example Output

```text
25
```

---

# 18. Count Failed Login Attempts

## Command

```bash
grep -ic "failed password" /var/log/auth.log
```

## Example Output

```text
8
```

---

# 19. Search Multiple Patterns

## Command

```bash
grep -Ei "error|failed|warning" /var/log/syslog
```

## Example Output

```text
ERROR database connection failed
WARNING disk usage high
FAILED service startup
```

---

# 20. Search Logs Recursively

## Command

```bash
grep -Rni "error" /var/log
```

## Example Output

```text
/var/log/syslog:100:ERROR application failed
/var/log/nginx/error.log:250:upstream error
```

---

# 21. Display Matching Line Numbers

## Command

```bash
grep -n "error" /var/log/syslog
```

## Example Output

```text
120:ERROR database connection failed
450:ERROR timeout occurred
```

---

# 22. Display Context Around Error

## Command

```bash
grep -i -C 3 "error" /var/log/syslog
```

## Example Output

```text
INFO starting application
INFO connecting database
ERROR database connection failed
WARNING retrying connection
INFO retry successful
```

---

# 23. Display Lines Before Error

## Command

```bash
grep -i -B 3 "error" /var/log/syslog
```

## Example Output

```text
INFO starting service
INFO loading configuration
INFO connecting database
ERROR database connection failed
```

---

# 24. Display Lines After Error

## Command

```bash
grep -i -A 3 "error" /var/log/syslog
```

## Example Output

```text
ERROR database connection failed
WARNING retrying
INFO connection restored
INFO service running
```

---

# 25. Display Unique Error Messages

## Command

```bash
grep -i "error" /var/log/syslog | sort -u
```

## Example Output

```text
ERROR database connection failed
ERROR connection timeout
ERROR permission denied
```

---

# 26. Count Error Types

## Command

```bash
grep -i "error" /var/log/syslog | sort | uniq -c
```

## Example Output

```text
15 ERROR database connection failed
8 ERROR timeout
3 ERROR permission denied
```

---

# 27. Check Systemd Journal

## Command

```bash
journalctl
```

## Example Output

```text
Aug 27 10:00:01 devops-server systemd[1]: Started system.
Aug 27 10:00:02 devops-server systemd[1]: Started NetworkManager.
```

---

# 28. Display Recent Journal Entries

## Command

```bash
journalctl -n
```

## Example Output

```text
Aug 27 10:20:01 systemd[1]: Started service.
Aug 27 10:20:02 systemd[1]: Service running.
```

---

# 29. Display Last 50 Journal Entries

## Command

```bash
journalctl -n 50
```

## Example Output

```text
Aug 27 10:20:01 systemd: Started service.
Aug 27 10:20:02 systemd: Service running.
```

---

# 30. Follow Journal Logs in Real Time

## Command

```bash
journalctl -f
```

## Example Output

```text
Aug 27 10:30:01 systemd[1]: Started service.
Aug 27 10:30:02 systemd[1]: Service running.
```

Press `Ctrl+C` to stop.

---

# 31. Display Logs for Current Boot

## Command

```bash
journalctl -b
```

## Example Output

```text
Aug 27 09:00:01 kernel: Linux booting
Aug 27 09:00:02 systemd[1]: Started system
```

---

# 32. Display Logs From Previous Boot

## Command

```bash
journalctl -b -1
```

## Example Output

```text
Aug 26 23:00:01 systemd[1]: Starting system
Aug 26 23:00:05 systemd[1]: Started system
```

---

# 33. List Available Boots

## Command

```bash
journalctl --list-boots
```

## Example Output

```text
-1  abc123  Wed Aug 26 09:00:01 2026
 0  def456  Thu Aug 27 09:00:01 2026
```

---

# 34. Display Logs for Specific Service

## Command

```bash
journalctl -u nginx
```

## Example Output

```text
Aug 27 10:00:01 nginx[1234]: Starting nginx
Aug 27 10:00:02 nginx[1234]: Started nginx
```

---

# 35. Display Recent Logs for Service

## Command

```bash
journalctl -u nginx -n 50
```

## Example Output

```text
Aug 27 10:00:01 nginx: Starting
Aug 27 10:00:02 nginx: Started
```

---

# 36. Follow Service Logs

## Command

```bash
journalctl -u nginx -f
```

## Example Output

```text
Aug 27 10:20:01 nginx: GET / 200
Aug 27 10:20:02 nginx: GET /api 200
```

Press `Ctrl+C` to stop.

---

# 37. Display Logs Since Today

## Command

```bash
journalctl --since today
```

## Example Output

```text
Aug 27 00:00:01 systemd: Started service.
Aug 27 10:00:01 nginx: Started nginx.
```

---

# 38. Display Logs Since Yesterday

## Command

```bash
journalctl --since yesterday
```

## Example Output

```text
Aug 26 12:00:01 systemd: Started service.
Aug 27 10:00:01 nginx: Started nginx.
```

---

# 39. Display Logs From Specific Time

## Command

```bash
journalctl --since "2026-08-27 10:00:00"
```

## Example Output

```text
Aug 27 10:00:01 nginx: Started nginx.
Aug 27 10:01:01 nginx: GET / 200
```

---

# 40. Display Logs Between Two Times

## Command

```bash
journalctl --since "2026-08-27 10:00:00" --until "2026-08-27 11:00:00"
```

## Example Output

```text
Aug 27 10:10:01 application: Started
Aug 27 10:20:01 application: Request received
```

---

# 41. Display Error-Level Logs

## Command

```bash
journalctl -p err
```

## Example Output

```text
Aug 27 10:15:01 kernel: I/O error
Aug 27 10:16:01 nginx: upstream connection failed
```

---

# 42. Display Warning and Error Logs

## Command

```bash
journalctl -p warning
```

## Example Output

```text
Aug 27 10:15:01 kernel: WARNING memory pressure
Aug 27 10:16:01 nginx: upstream timeout
```

---

# 43. Display Critical Logs

## Command

```bash
journalctl -p crit
```

## Example Output

```text
Aug 27 10:20:01 kernel: Critical hardware error
```

---

# 44. Display Emergency Logs

## Command

```bash
journalctl -p emerg
```

## Example Output

```text
Aug 27 10:21:01 kernel: Emergency condition detected
```

---

# 45. Display Logs by Priority Range

## Command

```bash
journalctl -p warning..err
```

## Example Output

```text
WARNING service timeout
ERROR database connection failed
```

---

# 46. Display Kernel Logs Using journalctl

## Command

```bash
journalctl -k
```

## Example Output

```text
Aug 27 09:00:01 kernel: Linux version 6.8.0
Aug 27 09:01:02 kernel: eth0: Link is Up
```

---

# 47. Display Kernel Errors

## Command

```bash
journalctl -k -p err
```

## Example Output

```text
Aug 27 10:10:01 kernel: I/O error
Aug 27 10:11:02 kernel: device failure
```

---

# 48. Display Logs With Full Timestamps

## Command

```bash
journalctl -o short-precise
```

## Example Output

```text
Aug 27 10:20:01.123456 systemd[1]: Started service.
```

---

# 49. Display Logs in JSON Format

## Command

```bash
journalctl -o json
```

## Example Output

```text
{"MESSAGE":"Started service","_SYSTEMD_UNIT":"nginx.service"}
```

---

# 50. Display Logs in JSON Pretty Format

## Command

```bash
journalctl -o json-pretty
```

## Example Output

```text
{
    "MESSAGE": "Started service",
    "_SYSTEMD_UNIT": "nginx.service"
}
```

---

# 51. Display Journal Disk Usage

## Command

```bash
journalctl --disk-usage
```

## Example Output

```text
Archived and active journals take up 850.0M in the file system.
```

---

# 52. Check Journal Configuration

## Command

```bash
journalctl --header
```

## Example Output

```text
File Path: /var/log/journal
Runtime Scope: system
```

---

# 53. Check systemd-journald Status

## Command

```bash
systemctl status systemd-journald
```

## Example Output

```text
● systemd-journald.service
   Active: active (running)
```

---

# 54. Restart systemd-journald

## Command

```bash
sudo systemctl restart systemd-journald
```

## Example Output

```text
```

---

# 55. Check Journal Configuration File

## Command

```bash
cat /etc/systemd/journald.conf
```

## Example Output

```text
[Journal]
#Storage=auto
#SystemMaxUse=
#RuntimeMaxUse=
#MaxRetentionSec=
```

---

# 56. Find rsyslog Service

## Command

```bash
systemctl status rsyslog
```

## Example Output

```text
● rsyslog.service
   Active: active (running)
```

---

# 57. Check rsyslog Configuration

## Command

```bash
cat /etc/rsyslog.conf
```

## Example Output

```text
module(load="imuxsock")
module(load="imklog")
*.*;auth,authpriv.none          -/var/log/syslog
```

---

# 58. List rsyslog Configuration Files

## Command

```bash
ls -lh /etc/rsyslog.d/
```

## Example Output

```text
-rw-r--r-- 1 root root 450 50-default.conf
-rw-r--r-- 1 root root 220 application.conf
```

---

# 59. Display Default rsyslog Configuration

## Command

```bash
cat /etc/rsyslog.d/50-default.conf
```

## Example Output

```text
auth,authpriv.*                 /var/log/auth.log
*.*;auth,authpriv.none          -/var/log/syslog
kern.*                          -/var/log/kern.log
```

---

# 60. Test rsyslog Configuration

## Command

```bash
sudo rsyslogd -N1
```

## Example Output

```text
rsyslogd: version 8.x
rsyslogd: End of config validation run. Bye.
```

---

# 61. Restart rsyslog

## Command

```bash
sudo systemctl restart rsyslog
```

## Example Output

```text
```

---

# 62. Check Logrotate Configuration

## Command

```bash
cat /etc/logrotate.conf
```

## Example Output

```text
weekly
rotate 4
create
include /etc/logrotate.d
```

---

# 63. List Logrotate Configurations

## Command

```bash
ls -lh /etc/logrotate.d/
```

## Example Output

```text
-rw-r--r-- 1 root root 120 nginx
-rw-r--r-- 1 root root 180 rsyslog
-rw-r--r-- 1 root root 150 apt
```

---

# 64. Display rsyslog Logrotate Configuration

## Command

```bash
cat /etc/logrotate.d/rsyslog
```

## Example Output

```text
/var/log/syslog
/var/log/mail.log
/var/log/kern.log
{
    rotate 4
    weekly
    missingok
    notifempty
    compress
}
```

---

# 65. Test Logrotate Configuration

## Command

```bash
sudo logrotate -d /etc/logrotate.conf
```

## Example Output

```text
reading config file /etc/logrotate.conf
rotating pattern: /var/log/syslog
considering log /var/log/syslog
```

`-d` performs a debug/dry-run and does not rotate logs.

---

# 66. Force Log Rotation

## Command

```bash
sudo logrotate -f /etc/logrotate.conf
```

## Example Output

```text
```

---

# 67. Display Logrotate State

## Command

```bash
cat /var/lib/logrotate/status
```

## Example Output

```text
logrotate state -- version 2
"/var/log/syslog" 2026-8-27
"/var/log/auth.log" 2026-8-27
```

---

# 68. Check Nginx Logs

## Command

```bash
ls -lh /var/log/nginx/
```

## Example Output

```text
-rw-r----- 1 www-data adm 120K access.log
-rw-r----- 1 www-data adm  80K error.log
```

---

# 69. Display Nginx Access Log

## Command

```bash
sudo tail -f /var/log/nginx/access.log
```

## Example Output

```text
192.168.1.50 - - [27/Aug/2026:10:20:01] "GET / HTTP/1.1" 200
192.168.1.50 - - [27/Aug/2026:10:20:02] "GET /api HTTP/1.1" 404
```

---

# 70. Display Nginx Error Log

## Command

```bash
sudo tail -f /var/log/nginx/error.log
```

## Example Output

```text
2026/08/27 10:20:01 [error] 1234#1234: connect() failed
2026/08/27 10:20:02 [error] 1234#1234: upstream timed out
```

---

# 71. Search Nginx Errors

## Command

```bash
sudo grep -i "error" /var/log/nginx/error.log
```

## Example Output

```text
connect() failed
upstream timed out
connection refused
```

---

# 72. Count HTTP 500 Errors

## Command

```bash
grep ' 500 ' /var/log/nginx/access.log | wc -l
```

## Example Output

```text
15
```

---

# 73. Count HTTP 404 Errors

## Command

```bash
grep ' 404 ' /var/log/nginx/access.log | wc -l
```

## Example Output

```text
25
```

---

# 74. Find Top HTTP Status Codes

## Command

```bash
awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c | sort -nr
```

## Example Output

```text
1200 200
150  404
50   500
20   301
```

---

# 75. Find Top Client IP Addresses

## Command

```bash
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head
```

## Example Output

```text
500 192.168.1.50
350 192.168.1.60
200 192.168.1.70
```

---

# 76. Find Most Requested URLs

## Command

```bash
awk '{print $7}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head
```

## Example Output

```text
500 /
300 /api
150 /login
100 /health
```

---

# 77. Find SSH Login Attempts

## Command

```bash
sudo grep "sshd" /var/log/auth.log
```

## Example Output

```text
Aug 27 10:00:01 sshd[1234]: Accepted publickey
Aug 27 10:01:01 sshd[1235]: Failed password
```

---

# 78. Find Successful SSH Logins

## Command

```bash
sudo grep "Accepted" /var/log/auth.log
```

## Example Output

```text
Aug 27 10:00:01 sshd[1234]: Accepted publickey for devops
Aug 27 10:05:01 sshd[1235]: Accepted password for admin
```

---

# 79. Find Failed SSH Logins

## Command

```bash
sudo grep "Failed password" /var/log/auth.log
```

## Example Output

```text
Aug 27 10:10:01 sshd[1234]: Failed password for invalid user test
```

---

# 80. Count Failed SSH Logins

## Command

```bash
sudo grep -c "Failed password" /var/log/auth.log
```

## Example Output

```text
25
```

---

# 81. Find Invalid SSH Users

## Command

```bash
sudo grep "Invalid user" /var/log/auth.log
```

## Example Output

```text
sshd[1234]: Invalid user admin from 192.168.1.50
sshd[1235]: Invalid user test from 192.168.1.60
```

---

# 82. Find sudo Commands in Logs

## Command

```bash
sudo grep "sudo:" /var/log/auth.log
```

## Example Output

```text
devops : TTY=pts/0 ; PWD=/home/devops ; USER=root ; COMMAND=/bin/systemctl restart nginx
```

---

# 83. Find Current User Login Records

## Command

```bash
last
```

## Example Output

```text
devops   pts/0  192.168.1.50  Thu Aug 27 10:00   still logged in
admin    pts/1  192.168.1.60  Thu Aug 27 09:00 - 09:30
```

---

# 84. Display Last 10 Login Records

## Command

```bash
last -10
```

## Example Output

```text
devops pts/0 192.168.1.50 Thu Aug 27 10:00 still logged in
admin  pts/1 192.168.1.60 Thu Aug 27 09:00 - 09:30
```

---

# 85. Display Failed Login Records

## Command

```bash
sudo lastb
```

## Example Output

```text
invalid pts/0 192.168.1.100 Thu Aug 27 10:20 - 10:20
admin   pts/1 192.168.1.110 Thu Aug 27 10:15 - 10:15
```

---

# 86. Display User Login History

## Command

```bash
lastlog
```

## Example Output

```text
Username         Port     From             Latest
root             **Never logged in**
devops           pts/0    192.168.1.50     Thu Aug 27 10:00
```

---

# 87. Display Kernel Messages Using dmesg

## Command

```bash
dmesg
```

## Example Output

```text
[    0.000000] Linux version 6.8.0
[    2.123456] eth0: Link is Up
```

---

# 88. Display Human-Readable Kernel Messages

## Command

```bash
sudo dmesg -H
```

## Example Output

```text
kernel: Linux version 6.8.0
kernel: eth0: Link is Up
```

---

# 89. Display Kernel Errors

## Command

```bash
sudo dmesg --level=err
```

## Example Output

```text
kernel: I/O error on device sda
kernel: filesystem error
```

---

# 90. Display Kernel Warnings

## Command

```bash
sudo dmesg --level=warn
```

## Example Output

```text
kernel: WARNING memory pressure
kernel: WARNING device timeout
```

---

# 91. Search dmesg for Disk Errors

## Command

```bash
sudo dmesg | grep -Ei "error|fail|io"
```

## Example Output

```text
I/O error on device sda
EXT4-fs error
device failure
```

---

# 92. Search dmesg for Network Errors

## Command

```bash
sudo dmesg | grep -Ei "eth|network|link|error"
```

## Example Output

```text
eth0: Link is Up
eth0: Link is Down
network device initialized
```

---

# 93. Search Logs for Out of Memory

## Command

```bash
sudo journalctl | grep -Ei "out of memory|oom|killed process"
```

## Example Output

```text
kernel: Out of memory: Killed process 2451
kernel: Killed process 2451 (python3)
```

---

# 94. Check OOM Events

## Command

```bash
sudo journalctl -k | grep -i oom
```

## Example Output

```text
kernel: Out of memory: Killed process 2451
```

---

# 95. Search Logs for Disk Errors

## Command

```bash
sudo journalctl -k | grep -Ei "disk|i/o error|filesystem"
```

## Example Output

```text
kernel: I/O error on device sda
kernel: EXT4-fs error
```

---

# 96. Search Logs for Network Errors

## Command

```bash
sudo journalctl -k | grep -Ei "network|eth0|link"
```

## Example Output

```text
kernel: eth0: Link is Up
kernel: eth0: Link is Down
```

---

# 97. Search All Logs for Permission Errors

## Command

```bash
sudo journalctl | grep -i "permission denied"
```

## Example Output

```text
application: Permission denied
nginx: open() failed: Permission denied
```

---

# 98. Search Logs for Connection Refused

## Command

```bash
sudo journalctl | grep -i "connection refused"
```

## Example Output

```text
application: connection refused
nginx: connect() failed (111: Connection refused)
```

---

# 99. Search Logs for Timeout Errors

## Command

```bash
sudo journalctl | grep -Ei "timeout|timed out"
```

## Example Output

```text
application: database connection timeout
nginx: upstream timed out
```

---

# 100. Search Logs for Database Errors

## Command

```bash
sudo journalctl | grep -Ei "mysql|postgres|database|sql"
```

## Example Output

```text
mysql: connection refused
application: database connection failed
```

---

# 101. Search Logs for Docker Errors

## Command

```bash
sudo journalctl | grep -i docker
```

## Example Output

```text
dockerd[1234]: container started
dockerd[1234]: failed to start container
```

---

# 102. Display Docker Service Logs

## Command

```bash
sudo journalctl -u docker
```

## Example Output

```text
dockerd[1234]: Docker daemon started
dockerd[1234]: container started
```

---

# 103. Follow Docker Service Logs

## Command

```bash
sudo journalctl -u docker -f
```

## Example Output

```text
dockerd: container started
dockerd: network created
dockerd: container stopped
```

Press `Ctrl+C` to stop.

---

# 104. Display SSH Service Logs

## Command

```bash
sudo journalctl -u ssh
```

## Example Output

```text
sshd[1234]: Server listening on port 22
sshd[1235]: Accepted publickey
```

---

# 105. Follow SSH Logs

## Command

```bash
sudo journalctl -u ssh -f
```

## Example Output

```text
sshd: Accepted publickey
sshd: Connection closed
```

---

# 106. Display Nginx Service Logs

## Command

```bash
sudo journalctl -u nginx
```

## Example Output

```text
nginx.service: Started
nginx.service: Reloaded
```

---

# 107. Display Logs for Failed Services

## Command

```bash
systemctl --failed
```

## Example Output

```text
UNIT                LOAD   ACTIVE SUB    DESCRIPTION
nginx.service       loaded failed failed A high performance web server
```

---

# 108. Find Failed Service Logs

## Command

```bash
sudo journalctl -p err -b
```

## Example Output

```text
nginx.service: Failed to start
database.service: Connection failed
```

---

# 109. Check Service Status and Logs

## Command

```bash
sudo systemctl status nginx
```

## Example Output

```text
● nginx.service
   Active: failed
   Process: 1234 ExecStart=/usr/sbin/nginx
   Main PID: 1234
```

---

# 110. Display Service Logs With Recent Entries

## Command

```bash
sudo journalctl -u nginx --since "10 minutes ago"
```

## Example Output

```text
nginx: Starting
nginx: Configuration loaded
nginx: upstream connection failed
```

---

# 111. Display Logs From Last Hour

## Command

```bash
journalctl --since "1 hour ago"
```

## Example Output

```text
Aug 27 10:00:01 systemd: Started service.
Aug 27 10:30:01 nginx: Request received.
```

---

# 112. Display Logs From Last 10 Minutes

## Command

```bash
journalctl --since "10 minutes ago"
```

## Example Output

```text
Aug 27 10:20:01 nginx: Request received.
Aug 27 10:25:01 application: Database connected.
```

---

# 113. Display Logs Until Specific Time

## Command

```bash
journalctl --until "2026-08-27 12:00:00"
```

## Example Output

```text
Aug 27 11:55:01 systemd: Service running.
Aug 27 11:59:01 nginx: Request completed.
```

---

# 114. Display Logs for Current User

## Command

```bash
journalctl _UID=$(id -u)
```

## Example Output

```text
Aug 27 10:20:01 devops bash[1234]: command executed
```

---

# 115. Display Logs by Process ID

## Command

```bash
journalctl _PID=1234
```

## Example Output

```text
Aug 27 10:20:01 nginx[1234]: worker started
Aug 27 10:20:02 nginx[1234]: request completed
```

---

# 116. Display Logs by Executable

## Command

```bash
journalctl /usr/sbin/nginx
```

## Example Output

```text
nginx[1234]: started
nginx[1234]: request received
```

---

# 117. Display Logs by Boot ID

## Command

```bash
journalctl _BOOT_ID=$(cat /proc/sys/kernel/random/boot_id)
```

## Example Output

```text
Aug 27 09:00:01 systemd: Boot started
```

---

# 118. Export Journal Logs to File

## Command

```bash
journalctl > system-logs.txt
```

## Example Output

```text
```

---

# 119. Export Service Logs to File

## Command

```bash
journalctl -u nginx > nginx-logs.txt
```

## Example Output

```text
```

---

# 120. Search Exported Logs

## Command

```bash
grep -i "error" nginx-logs.txt
```

## Example Output

```text
upstream connection error
connection refused
```

---

# 121. Compress Log File

## Command

```bash
gzip application.log
```

## Example Output

```text
```

The file becomes:

```text
application.log.gz
```

---

# 122. Decompress Log File

## Command

```bash
gunzip application.log.gz
```

## Example Output

```text
```

---

# 123. Read Compressed Log

## Command

```bash
zcat application.log.gz
```

## Example Output

```text
Aug 27 10:00:01 application started
Aug 27 10:01:01 request received
```

---

# 124. Search Compressed Logs

## Command

```bash
zgrep -i "error" application.log.gz
```

## Example Output

```text
ERROR database connection failed
ERROR timeout
```

---

# 125. List Compressed Logs

## Command

```bash
find /var/log -name "*.gz"
```

## Example Output

```text
/var/log/syslog.1.gz
/var/log/auth.log.2.gz
/var/log/nginx/access.log.1.gz
```

---

# 126. Find Logs Larger Than 100MB

## Command

```bash
find /var/log -type f -size +100M -ls
```

## Example Output

```text
123456 105000 /var/log/application.log
123457 120000 /var/log/nginx/access.log
```

---

# 127. Find Largest Log Files

## Command

```bash
find /var/log -type f -printf '%s %p\n' | sort -nr | head -10
```

## Example Output

```text
524288000 /var/log/application.log
250000000 /var/log/nginx/access.log
120000000 /var/log/syslog
```

---

# 128. Check Total Log Directory Size

## Command

```bash
sudo du -sh /var/log
```

## Example Output

```text
2.5G    /var/log
```

---

# 129. Find Largest Log Directories

## Command

```bash
sudo du -h --max-depth=1 /var/log | sort -hr
```

## Example Output

```text
2.5G    /var/log
1.2G    /var/log/nginx
800M    /var/log/journal
300M    /var/log/apache2
```

---

# 130. Check Journal Disk Usage

## Command

```bash
journalctl --disk-usage
```

## Example Output

```text
Archived and active journals take up 1.2G in the file system.
```

---

# 131. Remove Old Journal Logs

## Command

```bash
sudo journalctl --vacuum-time=7d
```

## Example Output

```text
Vacuuming done, freed 500.0M of archived journals.
```

This removes journal files older than 7 days.

---

# 132. Limit Journal Size

## Command

```bash
sudo journalctl --vacuum-size=500M
```

## Example Output

```text
Vacuuming done, freed 350.0M of archived journals.
```

---

# 133. Remove Old Journal Files by Number

## Command

```bash
sudo journalctl --vacuum-files=5
```

## Example Output

```text
Vacuuming done, retained 5 journal files.
```

---

# 134. Check Journal Persistent Storage

## Command

```bash
ls -ld /var/log/journal
```

## Example Output

```text
drwxr-sr-x 2 root systemd-journal 4096 /var/log/journal
```

---

# 135. Display Journal File Information

## Command

```bash
journalctl --header
```

## Example Output

```text
File Path: /var/log/journal/xxxx/system.journal
```

---

# 136. Verify Journal Logs

## Command

```bash
sudo journalctl --verify
```

## Example Output

```text
PASS: /var/log/journal/.../system.journal
```

---

# 137. Display Boot Errors

## Command

```bash
journalctl -b -p err
```

## Example Output

```text
kernel: device error
nginx.service: Failed to start
```

---

# 138. Display Boot Warnings

## Command

```bash
journalctl -b -p warning
```

## Example Output

```text
kernel: memory warning
systemd: service timeout warning
```

---

# 139. Check System Boot Logs

## Command

```bash
journalctl -b | head -50
```

## Example Output

```text
kernel: Linux version 6.8.0
systemd[1]: Starting system
systemd[1]: Started system
```

---

# 140. Check Shutdown Logs

## Command

```bash
journalctl -b -1 | tail -50
```

## Example Output

```text
systemd: Stopping service
systemd: Reached shutdown target
systemd: System shutdown complete
```

---

# 141. Monitor Logs With watch

## Command

```bash
watch -n 2 'tail -n 20 /var/log/syslog'
```

## Example Output

```text
Every 2.0s: tail -n 20 /var/log/syslog

Aug 27 10:20:01 systemd: Started service.
Aug 27 10:20:02 nginx: Request received.
```

Press `Ctrl+C` to exit.

---

# 142. Monitor Error Logs Continuously

## Command

```bash
tail -F /var/log/syslog | grep -i --line-buffered "error"
```

## Example Output

```text
ERROR database connection failed
ERROR upstream timeout
```

Press `Ctrl+C` to stop.

---

# 143. Monitor Nginx Errors Continuously

## Command

```bash
tail -F /var/log/nginx/error.log
```

## Example Output

```text
2026/08/27 10:20:01 [error] upstream timed out
2026/08/27 10:20:02 [error] connection refused
```

---

# 144. Find Today's Errors

## Command

```bash
journalctl --since today -p err
```

## Example Output

```text
Aug 27 10:20:01 nginx: upstream error
Aug 27 10:21:01 kernel: I/O error
```

---

# 145. Find Errors From Last Hour

## Command

```bash
journalctl --since "1 hour ago" -p err
```

## Example Output

```text
nginx: connection refused
application: database timeout
```

---

# 146. Count Journal Error Messages

## Command

```bash
journalctl -p err -b | wc -l
```

## Example Output

```text
25
```

---

# 147. Find Most Common Error Messages

## Command

```bash
journalctl -p err -b | awk -F': ' '{print $2}' | sort | uniq -c | sort -nr | head
```

## Example Output

```text
15 connection refused
10 timeout
5 permission denied
```

---

# 148. Find Failed Services From Logs

## Command

```bash
journalctl -b | grep -i "failed"
```

## Example Output

```text
nginx.service: Failed to start
docker.service: Failed to start
```

---

# 149. Check Service Restart History

## Command

```bash
journalctl -u nginx | grep -Ei "start|stop|restart"
```

## Example Output

```text
Started nginx
Stopped nginx
Started nginx
```

---

# 150. Check Application Log Directory

## Command

```bash
find /var/log -maxdepth 2 -type f
```

## Example Output

```text
/var/log/syslog
/var/log/auth.log
/var/log/nginx/access.log
/var/log/nginx/error.log
```

---

# 151. Find All Log Files

## Command

```bash
sudo find /var/log -type f
```

## Example Output

```text
/var/log/syslog
/var/log/auth.log
/var/log/kern.log
/var/log/nginx/access.log
/var/log/nginx/error.log
```

---

# 152. Find Logs Modified Today

## Command

```bash
sudo find /var/log -type f -mtime 0
```

## Example Output

```text
/var/log/syslog
/var/log/auth.log
/var/log/nginx/access.log
```

---

# 153. Find Logs Modified in Last Hour

## Command

```bash
sudo find /var/log -type f -mmin -60
```

## Example Output

```text
/var/log/syslog
/var/log/nginx/error.log
```

---

# 154. Check Log File Permissions

## Command

```bash
ls -l /var/log/syslog
```

## Example Output

```text
-rw-r----- 1 syslog adm 250K Aug 27 10:30 /var/log/syslog
```

---

# 155. Check Authentication Log Permissions

## Command

```bash
ls -l /var/log/auth.log
```

## Example Output

```text
-rw-r----- 1 syslog adm 120K Aug 27 10:30 /var/log/auth.log
```

---

# 156. Check Who Owns a Log File

## Command

```bash
stat /var/log/syslog
```

## Example Output

```text
File: /var/log/syslog
Size: 250000
Uid: 104
Gid: 4
Access: 0640
```

---

# 157. Display Log File Metadata

## Command

```bash
stat /var/log/nginx/error.log
```

## Example Output

```text
File: /var/log/nginx/error.log
Size: 80000
Modify: Aug 27 10:30:01
```

---

# 158. Find Open Log Files

## Command

```bash
sudo lsof /var/log/syslog
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NAME
rsyslogd 900 syslog 5w REG /var/log/syslog
```

---

# 159. Find Processes Writing to Logs

## Command

```bash
sudo lsof +D /var/log 2>/dev/null
```

## Example Output

```text
rsyslogd 900 syslog /var/log/syslog
nginx 1500 www-data /var/log/nginx/access.log
```

---

# 160. Check Log File Descriptors

## Command

```bash
sudo ls -l /proc/$(pgrep rsyslogd)/fd
```

## Example Output

```text
5 -> /var/log/syslog
6 -> /var/log/auth.log
```

---

# 161. Check Journald Process

## Command

```bash
ps aux | grep systemd-journald
```

## Example Output

```text
root  700  0.0  0.1  systemd-journald
```

---

# 162. Check rsyslog Process

## Command

```bash
ps aux | grep rsyslog
```

## Example Output

```text
syslog 900 0.0 0.1 /usr/sbin/rsyslogd
```

---

# 163. Check Logrotate Service

## Command

```bash
systemctl status logrotate.timer
```

## Example Output

```text
● logrotate.timer
   Active: active (waiting)
```

---

# 164. Check Logrotate Timer

## Command

```bash
systemctl list-timers | grep logrotate
```

## Example Output

```text
logrotate.timer   daily   logrotate.service
```

---

# 165. Run Logrotate Manually

## Command

```bash
sudo logrotate /etc/logrotate.conf
```

## Example Output

```text
```

---

# 166. Find Log Files With Specific Extension

## Command

```bash
find /var/log -type f -name "*.log"
```

## Example Output

```text
/var/log/application.log
/var/log/nginx/access.log
/var/log/nginx/error.log
```

---

# 167. Find Compressed Logs

## Command

```bash
find /var/log -type f -name "*.gz"
```

## Example Output

```text
/var/log/syslog.1.gz
/var/log/auth.log.2.gz
```

---

# 168. Search All Current and Compressed Logs

## Command

```bash
grep -Rni "error" /var/log --include="*.log"
```

## Example Output

```text
/var/log/nginx/error.log:10:upstream error
/var/log/application.log:25:database error
```

---

# 169. Search Case-Insensitive Logs

## Command

```bash
grep -Ri "error" /var/log
```

## Example Output

```text
/var/log/syslog:ERROR application failed
/var/log/nginx/error.log:upstream error
```

---

# 170. Search Logs Excluding Compressed Files

## Command

```bash
grep -Rni "error" /var/log --exclude="*.gz"
```

## Example Output

```text
/var/log/syslog:ERROR application failed
/var/log/nginx/error.log:upstream error
```

---

# 171. Display Log Lines Matching Date

## Command

```bash
grep "Aug 27" /var/log/syslog
```

## Example Output

```text
Aug 27 10:00:01 systemd: Started service.
Aug 27 10:01:01 nginx: Request received.
```

---

# 172. Display Log Lines for Specific Hour

## Command

```bash
grep "10:" /var/log/syslog
```

## Example Output

```text
Aug 27 10:10:01 systemd: Started service.
Aug 27 10:20:01 nginx: Request received.
```

---

# 173. Extract IP Addresses From Logs

## Command

```bash
grep -oE '([0-9]{1,3}\.){3}[0-9]{1,3}' /var/log/auth.log | sort -u
```

## Example Output

```text
192.168.1.50
192.168.1.60
10.10.10.20
```

---

# 174. Find Top IP Addresses in Authentication Logs

## Command

```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr
```

## Example Output

```text
50 192.168.1.50
25 192.168.1.60
10 10.10.10.20
```

---

# 175. Find Top Failed SSH IP Addresses

## Command

```bash
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
```

## Example Output

```text
50 192.168.1.50
30 192.168.1.60
15 10.10.10.20
```

---

# 176. Find Successful SSH Users

## Command

```bash
sudo grep "Accepted" /var/log/auth.log | awk '{print $9}' | sort | uniq -c
```

## Example Output

```text
25 devops
10 admin
```

---

# 177. Check Last Reboot

## Command

```bash
last reboot
```

## Example Output

```text
reboot system boot 6.8.0 Thu Aug 27 09:00 still running
```

---

# 178. Check System Uptime

## Command

```bash
uptime
```

## Example Output

```text
10:30:01 up 1:30, 2 users, load average: 0.20, 0.15, 0.10
```

---

# 179. Check System Boot Time

## Command

```bash
uptime -s
```

## Example Output

```text
2026-08-27 09:00:01
```

---

# 180. Check Systemd Boot Time

## Command

```bash
systemd-analyze
```

## Example Output

```text
Startup finished in 3.200s (kernel) + 5.100s (userspace) = 8.300s
```

---

# 181. Check Slow Services During Boot

## Command

```bash
systemd-analyze blame
```

## Example Output

```text
3.200s docker.service
2.100s nginx.service
1.500s NetworkManager.service
```

---

# 182. Check Critical Boot Chain

## Command

```bash
systemd-analyze critical-chain
```

## Example Output

```text
graphical.target
└─multi-user.target
  └─nginx.service
    └─network-online.target
```

---

# 183. Check Kernel Ring Buffer for Errors

## Command

```bash
sudo dmesg --level=err,warn
```

## Example Output

```text
kernel: WARNING device timeout
kernel: ERROR I/O failure
```

---

# 184. Search Journal for Segmentation Faults

## Command

```bash
journalctl | grep -i "segfault"
```

## Example Output

```text
kernel: application[1234]: segfault at 0 ip ...
```

---

# 185. Search Journal for Core Dumps

## Command

```bash
journalctl | grep -i "core dumped"
```

## Example Output

```text
application: process terminated and dumped core
```

---

# 186. Check Core Dump Information

## Command

```bash
coredumpctl list
```

## Example Output

```text
TIME PID UID GID SIG COREFILE EXE
Aug 27 10:20 2451 1000 1000 SIGSEGV present /usr/bin/app
```

---

# 187. Display Latest Core Dump

## Command

```bash
coredumpctl info
```

## Example Output

```text
PID: 2451
Signal: SIGSEGV
Executable: /usr/bin/app
```

---

# 188. Search Logs for Memory Problems

## Command

```bash
journalctl | grep -Ei "memory|oom|killed"
```

## Example Output

```text
kernel: Out of memory
kernel: Killed process 2451
```

---

# 189. Search Logs for CPU Problems

## Command

```bash
journalctl | grep -Ei "cpu|thermal|thrott"
```

## Example Output

```text
kernel: CPU temperature high
kernel: CPU throttling detected
```

---

# 190. Search Logs for Filesystem Problems

## Command

```bash
journalctl -k | grep -Ei "ext4|xfs|filesystem|mount"
```

## Example Output

```text
kernel: EXT4-fs mounted
kernel: EXT4-fs error
```

---

# 191. Search Logs for Storage Errors

## Command

```bash
journalctl -k | grep -Ei "disk|sda|nvme|i/o"
```

## Example Output

```text
kernel: sda I/O error
kernel: nvme timeout
```

---

# 192. Search Logs for Network Interface Errors

## Command

```bash
journalctl -k | grep -Ei "eth0|link|network"
```

## Example Output

```text
kernel: eth0: Link is Up
kernel: eth0: Link is Down
```

---

# 193. Display Logs in Reverse Order

## Command

```bash
journalctl -r
```

## Example Output

```text
Aug 27 10:30:01 latest log
Aug 27 10:29:01 previous log
Aug 27 10:28:01 older log
```

---

# 194. Display Only Messages From Current User

## Command

```bash
journalctl --user
```

## Example Output

```text
Aug 27 10:20:01 user application started
Aug 27 10:21:01 user application stopped
```

---

# 195. Display User Journal Logs in Real Time

## Command

```bash
journalctl --user -f
```

## Example Output

```text
user application started
user application request received
```

Press `Ctrl+C` to stop.

---

# 196. Display Journal Logs Without Pager

## Command

```bash
journalctl --no-pager
```

## Example Output

```text
Aug 27 10:00:01 systemd: Started service.
Aug 27 10:01:01 nginx: Started nginx.
```

---

# 197. Display Journal Logs With Short Output

## Command

```bash
journalctl -o short
```

## Example Output

```text
Aug 27 10:00:01 systemd: Started service.
Aug 27 10:01:01 nginx: Started nginx.
```

---

# 198. Display Journal Logs With Full Output

## Command

```bash
journalctl -o verbose
```

## Example Output

```text
MESSAGE=Started service
_PID=1234
_UID=0
_SYSTEMD_UNIT=nginx.service
```

---

# 199. Display Service Logs Without Pager

## Command

```bash
journalctl -u nginx --no-pager
```

## Example Output

```text
nginx.service: Started
nginx.service: Request received
```

---

# 200. Production Log Troubleshooting Flow

## Command

```bash
# Check system errors
journalctl -p err -b

# Check failed services
systemctl --failed

# Check service status
systemctl status nginx

# Check service logs
journalctl -u nginx -n 100

# Follow service logs
journalctl -u nginx -f

# Check application logs
tail -n 100 /var/log/application.log

# Search errors
grep -Ei "error|failed|warning" /var/log/application.log

# Check kernel errors
dmesg --level=err,warn

# Check disk usage
df -h

# Check log directory usage
du -sh /var/log

# Check journal usage
journalctl --disk-usage
```

## Example Output

```text
System Errors
Failed Services
Service Status
Service Logs
Application Errors
Kernel Errors
Disk Usage
Journal Usage
```

---

# 📚 Important Linux Log Files

## Command

```text
/var/log/syslog
/var/log/auth.log
/var/log/kern.log
/var/log/dmesg
/var/log/messages
/var/log/boot.log
/var/log/cron
/var/log/maillog
/var/log/nginx/access.log
/var/log/nginx/error.log
/var/log/apache2/access.log
/var/log/apache2/error.log
/var/log/journal/
```

## Example Output

```text
/var/log/syslog              → General system logs
/var/log/auth.log            → Authentication and sudo logs
/var/log/kern.log            → Kernel logs
/var/log/dmesg               → Kernel ring buffer
/var/log/boot.log            → Boot logs
/var/log/nginx/access.log    → Nginx access logs
/var/log/nginx/error.log     → Nginx error logs
/var/log/journal/            → systemd journal logs
```

---

# 📌 Linux Log Levels

## Command

```text
0   emerg
1   alert
2   crit
3   err
4   warning
5   notice
6   info
7   debug
```

## Example Output

```text
emerg   → Emergency
alert   → Immediate action required
crit    → Critical condition
err     → Error
warning → Warning
notice  → Normal but significant
info    → Informational
debug   → Debug information
```

---

# 📌 Important Log Management Commands

## Command

```bash
cat /var/log/syslog
tail /var/log/syslog
tail -f /var/log/syslog
head /var/log/syslog
grep -i error /var/log/syslog
less /var/log/syslog
journalctl
journalctl -f
journalctl -u nginx
journalctl -p err
journalctl -b
journalctl --since today
journalctl --disk-usage
journalctl --vacuum-time=7d
dmesg
dmesg --level=err
systemctl status rsyslog
systemctl status systemd-journald
logrotate
logrotate -d
logrotate -f
last
lastb
lastlog
coredumpctl
```

## Example Output

```text
System Log Management
Journal Management
Service Troubleshooting
Kernel Log Analysis
Authentication Log Analysis
Log Rotation
Disk Usage Analysis
Production Troubleshooting
```

---

# 🧪 Practical Production Troubleshooting Flow

## Command

```bash
# 1. Check failed services
systemctl --failed

# 2. Check system errors
journalctl -p err -b

# 3. Check warnings
journalctl -p warning -b

# 4. Check current boot
journalctl -b

# 5. Check service
systemctl status nginx

# 6. Check service logs
journalctl -u nginx -n 100

# 7. Follow service logs
journalctl -u nginx -f

# 8. Check application logs
tail -n 100 /var/log/application.log

# 9. Search errors
grep -Ei "error|failed|warning" /var/log/application.log

# 10. Check kernel errors
dmesg --level=err,warn

# 11. Check disk space
df -h

# 12. Check log storage
du -sh /var/log

# 13. Check journal storage
journalctl --disk-usage

# 14. Check authentication failures
sudo grep "Failed password" /var/log/auth.log
```

## Example Output

```text
Failed service detected
System error detected
Application error detected
Kernel warning detected
Disk usage checked
Log usage checked
Authentication failures identified
```

---

# 🎯 DevOps Logging Skills Practiced

## Command

```bash
journalctl
journalctl -u
journalctl -p
journalctl -b
journalctl -f
grep
tail
head
less
dmesg
rsyslogd
logrotate
last
lastb
lastlog
coredumpctl
systemctl
```

## Example Output

```text
System Log Analysis
Service Log Analysis
Application Log Analysis
Authentication Troubleshooting
Kernel Troubleshooting
Log Rotation
Log Storage Management
Production Incident Investigation
Error Detection
Performance Troubleshooting
```

---

# 🏆 DevOps Interview Commands

## Command

```bash
# View system logs
journalctl

# View latest logs
journalctl -n 50

# Follow logs
journalctl -f

# View service logs
journalctl -u nginx

# View service logs in real time
journalctl -u nginx -f

# View errors
journalctl -p err

# View current boot errors
journalctl -b -p err

# View logs from last hour
journalctl --since "1 hour ago"

# Check failed services
systemctl --failed

# Check kernel logs
dmesg

# Check kernel errors
dmesg --level=err

# Check syslog
tail -f /var/log/syslog

# Check authentication logs
tail -f /var/log/auth.log

# Search errors
grep -i error /var/log/syslog

# Check nginx errors
tail -f /var/log/nginx/error.log

# Check log disk usage
journalctl --disk-usage

# Check /var/log usage
du -sh /var/log

# Check logrotate
cat /etc/logrotate.conf

# Test logrotate
sudo logrotate -d /etc/logrotate.conf

# Check failed SSH logins
sudo grep "Failed password" /var/log/auth.log

# Check successful SSH logins
sudo grep "Accepted" /var/log/auth.log
```

## Example Output

```text
These commands are commonly useful for:

System Troubleshooting
Service Troubleshooting
Application Troubleshooting
Authentication Troubleshooting
Kernel Troubleshooting
Nginx Troubleshooting
Docker Troubleshooting
Log Rotation
Disk Usage Investigation
Production Incident Investigation
DevOps Infrastructure Troubleshooting
```

---

# 🚀 Production Log Troubleshooting Cheat Sheet

## Command

```bash
# System errors
journalctl -p err -b

# Failed services
systemctl --failed

# Service status
systemctl status nginx

# Service logs
journalctl -u nginx -n 100

# Follow service logs
journalctl -u nginx -f

# System logs
tail -f /var/log/syslog

# Authentication logs
tail -f /var/log/auth.log

# Nginx access logs
tail -f /var/log/nginx/access.log

# Nginx error logs
tail -f /var/log/nginx/error.log

# Search errors
grep -Ei "error|failed|warning" /var/log/syslog

# Kernel errors
dmesg --level=err,warn

# Disk errors
journalctl -k | grep -Ei "disk|i/o|error"

# Network errors
journalctl -k | grep -Ei "network|eth0|link"

# OOM errors
journalctl -k | grep -Ei "oom|out of memory|killed"

# Permission errors
journalctl | grep -i "permission denied"

# Connection errors
journalctl | grep -Ei "connection refused|timeout"

# Check log storage
df -h /var/log

# Check log directory size
du -sh /var/log

# Check journal size
journalctl --disk-usage

# Check logrotate
systemctl list-timers | grep logrotate
```

## Example Output

```text
System Errors       → journalctl
Failed Services     → systemctl --failed
Service Logs        → journalctl -u
Live Logs           → journalctl -f
System Logs         → /var/log/syslog
Auth Logs           → /var/log/auth.log
Nginx Logs          → /var/log/nginx/
Kernel Logs         → dmesg / journalctl -k
OOM Investigation   → journalctl -k
Network Errors      → journalctl -k
Disk Errors         → journalctl -k
Log Storage         → df / du
Log Rotation        → logrotate
```

---

# ✅ Learning Outcome

## Command

```bash
journalctl
grep
tail
dmesg
systemctl
logrotate
last
lastb
coredumpctl
du
df
```

## Example Output

```text
By completing this topic, you should be able to:

- Understand Linux logging
- Locate important Linux log files
- Read system logs
- Search logs using grep
- Monitor logs in real time
- Analyze systemd journal logs
- Filter logs by service
- Filter logs by priority
- Analyze current and previous boot logs
- Troubleshoot failed systemd services
- Analyze authentication failures
- Analyze SSH login attempts
- Analyze kernel errors
- Troubleshoot OOM events
- Troubleshoot disk errors
- Troubleshoot network errors
- Analyze Nginx logs
- Analyze application logs
- Understand rsyslog
- Understand systemd-journald
- Configure and troubleshoot logrotate
- Monitor log disk usage
- Clean old journal logs
- Analyze compressed logs
- Find large log files
- Investigate production incidents
- Perform DevOps log troubleshooting
```

---

# 📌 Quick Reference

## Command

```bash
journalctl -f
journalctl -u nginx -f
journalctl -p err -b
journalctl --since today
journalctl --disk-usage
journalctl --vacuum-time=7d
systemctl --failed
systemctl status nginx
dmesg --level=err,warn
tail -f /var/log/syslog
tail -f /var/log/auth.log
tail -f /var/log/nginx/error.log
grep -i error /var/log/syslog
sudo grep "Failed password" /var/log/auth.log
du -sh /var/log
df -h
logrotate -d /etc/logrotate.conf
last
lastb
coredumpctl
```

## Example Output

```text
System Logs
Service Logs
Error Logs
Boot Logs
Authentication Logs
Kernel Logs
Application Logs
Nginx Logs
Log Rotation
Log Storage
Production Troubleshooting
```
