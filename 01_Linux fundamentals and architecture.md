# 1. Linux fundamentals and architecture

Linux architecture forms the foundation of modern bioinformatics and precision medicine computing. Understanding its core components and how they interact is crucial for developing robust medical applications and handling sensitive patient data securely.

Before you start with the lesson, make sure that you have the following ready:
1. Download and install VMWare: https://www.techspot.com/downloads/189-vmware-workstation-for-windows.html
2. Download Ubuntu Lite (Free): https://www.linuxliteos.com/index.html (linux-lite-7.2-64bit.iso)

*If you know how to set up Ubuntu Lite, please feel free to go ahead and set it up. It should be quite straightforward*


## 1.1. Core architecture 

### 1.1.1. Kernel 

The kernel is the core component of Linux that manages hardware resources and provides essential services. It acts as an intermediary between hardware and software.

**The key responsibilities:**

- Memory management (crucial for handling large genomic datasets)
- Process scheduling (managing multiple analysis pipelines)
- Device management (sequencing machines, storage devices)
- System calls & security (protecting patient data)

Here are some of the commands:

```
# View kernel information
uname -a                 # Show all kernel information
uname -r                 # Show kernel release version
dmesg                    # Display kernel ring buffer messages
sysctl -a                # Show all kernel parameters
cat /proc/version        # Show kernel version details
```

### 1.1.2. Shell

The shall is the command interpreter that provides user interface to kernel services

**There are a few types of shells:**

- bash (Bourne Again Shell) - most common
- zsh (Z Shell) - enhanced features
- sh (Bourne Shell) - original Unix shell
- csh/tcsh (C Shell) - C-like syntax

Here are some of the commands:

```
# Shell information and manipulation
echo $SHELL             # Show current shell
cat /etc/shells         # List available shells
chsh -s /bin/bash       # Change default shell
ps -p $$                # Show current shell process
echo $0                  # Show shell name
```

### 1.1.3. User space 

The user space is where user applications and processes run. It is separated from kernel space for security and stability. 

**The user space contains:**

- User applications (medical imaging software, sequence analyzers)
- System utilities
- User data
- Configuration files

Here are some of the commands:

```
# User space operations
who                     # Show logged-in users
w                       # Show who is logged in and what they're doing
id                      # Show user and group IDs
whoami                  # Show current username
ps aux                  # Show user processes
```    

### 1.1.4. How are they all related? 

Think of a restaurant...

The **kernel** is like the kitchen, where all the actual work happens - only trained chefs (privileged instructions) can operate the equipment and handle raw ingredients (hardware). 

The ****user space** is like the dining area, where customers (applications) sit but can't directly access the kitchen. 

The **shell** acts as the waiter, taking orders from customers in plain language ("I want noodles"), translating them into kitchen terminology (system calls), and bringing back the prepared dishes (output) to the customers.

<p align="center">
  <img src="https://www.nutanixbible.com/imagesv2/user_vs_kernel_1.png" alt="Relationship between kernel, userspace and shell" width="500" height="400">
</p>

Image from [nutanixbible](https://www.nutanixbible.com/0-a-brief-lesson-in-history.html)

## 1.2. File system hierachy

The Filesystem Hierarchy Standard (FHS) is a crucial component of Linux/Unix systems that defines the directory structure and directory contents in Unix-like operating systems. It was created to provide consistency across different Linux distributions, making it easier for users and software to navigate the system.

- `/` (root): The top-level directory of the entire system
- `/bin`: Contains essential command-line binaries (programs) that need to be available for all users, like ls, cp, mv
- `/boot`: Contains files needed for booting the system, including the Linux kernel and bootloader configuration
- `/dev`: Contains device files that represent hardware components and drivers
- `/etc`: Stores system-wide configuration files
- `/home`: Personal directories for regular users, where they store their files and settings
- `/lib`: Contains essential shared libraries needed by programs in /bin and /sbin
- `/mnt`: A mount point for temporarily mounting other filesystems
- `/opt`: Optional software packages and third-party applications
- `/proc`: A virtual filesystem providing process and kernel information
- `/root`: Home directory for the root (administrator) user
- `/sbin`: System binaries, commands used for system administration
- `/tmp`: Temporary files that are cleared on reboot
- `/usr`: User programs, libraries, documentation, and source code
- `/var`: Variable data files like logs, mail spools, and temporary files that need to persist across reboots

If you are interested to know more, you can refer [here](https://www.geeksforgeeks.org/linux-file-hierarchy-structure/)

Here are some of the commands:

```
# Directory structure navigation
**ls /                    # List root directory contents
**du -sh /                # Show size of root directories
**du -h --max-depth=1     # First-level directory sizes
tree -L 1 /               # Show first level of directory tree
findmnt                   # Show mounted filesystems
df -h                     # Show disk space usage

# Common directory operations
ls /bin                  # List essential commands
ls /etc                  # List system configurations
ls /home                 # List user home directories
ls /var/log              # List system logs
```  

## 1.3. System components 

### 1.3.1. Process management 

Each process has a unique Process IDentifier. 
These processes can be:

**(a) Foreground (interactive)**
**(b) Background (automated analysis)**
**(c) Daemon (services e.g. internet connections)**
    - Usually end with 'd' in their name
    - For example:
  
      sshd (SSH daemon)
      httpd (HTTP daemon)
      systemd (system daemon)

### 1.3.2. Memory management 

Memory Management is a crucial function of operating systems that handles how memory is allocated, used, and freed. Here's a breakdown of each component:

**(a) Virtual memory system:**
**What is it:** A memory management technique that provides an abstraction of the physical memory

**Why is it needed:** If you have 8GB of RAM and try to run several large programs (like Chrome, Photoshop, and a game) that together need 12GB, virtual memory allows this by keeping the most-used 8GB in RAM and moving the less-used 4GB to disk. This allows the overcoming of physical memory size restrictions. 

**(b) Swap space:**
**What is it:** A portion of hard disk used as an extension of RAM

**Why is it needed:** When RAM becomes full, swap space prevents system crashes. It moves less-used memory pages to disk and allows programs to continue running even when RAM is exhausted

> [!NOTE]
> RAM (Random Access Memory) is a type of computer memory that temporarily stores data that the CPU (Central Processing Unit) needs immediate access to. It is a temporary storage that holds currently running programs and data.
> More RAM generally means you have a faster program loading, better multi-tasking, smoother system operation and less reliance on swap space. 

**(c) Memory allocation for large datasets :**
**What is it:** Memory Allocation for Large Datasets refers to how operating systems handle and manage large amounts of data in memory. The key aspects of such memory allocation includes dynamic memory allocation, memory fragmentation management, large pages support, memory mapping and caching strategies. 

**Why is it needed:** These different mechanisms work together to ensure sufficient memory utilization, fast data access, minimal memory waste and system stability with large datasets. 

### 1.4. Device management 

**(a) Device files in /dev**
**What is it:** The /dev directory contains special files called device files or device nodes. These files serve as interfaces to hardware devices and device drivers in the kernel. Each device file represents either a physical device (like hard drives, USB devices) or a virtual device (like /dev/null or /dev/random)

**Why is it needed:** This provides a standardized way for programs to communicate with hardware

**(b) Mounting storage devices**
**What is it:** Mounting is the process of making a storage device's filesystem accessible to the system. It attaches the device's filesystem to a specific directory (mount point) in the system's directory tree

**Why is it needed:** This makes storage device contents accessible to users and applications

**(c) Peripheral management**
**What is it:** This is a system for managing external devices like printers, scanners, cameras, etc. This includes device detection, driver loading, and configuration

**Why is it needed:** This enables plug-and-play functionality for devices

### 1.5. Job control and process management
Job control allows users to manage multiple processes running in their terminal session. There are two types of jobs:

**(a) Foreground jobs**
These jobs occupies the terminal session and receives input directly from the keyboard and outputs directly to the terminal. User must wait for the job to finish before entering new commands

**(b) Background jobs**
This runs independently of terminal sessions and does not ccept keyboard input. 

Here are some job management commands: 

```
#DO NOT TRY THESE COMMANDS
jobs              # List all background jobs with their job numbers
fg %n             # Bring job number n to foreground
bg %n             # Resume suspended job n in background
```

There are times when you need to terminate processes using these commands:

```
#DO NOT TRY THESE COMMANDS
kill -9 PID       # Force terminate process with given PID
                  # -9 is SIGKILL signal
pkill -f "pattern"# Kill processes matching pattern
                  # Useful for killing multiple related processes
```

You can monitor the processes using these commands

```
top               # Real-time process viewer
htop              # Enhanced version of top
ps aux            # Snapshot of current processes
```

