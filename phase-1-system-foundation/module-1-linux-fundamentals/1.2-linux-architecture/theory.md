#
**📘 PHASE 1 — MODULE 1.2**

**🧠 PART 1 — LINUX ARCHITECTURE (FULL THEORY — CLEAN NOTES)**

##
**🔹 Lab Instruction for This Part**

👉 **Work on: devops-control**
👉 Only understanding — no commands now

🔹 What is Linux Architecture?
📌 Simple Definition

Linux architecture is:
👉 How the Linux system is structured internally

It shows:

How components are connected
How data flows inside the system
🧠 Big Picture (VERY IMPORTANT)

Linux is divided into layers:

User
 ↓
Applications
 ↓
Shell
 ↓
System Libraries
 ↓
Kernel
 ↓
Hardware

👉 Everything flows top → down → top

🔹 1. Kernel (CORE OF SYSTEM)
🧠 What is Kernel?

Kernel is:
👉 The heart of Linux

It directly controls:

CPU
Memory
Disk
Network
🔥 Kernel Responsibilities
1. Process Management
Runs programs
Schedules CPU
2. Memory Management
Allocates RAM
Prevents conflicts
3. Device Management
Controls hardware devices
4. File System Management
Reads/writes files
5. System Calls
Interface between apps and hardware
⚠️ Important

👉 Kernel runs in kernel space
👉 Full control, high risk

🔹 2. Shell (USER INTERFACE)
🧠 What is Shell?

Shell is:
👉 Interface between user and kernel

It takes your commands and:
➡️ Sends them to kernel

📌 Example

You type:

ls

Flow:

Shell receives command
Shell processes it
Sends request to kernel
Kernel executes
Output returned
🧾 Types of Shells
bash (default)
sh
zsh
⚡ Key Role

👉 Shell = command interpreter

🔹 3. System Libraries
🧠 What are System Libraries?

System libraries are:
👉 Pre-written code that programs use

They help:

Applications communicate with kernel
Avoid writing low-level code
📌 Example

Instead of writing:

complex system calls

Apps use:

library functions
🔄 Flow

Application → Library → System Call → Kernel

🧠 Why Important?
Makes development easier
Standard way to interact with OS
Improves efficiency
🔹 4. Utilities (SYSTEM TOOLS)
🧠 What are Utilities?

Utilities are:
👉 Built-in tools/commands in Linux

📌 Examples
ls → list files
cp → copy files
mv → move files
ps → process list
top → system monitor
⚡ Key Idea

👉 Utilities = daily working tools

🧠 HOW EVERYTHING WORKS TOGETHER (VERY IMPORTANT)
🔄 Full Flow Example

Command:

ls
Internal Flow:
User types command
Shell receives input
Shell calls utility (ls)
Utility uses system libraries
Libraries use system calls
Kernel accesses hardware
Result returned back
🔥 Visual Flow
User
 ↓
Shell
 ↓
Utility (ls)
 ↓
System Libraries
 ↓
Kernel
 ↓
Hardware
🧠 FINAL UNDERSTANDING (MUST BE CLEAR)

After this module, you must know:

Kernel = core control
Shell = command interface
Libraries = bridge
Utilities = tools

👉 All work together as a system