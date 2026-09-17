# Networking Fundamentals Study Guide

This document reorganizes and explains the networking material from the supplied notes into one coherent reference. It covers Ethernet cables and standards, baseband signaling, hubs and switches, servers, DHCP, DNS, HTTP/HTTPS, FTP, TCP/UDP, ports, DNS records, routers, default gateways, and routing tables.

---

## 1. RJ-45 Ethernet Cables

### What is an RJ-45 cable?

An **RJ-45 cable** is the common name for an Ethernet cable terminated with an RJ-45-style connector. In Ethernet terminology, the connector is more precisely an **8P8C connector**.

An Ethernet twisted-pair cable normally contains:

- 8 individual copper wires
- 4 twisted pairs
- A connector with 8 contact positions
- A cable category such as Cat5e, Cat6, or Cat6a

The important distinction is:

> **RJ-45 refers to the connector; Ethernet refers to the networking technology and its standards.**

Not every Ethernet cable uses an RJ-45 connector. Older Ethernet used coaxial cable, while many high-speed Ethernet connections use fiber-optic cable.

---

## 2. T568A and T568B Wiring

The wires inside twisted-pair Ethernet cables are arranged according to wiring schemes such as **T568A** and **T568B**.

### T568A

| Pin | Wire |
|---:|---|
| 1 | White/Green |
| 2 | Green |
| 3 | White/Orange |
| 4 | Blue |
| 5 | White/Blue |
| 6 | Orange |
| 7 | White/Brown |
| 8 | Brown |

### T568B

| Pin | Wire |
|---:|---|
| 1 | White/Orange |
| 2 | Orange |
| 3 | White/Green |
| 4 | Blue |
| 5 | White/Blue |
| 6 | Green |
| 7 | White/Brown |
| 8 | Brown |

The main difference is that the orange and green pairs exchange positions.

---

## 3. Straight-Through vs. Crossover Cables

### Straight-through cable

A straight-through cable uses the **same wiring standard on both ends**:

- T568A → T568A
- T568B → T568B

It is traditionally used to connect different types of devices, for example:

- PC → switch
- PC → hub
- Switch → router
- PC → wall/network outlet

The wires remain in the same pin positions from one end to the other.

### Crossover cable

A crossover cable traditionally uses a different wiring standard on each end:

- T568A → T568B

For 10/100 Ethernet, the transmit and receive pairs are crossed:

- Pin 1 ↔ Pin 3
- Pin 2 ↔ Pin 6

It was traditionally used for directly connecting similar devices:

- PC → PC
- Switch → switch
- Router → router

### Auto-MDIX

Modern Ethernet interfaces commonly support **Auto-MDIX**.

Auto-MDIX automatically detects the wiring relationship and adjusts the transmit/receive configuration. Because of this, manually choosing a crossover cable is rarely necessary with modern equipment.

### Quick comparison

| Feature | Straight-through | Crossover |
|---|---|---|
| Ends | Same standard | Different standards |
| Typical wiring | A-A or B-B | A-B |
| Traditional use | Different device types | Similar device types |
| Modern necessity | Common | Rare because of Auto-MDIX |

---

# 4. Ethernet Standards

Ethernet standards are defined primarily by the **IEEE 802.3** family of standards.

An Ethernet standard defines things such as:

- Transmission speed
- Signaling method
- Physical medium
- Maximum distance
- Encoding
- Connector or interface requirements

The name often follows a pattern such as:

```text
SPEED + BASE + MEDIUM/DISTANCE
```

For example:

```text
1000BASE-T
```

means:

- `1000` → 1000 Mbps = 1 Gbps
- `BASE` → baseband signaling
- `T` → twisted pair

---

## 5. Understanding Ethernet Names

Some common suffixes include:

| Symbol | Meaning |
|---|---|
| `T` | Twisted pair |
| `F` | Fiber |
| `2` | Approximately 200 m in the original 10BASE2 naming |
| `5` | 500 m in 10BASE5 |
| `SX` | Short-wavelength fiber |
| `LX` | Long-wavelength fiber |
| `SR` | Short-range fiber |
| `LR` | Long-range fiber |

The `2` in **10BASE2** refers approximately to 200 meters, although the actual maximum segment length is about **185 m**.

---

## 6. Classic Ethernet Standards

### 10BASE5

**10BASE5** was an early Ethernet standard.

- Speed: 10 Mbps
- Medium: Thick coaxial cable
- Maximum segment length: 500 m
- Topology: Bus
- Often called "Thicknet"
- Uses special attachment hardware rather than RJ-45
- Obsolete

### 10BASE2

**10BASE2** used thinner coaxial cable.

- Speed: 10 Mbps
- Medium: Thin coaxial cable, commonly RG-58
- Maximum segment length: 185 m
- Connector: BNC
- Topology: Bus
- Often called "Thinnet"
- Required termination
- Obsolete

### 10BASE-T

**10BASE-T** brought Ethernet to twisted-pair cabling.

- Speed: 10 Mbps
- Medium: Twisted pair
- Typical connector: RJ-45/8P8C
- Maximum cable segment: 100 m
- Originally associated with Cat3 or better
- Uses two twisted pairs
- Usually connected in a star topology through a hub or switch

This is historically important because modern Ethernet over copper evolved from this approach.

---

## 7. Fast Ethernet

### 100BASE-TX

- Speed: 100 Mbps
- Medium: Cat5 twisted pair
- Connector: RJ-45
- Maximum segment: 100 m
- Uses two pairs
- Also called Fast Ethernet

### 100BASE-FX

- Speed: 100 Mbps
- Medium: Fiber
- Typical connectors: SC/ST
- Approximately 2 km in common full-duplex multimode implementations

Other historical variants existed, such as 100BASE-T4 and 100BASE-T2, but they are obsolete.

---

## 8. Gigabit Ethernet

### 1000BASE-T

**1000BASE-T** provides 1 Gbps Ethernet over copper twisted-pair cabling.

- Speed: 1 Gbps
- Medium: Cat5e/Cat6
- Connector: RJ-45/8P8C
- Maximum segment: 100 m
- Uses all four twisted pairs

This is one of the most common wired Ethernet standards in modern LANs.

### 1000BASE-SX

- Speed: 1 Gbps
- Medium: Multimode fiber
- Short-wavelength optical transmission
- Commonly used for shorter fiber links

### 1000BASE-LX

- Speed: 1 Gbps
- Medium: Primarily single-mode fiber, with some multimode applications
- Long-wavelength optical transmission
- Can reach several kilometers depending on the fiber and implementation

---

## 9. Multigigabit and 10-Gigabit Ethernet

### 2.5GBASE-T and 5GBASE-T

These standards provide:

- 2.5 Gbps or 5 Gbps
- Twisted-pair copper
- RJ-45/8P8C
- Up to approximately 100 m under appropriate cabling conditions

They are useful when existing copper cabling needs more performance than 1 Gbps without immediately moving to 10 Gbps.

### 10GBASE-T

- Speed: 10 Gbps
- Medium: Twisted pair
- Connector: RJ-45/8P8C
- Cat6: up to about 55 m in typical deployments
- Cat6a: up to 100 m

### 10GBASE-SR

- Speed: 10 Gbps
- Medium: Multimode fiber
- Designed for relatively short fiber links
- Common distances are roughly 300–400 m depending on the fiber grade

### 10GBASE-LR

- Speed: 10 Gbps
- Medium: Single-mode fiber
- Long-range Ethernet
- Common maximum distance: approximately 10 km

### 40GBASE-T

- Speed: 40 Gbps
- Medium: Cat8 twisted pair
- Maximum channel length: approximately 30 m
- Intended for high-speed short copper links

---

## 10. Ethernet Cable Categories

Do not confuse an **Ethernet standard** with a **cable category**.

For example:

```text
1000BASE-T = Ethernet standard
Cat6       = cable category
```

The cable category describes the electrical characteristics and performance capabilities of the cable.

Common relationships include:

| Cable | Common Ethernet uses |
|---|---|
| Cat3 | 10BASE-T |
| Cat5 | 100BASE-TX |
| Cat5e | 1000BASE-T, 2.5GBASE-T and some 5GBASE-T deployments |
| Cat6 | 1000BASE-T, 2.5G/5GBASE-T, 10GBASE-T for shorter distances |
| Cat6a | 10GBASE-T up to 100 m |
| Cat8 | 40GBASE-T up to 30 m |

Today, 10BASE2 and 10BASE5 are historical technologies. Modern copper Ethernet is dominated by standards such as 1000BASE-T, 2.5GBASE-T, 5GBASE-T, and 10GBASE-T. Fiber is widely used for longer distances and high-speed backbone links.

---

# 11. Baseband Signaling

The `BASE` in Ethernet names such as `10BASE-T`, `100BASE-TX`, and `1000BASE-T` means **baseband**.

### What is baseband signaling?

Baseband signaling transmits the data signal directly over the medium rather than shifting it onto a separate high-frequency carrier.

The signal occupies frequencies starting near DC and extending upward according to the signaling system.

In simple terms:

> **Baseband = the data signal itself is transmitted over the medium.**

This does not mean Ethernet sends raw bits with no encoding. Ethernet can use line coding, scrambling, pulse shaping, and multilevel signaling. What matters is that the data is not being carried as a separate RF carrier in the way traditional broadband systems do.

### Baseband vs. broadband

| Feature | Baseband | Broadband |
|---|---|---|
| Basic idea | Data signal transmitted directly | Data modulated onto carrier frequencies |
| Channel use | Main signal occupies the available transmission band | Multiple frequency bands/channels can coexist |
| Typical examples | Ethernet LANs | Cable TV, some broadband systems, radio |
| Ethernet example | 1000BASE-T | 10BROAD36 |

A consumer saying "I have broadband internet" does not necessarily mean they are talking about the technical Ethernet meaning of broadband.

---

# 12. Hub

A **hub** is a simple multiport repeater.

Its job is to connect devices in a LAN and repeat incoming electrical signals.

### How a hub works

Suppose four computers are connected to a hub:

```text
PC1 ─┐
PC2 ─┼── HUB
PC3 ─┤
PC4 ─┘
```

If PC1 sends a signal, the hub repeats that signal to the other ports.

The hub does not understand:

- MAC addresses
- IP addresses
- TCP ports
- Applications

It simply repeats signals.

### OSI layer

A hub operates at:

**Layer 1 — Physical layer**

### Characteristics

- One shared collision domain
- Shared bandwidth
- Typically half-duplex
- No MAC address table
- No traffic filtering
- No intelligent forwarding
- Mostly obsolete today

---

# 13. Switch

A **network switch** connects devices in a LAN and intelligently forwards Ethernet frames.

Unlike a hub, a switch examines Ethernet frames and learns where devices are located based on their **MAC addresses**.

### MAC address table

A switch maintains a table similar to:

| MAC address | Port |
|---|---|
| AA:AA:AA:AA:AA:01 | Port 1 |
| BB:BB:BB:BB:BB:02 | Port 2 |
| CC:CC:CC:CC:CC:03 | Port 3 |

If a frame arrives with a known destination MAC address, the switch forwards it to the corresponding port.

### How a switch learns

When a frame enters a switch:

1. The switch reads the source MAC address.
2. It records that MAC address against the incoming port.
3. It reads the destination MAC address.
4. If the destination is known, it forwards the frame to the correct port.
5. If the destination is unknown, it floods the frame to appropriate ports.
6. Broadcast frames are normally flooded within the VLAN.

### OSI layer

A traditional Ethernet switch operates primarily at:

**Layer 2 — Data Link layer**

Some multilayer switches also perform routing at Layer 3.

---

# 14. Hub vs. Switch

| Feature | Hub | Switch |
|---|---|---|
| OSI layer | Layer 1 | Layer 2 |
| Main unit | Signals/bits | Ethernet frames |
| Uses MAC addresses | No | Yes |
| MAC table | No | Yes |
| Forwarding | Repeats to other ports | Sends to appropriate port |
| Bandwidth | Shared | Per-port bandwidth |
| Collision domains | One shared domain | Usually one per port |
| Duplex | Usually half-duplex | Full-duplex supported |
| Traffic filtering | No | Yes |
| Broadcasts | Repeated | Forwarded within VLAN |
| Modern use | Obsolete | Standard LAN technology |

A useful mental model is:

> **Hub = repeat everything.**  
> **Switch = learn where devices are and forward intelligently.**

---

# 15. Server

A **server** is a computer or software system that provides resources or services to other devices, called clients, over a network.

Examples include:

- Web server
- File server
- Database server
- DNS server
- DHCP server
- Mail server
- Authentication server

The basic model is:

```text
Client → Request → Server
Client ← Response ← Server
```

A server itself is not a specific protocol and therefore does not have one universal port. A server listens on ports belonging to the services it provides.

---

# 16. DHCP

**DHCP = Dynamic Host Configuration Protocol**

DHCP automatically provides network configuration to clients.

It can provide:

- IP address
- Subnet mask
- Default gateway
- DNS server address
- Lease duration

Without DHCP, these settings can be configured manually.

## DHCP DORA process

The classic DHCP exchange is called **DORA**:

### 1. Discover

The client broadcasts a DHCP Discover message because it may not yet have an IP address or know where the DHCP server is.

### 2. Offer

The DHCP server responds with an IP address and other configuration information it can offer.

### 3. Request

The client requests the offered configuration.

### 4. Acknowledge

The DHCP server acknowledges the lease.

```text
Client                  DHCP Server

  |--- DHCP Discover ----->|
  |<---- DHCP Offer -------|
  |--- DHCP Request ------>|
  |<--- DHCP ACK ----------|
```

### DHCP ports and OSI layer

- Server: UDP port 67
- Client: UDP port 68
- OSI: Application layer, Layer 7
- Transport protocol: UDP

---

# 17. DNS

**DNS = Domain Name System**

DNS is the system used to translate human-readable names into network addresses and to provide other information about domains and services.

For example:

```text
www.example.com → IP address
```

Instead of remembering an IP address, users can use a domain name.

## DNS hierarchy

DNS is distributed and hierarchical.

A simplified structure is:

```text
Root
 |
 +-- .com
 |    |
 |    +-- example.com
 |
 +-- .org
 |
 +-- .net
```

DNS can involve:

- Root servers
- TLD servers
- Authoritative DNS servers
- Recursive resolvers

## DNS ports

DNS normally uses:

- UDP port 53
- TCP port 53 when TCP is required, including zone transfers and certain larger responses

DNS is an:

**Application layer, OSI Layer 7** protocol.

---

# 18. HTTP

**HTTP = Hypertext Transfer Protocol**

HTTP is the main application protocol used to transfer web resources between clients and web servers.

Examples of clients:

- Web browsers
- Mobile applications
- API clients
- Command-line tools such as curl

HTTP can transfer:

- HTML
- JSON
- Images
- CSS
- JavaScript
- Other resources

## Request-response model

A simplified HTTP exchange:

```text
Client                         Web Server

  |------ HTTP Request -------->|
  |<----- HTTP Response --------|
```

A request may contain a method such as:

- GET
- POST
- PUT
- DELETE
- HEAD

HTTP is generally described as **stateless**, meaning each request is independent unless additional mechanisms such as cookies or application sessions are used.

### HTTP port and OSI layer

- TCP port 80
- Application layer, Layer 7

---

# 19. HTTPS

**HTTPS = HTTP Secure**

HTTPS is HTTP protected by **TLS (Transport Layer Security)**.

TLS provides:

- Encryption
- Integrity protection
- Server authentication through certificates

The basic idea is:

```text
HTTP
  ↓
TLS
  ↓
TCP
  ↓
IP
```

### HTTP vs. HTTPS

| Feature | HTTP | HTTPS |
|---|---|---|
| Typical port | TCP 80 | TCP 443 |
| Encryption | No built-in encryption | TLS encryption |
| Integrity protection | No TLS protection | Yes |
| Server authentication | Not provided by HTTP itself | TLS certificates provide authentication |
| Typical use | Unencrypted web traffic | Secure web traffic |

HTTPS still uses HTTP concepts such as GET and POST. The major difference is that the HTTP communication is protected by TLS.

HTTPS is normally classified as an **Application Layer, Layer 7** protocol, while TLS sits between the application protocols and the transport protocol in the practical protocol stack. OSI mappings for TLS vary somewhat depending on the model being used.

---

# 20. FTP

**FTP = File Transfer Protocol**

FTP is designed to transfer files between a client and server.

It supports operations such as:

- Uploading files
- Downloading files
- Listing directories
- Creating or removing directories
- Authentication

FTP uses separate connections for control and data.

### FTP control connection

The standard control connection uses:

**TCP port 21**

### FTP data connection

In traditional active FTP, the data connection uses:

**TCP port 20**

In passive FTP, the server normally selects a separate data port from a configured range.

### FTP OSI layer

FTP operates at:

**Application layer, Layer 7**

### Security note

Traditional FTP does not provide encryption for credentials and transferred data. Modern deployments generally prefer encrypted alternatives such as:

- FTPS, which adds TLS to FTP
- SFTP, which is a file-transfer protocol running over SSH and is not the same protocol as FTP

---

# 21. TCP

**TCP = Transmission Control Protocol**

TCP is a **connection-oriented transport-layer protocol**.

It provides mechanisms for reliable communication between applications.

TCP provides:

- Connection establishment
- Reliable delivery
- Ordered data
- Acknowledgements
- Retransmission of lost data
- Flow control
- Congestion control

## TCP three-way handshake

Before normal data transfer, TCP establishes a connection using a three-way handshake:

```text
Client                  Server

  |-------- SYN -------->|
  |<----- SYN-ACK -------|
  |-------- ACK -------->|
```

After the handshake, application data can be exchanged.

### TCP reliability

If data is lost, TCP can retransmit it.

If segments arrive out of order, TCP can put the data back into the correct order before presenting the byte stream to the application.

### OSI layer

TCP operates at:

**Layer 4 — Transport layer**

---

# 22. UDP

**UDP = User Datagram Protocol**

UDP is a connectionless transport protocol.

It provides much less overhead than TCP.

UDP does not guarantee:

- Delivery
- Ordering
- Retransmission
- Duplicate protection

Applications use UDP when they want a lightweight transport mechanism and can tolerate or handle loss themselves.

Common examples include:

- DNS
- DHCP
- VoIP
- Some real-time games
- Streaming and other real-time applications

### OSI layer

UDP operates at:

**Layer 4 — Transport layer**

---

# 23. TCP vs. UDP

| Feature | TCP | UDP |
|---|---|---|
| OSI layer | Layer 4 | Layer 4 |
| Connection | Connection-oriented | Connectionless |
| Reliability | Reliable | Best-effort |
| Ordering | Guaranteed | Not guaranteed |
| Retransmission | Yes | No |
| Acknowledgements | Yes | No |
| Flow control | Yes | No |
| Congestion control | Yes | No |
| Overhead | Higher | Lower |
| Header | At least 20 bytes | 8 bytes |
| Typical uses | Web, email, FTP, many APIs | DNS, DHCP, VoIP, real-time traffic |

A useful rule:

> **TCP prioritizes reliable, ordered delivery. UDP prioritizes low overhead and application-controlled behavior.**

"UDP is faster" is an oversimplification. UDP has less protocol overhead and does not wait for TCP-style reliability mechanisms, but the actual application performance depends on the application, network, and implementation.

---

# 24. Ports

A **port** is a 16-bit number used by TCP and UDP to identify an application endpoint or service on a host.

An IP address identifies a host.

A port helps identify the service or application on that host.

For example:

```text
192.168.1.10:443
```

means:

```text
IP address = 192.168.1.10
Port       = 443
```

Together with a transport protocol, this allows traffic to be delivered to the correct application.

A socket can be thought of as an endpoint involving an IP address and port, together with the transport protocol.

## Port ranges

| Range | Name |
|---:|---|
| 0–1023 | Well-known ports |
| 1024–49151 | Registered ports |
| 49152–65535 | Dynamic/private ports |

---

# 25. Important Protocol Ports

| Protocol | Transport | Port | OSI layer |
|---|---|---|---|
| DHCP server | UDP | 67 | Application, L7 |
| DHCP client | UDP | 68 | Application, L7 |
| DNS | UDP/TCP | 53 | Application, L7 |
| HTTP | TCP | 80 | Application, L7 |
| HTTPS | TCP | 443 | Application, L7 |
| FTP control | TCP | 21 | Application, L7 |
| FTP active data | TCP | 20 | Application, L7 |
| SSH | TCP | 22 | Application, L7 |
| Telnet | TCP | 23 | Application, L7 |
| SMTP | TCP | 25 | Application, L7 |
| TFTP | UDP | 69 | Application, L7 |
| POP3 | TCP | 110 | Application, L7 |
| IMAP | TCP | 143 | Application, L7 |
| SNMP | UDP | 161/162 | Application, L7 |
| LDAP | TCP/UDP | 389 | Application, L7 |
| RDP | TCP | 3389 | Application, L7 |
| TCP | — | Uses ports | Transport, L4 |
| UDP | — | Uses ports | Transport, L4 |

The port belongs to the transport-layer communication. The application protocol using that port belongs to the application layer.

---

# 26. DNS Record Types

DNS records describe how domain names and services should be resolved.

## A record

Maps a hostname to an **IPv4 address**.

```text
example.com → 192.0.2.10
```

## AAAA record

Maps a hostname to an **IPv6 address**.

```text
example.com → 2001:db8::10
```

The four A's distinguish it from the IPv4 A record.

## CNAME

Creates an alias from one name to another canonical name.

```text
www.example.com → example.com
```

A CNAME points to another DNS name rather than directly to an IP address.

## MX

Specifies the mail servers responsible for receiving email for a domain.

```text
example.com → mail.example.com
```

MX records also have a priority value.

## TXT

Stores text associated with a domain.

Common uses include:

- Domain verification
- SPF-related information
- DKIM-related information
- Other administrative or policy data

## NS

Specifies the authoritative name servers for a DNS zone.

## SOA

**SOA = Start of Authority**

Contains administrative information about a DNS zone, including information such as:

- Primary/authoritative server
- Zone administrator information
- Serial number
- Refresh timing
- Retry timing
- Expiration timing
- Negative caching/TTL-related information

## PTR

Used for **reverse DNS**.

Instead of:

```text
name → IP
```

PTR supports:

```text
IP → name
```

## SRV

Specifies the location of a service.

It can describe:

- Service name
- Protocol
- Priority
- Weight
- Port
- Target hostname

## CAA

Specifies which certificate authorities are authorized to issue certificates for a domain.

## DS

**DS = Delegation Signer**

Used as part of **DNSSEC** to establish a chain of trust between DNS zones.

## DNSKEY

Contains a public key used by DNSSEC.

## NAPTR

**NAPTR = Naming Authority Pointer**

Can be used for service discovery and rewriting rules, including some VoIP-related systems.

### DNS record summary

| Record | Purpose |
|---|---|
| A | Hostname → IPv4 |
| AAAA | Hostname → IPv6 |
| CNAME | Alias → canonical hostname |
| MX | Mail server |
| TXT | Text/policy/verification information |
| NS | Authoritative name server |
| SOA | Zone authority and administrative information |
| PTR | Reverse DNS |
| SRV | Service location |
| CAA | Allowed certificate authorities |
| DS | DNSSEC delegation signer |
| DNSKEY | DNSSEC public key |
| NAPTR | Service discovery/rewrite information |

ALIAS/ANAME are sometimes offered by DNS providers, but they are not standard DNS record types in the same way as the records above.

---

# 27. Router

A **router** is a networking device that connects different IP networks and forwards packets between them.

For example:

```text
LAN A
192.168.1.0/24
      |
      | Router
      |
LAN B / Internet
```

A router examines the destination IP address and uses a **routing table** to decide where the packet should go.

### Roles of a router

A router can:

- Connect different networks
- Connect a LAN to the internet
- Forward IP packets
- Maintain routing information
- Separate broadcast domains
- Perform NAT
- Provide DHCP services
- Provide firewall functions
- Support VPNs
- Apply QoS policies

Not every router performs every function, but these are common router capabilities.

### Routing protocols

Routers can learn routes through mechanisms such as:

- Static routes
- OSPF
- RIP
- EIGRP
- BGP

---

# 28. Router vs. Switch

| Feature | Switch | Router |
|---|---|---|
| Primary OSI layer | Layer 2 | Layer 3 |
| Address used | MAC address | IP address |
| Main unit | Ethernet frame | IP packet |
| Main purpose | Connect devices in a LAN | Connect different networks |
| Table | MAC address table | Routing table |
| Broadcast domains | Usually one per VLAN | Separate per interface/network |
| NAT | Normally no | Common router function |
| Typical use | LAN connectivity | Inter-network connectivity |

A Layer 3 switch can perform routing, so the distinction is about the primary role of traditional devices rather than an absolute hardware limitation.

---

# 29. OSI Layer of a Router

A traditional router primarily operates at:

**Layer 3 — Network layer**

It uses logical addresses such as IP addresses to determine where packets should be forwarded.

Compare:

```text
Hub    → Layer 1 → Signals
Switch → Layer 2 → MAC addresses / Frames
Router → Layer 3 → IP addresses / Packets
TCP    → Layer 4 → Reliable transport
UDP    → Layer 4 → Connectionless transport
HTTP   → Layer 7 → Web communication
```

---

# 30. Default Gateway

A **default gateway** is the IP address of the router interface that a host uses when it needs to communicate with a destination outside its own local subnet.

For example:

```text
Host:
IP address:       192.168.1.10
Subnet:           192.168.1.0/24
Default gateway:  192.168.1.1
```

If the host wants to reach:

```text
192.168.1.20
```

that destination is on the same subnet, so the host can communicate directly at the local network level.

If it wants to reach:

```text
8.8.8.8
```

that destination is outside the local subnet.

The host therefore sends the packet toward:

```text
192.168.1.1
```

The router then forwards the packet toward the remote network.

### Important points

- The default gateway is normally a router's interface on the local subnet.
- The gateway must be reachable from the host.
- It acts as the host's normal exit point to other networks.
- Without a default gateway, local communication can still work, but communication with remote networks normally cannot.

---

# 31. Routing Table

A **routing table** is a database maintained by a router or Layer 3 device containing information about reachable networks.

It answers the basic question:

> **"Where should I send this packet?"**

A routing table can contain entries such as:

| Destination | Next hop | Interface | Metric |
|---|---|---|---:|
| 192.168.1.0/24 | Directly connected | G0/1 | 0 |
| 192.168.2.0/24 | 10.0.0.2 | G0/0 | 1 |
| 0.0.0.0/0 | 203.0.113.1 | G0/2 | 10 |

### Important routing-table fields

#### Destination network

The network the router knows how to reach.

Example:

```text
192.168.2.0/24
```

#### Prefix/subnet mask

Defines how large the destination network is.

For example:

```text
/24
```

means the first 24 bits represent the network prefix.

#### Next hop

The address of the next router to which the packet should be forwarded.

#### Outgoing interface

The local interface through which the packet should leave.

#### Metric

A value used by routing mechanisms to compare routes. The meaning of the metric depends on the routing protocol.

#### Administrative distance

A value used by some routing implementations to determine how trustworthy a route source is when routes are learned from different sources.

---

# 32. How a Router Uses the Routing Table

When a router receives an IP packet:

### Step 1: Read the destination IP

The router examines the destination address in the packet.

### Step 2: Search the routing table

It looks for routes that match the destination.

### Step 3: Select the best match

If several routes match, routers use the **longest-prefix match** principle.

For example:

```text
10.0.0.0/8       → Route A
10.1.0.0/16      → Route B
10.1.2.0/24      → Route C
```

For:

```text
10.1.2.50
```

all three routes match, but:

```text
10.1.2.0/24
```

is the most specific route.

Therefore Route C is selected.

### Step 4: Forward the packet

The router sends the packet through the appropriate interface toward the next hop.

### Step 5: No matching route

If no route matches, the router normally drops the packet unless it has a **default route**.

---

# 33. Default Route

A default route is represented by:

```text
0.0.0.0/0
```

It matches destinations that do not match a more specific route.

For example:

```text
192.168.1.0/24 → local network
10.0.0.0/8     → internal network
0.0.0.0/0      → everything else
```

The default route is commonly used to send internet-bound traffic toward an upstream router.

---

# 34. Where Routes Come From

A router can learn routes in several ways.

### Directly connected routes

When an interface is configured with an IP address and subnet, the router can automatically know that network is directly connected.

### Static routes

An administrator manually configures a route.

Example conceptually:

```text
Destination: 192.168.2.0/24
Next hop:    10.0.0.2
```

### Dynamic routing

Routers can exchange routing information using routing protocols.

Examples:

- OSPF
- RIP
- EIGRP
- BGP

Dynamic routing is useful when networks are large or paths can change.

---

# 35. Putting Everything Together

A typical request to a website involves many of the concepts above.

Suppose a computer wants to visit:

```text
https://example.com
```

A simplified process is:

```text
1. DHCP
   ↓
   The computer obtains an IP address,
   subnet mask, gateway, and DNS server.

2. DNS
   ↓
   example.com is resolved to an IP address.

3. Default gateway
   ↓
   If the web server is outside the local subnet,
   the computer sends traffic toward its router.

4. Switch
   ↓
   The local Ethernet frame is forwarded through
   the LAN using MAC addresses.

5. Router
   ↓
   The router examines the destination IP and
   consults its routing table.

6. TCP
   ↓
   A reliable transport connection is established
   when the application uses TCP.

7. TLS
   ↓
   HTTPS establishes cryptographic protection.

8. HTTP
   ↓
   The browser sends an HTTP request and receives
   an HTTP response.

9. Response
   ↓
   The data travels back through the network.
```

This shows how different layers cooperate rather than replacing each other.

---

# 36. Layer-by-Layer Mental Model

A useful way to remember the concepts is:

```text
Application
Layer 7
HTTP, HTTPS, DNS, DHCP, FTP, SSH
        ↓
Transport
Layer 4
TCP, UDP, ports
        ↓
Network
Layer 3
IP, routers, routing tables, default gateway
        ↓
Data Link
Layer 2
Ethernet frames, MAC addresses, switches
        ↓
Physical
Layer 1
Electrical/optical signals, cables, connectors, hubs
```

The simplified relationship is:

```text
Application data
      ↓
TCP/UDP segment or datagram
      ↓
IP packet
      ↓
Ethernet frame
      ↓
Physical signal
```

At the receiving device, the process is reversed.

---

# 37. Essential Facts to Memorize

### Ethernet

- RJ-45/8P8C → common connector for twisted-pair Ethernet
- T568A and T568B → wiring schemes
- Straight-through → same wiring standard on both ends
- Crossover → different wiring standards on the ends
- Auto-MDIX → automatically handles transmit/receive orientation on modern equipment
- 10BASE2 → thin coax, 10 Mbps, approximately 185 m
- 10BASE5 → thick coax, 10 Mbps, 500 m
- 10BASE-T → twisted pair, 10 Mbps
- 100BASE-TX → 100 Mbps
- 1000BASE-T → 1 Gbps, four pairs
- 10GBASE-T → 10 Gbps copper

### Devices

- Hub → Layer 1
- Switch → Layer 2
- Router → Layer 3
- Layer 3 switch → can also route

### Transport

- TCP → Layer 4, connection-oriented, reliable, ordered
- UDP → Layer 4, connectionless, best-effort, low overhead
- Ports → identify application/service endpoints for TCP/UDP

### Important ports

- FTP → 20/21 TCP
- SSH → 22 TCP
- Telnet → 23 TCP
- SMTP → 25 TCP
- DNS → 53 UDP/TCP
- DHCP → 67/68 UDP
- TFTP → 69 UDP
- HTTP → 80 TCP
- POP3 → 110 TCP
- NTP → 123 UDP
- IMAP → 143 TCP
- SNMP → 161/162 UDP
- LDAP → 389 TCP/UDP
- HTTPS → 443 TCP
- RDP → 3389 TCP

### DNS records

- A → IPv4
- AAAA → IPv6
- CNAME → alias
- MX → mail server
- TXT → text/policy/verification
- NS → name server
- SOA → zone authority information
- PTR → reverse DNS
- SRV → service location
- CAA → certificate authority policy
- DS/DNSKEY → DNSSEC

### Routing

- Router → forwards packets between networks
- Routing table → tells the router where networks can be reached
- Default gateway → local router used to reach remote networks
- Default route → `0.0.0.0/0`
- Longest-prefix match → most specific matching route wins
- Static routes → manually configured
- Dynamic routes → learned through routing protocols

---

# 38. Final Conceptual Summary

Networking becomes much easier once the responsibilities are separated:

```text
Cable / Physical
        ↓
"How do the signals physically travel?"
        ↓
Ethernet / MAC / Switch
        ↓
"Which local device should receive this frame?"
        ↓
IP / Router / Routing table
        ↓
"Which network should receive this packet?"
        ↓
TCP / UDP / Port
        ↓
"Which application should receive this data?"
        ↓
HTTP / DNS / DHCP / FTP / HTTPS
        ↓
"What service or application is communicating?"
```

The central idea is that networking is a stack of cooperating layers:

- **Physical layer** moves signals.
- **Data Link layer** moves frames between local devices.
- **Network layer** moves packets between networks.
- **Transport layer** provides application-to-application communication and uses ports.
- **Application layer** defines the actual network services applications use.

Understanding those responsibilities makes the individual protocols much easier to remember.
