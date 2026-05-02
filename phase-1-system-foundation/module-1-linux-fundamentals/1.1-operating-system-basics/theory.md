📘 PHASE 1 — MODULE 1.1

🧠 PART 1 — OPERATING SYSTEM BASICS (FULL THEORY — CLEAN NOTES)

##
🔹 Lab Instruction for This Part

👉 Work on: devops-control (your main machine)

👉 No commands needed now — only understanding

##
🔹 1. What is an Operating System (OS)?

📌 Simple Definition

An Operating System (OS) is a software that:
    
    • Controls hardware 
    
    • Runs programs 
    
    • Connects user and machine 

##
🧠 Deep Understanding

A computer has only hardware:

    • CPU → processes data 

    • RAM → stores temporary data 

    • Disk → stores files 

👉 Hardware alone is useless without control

The OS acts as:

➡️ Controller + Manager + Interface

##
🔄 Real Flow (Important)

When you run a command:

    ls


What happens internally:

    1. You type command (user) 

    2. Shell receives input 

    3. OS processes request 

    4. Kernel accesses disk 

    5. Output is returned 

    6. You see result 

👉 OS is always in the middle

##
🎯 Core Responsibilities of OS

1. Process Management

        • Runs programs (called processes) 

        • Handles multiple tasks at once 

##
2. Memory Management

        • Allocates RAM 

        • Prevents apps from interfering 

##
3. File System Management

        • Stores files 

        • Organizes directories 

##
4. Device Management

    • Controls: 

        ◦ Keyboard 

        ◦ Disk 

        ◦ Network

##
5. Security & Permissions

        • Controls access 

        • Protects system 

##
🧠 Real-Life Analogy

    Component	      Role

    • Hardware	      Workers

    • User	          Boss

    • OS	          Manager

👉 Without OS → system chaos

👉 With OS → structured system

##
🔹 2. Kernel vs User Space (VERY IMPORTANT)

This is core DevOps concept — understand deeply.

##
🧠 What is Kernel?

📌 Definition

Kernel is the core part of OS

👉 It directly controls:

    • CPU 

    • Memory 

    • Devices 

##
🔥 Responsibilities of Kernel

    • Process scheduling 

    • Memory allocation 

    • Hardware communication 

    • System calls handling 

👉 Kernel = low-level control layer

##
🧠 What is User Space?

User space is where:

    • Applications run 

    • Users interact 

Examples:

    • Terminal 

    • Python scripts 

    • Nginx 

    • Applications 

##
⚖️ Kernel vs User Space

      Feature	          Kernel Space    	                User Space

    • Access              Full hardware access	            Limited

    • Risk	              Dangerous (can crash system)	    Safe

    • Runs	              Core OS	                        Applications

    • Control	          Direct	                        Indirect

##
🔄 How They Work Together

Flow:

    User → Application → Kernel → Hardware → Kernel → Application → User

##
🧩 Example

Command:

    cat file.txt


Flow:

    1. Runs in user space 

    2. Sends request to kernel 

    3. Kernel reads disk 

    4. Returns data 

    5. Output shown 

##
🔐 System Calls (VERY IMPORTANT)

Applications cannot directly access hardware.

They use:

👉 System Calls

Examples:

    • open() 

    • read() 

    • write() 

👉 These are controlled entry points to kernel

##
⚠️ Why Separation Exists?

If no separation:

    • System crashes 

    • Security issues 

    • Data corruption 

👉 Kernel protects system stability

##
🔹 3. Types of Operating Systems

##
🪟 1. Desktop OS

Used for personal systems

Examples:

    • Microsoft Windows 

    • macOS 

👉 GUI-based systems

##
🐧 2. Linux-Based OS

Examples:

    • Ubuntu 

    • CentOS 

    • Red Hat Enterprise Linux 

👉 Used in:

    • Servers 

    • Cloud 

    • DevOps 

##
🏢 3. Server OS

Optimized for:

    • Performance 

    • Stability 

    • Networking 

Examples:

    • Linux servers 

    • Windows Server 

##
📱 4. Mobile OS

Examples:

    • Android 

    • iOS 

##
🧠 Key Insight

👉 Linux dominates:

    • Servers 

    • Cloud 

    • DevOps 

##
🔹 4. What Linux Actually Is (CRITICAL UNDERSTANDING)

##
❌ Wrong Thinking

“Linux = Ubuntu”

    • 👉 Incorrect

##
✅ Correct Understanding

🧠 Linux = Kernel

Linux is:

    • 👉 Only the kernel

Created by:

    • 👉 Linus Torvalds

##
📦 What is Ubuntu?

Ubuntu is:

    • 👉 Linux Kernel + tools + software

##
🧱 Full Linux System =

    • Kernel (Linux) 

    • Shell (bash) 

    • Utilities (ls, cp, etc.) 

    • Package manager 

    • Optional GUI 

👉 This full package is called:

➡️ Distribution (Distro)

##
📌 Examples of Distros

    • Ubuntu 

    • Debian 

    • Fedora 

    • Arch Linux 

##
🚗 Real Analogy

      Component	 Example

    • Kernel	 Engine

    • Distro	 Full Car

👉 Kernel alone ≠ usable system

👉 Distro = complete OS

##
🧠 FINAL UNDERSTANDING (MUST BE CLEAR)

After this:

    • OS = system controller 

    • Kernel = core of OS 

    • User space = where apps run 

    • Linux = kernel only 

    • Ubuntu = Linux + tools