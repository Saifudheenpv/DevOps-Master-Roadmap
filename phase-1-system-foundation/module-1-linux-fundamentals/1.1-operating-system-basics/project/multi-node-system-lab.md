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

ssh app-node
hostname
exit
ssh monitor-node
hostname
exit
🧠 Goal
Ensure network + SSH working
OS networking stack verified
🧱 STEP 2 — Create User on app-node

👉 Work on: devops-control

ssh app-node

Now inside app-node:

sudo useradd devuser
sudo passwd devuser
🧠 Understanding
User created in /etc/passwd
Kernel registers identity
🧱 STEP 3 — Switch User
su - devuser
whoami
🧠 You are now:

👉 In user space (restricted)

🧱 STEP 4 — Create Application File
touch app.log
echo "App started" > app.log
cat app.log
🧠 What happens
File written via kernel → disk
🧱 STEP 5 — BREAK PERMISSION (CRITICAL)
chmod 000 app.log

Now try:

cat app.log
❌ Expected

Permission denied

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

Check file:

ls -l app.log
cat app.log
❌ Still fails
🧠 Understanding
Issue is not user-specific
Issue is file permission (kernel-level)
🧱 STEP 7 — FIX ISSUE

👉 Go to app-node as root

sudo chmod 644 app.log

Now test:

cat app.log
✅ Works
🧠 Lesson
Kernel enforces permissions globally
Fixing permission resolves issue for all users
🧱 STEP 8 — PROCESS CREATION (APP SIMULATION)

👉 On app-node:

sleep 500 &

Check:

ps aux | grep sleep
🧠 Understanding
Process created
Kernel managing lifecycle
🧱 STEP 9 — BREAK PROCESS (SIMULATE FAILURE)
kill <PID>
🧠 Result
App stopped
Kernel removed process
🧱 STEP 10 — DEBUG FROM CONTROL NODE

👉 Back to devops-control

ssh app-node
ps aux | grep sleep
❌ No process
🧠 Debug Thinking
App is not running
Need to restart
🧱 STEP 11 — SYSTEM CALL OBSERVATION
strace ls
🧠 Understanding
open(), read(), write()
User space → Kernel communication
🔥 FINAL DEBUG SCENARIO (REAL THINKING)
❗ Problem:

User says:
👉 “App not working”

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