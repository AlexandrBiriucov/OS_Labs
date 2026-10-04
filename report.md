#OS lab1 Report

### `whoami`

```bash
alex@ubuntu:~/os-lab1$ whoami
alex
```

The `whoami` command shows the username of the user currently logged into the system. In this case, the username is `alex`.

### `uname -a`

```bash
alex@ubuntu:~/os-lab1$ uname -a
Linux ubuntu 7.0.0-38-generic #38-Ubuntu SMP PREEMPT_DYNAMIC Fri Sep 4 09:10:14 UTC 2026 x86_64 GNU/Linux
```

The `uname -a` command displays detailed information about the operating system and kernel. Here, the system is running Ubuntu with a 64-bit (`x86_64`) Linux kernel.

### `uptime`

```bash
alex@ubuntu:~/os-lab1$ uptime
16:02:55 up 8 min, 1 user, load average: 0.22, 0.15, 0.08
```

The `uptime` command shows how long the system has been running, how many users are currently logged in, and the system load average.


##Part 1: Files and directories
1. The user(me) owns the files created , and group is also named after me. 
```
alex@ubuntu:~/os-lab1/demo$ ls -l 
total 8
-rw-rw-r-- 1 alex alex 24 Oct  4 16:16 note.txt
-rw-rw-r-- 1 alex alex 24 Oct  4 16:16 renamed.txt
alex@ubuntu:~/os-lab1/demo$ rm renamed.txt

```

2. After chmod 600 the 10 characters mean : the first character means file type, character 2-4 mean the access mode for the user, characters 5-7 mean the access mode for the group, and characters 8-10 mean the access mode for everyone else.
```
alex@ubuntu:~/os-lab1/demo$ ls -l note.txt
-rw-r--r-- 1 alex alex 24 Oct  4 16:16 note.txt

```
3. `/os-lab1/demo$` the first directory holds demo `directroy` which holds the `demo` directory with  `note.txt` file.


##Part 2: Process management

Commands execution:
```
alex@ubuntu:~$ ps aux | head
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.4  25268 16624 ?        Ss   15:54   0:01 /usr/lib/systemd/systemd --switched-root --system --deserialize=51
root           2  0.0  0.0      0     0 ?        S    15:54   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    15:54   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   15:54   0:00 [kworker/R-rcu_gp]
root           5  0.0  0.0      0     0 ?        I<   15:54   0:00 [kworker/R-sync_wq]
root           6  0.0  0.0      0     0 ?        I<   15:54   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7  0.0  0.0      0     0 ?        I<   15:54   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   15:54   0:00 [kworker/R-netns]
root          10  0.0  0.0      0     0 ?        I<   15:54   0:00 [kworker/0:0H-kblockd]
alex@ubuntu:~$ ps aux | wc -l
214
alex@ubuntu:~$ top

top - 16:43:06 up 48 min,  1 user,  load average: 0.16, 0.31, 0.23
Tasks: 212 total,   1 running, 211 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.8 us,  0.8 sy,  0.0 ni, 98.4 id,  0.0 wa,  0.0 hi,  0.0 si
MiB Mem :   3302.8 total,    402.5 free,   1538.6 used,   1624.5 buff/
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1764.2 avail

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM 
      4 root       0 -20       0      0      0 I   0.0   0.0 
      5 root       0 -20       0      0      0 I   0.0   0.0 
      6 root       0 -20       0      0      0 I   0.0   0.0 
      7 root       0 -20       0      0      0 I   0.0   0.0 
      8 root       0 -20       0      0      0 I   0.0   0.0 
     10 root       0 -20       0      0      0 I   0.0   0.0 
     12 root      20   0       0      0      0 I   0.0   0.0 
     13 root       0 -20       0      0      0 I   0.0   0.0 
     14 root      20   0       0      0      0 S   0.0   0.0 
     15 root      20   0       0      0      0 I   0.0   0.0 
     16 root      20   0       0      0      0 S   0.0   0.0 
     17 root      20   0       0      0      0 S   0.0   0.0 
     18 root      rt   0       0      0      0 S   0.0   0.0 
     19 root      20   0       0      0      0 S   0.0   0.0 
alex@ubuntu:~$ sleep 300 &
[1] 5790
alex@ubuntu:~$ jobs
[1]+  Running                    sleep 300 &
alex@ubuntu:~$ ps -ef | grep sleep
alex        5790    4745  0 16:43 pts/0    00:00:00 sleep 300
alex        5794    4745  0 16:44 pts/0    00:00:00 grep --color=auto sleep
alex@ubuntu:~$ kill <PID>
bash: syntax error near unexpected token `newline'
alex@ubuntu:~$ ^C
alex@ubuntu:~$ kill <PID>
bash: syntax error near unexpected token `newline'
alex@ubuntu:~$ kill <5790>
bash: syntax error near unexpected token `5790'
alex@ubuntu:~$ kill 5790
[1]+  Terminated                 sleep 300
alex@ubuntu:~$ sleep 300 &
[1] 5810
alex@ubuntu:~$ PID=$!
alex@ubuntu:~$ ls /proc/$PID/
arch_status         fdinfo             net            setgroups
attr                gid_map            ns             smaps
autogroup           io                 numa_maps      smaps_rollup
auxv                ksm_merging_pages  oom_adj        stack
cgroup              ksm_stat           oom_score      stat
clear_refs          latency            oom_score_adj  statm
cmdline             limits             pagemap        status
comm                loginuid           patch_state    syscall
coredump_filter     map_files          personality    task
cpu_resctrl_groups  maps               projid_map     timens_offsets
cwd                 mem                root           timers
environ             mountinfo          sched          timerslack_ns
exe                 mounts             schedstat      uid_map
fd                  mountstats         sessionid      wchan
alex@ubuntu:~$ cat /proc/$PID/status | head -20
Name:	sleep
Umask:	0002
State:	S (sleeping)
Tgid:	5810
Ngid:	0
Pid:	5810
PPid:	4745
TracerPid:	0
Uid:	1000	1000	1000	1000
Gid:	1000	1000	1000	1000
FDSize:	256
Groups:	4 24 27 30 46 100 111 114 1000 
NStgid:	5810
NSpid:	5810
NSpgid:	5810
NSsid:	4745
Kthread:	0
VmPeak:	   16112 kB
VmSize:	   16112 kB
VmLck:	       0 kB
alex@ubuntu:~$ kill $PID
[1]+  Terminated                 sleep 300

```

# Observe
1. the first process is sleep 300 and its PID is 5790
```
1]+  Running                    sleep 300 &
alex@ubuntu:~$ ps -ef | grep sleep
alex        5790    4745  0 16:43 pts/0    00:00:00 sleep 300
alex        5794    4745  0 16:44 pts/0    00:00:00 grep --color=auto sleep

```
2. 213 processes
```
alex@ubuntu:~$ ps aux | wc -l
213

```
3. the state says sleeping, which means the process is alive but its waiting.
```
State:	S (sleeping)

```


###Part 3 Memory

Commands Execution:
```
alex@ubuntu:~$ free -h    
               total        used        free      shared  buff/cache   available
Mem:           3.2Gi       1.5Gi       378Mi        36Mi       1.6Gi       1.7Gi
Swap:             0B          0B          0B
alex@ubuntu:~$ cat /proc/meminfo | head -6
MemTotal:        3382032 kB
MemFree:          312768 kB
MemAvailable:    1734320 kB
Buffers:           54100 kB
Cached:          1575860 kB
SwapCached:            0 kB
alex@ubuntu:~$ sleep 300 & PID=$!
[1] 6087
alex@ubuntu:~$ grep VmRSS /proc/$PID/status 
VmRSS:	    7508 kB
alex@ubuntu:~$ kill $PID
[1]+  Terminated                 sleep 300
alex@ubuntu:~$ 
```

# Observe 
1.  the VM has 3.2 Gi of Ram and 378 Mi is free
```
total        used        free      shared  buff/cache   available
Mem:           3.2Gi       1.5Gi       378Mi        36Mi       1.6Gi       1.7Gi
Swap:             0B          0B          0B

```
2. Swap: disk space the OS uses as overflow when RAM fills up. Inactive memory pages get moved there. It's slower than RAM. It shows 0's probably because this machine uses none.

```
Swap:             0B          0B          0B

```

3.  The sleep process uses 7508 kb of ram and that kinda of surprises me because the process doesnt do anything but wait
```
alex@ubuntu:~$ grep VmRSS /proc/$PID/status 
VmRSS:	    7508 kB
```

### Part 4 Devices and storage

Command output:
```
alex@ubuntu:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           661M  2.1M  659M   1% /run
/dev/sda2       9.8G  6.8G  2.6G  74% /
tmpfs           1.7G     0  1.7G   0% /dev/shm
none            1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           1.7G  8.0K  1.7G   1% /tmp
none            1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
tmpfs           331M   80K  331M   1% /run/user/1000
/dev/sr0         51M   51M     0 100% /run/media/alex/VBox_GAs_7.2.20
alex@ubuntu:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0     4K  1 loop /snap/bare/5
loop1    7:1    0  66.8M  1 loop /snap/core24/1643
loop2    7:2    0  14.2M  1 loop /snap/desktop-security-center/206
loop3    7:3    0    20M  1 loop /snap/desktop-security-center/151
loop4    7:4    0 260.3M  1 loop /snap/firefox/8763
loop5    7:5    0 614.5M  1 loop /snap/gnome-46-2404/164
loop6    7:6    0  16.5M  1 loop /snap/firmware-updater/226
loop7    7:7    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop8    7:8    0   1.5M  1 loop /snap/hwctl/131
loop9    7:9    0   1.5M  1 loop /snap/hwctl/123
loop10   7:10   0   402M  1 loop /snap/mesa-2404/1839
loop11   7:11   0  18.8M  1 loop /snap/prompting-client/222
loop12   7:12   0  11.8M  1 loop /snap/snap-store/1390
loop13   7:13   0  18.4M  1 loop /snap/prompting-client/228
loop14   7:14   0  50.1M  1 loop /snap/snapd/27710
loop15   7:15   0   828K  1 loop /snap/snapd-desktop-integration/391
sda      8:0    0  10.1G  0 disk 
├─sda1   8:1    0     1M  0 part 
└─sda2   8:2    0    10G  0 part /
sr0     11:0    1  50.7M  1 rom  /run/media/alex/VBox_GAs_7.2.20
alex@ubuntu:~$ du -sh ~/os-lab1
12K	/home/alex/os-lab1
alex@ubuntu:~$ ls -l /dev | head
total 0
crw-r--r--  1 root    root     10, 235 Oct  4 15:54 autofs
drwxr-xr-x  2 root    root        460 Oct  4 16:48 block
drwxr-xr-x  2 root    root         80 Oct  4 15:54 bsg
crw-------  1 root    root     10, 234 Oct  4 15:54 btrfs-control
drwxr-xr-x  3 root    root         60 Oct  4 15:54 bus
lrwxrwxrwx+ 1 root    root          3 Oct  4 15:54 cdrom -> sr0
drwxr-xr-x  2 root    root       3740 Oct  4 17:14 char
crw-------  1 root    tty       5,   1 Oct  4 15:54 console
lrwxrwxrwx  1 root    root         11 Oct  4 15:54 core -> /proc/kcore
alex@ubuntu:~$ mount | head
tmpfs on /run type tmpfs (rw,nosuid,nodev,size=676408k,nr_inodes=819200,mode=755,inode64)
/dev/sda2 on / type ext4 (rw,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,size=731316k,nr_inodes=182829,mode=755,inode64)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,inode64,usrquota)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=600,ptmxmode=000)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
cgroup2 on /sys/fs/cgroup type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate,memory_recursiveprot,memory_hugetlb_accounting)
none on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)

```
#Observe 
1. My root files system is mounted on  `/dev/sda2` 
2. A /dev entry and what it stands for, for example:
`/dev/sda` is the first physical (or virtual) hard disk
`/dev/null` discards anything written to it
`/dev/tty` is  terminal
3. Everything is a file": write it in your own words, something like: disks, terminals and even process info appear as entries in the filesystem, so the same operations (open, read, write) work on all of them, rather than needing a different interface for each.






