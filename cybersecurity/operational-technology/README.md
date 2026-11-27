# Operational Technology & Industrial Control Systems — Fundamentals

**Learning source:** TryHackMe — introductory OT/ICS training room  
**Status:** Completed 27 November 2026  
**Environment:** Authorized, simulated water-tank HMI

## Overview

This write-up records foundational understanding of Operational Technology (OT), Industrial Control Systems (ICS), supervisory control, and cybersecurity decisions where computer-based commands can affect physical processes.

The exercises used a simulated water distribution interface. No real industrial equipment or production networks were accessed.

## 1. OT, ICS and SCADA

- **Operational Technology (OT):** Technology that monitors or controls physical equipment and processes; examples extend beyond factories to building systems, transportation and medical equipment.
- **Industrial Control Systems (ICS):** A subset of OT used in industrial environments including power generation, manufacturing, oil refining and water treatment.
- **Supervisory Control and Data Acquisition (SCADA):** A class of ICS used for supervisory monitoring, data collection and remote control across distributed sites. Remote connectivity can involve cellular, microwave or satellite links.

The fundamental relationship is **SCADA ⊂ ICS ⊂ OT** in the training's simplified classification. SCADA is not necessarily restricted to wide-area connections in every real-world deployment.

## 2. PLC control fundamentals

A **Programmable Logic Controller (PLC)** reads inputs, executes programmed logic and updates outputs, repeatedly.

| Element | Function | Example |
| --- | --- | --- |
| Input | Receives a measured condition | Tank-level sensor, temperature sensor, pressure transmitter |
| Setpoint | Desired target or threshold | Target temperature |
| Logic | Evaluates input conditions and control rules | Compare measured level with a threshold |
| Output | Commands physical equipment | Start or stop a pump; open or close a valve |

**Control path:** Sensor → PLC input → PLC logic → PLC output → actuator. An HMI provides the operator with a supervisory display and permitted control commands.

## 3. Simulated HMI: water tank operations

The training interface represented **Telamon Water District — Tank 01** with a displayed tank level, inlet pump **P-101**, outlet valve **V-202**, an emergency-stop control, a reset control and a recent water-level trend.

The practical control concept explored was:

1. Observe the tank's level and available controls.
2. Identify the pump as an **inlet** that introduces water into the tank.
3. Identify the valve as an **outlet** that allows water to leave.
4. With the inlet pump stopped, opening the outlet valve causes the tank level to **lower**.
5. Recognize that HMI actions may affect physical equipment through the PLC rather than merely changing an on-screen value.

This was an educational simulator, not validation of a field PLC configuration. No specific emergency-stop safety behavior or actual plant interlocks were verified.

## 4. IT versus OT security

IT and OT share essential security concepts including network segmentation, access control, monitoring, vulnerability management and incident response. OT implementation must additionally account for **human and environmental safety** and continuity of physical processes.

| Consideration | Typical IT emphasis | OT-specific consideration |
| --- | --- | --- |
| Primary mission | Information and business systems | Physical process monitoring and control |
| Security priorities | Confidentiality, integrity, availability | Safety first; then operational availability, integrity and confidentiality as context requires |
| Asset lifecycle | Regular replacement | Long-lived and legacy equipment |
| Patching | More frequent and routine | Testing, vendor coordination and maintenance windows |
| Vulnerability assessment | Active scanning often feasible | Passive monitoring often preferred; intrusive probing needs validation |
| Incident response | Isolation and restoration may be straightforward | Confirm process safety and operator coordination before containment |
| Encryption | Common in modern enterprise services | Some legacy industrial protocols lack native encryption |

These are **general tendencies, not universal rules**. Safe shutdown can take priority over keeping operations running when continued operation is dangerous.

## 5. Threat scenarios and defensive considerations

IP networking, Ethernet, cloud integration and IT/OT connectivity can expand the attack surface. Unauthorized HMI or PLC access might cause process disruption, misleading displays, unsafe control changes or equipment damage if other controls fail.

Defensive priorities explored conceptually:

- Inventory industrial assets and understand their process roles.
- Segment enterprise and OT networks and strictly control access paths.
- Apply least privilege to supervisory interfaces and engineering access.
- Use appropriate passive network monitoring for sensitive assets.
- Coordinate patching and incident response with operations and safety personnel.
- Preserve independent safety mechanisms and validated recovery procedures.

## Key takeaways

- **An input reads the process; an output commands equipment.**
- A **PLC** implements control logic while an **HMI** enables human supervision.
- **Physical safety** changes how cybersecurity controls are deployed in OT.
- Industrial security builds on IT networking fundamentals but requires process awareness, restraint and collaboration with engineers/operators.

## Scope and attribution

Training source: [TryHackMe](https://tryhackme.com/) introductory OT/ICS content. This documentation summarizes concepts and a simulated HMI interaction in original words; it does not claim production-system penetration testing, a deployed OT design, or an external certification.

