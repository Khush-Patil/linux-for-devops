# 🐧 Linux Fundamentals

# 1. Check Current User

## Command

```bash
whoami
```

## Example Output

```text
khushboo
```

---

# 2. Check User ID and Groups

## Command

```bash
id
```

## Example Output

```text
uid=1000(khushboo) gid=1000(khushboo) groups=1000(khushboo),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users),1001(docker)
```

---

# 3. Check Hostname

## Command

```bash
hostname
```

## Example Output

```text
KhushbooC-L
```

---

# 4. Check Operating System

## Command

```bash
cat /etc/os-release
```

## Example Output

```text
PRETTY_NAME="Ubuntu 24.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.3 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
```

---

# 5. Check Kernel Information

## Command

```bash
uname -a
```

## Example Output

```text
Linux KhushbooC-L 6.6.87.2-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC Thu Jun 5 18:30:46 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
```

---

# 6. Check Kernel Version

## Command

```bash
uname -r
```

## Example Output

```text
6.6.87.2-microsoft-standard-WSL2
```

---

# 7. Check System Architecture

## Command

```bash
uname -m
```

## Example Output

```text
x86_64
```

---

# 8. Check Current Date and Time

## Command

```bash
date
```

## Example Output

```text
Wed Aug 26 07:52:56 UTC 2026
```

---

# 9. Check System Uptime

## Command

```bash
uptime
```

## Example Output

```text
07:52:58 up 10:23, 1 user, load average: 0.00, 0.00, 0.00
```

---

# 10. Check Number of CPUs

## Command

```bash
nproc
```

## Example Output

```text
8
```

> Note: Your output may be different depending on your machine.

---

# 11. Check CPU Information

## Command

```bash
lscpu
```

## Example Output

```text
Architecture:                         x86_64
CPU op-mode(s):                       32-bit, 64-bit
Address sizes:                        39 bits physical, 48 bits virtual
Byte Order:                           Little Endian
CPU(s):                               8
On-line CPU(s) list:                  0-7
Vendor ID:                            GenuineIntel
Model name:                           11th Gen Intel(R) Core(TM) i5
CPU family:                           6
Model:                                140
Thread(s) per core:                   2
Core(s) per socket:                   4
Socket(s):                            1
```

> Note: CPU information will be different on different machines.

---

# 12. Check Memory Usage

## Command

```bash
free -h
```

## Example Output

```text
               total        used        free      shared  buff/cache   available
Mem:            7.7Gi       2.1Gi       1.2Gi       120Mi       4.4Gi       5.1Gi
Swap:           2.0Gi          0B       2.0Gi
```

> Note: Memory values will be different on different machines.

---

# 13. Check Disk Usage

## Command

```bash
df -h
```

## Example Output

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        50G   32G   16G  67% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
```

> Note: Disk information will be different on different machines.

---

# 14. Check Current Directory

## Command

```bash
pwd
```

## Example Output

```text
/home/khushboo/linux-for-devops
```

---

# 15. List Files and Directories

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

# 16. List Files in Detailed Format

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

# 17. List All Files Including Hidden Files

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

# 18. Show Command History

## Command

```bash
history
```

## Example Output

```text
  101  pwd
  102  ls
  103  whoami
  104  hostname
  105  uname -a
  106  df -h
  107  free -h
```

> Note: Your history will be different.

---

# 19. Search Command History

## Command

```bash
history | grep docker
```

## Example Output

```text
  120  docker ps
  125  docker images
  130  docker compose up -d
```

> Note: If you have never run a Docker command, you may get no output.

---

# 20. Find Command Location

## Command

```bash
which python3
```

## Example Output

```text
/usr/bin/python3
```

---

# 21. Find Command Location Using command -v

## Command

```bash
command -v python3
```

## Example Output

```text
/usr/bin/python3
```

---

# 22. Check Current User Environment Variable

## Command

```bash
echo $USER
```

## Example Output

```text
khushboo
```

---

# 23. Check Home Directory

## Command

```bash
echo $HOME
```

## Example Output

```text
/home/khushboo
```

---

# 24. Check Current Shell

## Command

```bash
echo $SHELL
```

## Example Output

```text
/bin/bash
```

---

# 25. Check PATH

## Command

```bash
echo $PATH
```

## Example Output

```text
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

> Note: Your PATH may contain additional directories.

---

# 26. Create a Directory

## Command

```bash
mkdir linux-lab
```

## Example Output

```text
```

> `mkdir` normally produces no output when the directory is created successfully.

---

# 27. Check Created Directory

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
linux-lab
scripts
```

---

# 28. Enter a Directory

## Command

```bash
cd linux-lab
```

## Example Output

```text
```

> `cd` normally produces no output when successful.

---

# 29. Check Current Directory

## Command

```bash
pwd
```

## Example Output

```text
/home/khushboo/linux-for-devops/linux-lab
```

---

# 30. Create an Empty File

## Command

```bash
touch hello.txt
```

## Example Output

```text
```

> `touch` normally produces no output when successful.

---

# 31. List the Created File

## Command

```bash
ls -l
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 0 Aug 26 08:30 hello.txt
```

---

# 32. Write Text to a File

## Command

```bash
echo "Hello Linux" > hello.txt
```

## Example Output

```text
```

> `echo` with `>` writes the text into the file and normally produces no terminal output.

---

# 33. Read File Contents

## Command

```bash
cat hello.txt
```

## Example Output

```text
Hello Linux
```

---

# 34. Append Text to a File

## Command

```bash
echo "I am learning DevOps" >> hello.txt
```

## Example Output

```text
```

---

# 35. Read Updated File

## Command

```bash
cat hello.txt
```

## Example Output

```text
Hello Linux
I am learning DevOps
```

---

# 36. Count Lines in a File

## Command

```bash
wc -l hello.txt
```

## Example Output

```text
2 hello.txt
```

---

# 37. Search Text in a File

## Command

```bash
grep "Linux" hello.txt
```

## Example Output

```text
Hello Linux
```

---

# 38. Copy a File

## Command

```bash
cp hello.txt hello-copy.txt
```

## Example Output

```text
```

> `cp` normally produces no output when successful.

---

# 39. Check Copied File

## Command

```bash
ls -l
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 29 Aug 26 08:35 hello-copy.txt
-rw-r--r-- 1 khushboo khushboo 29 Aug 26 08:30 hello.txt
```

---

# 40. Rename a File

## Command

```bash
mv hello-copy.txt devops.txt
```

## Example Output

```text
```

> `mv` normally produces no output when successful.

---

# 41. Check Renamed File

## Command

```bash
ls
```

## Example Output

```text
devops.txt
hello.txt
```

---

# 42. Remove a File

## Command

```bash
rm devops.txt
```

## Example Output

```text
```

> `rm` normally produces no output when successful.

---

# 43. Verify File Was Removed

## Command

```bash
ls
```

## Example Output

```text
hello.txt
```

---

# 44. Go to Parent Directory

## Command

```bash
cd ..
```

## Example Output

```text
```

> `cd ..` normally produces no output.

---

# 45. Remove an Empty Directory

## Command

```bash
rmdir linux-lab
```

## Example Output

```text
```

> `rmdir` normally produces no output when successful.

---

# 46. Check Git Version

## Command

```bash
git --version
```

## Example Output

```text
git version 2.43.0
```

> Note: Your Git version may be different.

---

# 47. Check Python Version

## Command

```bash
python3 --version
```

## Example Output

```text
Python 3.12.3
```

> Note: Your Python version may be different.

---

# 48. Check Docker Version

## Command

```bash
docker --version
```

## Example Output

```text
Docker version 29.1.3, build abcdef1
```

> Note: Your Docker version may be different.

---

# 49. Check Bash Version

## Command

```bash
bash --version
```

## Example Output

```text
GNU bash, version 5.2.21(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2022 Free Software Foundation, Inc.
```

---

# 50. Get Help for a Command

## Command

```bash
ls --help
```

## Example Output

```text
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).

-a, --all
    do not ignore entries starting with .

-l
    use a long listing format

-h, --human-readable
    with -l, print sizes like 1K 234M 2G etc.
```

> The complete output is much longer. Use `ls --help` to see all available options.

---

# 🧪 Practical Challenge

Run the following commands yourself:

```bash
whoami
id
hostname
cat /etc/os-release
uname -a
uname -r
uname -m
date
uptime
nproc
free -h
df -h
pwd
ls
ls -la
```

Then try:

```bash
mkdir test-lab
cd test-lab
touch test.txt
echo "Linux is powerful" > test.txt
cat test.txt
cp test.txt backup.txt
ls -l
mv backup.txt backup-copy.txt
ls -l
rm backup-copy.txt
ls -l
cd ..
rmdir test-lab
```

---

# ✅ Commands Learned

| Command | Purpose |
|---|---|
| `whoami` | Show current user |
| `id` | Show UID, GID and groups |
| `hostname` | Show hostname |
| `cat /etc/os-release` | Show OS information |
| `uname -a` | Show kernel information |
| `uname -r` | Show kernel version |
| `uname -m` | Show architecture |
| `date` | Show date and time |
| `uptime` | Show system uptime |
| `nproc` | Show CPU count |
| `lscpu` | Show CPU information |
| `free -h` | Show memory |
| `df -h` | Show disk usage |
| `pwd` | Show current directory |
| `ls` | List files |
| `ls -l` | Detailed listing |
| `ls -la` | List hidden files |
| `history` | Show command history |
| `grep` | Search text |
| `which` | Find command location |
| `echo` | Print/write text |
| `mkdir` | Create directory |
| `cd` | Change directory |
| `touch` | Create file |
| `cat` | Read file |
| `cp` | Copy file |
| `mv` | Move/rename file |
| `rm` | Remove file |
| `rmdir` | Remove empty directory |
