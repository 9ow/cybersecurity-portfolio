# Virtualization Fundamentals — TryHackMe

**Platform:** TryHackMe  
**Topic:** Virtualization, hypervisors, virtual machines, and containers  
**Status:** Completed — 8 November 2026

## Why virtualization?

Traditionally, organizations often dedicated one physical server to one application. As services multiplied, this increased hardware, electricity, cooling, maintenance, and space costs. Servers could remain at only **5–20% utilization**, while deploying or scaling a new service required more physical equipment.

**Virtualization** improves hardware utilization by allowing multiple independent virtual computers to share one physical host.

## Hypervisors

A **hypervisor** creates and manages virtual machines (VMs), allocates physical CPU, memory, and storage resources, provides isolation, and controls VM lifecycle operations such as **start, stop, pause, clone, and delete**.

| Hypervisor | Architecture | Common scenarios |
| --- | --- | --- |
| **Type 1** | Runs directly on physical hardware | Production servers, database servers, data centers |
| **Type 2** | Runs on top of an existing host operating system | Learning, software testing, Kali Linux, malware analysis environments |

The room presents these as typical choices rather than strict technical restrictions.

## Virtual machines (VMs)

Each VM acts as an independent computer with its own virtual CPU, RAM, storage, networking, operating system, applications, and settings, while sharing the underlying host hardware.

The room discusses **Oracle VirtualBox** and **VMware Workstation** as tools for running guest operating systems on a desktop computer. It also introduces isolating guest environments when testing suspicious files to reduce risk to the host system.

## Containers and Docker

A **container** packages an application together with its dependencies in a lightweight, isolated environment. Unlike a full VM, it shares an operating-system kernel instead of booting a separate guest kernel.

This allows containers to start quickly and generally use fewer resources. Because containers depend on the kernel they run on, operating-system compatibility matters.

**Docker** is a platform for building, deploying, and running containerized applications.

| Characteristic | VM | Container |
| --- | --- | --- |
| Main unit | Virtual computer | Application environment |
| Operating system | Separate guest OS/kernel | Shares underlying kernel |
| Resource overhead | Generally higher | Generally lower |
| Startup | Usually slower | Usually faster |
| Typical use | Different operating systems or full-machine environments | Lightweight application deployment |

## Interactive management scenario

The room introduces an **AutoGalo** company scenario in **Virtualization Manager**, a tool for viewing and managing a virtual environment.

| Section | Function |
| --- | --- |
| **Summary** | Overall status of the virtual environment |
| **Lab Machines** | VM details and available management actions |
| **Hosts** | Physical-host utilization and performance |

The troubleshooting scenario concerns employees not receiving email and directs the learner to inspect the VM named `Mail-SERVER` under **Lab Machines**.

## Key takeaways

- Sharing physical hardware can reduce underutilization and infrastructure costs.
- Hypervisors allocate resources and manage independent virtual machines.
- VMs provide full guest operating-system environments.
- Containers package applications and dependencies while sharing a kernel.
- Virtualization management interfaces provide visibility into VMs and their physical hosts.
