# 📌 Linux Storage Management
---

# 1. Display Block Devices

## Command

\`\`\`bash
lsblk
\`\`\`

## Example Output

\`\`\`text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0  100G  0 disk
├─sda1   8:1    0    1G  0 part /boot
└─sda2   8:2    0   99G  0 part /
\`\`\`

`lsblk` displays disks, partitions, sizes, types, and mount points.

---

# 2. Display Block Devices With Filesystem Information

## Command

\`\`\`bash
lsblk -f
\`\`\`

## Example Output

\`\`\`text
NAME   FSTYPE FSVER LABEL UUID                                 MOUNTPOINTS
sda
├─sda1 ext4   1.0         1234-abcd                            /boot
└─sda2 ext4   1.0         5678-efgh                            /
\`\`\`

---

# 3. Display Block Devices in Human-Readable Format

## Command

\`\`\`bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS
\`\`\`

## Example Output

\`\`\`text
NAME   SIZE TYPE FSTYPE MOUNTPOINTS
sda    100G disk
├─sda1   1G part ext4   /boot
└─sda2  99G part ext4   /
\`\`\`

---

# 4. Display Block Device UUID

## Command

\`\`\`bash
lsblk -o NAME,UUID
\`\`\`

## Example Output

\`\`\`text
NAME   UUID
sda
sda1   1234-abcd
sda2   5678-efgh
\`\`\`

---

# 5. Display Block Device Paths

## Command

\`\`\`bash
lsblk -o NAME,PATH
\`\`\`

## Example Output

\`\`\`text
NAME   PATH
sda    /dev/sda
sda1   /dev/sda1
sda2   /dev/sda2
\`\`\`

---

# 6. Display Block Device Attributes

## Command

\`\`\`bash
lsblk -o NAME,MAJ:MIN,SIZE,RO,TYPE,MOUNTPOINTS
\`\`\`

## Example Output

\`\`\`text
NAME   MAJ:MIN SIZE RO TYPE MOUNTPOINTS
sda      8:0   100G  0 disk
sda1     8:1     1G  0 part /boot
sda2     8:2    99G  0 part /
\`\`\`

---

# 7. Display Mounted Filesystems

## Command

\`\`\`bash
mount
\`\`\`

## Example Output

\`\`\`text
/dev/sda2 on / type ext4 (rw,relatime)
/dev/sda1 on /boot type ext4 (rw,relatime)
\`\`\`

---

# 8. Display Mounted Filesystems Using findmnt

## Command

\`\`\`bash
findmnt
\`\`\`

## Example Output

\`\`\`text
TARGET SOURCE    FSTYPE OPTIONS
/      /dev/sda2 ext4   rw,relatime
/boot  /dev/sda1 ext4   rw,relatime
\`\`\`

---

# 9. Display Filesystem Hierarchy

## Command

\`\`\`bash
findmnt -D
\`\`\`

## Example Output

\`\`\`text
SOURCE     FSTYPE  SIZE USED AVAIL USE% TARGET
/dev/sda2  ext4     99G  25G   69G  27% /
/dev/sda1  ext4    974M 120M  788M  14% /boot
\`\`\`

---

# 10. Check Disk Space

## Command

\`\`\`bash
df
\`\`\`

## Example Output

\`\`\`text
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda2       103833600 25000000 78833600 25% /
\`\`\`

---

# 11. Check Disk Space in Human-Readable Format

## Command

\`\`\`bash
df -h
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   25G   69G  27% /
/dev/sda1       974M  120M  788M  14% /boot
\`\`\`

---

# 12. Display Filesystem Type and Disk Usage

## Command

\`\`\`bash
df -Th
\`\`\`

## Example Output

\`\`\`text
Filesystem     Type  Size  Used Avail Use% Mounted on
/dev/sda2      ext4   99G   25G   69G  27% /
/dev/sda1      ext4  974M  120M  788M  14% /boot
\`\`\`

---

# 13. Check Inode Usage

## Command

\`\`\`bash
df -i
\`\`\`

## Example Output

\`\`\`text
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
/dev/sda2      6553600 250000 6303600    4% /
\`\`\`

---

# 14. Check Inode Usage in Human-Readable Format

## Command

\`\`\`bash
df -ih
\`\`\`

## Example Output

\`\`\`text
Filesystem     Inodes IUsed IFree IUse% Mounted on
/dev/sda2        6.3M  245K  6.1M    4% /
\`\`\`

---

# 15. Display Disk Usage of Current Directory

## Command

\`\`\`bash
du
\`\`\`

## Example Output

\`\`\`text
120     ./logs
350     ./app
1024    .
\`\`\`

---

# 16. Display Disk Usage in Human-Readable Format

## Command

\`\`\`bash
du -h
\`\`\`

## Example Output

\`\`\`text
120M    ./logs
350M    ./app
1.0G    .
\`\`\`

---

# 17. Display Total Directory Size

## Command

\`\`\`bash
du -sh .
\`\`\`

## Example Output

\`\`\`text
1.2G    .
\`\`\`

---

# 18. Check Size of Specific Directory

## Command

\`\`\`bash
du -sh /var/log
\`\`\`

## Example Output

\`\`\`text
850M    /var/log
\`\`\`

---

# 19. Display Size of First-Level Directories

## Command

\`\`\`bash
du -h --max-depth=1 /var
\`\`\`

## Example Output

\`\`\`text
120M    /var/cache
850M    /var/log
2.5G    /var/lib
3.5G    /var
\`\`\`

---

# 20. Find Largest Directories

## Command

\`\`\`bash
du -h --max-depth=1 /var | sort -hr
\`\`\`

## Example Output

\`\`\`text
3.5G    /var
2.5G    /var/lib
850M    /var/log
120M    /var/cache
\`\`\`

---

# 21. Find Large Files

## Command

\`\`\`bash
find /var -type f -size +500M
\`\`\`

## Example Output

\`\`\`text
/var/log/application.log
/var/lib/docker/containers/container.log
\`\`\`

---

# 22. Find Files Larger Than 1GB

## Command

\`\`\`bash
find / -type f -size +1G 2>/dev/null
\`\`\`

## Example Output

\`\`\`text
/var/lib/docker/overlay2/data.img
/home/devops/backup.tar
\`\`\`

---

# 23. Find Files Larger Than 100MB

## Command

\`\`\`bash
find / -type f -size +100M 2>/dev/null
\`\`\`

## Example Output

\`\`\`text
/var/log/application.log
/opt/application/app.jar
\`\`\`

---

# 24. Find Top 10 Largest Files

## Command

\`\`\`bash
find / -type f -printf '%s %p\n' 2>/dev/null | sort -nr | head -10
\`\`\`

## Example Output

\`\`\`text
524288000 /var/log/application.log
419430400 /opt/app/data.db
209715200 /home/devops/backup.tar
\`\`\`

---

# 25. Display File Size

## Command

\`\`\`bash
ls -lh file.txt
\`\`\`

## Example Output

\`\`\`text
-rw-r--r-- 1 devops devops 25M Aug 27 10:00 file.txt
\`\`\`

---

# 26. Display Files Sorted by Size

## Command

\`\`\`bash
ls -lhS
\`\`\`

## Example Output

\`\`\`text
-rw-r--r-- 1 devops devops 500M backup.tar
-rw-r--r-- 1 devops devops 250M application.log
-rw-r--r-- 1 devops devops 100M data.db
\`\`\`

---

# 27. Find Empty Files

## Command

\`\`\`bash
find /var/log -type f -empty
\`\`\`

## Example Output

\`\`\`text
/var/log/empty.log
\`\`\`

---

# 28. Find Empty Directories

## Command

\`\`\`bash
find /var -type d -empty
\`\`\`

## Example Output

\`\`\`text
/var/tmp/old
/var/cache/test
\`\`\`

---

# 29. Find Files Modified Recently

## Command

\`\`\`bash
find /var/log -type f -mtime -1
\`\`\`

## Example Output

\`\`\`text
/var/log/syslog
/var/log/application.log
\`\`\`

---

# 30. Find Files Modified More Than 30 Days Ago

## Command

\`\`\`bash
find /var/log -type f -mtime +30
\`\`\`

## Example Output

\`\`\`text
/var/log/old.log
/var/log/archive.log
\`\`\`

---

# 31. Display Disk Partitions

## Command

\`\`\`bash
sudo fdisk -l
\`\`\`

## Example Output

\`\`\`text
Disk /dev/sda: 100 GiB
Device     Start       End   Size Type
/dev/sda1  2048    2099199    1G Linux filesystem
/dev/sda2 2099200 209715199   99G Linux filesystem
\`\`\`

---

# 32. Display Partition Information for Specific Disk

## Command

\`\`\`bash
sudo fdisk -l /dev/sda
\`\`\`

## Example Output

\`\`\`text
Disk /dev/sda: 100 GiB
Device     Start       End   Size Type
/dev/sda1  2048    2099199    1G Linux filesystem
/dev/sda2 2099200 209715199   99G Linux filesystem
\`\`\`

---

# 33. Display Partition Table Using parted

## Command

\`\`\`bash
sudo parted -l
\`\`\`

## Example Output

\`\`\`text
Model: VMware Virtual disk
Disk /dev/sda: 107GB
Partition Table: gpt

Number  Start   End    Size   File system
1       1049kB  1075MB 1074MB ext4
2       1075MB  107GB  106GB  ext4
\`\`\`

---

# 34. Display Partition Table Type

## Command

\`\`\`bash
sudo parted /dev/sda print
\`\`\`

## Example Output

\`\`\`text
Model: VMware Virtual disk
Disk /dev/sda: 107GB
Partition Table: gpt
\`\`\`

---

# 35. Display Disk UUID

## Command

\`\`\`bash
sudo blkid
\`\`\`

## Example Output

\`\`\`text
/dev/sda1: UUID="1234-abcd" TYPE="ext4"
/dev/sda2: UUID="5678-efgh" TYPE="ext4"
\`\`\`

---

# 36. Check UUID of Specific Partition

## Command

\`\`\`bash
sudo blkid /dev/sda2
\`\`\`

## Example Output

\`\`\`text
/dev/sda2: UUID="5678-efgh" TYPE="ext4"
\`\`\`

---

# 37. Display Filesystem Information

## Command

\`\`\`bash
sudo file -s /dev/sda2
\`\`\`

## Example Output

\`\`\`text
/dev/sda2: Linux rev 1.0 ext4 filesystem data
\`\`\`

---

# 38. Check Filesystem Type

## Command

\`\`\`bash
lsblk -f
\`\`\`

## Example Output

\`\`\`text
NAME   FSTYPE
sda1   ext4
sda2   ext4
\`\`\`

---

# 39. Create ext4 Filesystem

## Command

\`\`\`bash
sudo mkfs.ext4 /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
Creating filesystem with 262144 4k blocks and 65536 inodes
Filesystem UUID: 1234-abcd
Superblock backups stored on blocks
Writing superblocks and filesystem accounting information: done
\`\`\`

> Formatting a partition destroys existing data. Verify the device before running `mkfs`.

---

# 40. Create XFS Filesystem

## Command

\`\`\`bash
sudo mkfs.xfs /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
meta-data=/dev/sdb1
data     =                       bsize=4096
naming   =version 2
log      =internal
realtime =none
\`\`\`

---

# 41. Create Filesystem With Label

## Command

\`\`\`bash
sudo mkfs.ext4 -L DATA /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
Filesystem label=DATA
Filesystem UUID=1234-abcd
\`\`\`

---

# 42. Display Filesystem Label

## Command

\`\`\`bash
lsblk -o NAME,LABEL,FSTYPE,SIZE,MOUNTPOINTS
\`\`\`

## Example Output

\`\`\`text
NAME   LABEL FSTYPE SIZE MOUNTPOINTS
sdb1   DATA  ext4    50G
\`\`\`

---

# 43. Create Mount Point

## Command

\`\`\`bash
sudo mkdir -p /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 44. Mount Filesystem

## Command

\`\`\`bash
sudo mount /dev/sdb1 /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 45. Verify Mount

## Command

\`\`\`bash
df -h /data
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb1        50G   24K   47G   1% /data
\`\`\`

---

# 46. Verify Mount Using findmnt

## Command

\`\`\`bash
findmnt /data
\`\`\`

## Example Output

\`\`\`text
TARGET SOURCE    FSTYPE OPTIONS
/data  /dev/sdb1 ext4   rw,relatime
\`\`\`

---

# 47. Unmount Filesystem

## Command

\`\`\`bash
sudo umount /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 48. Unmount Using Device Name

## Command

\`\`\`bash
sudo umount /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 49. Check Which Process Is Using Mount Point

## Command

\`\`\`bash
sudo lsof +D /data
\`\`\`

## Example Output

\`\`\`text
COMMAND PID USER FD TYPE DEVICE NAME
bash    2451 devops cwd DIR 8,17 /data
\`\`\`

---

# 50. Find Processes Using Filesystem

## Command

\`\`\`bash
sudo fuser -vm /data
\`\`\`

## Example Output

\`\`\`text
                     USER   PID ACCESS COMMAND
/data:               devops 2451 ..c.. bash
\`\`\`

---

# 51. Force Unmount

## Command

\`\`\`bash
sudo umount -f /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

> Force unmount should be used carefully, especially on network filesystems.

---

# 52. Lazy Unmount

## Command

\`\`\`bash
sudo umount -l /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 53. Mount Using UUID

## Command

\`\`\`bash
sudo mount UUID=5678-efgh /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 54. Display /etc/fstab

## Command

\`\`\`bash
cat /etc/fstab
\`\`\`

## Example Output

\`\`\`text
UUID=5678-efgh /data ext4 defaults 0 2
\`\`\`

---

# 55. Edit /etc/fstab

## Command

\`\`\`bash
sudo vi /etc/fstab
\`\`\`

## Example Output

\`\`\`text
UUID=5678-efgh /data ext4 defaults 0 2
\`\`\`

---

# 56. Test /etc/fstab Without Rebooting

## Command

\`\`\`bash
sudo mount -a
\`\`\`

## Example Output

\`\`\`text
\`\`\`

> Always test `/etc/fstab` after modifying it to avoid boot or mount problems.

---

# 57. Display Filesystem Mount Options

## Command

\`\`\`bash
findmnt -o TARGET,SOURCE,FSTYPE,OPTIONS
\`\`\`

## Example Output

\`\`\`text
TARGET SOURCE    FSTYPE OPTIONS
/      /dev/sda2 ext4   rw,relatime
/data  /dev/sdb1 ext4   rw,relatime
\`\`\`

---

# 58. Remount Filesystem

## Command

\`\`\`bash
sudo mount -o remount /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 59. Mount Filesystem as Read-Only

## Command

\`\`\`bash
sudo mount -o ro /dev/sdb1 /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 60. Remount Filesystem as Read-Only

## Command

\`\`\`bash
sudo mount -o remount,ro /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 61. Check Filesystem Mount Status

## Command

\`\`\`bash
findmnt /data
\`\`\`

## Example Output

\`\`\`text
TARGET SOURCE    FSTYPE OPTIONS
/data  /dev/sdb1 ext4   ro,relatime
\`\`\`

---

# 62. Check Filesystem Integrity

## Command

\`\`\`bash
sudo fsck /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
/dev/sdb1: clean, 12345/327680 files, 250000/1310720 blocks
\`\`\`

> Do not run filesystem repair tools on a mounted filesystem unless the filesystem/tool specifically supports it.

---

# 63. Check ext4 Filesystem

## Command

\`\`\`bash
sudo e2fsck -f /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
Pass 1: Checking inodes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information

/dev/sdb1: clean
\`\`\`

---

# 64. Display ext4 Filesystem Information

## Command

\`\`\`bash
sudo tune2fs -l /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
Filesystem volume name: DATA
Filesystem UUID: 1234-abcd
Filesystem features: has_journal ext_attr resize_inode
Block size: 4096
Inode size: 256
\`\`\`

---

# 65. Display ext4 Filesystem Label

## Command

\`\`\`bash
sudo tune2fs -l /dev/sdb1 | grep 'Filesystem volume name'
\`\`\`

## Example Output

\`\`\`text
Filesystem volume name: DATA
\`\`\`

---

# 66. Change ext4 Filesystem Label

## Command

\`\`\`bash
sudo e2label /dev/sdb1 BACKUP
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 67. Display ext4 Filesystem UUID

## Command

\`\`\`bash
sudo tune2fs -l /dev/sdb1 | grep UUID
\`\`\`

## Example Output

\`\`\`text
Filesystem UUID: 1234-abcd
\`\`\`

---

# 68. Display Superblock Information

## Command

\`\`\`bash
sudo dumpe2fs /dev/sdb1 | head
\`\`\`

## Example Output

\`\`\`text
Filesystem volume name = DATA
Filesystem UUID = 1234-abcd
Block size = 4096
\`\`\`

---

# 69. Display Disk Device Information

## Command

\`\`\`bash
sudo udevadm info --query=all --name=/dev/sda
\`\`\`

## Example Output

\`\`\`text
DEVNAME=/dev/sda
DEVTYPE=disk
ID_MODEL=Virtual_Disk
ID_BUS=virtio
\`\`\`

---

# 70. Display Disk Vendor and Model

## Command

\`\`\`bash
lsblk -o NAME,VENDOR,MODEL,SIZE,TYPE
\`\`\`

## Example Output

\`\`\`text
NAME VENDOR  MODEL          SIZE TYPE
sda  VMware  Virtual disk   100G disk
\`\`\`

---

# 71. Display Disk Serial Number

## Command

\`\`\`bash
sudo lsblk -o NAME,SERIAL
\`\`\`

## Example Output

\`\`\`text
NAME SERIAL
sda  VM123456789
\`\`\`

---

# 72. Check Disk Read-Only Status

## Command

\`\`\`bash
lsblk -o NAME,RO
\`\`\`

## Example Output

\`\`\`text
NAME RO
sda   0
sda1  0
sda2  0
\`\`\`

---

# 73. Display Disk Queue Information

## Command

\`\`\`bash
lsblk -o NAME,MIN-IO,OPT-IO,PHY-SEC,LOG-SEC
\`\`\`

## Example Output

\`\`\`text
NAME MIN-IO OPT-IO PHY-SEC LOG-SEC
sda    512      0     512     512
\`\`\`

---

# 74. Display Disk Scheduler

## Command

\`\`\`bash
cat /sys/block/sda/queue/scheduler
\`\`\`

## Example Output

\`\`\`text
none [mq-deadline] kyber
\`\`\`

---

# 75. Display Disk Rotational Status

## Command

\`\`\`bash
cat /sys/block/sda/queue/rotational
\`\`\`

## Example Output

\`\`\`text
1
\`\`\`

`1` generally indicates rotational media and `0` generally indicates non-rotational storage such as SSD.

---

# 76. Display Disk Sector Size

## Command

\`\`\`bash
cat /sys/block/sda/queue/logical_block_size
\`\`\`

## Example Output

\`\`\`text
512
\`\`\`

---

# 77. Check Disk Health Using SMART

## Command

\`\`\`bash
sudo smartctl -a /dev/sda
\`\`\`

## Example Output

\`\`\`text
SMART overall-health self-assessment test result: PASSED
Power_On_Hours: 1250
Temperature_Celsius: 35
\`\`\`

---

# 78. Check SMART Health Only

## Command

\`\`\`bash
sudo smartctl -H /dev/sda
\`\`\`

## Example Output

\`\`\`text
SMART overall-health self-assessment test result: PASSED
\`\`\`

---

# 79. Run SMART Short Test

## Command

\`\`\`bash
sudo smartctl -t short /dev/sda
\`\`\`

## Example Output

\`\`\`text
Testing has begun.
Please wait 2 minutes for test to complete.
\`\`\`

---

# 80. Display SMART Test Results

## Command

\`\`\`bash
sudo smartctl -l selftest /dev/sda
\`\`\`

## Example Output

\`\`\`text
SMART Self-test log
# 1 Short offline Completed without error
\`\`\`

---

# 81. Check Disk I/O Statistics

## Command

\`\`\`bash
iostat
\`\`\`

## Example Output

\`\`\`text
Device    tps   kB_read/s  kB_wrtn/s
sda      25.00     450.00      220.00
\`\`\`

---

# 82. Display Extended I/O Statistics

## Command

\`\`\`bash
iostat -x
\`\`\`

## Example Output

\`\`\`text
Device  r/s  w/s  rkB/s  wkB/s  await  %util
sda    12.0  8.0   450.0   220.0   4.20   15.5
\`\`\`

---

# 83. Monitor Disk I/O Continuously

## Command

\`\`\`bash
iostat -xz 2
\`\`\`

## Example Output

\`\`\`text
Device  r/s  w/s  await  %util
sda    20.0 15.0  5.20   22.0
\`\`\`

Press `Ctrl+C` to stop.

---

# 84. Monitor Disk I/O Using iotop

## Command

\`\`\`bash
sudo iotop
\`\`\`

## Example Output

\`\`\`text
TID  USER     DISK READ  DISK WRITE
2451 devops      2.50 MB/s   1.20 MB/s
\`\`\`

Press `q` to exit.

---

# 85. Monitor Disk I/O Using vmstat

## Command

\`\`\`bash
vmstat 2
\`\`\`

## Example Output

\`\`\`text
procs memory swap io system cpu
r b swpd free  buff cache bi bo
1 0  0   2G    1G   10G  20 15
\`\`\`

---

# 86. Display Disk Statistics From /proc

## Command

\`\`\`bash
cat /proc/diskstats
\`\`\`

## Example Output

\`\`\`text
8 0 sda 12345 0 456789 1200 23456 0 345678 1500
\`\`\`

---

# 87. Monitor Disk Statistics

## Command

\`\`\`bash
watch -n 2 'cat /proc/diskstats'
\`\`\`

## Example Output

\`\`\`text
8 0 sda 12450 0 457000 1210 23500 0 346000 1510
\`\`\`

Press `Ctrl+C` to exit.

---

# 88. Check Swap

## Command

\`\`\`bash
free -h
\`\`\`

## Example Output

\`\`\`text
              total   used   free
Mem:           15Gi    8Gi    4Gi
Swap:           2Gi  100Mi  1.9Gi
\`\`\`

---

# 89. Display Swap Devices

## Command

\`\`\`bash
swapon --show
\`\`\`

## Example Output

\`\`\`text
NAME      TYPE SIZE USED PRIO
/swapfile file   2G 100M   -2
\`\`\`

---

# 90. Display Swap Summary

## Command

\`\`\`bash
cat /proc/swaps
\`\`\`

## Example Output

\`\`\`text
Filename      Type Size Used Priority
/swapfile     file 2097148 102400 -2
\`\`\`

---

# 91. Enable Swap

## Command

\`\`\`bash
sudo swapon /swapfile
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 92. Disable Swap

## Command

\`\`\`bash
sudo swapoff /swapfile
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 93. Display Swappiness

## Command

\`\`\`bash
cat /proc/sys/vm/swappiness
\`\`\`

## Example Output

\`\`\`text
60
\`\`\`

---

# 94. Check Swappiness Using sysctl

## Command

\`\`\`bash
sysctl vm.swappiness
\`\`\`

## Example Output

\`\`\`text
vm.swappiness = 60
\`\`\`

---

# 95. Change Swappiness Temporarily

## Command

\`\`\`bash
sudo sysctl -w vm.swappiness=10
\`\`\`

## Example Output

\`\`\`text
vm.swappiness = 10
\`\`\`

---

# 96. Display LVM Physical Volumes

## Command

\`\`\`bash
sudo pvs
\`\`\`

## Example Output

\`\`\`text
PV         VG        Fmt  Attr PSize   PFree
/dev/sdb1  vg_data   lvm2 a--  <50.00g 20.00g
\`\`\`

---

# 97. Display Detailed Physical Volume Information

## Command

\`\`\`bash
sudo pvdisplay
\`\`\`

## Example Output

\`\`\`text
PV Name               /dev/sdb1
VG Name               vg_data
PV Size               <50.00 GiB
Free PE               5120
\`\`\`

---

# 98. Display LVM Volume Groups

## Command

\`\`\`bash
sudo vgs
\`\`\`

## Example Output

\`\`\`text
VG       #PV #LV #SN Attr   VSize   VFree
vg_data    1   2   0 wz--n- 49.99g  20.00g
\`\`\`

---

# 99. Display Detailed Volume Group Information

## Command

\`\`\`bash
sudo vgdisplay
\`\`\`

## Example Output

\`\`\`text
VG Name               vg_data
VG Size               49.99 GiB
Free  PE / Size       5120 / 20.00 GiB
\`\`\`

---

# 100. Display Logical Volumes

## Command

\`\`\`bash
sudo lvs
\`\`\`

## Example Output

\`\`\`text
LV       VG       Attr       LSize
lv_data  vg_data  -wi-ao---- 20.00g
lv_logs  vg_data  -wi-ao---- 10.00g
\`\`\`

---

# 101. Display Detailed Logical Volume Information

## Command

\`\`\`bash
sudo lvdisplay
\`\`\`

## Example Output

\`\`\`text
LV Path                /dev/vg_data/lv_data
LV Name                lv_data
VG Name                vg_data
LV Size                20.00 GiB
\`\`\`

---

# 102. Display Complete LVM Information

## Command

\`\`\`bash
sudo lvs -a -o +devices
\`\`\`

## Example Output

\`\`\`text
LV       VG       LSize  Devices
lv_data  vg_data  20.00g /dev/sdb1(0)
\`\`\`

---

# 103. Create Physical Volume

## Command

\`\`\`bash
sudo pvcreate /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
Physical volume "/dev/sdb1" successfully created.
\`\`\`

> Verify the device carefully before running `pvcreate`.

---

# 104. Create Volume Group

## Command

\`\`\`bash
sudo vgcreate vg_data /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
Volume group "vg_data" successfully created
\`\`\`

---

# 105. Create Logical Volume

## Command

\`\`\`bash
sudo lvcreate -L 20G -n lv_data vg_data
\`\`\`

## Example Output

\`\`\`text
Logical volume "lv_data" created.
\`\`\`

---

# 106. Create Logical Volume Using Percentage

## Command

\`\`\`bash
sudo lvcreate -l 100%FREE -n lv_data vg_data
\`\`\`

## Example Output

\`\`\`text
Logical volume "lv_data" created.
\`\`\`

---

# 107. Create ext4 Filesystem on LVM

## Command

\`\`\`bash
sudo mkfs.ext4 /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
Creating filesystem with 5242880 4k blocks
Filesystem UUID: 1234-abcd
Writing superblocks and filesystem accounting information: done
\`\`\`

---

# 108. Create Mount Point for LVM

## Command

\`\`\`bash
sudo mkdir -p /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 109. Mount LVM Logical Volume

## Command

\`\`\`bash
sudo mount /dev/vg_data/lv_data /data
\`\`\`

## Example Output

\`\`\`text
\`\`\`

---

# 110. Extend Logical Volume

## Command

\`\`\`bash
sudo lvextend -L +10G /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
Size of logical volume vg_data/lv_data changed from 20.00 GiB to 30.00 GiB.
Logical volume successfully resized.
\`\`\`

---

# 111. Extend Logical Volume and Filesystem

## Command

\`\`\`bash
sudo lvextend -r -L +10G /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
Size of logical volume changed.
Filesystem resized successfully.
\`\`\`

---

# 112. Extend Logical Volume to Use All Free Space

## Command

\`\`\`bash
sudo lvextend -r -l +100%FREE /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
Logical volume successfully resized.
Filesystem successfully resized.
\`\`\`

---

# 113. Reduce Logical Volume

## Command

\`\`\`bash
sudo lvreduce -L -5G /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
WARNING: Reducing active logical volume to 25.00 GiB.
Do you really want to reduce it? [y/n]
\`\`\`

> Reducing an LV can destroy data if the filesystem is not reduced first. Do not use this command casually in production.

---

# 114. Rename Logical Volume

## Command

\`\`\`bash
sudo lvrename vg_data lv_data lv_application
\`\`\`

## Example Output

\`\`\`text
Logical volume "lv_data" successfully renamed to "lv_application".
\`\`\`

---

# 115. Rename Volume Group

## Command

\`\`\`bash
sudo vgrename vg_data vg_application
\`\`\`

## Example Output

\`\`\`text
Volume group "vg_data" successfully renamed to "vg_application"
\`\`\`

---

# 116. Remove Logical Volume

## Command

\`\`\`bash
sudo lvremove /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
Do you really want to remove active logical volume "lv_data"? [y/n]
Logical volume "lv_data" successfully removed.
\`\`\`

> Removing an LV destroys the data stored on it.

---

# 117. Remove Volume Group

## Command

\`\`\`bash
sudo vgremove vg_data
\`\`\`

## Example Output

\`\`\`text
Volume group "vg_data" successfully removed.
\`\`\`

---

# 118. Remove Physical Volume

## Command

\`\`\`bash
sudo pvremove /dev/sdb1
\`\`\`

## Example Output

\`\`\`text
Labels on physical volume "/dev/sdb1" successfully wiped.
\`\`\`

---

# 119. Add Physical Volume to Existing Volume Group

## Command

\`\`\`bash
sudo vgextend vg_data /dev/sdc1
\`\`\`

## Example Output

\`\`\`text
Volume group "vg_data" successfully extended.
\`\`\`

---

# 120. Remove Physical Volume From Volume Group

## Command

\`\`\`bash
sudo vgreduce vg_data /dev/sdc1
\`\`\`

## Example Output

\`\`\`text
Removed "/dev/sdc1" from volume group "vg_data".
\`\`\`

---

# 121. Move LVM Data Between Physical Volumes

## Command

\`\`\`bash
sudo pvmove /dev/sdb1 /dev/sdc1
\`\`\`

## Example Output

\`\`\`text
/dev/sdb1: Moved 100.00%
\`\`\`

---

# 122. Display LVM Device Mapping

## Command

\`\`\`bash
sudo lvmdiskscan
\`\`\`

## Example Output

\`\`\`text
/dev/sda
/dev/sdb
/dev/sdb1
/dev/mapper/vg_data-lv_data
\`\`\`

---

# 123. Display Device Mapper Information

## Command

\`\`\`bash
sudo dmsetup ls
\`\`\`

## Example Output

\`\`\`text
vg_data-lv_data
vg_data-lv_logs
\`\`\`

---

# 124. Display Device Mapper Tree

## Command

\`\`\`bash
sudo dmsetup ls --tree
\`\`\`

## Example Output

\`\`\`text
vg_data-lv_data (253:0)
└─sdb1 (8:17)
\`\`\`

---

# 125. Display LVM Configuration

## Command

\`\`\`bash
sudo lvm version
\`\`\`

## Example Output

\`\`\`text
LVM version: 2.03.x
Library version: 1.02.x
Driver version: 4.47.x
\`\`\`

---

# 126. Display Filesystem Resize Information

## Command

\`\`\`bash
sudo resize2fs /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
Resizing the filesystem on /dev/vg_data/lv_data to 7864320 blocks.
The filesystem is now 7864320 blocks long.
\`\`\`

---

# 127. Grow ext4 Filesystem

## Command

\`\`\`bash
sudo resize2fs /dev/vg_data/lv_data
\`\`\`

## Example Output

\`\`\`text
The filesystem is now 7864320 blocks long.
\`\`\`

---

# 128. Display XFS Filesystem Information

## Command

\`\`\`bash
sudo xfs_info /data
\`\`\`

## Example Output

\`\`\`text
meta-data=/dev/mapper/vg_data-lv_data
isize=512
agcount=4
sectsz=512
bsize=4096
\`\`\`

---

# 129. Grow XFS Filesystem

## Command

\`\`\`bash
sudo xfs_growfs /data
\`\`\`

## Example Output

\`\`\`text
data blocks changed from 5242880 to 7864320
\`\`\`

---

# 130. Display XFS Filesystem Usage

## Command

\`\`\`bash
sudo xfs_info /data
\`\`\`

## Example Output

\`\`\`text
filesystem block size: 4096
allocation groups: 4
\`\`\`

---

# 131. Display Filesystem Reserved Blocks

## Command

\`\`\`bash
sudo tune2fs -l /dev/sda2 | grep 'Reserved block'
\`\`\`

## Example Output

\`\`\`text
Reserved block count: 524288
Reserved blocks uid: 0
Reserved blocks gid: 0
\`\`\`

---

# 132. Display Filesystem Block Size

## Command

\`\`\`bash
sudo tune2fs -l /dev/sda2 | grep 'Block size'
\`\`\`

## Example Output

\`\`\`text
Block size: 4096
\`\`\`

---

# 133. Check Disk Space for Root Filesystem

## Command

\`\`\`bash
df -h /
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   25G   69G  27% /
\`\`\`

---

# 134. Check Disk Space for /var

## Command

\`\`\`bash
df -h /var
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   25G   69G  27% /
\`\`\`

---

# 135. Check Disk Space for /home

## Command

\`\`\`bash
df -h /home
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   25G   69G  27% /
\`\`\`

---

# 136. Find Directories Consuming Most Space

## Command

\`\`\`bash
sudo du -xh / 2>/dev/null | sort -h | tail -20
\`\`\`

## Example Output

\`\`\`text
500M    /var/log
1.2G    /var/lib
2.5G    /opt
5.0G    /home
\`\`\`

---

# 137. Find Largest Files in /var

## Command

\`\`\`bash
sudo find /var -type f -printf '%s %p\n' 2>/dev/null | sort -nr | head -20
\`\`\`

## Example Output

\`\`\`text
524288000 /var/log/application.log
314572800 /var/lib/application/data.db
\`\`\`

---

# 138. Find Deleted Files Still Consuming Disk Space

## Command

\`\`\`bash
sudo lsof +L1
\`\`\`

## Example Output

\`\`\`text
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NLINK NAME
java    2451 app  5w REG  8,2 524288000 0 /var/log/application.log (deleted)
\`\`\`

> This is an important production troubleshooting command when `df` shows high usage but `du` does not explain it.

---

# 139. Compare df and du

## Command

\`\`\`bash
df -h /
sudo du -sh /
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size Used Avail Use% Mounted on
/dev/sda2       99G  80G   15G  85% /

75G /
\`\`\`

A significant difference can indicate deleted-but-open files, reserved space, filesystem metadata, or other filesystem-level usage.

---

# 140. Check Disk Usage by File Type

## Command

\`\`\`bash
find /var -type f -name "*.log" -printf '%s %p\n' 2>/dev/null | sort -nr | head
\`\`\`

## Example Output

\`\`\`text
524288000 /var/log/application.log
209715200 /var/log/nginx/access.log
104857600 /var/log/nginx/error.log
\`\`\`

---

# 141. Check Docker Disk Usage

## Command

\`\`\`bash
docker system df
\`\`\`

## Example Output

\`\`\`text
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          15        8         12.5GB    5.2GB
Containers      10        4         2.1GB     1.2GB
Local Volumes   8         6         4.5GB     1.0GB
Build Cache     25                  3.2GB     3.2GB
\`\`\`

---

# 142. Display Docker Volume Usage

## Command

\`\`\`bash
docker system df -v
\`\`\`

## Example Output

\`\`\`text
Local Volumes space usage:
VOLUME NAME       LINKS   SIZE
app_data          1       2.5GB
mysql_data        1       1.8GB
\`\`\`

---

# 143. List Docker Volumes

## Command

\`\`\`bash
docker volume ls
\`\`\`

## Example Output

\`\`\`text
DRIVER    VOLUME NAME
local     app_data
local     mysql_data
\`\`\`

---

# 144. Inspect Docker Volume

## Command

\`\`\`bash
docker volume inspect app_data
\`\`\`

## Example Output

\`\`\`text
[
    {
        "Name": "app_data",
        "Driver": "local",
        "Mountpoint": "/var/lib/docker/volumes/app_data/_data"
    }
]
\`\`\`

---

# 145. Check Docker Storage Directory

## Command

\`\`\`bash
sudo du -sh /var/lib/docker
\`\`\`

## Example Output

\`\`\`text
15G    /var/lib/docker
\`\`\`

---

# 146. Find Large Docker Container Logs

## Command

\`\`\`bash
sudo find /var/lib/docker/containers -type f -name "*-json.log" -printf '%s %p\n' 2>/dev/null | sort -nr | head
\`\`\`

## Example Output

\`\`\`text
524288000 /var/lib/docker/containers/abc123/abc123-json.log
314572800 /var/lib/docker/containers/def456/def456-json.log
\`\`\`

---

# 147. Check Temporary Storage

## Command

\`\`\`bash
df -h /tmp
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size Used Avail Use% Mounted on
/dev/sda2        99G  25G   69G  27% /
\`\`\`

---

# 148. Check /tmp Directory Size

## Command

\`\`\`bash
du -sh /tmp
\`\`\`

## Example Output

\`\`\`text
450M    /tmp
\`\`\`

---

# 149. Find Large Temporary Files

## Command

\`\`\`bash
find /tmp -type f -size +100M -ls
\`\`\`

## Example Output

\`\`\`text
2451 102400 /tmp/application.tmp
\`\`\`

---

# 150. Check Disk Space Continuously

## Command

\`\`\`bash
watch -n 5 'df -h'
\`\`\`

## Example Output

\`\`\`text
Every 5.0s: df -h

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   25G   69G  27% /
\`\`\`

Press `Ctrl+C` to exit.

---

# 151. Monitor Disk Usage of a Directory Continuously

## Command

\`\`\`bash
watch -n 5 'du -sh /var/log'
\`\`\`

## Example Output

\`\`\`text
Every 5.0s: du -sh /var/log

850M    /var/log
\`\`\`

Press `Ctrl+C` to exit.

---

# 152. Check File Open Descriptors

## Command

\`\`\`bash
sudo lsof
\`\`\`

## Example Output

\`\`\`text
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
systemd 1 root cwd DIR 8,2 4096 2 /
\`\`\`

---

# 153. Check Open Files in a Directory

## Command

\`\`\`bash
sudo lsof +D /var/log
\`\`\`

## Example Output

\`\`\`text
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
rsyslogd 900 syslog 5w REG 8,2 5242880 /var/log/syslog
\`\`\`

---

# 154. Check Which Process Is Using a File

## Command

\`\`\`bash
sudo lsof /var/log/syslog
\`\`\`

## Example Output

\`\`\`text
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
rsyslogd 900 syslog 5w REG 8,2 5242880 /var/log/syslog
\`\`\`

---

# 155. Check Filesystem Usage by Mount Point

## Command

\`\`\`bash
df -hT | column -t
\`\`\`

## Example Output

\`\`\`text
Filesystem  Type  Size  Used  Avail  Use%  Mounted
/dev/sda2   ext4   99G   25G   69G   27%   /
/dev/sda1   ext4  974M  120M  788M   14%   /boot
\`\`\`

---

# 156. Display Storage Devices Using /dev

## Command

\`\`\`bash
ls -l /dev/sd*
\`\`\`

## Example Output

\`\`\`text
brw-rw---- 1 root disk 8, 0 /dev/sda
brw-rw---- 1 root disk 8, 1 /dev/sda1
brw-rw---- 1 root disk 8, 2 /dev/sda2
\`\`\`

---

# 157. Display Device Major and Minor Numbers

## Command

\`\`\`bash
ls -l /dev/sda
\`\`\`

## Example Output

\`\`\`text
brw-rw---- 1 root disk 8, 0 /dev/sda
\`\`\`

---

# 158. Check Disk Write Cache

## Command

\`\`\`bash
sudo hdparm -W /dev/sda
\`\`\`

## Example Output

\`\`\`text
/dev/sda:
 write-caching =  1 (on)
\`\`\`

---

# 159. Display Disk Parameters

## Command

\`\`\`bash
sudo hdparm -I /dev/sda
\`\`\`

## Example Output

\`\`\`text
Model Number: Virtual Disk
Serial Number: VM123456
Firmware Revision: 1.0
\`\`\`

---

# 160. Test Disk Read Speed

## Command

\`\`\`bash
sudo hdparm -Tt /dev/sda
\`\`\`

## Example Output

\`\`\`text
Timing cached reads:   12000 MB in 2.00 seconds
Timing buffered disk reads: 800 MB in 3.00 seconds
\`\`\`

---

# 161. Check Mount Table

## Command

\`\`\`bash
cat /proc/mounts
\`\`\`

## Example Output

\`\`\`text
/dev/sda2 / ext4 rw,relatime 0 0
/dev/sda1 /boot ext4 rw,relatime 0 0
\`\`\`

---

# 162. Display Filesystem Kernel Information

## Command

\`\`\`bash
cat /proc/filesystems
\`\`\`

## Example Output

\`\`\`text
nodev   sysfs
nodev   proc
        ext4
        xfs
\`\`\`

---

# 163. Display Disk Quotas

## Command

\`\`\`bash
quota -s
\`\`\`

## Example Output

\`\`\`text
Disk quotas for user devops:
Filesystem blocks quota limit grace files quota limit grace
/dev/sda2  20G   25G   30G       150K 200K 250K
\`\`\`

---

# 164. Check User Disk Usage

## Command

\`\`\`bash
du -sh /home/devops
\`\`\`

## Example Output

\`\`\`text
12G    /home/devops
\`\`\`

---

# 165. Find Files Owned by Specific User

## Command

\`\`\`bash
find / -user devops -type f 2>/dev/null | head
\`\`\`

## Example Output

\`\`\`text
/home/devops/app.log
/home/devops/backup.tar
/opt/app/config.yml
\`\`\`

---

# 166. Find Large Files Owned by User

## Command

\`\`\`bash
find / -user devops -type f -size +500M 2>/dev/null
\`\`\`

## Example Output

\`\`\`text
/home/devops/backup.tar
/opt/app/data.db
\`\`\`

---

# 167. Display Directory Inode

## Command

\`\`\`bash
ls -ldi /var/log
\`\`\`

## Example Output

\`\`\`text
123456 drwxr-xr-x 10 root root 4096 Aug 27 10:00 /var/log
\`\`\`

---

# 168. Count Files in a Directory

## Command

\`\`\`bash
find /var/log -type f | wc -l
\`\`\`

## Example Output

\`\`\`text
245
\`\`\`

---

# 169. Count Files by Extension

## Command

\`\`\`bash
find /var/log -type f -name "*.log" | wc -l
\`\`\`

## Example Output

\`\`\`text
85
\`\`\`

---

# 170. Find Inode-Heavy Directories

## Command

\`\`\`bash
find /var -xdev -type f 2>/dev/null | cut -d/ -f1-4 | sort | uniq -c | sort -nr | head
\`\`\`

## Example Output

\`\`\`text
125000 /var/lib/application
85000  /var/cache/application
45000  /var/log
\`\`\`

---

# 171. Display File Allocation Information

## Command

\`\`\`bash
filefrag -v /var/log/application.log
\`\`\`

## Example Output

\`\`\`text
File size of /var/log/application.log is 524288000 bytes
ext: logical_offset physical_offset length
0:   0..1023     123456..124479   1024
\`\`\`

---

# 172. Check File Fragmentation

## Command

\`\`\`bash
sudo filefrag -v /var/log/application.log
\`\`\`

## Example Output

\`\`\`text
File size of application.log is 500 MB
extents found: 4
\`\`\`

---

# 173. Display Storage Hardware

## Command

\`\`\`bash
sudo lshw -class disk -class storage
\`\`\`

## Example Output

\`\`\`text
*-disk
   description: Disk
   product: Virtual Disk
   size: 100GiB
\`\`\`

---

# 174. Display PCI Storage Controllers

## Command

\`\`\`bash
lspci | grep -i -E 'storage|sata|scsi|nvme'
\`\`\`

## Example Output

\`\`\`text
00:07.0 SATA controller: Intel Corporation SATA Controller
\`\`\`

---

# 175. Display NVMe Devices

## Command

\`\`\`bash
lsblk | grep nvme
\`\`\`

## Example Output

\`\`\`text
nvme0n1       259:0    0  500G  0 disk
├─nvme0n1p1   259:1    0    1G  0 part /boot
└─nvme0n1p2   259:2    0  499G  0 part /
\`\`\`

---

# 176. Display NVMe Information

## Command

\`\`\`bash
sudo nvme list
\`\`\`

## Example Output

\`\`\`text
Node         Model                 Namespace Usage
/dev/nvme0n1 Virtual NVMe Disk    1         500 GB
\`\`\`

---

# 177. Display NVMe SMART Information

## Command

\`\`\`bash
sudo nvme smart-log /dev/nvme0
\`\`\`

## Example Output

\`\`\`text
critical_warning                    : 0
temperature                         : 35 C
percentage_used                     : 5%
data_units_read                     : 125000
data_units_written                  : 90000
\`\`\`

---

# 178. Check Disk Space Before Deployment

## Command

\`\`\`bash
df -h /
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   65G   29G  70% /
\`\`\`

---

# 179. Check Docker Storage Before Deployment

## Command

\`\`\`bash
docker system df
df -h /var/lib/docker
\`\`\`

## Example Output

\`\`\`text
Images          12GB
Containers       2GB
Volumes          5GB

Filesystem      Size Used Avail Use%
/dev/sda2        99G  70G   24G  75%
\`\`\`

---

# 180. Production Storage Health Check

## Command

\`\`\`bash
df -h
df -i
lsblk -f
findmnt
sudo lvs
sudo vgs
sudo pvs
iostat -xz 1 3
free -h
swapon --show
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size Used Avail Use%
/dev/sda2        99G  70G   24G  75%

Inodes           6.3M  500K  5.8M   8%

LVM:
VG       VSize   VFree
vg_data   100G    20G

Disk I/O:
Device  r/s  w/s  await  %util
sda     20   15   5.2    22%

Swap:
NAME      SIZE USED
/swapfile 2G  100M
\`\`\`

---

# 181. Check Storage Before Installing Packages

## Command

\`\`\`bash
df -h /
df -i /
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   70G   24G  75% /

Filesystem      Inodes IUsed IFree IUse% Mounted on
/dev/sda2         6.3M  500K  5.8M    8% /
\`\`\`

---

# 182. Check Storage Before Docker Build

## Command

\`\`\`bash
df -h /var/lib/docker
docker system df
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size Used Avail Use%
/dev/sda2        99G   80G   14G  86%

Images          20GB
Containers       5GB
Volumes          8GB
Build Cache      4GB
\`\`\`

---

# 183. Check Storage Before Database Deployment

## Command

\`\`\`bash
df -h /var/lib
df -i /var/lib
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size Used Avail Use%
/dev/sda2        99G   60G   34G  64%

Filesystem      Inodes IUsed IFree IUse%
/dev/sda2         6.3M  400K  5.9M    7%
\`\`\`

---

# 184. Check Disk Performance

## Command

\`\`\`bash
iostat -xz 1 5
\`\`\`

## Example Output

\`\`\`text
Device  r/s  w/s  rkB/s  wkB/s  await  %util
sda    100   80   5000   4000   8.20   65.0
\`\`\`

---

# 185. Check Disk Latency

## Command

\`\`\`bash
iostat -xz 1 3
\`\`\`

## Example Output

\`\`\`text
Device await
sda    12.50
\`\`\`

High `await` can indicate storage latency and should be investigated alongside workload and `%util`.

---

# 186. Check Disk Utilization

## Command

\`\`\`bash
iostat -xz 1 3 | grep -E 'Device|sda'
\`\`\`

## Example Output

\`\`\`text
Device  r/s  w/s  await  %util
sda    50   40   5.20   45.0
\`\`\`

---

# 187. Find Storage Bottleneck Processes

## Command

\`\`\`bash
sudo iotop -o
\`\`\`

## Example Output

\`\`\`text
TID  USER   DISK READ  DISK WRITE
2451 app       20 MB/s    10 MB/s
3100 mysql      5 MB/s     8 MB/s
\`\`\`

---

# 188. Monitor Disk Usage and I/O Together

## Command

\`\`\`bash
watch -n 2 'df -h; echo; iostat -xz 1 1'
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size Used Avail Use%
/dev/sda2        99G  70G   24G  75%

Device  r/s  w/s  await  %util
sda     20   15   5.20   22.0
\`\`\`

---

# 189. Storage Troubleshooting - Disk Full

## Command

\`\`\`bash
df -h
sudo du -xh / 2>/dev/null | sort -h | tail -20
sudo lsof +L1
\`\`\`

## Example Output

\`\`\`text
/dev/sda2 99G 98G 0G 100% /

500M /var/log/application.log
2G   /var/lib/docker
10G  /opt/application

java 2451 app /var/log/application.log (deleted)
\`\`\`

---

# 190. Storage Troubleshooting - Inode Full

## Command

\`\`\`bash
df -ih
\`\`\`

## Example Output

\`\`\`text
Filesystem      Inodes IUsed IFree IUse%
/dev/sda2         6.3M  6.2M  100K   99%
\`\`\`

If disk space is available but inode usage is near 100%, investigate directories containing huge numbers of small files.

---

# 191. Storage Troubleshooting - Find Huge Directory

## Command

\`\`\`bash
sudo du -xh --max-depth=1 /var | sort -hr
\`\`\`

## Example Output

\`\`\`text
20G /var
15G /var/lib
4G  /var/log
1G  /var/cache
\`\`\`

---

# 192. Storage Troubleshooting - Find Huge Log File

## Command

\`\`\`bash
sudo find /var/log -type f -size +500M -ls
\`\`\`

## Example Output

\`\`\`text
524288000 /var/log/application.log
\`\`\`

---

# 193. Storage Troubleshooting - Check Deleted Files

## Command

\`\`\`bash
sudo lsof +L1
\`\`\`

## Example Output

\`\`\`text
java 2451 app 5w REG 8,2 524288000 /var/log/application.log (deleted)
\`\`\`

---

# 194. Storage Troubleshooting - Check Mount

## Command

\`\`\`bash
findmnt
df -h
lsblk -f
\`\`\`

## Example Output

\`\`\`text
/data /dev/sdb1 ext4 rw,relatime

/dev/sdb1 50G 10G 38G 21% /data
\`\`\`

---

# 195. Storage Troubleshooting - Check LVM

## Command

\`\`\`bash
sudo pvs
sudo vgs
sudo lvs
\`\`\`

## Example Output

\`\`\`text
PV         VG       PSize   PFree
/dev/sdb1  vg_data  100G    20G

VG       VSize   VFree
vg_data  100G    20G

LV       VG       LSize
lv_data  vg_data   80G
\`\`\`

---

# 196. Storage Troubleshooting - Check Filesystem

## Command

\`\`\`bash
lsblk -f
findmnt
df -Th
\`\`\`

## Example Output

\`\`\`text
NAME FSTYPE UUID       MOUNTPOINTS
sda2 ext4   5678-efgh  /

Filesystem Type Size Used Avail Use%
/dev/sda2  ext4  99G  70G  24G  75%
\`\`\`

---

# 197. Storage Troubleshooting - Check Disk Health

## Command

\`\`\`bash
sudo smartctl -H /dev/sda
\`\`\`

## Example Output

\`\`\`text
SMART overall-health self-assessment test result: PASSED
\`\`\`

---

# 198. Storage Troubleshooting - Check I/O Performance

## Command

\`\`\`bash
iostat -xz 1 5
\`\`\`

## Example Output

\`\`\`text
Device  r/s  w/s  await  %util
sda     80   60   7.50   75.0
\`\`\`

---

# 199. Storage Troubleshooting - Check Processes

## Command

\`\`\`bash
sudo iotop -o
sudo lsof +L1
sudo lsof /var/log/application.log
\`\`\`

## Example Output

\`\`\`text
2451 java  20 MB/s
2451 java  /var/log/application.log (deleted)
\`\`\`

---

# 200. Complete Storage Troubleshooting Flow

## Command

\`\`\`bash
# Check disks
lsblk

# Check filesystems
lsblk -f

# Check mounted filesystems
findmnt

# Check disk space
df -h

# Check inode usage
df -ih

# Find large directories
sudo du -xh --max-depth=1 / | sort -hr | head -20

# Find large files
sudo find / -type f -size +1G -ls 2>/dev/null

# Check deleted files
sudo lsof +L1

# Check LVM
sudo pvs
sudo vgs
sudo lvs

# Check disk health
sudo smartctl -H /dev/sda

# Check I/O
iostat -xz 1 5

# Check I/O-heavy processes
sudo iotop -o
\`\`\`

## Example Output

\`\`\`text
Disk detected
Filesystem detected
Mount points verified
Disk usage checked
Inode usage checked
Large directories identified
Large files identified
Deleted files checked
LVM checked
SMART health checked
I/O performance checked
I/O-heavy processes identified
\`\`\`

---

# 📚 Storage Commands Summary

## Command

\`\`\`bash
# Block Devices
lsblk
lsblk -f
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS

# Disk Space
df
df -h
df -Th
df -i
df -ih

# Directory Usage
du
du -h
du -sh
du -xh
find

# Partitions
fdisk
parted
blkid

# Mounting
mount
umount
findmnt

# Filesystems
mkfs
fsck
e2fsck
resize2fs
tune2fs
xfs_info
xfs_growfs

# LVM
pvcreate
pvs
pvdisplay
vgcreate
vgs
vgdisplay
vgextend
vgreduce
lvcreate
lvs
lvdisplay
lvextend
lvreduce
lvrename
lvremove
pvmove

# Disk Health
smartctl
hdparm
nvme

# Disk I/O
iostat
iotop
vmstat
cat /proc/diskstats

# Swap
free
swapon
swapoff
sysctl

# Process/File Usage
lsof
fuser

# Docker Storage
docker system df
docker volume ls
docker volume inspect
\`\`\`

## Example Output

\`\`\`text
Block Device Management
Disk Space Management
Partition Management
Filesystem Management
Mount Management
LVM Management
Disk Health Monitoring
I/O Monitoring
Swap Management
Storage Troubleshooting
Docker Storage Management
\`\`\`

---

# 🧪 Practical Storage Lab

## Command

\`\`\`bash
lsblk
lsblk -f
df -h
df -ih
findmnt
sudo du -xh --max-depth=1 /var | sort -hr
sudo pvs
sudo vgs
sudo lvs
free -h
swapon --show
iostat -xz 1 3
\`\`\`

## Example Output

\`\`\`text
NAME   SIZE TYPE FSTYPE MOUNTPOINTS
sda    100G disk
sda1     1G part ext4   /boot
sda2    99G part ext4   /

Filesystem      Size Used Avail Use%
/dev/sda2        99G  70G   24G  75%

Inodes           6.3M 500K 5.8M 8%

TARGET SOURCE    FSTYPE
/      /dev/sda2 ext4

20G /var
15G /var/lib
4G  /var/log

VG       VSize   VFree
vg_data  100G    20G

LV       VG       LSize
lv_data  vg_data   80G

Swap:
NAME      SIZE USED
/swapfile 2G  100M

Device r/s w/s await %util
sda    20  15  5.2   22%
\`\`\`

---

# 🎯 DevOps Storage Skills Practiced

## Command

\`\`\`bash
lsblk
df -h
df -i
du -sh
find
fdisk
parted
blkid
mount
umount
findmnt
mkfs
fsck
pvs
vgs
lvs
lvextend
resize2fs
xfs_growfs
smartctl
iostat
iotop
lsof
fuser
swapon
free
docker system df
\`\`\`

## Example Output

\`\`\`text
Disk Identification
Partition Management
Filesystem Management
Mount Management
Disk Usage Analysis
Inode Management
LVM Administration
Filesystem Expansion
Disk Health Monitoring
I/O Monitoring
Swap Management
Docker Storage Management
Production Storage Troubleshooting
\`\`\`

---

# 🏆 DevOps Interview Commands

## Command

\`\`\`bash
# Check disk space
df -h

# Check inode usage
df -i

# Find largest directories
du -xh --max-depth=1 /var | sort -hr

# Find large files
find / -type f -size +1G 2>/dev/null

# Check disks and partitions
lsblk
sudo fdisk -l

# Check filesystem
lsblk -f

# Check mount points
findmnt

# Check process using mount
sudo lsof +D /data

# Check deleted files
sudo lsof +L1

# Check LVM
sudo pvs
sudo vgs
sudo lvs

# Extend LVM
sudo lvextend -r -L +10G /dev/vg_data/lv_data

# Check disk health
sudo smartctl -H /dev/sda

# Check disk I/O
iostat -xz 1 5

# Check I/O-heavy processes
sudo iotop -o

# Check swap
free -h
swapon --show

# Check Docker storage
docker system df
\`\`\`

## Example Output

\`\`\`text
Disk Space
Inode Usage
Large Files
Partition Information
Filesystem Information
Mount Information
LVM Information
Deleted Open Files
Disk Health
I/O Performance
Swap Usage
Docker Storage
\`\`\`

---

# 🚀 Production Storage Cheat Sheet

## Command

\`\`\`bash
# 1. Check overall disk usage
df -h

# 2. Check inode usage
df -ih

# 3. Identify disks and partitions
lsblk -f

# 4. Check mount points
findmnt

# 5. Find largest directories
sudo du -xh --max-depth=1 / | sort -hr | head -20

# 6. Find largest files
sudo find / -type f -size +1G -ls 2>/dev/null

# 7. Find deleted files consuming space
sudo lsof +L1

# 8. Check LVM
sudo pvs
sudo vgs
sudo lvs

# 9. Check disk health
sudo smartctl -H /dev/sda

# 10. Check detailed disk health
sudo smartctl -a /dev/sda

# 11. Check I/O
iostat -xz 1 5

# 12. Check I/O-heavy processes
sudo iotop -o

# 13. Check swap
free -h
swapon --show

# 14. Check Docker storage
docker system df

# 15. Check Docker directory
sudo du -sh /var/lib/docker

# 16. Check temporary storage
df -h /tmp

# 17. Check open files
sudo lsof

# 18. Check processes using filesystem
sudo fuser -vm /data
\`\`\`

## Example Output

\`\`\`text
Disk Usage       → df -h
Inodes           → df -ih
Partitions       → lsblk -f
Mounts           → findmnt
Large Directories → du
Large Files      → find
Deleted Files    → lsof +L1
LVM              → pvs/vgs/lvs
Disk Health      → smartctl
I/O              → iostat
I/O Processes    → iotop
Swap             → free/swapon
Docker Storage   → docker system df
Open Files       → lsof
Filesystem Users → fuser
\`\`\`

---

# 📌 Important Linux Storage Concepts

## Command

\`\`\`text
Disk
Partition
Block Device
Filesystem
Mount Point
Inode
Superblock
UUID
LVM
Physical Volume
Volume Group
Logical Volume
Swap
Disk I/O
Disk Latency
Filesystem Usage
Inode Usage
\`\`\`

## Example Output

\`\`\`text
Disk
  ↓
Partition
  ↓
Filesystem
  ↓
Mount Point
  ↓
Application Data

LVM:

Physical Volume
       ↓
Volume Group
       ↓
Logical Volume
       ↓
Filesystem
       ↓
Mount Point
\`\`\`

---

# 🔥 Storage Troubleshooting Decision Flow

## Command

\`\`\`bash
df -h
df -i
sudo du -xh --max-depth=1 / | sort -hr | head -20
sudo lsof +L1
lsblk -f
findmnt
sudo pvs
sudo vgs
sudo lvs
iostat -xz 1 3
sudo smartctl -H /dev/sda
\`\`\`

## Example Output

\`\`\`text
1. Is disk space full?
       ↓
   df -h

2. Is inode usage full?
       ↓
   df -i

3. Which directory is consuming space?
       ↓
   du

4. Are deleted files still open?
       ↓
   lsof +L1

5. Is filesystem mounted correctly?
       ↓
   findmnt

6. Is LVM out of space?
       ↓
   pvs / vgs / lvs

7. Is disk I/O slow?
       ↓
   iostat / iotop

8. Is physical disk healthy?
       ↓
   smartctl

9. Is Docker consuming storage?
       ↓
   docker system df
\`\`\`

---

# ✅ Learning Outcome

## Command

\`\`\`bash
lsblk
df
du
find
fdisk
parted
blkid
mount
umount
findmnt
mkfs
fsck
pvs
vgs
lvs
lvcreate
lvextend
resize2fs
xfs_growfs
smartctl
iostat
iotop
lsof
fuser
swapon
free
docker system df
\`\`\`

## Example Output

\`\`\`text
After completing this topic, you should be able to:

- Identify disks and block devices
- Identify partitions
- Check filesystem types
- Check disk capacity
- Check filesystem usage
- Check inode usage
- Find large files
- Find large directories
- Identify deleted files consuming disk space
- Create filesystems
- Mount filesystems
- Unmount filesystems
- Configure persistent mounts
- Understand /etc/fstab
- Check filesystem health
- Repair filesystems safely
- Understand UUIDs
- Understand disk partitions
- Create and manage LVM
- Create Physical Volumes
- Create Volume Groups
- Create Logical Volumes
- Extend Logical Volumes
- Extend ext4 filesystems
- Extend XFS filesystems
- Monitor disk I/O
- Monitor disk latency
- Check disk health
- Manage swap
- Troubleshoot Docker storage
- Troubleshoot disk-full issues
- Troubleshoot inode-full issues
- Troubleshoot storage performance
- Perform production storage investigations
\`\`\`

---

# 📌 Storage Administration Checklist

## Command

\`\`\`bash
lsblk -f
df -h
df -ih
findmnt
sudo blkid
sudo fdisk -l
sudo pvs
sudo vgs
sudo lvs
iostat -xz 1 3
sudo smartctl -H /dev/sda
free -h
swapon --show
docker system df
\`\`\`

## Example Output

\`\`\`text
[✓] Disk detected
[✓] Partitions checked
[✓] Filesystems checked
[✓] Mount points checked
[✓] UUIDs checked
[✓] Disk capacity checked
[✓] Inodes checked
[✓] LVM checked
[✓] Disk I/O checked
[✓] Disk health checked
[✓] Swap checked
[✓] Docker storage checked
\`\`\`

---

# 🎯 Real-World DevOps Storage Troubleshooting Example

## Command

\`\`\`bash
# Application reports "No space left on device"

df -h
df -i

sudo du -xh --max-depth=1 /var | sort -hr

sudo find /var/log -type f -size +500M -ls

sudo lsof +L1

docker system df

sudo du -sh /var/lib/docker

sudo lvs
sudo vgs
sudo pvs

iostat -xz 1 5
\`\`\`

## Example Output

\`\`\`text
Filesystem      Size Used Avail Use%
/dev/sda2        99G   98G     0 100%

Filesystem      Inodes IUsed IFree IUse%
/dev/sda2         6.3M  500K  5.8M    8%

20G /var
15G /var/lib
4G  /var/log

524288000 /var/log/application.log

java 2451 app /var/log/application.log (deleted)

Docker:
Images       15GB
Containers    3GB
Volumes       8GB

LVM:
vg_data 100G 0G

Disk I/O:
sda 80 r/s 60 w/s 15ms await 90% util
\`\`\`

---

# 🏁 Topic 07 Complete

This topic provides the core **Linux Storage Management skills required for DevOps, SRE, Cloud, Infrastructure, and Production Troubleshooting**.

## Key Areas

\`\`\`text
Disk Management
        ↓
Partition Management
        ↓
Filesystem Management
        ↓
Mount Management
        ↓
Disk Usage Analysis
        ↓
Inode Management
        ↓
LVM Management
        ↓
Disk Health
        ↓
I/O Monitoring
        ↓
Swap Management
        ↓
Docker Storage
        ↓
Production Troubleshooting
\`\`\`
