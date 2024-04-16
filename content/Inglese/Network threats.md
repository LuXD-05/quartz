---
public: true
edited_seconds: 60
modified_at: 16/04/2024 21:49:37
---
### Network Threats
##### DoS
An **attacker send more requests to a pc than the ones it can handle**. Then, eventually, the <u>attackers connects on a service port to make forged packets enter the user's network</u> (more on [[DoS]]).
##### Packet sniffing
An intruder can place a **packet sniffer** (tool used to <u>monitor packets in a network</u>) to **capture and analyse network traffic** (also, it's hard to detect it).
##### Port stealing
In this **traffic is stolen** and **directed to another port of a switch**. This allows someone to <u>receive packets originally directed to another pc</u> by <u>making the switch believe</u> that the <u>attacker's port is the correct</u> destination.
##### Unauthorised access
The term defines different types of attacks that aim to access info that a pc shouldn't provide (such as: accessing with someone else's account or guessing the password).
##### Destructive attacks
The term includes those that are called ***cyberattacks***, attacks employed by individuals or organisations, which are carried out against pc systems, infrastructures or networks in order to <u>steal, alter or destroy data</u>.
##### Spoofing
An ***IP spoofing attack*** is one in which the source **IP address of a packet is forged**. It divides in 2 types of attacks:
###### Spoofing-based DoS attacks
In an **IP spoofing-based DoS attack**, an attacker sends a packet with a <u>forged IP address</u> to a target host, which <u>sends an ACK back</u>. The host then <u>waits for a response that never comes</u>, resulting in the **accumulation of memory allocated** for each query **in the buffer**. After enough spoofed queries sent, the target's buffer will **overflow** and the device will **crash**.
###### MITM attacks
In **MITM** (***man-in-the-middle***) attacks, a **middleman** <u>intercepts traffic between 2 devices</u> and can either <u>monitor</u> or <u>alter</u> the data (users may never know that the traffic is being intercepted). 
Usually the middleman watches traffic, until an user sends a request to another device; that's when the attacker sends a **spoofed response** saying that the requested host is a <u>different device</u>. The communication starts and the compromised device continues to receive info even if a <u>response from the legitimate pc arrives</u>, because it will override the 1st.