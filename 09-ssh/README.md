# 📌 SSH (Secure Shell) — Beginner to Advanced
---

# 1. Check SSH Client Version

## Command

```bash
ssh -V
```

## Example Output

```text
OpenSSH_9.6p1 Ubuntu-3ubuntu13.14, OpenSSL 3.0.13
```

`ssh -V` displays the installed OpenSSH client version.

---

# 2. Check SSH Server Version

## Command

```bash
sudo sshd -V
```

## Example Output

```text
OpenSSH_9.6p1, OpenSSL 3.0.13
```

> `sshd -V` may print the version to stderr.

---

# 3. Check SSH Service Status

## Command

```bash
sudo systemctl status ssh
```

## Example Output

```text
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded
     Active: active (running)
```

---

# 4. Start SSH Service

## Command

```bash
sudo systemctl start ssh
```

## Example Output

```text
```

---

# 5. Stop SSH Service

## Command

```bash
sudo systemctl stop ssh
```

## Example Output

```text
```

> Be careful when stopping SSH on a remote server because your SSH connection may be disconnected.

---

# 6. Restart SSH Service

## Command

```bash
sudo systemctl restart ssh
```

## Example Output

```text
```

---

# 7. Reload SSH Configuration

## Command

```bash
sudo systemctl reload ssh
```

## Example Output

```text
```

`reload` applies configuration changes without completely stopping the SSH service.

---

# 8. Enable SSH Service at Boot

## Command

```bash
sudo systemctl enable ssh
```

## Example Output

```text
Synchronizing state of ssh.service with SysV service script
```

---

# 9. Disable SSH Service at Boot

## Command

```bash
sudo systemctl disable ssh
```

## Example Output

```text
Removed "/etc/systemd/system/sshd.service"
```

---

# 10. Check Whether SSH Is Enabled

## Command

```bash
systemctl is-enabled ssh
```

## Example Output

```text
enabled
```

---

# 11. Check Whether SSH Is Running

## Command

```bash
systemctl is-active ssh
```

## Example Output

```text
active
```

---

# 12. Check SSH Service Logs

## Command

```bash
sudo journalctl -u ssh
```

## Example Output

```text
Aug 27 10:20:01 server sshd[1234]: Server listening on 0.0.0.0 port 22.
Aug 27 10:21:10 server sshd[1250]: Accepted publickey for devops
```

---

# 13. Check Recent SSH Logs

## Command

```bash
sudo journalctl -u ssh -n 50
```

## Example Output

```text
Accepted publickey for devops
Failed password for root
Connection closed
```

---

# 14. Follow SSH Logs in Real Time

## Command

```bash
sudo journalctl -u ssh -f
```

## Example Output

```text
sshd[2451]: Accepted publickey for devops
sshd[2451]: pam_unix(sshd:session): session opened
```

Press `Ctrl+C` to exit.

---

# 15. Check SSH Listening Port

## Command

```bash
sudo ss -ltnp | grep ':22'
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:22 0.0.0.0:* users:(("sshd",pid=1234,fd=3))
```

---

# 16. Check All SSH Listening Addresses

## Command

```bash
sudo ss -lntp | grep sshd
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:22
LISTEN 0 128 [::]:22
```

---

# 17. Connect to Remote Server

## Command

```bash
ssh username@192.168.1.100
```

## Example Output

```text
The authenticity of host '192.168.1.100' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

---

# 18. Connect Using Hostname

## Command

```bash
ssh devops@server.example.com
```

## Example Output

```text
Welcome to Ubuntu 24.04.3 LTS
devops@server:~$
```

---

# 19. Connect Using IP Address

## Command

```bash
ssh devops@10.10.2.189
```

## Example Output

```text
devops@10.10.2.189's password:
```

---

# 20. Connect Using a Specific SSH Port

## Command

```bash
ssh -p 2222 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
devops@server:~$
```

---

# 21. Connect Using a Specific Private Key

## Command

```bash
ssh -i ~/.ssh/id_ed25519 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu 24.04.3 LTS
devops@server:~$
```

---

# 22. Connect Using PEM Key

## Command

```bash
ssh -i myserver.pem devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
devops@server:~$
```

---

# 23. Specify SSH Username

## Command

```bash
ssh -l devops 10.10.2.189
```

## Example Output

```text
devops@10.10.2.189's password:
```

---

# 24. Execute Remote Command

## Command

```bash
ssh devops@10.10.2.189 "hostname"
```

## Example Output

```text
prod-server
```

---

# 25. Execute Multiple Commands Remotely

## Command

```bash
ssh devops@10.10.2.189 "hostname && uptime && df -h"
```

## Example Output

```text
prod-server
10:30:12 up 20 days, 3 users, load average: 0.12, 0.10, 0.08
Filesystem      Size  Used Avail Use%
/dev/sda2        99G   25G   69G  27%
```

---

# 26. Execute Remote Command With sudo

## Command

```bash
ssh devops@10.10.2.189 "sudo systemctl status nginx"
```

## Example Output

```text
● nginx.service - A high performance web server
     Active: active (running)
```

---

# 27. Run Remote Shell

## Command

```bash
ssh devops@10.10.2.189
```

## Example Output

```text
devops@prod-server:~$
```

---

# 28. Exit SSH Session

## Command

```bash
exit
```

## Example Output

```text
logout
Connection to 10.10.2.189 closed.
```

---

# 29. SSH Verbose Mode

## Command

```bash
ssh -v devops@10.10.2.189
```

## Example Output

```text
OpenSSH_9.6p1
debug1: Connecting to 10.10.2.189 port 22.
debug1: Connection established.
debug1: Offering public key
```

Useful for troubleshooting SSH connection problems.

---

# 30. SSH Very Verbose Mode

## Command

```bash
ssh -vv devops@10.10.2.189
```

## Example Output

```text
debug1: Connecting to 10.10.2.189 port 22.
debug1: Authenticating to 10.10.2.189
debug1: Offering public key
```

---

# 31. SSH Maximum Verbose Mode

## Command

```bash
ssh -vvv devops@10.10.2.189
```

## Example Output

```text
debug1: Connecting to 10.10.2.189 port 22.
debug1: Offering public key
debug2: we sent a publickey packet
debug1: Authentication succeeded
```

Use `-vvv` when diagnosing authentication and connection failures.

---

# 32. Test SSH Port Without Logging In

## Command

```bash
nc -zv 10.10.2.189 22
```

## Example Output

```text
Connection to 10.10.2.189 22 port [tcp/ssh] succeeded!
```

---

# 33. Test SSH Port Using Telnet

## Command

```bash
telnet 10.10.2.189 22
```

## Example Output

```text
Trying 10.10.2.189...
Connected to 10.10.2.189.
Escape character is '^]'.
SSH-2.0-OpenSSH_9.6p1 Ubuntu
```

---

# 34. Generate ED25519 SSH Key

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

# 35. Generate RSA SSH Key

## Command

```bash
ssh-keygen -t rsa -b 4096
```

## Example Output

```text
Generating public/private rsa key pair.
Your identification has been saved in /home/devops/.ssh/id_rsa
```

---

# 36. Generate SSH Key With Comment

## Command

```bash
ssh-keygen -t ed25519 -C "devops@example.com"
```

## Example Output

```text
Generating public/private ed25519 key pair.
Your identification has been saved in /home/devops/.ssh/id_ed25519
```

---

# 37. List SSH Keys

## Command

```bash
ls -la ~/.ssh
```

## Example Output

```text
-rw------- 1 devops devops  464 id_ed25519
-rw-r--r-- 1 devops devops  104 id_ed25519.pub
-rw-r--r-- 1 devops devops  978 known_hosts
```

---

# 38. Display Public SSH Key

## Command

```bash
cat ~/.ssh/id_ed25519.pub
```

## Example Output

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExampleKey devops@example.com
```

---

# 39. Display RSA Public Key

## Command

```bash
cat ~/.ssh/id_rsa.pub
```

## Example Output

```text
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQExampleKey devops@example.com
```

---

# 40. Check SSH Key Fingerprint

## Command

```bash
ssh-keygen -lf ~/.ssh/id_ed25519.pub
```

## Example Output

```text
256 SHA256:ExampleFingerprint devops@example.com (ED25519)
```

---

# 41. Generate Fingerprint for PEM Key

## Command

```bash
ssh-keygen -lf myserver.pem
```

## Example Output

```text
4096 SHA256:ExampleFingerprint user@server (RSA)
```

---

# 42. Change Private Key Passphrase

## Command

```bash
ssh-keygen -p -f ~/.ssh/id_ed25519
```

## Example Output

```text
Enter old passphrase:
Enter new passphrase:
Key has been successfully updated.
```

---

# 43. Copy Public Key to Remote Server

## Command

```bash
ssh-copy-id devops@10.10.2.189
```

## Example Output

```text
Number of key(s) added: 1
Now try logging into the machine with:
ssh 'devops@10.10.2.189'
```

---

# 44. Copy Specific Public Key to Remote Server

## Command

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub devops@10.10.2.189
```

## Example Output

```text
Number of key(s) added: 1
```

---

# 45. Manually Add Public Key

## Command

```bash
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
```

## Example Output

```text
```

> Run this on the destination user's account.

---

# 46. Display Authorized Keys

## Command

```bash
cat ~/.ssh/authorized_keys
```

## Example Output

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExampleKey devops@example.com
```

---

# 47. Check Authorized Keys Permissions

## Command

```bash
ls -ld ~/.ssh
ls -l ~/.ssh/authorized_keys
```

## Example Output

```text
drwx------ 2 devops devops 4096 Aug 27 10:00 /home/devops/.ssh
-rw------- 1 devops devops  104 Aug 27 10:00 authorized_keys
```

---

# 48. Fix SSH Directory Permissions

## Command

```bash
chmod 700 ~/.ssh
```

## Example Output

```text
```

---

# 49. Fix Authorized Keys Permissions

## Command

```bash
chmod 600 ~/.ssh/authorized_keys
```

## Example Output

```text
```

---

# 50. Fix Private Key Permissions

## Command

```bash
chmod 600 ~/.ssh/id_ed25519
```

## Example Output

```text
```

---

# 51. Fix Public Key Permissions

## Command

```bash
chmod 644 ~/.ssh/id_ed25519.pub
```

## Example Output

```text
```

---

# 52. Fix PEM Key Permissions

## Command

```bash
chmod 400 myserver.pem
```

## Example Output

```text
```

---

# 53. Check SSH Key Permissions

## Command

```bash
ls -l ~/.ssh/
```

## Example Output

```text
-rw------- 1 devops devops  464 id_ed25519
-rw-r--r-- 1 devops devops  104 id_ed25519.pub
-rw------- 1 devops devops  104 authorized_keys
```

---

# 54. Use SSH Agent

## Command

```bash
eval "$(ssh-agent -s)"
```

## Example Output

```text
Agent pid 2451
```

---

# 55. Add SSH Key to Agent

## Command

```bash
ssh-add ~/.ssh/id_ed25519
```

## Example Output

```text
Identity added: /home/devops/.ssh/id_ed25519
```

---

# 56. List SSH Agent Keys

## Command

```bash
ssh-add -l
```

## Example Output

```text
256 SHA256:ExampleFingerprint devops@example.com (ED25519)
```

---

# 57. Remove Specific Key From Agent

## Command

```bash
ssh-add -d ~/.ssh/id_ed25519
```

## Example Output

```text
Identity removed: /home/devops/.ssh/id_ed25519
```

---

# 58. Remove All SSH Agent Keys

## Command

```bash
ssh-add -D
```

## Example Output

```text
All identities removed.
```

---

# 59. Check SSH Client Configuration

## Command

```bash
cat ~/.ssh/config
```

## Example Output

```text
Host production
    HostName 10.10.2.189
    User devops
    IdentityFile ~/.ssh/id_ed25519
```

---

# 60. Create SSH Client Configuration

## Command

```bash
vi ~/.ssh/config
```

## Example Configuration

```text
Host production
    HostName 10.10.2.189
    User devops
    Port 22
    IdentityFile ~/.ssh/id_ed25519
```

---

# 61. Connect Using SSH Config Alias

## Command

```bash
ssh production
```

## Example Output

```text
Welcome to Ubuntu
devops@production:~$
```

---

# 62. Check Effective SSH Client Configuration

## Command

```bash
ssh -G production
```

## Example Output

```text
user devops
hostname 10.10.2.189
port 22
identityfile ~/.ssh/id_ed25519
```

---

# 63. Display SSH Server Configuration

## Command

```bash
sudo cat /etc/ssh/sshd_config
```

## Example Output

```text
Port 22
PermitRootLogin prohibit-password
PubkeyAuthentication yes
PasswordAuthentication yes
```

---

# 64. Check SSH Configuration Syntax

## Command

```bash
sudo sshd -t
```

## Example Output

```text
```

No output normally means the configuration syntax is valid.

---

# 65. Check SSH Configuration With Detailed Output

## Command

```bash
sudo sshd -T
```

## Example Output

```text
port 22
pubkeyauthentication yes
passwordauthentication yes
permitrootlogin prohibit-password
```

---

# 66. Check Effective SSH Port

## Command

```bash
sudo sshd -T | grep '^port '
```

## Example Output

```text
port 22
```

---

# 67. Check Password Authentication

## Command

```bash
sudo sshd -T | grep passwordauthentication
```

## Example Output

```text
passwordauthentication yes
```

---

# 68. Check Public Key Authentication

## Command

```bash
sudo sshd -T | grep pubkeyauthentication
```

## Example Output

```text
pubkeyauthentication yes
```

---

# 69. Check Root Login Configuration

## Command

```bash
sudo sshd -T | grep permitrootlogin
```

## Example Output

```text
permitrootlogin prohibit-password
```

---

# 70. Change SSH Port

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
Port 2222
```

After changing the port:

```bash
sudo sshd -t
sudo systemctl reload ssh
```

Then connect using:

```bash
ssh -p 2222 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

> Make sure the firewall allows the new SSH port before closing your existing SSH session.

---

# 71. Disable Root SSH Login

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
PermitRootLogin no
```

Validate and reload:

```bash
sudo sshd -t
sudo systemctl reload ssh
```

---

# 72. Disable Password Authentication

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
PasswordAuthentication no
```

Validate and reload:

```bash
sudo sshd -t
sudo systemctl reload ssh
```

> Ensure key-based authentication works before disabling password authentication.

---

# 73. Enable Public Key Authentication

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
PubkeyAuthentication yes
```

---

# 74. Disable Empty Passwords

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
PermitEmptyPasswords no
```

---

# 75. Limit SSH Users

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
AllowUsers devops admin
```

---

# 76. Allow SSH Group

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
AllowGroups sshusers
```

---

# 77. Deny Specific SSH Users

## Command

```bash
sudo vi /etc/ssh/sshd_config
```

## Example Configuration

```text
DenyUsers testuser
```

---

# 78. Check SSH Host Key Files

## Command

```bash
sudo ls -l /etc/ssh/ssh_host_*
```

## Example Output

```text
-rw------- 1 root root  411 ssh_host_ed25519_key
-rw-r--r-- 1 root root  103 ssh_host_ed25519_key.pub
-rw------- 1 root root 2610 ssh_host_rsa_key
-rw-r--r-- 1 root root  575 ssh_host_rsa_key.pub
```

---

# 79. Display Server Host Key Fingerprint

## Command

```bash
sudo ssh-keygen -lf /etc/ssh/ssh_host_ed25519_key.pub
```

## Example Output

```text
256 SHA256:ExampleFingerprint root@server (ED25519)
```

---

# 80. Check Known Hosts File

## Command

```bash
cat ~/.ssh/known_hosts
```

## Example Output

```text
server.example.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExample
```

---

# 81. Search Known Hosts

## Command

```bash
ssh-keygen -F 10.10.2.189
```

## Example Output

```text
# Host 10.10.2.189 found: line 5
10.10.2.189 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExample
```

---

# 82. Remove Host From Known Hosts

## Command

```bash
ssh-keygen -R 10.10.2.189
```

## Example Output

```text
# Host 10.10.2.189 found: line 5
# Host 10.10.2.189 removed.
```

---

# 83. Add Host Key to Known Hosts

## Command

```bash
ssh-keyscan 10.10.2.189
```

## Example Output

```text
10.10.2.189 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExample
```

---

# 84. Save Host Key Using ssh-keyscan

## Command

```bash
ssh-keyscan 10.10.2.189 >> ~/.ssh/known_hosts
```

## Example Output

```text
```

> Verify host identity through a trusted channel before manually adding keys.

---

# 85. Copy File to Remote Server Using scp

## Command

```bash
scp file.txt devops@10.10.2.189:/home/devops/
```

## Example Output

```text
file.txt                                      100%   25KB  1.2MB/s   00:00
```

---

# 86. Copy File From Remote Server

## Command

```bash
scp devops@10.10.2.189:/home/devops/file.txt .
```

## Example Output

```text
file.txt                                      100%   25KB  1.2MB/s   00:00
```

---

# 87. Copy Directory to Remote Server

## Command

```bash
scp -r myapp/ devops@10.10.2.189:/opt/
```

## Example Output

```text
app.py
requirements.txt
config/
```

---

# 88. Copy Directory From Remote Server

## Command

```bash
scp -r devops@10.10.2.189:/opt/myapp/ .
```

## Example Output

```text
app.py
requirements.txt
config/
```

---

# 89. Copy File Using Specific SSH Key

## Command

```bash
scp -i ~/.ssh/id_ed25519 file.txt devops@10.10.2.189:/home/devops/
```

## Example Output

```text
file.txt 100%
```

---

# 90. Copy File Using Specific SSH Port

## Command

```bash
scp -P 2222 file.txt devops@10.10.2.189:/home/devops/
```

## Example Output

```text
file.txt 100%
```

---

# 91. Copy Multiple Files

## Command

```bash
scp file1.txt file2.txt devops@10.10.2.189:/home/devops/
```

## Example Output

```text
file1.txt 100%
file2.txt 100%
```

---

# 92. Copy Files Using rsync Over SSH

## Command

```bash
rsync -avz -e ssh ./myapp/ devops@10.10.2.189:/opt/myapp/
```

## Example Output

```text
sending incremental file list
app.py
requirements.txt

sent 15,000 bytes
received 500 bytes
```

---

# 93. Dry Run rsync Over SSH

## Command

```bash
rsync -avzn -e ssh ./myapp/ devops@10.10.2.189:/opt/myapp/
```

## Example Output

```text
sending incremental file list
app.py
requirements.txt

sent 500 bytes
received 100 bytes
```

`-n` performs a dry run without changing the destination.

---

# 94. Delete Files From Destination With rsync

## Command

```bash
rsync -avz --delete -e ssh ./myapp/ devops@10.10.2.189:/opt/myapp/
```

## Example Output

```text
deleting old-file.log
app.py
requirements.txt
```

> `--delete` can remove destination files. Use it carefully.

---

# 95. Use SFTP

## Command

```bash
sftp devops@10.10.2.189
```

## Example Output

```text
Connected to 10.10.2.189.
sftp>
```

---

# 96. List Remote Files Using SFTP

## Command

```bash
sftp> ls
```

## Example Output

```text
app.py
backup.tar
logs/
```

---

# 97. Upload File Using SFTP

## Command

```bash
sftp> put file.txt
```

## Example Output

```text
Uploading file.txt to /home/devops/file.txt
```

---

# 98. Download File Using SFTP

## Command

```bash
sftp> get file.txt
```

## Example Output

```text
Fetching /home/devops/file.txt to file.txt
```

---

# 99. Upload Directory Using SFTP

## Command

```bash
sftp> put -r myapp
```

## Example Output

```text
Uploading myapp/ to /home/devops/myapp/
```

---

# 100. Download Directory Using SFTP

## Command

```bash
sftp> get -r myapp
```

## Example Output

```text
Fetching /home/devops/myapp/ to myapp/
```

---

# 101. Display Remote Working Directory in SFTP

## Command

```bash
sftp> pwd
```

## Example Output

```text
Remote working directory: /home/devops
```

---

# 102. Display Local Working Directory in SFTP

## Command

```bash
sftp> lpwd
```

## Example Output

```text
Local working directory: /home/devops
```

---

# 103. Exit SFTP

## Command

```bash
sftp> exit
```

## Example Output

```text
```

---

# 104. SSH Local Port Forwarding

## Command

```bash
ssh -L 8080:localhost:80 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
devops@server:~$
```

This forwards:

```text
Local Port 8080 → Remote Server localhost:80
```

---

# 105. Access Remote Application Through Local Forwarding

## Command

```bash
ssh -L 8080:127.0.0.1:8000 devops@10.10.2.189
```

Then on the local machine:

```bash
curl http://localhost:8080
```

## Example Output

```text
HTTP/1.1 200 OK
```

---

# 106. SSH Remote Port Forwarding

## Command

```bash
ssh -R 8080:localhost:8000 devops@remote-server
```

## Example Output

```text
Welcome to Ubuntu
```

This creates a remote port forwarding tunnel.

---

# 107. SSH Dynamic Port Forwarding

## Command

```bash
ssh -D 1080 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

This creates a SOCKS proxy on local port `1080`.

---

# 108. Run SSH Tunnel in Background

## Command

```bash
ssh -fN -L 8080:localhost:8000 devops@10.10.2.189
```

## Example Output

```text
```

`-fN` runs the SSH tunnel in the background without executing a remote shell.

---

# 109. Check SSH Tunnel

## Command

```bash
ss -ltnp | grep ':8080'
```

## Example Output

```text
LISTEN 0 128 127.0.0.1:8080
```

---

# 110. Close SSH Tunnel

## Command

```bash
pkill -f "ssh -fN -L 8080"
```

## Example Output

```text
```

> Make sure the pattern matches only the intended SSH tunnel.

---

# 111. SSH Jump Host

## Command

```bash
ssh -J bastion@203.0.113.10 devops@10.10.2.189
```

## Example Output

```text
Welcome to internal-server
devops@internal-server:~$
```

---

# 112. SSH Through ProxyJump

## Command

```bash
ssh -o ProxyJump=bastion@203.0.113.10 devops@10.10.2.189
```

## Example Output

```text
Welcome to internal-server
```

---

# 113. SSH ProxyCommand

## Command

```bash
ssh -o ProxyCommand="ssh -W %h:%p bastion@203.0.113.10" devops@10.10.2.189
```

## Example Output

```text
Welcome to internal-server
```

---

# 114. SSH Agent Forwarding

## Command

```bash
ssh -A devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

Check forwarded agent:

```bash
ssh-add -l
```

## Example Output

```text
256 SHA256:ExampleFingerprint devops@example.com (ED25519)
```

> Use agent forwarding carefully and only with trusted hosts.

---

# 115. Disable Host Key Checking for Temporary Testing

## Command

```bash
ssh -o StrictHostKeyChecking=no devops@10.10.2.189
```

## Example Output

```text
Warning: Permanently added '10.10.2.189' to the list of known hosts.
```

> Avoid disabling host key checking in production because it weakens SSH host authentication.

---

# 116. Use Connection Timeout

## Command

```bash
ssh -o ConnectTimeout=10 devops@10.10.2.189
```

## Example Output

```text
Connection timed out
```

---

# 117. Disable Password Authentication for One Connection

## Command

```bash
ssh -o PreferredAuthentications=publickey -o PasswordAuthentication=no devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

---

# 118. Use Specific Identity File

## Command

```bash
ssh -o IdentityFile=~/.ssh/id_ed25519 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

---

# 119. List Available SSH Authentication Methods

## Command

```bash
ssh -v devops@10.10.2.189
```

## Example Output

```text
debug1: Authentications that can continue: publickey,password
```

---

# 120. Check Which SSH Keys Are Offered

## Command

```bash
ssh -vvv devops@10.10.2.189
```

## Example Output

```text
debug1: Offering public key: /home/devops/.ssh/id_ed25519
debug1: Server accepts key
```

---

# 121. Force SSH to Use Only One Key

## Command

```bash
ssh -o IdentitiesOnly=yes -i ~/.ssh/id_ed25519 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

This is useful when multiple keys are loaded into the SSH agent.

---

# 122. Test SSH Authentication Without Opening a Shell

## Command

```bash
ssh -o BatchMode=yes devops@10.10.2.189 "echo SSH_OK"
```

## Example Output

```text
SSH_OK
```

Useful for automation and CI/CD pipelines.

---

# 123. Run SSH With No Remote Command

## Command

```bash
ssh -N devops@10.10.2.189
```

## Example Output

```text
```

Useful for tunnels.

---

# 124. Keep SSH Connection Alive

## Command

```bash
ssh -o ServerAliveInterval=60 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

---

# 125. Configure SSH Keepalive

## Command

```bash
vi ~/.ssh/config
```

## Example Configuration

```text
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

---

# 126. Check SSH Connection Through DNS

## Command

```bash
ssh -v devops@server.example.com
```

## Example Output

```text
debug1: Connecting to server.example.com [10.10.2.189] port 22.
debug1: Connection established.
```

---

# 127. Check SSH Host Key

## Command

```bash
ssh-keyscan -t ed25519 10.10.2.189
```

## Example Output

```text
10.10.2.189 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExample
```

---

# 128. Check SSH Server Algorithms

## Command

```bash
ssh -Q cipher
```

## Example Output

```text
3des-cbc
aes128-ctr
aes192-ctr
aes256-ctr
chacha20-poly1305@openssh.com
```

---

# 129. Display Supported SSH MAC Algorithms

## Command

```bash
ssh -Q mac
```

## Example Output

```text
hmac-sha2-256
hmac-sha2-512
umac-128-etm@openssh.com
```

---

# 130. Display Supported SSH Key Types

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

# 131. Display Supported SSH KEX Algorithms

## Command

```bash
ssh -Q kex
```

## Example Output

```text
curve25519-sha256
diffie-hellman-group14-sha256
```

---

# 132. Check SSH Server Configuration for Security

## Command

```bash
sudo sshd -T | grep -E 'permitrootlogin|passwordauthentication|pubkeyauthentication|permitempty|x11forwarding'
```

## Example Output

```text
permitrootlogin no
passwordauthentication no
pubkeyauthentication yes
permitemptypasswords no
x11forwarding no
```

---

# 133. Check Failed SSH Login Attempts

## Command

```bash
sudo journalctl -u ssh | grep "Failed"
```

## Example Output

```text
Failed password for invalid user admin from 192.168.1.50
Failed password for root from 192.168.1.60
```

---

# 134. Check Successful SSH Logins

## Command

```bash
sudo journalctl -u ssh | grep "Accepted"
```

## Example Output

```text
Accepted publickey for devops from 192.168.1.50
Accepted password for admin from 192.168.1.60
```

---

# 135. Check SSH Login History

## Command

```bash
last
```

## Example Output

```text
devops   pts/0  192.168.1.50  Thu Aug 27 10:20   still logged in
admin    pts/1  192.168.1.60  Thu Aug 27 09:10 - 10:00
```

---

# 136. Check Failed Login History

## Command

```bash
sudo lastb
```

## Example Output

```text
admin    ssh:notty 192.168.1.100 Thu Aug 27 09:20
root     ssh:notty 192.168.1.101 Thu Aug 27 09:15
```

---

# 137. Check Current SSH Sessions

## Command

```bash
who
```

## Example Output

```text
devops   pts/0  2026-08-27 10:20 (192.168.1.50)
admin    pts/1  2026-08-27 10:25 (192.168.1.60)
```

---

# 138. Check Logged-in Users

## Command

```bash
w
```

## Example Output

```text
USER   TTY   FROM           LOGIN@  IDLE  WHAT
devops pts/0 192.168.1.50  10:20   2m    -bash
admin  pts/1 192.168.1.60  10:25   1m    top
```

---

# 139. Find SSH Processes

## Command

```bash
ps aux | grep '[s]sh'
```

## Example Output

```text
root  1234  0.0  sshd: /usr/sbin/sshd
devops 2451 0.0 sshd: devops@pts/0
```

---

# 140. Find SSHD Process

## Command

```bash
pgrep -a sshd
```

## Example Output

```text
1234 /usr/sbin/sshd -D
2451 sshd: devops@pts/0
```

---

# 141. Find Process Listening on SSH Port

## Command

```bash
sudo lsof -i :22
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NODE NAME
sshd    1234 root 3u IPv4 TCP *:ssh (LISTEN)
```

---

# 142. Check SSH Connections With ss

## Command

```bash
sudo ss -tnp | grep ':22'
```

## Example Output

```text
ESTAB 0 0 10.10.2.189:22 10.10.2.50:52314 users:(("sshd",pid=2451))
```

---

# 143. Count Active SSH Connections

## Command

```bash
sudo ss -tn state established '( sport = :22 )' | tail -n +2 | wc -l
```

## Example Output

```text
5
```

---

# 144. Check SSH Firewall Rule

## Command

```bash
sudo ufw status | grep 22
```

## Example Output

```text
22/tcp                   ALLOW       Anywhere
```

---

# 145. Allow SSH Through UFW

## Command

```bash
sudo ufw allow ssh
```

## Example Output

```text
Rule added
Rule added (v6)
```

---

# 146. Allow SSH Port 22 Explicitly

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

# 147. Allow Custom SSH Port

## Command

```bash
sudo ufw allow 2222/tcp
```

## Example Output

```text
Rule added
Rule added (v6)
```

---

# 148. Check SSH Server Configuration Before Reload

## Command

```bash
sudo sshd -t && echo "SSH configuration OK"
```

## Example Output

```text
SSH configuration OK
```

---

# 149. Reload SSH Safely

## Command

```bash
sudo sshd -t && sudo systemctl reload ssh
```

## Example Output

```text
```

---

# 150. Check SSH Service After Configuration Change

## Command

```bash
sudo systemctl status ssh --no-pager
```

## Example Output

```text
Active: active (running)
```

---

# 151. Check SSH Configuration File Includes

## Command

```bash
grep -R "^Include" /etc/ssh/sshd_config /etc/ssh/sshd_config.d/ 2>/dev/null
```

## Example Output

```text
/etc/ssh/sshd_config:Include /etc/ssh/sshd_config.d/*.conf
```

---

# 152. List SSH Configuration Files

## Command

```bash
ls -la /etc/ssh/sshd_config.d/
```

## Example Output

```text
-rw-r--r-- 1 root root 250 ssh-hardening.conf
```

---

# 153. Search SSH Configuration

## Command

```bash
sudo grep -RniE 'Port|PermitRootLogin|PasswordAuthentication|PubkeyAuthentication' /etc/ssh/
```

## Example Output

```text
/etc/ssh/sshd_config:Port 22
/etc/ssh/sshd_config:PermitRootLogin no
/etc/ssh/sshd_config:PasswordAuthentication no
```

---

# 154. Check SSH Client Configuration Files

## Command

```bash
ls -la /etc/ssh/ssh_config ~/.ssh/config
```

## Example Output

```text
-rw-r--r-- 1 root root 3000 /etc/ssh/ssh_config
-rw------- 1 devops devops 200 /home/devops/.ssh/config
```

---

# 155. Test SSH DNS Resolution

## Command

```bash
getent hosts server.example.com
```

## Example Output

```text
10.10.2.189 server.example.com
```

---

# 156. Test SSH Network Connectivity

## Command

```bash
ping -c 4 10.10.2.189
```

## Example Output

```text
4 packets transmitted, 4 received, 0% packet loss
```

---

# 157. Test SSH Port Connectivity

## Command

```bash
nc -zv 10.10.2.189 22
```

## Example Output

```text
Connection to 10.10.2.189 22 port [tcp/ssh] succeeded!
```

---

# 158. Test SSH With Timeout

## Command

```bash
timeout 5 bash -c '</dev/tcp/10.10.2.189/22' && echo "Port 22 is open"
```

## Example Output

```text
Port 22 is open
```

---

# 159. Diagnose SSH Connection

## Command

```bash
ssh -vvv devops@10.10.2.189
```

## Example Output

```text
debug1: Connecting to 10.10.2.189 port 22.
debug1: Connection established.
debug1: Authenticating to 10.10.2.189
debug1: Offering public key
debug1: Authentication succeeded
```

---

# 160. Check SSH Authentication Without Password Prompt

## Command

```bash
ssh -o BatchMode=yes -o ConnectTimeout=10 devops@10.10.2.189 "echo OK"
```

## Example Output

```text
OK
```

---

# 161. Check SSH Using Specific PEM Key

## Command

```bash
ssh -vvv -i airawat_demo_devops.pem devops@10.10.2.189
```

## Example Output

```text
debug1: identity_file airawat_demo_devops.pem type 0
debug1: Offering public key
```

---

# 162. Fix PEM Key Permission Error

## Command

```bash
chmod 400 airawat_demo_devops.pem
```

## Example Output

```text
```

---

# 163. Check PEM Key Ownership

## Command

```bash
ls -l airawat_demo_devops.pem
```

## Example Output

```text
-r-------- 1 devops devops 1675 airawat_demo_devops.pem
```

---

# 164. Change PEM Key Ownership

## Command

```bash
sudo chown "$USER":"$USER" airawat_demo_devops.pem
```

## Example Output

```text
```

---

# 165. Check SSH Private Key Type

## Command

```bash
ssh-keygen -lf ~/.ssh/id_ed25519
```

## Example Output

```text
256 SHA256:ExampleFingerprint devops@example.com (ED25519)
```

---

# 166. Convert PEM Public Key

## Command

```bash
ssh-keygen -y -f myserver.pem
```

## Example Output

```text
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQExample
```

---

# 167. Compare Private Key and Public Key

## Command

```bash
ssh-keygen -y -f myserver.pem > /tmp/myserver.pub
diff <(cut -d' ' -f1-2 /tmp/myserver.pub) <(cut -d' ' -f1-2 ~/.ssh/myserver.pub)
```

## Example Output

```text
```

No output from `diff` means the key material matches.

---

# 168. Check Remote SSH Host Key

## Command

```bash
ssh-keyscan 10.10.2.189 2>/dev/null | ssh-keygen -lf -
```

## Example Output

```text
256 SHA256:ExampleFingerprint 10.10.2.189 (ED25519)
```

---

# 169. Check SSH Server Banner

## Command

```bash
nc 10.10.2.189 22
```

## Example Output

```text
SSH-2.0-OpenSSH_9.6p1 Ubuntu-3ubuntu13.14
```

Press `Ctrl+C` to exit.

---

# 170. SSH Copy File and Execute Command

## Command

```bash
scp app.tar.gz devops@10.10.2.189:/tmp/ && ssh devops@10.10.2.189 "ls -lh /tmp/app.tar.gz"
```

## Example Output

```text
app.tar.gz 100%
-rw-r--r-- 1 devops devops 250M /tmp/app.tar.gz
```

---

# 171. Execute Local Script on Remote Server

## Command

```bash
ssh devops@10.10.2.189 'bash -s' < deploy.sh
```

## Example Output

```text
Deployment started
Deployment completed
```

---

# 172. Execute Remote Script Directly

## Command

```bash
ssh devops@10.10.2.189 "bash /opt/scripts/deploy.sh"
```

## Example Output

```text
Deployment completed successfully
```

---

# 173. Check Remote Hostname Through SSH

## Command

```bash
ssh devops@10.10.2.189 hostname
```

## Example Output

```text
prod-server
```

---

# 174. Check Remote Kernel Through SSH

## Command

```bash
ssh devops@10.10.2.189 uname -r
```

## Example Output

```text
6.8.0-79-generic
```

---

# 175. Check Remote Disk Through SSH

## Command

```bash
ssh devops@10.10.2.189 "df -h"
```

## Example Output

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   25G   69G  27% /
```

---

# 176. Check Remote Memory Through SSH

## Command

```bash
ssh devops@10.10.2.189 "free -h"
```

## Example Output

```text
Mem:           15Gi       4Gi       6Gi       200Mi       5Gi       10Gi
```

---

# 177. Check Remote Processes Through SSH

## Command

```bash
ssh devops@10.10.2.189 "ps aux --sort=-%cpu | head"
```

## Example Output

```text
USER PID %CPU %MEM COMMAND
root 1250 45.0 2.1 python3 app.py
```

---

# 178. Check Remote Services Through SSH

## Command

```bash
ssh devops@10.10.2.189 "systemctl --type=service --state=running"
```

## Example Output

```text
ssh.service
nginx.service
docker.service
```

---

# 179. Restart Remote Service Through SSH

## Command

```bash
ssh devops@10.10.2.189 "sudo systemctl restart nginx"
```

## Example Output

```text
```

---

# 180. Check Remote Docker Through SSH

## Command

```bash
ssh devops@10.10.2.189 "docker ps"
```

## Example Output

```text
CONTAINER ID   IMAGE       STATUS
abc123         nginx:latest Up 2 hours
```

---

# 181. Check Remote Docker Compose Through SSH

## Command

```bash
ssh devops@10.10.2.189 "cd /opt/app && docker compose ps"
```

## Example Output

```text
NAME        STATUS
api         Up
frontend    Up
database    Up
```

---

# 182. Execute Git Command Remotely

## Command

```bash
ssh devops@10.10.2.189 "cd /opt/app && git status"
```

## Example Output

```text
On branch main
Your branch is up to date with 'origin/main'.
```

---

# 183. Git Over SSH

## Command

```bash
git clone git@github.com:username/repository.git
```

## Example Output

```text
Cloning into 'repository'...
remote: Enumerating objects
Receiving objects: 100%
```

---

# 184. Test GitHub SSH Authentication

## Command

```bash
ssh -T git@github.com
```

## Example Output

```text
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

# 185. Test Bitbucket SSH Authentication

## Command

```bash
ssh -T git@bitbucket.org
```

## Example Output

```text
authenticated via ssh key.

You are authenticated as username.
```

---

# 186. Check SSH Known Host for GitHub

## Command

```bash
ssh-keygen -F github.com
```

## Example Output

```text
# Host github.com found
github.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExample
```

---

# 187. Use SSH Config for GitHub

## Command

```bash
vi ~/.ssh/config
```

## Example Configuration

```text
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
```

---

# 188. Check GitHub SSH Connection Verbosely

## Command

```bash
ssh -vvv git@github.com
```

## Example Output

```text
debug1: Connecting to github.com port 22.
debug1: Offering public key
debug1: Server accepts key
```

---

# 189. SSH Port Forwarding for Database

## Command

```bash
ssh -L 3307:127.0.0.1:3306 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

Then connect locally:

```bash
mysql -h 127.0.0.1 -P 3307 -u username -p
```

---

# 190. SSH Port Forwarding for PostgreSQL

## Command

```bash
ssh -L 5433:127.0.0.1:5432 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

Then connect locally:

```bash
psql -h 127.0.0.1 -p 5433 -U postgres
```

---

# 191. SSH Tunnel for Internal Web Application

## Command

```bash
ssh -L 8080:127.0.0.1:8080 devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

Access locally:

```bash
curl http://localhost:8080
```

## Example Output

```text
HTTP/1.1 200 OK
```

---

# 192. SSH Tunnel Through Bastion Host

## Command

```bash
ssh -J devops@203.0.113.10 -L 8080:127.0.0.1:8080 devops@10.10.2.189
```

## Example Output

```text
Welcome to internal-server
```

---

# 193. Use ControlMaster for SSH Connection Reuse

## Command

```bash
ssh -M -S ~/.ssh/cm-%r@%h:%p devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

---

# 194. Check SSH Control Socket

## Command

```bash
ls -l ~/.ssh/cm-*
```

## Example Output

```text
srw------- 1 devops devops 0 Aug 27 10:30 cm-devops@10.10.2.189:22
```

---

# 195. Close SSH Master Connection

## Command

```bash
ssh -S ~/.ssh/cm-devops@10.10.2.189:22 -O exit devops@10.10.2.189
```

## Example Output

```text
Exit request sent.
```

---

# 196. Enable SSH Compression

## Command

```bash
ssh -C devops@10.10.2.189
```

## Example Output

```text
Welcome to Ubuntu
```

Useful for slow network connections and compressible data.

---

# 197. Use SSH Escape Commands

## Command

```text
~?
```

## Example Output

```text
Supported escape sequences:
~.  terminate connection
~^Z suspend
~#  list forwarded connections
~?  this message
~~  send the escape character
```

---

# 198. Force SSH Connection Termination

## Command

```text
~.
```

## Example Output

```text
Connection to 10.10.2.189 closed.
```

Use this when an SSH session becomes unresponsive.

---

# 199. Suspend SSH Session

## Command

```text
~^Z
```

## Example Output

```text
[1]+  Stopped ssh devops@10.10.2.189
```

---

# 200. Display SSH Forwarded Connections

## Command

```text
~#
```

## Example Output

```text
The following connections are open:
 port 8080
```

---

# 201. Check SSH Client Configuration

## Command

```bash
ssh -G devops@10.10.2.189 | less
```

## Example Output

```text
user devops
hostname 10.10.2.189
port 22
identityfile ~/.ssh/id_ed25519
```

---

# 202. Check SSH Authentication Method

## Command

```bash
ssh -v -o PreferredAuthentications=publickey devops@10.10.2.189
```

## Example Output

```text
debug1: Offering public key
debug1: Server accepts key
debug1: Authentication succeeded
```

---

# 203. Check SSH Password Authentication

## Command

```bash
ssh -v -o PreferredAuthentications=password devops@10.10.2.189
```

## Example Output

```text
debug1: Authentications that can continue: publickey,password
```

---

# 204. Check SSH Server Logs on Ubuntu

## Command

```bash
sudo tail -f /var/log/auth.log
```

## Example Output

```text
sshd[2451]: Accepted publickey for devops from 10.10.2.50
sshd[2500]: Failed password for invalid user admin
```

Press `Ctrl+C` to exit.

---

# 205. Search Authentication Logs for Failed SSH

## Command

```bash
sudo grep "Failed password" /var/log/auth.log
```

## Example Output

```text
Failed password for invalid user admin from 192.168.1.50
Failed password for root from 192.168.1.60
```

---

# 206. Search Authentication Logs for Successful SSH

## Command

```bash
sudo grep "Accepted" /var/log/auth.log
```

## Example Output

```text
Accepted publickey for devops from 192.168.1.50
Accepted password for admin from 192.168.1.60
```

---

# 207. Count Failed SSH Login Attempts

## Command

```bash
sudo grep "Failed password" /var/log/auth.log | wc -l
```

## Example Output

```text
25
```

---

# 208. Find Top Source IPs for Failed SSH Attempts

## Command

```bash
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
```

## Example Output

```text
50 192.168.1.50
35 192.168.1.60
20 203.0.113.25
```

> Log formats can differ between distributions, so verify the fields on your system before relying on this exact `awk` expression.

---

# 209. Monitor SSH Authentication Logs

## Command

```bash
sudo tail -f /var/log/auth.log | grep sshd
```

## Example Output

```text
sshd[2451]: Accepted publickey for devops
sshd[2500]: Failed password for invalid user test
```

---

# 210. Check SSH Service Dependencies

## Command

```bash
systemctl list-dependencies ssh
```

## Example Output

```text
ssh.service
├─system.slice
└─network.target
```

---

# 211. Display SSH Service Unit

## Command

```bash
systemctl cat ssh
```

## Example Output

```text
[Unit]
Description=OpenBSD Secure Shell server
After=network.target
```

---

# 212. Check SSH Service Process

## Command

```bash
systemctl status ssh --no-pager
```

## Example Output

```text
Main PID: 1234 (sshd)
Tasks: 1
Memory: 2.5M
```

---

# 213. Restart SSH After Configuration Change

## Command

```bash
sudo sshd -t && sudo systemctl restart ssh
```

## Example Output

```text
```

> Prefer `reload` when possible to reduce disruption to existing sessions.

---

# 214. Check SSH Port With ss

## Command

```bash
sudo ss -lntp | grep ssh
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:22
```

---

# 215. Check SSH Port With lsof

## Command

```bash
sudo lsof -nP -iTCP:22 -sTCP:LISTEN
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NODE NAME
sshd 1234 root 3u IPv4 TCP *:22 (LISTEN)
```

---

# 216. Check SSH Network Path

## Command

```bash
traceroute 10.10.2.189
```

## Example Output

```text
1  192.168.1.1
2  10.10.0.1
3  10.10.2.189
```

---

# 217. Capture SSH Traffic

## Command

```bash
sudo tcpdump -i eth0 port 22
```

## Example Output

```text
IP 10.10.2.50.52314 > 10.10.2.189.22: Flags [S]
IP 10.10.2.189.22 > 10.10.2.50.52314: Flags [S.]
```

---

# 218. Capture SSH Traffic From Specific Host

## Command

```bash
sudo tcpdump -i eth0 host 10.10.2.50 and port 22
```

## Example Output

```text
IP 10.10.2.50.52314 > 10.10.2.189.22
```

---

# 219. Save SSH Packet Capture

## Command

```bash
sudo tcpdump -i eth0 port 22 -w ssh.pcap
```

## Example Output

```text
tcpdump: listening on eth0
```

Press `Ctrl+C` to stop.

---

# 220. Read SSH Packet Capture

## Command

```bash
sudo tcpdump -r ssh.pcap
```

## Example Output

```text
IP 10.10.2.50.52314 > 10.10.2.189.22
```

---

# 221. Check SSH Server Hostname

## Command

```bash
hostnamectl
```

## Example Output

```text
Static hostname: prod-server
Operating System: Ubuntu 24.04.3 LTS
```

---

# 222. Check SSH Server IP

## Command

```bash
hostname -I
```

## Example Output

```text
10.10.2.189
```

---

# 223. Check Remote SSH Server Uptime

## Command

```bash
ssh devops@10.10.2.189 uptime
```

## Example Output

```text
10:45:12 up 20 days, 3 users, load average: 0.12, 0.10, 0.08
```

---

# 224. Check Remote SSH Server OS

## Command

```bash
ssh devops@10.10.2.189 "cat /etc/os-release"
```

## Example Output

```text
PRETTY_NAME="Ubuntu 24.04.3 LTS"
VERSION_ID="24.04"
```

---

# 225. Check Remote SSH Server Kernel

## Command

```bash
ssh devops@10.10.2.189 "uname -a"
```

## Example Output

```text
Linux prod-server 6.8.0-79-generic x86_64 GNU/Linux
```

---

# 226. Check Remote SSH Disk Space

## Command

```bash
ssh devops@10.10.2.189 "df -h"
```

## Example Output

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   25G   69G  27% /
```

---

# 227. Check Remote SSH Memory

## Command

```bash
ssh devops@10.10.2.189 "free -h"
```

## Example Output

```text
Mem:           15Gi       4Gi       6Gi
Swap:           2Gi       0Gi       2Gi
```

---

# 228. Check Remote SSH CPU

## Command

```bash
ssh devops@10.10.2.189 "nproc && uptime"
```

## Example Output

```text
8
10:50:12 up 20 days, load average: 0.12, 0.10, 0.08
```

---

# 229. Check Remote Service Status

## Command

```bash
ssh devops@10.10.2.189 "sudo systemctl is-active nginx"
```

## Example Output

```text
active
```

---

# 230. Check Remote Application Port

## Command

```bash
ssh devops@10.10.2.189 "sudo ss -lntp | grep ':8000'"
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8000 users:(("python3",pid=2451))
```

---

# 231. Check Remote Docker Containers

## Command

```bash
ssh devops@10.10.2.189 "docker ps --format 'table {{.Names}}\t{{.Status}}\t{{.Ports}}'"
```

## Example Output

```text
NAMES      STATUS       PORTS
api        Up 2 hours   0.0.0.0:8000->8000/tcp
nginx      Up 2 hours   0.0.0.0:80->80/tcp
```

---

# 232. Run Remote Docker Compose Command

## Command

```bash
ssh devops@10.10.2.189 "cd /opt/myapp && docker compose ps"
```

## Example Output

```text
NAME    STATUS
api     Up
worker  Up
db      Up
```

---

# 233. Remote Deployment Using SSH

## Command

```bash
ssh devops@10.10.2.189 "cd /opt/myapp && git pull && docker compose up -d --build"
```

## Example Output

```text
Already up to date.
Building api
Building worker
Container api Started
Container worker Started
```

---

# 234. Remote Deployment With Script

## Command

```bash
scp deploy.sh devops@10.10.2.189:/tmp/
ssh devops@10.10.2.189 "bash /tmp/deploy.sh"
```

## Example Output

```text
deploy.sh 100%
Deployment started
Deployment completed
```

---

# 235. Use SSH in CI/CD

## Command

```bash
ssh -o BatchMode=yes devops@10.10.2.189 "cd /opt/app && ./deploy.sh"
```

## Example Output

```text
Deployment started
Deployment successful
```

---

# 236. SSH Health Check Script

## Command

```bash
for host in 10.10.2.189 10.10.2.190 10.10.2.191; do
    ssh -o BatchMode=yes -o ConnectTimeout=5 devops@$host "hostname" \
    && echo "$host OK" \
    || echo "$host FAILED"
done
```

## Example Output

```text
prod-01
10.10.2.189 OK
prod-02
10.10.2.190 OK
10.10.2.191 FAILED
```

---

# 237. Execute Command on Multiple Servers

## Command

```bash
for host in server1 server2 server3; do
    ssh devops@$host "hostname && uptime"
done
```

## Example Output

```text
server1
10:00:00 up 20 days

server2
10:00:01 up 15 days

server3
10:00:02 up 30 days
```

---

# 238. Copy File to Multiple Servers

## Command

```bash
for host in server1 server2 server3; do
    scp app.conf devops@$host:/tmp/
done
```

## Example Output

```text
app.conf 100%
app.conf 100%
app.conf 100%
```

---

# 239. Check SSH Connectivity to Multiple Servers

## Command

```bash
for host in server1 server2 server3; do
    ssh -o BatchMode=yes -o ConnectTimeout=5 devops@$host "echo SSH_OK"
done
```

## Example Output

```text
SSH_OK
SSH_OK
SSH_OK
```

---

# 240. SSH Production Troubleshooting Flow

## Command

```bash
# 1. Check DNS
getent hosts server.example.com

# 2. Check network connectivity
ping -c 4 server.example.com

# 3. Check SSH port
nc -zv server.example.com 22

# 4. Check SSH service
sudo systemctl status ssh

# 5. Check listening port
sudo ss -lntp | grep ':22'

# 6. Check firewall
sudo ufw status

# 7. Test SSH with verbose logging
ssh -vvv devops@server.example.com

# 8. Check SSH configuration
sudo sshd -t

# 9. Check SSH logs
sudo journalctl -u ssh -n 100

# 10. Check authentication logs
sudo tail -n 100 /var/log/auth.log
```

## Example Output

```text
DNS              → server.example.com resolved
Network          → ping successful
Port 22          → open
SSH Service      → active
Listening Port   → 0.0.0.0:22
Firewall         → 22/tcp allowed
Authentication   → publickey accepted
SSH Config       → valid
Logs             → no critical errors
```

---

# 241. SSH Authentication Troubleshooting Flow

## Command

```bash
# Check private key
ls -l ~/.ssh/id_ed25519

# Check permissions
chmod 600 ~/.ssh/id_ed25519

# Check public key
cat ~/.ssh/id_ed25519.pub

# Check SSH agent
ssh-add -l

# Add key to agent
ssh-add ~/.ssh/id_ed25519

# Check authorized keys
ssh devops@server "cat ~/.ssh/authorized_keys"

# Test verbose authentication
ssh -vvv devops@server
```

## Example Output

```text
Private key found
Correct permissions
Public key available
SSH agent running
Key loaded
Authorized key present
Authentication successful
```

---

# 242. SSH Connection Troubleshooting Flow

## Command

```bash
getent hosts server.example.com
ping -c 4 server.example.com
nc -zv server.example.com 22
ssh -vvv devops@server.example.com
```

## Example Output

```text
server.example.com → 10.10.2.189
4 packets transmitted, 4 received
Connection to 10.10.2.189 22 port succeeded
Authentication succeeded
```

---

# 243. SSH Key Permission Troubleshooting

## Command

```bash
ls -ld ~/.ssh
ls -l ~/.ssh/id_ed25519 ~/.ssh/authorized_keys
```

## Example Output

```text
drwx------ ~/.ssh
-rw------- ~/.ssh/id_ed25519
-rw------- ~/.ssh/authorized_keys
```

Correct permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 600 ~/.ssh/authorized_keys
chmod 644 ~/.ssh/id_ed25519.pub
```

---

# 244. SSH Server Permission Troubleshooting

## Command

```bash
ls -ld /home/devops
ls -ld /home/devops/.ssh
ls -l /home/devops/.ssh/authorized_keys
```

## Example Output

```text
drwxr-xr-x /home/devops
drwx------ /home/devops/.ssh
-rw------- /home/devops/.ssh/authorized_keys
```

---

# 245. Check SSH Authentication Logs in Real Time

## Command

```bash
sudo journalctl -u ssh -f
```

## Example Output

```text
sshd[2451]: Connection from 10.10.2.50 port 52314
sshd[2451]: Failed publickey for devops
sshd[2451]: Accepted publickey for devops
```

---

# 246. Check SSH Service After Reboot

## Command

```bash
systemctl is-active ssh && systemctl is-enabled ssh
```

## Example Output

```text
active
enabled
```

---

# 247. Check SSH Configuration Before Deployment

## Command

```bash
sudo sshd -t && echo "SSH configuration is valid"
```

## Example Output

```text
SSH configuration is valid
```

---

# 248. Backup SSH Configuration

## Command

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
```

## Example Output

```text
```

---

# 249. Restore SSH Configuration Backup

## Command

```bash
sudo cp /etc/ssh/sshd_config.backup /etc/ssh/sshd_config
sudo sshd -t
sudo systemctl reload ssh
```

## Example Output

```text
```

---

# 250. Complete SSH Security Check

## Command

```bash
sudo sshd -T | grep -E \
'permitrootlogin|passwordauthentication|pubkeyauthentication|permitemptypasswords|x11forwarding|maxauthtries|clientaliveinterval|clientalivecountmax'
```

## Example Output

```text
permitrootlogin no
passwordauthentication no
pubkeyauthentication yes
permitemptypasswords no
x11forwarding no
maxauthtries 3
clientaliveinterval 300
clientalivecountmax 2
```

---

# 📚 SSH Commands Summary

## Command

```bash
ssh
ssh-keygen
ssh-copy-id
ssh-add
ssh-agent
ssh-keyscan
ssh-keygen -F
ssh-keygen -R
scp
sftp
rsync
ss
lsof
nc
systemctl
journalctl
sshd
ssh-keygen
tcpdump
ufw
last
lastb
who
w
```

## Example Output

```text
SSH Connection
SSH Key Management
SSH Authentication
SSH Server Configuration
SSH Client Configuration
Secure File Transfer
SFTP
Rsync Over SSH
SSH Port Forwarding
SSH Tunneling
SSH Jump Hosts
SSH Agent Forwarding
SSH Troubleshooting
SSH Security Hardening
SSH Monitoring
DevOps Remote Execution
CI/CD Deployment
Production Troubleshooting
```

---

# 📌 Important SSH Files

## Command

```text
~/.ssh/
~/.ssh/config
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
~/.ssh/authorized_keys
~/.ssh/known_hosts
/etc/ssh/sshd_config
/etc/ssh/sshd_config.d/
/etc/ssh/ssh_config
/etc/ssh/ssh_host_*
/var/log/auth.log
```

## Example Output

```text
~/.ssh/id_ed25519       → Private SSH Key
~/.ssh/id_ed25519.pub   → Public SSH Key
~/.ssh/authorized_keys  → Authorized Public Keys
~/.ssh/known_hosts      → Known Remote Host Keys
~/.ssh/config           → SSH Client Configuration
/etc/ssh/sshd_config    → SSH Server Configuration
/etc/ssh/ssh_host_*     → SSH Server Host Keys
/var/log/auth.log       → Authentication Logs
```

---

# 📌 Important SSH Permissions

## Command

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/config
chmod 400 myserver.pem
```

## Example Output

```text
~/.ssh                 → 700
Private Key            → 600
Public Key             → 644
authorized_keys        → 600
SSH config             → 600
PEM private key        → 400
```

---

# 📌 Important SSH Ports

## Command

```text
22
2222
```

## Example Output

```text
22    → Default SSH Port
2222  → Common Custom SSH Port
```

---

# 🎯 DevOps SSH Skills Practiced

## Command

```bash
ssh
ssh-keygen
ssh-copy-id
ssh-agent
ssh-add
scp
sftp
rsync
ssh -L
ssh -R
ssh -D
ssh -J
ssh -A
ssh -vvv
ss
lsof
journalctl
systemctl
tcpdump
ufw
```

## Example Output

```text
Remote Server Access
SSH Key Authentication
Passwordless Authentication
Secure File Transfer
Application Deployment
Port Forwarding
SSH Tunneling
Bastion Host Access
Jump Host Configuration
CI/CD Remote Execution
Production Troubleshooting
SSH Security Hardening
Authentication Troubleshooting
Network Troubleshooting
```

---

# 🧪 Practical SSH Lab

## Command

```bash
# Step 1: Check SSH client
ssh -V

# Step 2: Generate SSH key
ssh-keygen -t ed25519

# Step 3: Display public key
cat ~/.ssh/id_ed25519.pub

# Step 4: Copy key to server
ssh-copy-id devops@10.10.2.189

# Step 5: Test passwordless login
ssh devops@10.10.2.189

# Step 6: Check hostname
hostname

# Step 7: Check remote system
uname -a

# Step 8: Check disk
df -h

# Step 9: Check memory
free -h

# Step 10: Check SSH service
sudo systemctl status ssh

# Step 11: Exit
exit
```

## Example Output

```text
SSH key generated successfully

Public key copied to remote server

Passwordless SSH login successful

Remote Host:
prod-server

Operating System:
Ubuntu 24.04.3 LTS

SSH Service:
active (running)
```

---

# 🚀 Production SSH Troubleshooting Cheat Sheet

## Command

```bash
# Check SSH client version
ssh -V

# Check DNS
getent hosts server.example.com

# Check network
ping -c 4 server.example.com

# Check SSH port
nc -zv server.example.com 22

# Check SSH service
sudo systemctl status ssh

# Check SSH listening port
sudo ss -lntp | grep ':22'

# Check firewall
sudo ufw status

# Check SSH configuration
sudo sshd -t

# Check effective configuration
sudo sshd -T

# Check authentication logs
sudo journalctl -u ssh -n 100

# Check Ubuntu authentication log
sudo tail -n 100 /var/log/auth.log

# Check private key
ls -l ~/.ssh/id_ed25519

# Fix private key permission
chmod 600 ~/.ssh/id_ed25519

# Check SSH agent
ssh-add -l

# Add key
ssh-add ~/.ssh/id_ed25519

# Check authorized keys
cat ~/.ssh/authorized_keys

# Debug SSH
ssh -vvv devops@server.example.com
```

## Example Output

```text
DNS              → Working
Network          → Reachable
Port 22          → Open
SSH Service      → Active
Firewall         → SSH Allowed
SSH Config       → Valid
Private Key      → Available
SSH Agent        → Key Loaded
Authorized Key   → Present
Authentication   → Successful
```

---

# 🏆 DevOps Interview Commands

## Command

```bash
# SSH connection
ssh user@server

# SSH with private key
ssh -i key.pem user@server

# SSH with custom port
ssh -p 2222 user@server

# Verbose SSH troubleshooting
ssh -vvv user@server

# Generate ED25519 key
ssh-keygen -t ed25519

# Copy public key
ssh-copy-id user@server

# Check SSH keys
ssh-add -l

# Copy file
scp file user@server:/path/

# Copy directory
scp -r directory user@server:/path/

# Synchronize files
rsync -avz -e ssh directory/ user@server:/path/

# SFTP
sftp user@server

# Local port forwarding
ssh -L 8080:localhost:8000 user@server

# Remote port forwarding
ssh -R 8080:localhost:8000 user@server

# Dynamic forwarding
ssh -D 1080 user@server

# Jump host
ssh -J user@bastion user@internal-server

# Check SSH port
sudo ss -lntp | grep ':22'

# Find SSH process
pgrep -a sshd

# Find process using SSH port
sudo lsof -i :22

# Check SSH logs
sudo journalctl -u ssh

# Check SSH configuration
sudo sshd -t

# Check effective SSH configuration
sudo sshd -T
```

## Example Output

```text
SSH Access
SSH Authentication
SSH Key Management
Secure File Transfer
Remote Deployment
Port Forwarding
SSH Tunneling
Bastion Host Access
Network Troubleshooting
Authentication Troubleshooting
Security Hardening
Production Incident Investigation
CI/CD Automation
```

---

# ✅ Learning Outcome

## Command

```bash
ssh
ssh-keygen
ssh-copy-id
ssh-agent
ssh-add
scp
sftp
rsync
ssh -L
ssh -R
ssh -D
ssh -J
ssh -A
ssh -vvv
ss
lsof
journalctl
systemctl
sshd
tcpdump
ufw
```

## Example Output

```text
By completing this topic, you should be able to:

- Connect to Linux servers using SSH
- Understand SSH client and SSH server
- Generate SSH keys
- Use ED25519 and RSA keys
- Configure passwordless SSH
- Configure authorized_keys
- Manage SSH permissions
- Use ssh-agent
- Troubleshoot private key problems
- Troubleshoot public key authentication
- Configure SSH client aliases
- Configure SSH server settings
- Change SSH ports
- Disable root SSH login
- Disable password authentication
- Configure SSH firewall rules
- Transfer files using SCP
- Transfer files using SFTP
- Synchronize files using rsync
- Execute commands remotely
- Execute scripts remotely
- Use SSH in CI/CD pipelines
- Configure local port forwarding
- Configure remote port forwarding
- Configure dynamic SOCKS forwarding
- Use bastion and jump hosts
- Use SSH agent forwarding
- Troubleshoot SSH connectivity
- Analyze SSH authentication logs
- Monitor SSH connections
- Capture SSH traffic
- Perform SSH security hardening
- Manage production Linux servers
```

---

# 📌 Final SSH Production Checklist

## Command

```bash
# SSH service
systemctl is-active ssh

# SSH enabled at boot
systemctl is-enabled ssh

# SSH configuration valid
sudo sshd -t

# SSH effective configuration
sudo sshd -T

# SSH listening port
sudo ss -lntp | grep ssh

# Firewall
sudo ufw status

# SSH logs
sudo journalctl -u ssh -n 50

# Authentication logs
sudo tail -n 50 /var/log/auth.log

# SSH keys
ls -la ~/.ssh

# SSH agent
ssh-add -l

# Authorized keys
cat ~/.ssh/authorized_keys

# Test SSH
ssh -o BatchMode=yes -o ConnectTimeout=10 user@server "echo SSH_OK"

# Check remote host
ssh user@server "hostname && uptime"

# Check remote disk
ssh user@server "df -h"

# Check remote memory
ssh user@server "free -h"

# Check remote ports
ssh user@server "sudo ss -lntup"
```

## Example Output

```text
SSH Service       → active
Boot Enabled      → enabled
Configuration     → valid
SSH Port          → listening
Firewall          → configured
Logs              → healthy
SSH Keys          → configured
Agent             → running
Authorized Keys   → present
Authentication    → successful
Remote Server     → reachable
Disk              → healthy
Memory            → healthy
Network Ports     → verified
```

---

# 🎯 SSH Troubleshooting Decision Flow

## Command

```bash
# 1. DNS
getent hosts SERVER

# 2. Network
ping -c 4 SERVER

# 3. Port
nc -zv SERVER 22

# 4. SSH
ssh -vvv USER@SERVER

# 5. Server SSH service
sudo systemctl status ssh

# 6. Listening port
sudo ss -lntp | grep ':22'

# 7. Firewall
sudo ufw status

# 8. SSH configuration
sudo sshd -t

# 9. Authentication
ls -la ~/.ssh
ssh-add -l

# 10. Server logs
sudo journalctl -u ssh -n 100
```

## Example Output

```text
DNS
 ↓
Network Connectivity
 ↓
TCP Port 22
 ↓
SSH Service
 ↓
SSH Configuration
 ↓
SSH Key
 ↓
Authentication
 ↓
Remote Shell
```
