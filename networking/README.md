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