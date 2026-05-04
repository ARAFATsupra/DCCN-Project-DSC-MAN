# Daffodil Smart City MAN (DSCM)

> A Metropolitan Area Network (MAN) simulation connecting three branches of Daffodil Smart City using Cisco Packet Tracer.

---

## Table of Contents

- [About the Project](#about-the-project)
- [Network Architecture](#network-architecture)
- [IP Addressing Scheme](#ip-addressing-scheme)
- [Tools and Technologies](#tools-and-technologies)
- [How to Open the Simulation](#how-to-open-the-simulation)
- [Configuration Summary](#configuration-summary)
- [Testing and Results](#testing-and-results)
- [Limitations](#limitations)
- [Future Work](#future-work)
- [Team](#team)
- [Course Information](#course-information)
- [References](#references)

---

## About the Project

Daffodil Smart City (DSC) has three major branches spread across the city that previously had no direct network connection. This lack of connectivity led to slow file sharing, poor communication, high individual internet costs, and outdated data at each location.

This project designs and simulates the **Daffodil Smart City Metropolitan Area Network (DSC-MAN)** — a star-topology MAN that connects all three branches through high-speed fiber optic and serial links, with DIU acting as the central hub.

**Branches connected:**

| Branch | Role |
|--------|------|
| Daffodil International University (DIU) | Main hub — hosts the central Database Server and internet access |
| Daffodil Medical Center | Runs the Email Server for official institutional communication |
| Daffodil School | Runs the Web Server for the DSC student portal and website |

---

## Network Architecture

The network follows a **Star Topology** where the DIU Main Branch sits at the center, directly connected to the other two branches via serial WAN links.

```
        [DIU Main Branch]
         (Router0 - Hub)
        /               \
 Serial Link         Serial Link
      /                   \
[Medical Center]      [Daffodil School]
  (Router1)              (Router2)
```

**Devices used per branch:**

- 1 Router (PT-Router) — for inter-branch WAN connectivity
- 1 Switch (2950-24) — for local LAN connectivity
- 1 Server-PT — for centralized services (DHCP, DNS, Web, Email, Database)
- 3 PCs — representing end users in each branch

**Total devices: 3 Routers, 3 Switches, 3 Servers, 9 PCs**

**Connection types:**
- Copper straight-through cables — PCs and Servers to Switches
- Serial DTE cables — Router-to-Router inter-branch links (clock rate: 2,000,000 bps)

---

## IP Addressing Scheme

| Branch | Router IP (FastEthernet) | Server IP | DHCP Start IP | Subnet Mask |
|--------|--------------------------|-----------|---------------|-------------|
| DIU (Main Hub) | 10.168.10.100 | 10.168.10.1 | 10.168.10.2 | 255.255.255.0 |
| Daffodil Medical Center | 192.168.10.100 | 192.168.10.1 | 192.168.10.2 | 255.255.255.0 |
| Daffodil School | 172.168.10.100 | 172.168.10.1 | 172.168.10.2 | 255.255.255.0 |

All PCs in each branch receive their IP addresses automatically via **DHCP**, configured on the branch server.

**Routing Protocol:** RIP Version 2 (RIPv2) — enables all routers to learn about remote networks automatically.

---

## Tools and Technologies

| Tool | Purpose |
|------|---------|
| Cisco Packet Tracer 8.2 | Network simulation and testing |
| Router IOS CLI | Router and switch configuration |
| Server-PT Services | DHCP, DNS, Web (HTTP), Email (SMTP) simulation |
| MS Word | Report documentation |
| Cisco RIPv2 | Dynamic inter-branch routing protocol |

---

## How to Open the Simulation

You need **Cisco Packet Tracer** installed on your computer. It is free for students via the Cisco Networking Academy.

1. Download and install Cisco Packet Tracer from [https://www.netacad.com](https://www.netacad.com).
2. Clone or download this repository.
3. Open Cisco Packet Tracer.
4. Go to **File > Open**.
5. Open the file:
   - `DCCN_Project_DSC_MAN_Team_Insight.pkt` — Full DSC MAN simulation
   - `DCCN_Project_MCBN_Team_Insight.pkt` — Medical Center Branch Network simulation
6. The network topology will load automatically. You can click any device to inspect its configuration.

---

## Configuration Summary

### Step 1 — Place and Connect Devices
- Add 3 PT-Routers, 3 Cisco 2950-24 Switches, 3 Server-PTs, and 9 PCs.
- Connect each Router to its local Switch using a copper straight-through cable.
- Connect each Switch to its local Server and 3 PCs using copper straight-through cables.
- Connect the 3 Routers to each other using Serial DTE cables on the Serial 2/0 and Serial 3/0 ports.

### Step 2 — Configure Each Router's LAN Interface (FastEthernet0/0)
- Turn on the port and assign the correct IP address and subnet mask for that branch.

### Step 3 — Configure Each Server
- Assign a static IP address and default gateway.
- Enable DHCP service and set the default gateway and start IP for automatic PC addressing.

### Step 4 — Configure PCs
- Set each PC to DHCP mode so it receives an IP address automatically from the server.

### Step 5 — Configure Router Serial Links (WAN)
- On Router0 (DIU): configure Serial 2/0 toward School and Serial 3/0 toward Medical Center. Set clock rate 2000000 on the DCE side.
- Repeat on Router1 and Router2 with their respective serial interfaces.

### Step 6 — Enable RIPv2 Routing
- On each router, enter CLI and configure RIP version 2 with all directly connected network addresses.

---

## Testing and Results

The following tests were performed to verify that the MAN simulation works correctly:

| Test | Command | Expected Result |
|------|---------|-----------------|
| Intra-branch ping | `ping [server IP]` from any branch PC | Successful reply |
| Inter-branch ping | `ping [remote branch PC IP]` | Successful reply |
| Routing table check | `show ip route` on any router | Remote networks shown via RIP |
| DHCP verification | Check IP config on any PC | Valid IP automatically assigned |
| Traceroute | `tracert [remote IP]` from PC | Traffic passing through DIU router |

All tests passed successfully. Every PC in every branch can communicate with every other PC across the city through the simulated MAN.

---

## Limitations

- The network exists only as a simulation in Cisco Packet Tracer — no physical hardware was used.
- Internet access is simulated, not a real ISP connection.
- Only a small number of end devices (9 PCs) were used for demonstration purposes.
- No advanced security features such as firewalls, VPNs, or intrusion detection systems were implemented in this version.

---

## Future Work

- Build the same network physically using real routers, switches, and fiber optic cables.
- Extend the MAN to connect more city branches without redesigning the core architecture.
- Add firewalls, VPNs, and network monitoring tools to improve security.
- Implement backup links and redundant servers for high availability.
- Integrate cloud storage for remote access, data backup, and disaster recovery.

---

## Team

**Team Insight** — Group 2, 8th Batch, Section A, Summer 2025

---

## Course Information

| Field | Details |
|-------|---------|
| Course Title | Data Communication and Computer Network |
| Course Code | ITM 315 |
| Department | Information Technology and Management (ITM) |
| Faculty | Faculty of Science and Information Technology |
| University | Daffodil International University (DIU) |
| Supervisor | Ms. Nishat Tasnim Shishir, Lecturer, Dept. of ITM |
| Submission Date | 13th August 2025 |

---

## References

- Cisco Networking Academy. (2023). *Cisco Packet Tracer 8.2 – Networking simulation tool.* Cisco Systems, Inc. https://www.netacad.com/courses/packet-tracer
- Olivier Bonaventure. (2022). *Computer Networking: Principles, Protocols and Practice* (3rd ed.). https://inl.info.ucl.ac.be/CNP3
- Cisco Systems. (2022). *Packet Tracer Tutorial – Connecting Routers and Switches.* Cisco Support. https://www.cisco.com
- Subnetting Practice. (2023). *Subnet mask and IP addressing basics.* https://www.subnettingpractice.com
- GeeksforGeeks. (2023). *Types of Network Topologies.* https://www.geeksforgeeks.org/types-of-network-topologies

---

*This project was submitted as part of the academic requirement for ITM 315 at Daffodil International University.*
