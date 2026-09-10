
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
