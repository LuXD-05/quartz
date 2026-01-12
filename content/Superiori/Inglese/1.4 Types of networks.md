### Types

##### Circuit switching

<u>Physical</u> infrastructure made of **circuit switches** and **transmission media**, before the communication, a <u>connection is established</u> between the transmitter and the receiver at a physical level (*virtual circuit*); it stays <u>reserved</u> (ex: telephone network).

Network layer protocols provide a **connection-oriented** and **reliable** service.

##### Packet switching

Packets travel in an infrastructure made of **transmission media** and **packet switching nodes** (PSN). Routers choose the packet’s path considering: <u>info about the receiver</u> and <u>network state</u>. Network resources are provided **on demand** to individual packets (ex: internet).

Network layer protocols provide a **connectionless** and **unreliable** service.

### Modes

##### Connection-oriented

Before communicating, a ***handshake*** is performed: the transmitter network protocol <u>exchanges control packets</u> with the receiver network protocol. This is done because:

- **Transmitter**: checks if the receiver is available,
- **Receiver**: prepares it to receive packets,
- (**Both**: to agree on any parameters).

Once the **handshake** is done, the communication begins; at the end of which, follows a phase of **termination** that frees the resources used for communicating.

“*Connection oriented*” as it occurs between logical layers with information saved in memory and protocols; not involving any aspect of the physical layer. The connection is **virtual**.

##### Connectionless

**No handshakes** are performed, when the transmitter has data to send, it sends it.

### Reliability

###### Reliable

Ensures that data is delivered <u>correctly</u>, <u>without duplicates</u>, <u>lossless</u> and in the <u>right order</u>. If a packet is <u>corrupted</u>, it’s <u>retransmitted</u> by the transmitter.

###### Unreliable

The service <u>doesn’t guarantee anything</u>. <u>Corrupted packets</u> will be simply <u>discarded</u> by the receiver.

