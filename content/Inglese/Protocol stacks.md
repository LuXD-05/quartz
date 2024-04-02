---
public: true
edited_seconds: 10
modified_at: 02/04/2024 11:15:16
---
Networks are complex and in order to communicate, devices must follow network protocols organized in stacks.

Network architectures

ISO/OSI (International Standard Organization / Open System Interconnection)

(Doesn’t correspond to real network) it’s a system defined by **ISO**, specifically **Zimmermann** in **1980** as 1st step to **standardize** international **protocols** for the various levels. Concerns the interconnection of open systems, as defined by the EU Commission.

TCP/IP

Is the architecture over which **Internet is based nowadays**, defined by **Cherf** and **Kahn** in **1974**. Its goal was to give an organic structure to the already existing protocols (the 1st ARPAnet).

Hybrid model layers

Physical (ISO/OSI)

Handles the **transmission of bits** with the purpose of **transmitting them from 1 end of a physical link to the other**. Service offered at highest level to ensure that each bit at 1 is received with that value. This layer:

-      Establishes the signals for the link (electrical, optic, wireless) to represent 1 and 0,

-      How long a bit lasts,

-      If transmission is full duplex or not,

-      How to establish and end a connection,

-      Shape and size of the connectors,

-      Type of transmission mediums/means.

**Hubs** operate at physical level.

Datalink (ISO/OSI)

**Transfers frames from a node to another** (services and protocols for this are various, like WiFi or Frame Relay).

**Switches** and **bridges** operate at this level.

Network (TCP/IP)

**Transfers datagrams from a host to another**, **handling** also the **path to reach the destination**. The IP (Internet Protocol) is used in **IPv4** and **IPv6** versions, but also the **ICMP**.

**Routers** operate in this level.

Transport (TCP/IP)

(Only in hosts), 2 POVs:

-      **Transmitting** host --> handle **data from** **application layer and transfer it to the network layer**,

-      **Destination** host --> handle **datagrams from layer 3 and deliver the data to the correct application protocol**.

Used protocols: **TCP** and **UDP**.

Application (TCP/IP)

(Only in hosts), **interfaces a program to the physical network**, allowing apps to communicate with other ones. Many protocols in this layer: HTTP/S for web pages, SMTP/POP3/IMAP for emails, FTP for file transfer, DNS for IP addresses…