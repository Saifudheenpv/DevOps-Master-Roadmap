🛠️ PHASE 1 — MODULE 1.1

⚙️ PART 2 — REAL TASKS (LAB-BASED, STEP-BY-STEP)

##
🔹 Lab Instruction

👉 Work on: devops-control (main machine)

👉 Later we will involve app-node and monitor-node

##
🔹 TASK 1 — Identify Your OS (Distro Level)

📌 Command

    cat /etc/os-release

##
    devops@devops-control:~$ cat /etc/os-release 
    PRETTY_NAME="Ubuntu 24.04.4 LTS"
    NAME="Ubuntu"
    VERSION_ID="24.04"
    VERSION="24.04.4 LTS (Noble Numbat)"
    VERSION_CODENAME=noble
    ID=ubuntu
    ID_LIKE=debian
    HOME_URL="https://www.ubuntu.com/"
    SUPPORT_URL="https://help.ubuntu.com/"
    BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
    PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
    UBUNTU_CODENAME=noble
    LOGO=ubuntu-logo

##
✅ What You Should See

NAME (Ubuntu)

VERSION

ID

##
🧠 Understanding

This is Linux Distribution info

Stored in /etc (system config directory)

Confirms:

👉 You are using a distro, not just kernel

##
🔹 TASK 2 — Check Kernel (CORE)

📌 Command

    uname -r

##
    devops@devops-control:~$ uname -r
    6.8.0-111-generic

##
📌 Full Info

    uname -a

##
    devops@devops-control:~$ uname -a
    Linux devops-control 6.8.0-111-generic #111-Ubuntu SMP PREEMPT_DYNAMIC Sat Apr 11 23:16:02 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

##
🧠 Understanding

Shows Linux kernel version

Confirms:

👉 Linux = kernel

👉 Ubuntu = full OS

##
🔹 TASK 3 — System Architecture

    uname -m

##
    devops@devops-control:~$ uname -m
    x86_64

##
🧠 Understanding

CPU architecture (x86_64)

Important for:

    Docker images
    
    Binary compatibility

##
🔹 TASK 4 — Observe Processes (Kernel in Action)

    ps aux | head

##
    devops@devops-control:~$ ps aux | head
    USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root           1  0.0  0.3  22032 13316 ?        Ss   06:54   0:02 /sbin/init
    root           2  0.0  0.0      0     0 ?        S    06:54   0:00 [kthreadd]
    root           3  0.0  0.0      0     0 ?        S    06:54   0:00 [pool_workqueue_release]
    root           4  0.0  0.0      0     0 ?        I<   06:54   0:00 [kworker/R-rcu_g]
    root           5  0.0  0.0      0     0 ?        I<   06:54   0:00 [kworker/R-rcu_p]
    root           6  0.0  0.0      0     0 ?        I<   06:54   0:00 [kworker/R-slub_]
    root           7  0.0  0.0      0     0 ?        I<   06:54   0:00 [kworker/R-netns]
    root           9  0.0  0.0      0     0 ?        I<   06:54   0:00 [kworker/0:0H-events_highpri]
    root          11  0.0  0.0      0     0 ?        I    06:54   0:00 [kworker/u4:0-ipv6_addrconf]

##
🧠 Understanding

Shows running processes

Each process:
    
    Uses CPU
    
    Uses memory

Managed by kernel scheduler

##
🔹 TASK 5 — Live System Monitoring

    top

👉 Press q to exit

##
    devops@devops-control:~$ top

##
    top - 09:54:59 up  3:00,  1 user,  load average: 0.00, 0.00, 0.00
    Tasks: 134 total,   1 running, 133 sleeping,   0 stopped,   0 zombie
    %Cpu(s):  0.3 us,  0.3 sy,  0.0 ni, 99.4 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
    MiB Mem :   3915.9 total,   3376.7 free,    442.0 used,    324.3 buff/cache     
    MiB Swap:   2886.0 total,   2886.0 free,      0.0 used.   3473.9 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                               
    988 devops    20   0   15124   7136   5140 S   0.7   0.2   0:00.56 sshd                                  
    1341 root      20   0       0      0      0 I   0.3   0.0   0:01.70 kworker/1:3-events                    
    1 root      20   0   22032  13316   9572 S   0.0   0.3   0:02.19 systemd                               
    2 root      20   0       0      0      0 S   0.0   0.0   0:00.01 kthreadd                              
    3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release                
    4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_g                       
    5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_p                       
    6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_                       
    7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns                       
    9 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-events_highpri           
    11 root      20   0       0      0      0 I   0.0   0.0   0:00.00 kworker/u4:0-ipv6_addrconf            
    12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_pe                       
    13 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_kthread                     
    14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_rude_kthread                
    15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_trace_kthread               
    16 root      20   0       0      0      0 S   0.0   0.0   0:00.02 ksoftirqd/0                           
    17 root      20   0       0      0      0 I   0.0   0.0   0:00.15 rcu_preempt                           
    18 root      rt   0       0      0      0 S   0.0   0.0   0:00.03 migration/0                           
    19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/0                         
    20 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/0                               
    21 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/1                               
    22 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/1  

##
🧠 Understanding

Real-time system activity

CPU / Memory usage

Kernel scheduling in action

##
🔹 TASK 6 — User Space Check

    whoami

##
    devops@devops-control:~$ whoami 
    devops

##
    id

##
    devops@devops-control:~$ id
    uid=1000(devops) gid=1000(devops) groups=1000(devops),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),101(lxd)

##
🧠 Understanding

You are a user in user space

Not root → limited privileges

##
🔹 TASK 7 — Permission Check (BREAK)

    cd /root

##
    devops@devops-control:~$ cd /root
    -bash: cd: /root: Permission denied

##
❌ Expected

Permission denied

##
🧠 Why?

/root belongs to root user

Kernel blocks access

##
🔹 TASK 8 — Elevate to Kernel-Level Permission

    sudo ls /root

##
    devops@devops-control:~$ sudo ls /root

##
🧠 Understanding

sudo = temporary root privilege

Kernel now allows access

##
🔹 TASK 9 — Observe System Calls (VERY IMPORTANT)

    strace ls

##
    devops@devops-control:~$ strace ls
    execve("/usr/bin/ls", ["ls"], 0x7ffef3f628b0 /* 22 vars */) = 0
    brk(NULL)                               = 0x5d15f2b1f000
    mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7d77bc92a000
    access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
    openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
    fstat(3, {st_mode=S_IFREG|0644, st_size=22439, ...}) = 0
    mmap(NULL, 22439, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7d77bc924000
    close(3) 

##
📌 If not installed
    
    sudo apt install strace -y

##
🧠 Understanding

You will see:

open()

read()

write()

👉 These are system calls

👉 User space → Kernel communication

##
🔹 TASK 10 — System Uptime

    uptime

##
    devops@devops-control:~$ uptime 
    09:59:07 up  3:04,  1 user,  load average: 0.00, 0.00, 0.00

##
🧠 Understanding

System load

Running time

Kernel workload insight

##
🔹 TASK 11 — Multi-Node Verification (IMPORTANT)

👉 Now involve your lab nodes

##
📌 From devops-control → test connection

    ping -c 3 app-node

##
    devops@devops-control:~$ ping -c 3 app 
    PING app (192.168.122.175) 56(84) bytes of data.
    64 bytes from app (192.168.122.175): icmp_seq=1 ttl=64 time=1.06 ms
    64 bytes from app (192.168.122.175): icmp_seq=2 ttl=64 time=0.632 ms
    64 bytes from app (192.168.122.175): icmp_seq=3 ttl=64 time=0.594 ms

    --- app ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2031ms
    rtt min/avg/max/mdev = 0.594/0.760/1.055/0.208 ms

##
    ping -c 3 monitor-node

##
    devops@devops-control:~$ ping -c 3 monitor 
    PING monitor (192.168.122.202) 56(84) bytes of data.
    64 bytes from monitor (192.168.122.202): icmp_seq=1 ttl=64 time=0.551 ms
    64 bytes from monitor (192.168.122.202): icmp_seq=2 ttl=64 time=0.566 ms
    64 bytes from monitor (192.168.122.202): icmp_seq=3 ttl=64 time=0.506 ms

    --- monitor ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2064ms
    rtt min/avg/max/mdev = 0.506/0.541/0.566/0.025 ms

##
📌 SSH test (passwordless)

    ssh app-node

##
    devops@devops-control:~$ ssh app
    Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-111-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/pro


##
    ssh monitor-node

##
    devops@devops-control:~$ ssh monitor 
    Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-111-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/pro


##
🧠 Understanding

OS is managing:

    Network stack

    Remote access

Kernel handles:

    TCP/IP communication

##
🔥 MINI DEBUG THINKING (WRITE THIS)

Answer in your notes:

Why /root access failed?

    Because the user does not haev the permisson. that belongs to root user only.

What exactly does sudo change?

    This will make the permission like root user.

What is kernel doing in top?

    Kernel's work is shown in the CPU usage.

What are system calls in strace?

    To observe system calls

How does SSH work between nodes?

    SSH work between the machines, because of the key-based authentication we create in the host machine, from where we could to connect the machines.

👉 This builds real DevOps mindset