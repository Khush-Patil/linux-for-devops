# 📌 Linux Crontab & Job Scheduling

This lab covers Linux **Cron and Crontab** from **beginner to advanced**, including cron syntax, scheduled jobs, user crontabs, system-wide cron jobs, environment variables, logging, troubleshooting, `at`, `anacron`, and DevOps automation.

---

# 1. Check Cron Service Status

## Command

```bash
systemctl status cron
```

## Example Output

```text
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled)
     Active: active (running)
```

`systemctl status cron` checks whether the Cron service is running.

---

# 2. Check Whether Cron Is Active

## Command

```bash
systemctl is-active cron
```

## Example Output

```text
active
```

---

# 3. Check Whether Cron Starts at Boot

## Command

```bash
systemctl is-enabled cron
```

## Example Output

```text
enabled
```

---

# 4. Start Cron Service

## Command

```bash
sudo systemctl start cron
```

## Example Output

```text
```

---

# 5. Stop Cron Service

## Command

```bash
sudo systemctl stop cron
```

## Example Output

```text
```

> Be careful when stopping Cron because scheduled jobs will not execute while the service is stopped.

---

# 6. Restart Cron Service

## Command

```bash
sudo systemctl restart cron
```

## Example Output

```text
```

---

# 7. Reload Cron Service

## Command

```bash
sudo systemctl reload cron
```

## Example Output

```text
```

---

# 8. Enable Cron at Boot

## Command

```bash
sudo systemctl enable cron
```

## Example Output

```text
Created symlink /etc/systemd/system/multi-user.target.wants/cron.service
```

---

# 9. Enable and Start Cron

## Command

```bash
sudo systemctl enable --now cron
```

## Example Output

```text
```

---

# 10. Display Cron Logs

## Command

```bash
journalctl -u cron
```

## Example Output

```text
Aug 27 10:00:01 server CRON[1234]: (root) CMD (/usr/local/bin/backup.sh)
Aug 27 10:05:01 server CRON[1250]: (devops) CMD (/home/devops/test.sh)
```

---

# 11. Display Last 50 Cron Logs

## Command

```bash
journalctl -u cron -n 50
```

## Example Output

```text
Aug 27 10:00:01 server CRON[1234]: (root) CMD (/usr/local/bin/backup.sh)
Aug 27 10:05:01 server CRON[1250]: (devops) CMD (/home/devops/test.sh)
```

---

# 12. Follow Cron Logs in Real Time

## Command

```bash
journalctl -u cron -f
```

## Example Output

```text
Aug 27 12:00:01 server CRON[1500]: (devops) CMD (/home/devops/test.sh)
Aug 27 12:01:01 server CRON[1505]: (devops) CMD (/home/devops/backup.sh)
```

Press `Ctrl+C` to exit.

---

# 13. Display Current User's Crontab

## Command

```bash
crontab -l
```

## Example Output

```text
# Daily backup
0 2 * * * /home/devops/backup.sh
```

---

# 14. Edit Current User's Crontab

## Command

```bash
crontab -e
```

## Example Output

```text
# Opens the crontab editor
```

---

# 15. Remove Current User's Crontab

## Command

```bash
crontab -r
```

## Example Output

```text
```

> This removes all cron jobs for the current user.

---

# 16. Remove Crontab With Confirmation

## Command

```bash
crontab -i -r
```

## Example Output

```text
crontab: really delete devops's crontab?
```

---

# 17. Display Root User's Crontab

## Command

```bash
sudo crontab -l
```

## Example Output

```text
0 2 * * * /usr/local/bin/backup.sh
```

---

# 18. Edit Root User's Crontab

## Command

```bash
sudo crontab -e
```

## Example Output

```text
# Opens root crontab editor
```

---

# 19. Display Another User's Crontab

## Command

```bash
sudo crontab -u devops -l
```

## Example Output

```text
*/5 * * * * /home/devops/check.sh
```

---

# 20. Edit Another User's Crontab

## Command

```bash
sudo crontab -u devops -e
```

## Example Output

```text
# Opens devops user's crontab
```

---

# 21. Display Crontab Help

## Command

```bash
crontab --help
```

## Example Output

```text
Usage:
 crontab [options] file
 crontab [options]
```

---

# 22. Cron Basic Syntax

## Command

```text
* * * * * command
```

## Example Output

```text
| | | | |
| | | | +---- Day of week
| | | +------ Month
| | +-------- Day of month
| +---------- Hour
+------------ Minute
```

---

# 23. Cron Field Ranges

## Command

```text
* * * * * command
```

## Example Output

```text
Minute        0-59
Hour          0-23
Day of Month  1-31
Month         1-12
Day of Week   0-7
```

`0` and `7` generally represent Sunday.

---

# 24. Run Job Every Minute

## Command

```bash
* * * * * /home/devops/script.sh
```

## Example Output

```text
Job runs every minute.
```

---

# 25. Run Job Every 5 Minutes

## Command

```bash
*/5 * * * * /home/devops/script.sh
```

## Example Output

```text
12:00
12:05
12:10
12:15
```

---

# 26. Run Job Every 10 Minutes

## Command

```bash
*/10 * * * * /home/devops/script.sh
```

## Example Output

```text
12:00
12:10
12:20
12:30
```

---

# 27. Run Job Every 15 Minutes

## Command

```bash
*/15 * * * * /home/devops/script.sh
```

## Example Output

```text
12:00
12:15
12:30
12:45
```

---

# 28. Run Job Every 30 Minutes

## Command

```bash
*/30 * * * * /home/devops/script.sh
```

## Example Output

```text
12:00
12:30
13:00
13:30
```

---

# 29. Run Job Every Hour

## Command

```bash
0 * * * * /home/devops/script.sh
```

## Example Output

```text
13:00
14:00
15:00
16:00
```

---

# 30. Run Job Every 2 Hours

## Command

```bash
0 */2 * * * /home/devops/script.sh
```

## Example Output

```text
00:00
02:00
04:00
06:00
```

---

# 31. Run Job Every 6 Hours

## Command

```bash
0 */6 * * * /home/devops/script.sh
```

## Example Output

```text
00:00
06:00
12:00
18:00
```

---

# 32. Run Job Every Day at Midnight

## Command

```bash
0 0 * * * /home/devops/script.sh
```

## Example Output

```text
00:00 every day
```

---

# 33. Run Job Every Day at 2 AM

## Command

```bash
0 2 * * * /home/devops/script.sh
```

## Example Output

```text
02:00 every day
```

---

# 34. Run Job Every Day at 6 AM

## Command

```bash
0 6 * * * /home/devops/script.sh
```

## Example Output

```text
06:00 every day
```

---

# 35. Run Job Every Day at 10:30 PM

## Command

```bash
30 22 * * * /home/devops/script.sh
```

## Example Output

```text
22:30 every day
```

---

# 36. Run Job at Multiple Hours

## Command

```bash
0 9,12,18 * * * /home/devops/script.sh
```

## Example Output

```text
09:00
12:00
18:00
```

---

# 37. Run Job at Multiple Minutes

## Command

```bash
0,30 * * * * /home/devops/script.sh
```

## Example Output

```text
13:00
13:30
14:00
14:30
```

---

# 38. Run Job During Specific Hours

## Command

```bash
0 9-17 * * * /home/devops/script.sh
```

## Example Output

```text
09:00
10:00
11:00
12:00
13:00
14:00
15:00
16:00
17:00
```

---

# 39. Run Job Every 10 Minutes During Working Hours

## Command

```bash
*/10 9-17 * * * /home/devops/script.sh
```

## Example Output

```text
09:00
09:10
09:20
09:30
...
17:30
17:40
17:50
```

---

# 40. Run Job Every Monday

## Command

```bash
0 9 * * 1 /home/devops/script.sh
```

## Example Output

```text
Monday 09:00
```

---

# 41. Run Job Every Sunday

## Command

```bash
0 9 * * 0 /home/devops/script.sh
```

## Example Output

```text
Sunday 09:00
```

---

# 42. Run Job Monday Through Friday

## Command

```bash
0 9 * * 1-5 /home/devops/script.sh
```

## Example Output

```text
Monday 09:00
Tuesday 09:00
Wednesday 09:00
Thursday 09:00
Friday 09:00
```

---

# 43. Run Job on Weekends

## Command

```bash
0 10 * * 6,0 /home/devops/script.sh
```

## Example Output

```text
Saturday 10:00
Sunday 10:00
```

---

# 44. Run Job on First Day of Every Month

## Command

```bash
0 0 1 * * /home/devops/script.sh
```

## Example Output

```text
First day of every month at 00:00
```

---

# 45. Run Job on the 15th of Every Month

## Command

```bash
0 2 15 * * /home/devops/script.sh
```

## Example Output

```text
15th day of every month at 02:00
```

---

# 46. Run Job Every Day in January

## Command

```bash
0 9 * 1 * /home/devops/script.sh
```

## Example Output

```text
Every day at 09:00 during January
```

---

# 47. Run Job Every Quarter

## Command

```bash
0 0 1 1,4,7,10 * /home/devops/script.sh
```

## Example Output

```text
January 1
April 1
July 1
October 1
```

---

# 48. Run Job on Specific Dates

## Command

```bash
0 12 1,15 * * /home/devops/script.sh
```

## Example Output

```text
1st of every month at 12:00
15th of every month at 12:00
```

---

# 49. Run Job After System Reboot

## Command

```bash
@reboot /home/devops/startup.sh
```

## Example Output

```text
Startup script runs after system boot.
```

---

# 50. Run Job Yearly

## Command

```bash
@yearly /home/devops/yearly.sh
```

## Example Output

```text
Job runs once per year.
```

---

# 51. Run Job Annually

## Command

```bash
@annually /home/devops/yearly.sh
```

## Example Output

```text
Job runs once per year.
```

---

# 52. Run Job Monthly

## Command

```bash
@monthly /home/devops/monthly.sh
```

## Example Output

```text
Job runs once per month.
```

---

# 53. Run Job Weekly

## Command

```bash
@weekly /home/devops/weekly.sh
```

## Example Output

```text
Job runs once per week.
```

---

# 54. Run Job Daily

## Command

```bash
@daily /home/devops/daily.sh
```

## Example Output

```text
Job runs once per day.
```

---

# 55. Run Job Hourly

## Command

```bash
@hourly /home/devops/hourly.sh
```

## Example Output

```text
Job runs once per hour.
```

---

# 56. Run a Shell Script With Cron

## Command

```bash
chmod +x /home/devops/backup.sh
```

```bash
crontab -e
```

```text
0 2 * * * /home/devops/backup.sh
```

## Example Output

```text
Backup script runs every day at 02:00.
```

---

# 57. Run Cron Job With Bash Explicitly

## Command

```bash
0 2 * * * /bin/bash /home/devops/backup.sh
```

## Example Output

```text
Backup script executed at 02:00.
```

---

# 58. Redirect Cron Output to a Log File

## Command

```bash
*/5 * * * * /home/devops/check.sh >> /home/devops/cron.log 2>&1
```

## Example Output

```text
Cron output is written to:

/home/devops/cron.log
```

---

# 59. Redirect Standard Output Only

## Command

```bash
*/5 * * * * /home/devops/check.sh >> /home/devops/cron.log
```

## Example Output

```text
Command output is stored in cron.log.
```

---

# 60. Redirect Errors Only

## Command

```bash
*/5 * * * * /home/devops/check.sh 2>> /home/devops/cron-error.log
```

## Example Output

```text
Errors are stored in:

/home/devops/cron-error.log
```

---

# 61. Redirect Output and Errors to Different Files

## Command

```bash
*/5 * * * * /home/devops/check.sh >> /home/devops/output.log 2>> /home/devops/error.log
```

## Example Output

```text
output.log → Standard output
error.log  → Error output
```

---

# 62. Discard Cron Output

## Command

```bash
*/5 * * * * /home/devops/check.sh >/dev/null 2>&1
```

## Example Output

```text
No output is stored.
```

---

# 63. Send Cron Output to Mail

## Command

```bash
MAILTO="devops@example.com"
0 2 * * * /home/devops/backup.sh
```

## Example Output

```text
Cron output can be sent through the system mail configuration.
```

---

# 64. Disable Cron Email

## Command

```bash
MAILTO=""
```

## Example Output

```text
Cron email notifications disabled.
```

---

# 65. Set PATH in Crontab

## Command

```bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

## Example Output

```text
Cron uses the specified PATH.
```

---

# 66. Set Environment Variable in Crontab

## Command

```bash
APP_ENV=production
```

## Example Output

```text
APP_ENV is available to cron jobs.
```

---

# 67. Use Environment Variable in Cron Job

## Command

```bash
APP_ENV=production
0 * * * * /home/devops/check.sh
```

## Example Output

```text
Cron job runs with:

APP_ENV=production
```

---

# 68. Display Current PATH

## Command

```bash
echo "$PATH"
```

## Example Output

```text
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

---

# 69. Check Cron Environment

## Command

```bash
env
```

## Example Output

```text
HOME=/home/devops
LOGNAME=devops
PATH=/usr/bin:/bin
SHELL=/bin/sh
```

---

# 70. Check Current Shell

## Command

```bash
echo "$SHELL"
```

## Example Output

```text
/bin/bash
```

---

# 71. Check Current User

## Command

```bash
whoami
```

## Example Output

```text
devops
```

---

# 72. Test Cron With a Simple Date Job

## Command

```bash
* * * * * date >> /tmp/cron-test.log 2>&1
```

## Example Output

```text
Thu Aug 27 12:00:01 IST 2026
Thu Aug 27 12:01:01 IST 2026
Thu Aug 27 12:02:01 IST 2026
```

---

# 73. Check Cron Test Log

## Command

```bash
cat /tmp/cron-test.log
```

## Example Output

```text
Thu Aug 27 12:00:01 IST 2026
Thu Aug 27 12:01:01 IST 2026
```

---

# 74. Monitor Cron Test Log

## Command

```bash
tail -f /tmp/cron-test.log
```

## Example Output

```text
Thu Aug 27 12:00:01 IST 2026
Thu Aug 27 12:01:01 IST 2026
Thu Aug 27 12:02:01 IST 2026
```

Press `Ctrl+C` to exit.

---

# 75. Check Cron Logs Using grep

## Command

```bash
journalctl -u cron | grep CRON
```

## Example Output

```text
Aug 27 12:00:01 server CRON[1500]: (devops) CMD (date >> /tmp/cron-test.log)
```

---

# 76. Check Cron Logs for a Specific User

## Command

```bash
journalctl -u cron | grep '(devops)'
```

## Example Output

```text
Aug 27 12:00:01 server CRON[1500]: (devops) CMD (/home/devops/check.sh)
```

---

# 77. Check Today's Cron Logs

## Command

```bash
journalctl -u cron --since today
```

## Example Output

```text
Aug 27 10:00:01 server CRON[1234]: (root) CMD (/usr/local/bin/backup.sh)
Aug 27 11:00:01 server CRON[1250]: (devops) CMD (/home/devops/check.sh)
```

---

# 78. Check Cron Logs From the Last Hour

## Command

```bash
journalctl -u cron --since "1 hour ago"
```

## Example Output

```text
Aug 27 11:00:01 server CRON[1250]: (devops) CMD (/home/devops/check.sh)
Aug 27 11:30:01 server CRON[1300]: (devops) CMD (/home/devops/check.sh)
```

---

# 79. Check Traditional Cron Log

## Command

```bash
sudo grep CRON /var/log/syslog
```

## Example Output

```text
Aug 27 12:00:01 server CRON[1500]: (devops) CMD (/home/devops/check.sh)
```

---

# 80. Follow Traditional Cron Log

## Command

```bash
sudo tail -f /var/log/syslog | grep CRON
```

## Example Output

```text
Aug 27 12:01:01 server CRON[1505]: (devops) CMD (/home/devops/check.sh)
```

---

# 81. Check System Cron Directory

## Command

```bash
ls -lah /etc/cron.d
```

## Example Output

```text
-rw-r--r-- 1 root root 250 backup
-rw-r--r-- 1 root root 180 monitoring
```

---

# 82. Display System Cron File

## Command

```bash
cat /etc/cron.d/backup
```

## Example Output

```text
0 2 * * * root /usr/local/bin/backup.sh
```

---

# 83. Check Hourly Cron Jobs

## Command

```bash
ls -lah /etc/cron.hourly/
```

## Example Output

```text
-rwxr-xr-x 1 root root 500 cleanup
-rwxr-xr-x 1 root root 350 update
```

---

# 84. Check Daily Cron Jobs

## Command

```bash
ls -lah /etc/cron.daily/
```

## Example Output

```text
-rwxr-xr-x 1 root root 120 logrotate
-rwxr-xr-x 1 root root 250 updatedb
```

---

# 85. Check Weekly Cron Jobs

## Command

```bash
ls -lah /etc/cron.weekly/
```

## Example Output

```text
-rwxr-xr-x 1 root root 300 cleanup
```

---

# 86. Check Monthly Cron Jobs

## Command

```bash
ls -lah /etc/cron.monthly/
```

## Example Output

```text
-rwxr-xr-x 1 root root 200 maintenance
```

---

# 87. Check Main Cron Configuration

## Command

```bash
cat /etc/crontab
```

## Example Output

```text
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# m h dom mon dow user command
17 * * * * root cd / && run-parts --report /etc/cron.hourly
```

> `/etc/crontab` includes an additional **user field** compared with a normal user crontab.

---

# 88. Display Cron Allow File

## Command

```bash
sudo cat /etc/cron.allow
```

## Example Output

```text
devops
admin
```

---

# 89. Display Cron Deny File

## Command

```bash
sudo cat /etc/cron.deny
```

## Example Output

```text
guest
testuser
```

---

# 90. Check Cron Allow/Deny Files

## Command

```bash
ls -l /etc/cron.allow /etc/cron.deny 2>/dev/null
```

## Example Output

```text
-rw-r----- 1 root root 20 /etc/cron.allow
```

---

# 91. Check Crontab Storage Directory

## Command

```bash
sudo ls -lah /var/spool/cron/crontabs/
```

## Example Output

```text
-rw------- 1 devops crontab 980 Aug 27 12:00 devops
```

> Do not manually edit files under `/var/spool/cron/crontabs/`. Use `crontab -e`.

---

# 92. Find Cron Configuration Files

## Command

```bash
find /etc -iname '*cron*' -type f
```

## Example Output

```text
/etc/crontab
/etc/cron.d/anacron
/etc/cron.d/e2scrub_all
/etc/cron.d/backup
```

---

# 93. Check Cron Process

## Command

```bash
ps aux | grep '[c]ron'
```

## Example Output

```text
root      900  0.0  0.1  12345  2048 ?  Ss  10:00  0:00 /usr/sbin/cron
```

---

# 94. Find Cron Process ID

## Command

```bash
pgrep -x cron
```

## Example Output

```text
900
```

---

# 95. Display Cron Process Details

## Command

```bash
ps -fp "$(pgrep -x cron)"
```

## Example Output

```text
UID   PID  PPID C STIME TTY  TIME CMD
root  900     1 0 10:00 ?    00:00:00 /usr/sbin/cron
```

---

# 96. Check Cron Executable

## Command

```bash
which cron
```

## Example Output

```text
/usr/sbin/cron
```

---

# 97. Check Cron Binary

## Command

```bash
ls -l /usr/sbin/cron
```

## Example Output

```text
-rwxr-xr-x 1 root root 51776 /usr/sbin/cron
```

---

# 98. Check Script Permissions

## Command

```bash
ls -l /home/devops/backup.sh
```

## Example Output

```text
-rwxr-xr-x 1 devops devops 850 Aug 27 10:00 /home/devops/backup.sh
```

---

# 99. Make Script Executable

## Command

```bash
chmod +x /home/devops/backup.sh
```

## Example Output

```text
```

---

# 100. Test Script Manually Before Cron

## Command

```bash
/home/devops/backup.sh
```

## Example Output

```text
Backup completed successfully.
```

> Always test a script manually before scheduling it with Cron.

---

# 101. Run Script Using Absolute Bash Path

## Command

```bash
/bin/bash /home/devops/backup.sh
```

## Example Output

```text
Backup completed successfully.
```

---

# 102. Check Script Syntax

## Command

```bash
bash -n /home/devops/backup.sh
```

## Example Output

```text
```

No output normally means there is no syntax error.

---

# 103. Debug Bash Script

## Command

```bash
bash -x /home/devops/backup.sh
```

## Example Output

```text
+ DATE=2026-08-27
+ mkdir -p /backup
+ tar -czf /backup/app.tar.gz /opt/app
+ echo 'Backup completed'
Backup completed
```

---

# 104. Use Full Paths in Cron

## Command

```bash
0 2 * * * /usr/bin/python3 /home/devops/script.py
```

## Example Output

```text
Python script runs at 02:00.
```

> Cron has a limited environment, so using absolute paths is recommended.

---

# 105. Run Python Script With Cron

## Command

```bash
*/10 * * * * /usr/bin/python3 /home/devops/script.py >> /home/devops/python-cron.log 2>&1
```

## Example Output

```text
Python script executed every 10 minutes.
```

---

# 106. Run Docker Command With Cron

## Command

```bash
0 2 * * * /usr/bin/docker system prune -f >> /var/log/docker-cleanup.log 2>&1
```

## Example Output

```text
Total reclaimed space: 1.2GB
```

> The Cron user must have permission to run Docker.

---

# 107. Run Docker Compose Command With Cron

## Command

```bash
0 2 * * * cd /opt/myapp && /usr/bin/docker compose pull >> /var/log/app-update.log 2>&1
```

## Example Output

```text
Pulling latest images...
Image pulled successfully.
```

---

# 108. Run Backup Command With Cron

## Command

```bash
0 2 * * * tar -czf /backup/app-$(date +\%F).tar.gz /opt/app
```

## Example Output

```text
/backup/app-2026-08-27.tar.gz
```

> In a crontab, `%` has special meaning. Escape it as `\%` when it is intended for the command.

---

# 109. Run Database Backup With Cron

## Command

```bash
0 2 * * * /usr/bin/mysqldump -u backupuser -p'PASSWORD' database > /backup/database-$(date +\%F).sql
```

## Example Output

```text
/backup/database-2026-08-27.sql
```

> Avoid placing passwords directly in crontab files in production. Prefer a protected credentials file or another secure mechanism.

---

# 110. Delete Old Backup Files

## Command

```bash
0 3 * * * /usr/bin/find /backup -type f -mtime +7 -delete
```

## Example Output

```text
Files older than 7 days are removed.
```

---

# 111. Check Disk Space With Cron

## Command

```bash
0 * * * * /bin/df -h > /tmp/disk-usage.txt
```

## Example Output

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   45G   49G  48% /
```

---

# 112. Create Disk Monitoring Cron Job

## Command

```bash
*/10 * * * * /bin/df -h / | /usr/bin/tail -1 >> /var/log/disk-monitor.log
```

## Example Output

```text
/dev/sda2 99G 45G 49G 48% /
```

---

# 113. Check Cron Job Environment

## Command

```bash
* * * * * env > /tmp/cron-env.txt
```

## Example Output

```text
HOME=/home/devops
LOGNAME=devops
PATH=/usr/bin:/bin
SHELL=/bin/sh
```

---

# 114. Compare Interactive and Cron Environment

## Command

```bash
env > /tmp/interactive-env.txt
```

```bash
diff /tmp/interactive-env.txt /tmp/cron-env.txt
```

## Example Output

```text
PATH values may differ.
SHELL values may differ.
HOME may differ.
```

---

# 115. Check Cron Timezone

## Command

```bash
timedatectl
```

## Example Output

```text
Local time: Thu 2026-08-27 12:00:00 IST
Time zone: Asia/Kolkata (IST, +0530)
System clock synchronized: yes
```

---

# 116. Display Current Date and Time

## Command

```bash
date
```

## Example Output

```text
Thu Aug 27 12:00:00 IST 2026
```

---

# 117. Display Current Timezone

## Command

```bash
timedatectl | grep "Time zone"
```

## Example Output

```text
Time zone: Asia/Kolkata (IST, +0530)
```

---

# 118. Display Timezone Environment

## Command

```bash
echo "$TZ"
```

## Example Output

```text
Asia/Kolkata
```

---

# 119. Set Timezone for a Cron Job

## Command

```bash
TZ=Asia/Kolkata
0 9 * * * /home/devops/report.sh
```

## Example Output

```text
Report runs at 09:00 in the configured timezone.
```

> Timezone behavior can depend on the Cron implementation and system configuration. Verify the behavior on your Linux distribution.

---

# 120. Check if a Cron Job Is Installed

## Command

```bash
crontab -l | grep backup
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
```

---

# 121. Search Cron Jobs

## Command

```bash
crontab -l | grep -v '^#' | grep -v '^$'
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
*/5 * * * * /home/devops/health-check.sh
```

---

# 122. Count Active Cron Jobs

## Command

```bash
crontab -l 2>/dev/null | grep -v '^#' | grep -v '^$' | wc -l
```

## Example Output

```text
5
```

---

# 123. Backup Current Crontab

## Command

```bash
crontab -l > ~/crontab-backup.txt
```

## Example Output

```text
```

---

# 124. Restore Crontab From Backup

## Command

```bash
crontab ~/crontab-backup.txt
```

## Example Output

```text
```

---

# 125. Copy Crontab to Another Server

## Command

```bash
scp ~/crontab-backup.txt devops@server:/tmp/
```

## Example Output

```text
crontab-backup.txt 100% 500 10KB/s 00:00
```

---

# 126. Install Crontab From a File

## Command

```bash
crontab /tmp/crontab-backup.txt
```

## Example Output

```text
```

---

# 127. Check Installed Cron Jobs After Restore

## Command

```bash
crontab -l
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
*/5 * * * * /home/devops/health-check.sh
```

---

# 128. Find Jobs Running Every Minute

## Command

```bash
crontab -l | grep '^\* \* \* \* \*'
```

## Example Output

```text
* * * * * /home/devops/health-check.sh
```

---

# 129. Find Jobs Running Daily

## Command

```bash
crontab -l | grep -E '^(@daily|0 [0-9]+ \* \* \*)'
```

## Example Output

```text
@daily /home/devops/report.sh
0 2 * * * /home/devops/backup.sh
```

---

# 130. Find Jobs Related to Backup

## Command

```bash
crontab -l | grep -i backup
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
0 3 * * * /home/devops/delete-old-backups.sh
```

---

# 131. Check Cron Service Dependencies

## Command

```bash
systemctl list-dependencies cron
```

## Example Output

```text
cron.service
├─system.slice
├─sysinit.target
└─basic.target
```

---

# 132. Display Cron Service Properties

## Command

```bash
systemctl show cron
```

## Example Output

```text
Id=cron.service
LoadState=loaded
ActiveState=active
SubState=running
```

---

# 133. Check Cron Service Start Time

## Command

```bash
systemctl show cron -p ActiveEnterTimestamp
```

## Example Output

```text
ActiveEnterTimestamp=Thu 2026-08-27 10:00:00 IST
```

---

# 134. Check Failed Cron Service

## Command

```bash
systemctl --failed | grep cron
```

## Example Output

```text
```

No output means no failed Cron service is listed.

---

# 135. Check Cron Journal Errors

## Command

```bash
journalctl -u cron -p err
```

## Example Output

```text
No entries.
```

---

# 136. Check Cron Service Since Boot

## Command

```bash
journalctl -u cron -b
```

## Example Output

```text
Aug 27 10:00:00 server systemd[1]: Started cron.service.
Aug 27 10:01:01 server CRON[1234]: (root) CMD (/usr/local/bin/job.sh)
```

---

# 137. Check Cron Job With Specific Command

## Command

```bash
journalctl -u cron | grep '/home/devops/backup.sh'
```

## Example Output

```text
Aug 27 02:00:01 server CRON[3000]: (devops) CMD (/home/devops/backup.sh)
```

---

# 138. Check Cron Jobs for Root

## Command

```bash
sudo journalctl -u cron | grep '(root)'
```

## Example Output

```text
Aug 27 02:00:01 server CRON[3000]: (root) CMD (/usr/local/bin/backup.sh)
```

---

# 139. Check Cron Jobs for Current User

## Command

```bash
journalctl -u cron | grep "($(whoami))"
```

## Example Output

```text
Aug 27 12:00:01 server CRON[1500]: (devops) CMD (/home/devops/check.sh)
```

---

# 140. Test Whether Cron Can Execute a Command

## Command

```bash
* * * * * /usr/bin/touch /tmp/cron-working
```

## Example Output

```text
```

---

# 141. Verify Cron Execution

## Command

```bash
ls -l /tmp/cron-working
```

## Example Output

```text
-rw-r--r-- 1 devops devops 0 Aug 27 12:05 /tmp/cron-working
```

---

# 142. Check Cron Execution Time

## Command

```bash
stat /tmp/cron-working
```

## Example Output

```text
Access: 2026-08-27 12:05:01
Modify: 2026-08-27 12:05:01
Change: 2026-08-27 12:05:01
```

---

# 143. Remove Test Cron Job

## Command

```bash
crontab -e
```

```text
# Remove the test line:

* * * * * /usr/bin/touch /tmp/cron-working
```

## Example Output

```text
Test cron job removed.
```

---

# 144. Use `at` for One-Time Jobs

## Command

```bash
echo "/home/devops/backup.sh" | at 23:00
```

## Example Output

```text
job 12 at Thu Aug 27 23:00:00 2026
```

> `at` is designed for one-time scheduled jobs, while Cron is designed primarily for recurring jobs.

---

# 145. List Pending `at` Jobs

## Command

```bash
atq
```

## Example Output

```text
12      Thu Aug 27 23:00:00 2026 a devops
```

---

# 146. Display an `at` Job

## Command

```bash
at -c 12
```

## Example Output

```text
#!/bin/sh
/home/devops/backup.sh
```

---

# 147. Delete an `at` Job

## Command

```bash
atrm 12
```

## Example Output

```text
```

---

# 148. Check `atd` Service

## Command

```bash
systemctl status atd
```

## Example Output

```text
● atd.service - Deferred execution scheduler
     Active: active (running)
```

---

# 149. Start `atd`

## Command

```bash
sudo systemctl enable --now atd
```

## Example Output

```text
```

---

# 150. Check Anacron Configuration

## Command

```bash
cat /etc/anacrontab
```

## Example Output

```text
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

1       5       cron.daily      run-parts --report /etc/cron.daily
7       10      cron.weekly     run-parts --report /etc/cron.weekly
@monthly 15     cron.monthly    run-parts --report /etc/cron.monthly
```

---

# 151. Check Anacron Service

## Command

```bash
systemctl status anacron
```

## Example Output

```text
● anacron.service
     Active: inactive (dead)
```

> Depending on the Linux distribution, Anacron may be triggered by other system scheduling mechanisms rather than running continuously as a daemon.

---

# 152. Run Anacron Manually

## Command

```bash
sudo anacron -n
```

## Example Output

```text
Anacron jobs started
```

---

# 153. Force Anacron Jobs

## Command

```bash
sudo anacron -f
```

## Example Output

```text
Running scheduled jobs
```

---

# 154. Check Anacron Spool

## Command

```bash
ls -lah /var/spool/anacron/
```

## Example Output

```text
-rw------- 1 root root 9 Aug 27 cron.daily
-rw------- 1 root root 9 Aug 24 cron.weekly
```

---

# 155. Check Cron Package

## Command

```bash
dpkg -l | grep cron
```

## Example Output

```text
ii  cron  3.0pl1-184ubuntu2  amd64  process scheduling daemon
```

---

# 156. Check Cron Package With apt

## Command

```bash
apt policy cron
```

## Example Output

```text
cron:
  Installed: 3.0pl1-184ubuntu2
  Candidate: 3.0pl1-184ubuntu2
```

---

# 157. Install Cron

## Command

```bash
sudo apt update
sudo apt install cron
```

## Example Output

```text
cron is already the newest version.
```

---

# 158. Check Cron Configuration Permissions

## Command

```bash
ls -ld /etc/cron.d /etc/cron.daily /etc/cron.hourly /etc/cron.weekly /etc/cron.monthly
```

## Example Output

```text
drwxr-xr-x root root /etc/cron.d
drwxr-xr-x root root /etc/cron.daily
drwxr-xr-x root root /etc/cron.hourly
drwxr-xr-x root root /etc/cron.weekly
drwxr-xr-x root root /etc/cron.monthly
```

---

# 159. Check Script Ownership

## Command

```bash
ls -l /usr/local/bin/backup.sh
```

## Example Output

```text
-rwxr-xr-x 1 root root 850 Aug 27 10:00 /usr/local/bin/backup.sh
```

---

# 160. Check Script Directory Permissions

## Command

```bash
namei -l /home/devops/backup.sh
```

## Example Output

```text
f: /home/devops/backup.sh
drwxr-xr-x root   root   /
drwxr-xr-x root   root   home
drwx------ devops devops devops
-rwxr-xr-x devops devops backup.sh
```

---

# 161. Check Cron User Permissions

## Command

```bash
id devops
```

## Example Output

```text
uid=1001(devops) gid=1001(devops) groups=1001(devops),999(docker)
```

---

# 162. Check Whether Cron Can Access a Directory

## Command

```bash
sudo -u devops ls -la /home/devops
```

## Example Output

```text
-rwxr-xr-x backup.sh
-rw-r--r-- cron.log
```

---

# 163. Check Cron Job Command With `sudo`

## Command

```bash
sudo -u devops /home/devops/backup.sh
```

## Example Output

```text
Backup completed successfully.
```

---

# 164. Check Cron Job Using `runuser`

## Command

```bash
sudo runuser -u devops -- /home/devops/backup.sh
```

## Example Output

```text
Backup completed successfully.
```

---

# 165. Prevent Concurrent Cron Jobs With flock

## Command

```bash
*/5 * * * * /usr/bin/flock -n /tmp/backup.lock /home/devops/backup.sh
```

## Example Output

```text
Only one backup instance runs at a time.
```

---

# 166. Use flock With Log File

## Command

```bash
*/5 * * * * /usr/bin/flock -n /tmp/backup.lock /home/devops/backup.sh >> /var/log/backup.log 2>&1
```

## Example Output

```text
Backup job executed.
```

---

# 167. Check Lock File

## Command

```bash
ls -l /tmp/backup.lock
```

## Example Output

```text
-rw-r--r-- 1 devops devops 0 Aug 27 12:00 /tmp/backup.lock
```

---

# 168. Check Running Backup Process

## Command

```bash
pgrep -af backup.sh
```

## Example Output

```text
2451 /bin/bash /home/devops/backup.sh
```

---

# 169. Find Cron-Started Processes

## Command

```bash
ps -ef --forest | grep -i cron
```

## Example Output

```text
root   900  1  /usr/sbin/cron
devops 2451 900 /bin/bash /home/devops/backup.sh
```

---

# 170. Monitor Cron Processes

## Command

```bash
watch -n 1 'pgrep -af cron'
```

## Example Output

```text
900 /usr/sbin/cron
```

Press `Ctrl+C` to exit.

---

# 171. Check Cron Resource Usage

## Command

```bash
ps -C cron -o pid,ppid,%cpu,%mem,etime,cmd
```

## Example Output

```text
PID  PPID %CPU %MEM     ELAPSED CMD
900     1 0.0  0.1       02:00 /usr/sbin/cron
```

---

# 172. Run Cron Job With Timeout

## Command

```bash
*/5 * * * * /usr/bin/timeout 300 /home/devops/backup.sh
```

## Example Output

```text
Backup is allowed to run for a maximum of 300 seconds.
```

---

# 173. Create a Health Check Cron Job

## Command

```bash
*/5 * * * * /usr/bin/curl -fsS http://localhost:8080/health >> /var/log/health-check.log 2>&1
```

## Example Output

```text
{"status":"healthy"}
```

---

# 174. Check Application Health With Cron

## Command

```bash
*/5 * * * * /usr/bin/curl -fsS http://localhost:8080/health || /usr/local/bin/restart-app.sh
```

## Example Output

```text
Application healthy.
```

---

# 175. Schedule Log Cleanup

## Command

```bash
0 1 * * * /usr/bin/find /var/log/myapp -type f -mtime +30 -delete
```

## Example Output

```text
Log files older than 30 days are deleted.
```

---

# 176. Schedule Temporary File Cleanup

## Command

```bash
0 3 * * * /usr/bin/find /tmp/myapp -type f -mtime +7 -delete
```

## Example Output

```text
Temporary files older than 7 days are deleted.
```

---

# 177. Schedule Docker Log Cleanup Script

## Command

```bash
0 3 * * * /usr/local/bin/docker-log-cleanup.sh >> /var/log/docker-cleanup.log 2>&1
```

## Example Output

```text
Docker log cleanup completed.
```

---

# 178. Schedule Git Repository Backup

## Command

```bash
0 1 * * * /usr/local/bin/git-backup.sh >> /var/log/git-backup.log 2>&1
```

## Example Output

```text
Git repository backup completed.
```

---

# 179. Schedule Server Health Report

## Command

```bash
0 8 * * * /usr/local/bin/server-health.sh > /var/log/server-health.log 2>&1
```

## Example Output

```text
CPU: 18%
Memory: 42%
Disk: 58%
Services: OK
```

---

# 180. Schedule Certificate Expiry Check

## Command

```bash
0 9 * * * /usr/local/bin/check-certificates.sh >> /var/log/certificate-check.log 2>&1
```

## Example Output

```text
example.com certificate expires in 72 days.
```

---

# 181. Schedule Service Status Check

## Command

```bash
*/10 * * * * /usr/bin/systemctl is-active --quiet nginx || /usr/bin/systemctl restart nginx
```

## Example Output

```text
nginx service is active.
```

> Use automated service restarts carefully in production.

---

# 182. Schedule Nginx Configuration Check

## Command

```bash
0 4 * * * /usr/sbin/nginx -t >> /var/log/nginx-config-check.log 2>&1
```

## Example Output

```text
syntax is ok
test is successful
```

---

# 183. Schedule Database Health Check

## Command

```bash
*/5 * * * * /usr/bin/mysqladmin ping -u root -p'PASSWORD' >> /var/log/mysql-health.log 2>&1
```

## Example Output

```text
mysqld is alive
```

> Do not expose production database passwords in crontab. Use secure credentials management.

---

# 184. Schedule Disk Alert Script

## Command

```bash
*/10 * * * * /usr/local/bin/disk-alert.sh >> /var/log/disk-alert.log 2>&1
```

## Example Output

```text
Disk usage: 82%
Warning threshold: 80%
```

---

# 185. Check Disk Usage Before Running Backup

## Command

```bash
0 2 * * * /bin/df -P /backup | /usr/bin/awk 'NR==2 {gsub("%","",$5); if ($5 < 80) system("/home/devops/backup.sh")}'
```

## Example Output

```text
Backup started because disk usage is below 80%.
```

---

# 186. Use a Wrapper Script for Complex Cron Jobs

## Command

```bash
#!/bin/bash

set -e

/usr/bin/df -h
/usr/bin/systemctl is-active nginx
/usr/bin/curl -fsS http://localhost:8080/health
```

## Example Output

```text
Filesystem      Size  Used Avail Use%
/dev/sda2        99G   45G   49G  48%

active

{"status":"healthy"}
```

---

# 187. Schedule Wrapper Script

## Command

```bash
*/10 * * * * /usr/local/bin/server-health.sh >> /var/log/server-health.log 2>&1
```

## Example Output

```text
Server health check completed.
```

---

# 188. Check for Duplicate Cron Jobs

## Command

```bash
crontab -l | sort | uniq -d
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
```

---

# 189. Sort Cron Jobs

## Command

```bash
crontab -l | grep -v '^#' | sort
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
0 3 * * * /home/devops/cleanup.sh
*/5 * * * * /home/devops/health.sh
```

---

# 190. Validate Cron Expression Manually

## Command

```bash
date
```

```bash
crontab -l
```

## Example Output

```text
Current time:
Thu Aug 27 12:00:00 IST 2026

Cron:
0 13 * * * /home/devops/script.sh
```

The job will run at `13:00` every day.

---

# 191. Install Cron Expression Helper

## Command

```bash
sudo apt install cron-utils
```

## Example Output

```text
cron-utils installed successfully.
```

> Package availability varies by Linux distribution. Use the package manager for your distribution.

---

# 192. Check Cron Job Syntax With a Linter

## Command

```bash
crontab -e
```

## Example Output

```text
# Use valid five-field cron syntax:
0 2 * * * /home/devops/backup.sh
```

> Cron implementations may reject invalid syntax when the crontab is installed.

---

# 193. Check Installed Crontab After Editing

## Command

```bash
crontab -l
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
*/5 * * * * /home/devops/health.sh
```

---

# 194. Check Cron Job Ownership

## Command

```bash
sudo crontab -u devops -l
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
```

The job executes with the permissions of the `devops` user.

---

# 195. Run Cron Job as Root

## Command

```bash
sudo crontab -e
```

```text
0 2 * * * /usr/local/bin/root-backup.sh
```

## Example Output

```text
Root backup runs every day at 02:00.
```

---

# 196. Understand User Crontab vs System Crontab

## Command

```bash
crontab -e
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
```

System-wide:

```bash
sudo cat /etc/crontab
```

## Example Output

```text
0 2 * * * root /usr/local/bin/backup.sh
```

User crontab:

```text
minute hour day month weekday command
```

System crontab:

```text
minute hour day month weekday user command
```

---

# 197. Check Cron Environment From a Script

## Command

```bash
#!/bin/bash

{
    echo "DATE=$(date)"
    echo "USER=$(whoami)"
    echo "HOME=$HOME"
    echo "PATH=$PATH"
    echo "SHELL=$SHELL"
} >> /tmp/cron-debug.log
```

## Example Output

```text
DATE=Thu Aug 27 12:00:01 IST 2026
USER=devops
HOME=/home/devops
PATH=/usr/bin:/bin
SHELL=/bin/sh
```

---

# 198. Debug a Cron Job

## Command

```bash
crontab -l
```

```bash
journalctl -u cron -n 100
```

```bash
tail -100 /var/log/syslog | grep CRON
```

```bash
ls -l /home/devops/script.sh
```

```bash
/home/devops/script.sh
```

## Example Output

```text
Cron entry exists.
Cron service is running.
Cron execution is visible in logs.
Script is executable.
Script works manually.
```

---

# 199. Check Common Cron Problems

## Command

```bash
systemctl status cron
crontab -l
ls -l /home/devops/script.sh
/home/devops/script.sh
journalctl -u cron -n 50
```

## Example Output

```text
Cron service: active
Crontab: configured
Script: executable
Manual execution: successful
Cron logs: job executed
```

---

# 200. Production Cron Troubleshooting Flow

## Command

```bash
# 1. Check Cron service
systemctl status cron

# 2. Check current user's cron jobs
crontab -l

# 3. Check root cron jobs
sudo crontab -l

# 4. Check system cron configuration
cat /etc/crontab

# 5. Check cron directories
ls -lah /etc/cron.d
ls -lah /etc/cron.daily
ls -lah /etc/cron.hourly

# 6. Check Cron logs
journalctl -u cron -n 100

# 7. Check traditional logs
sudo grep CRON /var/log/syslog

# 8. Check script permissions
ls -l /path/to/script.sh

# 9. Test script manually
/path/to/script.sh

# 10. Check script syntax
bash -n /path/to/script.sh

# 11. Check required commands
which bash
which python3
which curl
which docker

# 12. Check environment
env

# 13. Check disk space
df -h

# 14. Check running process
pgrep -af script.sh
```

## Example Output

```text
Cron service      → active
Crontab           → configured
System cron       → configured
Cron logs         → job executed
Permissions       → executable
Manual execution  → successful
Script syntax     → valid
Dependencies      → available
Disk space        → available
Process            → running/completed
```

---

# 📚 Cron Special Scheduling Keywords

## Command

```text
@reboot
@yearly
@annually
@monthly
@weekly
@daily
@midnight
@hourly
```

## Example Output

```text
@reboot    → Run after reboot
@yearly    → Run once a year
@annually  → Run once a year
@monthly   → Run once a month
@weekly    → Run once a week
@daily     → Run once a day
@midnight  → Run once a day around midnight
@hourly    → Run once an hour
```

---

# 📚 Cron Operators

## Command

```text
*       Any value
,       Multiple values
-       Range
/       Step value
```

## Example Output

```text
*       Every value
1,5     Values 1 and 5
1-5     Values from 1 through 5
*/5     Every 5 units
```

---

# 📚 Cron Examples Cheat Sheet

## Command

```text
* * * * * command
*/5 * * * * command
*/10 * * * * command
*/15 * * * * command
0 * * * * command
0 */2 * * * command
0 0 * * * command
0 2 * * * command
30 22 * * * command
0 9 * * 1 command
0 9 * * 1-5 command
0 10 * * 6,0 command
0 0 1 * * command
0 2 15 * * command
@reboot command
@daily command
@weekly command
@monthly command
@yearly command
```

## Example Output

```text
Every minute
Every 5 minutes
Every 10 minutes
Every 15 minutes
Every hour
Every 2 hours
Every midnight
Every day at 02:00
Every day at 22:30
Every Monday at 09:00
Monday-Friday at 09:00
Saturday-Sunday at 10:00
First day of every month
15th day of every month
After system reboot
Daily
Weekly
Monthly
Yearly
```

---

# 📚 Important Cron Files and Directories

## Command

```bash
/etc/crontab
/etc/cron.d/
/etc/cron.hourly/
/etc/cron.daily/
/etc/cron.weekly/
/etc/cron.monthly/
/etc/cron.allow
/etc/cron.deny
/var/spool/cron/crontabs/
```

## Example Output

```text
/etc/crontab                    → System-wide Cron configuration
/etc/cron.d/                    → Additional system Cron jobs
/etc/cron.hourly/               → Hourly jobs
/etc/cron.daily/                → Daily jobs
/etc/cron.weekly/               → Weekly jobs
/etc/cron.monthly/              → Monthly jobs
/etc/cron.allow                 → Users allowed to use Cron
/etc/cron.deny                  → Users denied from using Cron
/var/spool/cron/crontabs/       → User crontab storage
```

---

# 📚 Cron Related Commands Summary

## Command

```bash
crontab -l
crontab -e
crontab -r
crontab -i -r
sudo crontab -l
sudo crontab -e
sudo crontab -u devops -l
sudo crontab -u devops -e
systemctl status cron
systemctl start cron
systemctl stop cron
systemctl restart cron
systemctl reload cron
systemctl enable cron
systemctl enable --now cron
systemctl is-active cron
systemctl is-enabled cron
journalctl -u cron
journalctl -u cron -f
journalctl -u cron -n 50
journalctl -u cron --since today
journalctl -u cron --since "1 hour ago"
ps aux | grep '[c]ron'
pgrep -x cron
cat /etc/crontab
ls -lah /etc/cron.d
ls -lah /etc/cron.daily
ls -lah /etc/cron.hourly
ls -lah /etc/cron.weekly
ls -lah /etc/cron.monthly
cat /etc/cron.allow
cat /etc/cron.deny
at
atq
at -c
atrm
anacron
```

## Example Output

```text
Crontab Management
Cron Service Management
Cron Job Scheduling
Cron Job Monitoring
Cron Log Analysis
System Cron Management
One-Time Job Scheduling
Anacron Management
Production Automation
```

---

# 🧪 Practical Cron Lab

## Command

```bash
# Step 1: Create a test script

cat > /tmp/cron-test.sh <<'EOF'
#!/bin/bash
echo "Cron executed at $(date)" >> /tmp/cron-test.log
EOF

# Step 2: Make it executable

chmod +x /tmp/cron-test.sh

# Step 3: Test manually

/tmp/cron-test.sh

# Step 4: Verify the log

cat /tmp/cron-test.log

# Step 5: Add Cron job

crontab -e
```

```text
* * * * * /tmp/cron-test.sh
```

## Example Output

```text
Cron executed at Thu Aug 27 12:00:01 IST 2026
Cron executed at Thu Aug 27 12:01:01 IST 2026
Cron executed at Thu Aug 27 12:02:01 IST 2026
```

---

# 🧪 Practical Backup Cron Lab

## Command

```bash
mkdir -p /home/devops/backups

cat > /home/devops/backup.sh <<'EOF'
#!/bin/bash

SOURCE="/home/devops/app"
DEST="/home/devops/backups"

mkdir -p "$DEST"

tar -czf "$DEST/app-$(date +%F).tar.gz" "$SOURCE"

echo "Backup completed at $(date)"
EOF

chmod +x /home/devops/backup.sh

/home/devops/backup.sh
```

```bash
crontab -e
```

```text
0 2 * * * /home/devops/backup.sh >> /home/devops/backup.log 2>&1
```

## Example Output

```text
Backup completed at Thu Aug 27 02:00:01 IST 2026
```

---

# 🧪 Practical Health Check Cron Lab

## Command

```bash
cat > /home/devops/health-check.sh <<'EOF'
#!/bin/bash

if curl -fsS http://localhost:8080/health >/dev/null; then
    echo "$(date) - Application is healthy"
else
    echo "$(date) - Application is DOWN"
fi
EOF

chmod +x /home/devops/health-check.sh

/home/devops/health-check.sh
```

```bash
crontab -e
```

```text
*/5 * * * * /home/devops/health-check.sh >> /home/devops/health-check.log 2>&1
```

## Example Output

```text
Thu Aug 27 12:00:01 IST 2026 - Application is healthy
```

---

# 🧪 Practical Disk Monitoring Cron Lab

## Command

```bash
cat > /home/devops/disk-check.sh <<'EOF'
#!/bin/bash

USAGE=$(df -P / | awk 'NR==2 {gsub("%","",$5); print $5}')

if [ "$USAGE" -ge 80 ]; then
    echo "$(date) - WARNING: Disk usage is ${USAGE}%"
else
    echo "$(date) - Disk usage is ${USAGE}%"
fi
EOF

chmod +x /home/devops/disk-check.sh

/home/devops/disk-check.sh
```

```bash
crontab -e
```

```text
*/10 * * * * /home/devops/disk-check.sh >> /home/devops/disk-check.log 2>&1
```

## Example Output

```text
Thu Aug 27 12:00:01 IST 2026 - Disk usage is 48%
```

---

# 🎯 DevOps Cron Use Cases

## Command

```bash
# Backup
0 2 * * * /usr/local/bin/backup.sh

# Log cleanup
0 3 * * * /usr/local/bin/cleanup.sh

# Health check
*/5 * * * * /usr/local/bin/health-check.sh

# Disk monitoring
*/10 * * * * /usr/local/bin/disk-check.sh

# Certificate monitoring
0 9 * * * /usr/local/bin/cert-check.sh

# Docker maintenance
0 2 * * 0 /usr/local/bin/docker-cleanup.sh

# Database backup
0 1 * * * /usr/local/bin/db-backup.sh

# Git repository backup
0 1 * * * /usr/local/bin/git-backup.sh

# Application restart check
*/5 * * * * /usr/local/bin/service-check.sh

# Server health report
0 8 * * * /usr/local/bin/server-health.sh
```

## Example Output

```text
Automated Backups
Log Rotation
Health Monitoring
Disk Monitoring
SSL Certificate Monitoring
Docker Maintenance
Database Backups
Git Backups
Service Monitoring
Server Health Reporting
```

---

# 🏆 Production Cron Troubleshooting Cheat Sheet

## Command

```bash
# Check Cron service
systemctl status cron

# Check whether Cron is running
systemctl is-active cron

# Check current user's Cron
crontab -l

# Check root Cron
sudo crontab -l

# Check system Cron
cat /etc/crontab

# Check Cron directories
ls -lah /etc/cron.d
ls -lah /etc/cron.daily
ls -lah /etc/cron.hourly

# Check Cron logs
journalctl -u cron -n 100

# Follow Cron logs
journalctl -u cron -f

# Check traditional logs
sudo grep CRON /var/log/syslog

# Check script permissions
ls -l /path/to/script.sh

# Check directory permissions
namei -l /path/to/script.sh

# Test script manually
/path/to/script.sh

# Check Bash syntax
bash -n /path/to/script.sh

# Debug script
bash -x /path/to/script.sh

# Check required command paths
which bash
which python3
which curl
which docker

# Check environment
env

# Check disk space
df -h

# Check inode usage
df -ih

# Check running script
pgrep -af script.sh

# Prevent duplicate execution
flock -n /tmp/job.lock /path/to/script.sh

# Check current timezone
timedatectl

# Check current time
date
```

## Example Output

```text
Cron Service       → Active
Crontab            → Configured
System Cron        → Configured
Cron Logs          → Job Executed
Permissions        → Correct
Script             → Executable
Dependencies       → Available
Environment        → Correct
Disk Space         → Available
Inodes             → Available
Process            → Running
Locking            → No Duplicate Job
Timezone           → Correct
System Time        → Correct
```

---

# 🎯 Important Cron Best Practices

## Command

```bash
# Use absolute paths
0 2 * * * /usr/bin/python3 /home/devops/script.py

# Redirect output
0 2 * * * /home/devops/script.sh >> /var/log/script.log 2>&1

# Use locking
0 2 * * * /usr/bin/flock -n /tmp/script.lock /home/devops/script.sh

# Use timeout
0 2 * * * /usr/bin/timeout 300 /home/devops/script.sh

# Test scripts manually
/home/devops/script.sh

# Check script syntax
bash -n /home/devops/script.sh

# Check Cron logs
journalctl -u cron

# Backup crontab
crontab -l > ~/crontab-backup.txt
```

## Example Output

```text
Absolute Paths       → Reliable command execution
Logging              → Easier troubleshooting
flock                → Prevents duplicate jobs
timeout              → Prevents jobs running indefinitely
Manual Testing       → Detects script problems
Syntax Checking      → Detects Bash errors
Cron Logs            → Shows job execution
Crontab Backup       → Easy recovery
```

---

# 📌 Important Difference: Cron vs Anacron vs At

## Command

```text
Cron
Anacron
At
```

## Example Output

```text
Cron
→ Recurring jobs
→ Exact scheduled times
→ Suitable for servers

Anacron
→ Periodic jobs
→ Useful when systems are not always running
→ Commonly used for daily/weekly/monthly maintenance

At
→ One-time jobs
→ Executes a command once at a specified time
```
---


# 📚 Complete Crontab Command Summary

## Command

```bash
crontab -l
crontab -e
crontab -r
crontab -i -r
crontab --help

sudo crontab -l
sudo crontab -e
sudo crontab -u devops -l
sudo crontab -u devops -e

systemctl status cron
systemctl is-active cron
systemctl is-enabled cron
sudo systemctl start cron
sudo systemctl stop cron
sudo systemctl restart cron
sudo systemctl reload cron
sudo systemctl enable cron
sudo systemctl enable --now cron

journalctl -u cron
journalctl -u cron -f
journalctl -u cron -n 50
journalctl -u cron -b
journalctl -u cron --since today
journalctl -u cron --since "1 hour ago"
journalctl -u cron -p err

sudo grep CRON /var/log/syslog
sudo tail -f /var/log/syslog | grep CRON

cat /etc/crontab
ls -lah /etc/cron.d
ls -lah /etc/cron.hourly
ls -lah /etc/cron.daily
ls -lah /etc/cron.weekly
ls -lah /etc/cron.monthly

cat /etc/cron.allow
cat /etc/cron.deny

sudo ls -lah /var/spool/cron/crontabs/

ps aux | grep '[c]ron'
pgrep -x cron
ps -C cron -o pid,ppid,%cpu,%mem,etime,cmd

at
atq
at -c
atrm

systemctl status atd
systemctl enable --now atd

cat /etc/anacrontab
anacron -n
anacron -f

date
timedatectl
env
whoami
echo "$PATH"
echo "$SHELL"

chmod +x /path/to/script.sh
bash -n /path/to/script.sh
bash -x /path/to/script.sh
namei -l /path/to/script.sh

flock
timeout
```

## Example Output

```text
Crontab Management
Cron Scheduling
Cron Service Management
Cron Monitoring
Cron Logging
System-Wide Scheduling
User Scheduling
One-Time Scheduling
Anacron Scheduling
Environment Troubleshooting
Script Troubleshooting
Production Automation
DevOps Job Scheduling
```

---

# ✅ Learning Outcome

## Command

```bash
crontab -l
crontab -e
systemctl status cron
journalctl -u cron
cat /etc/crontab
ls -lah /etc/cron.d
at
atq
anacron
flock
```

## Example Output

```text
By completing this topic, you should be able to:

- Understand Cron and Crontab
- Understand Cron syntax
- Create scheduled jobs
- Edit user Crontab
- Manage root Crontab
- Schedule jobs every minute
- Schedule jobs every hour
- Schedule daily jobs
- Schedule weekly jobs
- Schedule monthly jobs
- Schedule yearly jobs
- Schedule jobs after reboot
- Use Cron special keywords
- Use Cron ranges
- Use Cron lists
- Use Cron step values
- Redirect Cron output
- Configure Cron logging
- Troubleshoot failed Cron jobs
- Check Cron service status
- Analyze Cron logs
- Understand system-wide Cron jobs
- Understand /etc/crontab
- Understand /etc/cron.d
- Use at for one-time jobs
- Understand Anacron
- Prevent duplicate jobs with flock
- Use timeout for long-running jobs
- Automate backups
- Automate database backups
- Automate Docker maintenance
- Automate health checks
- Automate disk monitoring
- Automate log cleanup
- Automate certificate checks
- Automate service monitoring
- Build production-ready Cron jobs
- Troubleshoot Cron issues in DevOps environments
```

---

# 🎯 Final DevOps Crontab Cheat Sheet

## Command

```bash
# Service
systemctl status cron
systemctl is-active cron
systemctl is-enabled cron

# Crontab
crontab -l
crontab -e
sudo crontab -l
sudo crontab -e

# Logs
journalctl -u cron
journalctl -u cron -f
sudo grep CRON /var/log/syslog

# System Cron
cat /etc/crontab
ls -lah /etc/cron.d
ls -lah /etc/cron.daily
ls -lah /etc/cron.hourly

# Test
* * * * * date >> /tmp/cron-test.log 2>&1

# Every 5 minutes
*/5 * * * * /home/devops/script.sh

# Every hour
0 * * * * /home/devops/script.sh

# Daily at 2 AM
0 2 * * * /home/devops/script.sh

# Monday-Friday
0 9 * * 1-5 /home/devops/script.sh

# Monthly
0 0 1 * * /home/devops/script.sh

# Reboot
@reboot /home/devops/startup.sh

# Logging
*/5 * * * * /home/devops/script.sh >> /var/log/script.log 2>&1

# Locking
*/5 * * * * flock -n /tmp/job.lock /home/devops/script.sh

# Timeout
*/5 * * * * timeout 300 /home/devops/script.sh

# One-time job
echo "/home/devops/script.sh" | at 23:00

# Pending at jobs
atq

# Delete at job
atrm JOB_ID

# Backup crontab
crontab -l > ~/crontab-backup.txt
```

## Example Output

```text
Cron Service       → systemctl
Crontab            → crontab
Scheduling         → */5, 0 2 * * *
Logging            → journalctl
System Cron        → /etc/crontab
Testing            → /tmp/cron-test.log
Locking            → flock
Timeout            → timeout
One-Time Jobs      → at
Job Queue          → atq
Job Removal        → atrm
Backup             → crontab -l
```

---

# 🏆 Topic 11 Complete

## Command

```bash
crontab
cron
systemctl
journalctl
at
atq
atrm
anacron
flock
timeout
date
timedatectl
bash
chmod
find
grep
tail
ps
pgrep
```

## Example Output

```text
Linux Cron & Crontab
        ↓
Job Scheduling
        ↓
Automation
        ↓
Logging
        ↓
Monitoring
        ↓
Troubleshooting
        ↓
Backup Automation
        ↓
DevOps Production Automation
```
