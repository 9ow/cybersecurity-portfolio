# Windows Basics — TryHackMe

**Status:** Completed  
**Platform:** TryHackMe  
**Completed:** 8 November 2026  
**Focus:** Windows administration fundamentals, desktop navigation, file and application management, system monitoring, and security controls

## Windows interface and account access

Early Microsoft systems such as MS-DOS used text-based commands. Windows 1.0 introduced graphical windows, menus, and mouse interaction in 1985; the platform later evolved into a full operating system.

Windows verifies a user's identity during sign-in, and the account's privileges determine what operations are permitted.

| Account | Access |
| --- | --- |
| Guest | Restricted temporary access |
| Standard | Everyday application use and personal settings |
| Administrator | Privileged system configuration, installation, and user management |

The exercise environment used an **Administrator** session on **Windows Server 2019 Datacenter**.

### Desktop components

- **Desktop:** Workspace for icons, files, folders, and shortcuts.
- **Taskbar:** Access to open and pinned applications and system controls.
- **Start menu:** Applications, settings, user options, and power controls.
- **Search:** Locate files, applications, folders, and settings.
- **Task View:** View and switch between open windows.
- **Notification area:** Network, audio, date and time, and notifications.

## System information

The **About your PC** interface showed the following properties of the training workstation:

| Property | Observed value |
| --- | --- |
| Device name | `TryHatMe` |
| Processor | AMD EPYC 7571, 2.20 GHz |
| Installed RAM | 4.00 GB |
| Architecture | 64-bit operating system, x64-based processor |
| Windows edition | Windows Server 2019 Datacenter |
| Version | `1809` |
| OS build | `17763.8146` |

In **Settings → Time & Language**, the configured **Country or region** was **United States**. The **Users** tab in Task Manager showed **Administrator** as the signed-in account.

## File navigation and management

Windows File Explorer provides a graphical interface for working with hierarchical folder structures, files, and directories.

The onboarding exercise introduced the path:

```text
C:\Users\Administrator\Desktop\TryHatMe Onboarding
```

The path identifies the system drive, user profile, Desktop directory, and onboarding folder. File Explorer also supports folder navigation, viewing, sharing, editing, and searching.

## Application lifecycle management

Windows applications can be installed, updated, and removed through several mechanisms.

### Updates

- **Windows Update** delivers operating-system updates and updates to some built-in applications and security functionality.
- Some applications update automatically.
- Third-party applications may provide their own update tools or require manual installer downloads.
- Updates can include security patches, performance improvements, and bug fixes.

### Installation and removal

Common sources include the **Microsoft Store** and trusted software-vendor installers, often packaged as `.exe` or `.msi` files.

The exercise used the **`TryHatMeWelcome`** installer from the onboarding folder.

Uninstallation options introduced included **Add or remove programs**, **Control Panel → Uninstall a program**, an application's own uninstaller, and supported store-based removal.

## Windows Settings and Control Panel

| Interface | Purpose |
| --- | --- |
| **Windows Settings** | Modern interface for system, display, audio, accounts, applications, networking, accessibility, and security preferences |
| **Control Panel** | Legacy interface containing configuration and administration tools |

Both allow inspection or modification of Windows settings.

## Task Manager and process visibility

Windows Task Manager provides live visibility into applications, background processes, users, services, and resource utilization.

| Tab | Information |
| --- | --- |
| Processes | Active applications, background processes, and resource use |
| Performance | CPU, memory, network, and other resource statistics |
| Users | Signed-in sessions and resource use |
| Details | Detailed process information, including process IDs (PIDs) |
| Services | Service names and running/stopped states |

## Built-in Windows security

### Windows Security

Windows includes a central security interface with four areas:

1. **Virus & threat protection:** Malware detection, real-time protection, and scanning options.
2. **Firewall & network protection:** Controls for network access.
3. **App & browser control:** Protection against potentially unsafe applications, files, and websites.
4. **Device security:** Hardware-backed security features.

### Custom antivirus scanning

The room demonstrated the workflow:

`Windows Security → Virus & threat protection → Scan options → Custom scan → Scan now`

The target was the **`TryHatMe Onboarding`** directory. The exercise described a harmless **EICAR antivirus test file** and how to inspect detection details, including affected items.

### Windows Defender Firewall

Windows Defender Firewall applies network-access rules to permitted and blocked connections. Rules can be inspected in advanced settings and can be scoped to network profiles:

| Profile | Intended network |
| --- | --- |
| Domain | Organization domain network |
| Private | Trusted home or training network |
| Public | Untrusted network such as public Wi-Fi |

Advanced firewall settings expose inbound, outbound, and connection rules, including names, groups, applicable profiles, status, and actions.

## Skills covered

- Navigate Windows desktop and Start menu tools.
- Inspect workstation operating-system and hardware properties.
- Identify user-account privileges and the signed-in session.
- Navigate file paths and manage applications.
- Review Windows Update and software installation methods.
- Use Task Manager to observe processes, resource usage, and services.
- Locate native antivirus and firewall controls and understand network profiles.
