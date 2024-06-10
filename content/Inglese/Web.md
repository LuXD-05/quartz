### HTML

It’s the **standard markup language to create web pages**. Consists of several key components, including **tags** and **attributes**, character-based data types, character references and entity references. HTML tags come in **pairs**, called the **opening** (start) and **closing** (end) **tags**.

##### Markup language

System for structuring a document’s content in a way that is syntactically distinguishable from the text.

### HTTP

***HyperText Transfer Protocol*** is an <u>application protocol used to load webpages</u> using hypertext links. It’s the foundation of data communication on the WWW.

##### HTTPS

It consists of communications over **HTTP** in a connection **encrypted by TLS**.

Main reasons: **auth** for visited websites & **privacy** and **integrity** of exchanged data.

### TLS

***Transport Layer Security*** is a cryptographic protocol that <u>provides communication security over a network</u>.

- Connection is <u>private</u> thanks to <u>symmetric cryptography used to encrypt data</u>,
- The <u>identity of the</u> communicating <u>parties can be authenticated with public key cryptography</u>,
- Connection ensures <u>integrity</u> because the messages include an <u>integrity check with a message auth code</u>.

### URL

A **URL** is a <u>reference to a web resource</u> that specifies its location on a pc network & a mechanism for retrieving it.

##### Parts

A URL is made of:

1) **Scheme**: <u>protocol</u> used to access the resource in internet (<u>HTTP or HTTPS</u>).
2) **Host**: <u>host</u> that the web client wants <u>to access</u>.
3) **Path**: <u>resource</u> that the web client wants <u>to access</u>.

##### Query string

<u>String</u> (after the path in the URL) that <u>provides info that the resource can use</u> for some purpose, like: user data, port, query, fragments…

### Internet

1) Internet as a Network Infrastructure

Hardware and software that implement the network conveying data:

- **Hw**: **physical devices** (packet switches or routers, but hosts/_end-systems_ too, because they are access devices).
- **Sw**: **components** (TCP/IP protocols).

2) Internet as a Service Infrastructure

- **Services**: apps for web browsing (email, chats, news, socials…).
- **Service providers**: ISP (Internet Service Providers).

### Infrastructure

Set of complementary elements and activities necessary to carry out a main activity.

**Internet as a Network Infrastructure**

Internet

**Pc network which interconnects millions of hosts**/end-systems (pcs, servers, phones, webcams, TVs…) **in the world**.

End-systems

Or **terminals**, because they are **at the edges of the network**; & **hosts** because they **host network apps & protocols**.

Hosts are interconnected through **links** (physical copper/fiber or wireless) and **packet switches**.

Transmissive media vs links

Transmissive media are **physical links on which a signal goes from 1 point to another of a network**. **When 2 hosts try to contact one another**, a **link between them is established on/through the transmissive media**.

The transmission media can hold **multiple links** (communication channels) if they are set on **different frequencies**. (ADSL on band 0-4 kHz, like for Public Switch Telephone Network; data transmission on band 25 kHz – 1.1 MHz).

Packet switches

**On** the **internet data** is **sent in packets**. **Packets contain** the **receiver’s address** (info to get to it).

**Packet switches choose the path to forward packets** so that they can reach their destination.

### ISP

**Internet Service Providers**, they **offer services to enable hosts to access** the **internet** (like Telecom, FastWeb…).

Each ISP has a network of packet switches connected to each other and to other ISP’s switches through links.

ISPs are organized in a hierarchical Tier structure.   The **set of standard internet protocols** is the **TCP/IP**.

Packet switch networks use the IP protocol and follow conventions defined by IPv4 and IPv6 protocols.

On the other hand, hosts also use protocols that define the structure of packets & control their sending & receiving.

### RFC (Request for Comments)

In those is published **documentation** about the technologies, methods and protocols **for the internet by** the **IETF** (Internet Engineering Task Force). **RFCs** are **identified by numbers**.

### STDs (Interned Standards)

**Some RFCs** officially **designated as STDs**, **identified by an STD number** (that **doesn’t change** even if the RFC number which it refers to changes). Some are **required** (**basic protocols for internet to work**), while others are **recommended**.

**Internet as a Service Infrastructure**

**Internet** can also be described as an **infrastructure that offers app-type services** (like email, chat, VoIP, streaming, games, P2P, auth, ecommerce…). Applications offered as network services are called **distributed**, because they **involve multiple hosts** that exchange data. App is a program that runs on hosts, written in C, C#, Java…

So, the IaaS is made of apps and the network including all hosts running the software.

