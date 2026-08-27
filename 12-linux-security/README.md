# 🔐 Linux Security — Hands-on Lab

---

# 1. Check Current User

## Command

```bash
whoami
```

## Example Output

```text
devops
```

`whoami` displays the currently logged-in username.

---

# 2. Display User ID

## Command

```bash
id
```

## Example Output

```text
uid=1000(devops) gid=1000(devops) groups=1000(devops),27(sudo)
```

---

# 3. Display Current User ID Only

## Command

```bash
id -u
```

## Example Output

```text
1000
```

---

# 4. Display Current Group ID

## Command

```bash
id -g
```

## Example Output

```text
1000
```

---

# 5. Display Current User Groups

## Command

```bash
id -Gn
```

## Example Output

```text
devops sudo docker
```

---

# 6. Display All Groups of Current User

## Command

```bash
groups
```

## Example Output

```text
devops : devops sudo docker
```

---

# 7. Display Logged-In Users

## Command

```bash
who
```

## Example Output

```text
devops   pts/0   2026-08-27 09:20 (192.168.1.50)
```

---

# 8. Display Detailed Login Information

## Command

```bash
w
```

## Example Output

```text
USER   TTY   FROM          LOGIN@   IDLE   JCPU   PCPU WHAT
devops pts/0 192.168.1.50 09:20    1:00   0.10s  0.02s bash
```

---

# 9. Display Login History

## Command

```bash
last
```

## Example Output

```text
devops pts/0 192.168.1.50 Thu Aug 27 09:20 still logged in
```

---

# 10. Display Failed Login Attempts

## Command

```bash
sudo lastb
```

## Example Output

```text
unknown pts/1 192.168.1.100 Thu Aug 27 08:30 - 08:30
```

---

# 11. Display Last Login of Users

## Command

```bash
lastlog
```

## Example Output

```text
Username         Port     From             Latest
root             **Never logged in**
devops           pts/0    192.168.1.50     Thu Aug 27 09:20
```

---

# 12. Display Password Information

## Command

```bash
sudo chage -l devops
```

## Example Output

```text
Last password change                                    : Aug 01, 2026
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change           : 99999
```

---

# 13. Display User Account Information

## Command

```bash
getent passwd devops
```

## Example Output

```text
devops:x:1000:1000:DevOps User:/home/devops:/bin/bash
```

---

# 14. Display All Users

## Command

```bash
cut -d: -f1 /etc/passwd
```

## Example Output

```text
root
daemon
www-data
devops
```

---

# 15. Display Users With Login Shell

## Command

```bash
grep -vE '/nologin|/false' /etc/passwd
```

## Example Output

```text
root:x:0:0:root:/root:/bin/bash
devops:x:1000:1000:DevOps User:/home/devops:/bin/bash
```

---

# 16. Display System Users

## Command

```bash
awk -F: '$3 < 1000 {print $1}' /etc/passwd
```

## Example Output

```text
root
daemon
bin
sys
sync
www-data
```

---

# 17. Check Root User

## Command

```bash
id root
```

## Example Output

```text
uid=0(root) gid=0(root) groups=0(root)
```

---

# 18. Switch to Root User

## Command

```bash
sudo -i
```

## Example Output

```text
root@server:~#
```

---

# 19. Execute Command as Root

## Command

```bash
sudo whoami
```

## Example Output

```text
root
```

---

# 20. Display Sudo Permissions

## Command

```bash
sudo -l
```

## Example Output

```text
User devops may run the following commands:
    (ALL : ALL) ALL
```

---

# 21. Check Sudo Configuration

## Command

```bash
sudo visudo
```

## Example Output

```text
#
# This file MUST be edited with the 'visudo' command as root.
#
```

Always use `visudo` instead of directly editing `/etc/sudoers`.

---

# 22. Display Sudoers File

## Command

```bash
sudo cat /etc/sudoers
```

## Example Output

```text
root ALL=(ALL:ALL) ALL
%sudo ALL=(ALL:ALL) ALL
```

---

# 23. Display Sudo Configuration Directory

## Command

```bash
sudo ls -la /etc/sudoers.d/
```

## Example Output

```text
-r--r----- 1 root root  45 devops
```

---

# 24. Check File Permissions

## Command

```bash
ls -l /etc/passwd
```

## Example Output

```text
-rw-r--r-- 1 root root 3200 Aug 27 09:00 /etc/passwd
```

---

# 25. Check Shadow File Permissions

## Command

```bash
sudo ls -l /etc/shadow
```

## Example Output

```text
-rw-r----- 1 root shadow 1800 Aug 27 09:00 /etc/shadow
```

---

# 26. Check Group File Permissions

## Command

```bash
ls -l /etc/group
```

## Example Output

```text
-rw-r--r-- 1 root root 1500 Aug 27 09:00 /etc/group
```

---

# 27. Check Shadow Group Permissions

## Command

```bash
sudo ls -l /etc/gshadow
```

## Example Output

```text
-rw-r----- 1 root shadow 1200 Aug 27 09:00 /etc/gshadow
```

---

# 28. Display File Permissions

## Command

```bash
ls -l file.txt
```

## Example Output

```text
-rw-r--r-- 1 devops devops 1024 Aug 27 10:00 file.txt
```

---

# 29. Change File Permission

## Command

```bash
chmod 600 secret.txt
```

## Example Output

```text
```

---

# 30. Change Directory Permission

## Command

```bash
chmod 755 application
```

## Example Output

```text
```

---

# 31. Give Execute Permission

## Command

```bash
chmod +x script.sh
```

## Example Output

```text
```

---

# 32. Remove Execute Permission

## Command

```bash
chmod -x script.sh
```

## Example Output

```text
```

---

# 33. Set Owner Read/Write Permission

## Command

```bash
chmod u+rw file.txt
```

## Example Output

```text
```

---

# 34. Remove Group Write Permission

## Command

```bash
chmod g-w file.txt
```

## Example Output

```text
```

---

# 35. Remove Other Write Permission

## Command

```bash
chmod o-w file.txt
```

## Example Output

```text
```

---

# 36. Set Read Permission for Everyone

## Command

```bash
chmod a+r file.txt
```

## Example Output

```text
```

---

# 37. Set Permission Using Numeric Mode

## Command

```bash
chmod 644 file.txt
```

## Example Output

```text
```

---

# 38. Set Executable Script Permission

## Command

```bash
chmod 755 script.sh
```

## Example Output

```text
```

---

# 39. Set Private File Permission

## Command

```bash
chmod 600 secret.txt
```

## Example Output

```text
```

---

# 40. Set Private Directory Permission

## Command

```bash
chmod 700 private
```

## Example Output

```text
```

---

# 41. Recursively Change Permissions

## Command

```bash
chmod -R 755 application/
```

## Example Output

```text
```

Use recursive permissions carefully in production.

---

# 42. Change File Owner

## Command

```bash
sudo chown devops file.txt
```

## Example Output

```text
```

---

# 43. Change File Group

## Command

```bash
sudo chgrp devops file.txt
```

## Example Output

```text
```

---

# 44. Change Owner and Group

## Command

```bash
sudo chown devops:devops file.txt
```

## Example Output

```text
```

---

# 45. Recursively Change Ownership

## Command

```bash
sudo chown -R devops:devops application/
```

## Example Output

```text
```

---

# 46. Display File Ownership

## Command

```bash
stat file.txt
```

## Example Output

```text
File: file.txt
Size: 1024
Uid: 1000
Gid: 1000
Access: (0644/-rw-r--r--)
```

---

# 47. Display Permission Bits Only

## Command

```bash
stat -c '%A %a %n' file.txt
```

## Example Output

```text
-rw-r--r-- 644 file.txt
```

---

# 48. Find World-Writable Files

## Command

```bash
sudo find / -type f -perm -0002 2>/dev/null
```

## Example Output

```text
/tmp/example.txt
/var/tmp/test.log
```

---

# 49. Find World-Writable Directories

## Command

```bash
sudo find / -type d -perm -0002 2>/dev/null
```

## Example Output

```text
/tmp
/var/tmp
```

---

# 50. Find SUID Files

## Command

```bash
sudo find / -type f -perm -4000 2>/dev/null
```

## Example Output

```text
/usr/bin/passwd
/usr/bin/sudo
/usr/bin/su
```

---

# 51. Find SGID Files

## Command

```bash
sudo find / -type f -perm -2000 2>/dev/null
```

## Example Output

```text
/usr/bin/wall
/usr/bin/chage
```

---

# 52. Find SUID and SGID Files

## Command

```bash
sudo find / -type f \( -perm -4000 -o -perm -2000 \) 2>/dev/null
```

## Example Output

```text
/usr/bin/passwd
/usr/bin/sudo
/usr/bin/wall
```

---

# 53. Check Sticky Bit

## Command

```bash
ls -ld /tmp
```

## Example Output

```text
drwxrwxrwt 10 root root 4096 Aug 27 10:00 /tmp
```

The `t` indicates the sticky bit.

---

# 54. Set Sticky Bit

## Command

```bash
chmod +t shared/
```

## Example Output

```text
```

---

# 55. Remove Sticky Bit

## Command

```bash
chmod -t shared/
```

## Example Output

```text
```

---

# 56. Check ACL

## Command

```bash
getfacl file.txt
```

## Example Output

```text
# file: file.txt
# owner: devops
# group: devops
user::rw-
group::r--
other::r--
```

---

# 57. Set ACL Permission

## Command

```bash
setfacl -m u:john:r file.txt
```

## Example Output

```text
```

---

# 58. Remove ACL Entry

## Command

```bash
setfacl -x u:john file.txt
```

## Example Output

```text
```

---

# 59. Set Default ACL on Directory

## Command

```bash
setfacl -d -m g:devops:rwx application/
```

## Example Output

```text
```

---

# 60. Remove All ACL Entries

## Command

```bash
setfacl -b file.txt
```

## Example Output

```text
```

---

# 61. Display User Groups

## Command

```bash
getent group
```

## Example Output

```text
root:x:0:
sudo:x:27:devops
docker:x:999:devops
```

---

# 62. Check Specific Group

## Command

```bash
getent group sudo
```

## Example Output

```text
sudo:x:27:devops
```

---

# 63. Create User

## Command

```bash
sudo useradd devuser
```

## Example Output

```text
```

---

# 64. Create User With Home Directory

## Command

```bash
sudo useradd -m devuser
```

## Example Output

```text
```

---

# 65. Create User With Bash Shell

## Command

```bash
sudo useradd -m -s /bin/bash devuser
```

## Example Output

```text
```

---

# 66. Set User Password

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

---

# 67. Lock User Account

## Command

```bash
sudo passwd -l devuser
```

## Example Output

```text
passwd: password changed.
```

---

# 68. Unlock User Account

## Command

```bash
sudo passwd -u devuser
```

## Example Output

```text
passwd: password changed.
```

---

# 69. Delete User

## Command

```bash
sudo userdel devuser
```

## Example Output

```text
```

---

# 70. Delete User and Home Directory

## Command

```bash
sudo userdel -r devuser
```

## Example Output

```text
```

---

# 71. Change User Shell

## Command

```bash
sudo chsh -s /bin/bash devuser
```

## Example Output

```text
```

---

# 72. Change User Information

## Command

```bash
sudo usermod -c "DevOps User" devuser
```

## Example Output

```text
```

---

# 73. Add User to Group

## Command

```bash
sudo usermod -aG sudo devuser
```

## Example Output

```text
```

---

# 74. Add User to Docker Group

## Command

```bash
sudo usermod -aG docker devuser
```

## Example Output

```text
```

Adding a user to the `docker` group effectively grants root-equivalent control over the host.

---

# 75. Remove User From Group

## Command

```bash
sudo gpasswd -d devuser docker
```

## Example Output

```text
Removing user devuser from group docker
```

---

# 76. Create Group

## Command

```bash
sudo groupadd developers
```

## Example Output

```text
```

---

# 77. Delete Group

## Command

```bash
sudo groupdel developers
```

## Example Output

```text
```

---

# 78. Display User Account Status

## Command

```bash
sudo passwd -S devops
```

## Example Output

```text
devops P 08/01/2026 0 99999 7 -1
```

---

# 79. Check Locked Accounts

## Command

```bash
sudo passwd -S -a
```

## Example Output

```text
root L
devops P
```

---

# 80. Check Login Shell

## Command

```bash
getent passwd devops | cut -d: -f7
```

## Example Output

```text
/bin/bash
```

---

# 81. Disable Interactive Login

## Command

```bash
sudo usermod -s /usr/sbin/nologin devuser
```

## Example Output

```text
```

---

# 82. Check SSH Service

## Command

```bash
sudo systemctl status ssh
```

## Example Output

```text
● ssh.service - OpenBSD Secure Shell server
     Active: active (running)
```

---

# 83. Check SSH Configuration

## Command

```bash
sudo sshd -t
```

## Example Output

```text
```

No output generally means the configuration syntax is valid.

---

# 84. Display SSH Configuration

## Command

```bash
sudo grep -vE '^\s*#|^\s*$' /etc/ssh/sshd_config
```

## Example Output

```text
Port 22
PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes
```

---

# 85. Check SSH Port

## Command

```bash
sudo ss -ltnp | grep ':22'
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:22 users:(("sshd",pid=1234))
```

---

# 86. Test SSH Connection

## Command

```bash
ssh user@192.168.1.100
```

## Example Output

```text
user@192.168.1.100's password:
```

---

# 87. Test SSH With Verbose Output

## Command

```bash
ssh -v user@192.168.1.100
```

## Example Output

```text
OpenSSH_9.x
debug1: Connecting to 192.168.1.100 port 22.
debug1: Connection established.
```

---

# 88. Test SSH With Maximum Debugging

## Command

```bash
ssh -vvv user@192.168.1.100
```

## Example Output

```text
debug1: Connecting to 192.168.1.100 port 22.
debug1: Offering public key
debug1: Server accepts key
```

---

# 89. Generate SSH Key

## Command

```bash
ssh-keygen -t ed25519
```

## Example Output

```text
Generating public/private ed25519 key pair.
Enter file in which to save the key:
/home/devops/.ssh/id_ed25519
```

---

# 90. Display SSH Public Key

## Command

```bash
cat ~/.ssh/id_ed25519.pub
```

## Example Output

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAA... devops@server
```

---

# 91. Copy SSH Key to Remote Server

## Command

```bash
ssh-copy-id user@192.168.1.100
```

## Example Output

```text
Number of key(s) added: 1
```

---

# 92. Check SSH Directory Permissions

## Command

```bash
ls -ld ~/.ssh
```

## Example Output

```text
drwx------ 2 devops devops 4096 Aug 27 10:00 /home/devops/.ssh
```

---

# 93. Check SSH Private Key Permissions

## Command

```bash
ls -l ~/.ssh/id_ed25519
```

## Example Output

```text
-rw------- 1 devops devops 411 Aug 27 10:00 id_ed25519
```

---

# 94. Set SSH Directory Permissions

## Command

```bash
chmod 700 ~/.ssh
```

## Example Output

```text
```

---

# 95. Set SSH Private Key Permissions

## Command

```bash
chmod 600 ~/.ssh/id_ed25519
```

## Example Output

```text
```

---

# 96. Set SSH Public Key Permissions

## Command

```bash
chmod 644 ~/.ssh/id_ed25519.pub
```

## Example Output

```text
```

---

# 97. Set authorized_keys Permissions

## Command

```bash
chmod 600 ~/.ssh/authorized_keys
```

## Example Output

```text
```

---

# 98. Disable SSH Root Login

## Command

```bash
sudo grep -E '^PermitRootLogin' /etc/ssh/sshd_config
```

## Example Output

```text
PermitRootLogin no
```

After changing SSH configuration:

```bash
sudo sshd -t
sudo systemctl reload ssh
```

---

# 99. Check Password Authentication

## Command

```bash
sudo sshd -T | grep passwordauthentication
```

## Example Output

```text
passwordauthentication yes
```

---

# 100. Check Public Key Authentication

## Command

```bash
sudo sshd -T | grep pubkeyauthentication
```

## Example Output

```text
pubkeyauthentication yes
```

---

# 101. Check SSH Root Login Setting

## Command

```bash
sudo sshd -T | grep permitrootlogin
```

## Example Output

```text
permitrootlogin no
```

---

# 102. Check SSH Authentication Logs

## Command

```bash
sudo journalctl -u ssh
```

## Example Output

```text
Accepted publickey for devops from 192.168.1.50
Failed password for invalid user test from 192.168.1.100
```

---

# 103. Find Failed SSH Login Attempts

## Command

```bash
sudo journalctl -u ssh | grep -i "failed"
```

## Example Output

```text
Failed password for invalid user admin from 192.168.1.100
```

---

# 104. Find Successful SSH Logins

## Command

```bash
sudo journalctl -u ssh | grep -i "accepted"
```

## Example Output

```text
Accepted publickey for devops from 192.168.1.50
```

---

# 105. Display Firewall Status

## Command

```bash
sudo ufw status
```

## Example Output

```text
Status: active

To                         Action      From
22/tcp                     ALLOW       Anywhere
80/tcp                     ALLOW       Anywhere
443/tcp                    ALLOW       Anywhere
```

---

# 106. Display Detailed Firewall Status

## Command

```bash
sudo ufw status verbose
```

## Example Output

```text
Status: active
Logging: on
Default: deny (incoming), allow (outgoing)
```

---

# 107. Display Numbered Firewall Rules

## Command

```bash
sudo ufw status numbered
```

## Example Output

```text
[ 1] 22/tcp ALLOW IN Anywhere
[ 2] 80/tcp ALLOW IN Anywhere
[ 3] 443/tcp ALLOW IN Anywhere
```

---

# 108. Allow SSH

## Command

```bash
sudo ufw allow 22/tcp
```

## Example Output

```text
Rule added
Rule added (v6)
```

---

# 109. Allow HTTP

## Command

```bash
sudo ufw allow 80/tcp
```

## Example Output

```text
Rule added
Rule added (v6)
```

---

# 110. Allow HTTPS

## Command

```bash
sudo ufw allow 443/tcp
```

## Example Output

```text
Rule added
Rule added (v6)
```

---

# 111. Deny Specific Port

## Command

```bash
sudo ufw deny 8080/tcp
```

## Example Output

```text
Rule added
Rule added (v6)
```

---

# 112. Delete Firewall Rule

## Command

```bash
sudo ufw delete deny 8080/tcp
```

## Example Output

```text
Rule deleted
Rule deleted (v6)
```

---

# 113. Enable Firewall

## Command

```bash
sudo ufw enable
```

## Example Output

```text
Firewall is active and enabled on system startup
```

Be careful when enabling UFW remotely. Ensure SSH is allowed first.

---

# 114. Disable Firewall

## Command

```bash
sudo ufw disable
```

## Example Output

```text
Firewall stopped and disabled on system startup
```

---

# 115. Check iptables Rules

## Command

```bash
sudo iptables -L -n -v
```

## Example Output

```text
Chain INPUT (policy ACCEPT)
target     prot opt source      destination
ACCEPT     tcp  --  0.0.0.0/0   0.0.0.0/0  tcp dpt:22
```

---

# 116. Display iptables With Line Numbers

## Command

```bash
sudo iptables -L -n --line-numbers
```

## Example Output

```text
num  target  prot source       destination
1    ACCEPT  tcp  0.0.0.0/0    0.0.0.0/0 tcp dpt:22
```

---

# 117. Display NAT Rules

## Command

```bash
sudo iptables -t nat -L -n -v
```

## Example Output

```text
Chain PREROUTING
Chain POSTROUTING
Chain OUTPUT
```

---

# 118. Display nftables Rules

## Command

```bash
sudo nft list ruleset
```

## Example Output

```text
table inet filter {
    chain input {
        type filter hook input priority filter;
    }
}
```

---

# 119. Check nftables Service

## Command

```bash
sudo systemctl status nftables
```

## Example Output

```text
● nftables.service
     Active: active (exited)
```

---

# 120. Check AppArmor Status

## Command

```bash
sudo aa-status
```

## Example Output

```text
apparmor module is loaded.
10 profiles are loaded.
8 profiles are in enforce mode.
```

---

# 121. List AppArmor Profiles

## Command

```bash
sudo aa-status --profiled
```

## Example Output

```text
/usr/sbin/cupsd
/usr/sbin/sshd
/usr/sbin/nginx
```

---

# 122. Check AppArmor Processes

## Command

```bash
sudo aa-status --processes
```

## Example Output

```text
1234 /usr/sbin/sshd
1500 /usr/sbin/nginx
```

---

# 123. Display AppArmor Profiles

## Command

```bash
ls /etc/apparmor.d/
```

## Example Output

```text
usr.sbin.sshd
usr.sbin.nginx
usr.sbin.cupsd
```

---

# 124. Check Security Events in Kernel Logs

## Command

```bash
sudo dmesg | grep -i -E 'apparmor|audit|denied'
```

## Example Output

```text
apparmor="DENIED" operation="open" profile="/usr/sbin/nginx"
```

---

# 125. Check Audit Service

## Command

```bash
sudo systemctl status auditd
```

## Example Output

```text
● auditd.service
     Active: active (running)
```

---

# 126. Display Audit Logs

## Command

```bash
sudo ausearch -m USER_LOGIN
```

## Example Output

```text
type=USER_LOGIN msg=audit(...) uid=1000
```

---

# 127. Search Failed Login Audit Events

## Command

```bash
sudo ausearch -m USER_LOGIN --success no
```

## Example Output

```text
type=USER_LOGIN msg=audit(...) res=failed
```

---

# 128. Search File Access Audit Events

## Command

```bash
sudo ausearch -m PATH
```

## Example Output

```text
type=PATH msg=audit(...)
name="/etc/passwd"
```

---

# 129. Display Audit Summary

## Command

```bash
sudo aureport
```

## Example Output

```text
Authentication Report
======================
total auth attempts: 120
```

---

# 130. Display Login Authentication Report

## Command

```bash
sudo aureport -au
```

## Example Output

```text
Authentication Report
success  failed  acct
100      20      devops
```

---

# 131. Search Authentication Logs

## Command

```bash
sudo journalctl _SYSTEMD_UNIT=ssh.service
```

## Example Output

```text
Accepted publickey for devops
Failed password for invalid user admin
```

---

# 132. Display Security-Related Journal Logs

## Command

```bash
sudo journalctl | grep -i -E 'authentication|failed|denied|sudo'
```

## Example Output

```text
sudo: devops : TTY=pts/0 ; COMMAND=/usr/bin/systemctl status ssh
Failed password for invalid user admin
```

---

# 133. Display sudo Logs

## Command

```bash
sudo journalctl | grep sudo
```

## Example Output

```text
sudo: devops : COMMAND=/usr/bin/apt update
```

---

# 134. Display Authentication Log

## Command

```bash
sudo tail -f /var/log/auth.log
```

## Example Output

```text
sshd[1234]: Accepted publickey for devops
sudo: devops : COMMAND=/usr/bin/systemctl status nginx
```

Press `Ctrl+C` to exit.

---

# 135. Search Failed Authentication

## Command

```bash
sudo grep -i "failed" /var/log/auth.log
```

## Example Output

```text
Failed password for invalid user admin from 192.168.1.100
```

---

# 136. Search Successful Authentication

## Command

```bash
sudo grep -i "accepted" /var/log/auth.log
```

## Example Output

```text
Accepted publickey for devops from 192.168.1.50
```

---

# 137. Count Failed SSH Attempts

## Command

```bash
sudo grep -i "failed password" /var/log/auth.log | wc -l
```

## Example Output

```text
25
```

---

# 138. Find Invalid SSH Users

## Command

```bash
sudo grep -i "invalid user" /var/log/auth.log
```

## Example Output

```text
Invalid user admin from 192.168.1.100
Invalid user test from 192.168.1.101
```

---

# 139. Find Top Source IPs From Failed SSH Attempts

## Command

```bash
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
```

## Example Output

```text
25 192.168.1.100
15 192.168.1.101
10 10.10.10.50
```

---

# 140. Check Running Processes

## Command

```bash
ps aux
```

## Example Output

```text
USER       PID %CPU %MEM COMMAND
root         1  0.0  0.1 /sbin/init
devops    2451  0.1  1.2 python3 app.py
```

---

# 141. Find Root-Owned Processes

## Command

```bash
ps -U root -u root u
```

## Example Output

```text
USER PID %CPU %MEM COMMAND
root   1  0.0  0.1 /sbin/init
root 900  0.0  0.2 /usr/sbin/sshd
```

---

# 142. Find Processes Listening on Network Ports

## Command

```bash
sudo ss -lntup
```

## Example Output

```text
tcp LISTEN 0 128 0.0.0.0:22 users:(("sshd",pid=900))
tcp LISTEN 0 511 0.0.0.0:80 users:(("nginx",pid=1500))
```

---

# 143. Find Process Using Specific Port

## Command

```bash
sudo lsof -i :8080
```

## Example Output

```text
COMMAND  PID USER  FD TYPE DEVICE NODE NAME
python3 2451 devops 3u IPv4 TCP *:8080 (LISTEN)
```

---

# 144. Find Deleted Files Still Open

## Command

```bash
sudo lsof +L1
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NLINK NAME
python  2451 devops 4w REG 8,1 524288000 0 /var/log/app.log (deleted)
```

Deleted-but-open files can continue consuming disk space.

---

# 145. Check Process Capabilities

## Command

```bash
sudo getcap /usr/bin/ping
```

## Example Output

```text
/usr/bin/ping cap_net_raw=ep
```

---

# 146. Find Files With Linux Capabilities

## Command

```bash
sudo getcap -r / 2>/dev/null
```

## Example Output

```text
/usr/bin/ping cap_net_raw=ep
```

---

# 147. Display File Capabilities

## Command

```bash
getcap /usr/bin/ping
```

## Example Output

```text
/usr/bin/ping cap_net_raw=ep
```

---

# 148. Check Kernel Security Parameters

## Command

```bash
sysctl -a 2>/dev/null | grep -E 'kernel|net.ipv4'
```

## Example Output

```text
kernel.randomize_va_space = 2
net.ipv4.ip_forward = 0
net.ipv4.tcp_syncookies = 1
```

---

# 149. Check ASLR

## Command

```bash
cat /proc/sys/kernel/randomize_va_space
```

## Example Output

```text
2
```

Common values:

```text
0 = Disabled
1 = Partial randomization
2 = Full randomization
```

---

# 150. Check IP Forwarding

## Command

```bash
sysctl net.ipv4.ip_forward
```

## Example Output

```text
net.ipv4.ip_forward = 0
```

---

# 151. Check TCP SYN Cookies

## Command

```bash
sysctl net.ipv4.tcp_syncookies
```

## Example Output

```text
net.ipv4.tcp_syncookies = 1
```

---

# 152. Check Reverse Path Filtering

## Command

```bash
sysctl net.ipv4.conf.all.rp_filter
```

## Example Output

```text
net.ipv4.conf.all.rp_filter = 2
```

---

# 153. Check Kernel Hardening Parameters

## Command

```bash
sysctl -a 2>/dev/null | grep -E 'randomize_va_space|dmesg_restrict|kptr_restrict'
```

## Example Output

```text
kernel.randomize_va_space = 2
kernel.dmesg_restrict = 1
kernel.kptr_restrict = 2
```

---

# 154. Check Kernel Version

## Command

```bash
uname -r
```

## Example Output

```text
6.8.0-40-generic
```

---

# 155. Display Kernel Information

## Command

```bash
uname -a
```

## Example Output

```text
Linux devops-server 6.8.0-40-generic x86_64 GNU/Linux
```

---

# 156. Check Operating System Version

## Command

```bash
cat /etc/os-release
```

## Example Output

```text
NAME="Ubuntu"
VERSION="24.04.3 LTS (Noble Numbat)"
```

---

# 157. Check Security Updates

## Command

```bash
apt list --upgradable
```

## Example Output

```text
Listing...
openssl/noble-security 3.x
openssh-server/noble-security 1:9.x
```

---

# 158. Check Installed OpenSSH Version

## Command

```bash
ssh -V
```

## Example Output

```text
OpenSSH_9.xp1 Ubuntu-3ubuntu13
```

---

# 159. Check Installed OpenSSL Version

## Command

```bash
openssl version
```

## Example Output

```text
OpenSSL 3.0.x
```

---

# 160. Update Package Information

## Command

```bash
sudo apt update
```

## Example Output

```text
Reading package lists... Done
```

---

# 161. Upgrade Security Packages

## Command

```bash
sudo apt upgrade
```

## Example Output

```text
The following packages will be upgraded:
  openssh-server openssl
```

---

# 162. Check Unattended Upgrades

## Command

```bash
systemctl status unattended-upgrades
```

## Example Output

```text
● unattended-upgrades.service
     Active: active (running)
```

---

# 163. Display Unattended Upgrade Configuration

## Command

```bash
sudo cat /etc/apt/apt.conf.d/20auto-upgrades
```

## Example Output

```text
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
```

---

# 164. Check Services Running as Root

## Command

```bash
ps -eo user,pid,cmd | awk '$1=="root"'
```

## Example Output

```text
root 1 /sbin/init
root 900 /usr/sbin/sshd
root 1500 nginx: master process
```

---

# 165. Check Enabled Services

## Command

```bash
systemctl list-unit-files --type=service --state=enabled
```

## Example Output

```text
ssh.service enabled
nginx.service enabled
docker.service enabled
```

---

# 166. Find Failed Services

## Command

```bash
systemctl --failed
```

## Example Output

```text
UNIT              LOAD   ACTIVE SUB    DESCRIPTION
example.service   loaded failed failed Example Service
```

---

# 167. Check Running Services

## Command

```bash
systemctl list-units --type=service --state=running
```

## Example Output

```text
ssh.service
nginx.service
docker.service
```

---

# 168. Check Service Status

## Command

```bash
sudo systemctl status nginx
```

## Example Output

```text
● nginx.service
     Active: active (running)
```

---

# 169. Check Service Logs

## Command

```bash
sudo journalctl -u nginx
```

## Example Output

```text
nginx[1500]: server started
```

---

# 170. Check Recent Security Logs

## Command

```bash
sudo journalctl --since "1 hour ago" | grep -i -E 'failed|denied|authentication|sudo'
```

## Example Output

```text
Failed password for invalid user admin
sudo: devops : COMMAND=/usr/bin/systemctl status nginx
```

---

# 171. Check File Integrity Using sha256sum

## Command

```bash
sha256sum file.txt
```

## Example Output

```text
3a7bd3e2360a3d29...  file.txt
```

---

# 172. Generate SHA512 Hash

## Command

```bash
sha512sum file.txt
```

## Example Output

```text
cf83e1357eefb8bd...  file.txt
```

---

# 173. Verify SHA256 Checksum

## Command

```bash
sha256sum -c checksum.sha256
```

## Example Output

```text
file.txt: OK
```

---

# 174. Generate MD5 Hash

## Command

```bash
md5sum file.txt
```

## Example Output

```text
d41d8cd98f00b204e9800998ecf8427e  file.txt
```

MD5 should not be used for security-sensitive integrity or cryptographic purposes.

---

# 175. Generate Random Data

## Command

```bash
openssl rand -hex 32
```

## Example Output

```text
7c4a8d09ca3762af61e59520943dc264
```

---

# 176. Generate Random Base64 Data

## Command

```bash
openssl rand -base64 32
```

## Example Output

```text
mK8dR5Y9n2vLx7Q3pA1sB8cD0eF4gH6j
```

---

# 177. Encrypt File Using GPG

## Command

```bash
gpg -c secret.txt
```

## Example Output

```text
Enter passphrase:
```

Creates:

```text
secret.txt.gpg
```

---

# 178. Decrypt GPG File

## Command

```bash
gpg -d secret.txt.gpg
```

## Example Output

```text
Sensitive information
```

---

# 179. Encrypt File Using OpenSSL

## Command

```bash
openssl enc -aes-256-cbc -salt -in secret.txt -out secret.enc
```

## Example Output

```text
enter AES-256-CBC encryption password:
```

---

# 180. Decrypt OpenSSL File

## Command

```bash
openssl enc -d -aes-256-cbc -in secret.enc -out secret.txt
```

## Example Output

```text
enter AES-256-CBC decryption password:
```

---

# 181. Check TLS Certificate

## Command

```bash
echo | openssl s_client -connect google.com:443 2>/dev/null | openssl x509 -noout -subject -issuer -dates
```

## Example Output

```text
subject=CN=*.google.com
issuer=CN=WE1
notBefore=Aug 01 00:00:00 2026 GMT
notAfter=Oct 24 23:59:59 2026 GMT
```

---

# 182. Check TLS Connection

## Command

```bash
openssl s_client -connect google.com:443
```

## Example Output

```text
CONNECTED
Protocol: TLSv1.3
Verify return code: 0 (ok)
```

---

# 183. Check HTTPS Headers

## Command

```bash
curl -I https://example.com
```

## Example Output

```text
HTTP/2 200
content-type: text/html
strict-transport-security: max-age=31536000
```

---

# 184. Check HTTP Security Headers

## Command

```bash
curl -sI https://example.com
```

## Example Output

```text
HTTP/2 200
strict-transport-security: max-age=31536000
x-content-type-options: nosniff
x-frame-options: SAMEORIGIN
```

---

# 185. Check HSTS Header

## Command

```bash
curl -sI https://example.com | grep -i strict-transport-security
```

## Example Output

```text
strict-transport-security: max-age=31536000
```

---

# 186. Check X-Frame-Options

## Command

```bash
curl -sI https://example.com | grep -i x-frame-options
```

## Example Output

```text
x-frame-options: SAMEORIGIN
```

---

# 187. Check Content Security Policy

## Command

```bash
curl -sI https://example.com | grep -i content-security-policy
```

## Example Output

```text
content-security-policy: default-src 'self'
```

---

# 188. Check Content Type Protection

## Command

```bash
curl -sI https://example.com | grep -i x-content-type-options
```

## Example Output

```text
x-content-type-options: nosniff
```

---

# 189. Check Open Network Connections

## Command

```bash
ss -tunap
```

## Example Output

```text
ESTAB 0 0 192.168.1.100:22 192.168.1.50:53214 users:(("sshd",pid=900))
```

---

# 190. Check Listening Ports

## Command

```bash
sudo ss -lntup
```

## Example Output

```text
tcp LISTEN 0 128 0.0.0.0:22
tcp LISTEN 0 511 0.0.0.0:80
tcp LISTEN 0 511 0.0.0.0:443
```

---

# 191. Find Services Exposed on All Interfaces

## Command

```bash
sudo ss -lntup | grep '0.0.0.0'
```

## Example Output

```text
tcp LISTEN 0 128 0.0.0.0:22
tcp LISTEN 0 511 0.0.0.0:80
```

Services listening on `0.0.0.0` may be reachable from all network interfaces.

---

# 192. Find Processes Using Network

## Command

```bash
sudo lsof -i
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NODE NAME
sshd 900 root 3u IPv4 TCP *:22 (LISTEN)
nginx 1500 root 6u IPv4 TCP *:80 (LISTEN)
```

---

# 193. Check Network Interface

## Command

```bash
ip -br addr
```

## Example Output

```text
lo    UNKNOWN 127.0.0.1/8
eth0  UP      192.168.1.100/24
```

---

# 194. Check Network Route

## Command

```bash
ip route
```

## Example Output

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0
```

---

# 195. Capture Network Packets

## Command

```bash
sudo tcpdump -i eth0
```

## Example Output

```text
IP 192.168.1.100.22 > 192.168.1.50.53214: Flags [P.]
```

Press `Ctrl+C` to stop.

---

# 196. Capture SSH Traffic

## Command

```bash
sudo tcpdump -i eth0 tcp port 22
```

## Example Output

```text
IP 192.168.1.50.53214 > 192.168.1.100.22: Flags [S]
```

---

# 197. Capture HTTP Traffic

## Command

```bash
sudo tcpdump -i eth0 tcp port 80
```

## Example Output

```text
IP 192.168.1.100.50000 > 192.168.1.100.80: Flags [S]
```

---

# 198. Capture HTTPS Traffic

## Command

```bash
sudo tcpdump -i eth0 tcp port 443
```

## Example Output

```text
IP 192.168.1.100.50000 > 142.250.183.14.443: Flags [S]
```

---

# 199. Capture ICMP Traffic

## Command

```bash
sudo tcpdump -i eth0 icmp
```

## Example Output

```text
IP 192.168.1.100 > 8.8.8.8: ICMP echo request
IP 8.8.8.8 > 192.168.1.100: ICMP echo reply
```

---

# 200. Save Network Capture

## Command

```bash
sudo tcpdump -i eth0 -w security.pcap
```

## Example Output

```text
tcpdump: listening on eth0
```

---

# 201. Read Packet Capture

## Command

```bash
sudo tcpdump -r security.pcap
```

## Example Output

```text
IP 192.168.1.100.22 > 192.168.1.50.53214
```

---

# 202. Check File Access Time

## Command

```bash
stat file.txt
```

## Example Output

```text
Access: 2026-08-27 10:00:00
Modify: 2026-08-27 09:55:00
Change: 2026-08-27 09:55:00
```

---

# 203. Find Recently Modified Files

## Command

```bash
find /etc -type f -mtime -1 2>/dev/null
```

## Example Output

```text
/etc/ssh/sshd_config
/etc/passwd
```

---

# 204. Find Recently Modified Files in Last Hour

## Command

```bash
find /etc -type f -mmin -60 2>/dev/null
```

## Example Output

```text
/etc/ssh/sshd_config
```

---

# 205. Find Recently Created or Modified Files

## Command

```bash
find /var/log -type f -mmin -30 2>/dev/null
```

## Example Output

```text
/var/log/auth.log
/var/log/syslog
```

---

# 206. Find Files Owned by Root

## Command

```bash
sudo find /etc -user root -type f
```

## Example Output

```text
/etc/passwd
/etc/shadow
/etc/ssh/sshd_config
```

---

# 207. Find Files Owned by Specific User

## Command

```bash
sudo find /home -user devops -type f
```

## Example Output

```text
/home/devops/app/config.yaml
/home/devops/script.sh
```

---

# 208. Find Files With No Owner

## Command

```bash
sudo find / -nouser 2>/dev/null
```

## Example Output

```text
/opt/application/unknown-file
```

---

# 209. Find Files With No Group

## Command

```bash
sudo find / -nogroup 2>/dev/null
```

## Example Output

```text
/opt/application/file.txt
```

---

# 210. Check /etc/passwd Integrity

## Command

```bash
sudo pwck
```

## Example Output

```text
user 'devops': directory '/home/devops' does not exist
```

No output generally means no detected problems.

---

# 211. Check Group File Integrity

## Command

```bash
sudo grpck
```

## Example Output

```text
```

---

# 212. Check Password Aging

## Command

```bash
sudo chage -l devops
```

## Example Output

```text
Last password change : Aug 01, 2026
Password expires     : Nov 01, 2026
Account expires      : never
```

---

# 213. Set Password Expiration

## Command

```bash
sudo chage -M 90 devops
```

## Example Output

```text
```

---

# 214. Set Minimum Password Age

## Command

```bash
sudo chage -m 1 devops
```

## Example Output

```text
```

---

# 215. Set Password Warning Period

## Command

```bash
sudo chage -W 7 devops
```

## Example Output

```text
```

---

# 216. Force Password Change

## Command

```bash
sudo chage -d 0 devops
```

## Example Output

```text
```

---

# 217. Check Password Hash Storage

## Command

```bash
sudo grep '^devops:' /etc/shadow
```

## Example Output

```text
devops:$y$j9T$...:...
```

Do not expose `/etc/shadow` contents in logs, screenshots, or repositories.

---

# 218. Check Root SSH Login Attempts

## Command

```bash
sudo grep -i "root" /var/log/auth.log | grep ssh
```

## Example Output

```text
Failed password for root from 192.168.1.100
```

---

# 219. Check Invalid User Attempts

## Command

```bash
sudo grep -i "invalid user" /var/log/auth.log | tail
```

## Example Output

```text
Invalid user admin from 192.168.1.100
Invalid user ubuntu from 192.168.1.101
```

---

# 220. Count Invalid User Attempts

## Command

```bash
sudo grep -i "invalid user" /var/log/auth.log | wc -l
```

## Example Output

```text
42
```

---

# 221. Check sudo Command History

## Command

```bash
sudo journalctl | grep 'sudo:'
```

## Example Output

```text
sudo: devops : COMMAND=/usr/bin/systemctl restart nginx
sudo: devops : COMMAND=/usr/bin/docker ps
```

---

# 222. Check Security-Relevant Kernel Messages

## Command

```bash
sudo dmesg --level=err,warn
```

## Example Output

```text
kernel: device warning
kernel: security module loaded
```

---

# 223. Check Kernel Audit Messages

## Command

```bash
sudo dmesg | grep -i audit
```

## Example Output

```text
audit: initializing netlink subsys
```

---

# 224. Check AppArmor Denials

## Command

```bash
sudo journalctl | grep -i apparmor | grep -i denied
```

## Example Output

```text
apparmor="DENIED" operation="open" profile="/usr/sbin/nginx"
```

---

# 225. Check System Boot Security Logs

## Command

```bash
sudo journalctl -b | grep -i -E 'security|apparmor|audit'
```

## Example Output

```text
AppArmor: AppArmor initialized
audit: initializing
```

---

# 226. Check World-Readable Sensitive Files

## Command

```bash
sudo find /etc -type f -perm -004 2>/dev/null
```

## Example Output

```text
/etc/passwd
/etc/group
```

---

# 227. Check World-Writable Configuration Files

## Command

```bash
sudo find /etc -type f -perm -002 2>/dev/null
```

## Example Output

```text
/etc/example.conf
```

---

# 228. Check SUID Binaries in Common Locations

## Command

```bash
sudo find /usr/bin /usr/sbin -type f -perm -4000 2>/dev/null
```

## Example Output

```text
/usr/bin/passwd
/usr/bin/sudo
/usr/bin/su
```

---

# 229. Check SGID Binaries

## Command

```bash
sudo find /usr/bin /usr/sbin -type f -perm -2000 2>/dev/null
```

## Example Output

```text
/usr/bin/wall
```

---

# 230. Check Security Capabilities

## Command

```bash
sudo getcap -r /usr/bin /usr/sbin 2>/dev/null
```

## Example Output

```text
/usr/bin/ping cap_net_raw=ep
```

---

# 231. Check File ACLs Recursively

## Command

```bash
getfacl -R application/
```

## Example Output

```text
# file: application/config.yaml
user::rw-
group::r--
other::---
```

---

# 232. Check SSH Known Hosts

## Command

```bash
cat ~/.ssh/known_hosts
```

## Example Output

```text
192.168.1.100 ssh-ed25519 AAAAC3...
```

---

# 233. Scan SSH Host Key

## Command

```bash
ssh-keyscan 192.168.1.100
```

## Example Output

```text
192.168.1.100 ssh-ed25519 AAAAC3...
```

Verify host keys through a trusted channel before accepting them.

---

# 234. Check SSH Supported Algorithms

## Command

```bash
ssh -Q cipher
```

## Example Output

```text
aes128-ctr
aes256-ctr
chacha20-poly1305@openssh.com
```

---

# 235. Check SSH MAC Algorithms

## Command

```bash
ssh -Q mac
```

## Example Output

```text
hmac-sha2-256
hmac-sha2-512
```

---

# 236. Check SSH Key Types

## Command

```bash
ssh -Q key
```

## Example Output

```text
ssh-ed25519
ssh-rsa
ecdsa-sha2-nistp256
```

---

# 237. Check SSH Effective Configuration

## Command

```bash
sudo sshd -T
```

## Example Output

```text
port 22
permitrootlogin no
pubkeyauthentication yes
passwordauthentication no
```

---

# 238. Check SSH Configuration for Security Settings

## Command

```bash
sudo sshd -T | grep -E 'permitrootlogin|passwordauthentication|pubkeyauthentication|maxauthtries|x11forwarding'
```

## Example Output

```text
permitrootlogin no
passwordauthentication no
pubkeyauthentication yes
maxauthtries 3
x11forwarding no
```

---

# 239. Check Maximum SSH Authentication Attempts

## Command

```bash
sudo sshd -T | grep maxauthtries
```

## Example Output

```text
maxauthtries 3
```

---

# 240. Check SSH X11 Forwarding

## Command

```bash
sudo sshd -T | grep x11forwarding
```

## Example Output

```text
x11forwarding no
```

---

# 241. Check SSH TCP Forwarding

## Command

```bash
sudo sshd -T | grep allowtcpforwarding
```

## Example Output

```text
allowtcpforwarding yes
```

Review whether forwarding is actually required in your environment.

---

# 242. Check SSH LoginGraceTime

## Command

```bash
sudo sshd -T | grep logingracetime
```

## Example Output

```text
logingracetime 120
```

---

# 243. Check SSH Max Sessions

## Command

```bash
sudo sshd -T | grep maxsessions
```

## Example Output

```text
maxsessions 10
```

---

# 244. Check Firewall Logging

## Command

```bash
sudo ufw status verbose
```

## Example Output

```text
Logging: on (low)
```

---

# 245. Enable Firewall Logging

## Command

```bash
sudo ufw logging on
```

## Example Output

```text
Logging enabled
```

---

# 246. Check Firewall Logs

## Command

```bash
sudo journalctl -k | grep UFW
```

## Example Output

```text
UFW BLOCK IN=eth0 SRC=192.168.1.100 DST=192.168.1.200 DPT=8080
```

---

# 247. Monitor Authentication Logs Continuously

## Command

```bash
sudo tail -f /var/log/auth.log
```

## Example Output

```text
sshd[1234]: Accepted publickey for devops
```

Press `Ctrl+C` to exit.

---

# 248. Monitor Security Journal Continuously

## Command

```bash
sudo journalctl -f
```

## Example Output

```text
Aug 27 10:30:00 server sshd[1234]: Accepted publickey
```

Press `Ctrl+C` to exit.

---

# 249. Check Disk Space for Security Logs

## Command

```bash
df -h /var/log
```

## Example Output

```text
Filesystem Size Used Avail Use% Mounted on
/dev/sda2   99G  25G   69G  27% /
```

---

# 250. Check Journal Disk Usage

## Command

```bash
journalctl --disk-usage
```

## Example Output

```text
Archived and active journals take up 250.0M in the file system.
```

---

# 251. Check Login History

## Command

```bash
last -n 20
```

## Example Output

```text
devops pts/0 192.168.1.50 Thu Aug 27 09:20 still logged in
```

---

# 252. Check Failed Login History

## Command

```bash
sudo lastb -n 20
```

## Example Output

```text
admin pts/1 192.168.1.100 Thu Aug 27 08:30 - 08:30
```

---

# 253. Check Currently Logged-In Users

## Command

```bash
users
```

## Example Output

```text
devops
```

---

# 254. Check Login Sessions

## Command

```bash
loginctl list-sessions
```

## Example Output

```text
SESSION UID USER SEAT TTY
1      1000 devops     pts/0
```

---

# 255. Display User Session Details

## Command

```bash
loginctl show-session 1
```

## Example Output

```text
Id=1
User=1000
Name=devops
Remote=yes
```

---

# 256. Terminate User Session

## Command

```bash
sudo loginctl terminate-user devuser
```

## Example Output

```text
```

Use carefully because this terminates all sessions belonging to the user.

---

# 257. Check Loginctl User Status

## Command

```bash
loginctl user-status devops
```

## Example Output

```text
devops (1000)
Since: Thu 2026-08-27 09:20
State: active
```

---

# 258. Check Secure Boot Status

## Command

```bash
mokutil --sb-state
```

## Example Output

```text
SecureBoot enabled
```

---

# 259. Check TPM Device

## Command

```bash
ls -l /dev/tpm*
```

## Example Output

```text
crw-rw---- 1 tss root 10, 224 /dev/tpm0
```

---

# 260. Check Kernel Modules

## Command

```bash
lsmod
```

## Example Output

```text
Module       Size Used by
overlay      151552 1
bridge       307200 1
```

---

# 261. Check Loaded Security Modules

## Command

```bash
cat /sys/kernel/security/lsm
```

## Example Output

```text
landlock,lockdown,yama,integrity,apparmor
```

---

# 262. Check Yama Security Setting

## Command

```bash
cat /proc/sys/kernel/yama/ptrace_scope
```

## Example Output

```text
1
```

---

# 263. Check Kernel Lockdown Mode

## Command

```bash
cat /sys/kernel/security/lockdown
```

## Example Output

```text
none [integrity] confidentiality
```

The active mode is shown in brackets.

---

# 264. Check Secure Kernel Boot Parameters

## Command

```bash
cat /proc/cmdline
```

## Example Output

```text
BOOT_IMAGE=/vmlinuz root=/dev/sda2 ro quiet splash
```

---

# 265. Check Process Namespace Information

## Command

```bash
lsns
```

## Example Output

```text
NS         TYPE   NPROCS PID USER COMMAND
4026531837 mnt    120    1 root /sbin/init
4026531834 pid    120    1 root /sbin/init
```

---

# 266. Check Container Processes

## Command

```bash
ps aux | grep -E 'docker|containerd'
```

## Example Output

```text
root 900 /usr/bin/containerd
root 1200 /usr/bin/dockerd
```

---

# 267. Check Docker Socket Permissions

## Command

```bash
ls -l /var/run/docker.sock
```

## Example Output

```text
srw-rw---- 1 root docker 0 Aug 27 10:00 /var/run/docker.sock
```

Access to the Docker socket can provide root-equivalent control of the host.

---

# 268. Check Docker Group Membership

## Command

```bash
getent group docker
```

## Example Output

```text
docker:x:999:devops
```

---

# 269. Check File Security Context

## Command

```bash
ls -Z file.txt
```

## Example Output

```text
-rw-r--r-- devops devops unconfined_u:object_r:user_home_t:s0 file.txt
```

---

# 270. Display Security Context of Process

## Command

```bash
ps -eZ
```

## Example Output

```text
LABEL                 PID TTY CMD
unconfined_u:...      123 pts/0 bash
```

---

# 271. Check SELinux Status If Installed

## Command

```bash
getenforce
```

## Example Output

```text
Enforcing
```

Ubuntu commonly uses AppArmor instead of SELinux by default.

---

# 272. Display SELinux Status If Installed

## Command

```bash
sestatus
```

## Example Output

```text
SELinux status:                 enabled
Current mode:                   enforcing
```

---

# 273. Search Security Configuration Files

## Command

```bash
sudo find /etc -maxdepth 2 -type f \( -name '*security*' -o -name '*ssh*' \)
```

## Example Output

```text
/etc/security/limits.conf
/etc/ssh/sshd_config
```

---

# 274. Check PAM Configuration

## Command

```bash
ls -l /etc/pam.d/
```

## Example Output

```text
-rw-r--r-- 1 root root common-auth
-rw-r--r-- 1 root root common-account
-rw-r--r-- 1 root root common-password
```

---

# 275. Check Password Policy

## Command

```bash
grep -vE '^\s*#|^\s*$' /etc/security/pwquality.conf
```

## Example Output

```text
minlen = 12
minclass = 3
```

---

# 276. Check Login Definitions

## Command

```bash
grep -vE '^\s*#|^\s*$' /etc/login.defs
```

## Example Output

```text
PASS_MAX_DAYS 90
PASS_MIN_DAYS 1
PASS_WARN_AGE 7
```

---

# 277. Check Password Hash Algorithm Configuration

## Command

```bash
grep -E '^ENCRYPT_METHOD' /etc/login.defs
```

## Example Output

```text
ENCRYPT_METHOD SHA512
```

---

# 278. Check Resource Limits

## Command

```bash
ulimit -a
```

## Example Output

```text
open files                      1024
max user processes              63467
stack size              8192 kbytes
```

---

# 279. Check Open File Limit

## Command

```bash
ulimit -n
```

## Example Output

```text
1024
```

---

# 280. Check Maximum User Processes

## Command

```bash
ulimit -u
```

## Example Output

```text
63467
```

---

# 281. Check Login Shell Restrictions

## Command

```bash
cat /etc/shells
```

## Example Output

```text
/bin/sh
/bin/bash
/usr/bin/bash
/usr/sbin/nologin
```

---

# 282. Find Users With Dangerous Login Shells

## Command

```bash
awk -F: '$7 !~ /(nologin|false)$/ {print $1,$7}' /etc/passwd
```

## Example Output

```text
root /bin/bash
devops /bin/bash
```

---

# 283. Check Cron Jobs

## Command

```bash
crontab -l
```

## Example Output

```text
0 2 * * * /home/devops/backup.sh
```

---

# 284. Check Root Cron Jobs

## Command

```bash
sudo crontab -l
```

## Example Output

```text
0 3 * * * /usr/local/bin/backup.sh
```

---

# 285. Check System Cron Jobs

## Command

```bash
sudo ls -la /etc/cron.d/
```

## Example Output

```text
backup
logrotate
```

---

# 286. Find Writable Cron Files

## Command

```bash
sudo find /etc/cron* -type f -writable -ls
```

## Example Output

```text
/etc/cron.d/example
```

Review unexpected writable cron files carefully.

---

# 287. Check Systemd Timers

## Command

```bash
systemctl list-timers
```

## Example Output

```text
NEXT                         LEFT LAST PASSED UNIT
Thu 2026-08-27 12:00:00      1h   11:00 1h   apt-daily.timer
```

---

# 288. Find World-Writable Systemd Files

## Command

```bash
sudo find /etc/systemd /usr/lib/systemd -type f -perm -0002 2>/dev/null
```

## Example Output

```text
```

Unexpected results should be investigated.

---

# 289. Check PATH Security

## Command

```bash
echo "$PATH"
```

## Example Output

```text
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

---

# 290. Find Current Directory in PATH

## Command

```bash
echo "$PATH" | tr ':' '\n' | grep -x '\.'
```

## Example Output

```text
```

Avoid placing `.` in privileged PATH values.

---

# 291. Check Sudo Environment

## Command

```bash
sudo env | sort
```

## Example Output

```text
HOME=/root
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
USER=root
```

---

# 292. Check Sudo Secure Path

## Command

```bash
sudo -V | grep -i secure_path
```

## Example Output

```text
Value to override user's PATH with: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

---

# 293. Find SSH Authorized Keys

## Command

```bash
find /home -name authorized_keys -type f 2>/dev/null
```

## Example Output

```text
/home/devops/.ssh/authorized_keys
/home/admin/.ssh/authorized_keys
```

---

# 294. Check Authorized Keys Permissions

## Command

```bash
sudo find /home -name authorized_keys -exec ls -l {} \; 2>/dev/null
```

## Example Output

```text
-rw------- 1 devops devops 400 Aug 27 10:00 /home/devops/.ssh/authorized_keys
```

---

# 295. Find Private SSH Keys

## Command

```bash
sudo find /home -type f \( -name 'id_rsa' -o -name 'id_ed25519' -o -name 'id_ecdsa' \) 2>/dev/null
```

## Example Output

```text
/home/devops/.ssh/id_ed25519
```

Protect private keys and never commit them to Git repositories.

---

# 296. Find Files Named .env

## Command

```bash
find / -name ".env" -type f 2>/dev/null
```

## Example Output

```text
/opt/application/.env
/home/devops/project/.env
```

---

# 297. Check .env File Permissions

## Command

```bash
ls -l .env
```

## Example Output

```text
-rw------- 1 devops devops 500 Aug 27 10:00 .env
```

---

# 298. Search for Private Keys

## Command

```bash
sudo find / -type f \( -name "*.pem" -o -name "id_rsa" -o -name "id_ed25519" \) 2>/dev/null
```

## Example Output

```text
/home/devops/.ssh/id_ed25519
/opt/app/server.pem
```

---

# 299. Check Git Repository for Secrets

## Command

```bash
git status --short
```

## Example Output

```text
 M application/config.yaml
?? .env
```

Never commit passwords, API keys, private keys, or tokens.

---

# 300. Search Configuration for Common Secret Names

## Command

```bash
grep -RniE 'password|secret|api[_-]?key|token|private[_-]?key' . 2>/dev/null
```

## Example Output

```text
./config.yaml:12:api_key: REDACTED
./application.env:5:password: REDACTED
```

Use this carefully and avoid exposing actual secrets in terminal history or logs.

---

# 301. Check Shell History

## Command

```bash
history
```

## Example Output

```text
1001 sudo systemctl restart nginx
1002 docker ps
1003 ssh user@server
```

---

# 302. Search Shell History for Password Commands

## Command

```bash
history | grep -Ei 'password|passwd'
```

## Example Output

```text
1020 passwd devuser
```

Avoid entering secrets directly on command lines because they may appear in history or process listings.

---

# 303. Check Bash History File Permissions

## Command

```bash
ls -l ~/.bash_history
```

## Example Output

```text
-rw------- 1 devops devops 5000 Aug 27 10:00 /home/devops/.bash_history
```

---

# 304. Check Environment Variables

## Command

```bash
env
```

## Example Output

```text
USER=devops
HOME=/home/devops
PATH=/usr/local/bin:/usr/bin:/bin
```

Do not expose environments containing secrets.

---

# 305. Search Environment for Potential Secrets

## Command

```bash
env | grep -Ei 'key|token|secret|password'
```

## Example Output

```text
API_KEY=REDACTED
```

---

# 306. Check Mounted Filesystems

## Command

```bash
findmnt
```

## Example Output

```text
TARGET SOURCE    FSTYPE OPTIONS
/      /dev/sda2 ext4   rw,relatime
```

---

# 307. Find Writable Mounts

## Command

```bash
findmnt -o TARGET,OPTIONS | grep rw
```

## Example Output

```text
/ rw,relatime
/home rw,relatime
```

---

# 308. Check Mount Options

## Command

```bash
findmnt -no TARGET,OPTIONS /
```

## Example Output

```text
/ rw,relatime
```

For sensitive filesystems, options such as `nosuid`, `nodev`, and `noexec` may be appropriate depending on the workload.

---

# 309. Check /tmp Mount Configuration

## Command

```bash
findmnt /tmp
```

## Example Output

```text
TARGET SOURCE FSTYPE OPTIONS
/tmp   tmpfs  tmpfs  rw,nosuid,nodev,noexec
```

---

# 310. Check Security Updates From Ubuntu

## Command

```bash
ubuntu-security-status
```

## Example Output

```text
This system is not attached to an Ubuntu Pro subscription.
```

Output depends on the Ubuntu version and configuration.

---

# 311. Check Installed Packages

## Command

```bash
dpkg -l
```

## Example Output

```text
ii  openssh-server  1:9.x  amd64  secure shell server
ii  openssl         3.x    amd64  Secure Sockets Layer toolkit
```

---

# 312. Check Specific Package

## Command

```bash
dpkg -l openssh-server
```

## Example Output

```text
ii  openssh-server  1:9.x  amd64  secure shell server
```

---

# 313. Check Package Installation Files

## Command

```bash
dpkg -L openssh-server
```

## Example Output

```text
/etc/ssh/sshd_config
/usr/sbin/sshd
/usr/share/man/man8/sshd.8.gz
```

---

# 314. Check Package Integrity

## Command

```bash
sudo debsums -s
```

## Example Output

```text
```

Install `debsums` if required:

```bash
sudo apt install debsums
```

---

# 315. Check Rootkit Scanner If Installed

## Command

```bash
sudo rkhunter --check
```

## Example Output

```text
System checks summary
=====================
File properties checks: OK
Rootkits checks: OK
```

Use security scanners as additional signals, not as proof that a system is clean.

---

# 316. Check ClamAV Status If Installed

## Command

```bash
sudo systemctl status clamav-daemon
```

## Example Output

```text
● clamav-daemon.service
     Active: active (running)
```

---

# 317. Scan Directory Using ClamAV

## Command

```bash
clamscan -r /home/devops
```

## Example Output

```text
Known viruses: 8600000
Scanned files: 1200
Infected files: 0
```

---

# 318. Check Fail2ban Status If Installed

## Command

```bash
sudo fail2ban-client status
```

## Example Output

```text
Status
|- Number of jail: 1
`- Jail list: sshd
```

---

# 319. Check Fail2ban SSH Jail

## Command

```bash
sudo fail2ban-client status sshd
```

## Example Output

```text
Status for the jail: sshd
|- Currently failed: 2
|- Currently banned: 1
`- Banned IP list: 192.168.1.100
```

---

# 320. Check Security Service Status

## Command

```bash
systemctl list-units --type=service | grep -Ei 'audit|apparmor|fail2ban|ufw'
```

## Example Output

```text
apparmor.service loaded active exited
auditd.service loaded active running
ufw.service loaded active exited
```

---

# 🧪 Practical Linux Security Audit Flow

## Command

```bash
whoami
id
groups
sudo -l
last -n 10
sudo lastb -n 10
sudo ss -lntup
sudo ufw status verbose
sudo systemctl --failed
sudo aa-status
sudo journalctl --since "1 hour ago" | grep -i -E 'failed|denied|authentication|sudo'
sudo find / -type f -perm -4000 2>/dev/null
sudo find / -type f -perm -0002 2>/dev/null
sudo getcap -r / 2>/dev/null
```

## Example Output

```text
Current User       → devops
User Groups        → sudo docker
Sudo Permissions   → Allowed commands
Login History      → Recent sessions
Failed Logins      → Authentication failures
Listening Ports    → 22, 80, 443
Firewall           → Active
Failed Services    → None
AppArmor            → Enforcing
Security Logs      → Reviewed
SUID Files         → Reviewed
World-Writable     → Reviewed
Capabilities       → Reviewed
```

---

# 🧪 SSH Security Audit Flow

## Command

```bash
sudo sshd -t
sudo sshd -T | grep -E 'permitrootlogin|passwordauthentication|pubkeyauthentication|maxauthtries|x11forwarding'
sudo ss -lntp | grep ':22'
sudo journalctl -u ssh --since "24 hours ago"
sudo grep -i "failed password" /var/log/auth.log
sudo grep -i "accepted" /var/log/auth.log
```

## Example Output

```text
SSH Configuration → Valid
Root Login         → Disabled
Password Login     → Disabled
Public Key         → Enabled
Max Auth Attempts  → 3
X11 Forwarding     → Disabled
SSH Port           → 22
Failed Attempts    → Reviewed
Successful Logins  → Reviewed
```

---

# 🧪 File Permission Security Audit

## Command

```bash
ls -la
find . -type f -perm -0002
find . -type f -perm -4000
find . -type f -perm -2000
getfacl file.txt
stat file.txt
```

## Example Output

```text
World-Writable Files → Reviewed
SUID Files           → Reviewed
SGID Files           → Reviewed
ACL                  → Reviewed
Ownership            → Reviewed
Permissions          → Reviewed
```

---

# 🧪 User Security Audit

## Command

```bash
cut -d: -f1 /etc/passwd
grep -vE '/nologin|/false' /etc/passwd
sudo passwd -S -a
sudo chage -l devops
sudo getent group sudo
sudo getent group docker
```

## Example Output

```text
Users                  → Listed
Interactive Users      → Reviewed
Locked Accounts        → Reviewed
Password Expiration    → Reviewed
Sudo Members           → Reviewed
Docker Group Members   → Reviewed
```

---

# 🧪 Network Security Audit

## Command

```bash
ip -br addr
ip route
sudo ss -lntup
sudo lsof -i
sudo ufw status numbered
sudo nft list ruleset
```

## Example Output

```text
Interfaces       → eth0
IP Address       → 192.168.1.100
Default Gateway  → 192.168.1.1
Listening Ports  → 22, 80, 443
Network Processes → sshd, nginx
Firewall Rules   → Reviewed
nftables Rules   → Reviewed
```

---

# 🧪 Log Security Audit

## Command

```bash
sudo journalctl --since "24 hours ago"
sudo journalctl -u ssh --since "24 hours ago"
sudo grep -i "failed" /var/log/auth.log
sudo grep -i "accepted" /var/log/auth.log
sudo grep -i "sudo" /var/log/auth.log
sudo journalctl | grep -i "denied"
```

## Example Output

```text
SSH Failures       → Reviewed
SSH Successes      → Reviewed
sudo Activity      → Reviewed
Access Denials     → Reviewed
System Events      → Reviewed
```

---

# 🧪 Production Security Troubleshooting Flow

## Command

```bash
# 1. Identify current user
whoami

# 2. Check privileges
id
sudo -l

# 3. Check active sessions
who
w
last -n 10

# 4. Check failed logins
sudo lastb -n 20

# 5. Check listening services
sudo ss -lntup

# 6. Check firewall
sudo ufw status verbose

# 7. Check SSH security
sudo sshd -T | grep -E 'permitrootlogin|passwordauthentication|pubkeyauthentication'

# 8. Check failed SSH attempts
sudo grep -i "failed" /var/log/auth.log

# 9. Check successful SSH logins
sudo grep -i "accepted" /var/log/auth.log

# 10. Check security logs
sudo journalctl --since "1 hour ago" | grep -i -E 'failed|denied|authentication|sudo'

# 11. Check AppArmor
sudo aa-status

# 12. Check SUID files
sudo find / -type f -perm -4000 2>/dev/null

# 13. Check world-writable files
sudo find / -type f -perm -0002 2>/dev/null

# 14. Check capabilities
sudo getcap -r / 2>/dev/null

# 15. Check recent file modifications
sudo find /etc -type f -mmin -60 2>/dev/null
```

## Example Output

```text
User Identity       → Verified
Privileges          → Verified
Sessions            → Reviewed
Failed Logins       → Reviewed
Open Ports          → Reviewed
Firewall            → Verified
SSH Configuration  → Verified
Authentication Logs → Reviewed
AppArmor            → Verified
SUID Files          → Reviewed
Writable Files      → Reviewed
Capabilities        → Reviewed
Recent Changes      → Reviewed
```

---

# 📚 Linux Security Commands Summary

## Command

```bash
whoami
id
groups
who
w
last
lastb
lastlog
loginctl
sudo
visudo
passwd
chage
useradd
usermod
userdel
groupadd
groupdel
getent
chmod
chown
chgrp
stat
getfacl
setfacl
find
ps
ss
lsof
systemctl
journalctl
ufw
iptables
nft
tcpdump
ssh
ssh-keygen
ssh-copy-id
sshd
openssl
gpg
sha256sum
sysctl
dmesg
aa-status
ausearch
aureport
auditctl
apt
dpkg
crontab
findmnt
mokutil
lsmod
getcap
setcap
```

## Example Output

```text
User Management
Access Control
File Permissions
Ownership
ACL
Sudo Security
SSH Security
Firewall Management
Network Security
Process Security
Service Security
Authentication Monitoring
Audit Logging
AppArmor
Kernel Security
Cryptographic Verification
Encryption
Package Security
System Hardening
Security Auditing
Incident Troubleshooting
```

---

# 🔐 Important Linux Security Files

## Command

```text
/etc/passwd
/etc/shadow
/etc/group
/etc/gshadow
/etc/sudoers
/etc/sudoers.d/
/etc/ssh/sshd_config
/etc/ssh/ssh_config
/etc/ssh/ssh_host_*_key
/etc/pam.d/
/etc/security/
/etc/login.defs
/etc/security/pwquality.conf
/etc/apparmor/
/etc/apparmor.d/
/var/log/auth.log
/var/log/syslog
/var/log/kern.log
/var/log/audit/
/var/lib/fail2ban/
```

## Example Output

```text
/etc/passwd              → User account information
/etc/shadow              → Password hashes and aging
/etc/group               → Group information
/etc/gshadow             → Secure group information
/etc/sudoers             → Sudo configuration
/etc/ssh/sshd_config     → SSH server configuration
/etc/pam.d/              → Authentication configuration
/etc/security/           → Security policies
/etc/login.defs          → Login/password defaults
/etc/apparmor.d/         → AppArmor profiles
/var/log/auth.log        → Authentication logs
/var/log/audit/          → Audit logs
```

---

# 🔑 Important Linux Permission Values

## Command

```text
400   Owner read
200   Owner write
100   Owner execute

040   Group read
020   Group write
010   Group execute

004   Other read
002   Other write
001   Other execute
```

## Example Output

```text
644 → rw-r--r--
755 → rwxr-xr-x
700 → rwx------
600 → rw-------
640 → rw-r-----
```

---

# 🔑 Special Linux Permission Bits

## Command

```text
4000  SUID
2000  SGID
1000  Sticky Bit
```

## Example Output

```text
SUID       → Program executes with file owner's privileges
SGID       → Program/directory uses group privileges
Sticky Bit → Users generally cannot delete other users' files in shared directories
```

---

# 🌐 Important Security Ports

## Command

```text
20      FTP Data
21      FTP
22      SSH
23      Telnet
25      SMTP
53      DNS
67      DHCP Server
68      DHCP Client
80      HTTP
110     POP3
123     NTP
143     IMAP
389     LDAP
443     HTTPS
445     SMB
465     SMTPS
587     SMTP Submission
636     LDAPS
993     IMAPS
995     POP3S
3306    MySQL
5432    PostgreSQL
6379    Redis
8080    HTTP Alternative
8443    HTTPS Alternative
9090    Prometheus
```

## Example Output

```text
22      → SSH
53      → DNS
80      → HTTP
443     → HTTPS
445     → SMB
3306    → MySQL
5432    → PostgreSQL
6379    → Redis
```

---

# 🎯 DevOps Security Interview Commands

## Command

```bash
whoami
id
sudo -l
ls -l
stat file.txt
chmod 600 secret.txt
chown user:group file.txt
getfacl file.txt
find / -perm -4000 2>/dev/null
find / -perm -0002 2>/dev/null
ps aux
sudo ss -lntup
sudo lsof -i :8080
sudo ufw status
sudo iptables -L -n -v
sudo nft list ruleset
sudo systemctl --failed
sudo journalctl -u ssh
sudo grep -i failed /var/log/auth.log
sudo lastb
sudo aa-status
sudo ausearch -m USER_LOGIN
sudo getcap -r / 2>/dev/null
sudo sshd -T
ssh -v user@server
ssh-keygen -t ed25519
openssl s_client -connect example.com:443
sha256sum file.txt
sysctl net.ipv4.ip_forward
cat /proc/sys/kernel/randomize_va_space
```

## Example Output

```text
Identity            → whoami / id
Privileges          → sudo -l
Permissions         → ls / chmod / stat
Ownership           → chown
ACL                 → getfacl
SUID                → find -perm -4000
World-Writable      → find -perm -0002
Processes           → ps
Network Ports       → ss
Port Owner          → lsof
Firewall            → ufw / nftables
Failed Services     → systemctl
Authentication      → journalctl / auth.log
Failed Logins       → lastb
AppArmor            → aa-status
Audit               → ausearch
Capabilities        → getcap
SSH Security        → sshd -T
SSH Debugging       → ssh -v
Encryption           → openssl / gpg
Integrity           → sha256sum
Kernel Hardening    → sysctl
ASLR                → randomize_va_space
```

---

# 🛡️ Linux Security Best Practices

## Command

```bash
# Check SSH configuration
sudo sshd -t

# Check firewall
sudo ufw status verbose

# Check listening ports
sudo ss -lntup

# Check failed logins
sudo lastb -n 20

# Check authentication failures
sudo grep -i "failed" /var/log/auth.log

# Check root login configuration
sudo sshd -T | grep permitrootlogin

# Check password authentication
sudo sshd -T | grep passwordauthentication

# Check AppArmor
sudo aa-status

# Check SUID files
sudo find / -type f -perm -4000 2>/dev/null

# Check world-writable files
sudo find / -type f -perm -0002 2>/dev/null

# Check file capabilities
sudo getcap -r / 2>/dev/null

# Check failed services
systemctl --failed

# Check security updates
apt list --upgradable
```

## Example Output

```text
SSH Configuration      → Valid
Firewall               → Active
Open Ports             → Reviewed
Failed Logins          → Reviewed
Root Login             → Disabled
Password Authentication → Disabled
AppArmor               → Active
SUID Files             → Reviewed
Writable Files         → Reviewed
Capabilities           → Reviewed
Failed Services        → None
Security Updates       → Reviewed
```

---

# 🚨 Security Incident Investigation Checklist

## Command

```bash
# Identify current user
whoami
id

# Identify logged-in users
who
w

# Review login history
last -n 50

# Review failed logins
sudo lastb -n 50

# Review SSH failures
sudo grep -i "failed password" /var/log/auth.log

# Review successful SSH logins
sudo grep -i "accepted" /var/log/auth.log

# Review sudo activity
sudo journalctl | grep sudo

# Review listening ports
sudo ss -lntup

# Review active network connections
sudo ss -tunap

# Review processes
ps auxf

# Review recent file modifications
sudo find /etc -type f -mmin -1440 2>/dev/null

# Review SUID files
sudo find / -type f -perm -4000 2>/dev/null

# Review world-writable files
sudo find / -type f -perm -0002 2>/dev/null

# Review file capabilities
sudo getcap -r / 2>/dev/null

# Review AppArmor denials
sudo journalctl | grep -i apparmor | grep -i denied

# Review audit logs
sudo ausearch -m USER_LOGIN

# Review firewall
sudo ufw status verbose

# Review system services
systemctl --failed

# Review kernel messages
sudo dmesg --level=err,warn
```

## Example Output

```text
1. User Identity          → Verified
2. Active Sessions        → Reviewed
3. Login History          → Reviewed
4. Failed Authentication  → Reviewed
5. Successful Logins      → Reviewed
6. sudo Activity          → Reviewed
7. Network Ports          → Reviewed
8. Active Connections     → Reviewed
9. Running Processes      → Reviewed
10. Recent File Changes   → Reviewed
11. SUID Files            → Reviewed
12. Writable Files        → Reviewed
13. Capabilities          → Reviewed
14. AppArmor              → Reviewed
15. Audit Logs            → Reviewed
16. Firewall              → Reviewed
17. Services              → Reviewed
18. Kernel Logs           → Reviewed
```

---

# 🏆 Production Security Quick Reference

## Command

```bash
# Current identity
whoami
id

# Privileges
sudo -l

# Users
who
w
last
sudo lastb

# SSH configuration
sudo sshd -t
sudo sshd -T

# SSH listening port
sudo ss -lntp | grep ':22'

# Network listening ports
sudo ss -lntup

# Process using port
sudo lsof -i :8080

# Firewall
sudo ufw status verbose

# nftables
sudo nft list ruleset

# Authentication logs
sudo tail -f /var/log/auth.log

# Security journal
sudo journalctl --since "1 hour ago"

# Failed authentication
sudo grep -i failed /var/log/auth.log

# AppArmor
sudo aa-status

# Audit
sudo ausearch -m USER_LOGIN

# SUID
sudo find / -type f -perm -4000 2>/dev/null

# SGID
sudo find / -type f -perm -2000 2>/dev/null

# World-writable
sudo find / -type f -perm -0002 2>/dev/null

# Capabilities
sudo getcap -r / 2>/dev/null

# Recent changes
sudo find /etc -type f -mmin -60 2>/dev/null

# Kernel security
sysctl -a 2>/dev/null | grep -E 'randomize|dmesg_restrict|kptr_restrict'

# File integrity
sha256sum file.txt

# TLS certificate
echo | openssl s_client -connect example.com:443 2>/dev/null | openssl x509 -noout -dates

# Security updates
apt list --upgradable
```

## Example Output

```text
Identity        → whoami / id
Privileges      → sudo -l
Users           → who / last
SSH             → sshd -T
Ports           → ss
Processes       → ps / lsof
Firewall        → ufw / nft
Authentication  → auth.log
AppArmor        → aa-status
Audit           → ausearch
SUID/SGID       → find
Capabilities    → getcap
File Integrity  → sha256sum
TLS             → openssl
Kernel Security → sysctl
Updates         → apt
```

---

# 📌 Linux Security Learning Path

## Command

```text
Level 1  → Users and Groups
Level 2  → File Permissions
Level 3  → Ownership
Level 4  → Sudo
Level 5  → ACL
Level 6  → SSH Security
Level 7  → Firewall
Level 8  → Network Security
Level 9  → Process Security
Level 10 → Service Security
Level 11 → Authentication Logs
Level 12 → Auditd
Level 13 → AppArmor
Level 14 → Kernel Hardening
Level 15 → File Integrity
Level 16 → Encryption
Level 17 → TLS Security
Level 18 → Security Monitoring
Level 19 → Incident Investigation
Level 20 → Production Security Troubleshooting
```

## Example Output

```text
Beginner
   ↓
Users
   ↓
Permissions
   ↓
Sudo
   ↓
SSH
   ↓
Firewall
   ↓
Logs
   ↓
AppArmor
   ↓
Audit
   ↓
Kernel Hardening
   ↓
Incident Response
   ↓
Production DevOps Security
```

---

# 🎯 DevOps Security Skills Practiced

## Command

```bash
chmod
chown
chgrp
getfacl
setfacl
sudo
visudo
passwd
chage
useradd
usermod
userdel
groupadd
ssh
ssh-keygen
sshd
ss
lsof
ufw
iptables
nft
tcpdump
systemctl
journalctl
last
lastb
loginctl
aa-status
ausearch
aureport
auditctl
getcap
setcap
sysctl
dmesg
openssl
gpg
sha256sum
find
stat
apt
dpkg
```

## Example Output

```text
Linux User Security
Linux Access Control
Linux File Security
Linux SSH Hardening
Linux Firewall Management
Linux Network Security
Linux Process Security
Linux Service Security
Linux Authentication Monitoring
Linux Audit Logging
Linux AppArmor
Linux Kernel Hardening
Linux Encryption
Linux TLS Security
Linux File Integrity
Linux Package Security
Linux Incident Investigation
Linux Production Security
```

---

# ✅ Learning Outcome

## Command

```bash
whoami
id
sudo -l
chmod
chown
getfacl
ssh
sshd
ss
lsof
ufw
nft
journalctl
last
lastb
aa-status
ausearch
getcap
sysctl
openssl
gpg
sha256sum
find
```

## Example Output

```text
By completing this topic, you should be able to:

- Understand Linux users and groups
- Identify user and group IDs
- Manage Linux users securely
- Manage Linux groups
- Understand Linux permissions
- Configure file ownership
- Use ACLs for fine-grained access control
- Configure sudo permissions
- Audit sudo access
- Secure SSH access
- Configure SSH key authentication
- Troubleshoot SSH authentication
- Disable unnecessary SSH access
- Configure firewall rules
- Analyze listening ports
- Identify processes using ports
- Monitor authentication logs
- Investigate failed login attempts
- Review successful login activity
- Understand SUID and SGID
- Identify world-writable files
- Review Linux capabilities
- Monitor AppArmor
- Analyze audit logs
- Review system services
- Check kernel security parameters
- Verify file integrity
- Understand encryption
- Inspect TLS certificates
- Check security updates
- Investigate suspicious activity
- Perform Linux security audits
- Troubleshoot production security issues
- Apply DevOps security best practices
```

---

# 🚀 Final Security Checklist

## Command

```bash
# Identity
whoami
id

# Privileges
sudo -l

# Users
who
last
sudo lastb

# Permissions
ls -l
stat file.txt
getfacl file.txt

# Ownership
ls -ln
chown

# SUID / SGID
sudo find / -type f -perm -4000 2>/dev/null
sudo find / -type f -perm -2000 2>/dev/null

# Writable files
sudo find / -type f -perm -0002 2>/dev/null

# SSH
sudo sshd -t
sudo sshd -T

# Ports
sudo ss -lntup

# Firewall
sudo ufw status verbose

# Authentication logs
sudo grep -i failed /var/log/auth.log
sudo grep -i accepted /var/log/auth.log

# Security logs
sudo journalctl --since "1 hour ago"

# AppArmor
sudo aa-status

# Audit
sudo ausearch -m USER_LOGIN

# Capabilities
sudo getcap -r / 2>/dev/null

# Kernel security
sysctl net.ipv4.ip_forward
cat /proc/sys/kernel/randomize_va_space

# File integrity
sha256sum file.txt

# TLS
openssl s_client -connect example.com:443

# Updates
apt list --upgradable
```

## Example Output

```text
Identity             → Verified
Privileges           → Reviewed
Users                → Reviewed
Permissions          → Secure
Ownership            → Verified
SUID/SGID            → Audited
Writable Files       → Audited
SSH                  → Hardened
Open Ports           → Audited
Firewall             → Active
Authentication Logs  → Reviewed
Security Logs        → Reviewed
AppArmor             → Active
Auditd               → Reviewed
Capabilities         → Audited
Kernel Security      → Reviewed
File Integrity       → Verified
TLS                  → Verified
Security Updates     → Reviewed
```

---

