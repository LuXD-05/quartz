---
public: true
edited_seconds: 10
modified_at: 02/04/2024 11:15:42
---
Circuit switching (ex: telephone network)

Physical infrastructure made of **circuit switches** and **transmission media**, **before** the **communication**, a **connection** is **established** **between** the **transmitter** **and** the **receiver** **at** a **physical** **level** (**_virtual circuit_**); it **stays reserved**.

Network layer protocols provide a **connection-oriented** and **reliable** service.

Packet switching (ex: internet)

The **data** is **organized in packets** and travels in an infrastructure made of **transmission media** and **packet switching** **nodes** (**PSN**). **Packet switches choose the** packet’s path considering: **info about the receiver** and **network state**. Network resources are provided **on demand** to individual packets.

Network layer protocols provide a **connectionless** and **unreliable** service.

**Types of service**

Protocols are designed to work in 2 ways:

Connection-oriented

Before communicating, a handshake is performed: the transmitter network protocol exchanges control packets with the receiver network protocol. This is done because:

-      **Transmitter** --> checks if the **receiver is available**,

-      **Receiver** --> **prepares** it **to receive** packets,

-      (**Both** --> to agree on any parameters).

Once the **handshake** is **done**, the **communication begins**; at the **end** of which, follows a phase of demolition (connection termination) that frees the resources used for communicating.

“_Connection oriented_” as it occurs between **logical** **layers** with information saved in memory and protocols; **not** **involving** any aspect of the **physical** layer. The connection is **virtual**.

Connectionless

**No handshakes** are performed, when the transmitter has data to send, it sends it.

Reliability

Protocols can ensure reliable data delivery or not give guarantees about data delivery. The service can be:

Reliable

Ensures that **data** is **delivered** **correctly**, **without duplicates**, **lossless** and in the **right order**. If a **packet** is **corrupted**, it’s **retransmitted** by the transmitter.

Unreliable

The **service doesn’t guarantee anything**. **Corrupted packets** will be simply **discarded** by the receiver.