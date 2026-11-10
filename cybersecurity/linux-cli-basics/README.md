# Linux CLI Basics — TryHackMe

**Status:** Completed  
**Platform:** TryHackMe  
**Focus:** Terminal navigation, file discovery, reading text files, and basic Linux system information.

## Overview

The Linux terminal is a text-based interface for interacting with an operating system through commands. It supports efficient navigation and direct access to system information, which are useful foundations for security analysis and administration.

## Navigation and file discovery

| Command | Purpose |
| --- | --- |
| `pwd` | Print the current working directory |
| `ls` | List files and directories |
| `ls -l` | Show a detailed listing, including permissions, ownership, size and timestamps |
| `ls -al` | Include hidden entries in the detailed listing |
| `cd Documents` | Enter a directory |
| `cd ..` | Move to the parent directory |
| `find ~ -name mission_brief.txt` | Search the home directory recursively for a filename |
| `cat mission_brief.txt` | Display a text file's contents |

Linux names beginning with a dot (`.`) are hidden by default from ordinary directory listings; they are not inherently secret.

### Observed exercise: locating the mission brief

Used `find` to locate `mission_brief.txt` and navigated to its containing directory before reading it with `cat`. The file contained the next assignment: identify the logged-in user, kernel version, total disk space, and Linux distribution.

This exercise demonstrates how to find a file when only its name is known, then inspect its contents without relying on a graphical file manager.

## Inspecting the Linux environment

| Command | Information |
| --- | --- |
| `whoami` | Current effective username |
| `uname` | Kernel name (for example, `Linux`) |
| `uname -a` | Kernel name, hostname, kernel release and other system details |
| `df -h` | Mounted filesystem capacity, used space, available space and utilization in human-readable units |
| `cd /etc` | Navigate to system configuration and information files |
| `cat os-release` | Read Linux distribution identification information from `/etc/os-release` |

### Interpreting system information

- **Kernel vs distribution:** `uname` reports kernel information; `/etc/os-release` identifies the installed Linux distribution.
- **Architecture:** `x86_64` indicates a 64-bit x86 environment.
- **Disk usage:** `df -h` includes filesystem size, used and available capacity, percentage used, and mount point.
- **Temporary filesystems:** `tmpfs` is a memory-backed filesystem and should not be confused with physical disk capacity.

The room's sample `/etc/os-release` output identified **Ubuntu 24.04.1 LTS (Noble Numbat)**.

## Final exercise

The room concluded with a mini challenge to locate `day1_report.txt` under the home directory, navigate to its directory, and read it using `cat`.

## Security relevance

These commands support initial Linux host inspection, locating evidence files, identifying system versions, and checking storage before log collection or analysis. They form the foundation for more advanced command-line investigation and administration.
