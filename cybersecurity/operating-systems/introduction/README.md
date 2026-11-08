# Operating Systems: Introduction — TryHackMe

**Status:** Completed  
**Date:** 8 November 2026  
**Focus:** OS architecture, system resource management, security, interfaces, and operating system families

## What an operating system does

An **operating system (OS)** coordinates applications, users, and physical hardware. It provides a common environment so each application does not need to directly manage the CPU, memory, storage, devices, and security independently.

The OS handles resource allocation and separates privileged system operations from restricted application execution.

## Five core operating system responsibilities

| Responsibility | Main functions | Example |
| --- | --- | --- |
| **Process management** | Create, schedule, prioritize, and terminate processes; allocate CPU time | Running a browser and music player at the same time |
| **Memory management** | Allocate and isolate process memory, reclaim RAM, and use virtual memory when needed | Multiple applications using RAM independently |
| **File system management** | Manage directories, paths, permissions, file names, and metadata | Saving files or setting read-only permissions |
| **User management** | Manage identities, authentication, and account permissions | Logging in and restricting access to user files |
| **Device management** | Load drivers and abstract device-specific hardware operations | Interacting with a mouse, printer, or external drive |

## OS security fundamentals

An OS provides foundational security controls before additional security tools are installed:

- **Authentication:** Verify identity with credentials or biometrics.
- **Permissions:** Control read, write, and execute access for users and applications.
- **Isolation:** Separate processes and distinguish restricted user space from privileged kernel space.
- **System protection:** Restrict unauthorized changes to important system files and settings.

### Kernel space and user space

**Kernel space** contains highly privileged system functionality that manages hardware and resources. **User space** is where ordinary applications execute with more restricted privileges. The separation reduces conflicts and limits unauthorized access to sensitive system operations.

## Operating system interfaces

| Interface | Interaction | Strengths |
| --- | --- | --- |
| **GUI (Graphical User Interface)** | Windows, icons, folders, and menus | Visual navigation and familiar interaction |
| **CLI (Command-Line Interface)** | Typed commands and syntax | Precision, control, and efficient advanced operations |

Both interfaces can display the same information, such as the contents of a user's home directory. In Linux, `ls` lists directory contents.

## Five categories of operating systems

| Category | Typical environments | Design priorities |
| --- | --- | --- |
| **Desktop** | Personal computers, gaming, office work | Rich GUI and multitasking |
| **Server** | Web hosting, databases, backend services | Uptime, remote administration, multi-user access, often headless |
| **Mobile** | Phones and tablets | Touch interface, power efficiency, application sandboxing |
| **Embedded** | Routers, vehicles, appliances, IoT | Small footprint and limited hardware requirements |
| **Virtual / Cloud** | VMs, cloud instances, container platforms | Rapid deployment, scalability, lightweight operation |

### Examples introduced in the room

- **Desktop:** Windows, macOS, Linux distributions such as Ubuntu, Debian, and Fedora.
- **Server:** Windows Server, Ubuntu Server, Debian, Red Hat, and Unix variants such as IBM AIX and Oracle Solaris.
- **Mobile:** Android and iOS.
- **Embedded / real-time:** OpenWrt, Ubuntu Core, Yocto Project, FreeRTOS, VxWorks, QNX.
- **Cloud / container-oriented:** Ubuntu LTS, Amazon Linux, Rocky Linux, Alpine Linux, Bottlerocket, Flatcar Linux.

## System information and file systems

The TryHackMe environment's **About This Computer** screen showed:

| Property | Observed value |
| --- | --- |
| Operating system | Ubuntu 24.04.1 LTS (Noble Numbat), 64-bit |
| Kernel | Linux 6.8.0-1016-aws x86_64 |
| Desktop environment | MATE 1.26.2 |
| Memory | 1.9 GiB |
| Processor | AMD EPYC 7571 × 2 |
| Available disk space | 9.1 GB |

The **System Monitor → File Systems** view identified the `/dev/root` device, mounted at `/`, as **`ext4`**, the fourth extended file system used in Linux.

## Security relevance

Understanding OS processes, memory, file permissions, identities, device drivers, and user/kernel separation provides a foundation for host security administration and analyzing system behavior.

## Key takeaways

1. The OS mediates between users, applications, and hardware.
2. Process, memory, file system, user, and device management are its core duties.
3. Security begins with authentication, permissions, isolation, and protected system resources.
4. GUI and CLI are different interfaces to the same operating system.
5. OS designs vary according to device purpose and workload.
