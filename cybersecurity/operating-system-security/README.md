# Operating System Security — TryHackMe

## Overview
Completed foundational training on operating system security, with emphasis on protecting confidentiality, integrity, and availability (CIA), identifying common access-control weaknesses, and understanding credential-based access to a Linux training system.

## Operating systems and security
An operating system mediates access between applications and hardware. Security matters because personal and organizational devices store confidential documents, communications, credentials, and other sensitive information.

| Principle | Security objective | Example risk |
| --- | --- | --- |
| Confidentiality | Restrict information to authorized people | Unauthorized reading of private files |
| Integrity | Prevent unauthorized changes to information | Altering a document without permission |
| Availability | Keep systems and information accessible when needed | Files rendered inaccessible by ransomware |

## Authentication and password weaknesses
Authentication verifies identity using:
- **Something you know:** password or PIN.
- **Something you are:** fingerprint.
- **Something you have:** a device receiving a verification code.

Weaknesses discussed included common passwords, keyboard patterns, passwords derived from personal information, and reuse across services. A password that is absent from a top-password list is not necessarily secure; predictable character substitutions can still be guessed. Prefer long, unique credentials and a password manager.

## File permissions and least privilege
The **principle of least privilege** limits users to the access needed for their responsibilities. Overly permissive read access threatens confidentiality; overly permissive write access threatens integrity. File permissions should reflect who needs to read or modify each resource.

## Malicious programs
- **Trojan horses:** can provide unauthorized access, potentially exposing or altering data.
- **Ransomware:** encrypts files and demands payment for a claimed means of restoring access, primarily threatening availability in the scenario discussed.

## Linux access and command-line fundamentals
The guided training scenario demonstrated remote access using SSH with supplied exercise credentials and introduced basic Linux account and file inspection.

| Command | Purpose |
| --- | --- |
| `ssh USERNAME@TARGET_IP` | Connect to a remote host over SSH |
| `whoami` | Identify the current account |
| `ls` | List non-hidden entries in the current directory |
| `cat FILENAME` | Display a text file's contents |
| `history` | Display available shell command history |
| `ls /home` | Inspect home directories on the training system |
| `su - USERNAME` | Switch to another local user, subject to authentication |

The exercise also introduced **initial access** versus **privilege escalation**. A normal user session does not imply administrative or root privileges. SSH host-key prompts should be verified before trusting a new server; password entry in a terminal normally shows no characters.

## Security lessons
1. Exposed or reused credentials can enable unauthorized access.
2. Authentication and file permissions serve different security purposes.
3. Excessive permissions can undermine confidentiality and integrity.
4. Malware can threaten one or more CIA objectives.
5. Record what access was actually obtained rather than assuming administrator-level control.

## Scope and evidence
This write-up documents the concepts and guided commands covered in the completed TryHackMe room. It does **not** claim independently verified root access, compromise of additional accounts, or completed privilege escalation. All example access belongs to the authorized training environment.
