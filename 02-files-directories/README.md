> ⚠️ Your output may be different from the examples depending on your Linux system.

---

# 1. Check Current Directory

## Command

```bash
pwd
```

## Example Output

```text
/home/khushboo/linux-for-devops
```

---

# 2. List Files and Directories

## Command

```bash
ls
```

## Example Output

```text
01-linux-fundamentals
02-files-directories
03-users-permissions
04-process-management
05-systemd-services
06-networking
07-storage
08-logs-troubleshooting
09-ssh
10-shell-scripting
11-cron-automation
12-linux-security
13-practical-labs
LICENSE
README.md
scripts
```

---

# 3. List Files in Long Format

## Command

```bash
ls -l
```

## Example Output

```text
total 20
drwxr-xr-x 2 khushboo khushboo 4096 Aug 25 07:48 01-linux-fundamentals
drwxr-xr-x 2 khushboo khushboo 4096 Aug 25 07:48 02-files-directories
drwxr-xr-x 2 khushboo khushboo 4096 Aug 25 07:48 03-users-permissions
-rw-r--r-- 1 khushboo khushboo 1071 Aug 25 07:46 LICENSE
-rw-r--r-- 1 khushboo khushboo  183 Aug 25 07:52 README.md
drwxr-xr-x 2 khushboo khushboo 4096 Aug 25 07:48 scripts
```

---

# 4. List Hidden Files

## Command

```bash
ls -la
```

## Example Output

```text
total 40
drwxr-xr-x 15 khushboo khushboo 4096 Aug 26 07:52 .
drwxr-x--- 25 khushboo khushboo 4096 Aug 26 07:30 ..
drwxr-xr-x  8 khushboo khushboo 4096 Aug 26 07:40 .git
-rw-r--r--  1 khushboo khushboo  183 Aug 25 07:52 README.md
-rw-r--r--  1 khushboo khushboo 1071 Aug 25 07:46 LICENSE
```

---

# 5. Create a Directory

## Command

```bash
mkdir lab
```

## Example Output

```text
```

> `mkdir` normally produces no output when successful.

---

# 6. Check the Directory

## Command

```bash
ls
```

## Example Output

```text
lab
```

---

# 7. Create Multiple Directories

## Command

```bash
mkdir dev test backup
```

## Example Output

```text
```

---

# 8. Create Nested Directories

## Command

```bash
mkdir -p project/config/app
```

## Example Output

```text
```

> `-p` creates parent directories automatically.

---

# 9. Check Nested Directory Structure

## Command

```bash
find project -type d
```

## Example Output

```text
project
project/config
project/config/app
```

---

# 10. Enter a Directory

## Command

```bash
cd project
```

## Example Output

```text
```

---

# 11. Go Back to Parent Directory

## Command

```bash
cd ..
```

## Example Output

```text
```

---

# 12. Go to Home Directory

## Command

```bash
cd ~
```

## Example Output

```text
```

---

# 13. Go to Previous Directory

## Command

```bash
cd -
```

## Example Output

```text
/home/khushboo/linux-for-devops
```

> `cd -` switches to the previous working directory.

---

# 14. Create an Empty File

## Command

```bash
touch app.txt
```

## Example Output

```text
```

---

# 15. Create Multiple Files

## Command

```bash
touch file1.txt file2.txt file3.txt
```

## Example Output

```text
```

---

# 16. Check Created Files

## Command

```bash
ls
```

## Example Output

```text
app.txt
file1.txt
file2.txt
file3.txt
```

---

# 17. Write Content to a File

## Command

```bash
echo "Hello Linux" > app.txt
```

## Example Output

```text
```

---

# 18. Read File Contents

## Command

```bash
cat app.txt
```

## Example Output

```text
Hello Linux
```

---

# 19. Add More Content to a File

## Command

```bash
echo "Linux is used in DevOps" >> app.txt
```

## Example Output

```text
```

---

# 20. Read the File Again

## Command

```bash
cat app.txt
```

## Example Output

```text
Hello Linux
Linux is used in DevOps
```

---

# 21. Display File with Line Numbers

## Command

```bash
cat -n app.txt
```

## Example Output

```text
     1  Hello Linux
     2  Linux is used in DevOps
```

---

# 22. View the Beginning of a File

## Command

```bash
head app.txt
```

## Example Output

```text
Hello Linux
Linux is used in DevOps
```

---

# 23. View First 1 Line

## Command

```bash
head -n 1 app.txt
```

## Example Output

```text
Hello Linux
```

---

# 24. View the End of a File

## Command

```bash
tail app.txt
```

## Example Output

```text
Hello Linux
Linux is used in DevOps
```

---

# 25. View Last 1 Line

## Command

```bash
tail -n 1 app.txt
```

## Example Output

```text
Linux is used in DevOps
```

---

# 26. Create a File with Multiple Lines

## Command

```bash
printf "Line 1\nLine 2\nLine 3\nLine 4\nLine 5\n" > numbers.txt
```

## Example Output

```text
```

---

# 27. Read the File

## Command

```bash
cat numbers.txt
```

## Example Output

```text
Line 1
Line 2
Line 3
Line 4
Line 5
```

---

# 28. Count Lines in a File

## Command

```bash
wc -l numbers.txt
```

## Example Output

```text
5 numbers.txt
```

---

# 29. Count Words in a File

## Command

```bash
wc -w numbers.txt
```

## Example Output

```text
10 numbers.txt
```

---

# 30. Count Characters in a File

## Command

```bash
wc -m numbers.txt
```

## Example Output

```text
35 numbers.txt
```

---

# 31. Copy a File

## Command

```bash
cp app.txt app-backup.txt
```

## Example Output

```text
```

---

# 32. Check Copied File

## Command

```bash
ls -l
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 36 Aug 26 14:00 app-backup.txt
-rw-r--r-- 1 khushboo khushboo 36 Aug 26 13:59 app.txt
```

---

# 33. Copy a File to a Directory

## Command

```bash
mkdir backup
cp app.txt backup/
```

## Example Output

```text
```

---

# 34. Check Backup Directory

## Command

```bash
ls backup/
```

## Example Output

```text
app.txt
```

---

# 35. Copy an Entire Directory

## Command

```bash
cp -r backup backup-copy
```

## Example Output

```text
```

> `-r` means recursive and is required for copying directories.

---

# 36. Move a File

## Command

```bash
mv app.txt backup/
```

## Example Output

```text
```

---

# 37. Check the Backup Directory

## Command

```bash
ls backup/
```

## Example Output

```text
app.txt
```

---

# 38. Rename a File

## Command

```bash
mv backup/app.txt backup/application.txt
```

## Example Output

```text
```

---

# 39. Check Renamed File

## Command

```bash
ls backup/
```

## Example Output

```text
application.txt
```

---

# 40. Rename a Directory

## Command

```bash
mv backup backup-files
```

## Example Output

```text
```

---

# 41. Check Directory

## Command

```bash
ls
```

## Example Output

```text
backup-copy
backup-files
dev
file1.txt
file2.txt
file3.txt
numbers.txt
project
test
```

---

# 42. Remove a File

## Command

```bash
rm file1.txt
```

## Example Output

```text
```

---

# 43. Remove Multiple Files

## Command

```bash
rm file2.txt file3.txt
```

## Example Output

```text
```

---

# 44. Remove an Empty Directory

## Command

```bash
rmdir dev
```

## Example Output

```text
```

---

# 45. Remove a Directory and Its Contents

## Command

```bash
rm -r backup-copy
```

## Example Output

```text
```

> `-r` means recursive.

---

# 46. Force Remove a File

## Command

```bash
rm -f numbers.txt
```

## Example Output

```text
```

> `-f` means force.

---

# 47. Check File Type

## Command

```bash
file app-backup.txt
```

## Example Output

```text
app-backup.txt: ASCII text
```

---

# 48. Check File Type of a Directory

## Command

```bash
file project
```

## Example Output

```text
project: directory
```

---

# 49. Check File Metadata

## Command

```bash
stat app-backup.txt
```

## Example Output

```text
  File: app-backup.txt
  Size: 36        Blocks: 8          IO Block: 4096   regular file
Device: 8,2       Inode: 123456      Links: 1
Access: (0644/-rw-r--r--)  Uid: (1000/khushboo)   Gid: (1000/khushboo)
Access: 2026-08-26 14:00:00.000000000 +0530
Modify: 2026-08-26 14:00:00.000000000 +0530
Change: 2026-08-26 14:00:00.000000000 +0530
 Birth: 2026-08-26 14:00:00.000000000 +0530
```

> Some fields and values vary by filesystem and Linux environment.

---

# 50. Check File Size

## Command

```bash
du -h app-backup.txt
```

## Example Output

```text
4.0K    app-backup.txt
```

---

# 51. Check Directory Size

## Command

```bash
du -sh project
```

## Example Output

```text
4.0K    project
```

---

# 52. Check Sizes of Files and Directories

## Command

```bash
du -sh *
```

## Example Output

```text
4.0K    01-linux-fundamentals
4.0K    02-files-directories
4.0K    backup-files
4.0K    project
4.0K    scripts
```

> Your output will be different.

---

# 53. Find Files by Name

## Command

```bash
find . -name "*.txt"
```

## Example Output

```text
./app-backup.txt
./hello.txt
./backup-files/application.txt
```

---

# 54. Find a Specific File

## Command

```bash
find . -name "app-backup.txt"
```

## Example Output

```text
./app-backup.txt
```

---

# 55. Find Directories

## Command

```bash
find . -type d
```

## Example Output

```text
.
./01-linux-fundamentals
./02-files-directories
./project
./project/config
./project/config/app
```

---

# 56. Find Files Only

## Command

```bash
find . -type f
```

## Example Output

```text
./README.md
./LICENSE
./app-backup.txt
./hello.txt
```

---

# 57. Find Files Modified Recently

## Command

```bash
find . -type f -mtime -1
```

## Example Output

```text
./README.md
./app-backup.txt
```

> `-mtime -1` means modified within approximately the last 24 hours.

---

# 58. Find Files Larger Than 1 MB

## Command

```bash
find . -type f -size +1M
```

## Example Output

```text
./logs/application.log
./backup/database.sql
```

> If no file matches, there will be no output.

---

# 59. Find Empty Files

## Command

```bash
find . -type f -empty
```

## Example Output

```text
./empty.txt
./test.txt
```

---

# 60. Find Empty Directories

## Command

```bash
find . -type d -empty
```

## Example Output

```text
./empty-directory
```

---

# 61. Find Files by Extension

## Command

```bash
find . -type f -name "*.log"
```

## Example Output

```text
./logs/app.log
./logs/error.log
```

---

# 62. Find Files and Execute a Command

## Command

```bash
find . -type f -name "*.log" -exec ls -lh {} \;
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 12K Aug 26 13:00 ./logs/app.log
-rw-r--r-- 1 khushboo khushboo 8K Aug 26 13:10 ./logs/error.log
```

---

# 63. Search for Text in Multiple Files

## Command

```bash
grep -R "ERROR" .
```

## Example Output

```text
./logs/app.log:ERROR Database connection failed
./logs/error.log:ERROR Connection timeout
```

> `-R` searches recursively inside directories.

---

# 64. Copy Using Wildcards

## Command

```bash
mkdir text-backup
cp *.txt text-backup/
```

## Example Output

```text
```

---

# 65. Check Copied Files

## Command

```bash
ls text-backup/
```

## Example Output

```text
app-backup.txt
hello.txt
```

---

# 66. Wildcard — Match Any Characters

## Command

```bash
ls *.txt
```

## Example Output

```text
app-backup.txt
hello.txt
```

> `*.txt` means any filename ending with `.txt`.

---

# 67. Wildcard — Match One Character

## Command

```bash
ls file?.txt
```

## Example Output

```text
file1.txt
file2.txt
```

> `?` matches exactly one character.

---

# 68. Wildcard — Character Range

## Command

```bash
ls file[1-3].txt
```

## Example Output

```text
file1.txt
file2.txt
file3.txt
```

---

# 69. Create a Symbolic Link

## Command

```bash
ln -s app-backup.txt app-link.txt
```

## Example Output

```text
```

---

# 70. Check Symbolic Link

## Command

```bash
ls -l app-link.txt
```

## Example Output

```text
lrwxrwxrwx 1 khushboo khushboo 14 Aug 26 14:20 app-link.txt -> app-backup.txt
```

> `l` at the beginning means symbolic link.

---

# 71. Read Through a Symbolic Link

## Command

```bash
cat app-link.txt
```

## Example Output

```text
Hello Linux
Linux is used in DevOps
```

---

# 72. Create a Hard Link

## Command

```bash
ln app-backup.txt app-hardlink.txt
```

## Example Output

```text
```

---

# 73. Check Hard Link

## Command

```bash
ls -li app-backup.txt app-hardlink.txt
```

## Example Output

```text
123456 -rw-r--r-- 2 khushboo khushboo 36 Aug 26 14:00 app-backup.txt
123456 -rw-r--r-- 2 khushboo khushboo 36 Aug 26 14:00 app-hardlink.txt
```

> Notice that both files have the same inode number.

---

# 74. Check Inode Number

## Command

```bash
ls -i app-backup.txt
```

## Example Output

```text
123456 app-backup.txt
```

---

# 75. Check Directory Tree

## Command

```bash
tree
```

## Example Output

```text
.
├── app-backup.txt
├── app-hardlink.txt
├── app-link.txt -> app-backup.txt
├── project
│   └── config
│       └── app
└── text-backup
    └── app-backup.txt

4 directories, 5 files
```

> If `tree` is not installed, install it using your package manager.

Ubuntu:

```bash
sudo apt install tree
```

---

# 76. Display Directory Tree with Directories Only

## Command

```bash
tree -d
```

## Example Output

```text
.
├── project
│   └── config
│       └── app
└── text-backup

4 directories
```

---

# 77. Create a DevOps Directory Structure

## Command

```bash
mkdir -p devops-project/{config,logs,scripts,backup}
```

## Example Output

```text
```

---

# 78. Check DevOps Directory Structure

## Command

```bash
tree devops-project
```

## Example Output

```text
devops-project
├── backup
├── config
├── logs
└── scripts

4 directories, 0 files
```

---

# 79. Create Application Configuration

## Command

```bash
echo "APP_ENV=development" > devops-project/config/app.conf
```

## Example Output

```text
```

---

# 80. Create Application Log

## Command

```bash
echo "Application started successfully" > devops-project/logs/app.log
```

## Example Output

```text
```

---

# 81. Create Deployment Script

## Command

```bash
echo '#!/bin/bash' > devops-project/scripts/deploy.sh
```

## Example Output

```text
```

---

# 82. View DevOps Project

## Command

```bash
tree devops-project
```

## Example Output

```text
devops-project
├── backup
├── config
│   └── app.conf
├── logs
│   └── app.log
└── scripts
    └── deploy.sh

4 directories, 3 files
```

---

# 83. Find Configuration Files

## Command

```bash
find devops-project -type f -name "*.conf"
```

## Example Output

```text
devops-project/config/app.conf
```

---

# 84. Find Log Files

## Command

```bash
find devops-project -type f -name "*.log"
```

## Example Output

```text
devops-project/logs/app.log
```

---

# 85. Find Shell Scripts

## Command

```bash
find devops-project -type f -name "*.sh"
```

## Example Output

```text
devops-project/scripts/deploy.sh
```

---

# 86. Search Configuration Content

## Command

```bash
grep -R "APP_ENV" devops-project/config
```

## Example Output

```text
devops-project/config/app.conf:APP_ENV=development
```

---

# 87. Compare Two Files

## Command

```bash
cp devops-project/config/app.conf devops-project/config/app-backup.conf
diff devops-project/config/app.conf devops-project/config/app-backup.conf
```

## Example Output

```text
```

> No output means the files are identical.

---

# 88. Modify the Backup Configuration

## Command

```bash
echo "APP_ENV=production" > devops-project/config/app-backup.conf
```

## Example Output

```text
```

---

# 89. Compare Files Again

## Command

```bash
diff devops-project/config/app.conf devops-project/config/app-backup.conf
```

## Example Output

```text
1c1
< APP_ENV=development
---
> APP_ENV=production
```

---

# 90. Find Files Modified in the Last Hour

## Command

```bash
find devops-project -type f -mmin -60
```

## Example Output

```text
devops-project/config/app.conf
devops-project/config/app-backup.conf
devops-project/logs/app.log
devops-project/scripts/deploy.sh
```

---

# 91. Find Files Larger Than 100 KB

## Command

```bash
find devops-project -type f -size +100k
```

## Example Output

```text
devops-project/logs/application.log
```

> No output means no matching file was found.

---

# 92. Find Files Smaller Than 1 KB

## Command

```bash
find devops-project -type f -size -1k
```

## Example Output

```text
devops-project/config/app.conf
devops-project/config/app-backup.conf
devops-project/logs/app.log
devops-project/scripts/deploy.sh
```

---

# 93. List Files Sorted by Modification Time

## Command

```bash
ls -lt
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 36 Aug 26 14:20 app-backup.txt
-rw-r--r-- 1 khushboo khushboo 29 Aug 26 14:10 hello.txt
drwxr-xr-x 2 khushboo khushboo 4096 Aug 26 14:00 project
```

---

# 94. List Files Sorted by Size

## Command

```bash
ls -lhS
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 2.5M Aug 26 14:00 application.log
-rw-r--r-- 1 khushboo khushboo 500K Aug 26 13:00 backup.sql
-rw-r--r-- 1 khushboo khushboo 36B Aug 26 14:20 app.txt
```

---

# 95. Find Largest Files

## Command

```bash
find . -type f -printf '%s %p\n' | sort -nr | head
```

## Example Output

```text
2500000 ./logs/application.log
500000 ./backup/database.sql
120000 ./data/report.csv
360 ./app.txt
```

> The first column is the file size in bytes.

---

# 96. Find Recently Modified Files

## Command

```bash
find . -type f -printf '%TY-%Tm-%Td %TH:%TM %p\n' | sort -r | head
```

## Example Output

```text
2026-08-26 14:20 ./app.txt
2026-08-26 14:15 ./logs/app.log
2026-08-26 14:10 ./config/app.conf
```

---

# 97. Find Files Owned by Current User

## Command

```bash
find . -type f -user "$(whoami)"
```

## Example Output

```text
./README.md
./LICENSE
./app.txt
./project/config/app.conf
```

---

# 98. Find Files with Specific Permissions

## Command

```bash
find . -type f -perm 644
```

## Example Output

```text
./README.md
./LICENSE
./app.txt
```

> File permissions will be covered in detail in **03-users-permissions**.

---

# 99. Count Files in a Directory

## Command

```bash
find devops-project -type f | wc -l
```

## Example Output

```text
4
```

---

# 100. Count Directories

## Command

```bash
find devops-project -type d | wc -l
```

## Example Output

```text
5
```

---

# 🧪 Practical Lab 1 — Basic File Management

Run these commands one by one:

```bash
mkdir practice
cd practice
touch file1.txt file2.txt file3.txt
echo "Linux DevOps Lab" > file1.txt
cp file1.txt file1-backup.txt
mv file2.txt renamed-file.txt
ls -l
cat file1.txt
rm file3.txt
ls -l
cd ..
```

## Expected Output

```text
total 12
-rw-r--r-- 1 khushboo khushboo 17 Aug 26 14:30 file1-backup.txt
-rw-r--r-- 1 khushboo khushboo 17 Aug 26 14:30 file1.txt
-rw-r--r-- 1 khushboo khushboo  0 Aug 26 14:30 renamed-file.txt

Linux DevOps Lab
```

---

# 🧪 Practical Lab 2 — DevOps Project Structure

Create this structure:

```text
application/
├── backup/
├── config/
│   ├── app.conf
│   └── database.conf
├── logs/
│   ├── app.log
│   └── error.log
└── scripts/
    ├── deploy.sh
    └── backup.sh
```

## Command

```bash
mkdir -p application/{backup,config,logs,scripts}
touch application/config/app.conf
touch application/config/database.conf
touch application/logs/app.log
touch application/logs/error.log
touch application/scripts/deploy.sh
touch application/scripts/backup.sh
```

## Check

```bash
tree application
```

## Example Output

```text
application
├── backup
├── config
│   ├── app.conf
│   └── database.conf
├── logs
│   ├── app.log
│   └── error.log
└── scripts
    ├── backup.sh
    └── deploy.sh

5 directories, 6 files
```

---

# 🧪 Practical Lab 3 — Find Application Files

## Find configuration files

```bash
find application -type f -name "*.conf"
```

## Example Output

```text
application/config/app.conf
application/config/database.conf
```

## Find log files

```bash
find application -type f -name "*.log"
```

## Example Output

```text
application/logs/app.log
application/logs/error.log
```

## Find scripts

```bash
find application -type f -name "*.sh"
```

## Example Output

```text
application/scripts/deploy.sh
application/scripts/backup.sh
```

---

# 🧪 Practical Lab 4 — Search Application Logs

Put sample log data into the log file:

```bash
echo "INFO Application started" > application/logs/app.log
echo "INFO Database connected" >> application/logs/app.log
echo "ERROR Database connection failed" >> application/logs/app.log
echo "INFO Application stopped" >> application/logs/app.log
```

## Read the log

```bash
cat application/logs/app.log
```

## Example Output

```text
INFO Application started
INFO Database connected
ERROR Database connection failed
INFO Application stopped
```

## Find errors

```bash
grep "ERROR" application/logs/app.log
```

## Example Output

```text
ERROR Database connection failed
```

---

# 🧪 Practical Lab 5 — Backup Configuration

Create a backup directory:

```bash
mkdir -p application/backup
```

Copy configuration files:

```bash
cp application/config/*.conf application/backup/
```

Check:

```bash
ls -l application/backup/
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 20 Aug 26 14:40 app.conf
-rw-r--r-- 1 khushboo khushboo 25 Aug 26 14:40 database.conf
```

---

# 🧪 Practical Lab 6 — Find Large Files

## Command

```bash
find . -type f -size +1M
```

## Example Output

```text
./application/logs/application.log
./backup/database.sql
```

If nothing is larger than 1 MB:

```text
```

No output means no matching file was found.

---

# 🧪 Practical Lab 7 — Find Recently Changed Files

## Command

```bash
find application -type f -mmin -60
```

## Example Output

```text
application/config/app.conf
application/config/database.conf
application/logs/app.log
application/logs/error.log
```

---

# 🧪 Practical Lab 8 — Create Symbolic Link

Create a link to the application log:

```bash
ln -s application/logs/app.log current.log
```

Check:

```bash
ls -l current.log
```

## Example Output

```text
lrwxrwxrwx 1 khushboo khushboo 24 Aug 26 14:45 current.log -> application/logs/app.log
```

Read it:

```bash
cat current.log
```

## Example Output

```text
INFO Application started
INFO Database connected
ERROR Database connection failed
INFO Application stopped
```

---

# 🧪 Practical Lab 9 — Disk Usage Investigation

## Check application size

```bash
du -sh application
```

## Example Output

```text
20K    application
```

## Check each directory

```bash
du -sh application/*
```

## Example Output

```text
4.0K    application/backup
8.0K    application/config
8.0K    application/logs
4.0K    application/scripts
```

---

# 🧪 Practical Lab 10 — Real DevOps Troubleshooting

Imagine an application is consuming too much disk space.

## Step 1 — Check disk usage

```bash
df -h
```

## Step 2 — Find large directories

```bash
du -sh /* 2>/dev/null | sort -h
```

## Step 3 — Find large files

```bash
find /var -type f -size +100M 2>/dev/null
```

## Step 4 — Find large log files

```bash
find /var/log -type f -size +100M 2>/dev/null
```

## Step 5 — Check recently modified files

```bash
find /var/log -type f -mtime -1 2>/dev/null
```

> ⚠️ These commands inspect system directories. Do not delete anything unless you understand what the file is and why it can be removed.

---

# 🧪 Practical Lab 11 — Cleanup

After completing the labs, remove the practice files.

## Remove practice directory

```bash
rm -rf practice
```

## Remove DevOps lab

```bash
rm -rf application
```

## Remove test files

```bash
rm -f current.log
rm -f app-backup.txt
rm -f app-hardlink.txt
rm -f app-link.txt
```

> ⚠️ Be very careful with `rm -rf`. Always check your current directory with `pwd` before deleting files or directories.

---


---

# 📚 Commands Learned

| Command | Purpose |
|---|---|
| `pwd` | Show current directory |
| `ls` | List files |
| `ls -l` | Detailed listing |
| `ls -la` | Show hidden files |
| `cd` | Change directory |
| `mkdir` | Create directory |
| `mkdir -p` | Create nested directories |
| `touch` | Create empty file |
| `cat` | Read file |
| `head` | Show beginning of file |
| `tail` | Show end of file |
| `echo` | Write/display text |
| `printf` | Format/write text |
| `wc` | Count lines/words/characters |
| `cp` | Copy files |
| `cp -r` | Copy directories |
| `mv` | Move/rename files |
| `rm` | Remove files |
| `rm -r` | Remove directories recursively |
| `rm -f` | Force remove |
| `rmdir` | Remove empty directory |
| `file` | Identify file type |
| `stat` | Show file metadata |
| `du` | Show file/directory size |
| `find` | Search files/directories |
| `grep` | Search text |
| `diff` | Compare files |
| `ln` | Create hard link |
| `ln -s` | Create symbolic link |
| `tree` | Display directory structure |
| `sort` | Sort output |
| `head` | Show first lines |

---

# 🧠 Important Concepts

## `>` vs `>>`

Overwrite a file:

```bash
echo "Hello" > file.txt
```

Append to a file:

```bash
echo "Hello" >> file.txt
```

---

## `cp` vs `mv`

Copy:

```bash
cp file.txt backup.txt
```

Move/rename:

```bash
mv file.txt backup.txt
```

---

## `rm` vs `rmdir`

Remove file:

```bash
rm file.txt
```

Remove empty directory:

```bash
rmdir directory
```

---

## `rm -r`

Remove directory and its contents:

```bash
rm -r directory
```

---

## `ln` vs `ln -s`

Hard link:

```bash
ln original.txt hardlink.txt
```

Symbolic link:

```bash
ln -s original.txt symlink.txt
```

---

