# 👤 Linux Users & Permissions — Hands-on Lab

This lab teaches Linux users, groups, ownership, permissions, and access control from **beginner to advanced**.

You will learn how to:

- Check current user
- Check user ID and groups
- Understand `/etc/passwd`
- Understand `/etc/group`
- Create users
- Modify users
- Delete users
- Create groups
- Add users to groups
- Remove users from groups
- Switch users
- Use `sudo`
- Understand file ownership
- Understand Linux permissions
- Use `chmod`
- Use `chown`
- Use `chgrp`
- Understand numeric permissions
- Understand symbolic permissions
- Understand `umask`
- Understand SUID
- Understand SGID
- Understand Sticky Bit
- Use ACLs
- Troubleshoot permission denied errors
- Perform practical DevOps permission tasks

> ⚠️ Some commands in this lab require `sudo`.
>
> ⚠️ Commands that create/delete users or groups should be performed on a test machine or lab VM.
>
> ⚠️ Your output may be different from the examples depending on your Linux system.

---

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

# 2. Check User ID

## Command

```bash
id
```

## Example Output

```text
uid=1000(khushboo) gid=1000(khushboo) groups=1000(khushboo),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users),1001(docker)
```

> UID = User ID  
> GID = Group ID

---

# 3. Check Current User's Groups

## Command

```bash
groups
```

## Example Output

```text
khushboo adm cdrom sudo dip plugdev users docker
```

---

# 4. Check User Information

## Command

```bash
id khushboo
```

## Example Output

```text
uid=1000(khushboo) gid=1000(khushboo) groups=1000(khushboo),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users),1001(docker)
```

---

# 5. Check `/etc/passwd`

## Command

```bash
cat /etc/passwd
```

## Example Output

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
khushboo:x:1000:1000:Khushboo Chaudhari:/home/khushboo:/bin/bash
```

> `/etc/passwd` contains information about Linux users.

---

# 6. View Only Your User from `/etc/passwd`

## Command

```bash
grep "^khushboo:" /etc/passwd
```

## Example Output

```text
khushboo:x:1000:1000:Khushboo Chaudhari:/home/khushboo:/bin/bash
```

---

# 7. Understand `/etc/passwd` Fields

A line looks like:

```text
khushboo:x:1000:1000:Khushboo Chaudhari:/home/khushboo:/bin/bash
```

The fields are:

```text
username
password placeholder
UID
GID
comment
home directory
login shell
```

---

# 8. Check `/etc/group`

## Command

```bash
cat /etc/group
```

## Example Output

```text
root:x:0:
sudo:x:27:khushboo
users:x:100:
docker:x:1001:khushboo
```

---

# 9. Check a Specific Group

## Command

```bash
getent group sudo
```

## Example Output

```text
sudo:x:27:khushboo
```

---

# 10. Check Current Login Shell

## Command

```bash
echo $SHELL
```

## Example Output

```text
/bin/bash
```

---

# 11. Check User's Home Directory

## Command

```bash
echo $HOME
```

## Example Output

```text
/home/khushboo
```

---

# 12. Check Current User's Groups

## Command

```bash
id -Gn
```

## Example Output

```text
khushboo adm cdrom sudo dip plugdev users docker
```

---

# 13. Check Current User's UID

## Command

```bash
id -u
```

## Example Output

```text
1000
```

---

# 14. Check Current User's GID

## Command

```bash
id -g
```

## Example Output

```text
1000
```

---

# 15. Check Another User's UID

## Command

```bash
id -u root
```

## Example Output

```text
0
```

> UID `0` belongs to the root user.

---

# 16. Check Root User

## Command

```bash
id root
```

## Example Output

```text
uid=0(root) gid=0(root) groups=0(root)
```

---

# 17. Check Current User's Login Information

## Command

```bash
who
```

## Example Output

```text
khushboo  pts/0  2026-08-26 15:00
```

---

# 18. Check Who Is Logged In

## Command

```bash
w
```

## Example Output

```text
15:00:20 up 10:30, 1 user, load average: 0.00, 0.00, 0.00
USER      TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
khushboo  pts/0    -                15:00    1.00s  0.02s  0.00s w
```

---

# 19. Check Last Logins

## Command

```bash
last
```

## Example Output

```text
khushboo pts/0        2026-08-26 15:00   still logged in
khushboo pts/0        2026-08-26 10:00   still logged in
```

> Your output depends on your login history.

---

# 20. Check `sudo` Access

## Command

```bash
sudo -l
```

## Example Output

```text
User khushboo may run the following commands on KhushbooC-L:
    (ALL : ALL) ALL
```

> This shows commands the current user is allowed to run using `sudo`.

---

# 21. Check File Ownership

## Command

```bash
ls -l
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 183 Aug 26 15:00 README.md
```

The important part is:

```text
-rw-r--r-- 1 khushboo khushboo
             |        |
             owner    group
```

---

# 22. Understand File Permissions

## Command

```bash
ls -l README.md
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 183 Aug 26 15:00 README.md
```

Permission section:

```text
-rw-r--r--
```

Breakdown:

```text
-    rw-    r--    r--
|    |      |      |
type owner  group  others
```

---

# 23. Understand Permission Symbols

```text
r = read
w = write
x = execute
- = permission not granted
```

Example:

```text
-rwxr-xr--
```

Means:

```text
Owner  = rwx
Group  = r-x
Others = r--
```

---

# 24. Check Permission in Numeric Form

## Command

```bash
stat -c "%a %n" README.md
```

## Example Output

```text
644 README.md
```

---

# 25. Understand Permission 644

```text
644
```

Means:

```text
Owner  = 6 = rw-
Group  = 4 = r--
Others = 4 = r--
```

Therefore:

```text
rw-r--r--
```

---

# 26. Understand Permission Numbers

```text
4 = read
2 = write
1 = execute
```

Examples:

```text
7 = 4 + 2 + 1 = rwx
6 = 4 + 2     = rw-
5 = 4 + 1     = r-x
4 = 4         = r--
3 = 2 + 1     = -wx
2 = 2         = -w-
1 = 1         = --x
0 =           = ---
```

---

# 27. Create a Permission Lab Directory

## Command

```bash
mkdir permission-lab
```

## Example Output

```text
```

---

# 28. Enter Permission Lab

## Command

```bash
cd permission-lab
```

## Example Output

```text
```

---

# 29. Create a Test File

## Command

```bash
touch test.txt
```

## Example Output

```text
```

---

# 30. Check Default Permissions

## Command

```bash
ls -l test.txt
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 0 Aug 26 15:10 test.txt
```

> Default permissions depend on your `umask`.

---

# 31. Give Owner Execute Permission

## Command

```bash
chmod u+x test.txt
```

## Example Output

```text
```

---

# 32. Check Permissions

## Command

```bash
ls -l test.txt
```

## Example Output

```text
-rwxr--r-- 1 khushboo khushboo 0 Aug 26 15:10 test.txt
```

---

# 33. Remove Owner Execute Permission

## Command

```bash
chmod u-x test.txt
```

## Example Output

```text
```

---

# 34. Give Group Write Permission

## Command

```bash
chmod g+w test.txt
```

## Example Output

```text
```

---

# 35. Remove Group Write Permission

## Command

```bash
chmod g-w test.txt
```

## Example Output

```text
```

---

# 36. Give Others Read Permission

## Command

```bash
chmod o+r test.txt
```

## Example Output

```text
```

---

# 37. Remove Others Read Permission

## Command

```bash
chmod o-r test.txt
```

## Example Output

```text
```

---

# 38. Give Owner Full Permissions

## Command

```bash
chmod u+rwx test.txt
```

## Example Output

```text
```

---

# 39. Give Group Read and Execute

## Command

```bash
chmod g+rx test.txt
```

## Example Output

```text
```

---

# 40. Remove All Permissions from Others

## Command

```bash
chmod o-rwx test.txt
```

## Example Output

```text
```

---

# 41. Set Permission Using Numeric Mode

## Command

```bash
chmod 644 test.txt
```

## Example Output

```text
```

---

# 42. Verify 644 Permission

## Command

```bash
ls -l test.txt
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 0 Aug 26 15:15 test.txt
```

---

# 43. Set 755 Permission

## Command

```bash
chmod 755 test.txt
```

## Example Output

```text
```

---

# 44. Verify 755 Permission

## Command

```bash
ls -l test.txt
```

## Example Output

```text
-rwxr-xr-x 1 khushboo khushboo 0 Aug 26 15:16 test.txt
```

---

# 45. Set 700 Permission

## Command

```bash
chmod 700 test.txt
```

## Example Output

```text
```

---

# 46. Verify 700 Permission

## Command

```bash
ls -l test.txt
```

## Example Output

```text
-rwx------ 1 khushboo khushboo 0 Aug 26 15:17 test.txt
```

---

# 47. Set 600 Permission

## Command

```bash
chmod 600 test.txt
```

## Example Output

```text
```

---

# 48. Verify 600 Permission

## Command

```bash
ls -l test.txt
```

## Example Output

```text
-rw------- 1 khushboo khushboo 0 Aug 26 15:18 test.txt
```

---

# 49. Set Directory Permission

## Command

```bash
chmod 755 permission-lab
```

## Example Output

```text
```

---

# 50. Check Directory Permission

## Command

```bash
ls -ld permission-lab
```

## Example Output

```text
drwxr-xr-x 2 khushboo khushboo 4096 Aug 26 15:10 permission-lab
```

> `ls -ld` shows permissions of the directory itself.

---

# 51. Create a Test User

## Command

```bash
sudo useradd testuser
```

## Example Output

```text
```

---

# 52. Check Test User

## Command

```bash
id testuser
```

## Example Output

```text
uid=1001(testuser) gid=1001(testuser) groups=1001(testuser)
```

> UID may be different on your system.

---

# 53. Check Test User in `/etc/passwd`

## Command

```bash
grep "^testuser:" /etc/passwd
```

## Example Output

```text
testuser:x:1001:1001::/home/testuser:/bin/sh
```

---

# 54. Create User with Home Directory

## Command

```bash
sudo useradd -m labuser
```

## Example Output

```text
```

> `-m` creates the user's home directory.

---

# 55. Check User Home Directory

## Command

```bash
ls -ld /home/labuser
```

## Example Output

```text
drwxr-x--- 2 labuser labuser 4096 Aug 26 15:25 /home/labuser
```

---

# 56. Create User with Bash Shell

## Command

```bash
sudo useradd -m -s /bin/bash devuser
```

## Example Output

```text
```

---

# 57. Check User Shell

## Command

```bash
getent passwd devuser
```

## Example Output

```text
devuser:x:1003:1003::/home/devuser:/bin/bash
```

---

# 58. Set Password for a User

## Command

```bash
sudo passwd devuser
```

## Example Output

```text
New password:
Retype new password:
passwd: password updated successfully
```

> Do not use a real production password in a lab.

---

# 59. Switch to Another User

## Command

```bash
su - devuser
```

## Example Output

```text
devuser@KhushbooC-L:~$
```

---

# 60. Check Current User After Switching

## Command

```bash
whoami
```

## Example Output

```text
devuser
```

---

# 61. Check User ID After Switching

## Command

```bash
id
```

## Example Output

```text
uid=1003(devuser) gid=1003(devuser) groups=1003(devuser)
```

---

# 62. Return to Previous User

## Command

```bash
exit
```

## Example Output

```text
logout
khushboo@KhushbooC-L:~$
```

---

# 63. Create a Group

## Command

```bash
sudo groupadd developers
```

## Example Output

```text
```

---

# 64. Check Group

## Command

```bash
getent group developers
```

## Example Output

```text
developers:x:1004:
```

---

# 65. Add User to Group

## Command

```bash
sudo usermod -aG developers devuser
```

## Example Output

```text
```

> `-aG` means append the user to the supplementary group.

---

# 66. Verify Group Membership

## Command

```bash
id devuser
```

## Example Output

```text
uid=1003(devuser) gid=1003(devuser) groups=1003(devuser),1004(developers)
```

---

# 67. Check Group Membership

## Command

```bash
groups devuser
```

## Example Output

```text
devuser : devuser developers
```

---

# 68. Remove User from a Group

## Command

```bash
sudo gpasswd -d devuser developers
```

## Example Output

```text
Removing user devuser from group developers
```

---

# 69. Verify Group Removal

## Command

```bash
groups devuser
```

## Example Output

```text
devuser : devuser
```

---

# 70. Add User to Multiple Groups

## Command

```bash
sudo usermod -aG developers,sudo devuser
```

## Example Output

```text
```

> ⚠️ Adding a user to `sudo` gives administrative privileges. Do this only in a lab environment.

---

# 71. Check Group Membership

## Command

```bash
id devuser
```

## Example Output

```text
uid=1003(devuser) gid=1003(devuser) groups=1003(devuser),27(sudo),1004(developers)
```

---

# 72. Change File Owner

First create a test file:

```bash
touch owner-test.txt
```

Then:

```bash
sudo chown devuser owner-test.txt
```

## Example Output

```text
```

---

# 73. Check New Owner

## Command

```bash
ls -l owner-test.txt
```

## Example Output

```text
-rw-r--r-- 1 devuser khushboo 0 Aug 26 15:35 owner-test.txt
```

---

# 74. Change Owner and Group

## Command

```bash
sudo chown devuser:developers owner-test.txt
```

## Example Output

```text
```

---

# 75. Verify Owner and Group

## Command

```bash
ls -l owner-test.txt
```

## Example Output

```text
-rw-r--r-- 1 devuser developers 0 Aug 26 15:35 owner-test.txt
```

---

# 76. Change Only Group

## Command

```bash
sudo chgrp developers owner-test.txt
```

## Example Output

```text
```

---

# 77. Verify Group

## Command

```bash
ls -l owner-test.txt
```

## Example Output

```text
-rw-r--r-- 1 devuser developers 0 Aug 26 15:35 owner-test.txt
```

---

# 78. Change Directory Ownership Recursively

## Command

```bash
sudo chown -R devuser:developers permission-lab
```

## Example Output

```text
```

> `-R` means recursive.

---

# 79. Verify Recursive Ownership

## Command

```bash
ls -l permission-lab
```

## Example Output

```text
-rw------- 1 devuser developers 0 Aug 26 15:18 test.txt
```

---

# 80. Check `umask`

## Command

```bash
umask
```

## Example Output

```text
0022
```

> `umask` controls default permissions for newly created files and directories.

---

# 81. Display `umask` Symbolically

## Command

```bash
umask -S
```

## Example Output

```text
u=rwx,g=rx,o=rx
```

---

# 82. Create File with Current `umask`

## Command

```bash
touch umask-test.txt
```

## Example Output

```text
```

---

# 83. Check Permission

## Command

```bash
ls -l umask-test.txt
```

## Example Output

```text
-rw-r--r-- 1 khushboo khushboo 0 Aug 26 15:45 umask-test.txt
```

---

# 84. Temporarily Change `umask`

## Command

```bash
umask 077
```

## Example Output

```text
```

---

# 85. Create a File with `umask 077`

## Command

```bash
touch private.txt
```

## Example Output

```text
```

---

# 86. Check Private File Permission

## Command

```bash
ls -l private.txt
```

## Example Output

```text
-rw------- 1 khushboo khushboo 0 Aug 26 15:50 private.txt
```

---

# 87. Restore Common `umask`

## Command

```bash
umask 022
```

## Example Output

```text
```

---

# 88. Understand Directory Execute Permission

Create a directory:

```bash
mkdir directory-test
touch directory-test/file.txt
```

Remove execute permission:

```bash
chmod 644 directory-test
```

## Example Output

```text
```

> Without execute permission on a directory, users cannot normally access files inside it even if the files themselves are readable.

Restore it:

```bash
chmod 755 directory-test
```

---

# 89. Test Read Permission

## Command

```bash
echo "Secret data" > read-test.txt
chmod 444 read-test.txt
cat read-test.txt
```

## Example Output

```text
Secret data
```

---

# 90. Test Write Permission

## Command

```bash
chmod 444 read-test.txt
echo "New data" >> read-test.txt
```

## Example Output

```text
bash: read-test.txt: Permission denied
```

> The exact error message may vary slightly.

---

# 91. Restore Write Permission

## Command

```bash
chmod 644 read-test.txt
```

## Example Output

```text
```

---

# 92. Test Execute Permission

Create a script:

```bash
echo '#!/bin/bash' > test-script.sh
echo 'echo "Script executed successfully"' >> test-script.sh
```

Try to execute:

```bash
./test-script.sh
```

## Example Output

```text
bash: ./test-script.sh: Permission denied
```

---

# 93. Add Execute Permission

## Command

```bash
chmod +x test-script.sh
```

## Example Output

```text
```

---

# 94. Execute the Script

## Command

```bash
./test-script.sh
```

## Example Output

```text
Script executed successfully
```

---

# 95. Check SUID Files

## Command

```bash
find /usr/bin -perm -4000 -type f 2>/dev/null
```

## Example Output

```text
/usr/bin/passwd
/usr/bin/su
/usr/bin/mount
/usr/bin/umount
```

> SUID allows a program to run with the privileges of the file owner.

---

# 96. Check SGID Files

## Command

```bash
find /usr/bin -perm -2000 -type f 2>/dev/null
```

## Example Output

```text
/usr/bin/chage
/usr/bin/ssh-agent
```

> Results vary by Linux distribution.

---

# 97. Create an SGID Directory

## Command

```bash
mkdir shared
chmod 2775 shared
```

## Example Output

```text
```

---

# 98. Check SGID Directory

## Command

```bash
ls -ld shared
```

## Example Output

```text
drwxrwsr-x 2 khushboo khushboo 4096 Aug 26 16:00 shared
```

> Notice the `s` in the group execute position.

---

# 99. Create a Sticky Bit Directory

## Command

```bash
mkdir shared-temp
chmod 1777 shared-temp
```

## Example Output

```text
```

---

# 100. Check Sticky Bit

## Command

```bash
ls -ld shared-temp
```

## Example Output

```text
drwxrwxrwt 2 khushboo khushboo 4096 Aug 26 16:05 shared-temp
```

> Notice the `t` at the end.

---

# 101. Check ACL Support

## Command

```bash
getfacl --version
```

## Example Output

```text
getfacl 2.3.2
```

> If the command is not available, install ACL tools:

```bash
sudo apt install acl
```

---

# 102. View File ACL

## Command

```bash
getfacl owner-test.txt
```

## Example Output

```text
# file: owner-test.txt
# owner: devuser
# group: developers
user::rw-
group::r--
other::r--
```

---

# 103. Add ACL Permission for a User

## Command

```bash
sudo setfacl -m u:devuser:rw owner-test.txt
```

## Example Output

```text
```

---

# 104. Check ACL

## Command

```bash
getfacl owner-test.txt
```

## Example Output

```text
# file: owner-test.txt
# owner: devuser
# group: developers
user::rw-
user:devuser:rw-
group::r--
mask::rw-
other::r--
```

---

# 105. Remove User ACL

## Command

```bash
sudo setfacl -x u:devuser owner-test.txt
```

## Example Output

```text
```

---

# 106. Remove All Extended ACLs

## Command

```bash
sudo setfacl -b owner-test.txt
```

## Example Output

```text
```

---

# 107. Check ACL Again

## Command

```bash
getfacl owner-test.txt
```

## Example Output

```text
# file: owner-test.txt
# owner: devuser
# group: developers
user::rw-
group::r--
other::r--
```

---

# 108. Check Permission with `namei`

## Command

```bash
namei -l /home/khushboo
```

## Example Output

```text
f: /home/khushboo
drwxr-xr-x root     root     /
drwxr-xr-x root     root     home
drwx------ khushboo khushboo khushboo
```

> `namei` helps troubleshoot permissions on every directory in a path.

---

# 109. Check Directory Permissions Recursively

## Command

```bash
namei -l /home/khushboo/permission-lab/test.txt
```

## Example Output

```text
f: /home/khushboo/permission-lab/test.txt
drwxr-xr-x root     root     /
drwxr-xr-x root     root     home
drwx------ khushboo khushboo khushboo
drwxr-xr-x khushboo khushboo permission-lab
-rw------- khushboo khushboo test.txt
```

---

# 110. Check Effective User

## Command

```bash
whoami
```

## Example Output

```text
khushboo
```

---

# 111. Run Command as Root

## Command

```bash
sudo whoami
```

## Example Output

```text
root
```

> `sudo` runs the command with elevated privileges when the user is authorized.

---

# 112. Check Root Environment

## Command

```bash
sudo id
```

## Example Output

```text
uid=0(root) gid=0(root) groups=0(root)
```

---

# 113. Compare Normal and Root Access

## Command

```bash
whoami
sudo whoami
```

## Example Output

```text
khushboo
root
```

---

# 114. Check Ownership of `/etc/passwd`

## Command

```bash
ls -l /etc/passwd
```

## Example Output

```text
-rw-r--r-- 1 root root 3200 Aug 26 10:00 /etc/passwd
```

---

# 115. Check Ownership of `/etc/shadow`

## Command

```bash
sudo ls -l /etc/shadow
```

## Example Output

```text
-rw-r----- 1 root shadow 1800 Aug 26 10:00 /etc/shadow
```

> `/etc/shadow` contains sensitive password-related information and is normally restricted.

---

# 116. Try Reading `/etc/shadow`

## Command

```bash
cat /etc/shadow
```

## Example Output

```text
cat: /etc/shadow: Permission denied
```

---

# 117. Read `/etc/shadow` with Sudo

## Command

```bash
sudo cat /etc/shadow
```

## Example Output

```text
root:!:...
daemon:*:...
```

> ⚠️ Do not share or publish the contents of `/etc/shadow`.

---

# 118. Check Password Policy

## Command

```bash
sudo chage -l devuser
```

## Example Output

```text
Last password change                                    : Aug 26, 2026
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```

---

# 119. Lock a User Account

## Command

```bash
sudo passwd -l devuser
```

## Example Output

```text
passwd: password changed.
```

---

# 120. Unlock a User Account

## Command

```bash
sudo passwd -u devuser
```

## Example Output

```text
passwd: password changed.
```

---

# 121. Disable User Login Shell

## Command

```bash
sudo usermod -s /usr/sbin/nologin devuser
```

## Example Output

```text
```

---

# 122. Check User Shell

## Command

```bash
getent passwd devuser
```

## Example Output

```text
devuser:x:1003:1003::/home/devuser:/usr/sbin/nologin
```

---

# 123. Restore Bash Shell

## Command

```bash
sudo usermod -s /bin/bash devuser
```

## Example Output

```text
```

---

# 124. Delete Test User

## Command

```bash
sudo userdel testuser
```

## Example Output

```text
```

---

# 125. Delete User and Home Directory

## Command

```bash
sudo userdel -r labuser
```

## Example Output

```text
```

> ⚠️ `-r` also removes the user's home directory.

---

# 126. Delete Test Group

## Command

```bash
sudo groupdel developers
```

## Example Output

```text
```

> Make sure the group is not being used as a primary group before deleting it.

---

# 🧪 Practical Lab 1 — User and Group Management

Create a lab user:

```bash
sudo useradd -m -s /bin/bash developer
```

Create a group:

```bash
sudo groupadd devops
```

Add the user to the group:

```bash
sudo usermod -aG devops developer
```

Check:

```bash
id developer
```

## Example Output

```text
uid=1004(developer) gid=1004(developer) groups=1004(developer),1005(devops)
```

---

# 🧪 Practical Lab 2 — Shared DevOps Directory

Create the directory:

```bash
sudo mkdir -p /opt/devops/shared
```

Create the group:

```bash
sudo groupadd devops-team
```

Add the user:

```bash
sudo usermod -aG devops-team developer
```

Change ownership:

```bash
sudo chown -R root:devops-team /opt/devops/shared
```

Set permissions:

```bash
sudo chmod -R 2775 /opt/devops/shared
```

Check:

```bash
ls -ld /opt/devops/shared
```

## Example Output

```text
drwxrwsr-x 2 root devops-team 4096 Aug 26 16:30 /opt/devops/shared
```

> This is a common pattern for shared application/deployment directories.

---

# 🧪 Practical Lab 3 — Private Configuration File

Create:

```bash
sudo mkdir -p /opt/myapp/config
```

Create configuration:

```bash
sudo touch /opt/myapp/config/app.conf
```

Set owner:

```bash
sudo chown root:root /opt/myapp/config/app.conf
```

Set secure permissions:

```bash
sudo chmod 600 /opt/myapp/config/app.conf
```

Check:

```bash
ls -l /opt/myapp/config/app.conf
```

## Example Output

```text
-rw------- 1 root root 0 Aug 26 16:40 /opt/myapp/config/app.conf
```

> `600` means only the owner can read and write the file.

---

# 🧪 Practical Lab 4 — Web Application Permissions

Create:

```bash
sudo mkdir -p /var/www/myapp
```

Create an application file:

```bash
sudo touch /var/www/myapp/index.html
```

Set ownership:

```bash
sudo chown -R root:www-data /var/www/myapp
```

Set directory permissions:

```bash
sudo find /var/www/myapp -type d -exec chmod 755 {} \;
```

Set file permissions:

```bash
sudo find /var/www/myapp -type f -exec chmod 644 {} \;
```

Check:

```bash
ls -l /var/www/myapp
```

## Example Output

```text
-rw-r--r-- 1 root www-data 0 Aug 26 16:50 index.html
```

---

# 🧪 Practical Lab 5 — Permission Denied Troubleshooting

Create a file:

```bash
echo "secret data" > secret.txt
```

Remove read permission:

```bash
chmod 000 secret.txt
```

Try reading:

```bash
cat secret.txt
```

## Example Output

```text
cat: secret.txt: Permission denied
```

Check permissions:

```bash
ls -l secret.txt
```

## Example Output

```text
---------- 1 khushboo khushboo 12 Aug 26 17:00 secret.txt
```

Fix:

```bash
chmod 644 secret.txt
```

Verify:

```bash
cat secret.txt
```

## Example Output

```text
secret data
```

---

# 🧪 Practical Lab 6 — Troubleshoot Directory Permission

Create:

```bash
mkdir restricted
touch restricted/file.txt
```

Remove directory execute permission:

```bash
chmod 644 restricted
```

Try:

```bash
ls restricted
```

## Example Output

```text
ls: cannot access 'restricted/file.txt': Permission denied
```

Check:

```bash
ls -ld restricted
```

## Example Output

```text
drw-r--r-- 2 khushboo khushboo 4096 Aug 26 17:10 restricted
```

Fix:

```bash
chmod 755 restricted
```

Check:

```bash
ls restricted
```

## Example Output

```text
file.txt
```

---

# 🧪 Practical Lab 7 — ACL Access

Create:

```bash
touch acl-test.txt
```

Set normal permission:

```bash
chmod 600 acl-test.txt
```

Add ACL:

```bash
sudo setfacl -m u:devuser:r acl-test.txt
```

Check:

```bash
getfacl acl-test.txt
```

## Example Output

```text
# file: acl-test.txt
# owner: khushboo
# group: khushboo
user::rw-
user:devuser:r--
group::---
mask::r--
other::---
```

> ACL allows more granular access than standard owner/group/other permissions.

---

# 🧪 Practical Lab 8 — DevOps Permission Investigation

Suppose an application gives:

```text
Permission denied
```

Run these commands:

## Step 1 — Check current user

```bash
whoami
```

## Step 2 — Check groups

```bash
id
```

## Step 3 — Check file permissions

```bash
ls -l /path/to/file
```

## Step 4 — Check parent directory permissions

```bash
namei -l /path/to/file
```

## Step 5 — Check ACL

```bash
getfacl /path/to/file
```

## Step 6 — Check ownership

```bash
stat /path/to/file
```

## Step 7 — Test access

```bash
sudo -u username cat /path/to/file
```

This workflow is useful when troubleshooting:

```text
Nginx
Gunicorn
Uvicorn
Docker
Jenkins
systemd
Python applications
Node.js applications
```

---

# 🧪 Practical Lab 9 — Jenkins Permission Scenario

Create a deployment directory:

```bash
sudo mkdir -p /opt/myapp
```

Create a deployment file:

```bash
sudo touch /opt/myapp/deploy.sh
```

Set ownership:

```bash
sudo chown root:devops-team /opt/myapp/deploy.sh
```

Set permissions:

```bash
sudo chmod 775 /opt/myapp/deploy.sh
```

Check:

```bash
ls -l /opt/myapp/deploy.sh
```

## Example Output

```text
-rwxrwxr-x 1 root devops-team 0 Aug 26 17:30 /opt/myapp/deploy.sh
```

> This allows the owner and members of `devops-team` to read, write, and execute the script.

---

# 🧪 Practical Lab 10 — Find Files with Dangerous Permissions

Find world-writable files:

```bash
find . -type f -perm -002
```

## Example Output

```text
./test-world-writable.txt
```

Find world-writable directories:

```bash
find . -type d -perm -002
```

## Example Output

```text
./shared-temp
```

> World-writable permissions should be reviewed carefully on production systems.

---

# 🧪 Practical Lab 11 — Find SUID Files

## Command

```bash
sudo find / -type f -perm -4000 2>/dev/null
```

## Example Output

```text
/usr/bin/passwd
/usr/bin/su
/usr/bin/mount
/usr/bin/umount
```

---

# 🧪 Practical Lab 12 — Find SGID Files

## Command

```bash
sudo find / -type f -perm -2000 2>/dev/null
```

## Example Output

```text
/usr/bin/chage
/usr/bin/ssh-agent
```

---

# 🧪 Practical Lab 13 — Find Files Owned by a User

## Command

```bash
find /tmp -user khushboo 2>/dev/null
```

## Example Output

```text
/tmp/test.txt
/tmp/application.log
```

---

# 🧪 Practical Lab 14 — Find Files Owned by Root

## Command

```bash
find /etc -user root -type f 2>/dev/null | head
```

## Example Output

```text
/etc/passwd
/etc/group
/etc/hostname
/etc/hosts
/etc/fstab
```

---

# 🧪 Practical Lab 15 — Check Permission of an Application

Assume application:

```text
/opt/myapp
```

Run:

```bash
ls -ld /opt/myapp
```

Then:

```bash
namei -l /opt/myapp
```

Then:

```bash
find /opt/myapp -maxdepth 2 -ls
```

Then:

```bash
getfacl /opt/myapp
```

Then:

```bash
sudo -u devuser ls -la /opt/myapp
```

This helps determine:

```text
Who owns the application?
Which group owns it?
Can the user enter the directory?
Can the user read files?
Can the user write files?
Are ACLs configured?
```

---

# 📚 Permission Cheat Sheet

## Read

```text
r = 4
```

## Write

```text
w = 2
```

## Execute

```text
x = 1
```

## Common Permissions

```text
600 = rw-------
644 = rw-r--r--
700 = rwx------
755 = rwxr-xr-x
775 = rwxrwxr-x
777 = rwxrwxrwx
```

---

# 📚 Ownership Commands

| Command | Purpose |
|---|---|
| `ls -l` | Check ownership and permissions |
| `chown` | Change owner |
| `chgrp` | Change group |
| `id` | Show user/group IDs |
| `groups` | Show group membership |
| `getent passwd` | Query user information |
| `getent group` | Query group information |

---

# 📚 User Commands

| Command | Purpose |
|---|---|
| `useradd` | Create user |
| `usermod` | Modify user |
| `userdel` | Delete user |
| `passwd` | Set/change password |
| `su` | Switch user |
| `sudo` | Run command with elevated privileges |
| `whoami` | Show current user |
| `who` | Show logged-in users |
| `w` | Show logged-in users and activity |
| `last` | Show login history |
| `chage` | Manage password aging |

---

# 📚 Group Commands

| Command | Purpose |
|---|---|
| `groupadd` | Create group |
| `groupdel` | Delete group |
| `groups` | Show user's groups |
| `usermod -aG` | Add user to group |
| `gpasswd -d` | Remove user from group |
| `getent group` | Query group information |

---

# 📚 Permission Commands

| Command | Purpose |
|---|---|
| `chmod` | Change permissions |
| `chown` | Change owner |
| `chgrp` | Change group |
| `umask` | Control default permissions |
| `getfacl` | View ACL |
| `setfacl` | Modify ACL |
| `namei -l` | Inspect path permissions |
| `stat` | Show detailed metadata |

---

# 📚 Special Permissions

| Permission | Numeric | Purpose |
|---|---:|---|
| SUID | `4000` | Execute with file owner's privileges |
| SGID | `2000` | Execute with group privileges / inherit group on directories |
| Sticky Bit | `1000` | Restrict deletion in shared directories |

Examples:

```bash
chmod 4755 file
chmod 2775 directory
chmod 1777 directory
```

---

# 🧠 Important Security Rules

## Rule 1 — Avoid `777`

Avoid:

```bash
chmod 777 file
```

unless there is a specific reason.

---

## Rule 2 — Use Least Privilege

Give users only the permissions they actually need.

---

## Rule 3 — Protect Secrets

Configuration files containing:

```text
passwords
API keys
database credentials
private keys
tokens
```

should not normally be world-readable.

Example:

```bash
chmod 600 .env
```

---

## Rule 4 — Be Careful with `sudo`

Before running:

```bash
sudo
```

understand what the command will modify.

---

## Rule 5 — Be Careful with Recursive Commands

Commands such as:

```bash
sudo chmod -R
sudo chown -R
```

can change permissions or ownership of thousands of files.

Always verify the path first:

```bash
pwd
ls -la
```

---

