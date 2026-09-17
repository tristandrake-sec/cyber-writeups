
**thm/linux-fundamentals**

**## Room / date**

- Linux Fundamentals — Monday 9/7

**## What it covered**

- Basic concepts like terminal text editors, package management, system logs, and various daily utilities, while getting comfortable with a terminal

**## What I actually did**

- Worked in the CLI running basic commands and using special characters that combine with basic commands

**## Where I got stuck**

- Reached for `file readme` when I wanted `cat readme` — `file` gives you the type ("ASCII text"), `cat` gives you the contents
- Tried to SSH into the AttackBox's own IP instead of the target machine's. Two separate boxes, two separate IPs, and the target has to be deployed separately

**## What I'd remember next time**

- Remember essential/basic commands to minimize lab time and get the proper response without assistance

---

**thm/networking-concepts**

**## Room / date**

- Networking Concepts — Tuesday 9/8

**## What it covered**

- Basic concepts like UDP and TCP, the OSI model, IP addresses and subnets, telnet, and encapsulation

**## What I actually did**

- Worked in the CLI, specifically with telnet, and got comfortable with certain ports/IP addresses
- Made a manual HTTP request: `GET / HTTP/1.1`, then `Host: telnet.thm`, then a blank line
- Identified the server from the response header — lighttpd/1.4.63

**## Where I got stuck**

- Got a 400 Bad Request because I sent the GET line without the Host header. HTTP/1.1 requires it
- Connection kept closing before I finished typing — the server times out idle connections fast, so you have to paste or type quickly

**## What I'd remember next time**

- The blank line is what tells the server the headers are done and to process the request

**thm/windows-fundamentals**

**## Room / date**

- Windows Fundamentals — Wednesday/Thursday 9/9–9/10

**## What it covered**

- Basic commands, where to find certain file systems or folders, setting and finding permissions for users, Task Manager usage, and User Account Control, while introducing System Configuration and advanced settings

**## What I actually did**

- Worked in a Windows lab setup, identifying where certain file systems and folders were and how to reach them through commands
- Worked on understanding and changing certain settings

**## Where I got stuck**

- Directions in the lab became unclear and I had to search my way around to find the answers needed to move on to the next part

**## What I'd remember next time**

- Remember essential/basic commands to minimize lab time and get the proper response without assistance

**thm/windows-fundamentals-3**

**## Room / date**

- Windows Fundamentals 3 — Monday 9/14

**## What it covered**

- Built-in Microsoft security tools designed to keep devices and data secure.

**## What I actually did**

- Viewed Windows Update & Security, deep-diving into specific sections: virus and threat protection, firewall and network protection, app and browser control, exploit protection, device security, core isolation, security processor details, BitLocker, and Volume Shadow Copy Service.
- Learned what these settings are, how they work, and how to properly configure them.

**## Where I got stuck**

- Didn't get stuck anywhere — mainly read-and-respond, didn't configure much myself.

**## What I'd remember next time**

- How to configure my own computer properly with the given info, and lock down the terms used in the room.

---

**thm/networking-essentials**

**## Room / date**

- Networking Essentials — Tuesday 9/15

**## What it covered**

- Protocols and technologies that enable automatic configuration, routing, and packet delivery.

**## What I actually did**

- Read and learned about DHCP, ARP (bridging from layer 3 addressing to layer 2 addressing), ICMP, routing, and NAT.
- Worked in the terminal with each topic — found echo ping requests, destination MAC addresses in an ARP request, and the destination IP address used when a client sends a DHCP discover packet.

**## Where I got stuck**

- Struggled toward the end with echo ping requests and how many bytes were being sent in the echo request.

**## What I'd remember next time**

- How to properly identify the number of bytes sent by echo ping requests.

---

**thm/active-directory-basics**

**## Room / date**

- Active Directory Basics — Wednesday 9/16 & Thursday 9/17

**## What it covered**

- Core concepts and functionality of Microsoft's Active Directory within a Windows domain environment.

**## What I actually did**

- Read and learned about Active Directory, Domain Controllers, managing users and computers in AD, group policy management, authentication methods, trees, forests, and trusts.
- Connected to the DC, reset Sophie's password as Phillip, forced a reset at next login, and logged in as Sophie to retrieve the desktop flag.

**## Where I got stuck**

- Getting the login flow to work — logging in as Phillip, forcing the reset, then logging in as Sophie.

**## What I'd remember next time**

- Sometimes TryHackMe doesn't provide all the info necessary, and you may need outside resources to answer the questions.
