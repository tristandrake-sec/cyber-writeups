## OSI-Model

**## What it is**

- The OSI model is a broad description of how network communication works, split into 7 layers. Understanding it makes conversations between people a lot easier — everyone has a shared reference.
- Mnemonic: **All People Seem To Need Data Processing** (Application → Physical).

**## The layers**

- **Layer 1 — Physical.** The physical signals sent through cables and fibers. Getting a signal from one part of the network to another. Issues are things like bad fiber or cable. A lot of troubleshooting here is testing cables, fibers, adapter cards, devices.
- **Layer 2 — Data Link.** Communication between two devices. Also called the MAC address layer. Usually associated with network cards (ethernet, wireless). MAC = Media Access Control address, also called a hardware address. Referred to as the switching layer — problems here may be with switches.
- **Layer 3 — Network.** The routing layer. Routers determine how to forward traffic, looking at IP addresses for the next hop. Also the layer that fragments frames into smaller pieces to fit through the network, then reassembles them on the other side.
- **Layer 4 — Transport.** The ability to transport data from one place to another — the "post office" layer. Protocols are TCP and UDP. Responsible for getting data from IP packets from one device to another. Before sending, we may have to make a session.
- **Layer 5 — Session.** Provides communication management between point A and point B. Stopping, starting, and restarting the session lives here.
- **Layer 6 — Presentation.** Putting data into a format we'll see with our own eyes. Application encryption and decryption. Operates right before we see the data.
- **Layer 7 — Application.** What we see on the screen. Common ones are HTTP, HTTPS, POP3.

**## What lives at each layer**

- **1** — cables, fibers, the signal itself
- **2** — frame, MAC addresses, extended unique identifier, switch
- **3** — IP address, router, packet
- **4** — TCP segment, UDP datagram
- **5** — control protocols, tunneling protocols
- **6** — application encryption (SSL/TLS)
- **7** — your eyes

**## Example: loading a webpage**

- **Physical** — electrical signals
- **Data Link** — ethernet
- **Network** — IP encapsulation
- **Transport** — TCP encapsulation
- **Session** — links the presentation layer to the transport layer
- **Presentation** — SSL encryption
- **Application** — [https://mail.google.com](https://mail.google.com)

**## What I mixed up**

- Mixed up fragmentation and segments. **Fragmentation** is at layer 3 — IP breaks a packet into smaller pieces when it's too big for the network hop, and reassembles at the destination. **Segments** are layer 4 — TCP splits the application data into segments the connection can carry, and reassembles at the far end.
- Also confused these with the OS memory-management meanings of the same words. Same terms, different field, different definitions.

## Networking Devices


**## What it is**

- A data center has many devices working together. Every device has a purpose, and the implementation may change over time. Once installed it's difficult to move. New technologies appear all the time.

**## Router**

- Takes data from one IP subnet and routes it to another.
- Layer 3 OSI device, relating to IP addresses.
- May be built into a switch — "layer 3 switch." The switch is still layer 2, just inside the same equipment.
- Often connects various networks: LAN, WAN, etc. Can be fiber or copper based.

**## Network switch**

- Functions at the MAC address layer — OSI layer 2, the data link layer.
- Bridging done in hardware, usually associated with an ASIC.
- Many ports and features. May provide PoE (Power over Ethernet).

**## Access point**

- Allows a wireless connection from our device to the rest of the network. Bridges the connection between the wireless and wired network.
- Layer 2 OSI device.
- Wireless networks are everywhere and don't have just a single access point. Configurations may change at any point — you need to make sure users can roam from one access point to another.

**## Centralized management**

- A centralized management tool lets you manage all access points from one spot.
- Can deploy new access points, do monitoring and alerting, configure changes and push them to all access points, and generate reports.
- These are proprietary systems.

**## Firewall**

- Filters traffic based on TCP or UDP.
- A modern one is likely an **NGFW** (next-generation firewall), which can identify the applications traversing the network and decide whether they're allowed.
- Can encrypt traffic, VPN between sites.
- Most firewalls can function as a layer 3 device and act as a router. Sits between the ingress and egress of the network — you rely on it to communicate between inside and outside.
- Supports NAT.

**## IDS / IPS**

- **IDS** — Intrusion Detection System. **IPS** — Intrusion Prevention System.
- Both look for inbound attacks on the network and identify them. May be exploits against operating systems, applications, etc.
- Detection alarms or alerts. Prevention stops it before it gets into the network.

**## Load balancer**

- Distributes massive loads across multiple servers, maintaining uptime and availability.
- Good at detecting outages and continuing to function.
- Can optimize communication through TCP offload, and function as SSL offload (handling decrypt/encrypt).
- Can perform caching, prioritize specific traffic (QoS), and do content switching.

**## Proxy**

- Manages connections by sitting in the middle of the conversation. Takes the user's request, performs it, receives the answer, verifies it isn't malicious, then provides it to the end user.
- Useful for caching, URL filtering, and content scanning.
- **Explicit** — applications need to be configured to use it. **Transparent** — invisible to the application.

**## NAS / SAN**

- **NAS** (network attached storage) — file-level access.
- **SAN** (storage area network) — very efficient at reading and writing, uses block-level access, which changes only the blocks necessary.
- Both need a lot of bandwidth and may use their own isolated network.

**## What I mixed up**

- Missed QoS (Quality of Service) — manages and prioritizes data traffic so critical applications maintain performance during network issues. Not tied to one device: implemented on routers, switches, firewalls, and load balancers. Also wrote "PoS" for it in my notes, which is point-of-sale, unrelated.

