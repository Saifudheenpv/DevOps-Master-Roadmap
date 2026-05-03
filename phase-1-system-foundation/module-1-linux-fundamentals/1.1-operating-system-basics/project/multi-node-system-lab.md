#
🚀 PHASE 1 — MODULE 1.1

🧪 PART 3 — REAL PROJECT (MULTI-NODE + BREAK + FIX)

##
🔹 Project Goal

You will:

    Use your 3-node lab
    
    Understand OS, Kernel, User Space practically
    
    Break real things
    
    Fix using logic (not guessing)

##
🧠 Lab Usage Plan

    Machine	            Role
    
    devops-control	    Control + Debug
    
    app-node	        Application server
    
    monitor-node	    Monitoring / Observer

##
🔥 PROJECT NAME

🖥️ “Multi-Node OS Behavior & Debug Lab”

##
🧱 STEP 1 — Verify All Nodes

👉 Work on: devops-control

    ping -c 2 app-node

#
    devops@devops-control:~$ ping -c 2 app
    PING app (192.168.122.175) 56(84) bytes of data.
    64 bytes from app (192.168.122.175): icmp_seq=1 ttl=64 time=0.799 ms
    64 bytes from app (192.168.122.175): icmp_seq=2 ttl=64 time=0.573 ms

    --- app ping statistics ---
    2 packets transmitted, 2 received, 0% packet loss, time 1000ms
    rtt min/avg/max/mdev = 0.573/0.686/0.799/0.113 ms

#
    ping -c 2 monitor-node

#
    devops@devops-control:~$ ping -c 2 monitor 
    PING monitor (192.168.122.202) 56(84) bytes of data.
    64 bytes from monitor (192.168.122.202): icmp_seq=1 ttl=64 time=0.734 ms
    64 bytes from monitor (192.168.122.202): icmp_seq=2 ttl=64 time=0.547 ms

    --- monitor ping statistics ---
    2 packets transmitted, 2 received, 0% packet loss, time 1009ms
    rtt min/avg/max/mdev = 0.547/0.640/0.734/0.093 ms

#
    ssh app-node
    hostname
    exit

#
    devops@devops-control:~$ ssh app
    Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-111-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/pro

    System information as of Sun May  3 10:41:44 AM UTC 2026

    System load:  0.0                Processes:               141
    Usage of /:   46.9% of 11.21GB   Users logged in:         1
    Memory usage: 7%                 IPv4 address for enp1s0: 192.168.122.175
    Swap usage:   0%

    * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
    just raised the bar for easy, resilient and secure K8s cluster deployment.

    https://ubuntu.com/engage/secure-kubernetes-at-the-edge

    Expanded Security Maintenance for Applications is not enabled.

    0 updates can be applied immediately.

    Enable ESM Apps to receive additional future security updates.
    See https://ubuntu.com/esm or run: sudo pro status


    Last login: Sun May  3 10:27:37 2026 from 192.168.***.*
    devops@app-node:~$ hostname
    app-node
    devops@app-node:~$ exit
    logout
    Connection to app closed.

#
    ssh monitor-node
    hostname
    exit

#
    devops@devops-control:~$ ssh monitor 
    Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-111-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/pro

    System information as of Sun May  3 10:43:22 AM UTC 2026

    System load:  0.0                Processes:               136
    Usage of /:   46.9% of 11.21GB   Users logged in:         1
    Memory usage: 7%                 IPv4 address for enp1s0: 192.168.122.202
    Swap usage:   0%


    Expanded Security Maintenance for Applications is not enabled.

    0 updates can be applied immediately.

    Enable ESM Apps to receive additional future security updates.
    See https://ubuntu.com/esm or run: sudo pro status


    Last login: Sun May  3 10:27:46 2026 from 192.168.***.*
    devops@monitor-node:~$ hostname
    monitor-node
    devops@monitor-node:~$ exit
    logout
    Connection to monitor closed.

##
🧠 Goal

Ensure network + SSH working

OS networking stack verified

##
🧱 STEP 2 — Create User on app-node

👉 Work on: devops-control

    ssh app-node

#
    devops@devops-control:~$ ssh app 
    Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-111-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/pro

    System information as of Sun May  3 10:45:35 AM UTC 2026

    System load:  0.0                Processes:               139
    Usage of /:   46.9% of 11.21GB   Users logged in:         1
    Memory usage: 7%                 IPv4 address for enp1s0: 192.168.122.175
    Swap usage:   0%

    * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
    just raised the bar for easy, resilient and secure K8s cluster deployment.

    https://ubuntu.com/engage/secure-kubernetes-at-the-edge

    Expanded Security Maintenance for Applications is not enabled.

    0 updates can be applied immediately.

    Enable ESM Apps to receive additional future security updates.
    See https://ubuntu.com/esm or run: sudo pro status


    Last login: Sun May  3 10:41:44 2026 from 192.168.***.*

Now inside app-node:

#
    sudo useradd devuser
    sudo passwd devuser

#
    devops@app-node:~$ sudo useradd devuser
    [sudo] password for devops: 
    devops@app-node:~$ sudo passwd devuser 
    New password: 
    Retype new password: 
    passwd: password updated successfully

##
🧠 Understanding

User created in /etc/passwd

Kernel registers identity

##
🧱 STEP 3 — Switch User

    su - devuser
    whoami

#
    devops@app-node:~$ su - devuser 
    Password: 
    $ whoami
    devuser
    $ 

##
🧠 You are now:

👉 In user space (restricted)

##
🧱 STEP 4 — Create Application File

    touch app.log
    echo "App started" > app.log
    cat app.log

#
    $ touch app.log
    $ ls
    app.log
    $ echo "App started" > app.log	
    $ cat app.log
    App started
    $ 

##
🧠 What happens

File written via kernel → disk

##
🧱 STEP 5 — BREAK PERMISSION (CRITICAL)

    chmod 000 app.log

Now try:

    cat app.log

#
    $ chmod 000 app.log
    $ cat app.log
    cat: app.log: Permission denied

##
❌ Expected

Permission denied

##
🧠 Why

Kernel blocks access

No read permission

🧱 STEP 6 — DEBUG FROM monitor-node

👉 Exit to control:

    exit

👉 Work on: monitor-node

    ssh monitor-node

Now try:

    ssh app-node

##
Check file:

    ls -l /home/devuser/app.log
    cat /home/devuser/app.log

#
    devops@app-node:~$ ls -l /home/devuser/
    total 4
    ---------- 1 devuser devuser 12 May  3 10:54 app.log
    devops@app-node:~$ cat /home/devuser/app.log 
    cat: /home/devuser/app.log: Permission denied
    devops@app-node:~$ 

❌ Still fails

##
🧠 Understanding

Issue is not user-specific

Issue is file permission (kernel-level)

##
🧱 STEP 7 — FIX ISSUE

👉 Go to app-node as root

    sudo chmod 644 /home/devuser/app.log

Now test:

    cat /home/devuser/app.log

#
    root@app-node:~# sudo chmod 644 /home/devuser/app.log
    root@app-node:~# cat /home/devuser/app.log 
    App started
    root@app-node:~# 

##
✅ Works

##
🧠 Lesson

Kernel enforces permissions globally

Fixing permission resolves issue for all users

##
🧱 STEP 8 — PROCESS CREATION (APP SIMULATION)

👉 On app-node:

    sleep 500 &

#
    devops@app-node:~$ sleep 500 &
    [1] 1945

##
Check:

    ps aux | grep sleep

#
    devops@app-node:~$ ps aux | grep sleep
    devops      1945  0.0  0.0   5684  2104 pts/1    S    11:07   0:00 sleep 500
    devops      1949  0.0  0.0   6544  2328 pts/1    S+   11:07   0:00 grep --color=auto sleep

##
🧠 Understanding

Process created

Kernel managing lifecycle

##
🧱 STEP 9 — BREAK PROCESS (SIMULATE FAILURE)

    kill <PID>

#
    devops@app-node:~$ kill 1945
    devops@app-node:~$ ps aux | grep sleep
    devops      1951  0.0  0.0   6544  2296 pts/1    S+   11:09   0:00 grep --color=auto sleep
    [1]+  Terminated              sleep 500

##
🧠 Result

App stopped

Kernel removed process

##
🧱 STEP 10 — DEBUG FROM CONTROL NODE

👉 Back to devops-control

    ssh app-node
    ps aux | grep sleep

##
❌ No process

##
🧠 Debug Thinking

App is not running

Need to restart

##
🧱 STEP 11 — SYSTEM CALL OBSERVATION

    strace ls

#
    devops@app-node:~$ strace ls
    execve("/usr/bin/ls", ["ls"], 0x7fff96d74d40 /* 22 vars */) = 0
    brk(NULL)                               = 0x5c209ebf6000
    mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7149e2d21000
    access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
    openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
    fstat(3, {st_mode=S_IFREG|0644, st_size=22439, ...}) = 0
    mmap(NULL, 22439, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7149e2d1b000
    close(3)                                = 0
    openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
    read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
    fstat(3, {st_mode=S_IFREG|0644, st_size=174472, ...}) = 0
    mmap(NULL, 181960, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7149e2cee000
    mmap(0x7149e2cf4000, 118784, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x7149e2cf4000
    mmap(0x7149e2d11000, 24576, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x23000) = 0x7149e2d11000
    mmap(0x7149e2d17000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x29000) = 0x7149e2d17000
    mmap(0x7149e2d19000, 5832, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7149e2d19000
    close(3)                                = 0
    openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
    read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\220\243\2\0\0\0\0\0"..., 832) = 832
    pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
    fstat(3, {st_mode=S_IFREG|0755, st_size=2125328, ...}) = 0
    pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
    mmap(NULL, 2170256, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7149e2a00000
    mmap(0x7149e2a28000, 1605632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x28000) = 0x7149e2a28000
    mmap(0x7149e2bb0000, 323584, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b0000) = 0x7149e2bb0000
    mmap(0x7149e2bff000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1fe000) = 0x7149e2bff000
    mmap(0x7149e2c05000, 52624, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7149e2c05000
    close(3)                                = 0
    openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpcre2-8.so.0", O_RDONLY|O_CLOEXEC) = 3
    read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
    fstat(3, {st_mode=S_IFREG|0644, st_size=625344, ...}) = 0
    mmap(NULL, 627472, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7149e2c54000
    mmap(0x7149e2c56000, 450560, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x2000) = 0x7149e2c56000
    mmap(0x7149e2cc4000, 163840, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x70000) = 0x7149e2cc4000
    mmap(0x7149e2cec000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x97000) = 0x7149e2cec000
    close(3)                                = 0
    mmap(NULL, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7149e2c51000
    arch_prctl(ARCH_SET_FS, 0x7149e2c51800) = 0
    set_tid_address(0x7149e2c51ad0)         = 2031
    set_robust_list(0x7149e2c51ae0, 24)     = 0
    rseq(0x7149e2c52120, 0x20, 0, 0x53053053) = 0
    mprotect(0x7149e2bff000, 16384, PROT_READ) = 0
    mprotect(0x7149e2cec000, 4096, PROT_READ) = 0
    mprotect(0x7149e2d17000, 4096, PROT_READ) = 0
    mprotect(0x5c205fe1b000, 8192, PROT_READ) = 0
    mprotect(0x7149e2d59000, 8192, PROT_READ) = 0
    prlimit64(0, RLIMIT_STACK, NULL, {rlim_cur=8192*1024, rlim_max=RLIM64_INFINITY}) = 0
    munmap(0x7149e2d1b000, 22439)           = 0
    statfs("/sys/fs/selinux", 0x7fff02cbffb0) = -1 ENOENT (No such file or directory)
    statfs("/selinux", 0x7fff02cbffb0)      = -1 ENOENT (No such file or directory)
    getrandom("\x65\xc8\x2a\x99\xe7\x55\x1d\xc1", 8, GRND_NONBLOCK) = 8
    brk(NULL)                               = 0x5c209ebf6000
    brk(0x5c209ec17000)                     = 0x5c209ec17000
    openat(AT_FDCWD, "/proc/filesystems", O_RDONLY|O_CLOEXEC) = 3
    fstat(3, {st_mode=S_IFREG|0444, st_size=0, ...}) = 0
    read(3, "nodev\tsysfs\nnodev\ttmpfs\nnodev\tbd"..., 1024) = 400
    read(3, "", 1024)                       = 0
    close(3)                                = 0
    access("/etc/selinux/config", F_OK)     = -1 ENOENT (No such file or directory)
    openat(AT_FDCWD, "/usr/lib/locale/locale-archive", O_RDONLY|O_CLOEXEC) = 3
    fstat(3, {st_mode=S_IFREG|0644, st_size=3055776, ...}) = 0
    mmap(NULL, 3055776, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7149e2600000
    close(3)                                = 0
    ioctl(1, TCGETS, {c_iflag=ICRNL|IXON|IUTF8, c_oflag=NL0|CR0|TAB0|BS0|VT0|FF0|OPOST|ONLCR, c_cflag=B38400|CS8|CREAD, c_lflag=ISIG|ICANON|ECHO|ECHOE|ECHOK|IEXTEN|ECHOCTL|ECHOKE, ...}) = 0
    ioctl(1, TIOCGWINSZ, {ws_row=29, ws_col=109, ws_xpixel=0, ws_ypixel=0}) = 0
    openat(AT_FDCWD, ".", O_RDONLY|O_NONBLOCK|O_CLOEXEC|O_DIRECTORY) = 3
    fstat(3, {st_mode=S_IFDIR|0750, st_size=4096, ...}) = 0
    getdents64(3, 0x5c209ebfcce0 /* 9 entries */, 32768) = 288
    getdents64(3, 0x5c209ebfcce0 /* 0 entries */, 32768) = 0
    close(3)                                = 0
    close(1)                                = 0
    close(2)                                = 0
    exit_group(0)                           = ?
    +++ exited with 0 +++

##
🧠 Understanding

open(), read(), write()

User space → Kernel communication

##
🔥 FINAL DEBUG SCENARIO (REAL THINKING)

❗ Problem:

User says:

👉 “App not working”

##
🧠 Your Debug Flow

Check process:

    ps aux

Check file:

    ls -l app.log

Check user:

    whoami

Fix:

    chmod 644 app.log

or restart:

     sleep 500 &

##
👉 This is real DevOps debugging mindset