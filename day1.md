1️⃣ Linux Core Architecture - User space requests services, kernel executes them, hardware performs the actual work.

+------------------------------------------------+
|                User Space                      |
|                                                |
|  Apps  |  Shell  |  Commands  |  Services      |
| (nginx |  bash   |  ls, ps    |  docker)       |
+---------------------↑--------------------------+
|                  Kernel                        |
|                                                |
|  Process Mgmt | Memory Mgmt | File System     |
|  CPU Sched    | Virtual Mem | Device Drivers  |
+---------------------↑--------------------------+
|                  Hardware                      |
|         CPU | RAM | Disk | Network             |
+------------------------------------------------+

2️⃣ Linux Boot → systemd Flow - systemd is the first userspace process started by the kernel.

Power ON
   |
   v
BIOS / UEFI
   |
   v
Bootloader (GRUB)
   |
   v
Kernel Loaded
   |
   v
systemd (PID 1)
   |
   +--> sshd
   +--> nginx
   +--> docker
   +--> cron

3️⃣ Process Creation Diagram (fork & exec) - A process is created using fork and exec system calls.

User runs command: ls
        |
        v
     Shell (bash)
        |
        v
      fork()
        |
        v
      exec()
        |
        v
   New Process (PID)

4️⃣ Process State Diagram (Simple & Clear) - Zombie processes are terminated but not cleaned up by the parent.

           +---------+
        | Running |
        +----+----+
             |
             v
        +---------+
        | Sleeping|
        +----+----+
             |
             v
        +---------+
        | Zombie  |
        +---------+

5️⃣ systemd Role Diagram (Service Management) - systemd manages services, dependencies, logging, and system targets.

               systemd (PID 1)
                     |
    ------------------------------------
    |        |         |               |
  nginx    sshd     docker           cron

6️⃣ User Command → Kernel → Hardware Flow - Applications never access hardware directly; the kernel acts as a bridge.

                    ls command
                        |
                        v
                    Shell (bash)
                        |
                        v 
                    System Call
                        |
                        v
                    Kernel
                        |
                        v
                    Disk / CPU

⭐ 30-Second Interview Summary (Memorize This)

Linux has three main layers: user space, kernel, and hardware.
systemd is the first process started by the kernel and manages all services.
Processes are created using fork and exec, and the kernel manages CPU, memory, and I/O.