````markdown
# 📌 Linux Networking Basics

This lab covers Linux networking commands from **beginner to advanced**.

---

# 1. Check Hostname

## Command

```bash
hostname
```

## Example Output

```text
devops-server
```

`hostname` displays the current system hostname.

---

# 2. Display Hostname Information

## Command

```bash
hostnamectl
```

## Example Output

```text
Static hostname: devops-server
Operating System: Ubuntu 24.04.3 LTS
Kernel: Linux 6.8.0
Architecture: x86-64
```

---

# 3. Display IP Address

## Command

```bash
ip addr
```

## Example Output

```text
2: eth0:
    inet 192.168.1.100/24
```

---

# 4. Display IP Address in Short Format

## Command

```bash
ip -br addr
```

## Example Output

```text
lo        UNKNOWN        127.0.0.1/8
eth0      UP             192.168.1.100/24
docker0   UP             172.17.0.1/16
```

---

# 5. Display IPv4 Address

## Command

```bash
ip -4 addr
```

## Example Output

```text
inet 192.168.1.100/24
```

---

# 6. Display IPv6 Address

## Command

```bash
ip -6 addr
```

## Example Output

```text
inet6 fe80::20c:29ff:fe12:3456/64
```

---

# 7. Display Network Interfaces

## Command

```bash
ip link
```

## Example Output

```text
1: lo: <LOOPBACK,UP,LOWER_UP>
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP>
```

---

# 8. Display Network Interfaces in Short Format

## Command

```bash
ip -br link
```

## Example Output

```text
lo        UNKNOWN
eth0      UP
docker0   UP
```

---

# 9. Check Specific Network Interface

## Command

```bash
ip link show eth0
```

## Example Output

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
```

---

# 10. Display MAC Address

## Command

```bash
ip link show eth0
```

## Example Output

```text
link/ether 00:0c:29:12:34:56
```

---

# 11. Display MAC Address Directly

## Command

```bash
cat /sys/class/net/eth0/address
```

## Example Output

```text
00:0c:29:12:34:56
```

---

# 12. Check Interface State

## Command

```bash
cat /sys/class/net/eth0/operstate
```

## Example Output

```text
up
```

---

# 13. Bring Interface Up

## Command

```bash
sudo ip link set eth0 up
```

## Example Output

```text
```

---

# 14. Bring Interface Down

## Command

```bash
sudo ip link set eth0 down
```

## Example Output

```text
```

> Be careful when running this on a remote server because it can disconnect your SSH session.

---

# 15. Display Network Statistics

## Command

```bash
ip -s link
```

## Example Output

```text
RX: bytes  packets  errors  dropped
TX: bytes  packets  errors  dropped
```

---

# 16. Display Statistics for eth0

## Command

```bash
ip -s link show eth0
```

## Example Output

```text
RX: bytes  packets  errors  dropped
TX: bytes  packets  errors  dropped
```

---

# 17. Check MTU

## Command

```bash
ip link show eth0
```

## Example Output

```text
eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
```

---

# 18. Display MTU Directly

## Command

```bash
cat /sys/class/net/eth0/mtu
```

## Example Output

```text
1500
```

---

# 19. Display Routing Table

## Command

```bash
ip route
```

## Example Output

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.100
```

---

# 20. Display Default Gateway

## Command

```bash
ip route | grep default
```

## Example Output

```text
default via 192.168.1.1 dev eth0
```

---

# 21. Display Default Gateway Only

## Command

```bash
ip route | awk '/default/ {print $3}'
```

## Example Output

```text
192.168.1.1
```

---

# 22. Display Route to Specific IP

## Command

```bash
ip route get 8.8.8.8
```

## Example Output

```text
8.8.8.8 via 192.168.1.1 dev eth0 src 192.168.1.100
```

---

# 23. Display Routing Table Using route

## Command

```bash
route -n
```

## Example Output

```text
Destination     Gateway         Genmask         Flags Metric Ref Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0   0 eth0
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0   0 eth0
```

---

# 24. Display ARP / Neighbor Table

## Command

```bash
ip neigh
```

## Example Output

```text
192.168.1.1 dev eth0 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

---

# 25. Display ARP Table

## Command

```bash
arp -n
```

## Example Output

```text
Address          HWtype  HWaddress
192.168.1.1      ether   aa:bb:cc:dd:ee:ff
```

---

# 26. Display Neighbors for eth0

## Command

```bash
ip neigh show dev eth0
```

## Example Output

```text
192.168.1.1 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

---

# 27. Test Network Connectivity

## Command

```bash
ping -c 4 8.8.8.8
```

## Example Output

```text
4 packets transmitted, 4 received, 0% packet loss
```

---

# 28. Ping a Domain

## Command

```bash
ping -c 4 google.com
```

## Example Output

```text
4 packets transmitted, 4 received, 0% packet loss
```

---

# 29. Ping Default Gateway

## Command

```bash
ping -c 4 "$(ip route | awk '/default/ {print $3; exit}')"
```

## Example Output

```text
4 packets transmitted, 4 received, 0% packet loss
```

---

# 30. Set Ping Timeout

## Command

```bash
ping -c 4 -W 2 8.8.8.8
```

## Example Output

```text
4 packets transmitted, 4 received, 0% packet loss
```

---

# 31. Check DNS Using nslookup

## Command

```bash
nslookup google.com
```

## Example Output

```text
Name: google.com
Address: 142.250.183.14
```

---

# 32. Check DNS Using dig

## Command

```bash
dig google.com
```

## Example Output

```text
;; ANSWER SECTION:
google.com. 300 IN A 142.250.183.14
```

---

# 33. Display DNS Answer Only

## Command

```bash
dig +short google.com
```

## Example Output

```text
142.250.183.14
```

---

# 34. Check A Record

## Command

```bash
dig A google.com
```

## Example Output

```text
google.com. 300 IN A 142.250.183.14
```

---

# 35. Check AAAA Record

## Command

```bash
dig AAAA google.com
```

## Example Output

```text
google.com. 300 IN AAAA 2607:f8b0:4004:c1b::65
```

---

# 36. Check MX Record

## Command

```bash
dig MX google.com
```

## Example Output

```text
google.com. 300 IN MX 10 smtp.google.com.
```

---

# 37. Check NS Record

## Command

```bash
dig NS google.com
```

## Example Output

```text
google.com. 86400 IN NS ns1.google.com.
```

---

# 38. Check TXT Record

## Command

```bash
dig TXT google.com
```

## Example Output

```text
google.com. 300 IN TXT "v=spf1..."
```

---

# 39. Reverse DNS Lookup

## Command

```bash
dig -x 8.8.8.8
```

## Example Output

```text
8.8.8.8.in-addr.arpa. PTR dns.google.
```

---

# 40. DNS Lookup Using host

## Command

```bash
host google.com
```

## Example Output

```text
google.com has address 142.250.183.14
```

---

# 41. Reverse DNS Using host

## Command

```bash
host 8.8.8.8
```

## Example Output

```text
8.8.8.8.in-addr.arpa domain name pointer dns.google.
```

---

# 42. Display DNS Configuration

## Command

```bash
cat /etc/resolv.conf
```

## Example Output

```text
nameserver 127.0.0.53
options edns0 trust-ad
```

---

# 43. Check DNS Status

## Command

```bash
resolvectl status
```

## Example Output

```text
Global
       Protocols: -LLMNR -mDNS
resolv.conf mode: stub

Link 2 (eth0)
      DNS Servers: 192.168.1.1
```

---

# 44. Resolve Domain Using resolvectl

## Command

```bash
resolvectl query google.com
```

## Example Output

```text
google.com: 142.250.183.14
```

---

# 45. Resolve Domain Using getent

## Command

```bash
getent hosts google.com
```

## Example Output

```text
142.250.183.14 google.com
```

---

# 46. Check Hosts File

## Command

```bash
cat /etc/hosts
```

## Example Output

```text
127.0.0.1 localhost
127.0.1.1 devops-server
```

---

# 47. Display Local IP Address

## Command

```bash
hostname -I
```

## Example Output

```text
192.168.1.100
```

---

# 48. Display Public IP Address

## Command

```bash
curl -s ifconfig.me
```

## Example Output

```text
203.0.113.25
```

---

# 49. Display Listening TCP and UDP Ports

## Command

```bash
ss -tuln
```

## Example Output

```text
Netid State  Local Address:Port
tcp   LISTEN 0.0.0.0:22
tcp   LISTEN 0.0.0.0:80
tcp   LISTEN 0.0.0.0:443
udp   UNCONN 0.0.0.0:53
```

---

# 50. Display Listening TCP Ports

## Command

```bash
ss -ltn
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:22
LISTEN 0 511 0.0.0.0:80
```

---

# 51. Display Listening UDP Ports

## Command

```bash
ss -lun
```

## Example Output

```text
UNCONN 0 0 0.0.0.0:53
UNCONN 0 0 0.0.0.0:123
```

---

# 52. Display Ports With Process Information

## Command

```bash
sudo ss -tulpn
```

## Example Output

```text
tcp LISTEN 0 128 0.0.0.0:22 users:(("sshd",pid=1234,fd=3))
tcp LISTEN 0 511 0.0.0.0:80 users:(("nginx",pid=1500,fd=6))
```

---

# 53. Check Specific Port

## Command

```bash
sudo ss -ltnp | grep ':80'
```

## Example Output

```text
LISTEN 0 511 0.0.0.0:80 users:(("nginx",pid=1500,fd=6))
```

---

# 54. Check Port 8000

## Command

```bash
sudo ss -ltnp | grep ':8000'
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:8000 users:(("python3",pid=2451,fd=3))
```

---

# 55. Find Process Using Port

## Command

```bash
sudo lsof -i :8080
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
python3 2451 devops 3u IPv4 12345 0t0 TCP *:8080 (LISTEN)
```

---

# 56. Find Processes Using Network

## Command

```bash
sudo lsof -i
```

## Example Output

```text
COMMAND PID USER FD TYPE DEVICE NODE NAME
sshd 1234 root 3u IPv4 12345 TCP *:22 (LISTEN)
nginx 1500 root 6u IPv4 12346 TCP *:80 (LISTEN)
```

---

# 57. Display TCP Connections

## Command

```bash
ss -tn
```

## Example Output

```text
State  Local Address:Port   Peer Address:Port
ESTAB  192.168.1.100:22     192.168.1.50:53214
```

---

# 58. Display UDP Connections

## Command

```bash
ss -un
```

## Example Output

```text
State   Local Address:Port
UNCONN  0.0.0.0:53
UNCONN  0.0.0.0:123
```

---

# 59. Display Established Connections

## Command

```bash
ss -tan state established
```

## Example Output

```text
ESTAB 0 0 192.168.1.100:22 192.168.1.50:53214
```

---

# 60. Count Established Connections

## Command

```bash
ss -tan state established | tail -n +2 | wc -l
```

## Example Output

```text
12
```

---

# 61. Display Socket Statistics

## Command

```bash
ss -s
```

## Example Output

```text
Total: 250
TCP: 15
UDP: 5
```

---

# 62. Check TCP Connections on Port 443

## Command

```bash
ss -tan | grep ':443'
```

## Example Output

```text
ESTAB 0 0 192.168.1.100:443 192.168.1.50:52100
```

---

# 63. Test TCP Port Using nc

## Command

```bash
nc -zv 192.168.1.100 80
```

## Example Output

```text
Connection to 192.168.1.100 80 port [tcp/http] succeeded!
```

---

# 64. Test SSH Port

## Command

```bash
nc -zv 192.168.1.100 22
```

## Example Output

```text
Connection to 192.168.1.100 22 port [tcp/ssh] succeeded!
```

---

# 65. Test Multiple Ports

## Command

```bash
nc -zv 192.168.1.100 22 80 443 8080
```

## Example Output

```text
Connection to 192.168.1.100 22 port [tcp/ssh] succeeded!
Connection to 192.168.1.100 80 port [tcp/http] succeeded!
Connection to 192.168.1.100 443 port [tcp/https] succeeded!
```

---

# 66. Test HTTP Connection

## Command

```bash
curl http://localhost
```

## Example Output

```text
<!DOCTYPE html>
<html>
...
</html>
```

---

# 67. Display HTTP Headers

## Command

```bash
curl -I http://localhost
```

## Example Output

```text
HTTP/1.1 200 OK
Server: nginx
Content-Type: text/html
```

---

# 68. Display Detailed curl Output

## Command

```bash
curl -v http://localhost
```

## Example Output

```text
* Connected to localhost
> GET / HTTP/1.1
< HTTP/1.1 200 OK
```

---

# 69. Follow HTTP Redirects

## Command

```bash
curl -IL http://example.com
```

## Example Output

```text
HTTP/1.1 301 Moved Permanently
location: https://example.com/

HTTP/2 200
```

---

# 70. Check HTTP Status Code

## Command

```bash
curl -o /dev/null -s -w "%{http_code}\n" http://localhost
```

## Example Output

```text
200
```

---

# 71. Check HTTP Response Time

## Command

```bash
curl -o /dev/null -s -w "Time: %{time_total}s\n" https://google.com
```

## Example Output

```text
Time: 0.245s
```

---

# 72. Download File Using curl

## Command

```bash
curl -O https://example.com/file.txt
```

## Example Output

```text
file.txt downloaded
```

---

# 73. Download File Using wget

## Command

```bash
wget https://example.com/file.txt
```

## Example Output

```text
Saving to: 'file.txt'
file.txt 100%[================>] 1.00K
```

---

# 74. Trace Network Path

## Command

```bash
traceroute google.com
```

## Example Output

```text
1  192.168.1.1
2  10.10.0.1
3  172.16.0.1
4  142.250.183.14
```

---

# 75. Trace Network Path Using ICMP

## Command

```bash
traceroute -I google.com
```

## Example Output

```text
1  192.168.1.1
2  10.10.0.1
3  142.250.183.14
```

---

# 76. Trace Network Path Using TCP

## Command

```bash
sudo traceroute -T -p 443 google.com
```

## Example Output

```text
1  192.168.1.1
2  10.10.0.1
3  142.250.183.14
```

---

# 77. Use tracepath

## Command

```bash
tracepath google.com
```

## Example Output

```text
1?: [LOCALHOST]
1: 192.168.1.1
2: 10.10.0.1
3: google.com
```

---

# 78. Display Network Statistics Using netstat

## Command

```bash
netstat -s
```

## Example Output

```text
Ip:
    12345 total packets received

Tcp:
    100 active connection openings
```

---

# 79. Display Listening Ports Using netstat

## Command

```bash
sudo netstat -tulnp
```

## Example Output

```text
Proto Local Address   PID/Program name
tcp   0.0.0.0:22      1234/sshd
tcp   0.0.0.0:80      1500/nginx
```

---

# 80. Display Network Interfaces Using netstat

## Command

```bash
netstat -i
```

## Example Output

```text
Kernel Interface table
Iface MTU RX-OK TX-OK RX-ERR TX-ERR
eth0 1500 12345 11234 0 0
```

---

# 81. Display NetworkManager Devices

## Command

```bash
nmcli device status
```

## Example Output

```text
DEVICE  TYPE      STATE      CONNECTION
eth0    ethernet  connected  Wired
lo      loopback  connected  --
```

---

# 82. Display NetworkManager Connections

## Command

```bash
nmcli connection show
```

## Example Output

```text
NAME    UUID                                  TYPE      DEVICE
Wired   abc12345-1234-5678-9012-abcdef123456 ethernet  eth0
```

---

# 83. Display Network Device Details

## Command

```bash
nmcli device show eth0
```

## Example Output

```text
GENERAL.DEVICE: eth0
GENERAL.TYPE: ethernet
IP4.ADDRESS[1]: 192.168.1.100/24
IP4.GATEWAY: 192.168.1.1
```

---

# 84. Display NetworkManager Status

## Command

```bash
nmcli general status
```

## Example Output

```text
STATE      CONNECTIVITY
connected  full
```

---

# 85. Bring Network Connection Up

## Command

```bash
sudo nmcli connection up "Wired"
```

## Example Output

```text
Connection successfully activated
```

---

# 86. Bring Network Connection Down

## Command

```bash
sudo nmcli connection down "Wired"
```

## Example Output

```text
Connection successfully deactivated
```

---

# 87. Check Ethernet Speed

## Command

```bash
sudo ethtool eth0 | grep Speed
```

## Example Output

```text
Speed: 1000Mb/s
```

---

# 88. Check Ethernet Duplex

## Command

```bash
sudo ethtool eth0 | grep Duplex
```

## Example Output

```text
Duplex: Full
```

---

# 89. Check Ethernet Link

## Command

```bash
sudo ethtool eth0 | grep "Link detected"
```

## Example Output

```text
Link detected: yes
```

---

# 90. Display Full Ethernet Information

## Command

```bash
sudo ethtool eth0
```

## Example Output

```text
Speed: 1000Mb/s
Duplex: Full
Auto-negotiation: on
Link detected: yes
```

---

# 91. Capture Network Packets

## Command

```bash
sudo tcpdump -i eth0
```

## Example Output

```text
IP 192.168.1.100.22 > 192.168.1.50.53214: Flags [P.]
```

Press `Ctrl+C` to stop packet capture.

---

# 92. Capture Only 10 Packets

## Command

```bash
sudo tcpdump -i eth0 -c 10
```

## Example Output

```text
10 packets captured
```

---

# 93. Capture ICMP Packets

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

# 94. Capture TCP Port 80 Traffic

## Command

```bash
sudo tcpdump -i eth0 tcp port 80
```

## Example Output

```text
IP 192.168.1.100.50000 > 192.168.1.100.80: Flags [S]
```

---

# 95. Capture TCP Port 443 Traffic

## Command

```bash
sudo tcpdump -i eth0 tcp port 443
```

## Example Output

```text
IP 192.168.1.100.50000 > 142.250.183.14.443: Flags [S]
```

---

# 96. Capture Traffic From Specific Host

## Command

```bash
sudo tcpdump -i eth0 host 192.168.1.50
```

## Example Output

```text
IP 192.168.1.100 > 192.168.1.50
```

---

# 97. Capture Traffic From Specific Source

## Command

```bash
sudo tcpdump -i eth0 src 192.168.1.50
```

## Example Output

```text
IP 192.168.1.50.53214 > 192.168.1.100.22
```

---

# 98. Capture Traffic to Specific Destination

## Command

```bash
sudo tcpdump -i eth0 dst 192.168.1.50
```

## Example Output

```text
IP 192.168.1.100.22 > 192.168.1.50.53214
```

---

# 99. Save Packet Capture to File

## Command

```bash
sudo tcpdump -i eth0 -w capture.pcap
```

## Example Output

```text
tcpdump: listening on eth0
```

Press `Ctrl+C` to stop.

---

# 100. Read Packet Capture File

## Command

```bash
sudo tcpdump -r capture.pcap
```

## Example Output

```text
IP 192.168.1.100.22 > 192.168.1.50.53214
```

---

# 101. Display Firewall Status Using UFW

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
```

---

# 102. Display Detailed Firewall Status

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

# 103. Allow SSH Through Firewall

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

# 104. Allow HTTP Through Firewall

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

# 105. Allow HTTPS Through Firewall

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

# 106. Allow Specific Port

## Command

```bash
sudo ufw allow 8080/tcp
```

## Example Output

```text
Rule added
Rule added (v6)
```

---

# 107. Deny Specific Port

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

# 108. Delete Firewall Rule

## Command

```bash
sudo ufw delete allow 8080/tcp
```

## Example Output

```text
Rule deleted
Rule deleted (v6)
```

---

# 109. Display Firewall Rules With Numbers

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

# 110. Check IP Forwarding

## Command

```bash
sysctl net.ipv4.ip_forward
```

## Example Output

```text
net.ipv4.ip_forward = 0
```

---

# 111. Enable IP Forwarding Temporarily

## Command

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

## Example Output

```text
net.ipv4.ip_forward = 1
```

---

# 112. Display IPv4 Kernel Networking Parameters

## Command

```bash
sysctl -a | grep net.ipv4
```

## Example Output

```text
net.ipv4.ip_forward = 0
net.ipv4.tcp_syncookies = 1
net.ipv4.ip_local_port_range = 32768 60999
```

---

# 113. Display TCP Parameters

## Command

```bash
sysctl -a | grep net.ipv4.tcp
```

## Example Output

```text
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_fin_timeout = 60
```

---

# 114. Display Listening Services

## Command

```bash
sudo ss -lntup
```

## Example Output

```text
tcp LISTEN 0 511 0.0.0.0:80 users:(("nginx",pid=1500))
tcp LISTEN 0 128 0.0.0.0:22 users:(("sshd",pid=1234))
```

---

# 115. Find Port Using fuser

## Command

```bash
sudo fuser -n tcp 8080
```

## Example Output

```text
8080/tcp: 2451
```

---

# 116. Find Process Using UDP Port

## Command

```bash
sudo fuser -n udp 53
```

## Example Output

```text
53/udp: 900
```

---

# 117. Check Network Interface Counters

## Command

```bash
cat /proc/net/dev
```

## Example Output

```text
Inter-| Receive
eth0: 123456 1200 0 0 0 0 0 0
```

---

# 118. Display TCP Information

## Command

```bash
cat /proc/net/tcp
```

## Example Output

```text
sl local_address rem_address st
0: 0100007F:1F90 00000000:0000 0A
```

---

# 119. Display UDP Information

## Command

```bash
cat /proc/net/udp
```

## Example Output

```text
sl local_address rem_address st
0: 00000000:0035 00000000:0000 07
```

---

# 120. Display Network Namespace

## Command

```bash
ip netns list
```

## Example Output

```text
devops-net
```

---

# 121. Create Network Namespace

## Command

```bash
sudo ip netns add devops-net
```

## Example Output

```text
```

---

# 122. Execute Command Inside Network Namespace

## Command

```bash
sudo ip netns exec devops-net ip addr
```

## Example Output

```text
1: lo: <LOOPBACK>
    inet 127.0.0.1/8
```

---

# 123. Bring Namespace Loopback Interface Up

## Command

```bash
sudo ip netns exec devops-net ip link set lo up
```

## Example Output

```text
```

---

# 124. Delete Network Namespace

## Command

```bash
sudo ip netns delete devops-net
```

## Example Output

```text
```

---

# 125. Display Network Routes

## Command

```bash
ip route show
```

## Example Output

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link
```

---

# 126. Display IPv4 Routes

## Command

```bash
ip -4 route
```

## Example Output

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0
```

---

# 127. Display IPv6 Routes

## Command

```bash
ip -6 route
```

## Example Output

```text
default via fe80::1 dev eth0
fe80::/64 dev eth0
```

---

# 128. Add Temporary Route

## Command

```bash
sudo ip route add 10.10.10.0/24 via 192.168.1.1
```

## Example Output

```text
```

---

# 129. Delete Route

## Command

```bash
sudo ip route del 10.10.10.0/24
```

## Example Output

```text
```

---

# 130. Display Network Device Statistics

## Command

```bash
sar -n DEV 1 3
```

## Example Output

```text
IFACE rxpck/s txpck/s rxkB/s txkB/s
eth0  120.00  100.00  50.00  40.00
```

---

# 131. Display TCP Statistics Using sar

## Command

```bash
sar -n TCP,ETCP 1 3
```

## Example Output

```text
active/s passive/s iseg/s oseg/s
2.00     1.00      100.00  120.00
```

---

# 132. Monitor Network Traffic Using iftop

## Command

```bash
sudo iftop -i eth0
```

## Example Output

```text
192.168.1.100 => 8.8.8.8
TX: 120Kb
RX: 350Kb
```

Press `q` to exit.

---

# 133. Monitor Network Traffic Using nload

## Command

```bash
nload eth0
```

## Example Output

```text
Incoming: 350 KBit/s
Outgoing: 120 KBit/s
```

Press `q` to exit.

---

# 134. Check Network Bandwidth Using iperf3

## Command

```bash
iperf3 -c 192.168.1.100
```

## Example Output

```text
[ ID] Interval Transfer Bandwidth
[ 5] 0.00-10.00 sec 1.10 GBytes 944 Mbits/sec
```

---

# 135. Start iperf3 Server

## Command

```bash
iperf3 -s
```

## Example Output

```text
Server listening on 5201
```

---

# 136. Check DNS Port 53

## Command

```bash
sudo ss -lunp | grep ':53'
```

## Example Output

```text
UNCONN 0 0 127.0.0.53:53 users:(("systemd-resolve",pid=900))
```

---

# 137. Check SSH Port 22

## Command

```bash
sudo ss -ltnp | grep ':22'
```

## Example Output

```text
LISTEN 0 128 0.0.0.0:22 users:(("sshd",pid=1234))
```

---

# 138. Check HTTP Port 80

## Command

```bash
sudo ss -ltnp | grep ':80'
```

## Example Output

```text
LISTEN 0 511 0.0.0.0:80 users:(("nginx",pid=1500))
```

---

# 139. Check HTTPS Port 443

## Command

```bash
sudo ss -ltnp | grep ':443'
```

## Example Output

```text
LISTEN 0 511 0.0.0.0:443 users:(("nginx",pid=1500))
```

---

# 140. Check Port Connectivity Using curl

## Command

```bash
curl -v telnet://192.168.1.100:8080
```

## Example Output

```text
Connected to 192.168.1.100
```

---

# 141. Check HTTP Headers From Remote Server

## Command

```bash
curl -I http://192.168.1.100:8080
```

## Example Output

```text
HTTP/1.1 200 OK
Server: nginx
```

---

# 142. Check HTTPS Certificate

## Command

```bash
openssl s_client -connect google.com:443
```

## Example Output

```text
CONNECTED
Certificate chain
SSL-Session:
    Protocol: TLSv1.3
```

---

# 143. Check HTTPS Certificate Expiry

## Command

```bash
echo | openssl s_client -connect google.com:443 2>/dev/null | openssl x509 -noout -dates
```

## Example Output

```text
notBefore=Aug 01 00:00:00 2026 GMT
notAfter=Oct 24 23:59:59 2026 GMT
```

---

# 144. Check HTTPS Certificate Subject

## Command

```bash
echo | openssl s_client -connect google.com:443 2>/dev/null | openssl x509 -noout -subject
```

## Example Output

```text
subject=CN=*.google.com
```

---

# 145. Check DNS and Connectivity Together

## Command

```bash
getent hosts google.com && ping -c 2 google.com
```

## Example Output

```text
142.250.183.14 google.com
2 packets transmitted, 2 received, 0% packet loss
```

---

# 146. Check Gateway, DNS and Internet

## Command

```bash
ip route | grep default
resolvectl status
ping -c 2 8.8.8.8
```

## Example Output

```text
default via 192.168.1.1 dev eth0
DNS Servers: 192.168.1.1
2 packets transmitted, 2 received, 0% packet loss
```

---

# 147. Find Top Network Connections

## Command

```bash
sudo ss -tnp
```

## Example Output

```text
ESTAB 0 0 192.168.1.100:22 192.168.1.50:53214 users:(("sshd",pid=1234))
```

---

# 148. Monitor Network Connections Continuously

## Command

```bash
watch -n 2 'ss -tuln'
```

## Example Output

```text
Every 2.0s: ss -tuln

LISTEN 0 128 0.0.0.0:22
LISTEN 0 511 0.0.0.0:80
```

Press `Ctrl+C` to exit.

---

# 149. Monitor Interface Statistics Continuously

## Command

```bash
watch -n 2 'ip -s link show eth0'
```

## Example Output

```text
RX: bytes packets errors dropped
TX: bytes packets errors dropped
```

Press `Ctrl+C` to exit.

---

# 150. Check Network Service Ports

## Command

```bash
sudo ss -lntup
```

## Example Output

```text
tcp LISTEN 0 128 0.0.0.0:22
tcp LISTEN 0 511 0.0.0.0:80
tcp LISTEN 0 511 0.0.0.0:443
udp UNCONN 0 0 0.0.0.0:53
```

---

# 📚 Networking Commands Summary

## Command

```bash
hostname
hostnamectl
ip addr
ip -br addr
ip link
ip -br link
ip route
ip neigh
ping
nslookup
dig
host
resolvectl
getent
ss
lsof
nc
curl
wget
traceroute
tracepath
netstat
nmcli
ethtool
tcpdump
ufw
sysctl
iperf3
sar
iftop
nload
openssl
```

## Example Output

```text
Network Interface Management
IP Address Management
MAC Address Management
Routing
DNS Troubleshooting
Connectivity Testing
Port Troubleshooting
TCP/UDP Analysis
HTTP/HTTPS Troubleshooting
Packet Capture
Firewall Management
Network Performance Monitoring
Network Namespace Management
```

---

# 🧪 Practical Networking Troubleshooting Flow

## Command

```bash
ip -br addr
ip route
ping -c 4 "$(ip route | awk '/default/ {print $3; exit}')"
ping -c 4 8.8.8.8
getent hosts google.com
ping -c 4 google.com
ss -lntup
sudo lsof -i
curl -I http://localhost
```

## Example Output

```text
eth0 UP 192.168.1.100/24

default via 192.168.1.1 dev eth0

4 packets transmitted, 4 received, 0% packet loss

google.com resolved successfully

LISTEN 0 128 0.0.0.0:22
LISTEN 0 511 0.0.0.0:80

HTTP/1.1 200 OK
```

This troubleshooting flow helps identify whether the problem is related to:

```text
1. Network Interface
2. IP Address
3. Default Gateway
4. Internet Connectivity
5. DNS Resolution
6. Listening Ports
7. Application
```

---

# 🎯 DevOps Networking Skills Practiced

## Command

```bash
ip addr
ip route
ip neigh
ping
dig
nslookup
ss
lsof
curl
traceroute
tcpdump
nmcli
ethtool
ufw
sysctl
```

## Example Output

```text
IP Address Investigation
Routing Investigation
DNS Troubleshooting
Port Investigation
Application Connectivity Testing
Network Path Analysis
Packet Capture
NetworkManager Troubleshooting
Firewall Troubleshooting
Kernel Network Configuration
```

---

# ✅ Learning Outcome

## Command

```bash
ip
ss
ping
dig
curl
tcpdump
traceroute
nmcli
lsof
ufw
```

## Example Output

```text
By completing this topic, you should be able to:

- Identify network interfaces
- Check IPv4 and IPv6 addresses
- Identify MAC addresses
- Understand routing tables
- Find the default gateway
- Test network connectivity
- Troubleshoot DNS
- Check listening ports
- Find processes using ports
- Analyze TCP and UDP connections
- Test HTTP and HTTPS services
- Trace network paths
- Capture network packets
- Analyze network traffic
- Check firewall configuration
- Configure network interfaces
- Troubleshoot production networking issues
- Monitor network performance
- Understand network namespaces
- Perform DevOps network troubleshooting
```

---

# 🚀 Production Troubleshooting Cheat Sheet

## Command

```bash
# Check IP
ip -br addr

# Check interface
ip -br link

# Check gateway
ip route

# Check DNS
resolvectl status

# Test gateway
ping -c 4 "$(ip route | awk '/default/ {print $3; exit}')"

# Test Internet
ping -c 4 8.8.8.8

# Test DNS
dig google.com +short

# Check all listening ports
sudo ss -lntup

# Find process using port
sudo lsof -i :8080

# Test application
curl -I http://localhost:8080

# Trace network path
traceroute google.com

# Capture packets
sudo tcpdump -i eth0

# Check firewall
sudo ufw status

# Check interface speed
sudo ethtool eth0

# Check network statistics
ip -s link
```

## Example Output

```text
IP Address      → ip -br addr
Interface       → ip -br link
Gateway         → ip route
DNS             → resolvectl status
Connectivity    → ping
DNS Resolution  → dig
Ports           → ss
Process/Port    → lsof
Application     → curl
Network Path    → traceroute
Packets         → tcpdump
Firewall        → ufw
Link Speed      → ethtool
Statistics      → ip -s link
```

---

# 📌 Important Networking Ports

## Command

```text
22    SSH
23    Telnet
25    SMTP
53    DNS
67    DHCP Server
68    DHCP Client
80    HTTP
110   POP3
123   NTP
143   IMAP
443   HTTPS
3306  MySQL
5432  PostgreSQL
6379  Redis
8080  HTTP Alternative
8443  HTTPS Alternative
9090  Prometheus
3000  Grafana / Node.js Applications
```

## Example Output

```text
Port 22    → SSH
Port 53    → DNS
Port 80    → HTTP
Port 443   → HTTPS
Port 3306  → MySQL
Port 5432  → PostgreSQL
Port 6379  → Redis
Port 8080  → Application
```

---

# 🏆 DevOps Interview Commands

## Command

```bash
ip addr
ip route
ip neigh
ss -tulnp
ss -tan
sudo lsof -i :8080
ping -c 4 8.8.8.8
dig google.com
nslookup google.com
curl -I http://localhost
curl -v http://localhost:8080
traceroute google.com
sudo tcpdump -i eth0 port 80
sudo ufw status
sudo ethtool eth0
nmcli device status
```

## Example Output

```text
These commands are commonly useful for:

Network Configuration
Network Troubleshooting
DNS Troubleshooting
Port Troubleshooting
Application Troubleshooting
Firewall Troubleshooting
Production Incident Investigation
DevOps Infrastructure Troubleshooting
```
``` 
````
