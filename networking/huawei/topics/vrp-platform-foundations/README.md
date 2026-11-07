# VRP Platform Foundations

**Source: `VRP-Foundation.pptx`, 58 slides.** Studied and quizzed, *not lab verified*.

## Slides 1–5: foundations
- **VRP** = Versatile Routing Platform, IP-based component OS for Huawei datacom; software core for low-end to core routers, Ethernet switches and service gateways. Unifies user and management interfaces, implements control plane, specifies interfaces to forwarding plane and communication between both planes.
- VRP timeline from slide 3: **VRP1** centralized, 1998–2001; **VRP2** distributed, 1999–2000; **VRP3** distributed platform/core support, 2000–2004; **VRP5** component-based/high performance, 2004–Now; **VRP8** multi-process, multi-CPU and multi-chassis, 2009–Now. These are the slide's historical labels, not updated release status.
- File system creates/views/renames/deletes files/directories. **`.cc` system software**, **`.cfg/.zip/.dat` configuration**, **`.pat` patch**, **`.bin` PAF** (features/resources).
- **SDRAM** running data; **flash** nonvolatile system/config; **SD card** nonvolatile storage; **NVRAM** logs buffered before flash; **USB** storage interface for upgrades/transfers.

## Slides 6–17: access and device startup
- Console cable host COM/serial → console; AR2200 supports Mini USB alternative and may require drivers. Source describes terminal emulator setup; slide's driver verification is `TUSB3410`. These steps are **not recorded as performed**.
- Default simultaneous console users **1**. Startup: **BootROM → system software → stored configuration**. The slide's Auto-Config warning mentions DHCP, routing, DNS, VTY settings.
- **CLI** access: console, Telnet, SSH. **Web system**: HTTP/HTTPS; GUI supports only some functions.

## Slides 18–29: CLI and interfaces
- User view `<Huawei>`; system view `[Huawei]` via `system-view`; interface and protocol views for corresponding configuration. `Ctrl+Z` returns to user view.
- Keyboard: `Ctrl+A` beginning; `Ctrl+C` interrupt; `Ctrl+B/F` left/right; `Ctrl+E` end; `Ctrl+H/D` delete; `Ctrl+N/P` next/previous history; `Ctrl+W/X/Y` delete word/left/right; `Esc+B/F/D` word navigation/deletion; `Tab` completion; partial help `d?`, full help `?`, contextual `display ?`.
- `sysname RTA`; `clock timezone`, `clock datetime`, `clock daylight-saving-time`, `display clock`. `header login` before authentication vs `header shell` after sign-in.
- **User levels** 0 visit, 1 monitoring, 2 configuration, 3–15 management; **command levels** 0–3.
- VTY initial range **0–4**, extend **0–14** with `user-interface maximum-vty 15`. Console relative number 0.
- Defaults: `idle-timeout` **10 min**, `screen-length` **24 lines** (maximum 512), `history-command max-size` **10** (maximum 256); `idle-timeout 1 30` = 1m30s. Commands `user privilege level 2`, `set authentication password cipher`.
- Interfaces: `interface GigabitEthernet 0/0/0`, `ip address 10.0.12.1 255.255.255.0`; `interface loopback 0`, `ip address 1.1.1.1 32`. A loopback is logical; slide example /32 isn't a universal default.

## Slides 30–45: VRP file-system/config management
- `cd` change folder, `pwd` current path, `dir` directory, `more` file contents; `mkdir`, `rmdir` (empty directories), `copy`, `move`, `rename`.
- `delete` recoverable, `undelete` recover; `delete /unreserved` permanently deletes; `reset recycle-bin` clears recycle bin. In `dir`, attribute leading `d` means directory.
- `display current-configuration` vs `display saved-configuration`; `save` persists; `display startup` views startup files; `startup saved-configuration flash:/huawei.zip` selects next configuration; `compare configuration` compares current and saved; `reset saved-configuration` clears startup saved config.
- `display version` media information; `format` wipes storage; `fixdisk flash:` repair.

## Slides 46–58: image management
- FTP/TFTP file transfers for software/config/logs. FTP client `ftp 10.1.1.2`; `get` downloads and `put` uploads. TFTP command syntax appears in slide 55.
- Set next image using `startup system-software vrp.cc`; `reboot` required to activate.

## Assessment
Prior full mock **13/15**; later direct **15/15** with uncertainty for LoopBack (50%), startup config (75%), image extension (75%). Restarted Slide 1 direct exam **10/10 at 100%**. Restarted Slide 2 result not reported. No lab execution evidence.
