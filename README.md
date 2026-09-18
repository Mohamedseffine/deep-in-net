# Cisco Packet Tracer — Networking Fundamentals Project

## Overview

This repository documents a progressive series of eight Cisco Packet Tracer exercises (`ex01.pkt` through `ex08.pkt`) built to practice core computer networking concepts, from basic peer-to-peer links to a multi-router WAN with VLSM addressing. Each exercise builds on the skills of the previous one, moving from simple host-to-host cabling to a full three-router internetwork carrying traffic across nine LANs.

## Knowledge and Skills Learned

- **IP Addressing & Subnetting** — assigning IPv4 addresses and subnet masks (`/24`, `/27`, `/29`, `/30`, `/26`, `/28`), and using Variable Length Subnet Masking (VLSM) to size subnets to the number of hosts they need.
- **Network Topologies** — building and telling apart point-to-point links, star (switched) topologies, and multi-router mesh/WAN topologies.
- **Network Devices** — configuring end devices (PCs, laptops, servers), Layer 2 switches, and Layer 3 routers (models 1841, 2911, 2901).
- **LAN Configuration** — setting default gateways, connecting hosts to switches, and verifying connectivity within a subnet using ICMP (`ping`).
- **Routing & WAN Links** — configuring router Ethernet and Serial interfaces, setting up WAN links (including DCE clock rate on serial connections), and routing traffic (static and/or dynamic) between separate networks.
- **Network Services** — deploying and using DHCP, DNS, HTTP/HTTPS, and FTP servers in a client-server model.
- **Simulation & Troubleshooting** — using Packet Tracer's Realtime and Simulation modes and the PDU list to send ICMP test traffic and verify end-to-end delivery.

## General Approach (Steps Followed in Every Exercise)

1. Place the required end devices, switches, and/or routers on the canvas.
2. Cable devices together (copper straight-through for host↔switch/router, serial for router↔router WAN links).
3. Assign IP addresses and subnet masks to every host and router interface, matching the subnet plan.
4. Set each host's default gateway where a router is present.
5. On routers, configure interface addressing and (from Exercise 4 onward) enable routing between attached/remote subnets.
6. On serial WAN links (Exercises 6–8), set the clock rate on the DCE side.
7. Deploy application services (DHCP/DNS/HTTP/FTP) where required (Exercise 3) and point clients at them.
8. Use Realtime mode with simple PDUs (ICMP ping) between hosts to verify connectivity, and use Simulation mode to inspect packet flow when troubleshooting.

---

## Exercise Breakdown

### Exercise 01 — Basic Peer-to-Peer Connectivity
**Topology:** Three isolated point-to-point links (no switches, no routers).
**Devices:** 6 PCs (PC0–PC5).

| Link | Device | IP Address | Subnet |
|---|---|---|---|
| 1 | PC0 | 192.168.1.4 | /24 |
| 1 | PC1 | 192.168.1.3 | /24 |
| 2 | PC2 | 192.168.13.82 | /29 |
| 2 | PC3 | 192.168.13.83 | /29 |
| 3 | PC5 | 192.168.13.253 | /29 |
| 3 | PC4 | 192.168.13.254 | /29 |

**Concept:** Direct host-to-host communication. Demonstrates assigning IPs/masks and verifying connectivity with `ping`. The `/29` links show how a smaller subnet (8 addresses, 6 usable) is used when only two hosts need to communicate.

---

### Exercise 02 — Basic LAN Switching (Star Topology)
**Topology:** Two independent star topologies, each centered on a switch.
**Devices:** 2 switches (Switch0, Switch1), 10 PCs (PC0–PC9).

| LAN | Switch | Hosts | Example IP | Subnet |
|---|---|---|---|---|
| 1 | Switch0 | PC0–PC4 | PC0: 192.168.1.5 | /29 |
| 2 | Switch1 | PC5–PC9 | PC5: 192.168.1.193 | /27 |

**Concept:** Introduces the Layer 2 switch as the central connecting device for a broadcast domain. The two LANs use different mask sizes (`/29` for 5 hosts vs. `/27` for a larger group) to show subnet sizing based on host count, while keeping the two LANs logically separate.

---

### Exercise 03 — Client-Server Model & Network Services
**Topology:** Single LAN, star topology, centered on one switch.
**Devices:** 1 switch, 4 servers (HTTPS, FTP, DNS, DHCP), 6 PCs (PC0–PC5).
**Network:** 192.168.1.0/24

| Device | IP Address |
|---|---|
| HTTPS Server | 192.168.1.99 |
| FTP Server | 192.168.1.100 |
| DNS Server | 192.168.1.101 |
| DHCP Server | 192.168.1.102 |
| PC5 (example) | 192.168.1.7/24 |
| PC0–PC4 | assigned via DHCP |

**Concept:** Focuses on application-layer services. The DHCP server automatically leases IP addresses to client PCs; the DNS server resolves domain names to IPs; the HTTP/HTTPS and FTP servers provide web and file access. This simulates a small business/school network.

---

### Exercise 04 — Basic Inter-Network Routing
**Topology:** Two PCs connected through a single router (routed point-to-point).
**Devices:** 1 router (Cisco 1841), 2 PCs (PC0, PC1).

| Device | IP Address | Subnet |
|---|---|---|
| PC0 | 192.168.1.2 | /30 |
| PC1 | 192.168.2.2 | /30 |

**Concept:** First introduction of Layer 3 routing. The router is the default gateway for both PCs, each on its own subnet. The `/30` mask is the standard choice for point-to-point WAN-style links since it yields exactly two usable addresses, minimizing wasted address space. Demonstrates that hosts on different subnets need a router between them to communicate.

---

### Exercise 05 — Connecting Multiple LANs
**Topology:** Two star LANs joined through a central router.
**Devices:** 1 router (Cisco 2911), 2 switches, 11 PCs.

| LAN | Switch | Router Interface Subnet | Example Host |
|---|---|---|---|
| Left | Switch0 | 192.168.1.6/29 | PC5 |
| Right | Switch1 | 192.168.1.194/27 | PC6 |

**Concept:** Scales up Exercise 04 by connecting two full LANs instead of two single hosts. The router needs one interface per LAN, each addressed within that LAN's own subnet. Every PC's default gateway points to its local router interface, and the router forwards traffic between the two subnets.

---

### Exercise 06 — Router-to-Router WAN Connection
**Topology:** Linear WAN chain — two routers joined by a serial link, one PC behind each.
**Devices:** 2 routers (Router0, Router1), 2 PCs (PC0, PC1).

**Concept:** Introduces the Serial interface (the red zig-zag WAN cable) for router-to-router links. Unlike Ethernet, a serial link requires a clock rate configured on the DCE (Data Communications Equipment) side. For PC0 and PC1 to reach each other, both routers need routing information (static routes or a dynamic protocol such as RIP/OSPF) describing how to reach the network attached to the other router.

---

### Exercise 07 — Multi-LAN WAN Integration
**Topology:** Two LANs connected over a serial WAN link between two routers.
**Devices:** 2 routers, 2 switches, 5 PCs, 1 laptop.

| Side | Devices | Example Subnet |
|---|---|---|
| Left LAN | Switch0 — PC0–PC4 | 192.168.1.6/24 |
| Right LAN | Switch1 — PC6–PC8, Laptop0 | separate subnet (implied) |

**Concept:** Combines Exercises 05 and 06 into a realistic branch-office scenario: two local networks, each behind its own router, connected over a WAN serial link. Requires full routing table configuration on both routers so traffic from either LAN can reach hosts on the other.

---

### Exercise 08 — Complex Multi-Router WAN Topology
**Topology:** Three-router mesh/partial-mesh WAN backbone with three attached LANs.
**Devices:** 3 routers (Router0, Router1, Router2), 3 switches, 1 laptop, 9 PCs.

**WAN backbone (point-to-point /30 links):**

| Link | Router A | Router B |
|---|---|---|
| Router0 ↔ Router1 | 10.10.0.1/30 | 10.10.0.2/30 |
| Router1 ↔ Router2 | 10.10.1.1/30 | 10.10.1.2/30 |

**LANs (VLSM-sized):**

| LAN | Location | Subnet |
|---|---|---|
| LAN A | Left (behind Router0) | 192.168.1.198/26 |
| LAN B | Middle (behind Router1) | 192.168.2.1/24 |
| LAN C | Right (behind Router2) | 192.168.3.164/28 |

**Concept:** The capstone exercise, combining every earlier concept into an enterprise-style topology. Three LANs of different sizes use VLSM (`/26`, `/24`, `/28`) to right-size each subnet, while the three routers form a WAN backbone linked by `/30` point-to-point serial connections. Full connectivity across all nine PCs and the laptop requires either a complete static routing configuration on all three routers or a dynamic routing protocol (e.g., OSPF) so every router learns about every remote LAN.

---

## Summary Table — Progression of Complexity

| Exercise | Routers | Switches | Hosts | New Concept Introduced |
|---|---|---|---|---|
| 01 | 0 | 0 | 6 | Direct P2P addressing |
| 02 | 0 | 2 | 10 | LAN switching |
| 03 | 0 | 1 | 6 + 4 servers | Client-server services (DHCP/DNS/HTTP/FTP) |
| 04 | 1 | 0 | 2 | Basic routing, /30 links |
| 05 | 1 | 2 | 11 | Router connecting multiple LANs |
| 06 | 2 | 0 | 2 | Serial WAN link, DCE clocking |
| 07 | 2 | 2 | 5 + 1 laptop | LAN + WAN combined |
| 08 | 3 | 3 | 9 + 1 laptop | VLSM + multi-router WAN backbone |

## Verification Method

Connectivity in every exercise was verified using ICMP `ping` PDUs sent between hosts (visible in the Packet Tracer PDU list at the bottom of each project), confirmed in Realtime mode, with Simulation mode available for step-by-step packet inspection when troubleshooting routing or addressing issues.
