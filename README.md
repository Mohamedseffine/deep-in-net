# Deep in Net – Networking Fundamentals Project

## Overview

This project introduces fundamental networking concepts through hands-on practice using Cisco Packet Tracer. The goal is to understand how different network devices, protocols, and configurations interact to enable communication between systems across multiple networks.

The project is divided into several exercises, each building on the previous one, gradually increasing in complexity. By the end, a complete multi-router network with proper routing between subnets is implemented.

---

## Objectives

- Understand the role of networking devices (PCs, switches, routers, servers)
- Learn how to assign and manage IP addressing and subnetting
- Apply the OSI model in practical scenarios
- Configure and troubleshoot networks using CLI
- Implement routing between multiple networks
- Understand key protocols such as DHCP, DNS, HTTP/HTTPS, and FTP

---

## Tools Used

- Cisco Packet Tracer
- Linux CLI (for conceptual understanding)
- Basic networking commands (`ping`, `show ip route`, `show ip interface brief`)

---

## Key Concepts Learned

### 1. Networking Devices

- **Switch**: Operates at Layer 2 (Data Link), connects devices within the same network using MAC addresses.
- **Hub**: Operates at Layer 1 (Physical), broadcasts data to all connected devices.
- **Router**: Operates at Layer 3 (Network), routes traffic between different networks.

---

### 2. Cables and Connections

- **RJ-45**: Standard connector used for Ethernet networking.
- **Straight-through cable**: Used between different device types (PC ↔ Switch).
- **Crossover cable**: Used between similar devices (Router ↔ Router).
- **Serial cable**: Used for router-to-router connections, requires clock rate on DCE side.

---

### 3. IP Addressing and Subnetting

- Each device must have:
  - Unique IP address
  - Correct subnet mask
  - Proper default gateway

- Example subnet types used:
  - `/24` → 255.255.255.0 (LANs)
  - `/30` → 255.255.255.252 (point-to-point links)
  - `/26` and `/28` for subnet division

---

### 4. Routing

Routers do not automatically know all networks.

- **Directly connected networks** are known automatically
- **Remote networks** require:
  - Static routes (`ip route`)
  - Or dynamic routing (not used here)

Example:

```
ip route 192.168.2.0 255.255.255.0 10.10.0.2
```

---

### 5. OSI Model (Practical View)

- Layer 1: Cables and physical connections
- Layer 2: Switches and MAC addressing
- Layer 3: Routing and IP addressing

Most troubleshooting issues in this project occurred at:

- Layer 1 (cables, interfaces down)
- Layer 3 (missing routes)

---

## Exercises Summary

### Exercise 1

Basic connectivity between PCs using direct connections.

### Exercise 2

Introduction to switches and hubs. Devices in the same network communicate through shared infrastructure.

### Exercise 3

Server configuration:

- DHCP for automatic IP assignment
- DNS for domain resolution
- HTTPS server with HTTP disabled
- FTP server with user permissions

### Exercise 4

Introduction to routers and default gateways.

### Exercise 5

Communication between subnets using a router.

### Exercise 6

Router-to-router communication using static routing.

### Exercise 7

Expansion of routing with multiple hosts and switches.

### Exercise 8

Complex network with:

- 3 routers
- 3 subnets
- Multiple routing paths

---

## Challenges and Troubleshooting

This project required extensive troubleshooting. The main difficulties encountered were:

### 1. Interfaces Not Working

- Interfaces remained `down/down`
- Cause: wrong cable type or incorrect port usage
- Solution: verify connections and use proper interfaces

---

### 2. Cable Issues

- Ethernet connections sometimes failed unexpectedly
- Switching to serial connections resolved instability

---

### 3. Missing Routes

- Devices could not communicate across networks
- Cause: routers did not know remote networks
- Solution: manually add static routes

---

### 4. Incorrect Subnetting

- Misunderstanding network vs host addresses
- Example: confusing `192.168.1.193` as network instead of host
- Solution: calculate subnet ranges properly

---

### 5. Default Gateway Misconfiguration

- PCs unable to reach other networks
- Cause: missing or incorrect gateway
- Solution: set gateway to router’s LAN IP

---

### 6. Serial Communication Issues

- Serial interfaces remained down
- Cause: missing clock rate on DCE side
- Solution: configure:

```
clock rate 64000
```

---

## Final Network Architecture

The final exercise included:

- 3 routers connected via serial links
- 3 LANs with different subnet sizes
- Static routing between all networks
- Full connectivity between all devices

---

## Testing Strategy

Connectivity was verified using:

- `ping` for reachability
- Packet Tracer simulation (envelope tool)
- CLI commands:
  - `show ip interface brief`
  - `show ip route`

---

## Conclusion

This project provided a complete introduction to practical networking:

- Building networks from scratch
- Configuring routers and interfaces
- Understanding and applying subnetting
- Implementing routing logic
- Debugging real-world networking issues

The most important takeaway is that networking problems should be approached methodically:

1. Check physical layer (cables, interfaces)
2. Verify IP configuration
3. Confirm routing tables
4. Test connectivity step by step

---

## Repository Structure

```
deep-in-net/
├── ex01.pkt
├── ex02.pkt
├── ex03.pkt
├── ex04.pkt
├── ex05.pkt
├── ex06.pkt
├── ex07.pkt
├── ex08.pkt
└── README.md
```

---

## Final Note

The project emphasizes practice over theory. Understanding comes from repeated configuration, testing, and debugging. Mistakes are part of the process, and each failure provides insight into how networks actually behave.
