---
public: true
modified_at: 28/04/2024 00:30:37
---
### Datagram IPv4
Hint: VHDTIFRDMFTPHIIO
::
- ***Version*** \[4 bit\]: contiene il valore binario "0100", ovvero 4 per indicare che il pacchetto è IPv4.
- ***Header length*** \[4 bit\]: indica la lunghezza dell'header del pacchetto (l'offset del *payload*), lungo da 20 a 60 byte in base alla presenza e la lunghezza delle *options*.
- ***Differentiated services*** (DS) \[8 bit\]: (prima era ***Type of Service*** ToS) ed è usato per determinare la priorità del pacchetto (tipo per le nuove tecnologie di *real-time streaming*).
- ***Total length*** \[16 bit\]: dimensione di *header* + *payload* (da 20 a 65535 byte ma spesso 1500 byte).
- ***Identifier*** \[16 bit\]: identifica univocamente i frammenti in cui potrebbe essere stato frammentato un pacchetto IP.
- *Flag* \[3 bit\]: bit usati per il controllo di frammentazione.
	- ***Reserved***: flag posto sempre a 0 (RFC 3514 "*[Evil bit](https://en.wikipedia.org/wiki/Evil_bit)*").
	- ***DF*** (*don’t fragment*): se posta a 1 il pacchetto non è frammentabile e viene scartato se non può essere inviato senza frammentarlo; altrimenti (a 0) è frammentabile.
	- ***MF*** (*more fragments*): se posta a 0 indica che il pacchetto è l'unico o l'ultimo frammento, mentre a 1 indica che dopo questo ci sono altri frammenti.
- ***Fragment offset*** \[13 bit\]: garantisce l'ordinamento dei frammenti specificando in che punto vanno inseriti (misurato in blocchi di 8 byte).
- ***TTL*** (*Time to Live*) \[8 bit\]: è il n° di hop max che un pacchetto può attraversare e viene diminuito ad ognuno. Quando arriva a 0, il router scarta il pacchetto e invia un messaggio **ICMP** ***time_exceeded*** all'origine.
- ***Protocol*** \[8 bit\]: indica il protocollo livello trasporto a cui consegnare il payload.
- ***Header checksum*** \[16 bit\]: verifica l'integrità dell'header IP.
- **IPv4 origine** \[32 bit\]: è l'IPv4 di origine (sempre unicast).
- **IPv4 destinazione** \[32 bit\]: è l'IPv4 di destinazione (unicast, multicast o broadcast).
- ***Options***: con queste si possono richiedere elaborazioni speciali del pacchetto.
<!--SR:!2024-04-30,2,200-->

### Indirizzi IP e IPv4
Hint: cosa fa IP?, IPv4 byte, notazione, net e host ID
::
##### IP (Internet Protocol)
1) Identifica un host in una rete,
2) Fornisce il path per raggiungere gli host,
3) Rende possibile la comunicazione tra host.
##### IPv4
4 byte $\;\rightarrow\;$ ogni byte convertito in decimale $\;\rightarrow\;$ forma ***dotted decimal*** $\;\rightarrow\;$ 32 bit in 4 gruppi di 8 (Es: "192.168.0.1"). IPv4 è composto da:
- **Net ID**: parte che identifica la **rete** (per instradamento a livello **subnet**)
- **Host ID**: parte che identifica gli **host** (per instradamento a livello **host**).
<!--SR:!2024-05-01,3,220-->

#### Politiche di distribuzione IPv4
Hint: classful e classless
::
Gli IPv4 sono distribuiti con 2 **politiche**:
##### Classful
Basata su:
- Suddivisione degli indirizzi in 5 **classi** (**A, B, C, D, E**)
- Separazione tra **Net ID** e **Host ID**
Con questo si assegnavano blocchi di indirizzi con *prefix length* (parte di IPv4 = a **Net ID**) **fissa** (/8, /16, /24).
**Svantaggio**: se ho 270 host devo per forza usare una /16 quindi enorme spreco di indirizzi su 65535.
##### Classless (CIDR)
Usa delle *prefix length* **variabili** da 1 a 31 quindi:
- Riduce problema esaurimento indirizzi IP,
- Gestione + efficiente di IP di organizzazioni.
Quando si configura un host gli si fornisce:
- **IPv4**
- **Subnet mask** (come IPv4 in dotted decimal, tipo /24 = 255.255.255.0): bit a 1 = Net ID, bit a 0 = Host ID.
<!--SR:!2024-05-01,3,220-->

#### Indirizzo di rete
::
Serve per sapere se spedire pacchetti localmente o a gateway verso internet e a quale rete appartiene esso.
- Destinazione **locale**: pacchetto inviato sul link.
- Destinazione **remota**: pacchetto inviato a dispositivo livello 3 (router).
Cambia quindi il **MAC del frame datalink**: per dest locale = MAC destinatario e per remota = MAC gateway.
L'indirizzo di rete si ottiene facendo un **AND** tra i bit di un **IPv4** e la sua **subnet mask**.
<!--SR:!2024-05-01,3,220-->

### Assegnazione indirizzi a NIC
::
Gli IP sono assegnati alle **NIC** (*Network Interface Card*) dei dispositivi, e l’assegnazione può essere:
- **Statica**: per stampanti/server/dispositivi accessi per mezzo di un **IP fisso** (**rischio**: conflitti),
- **Dinamica**: Con il [[8 VLAN#DHCP|DHCP]], per dispositivi locali che cambiano spesso. DHCP controlla gli IP della rete dando agli host quelli non statici e non crea conflitti.
<!--SR:!2024-05-01,3,220-->

### Indirizzamento
Hint: unicast, multicast, broadcast (2), loopback e link local.
::
##### Unicast
Tipo di comunicazione **host to host** (C/S o P2P) tra **1.1.1.1 e 223.255.255.255** (molti riservati)
##### Multicast
Comunicazione per spedire un pacchetto a un **gruppo di host** tra **224.0.0.0 e 239.255.255.255**.
##### Broadcast
Comunicazione per spedire un pacchetto a **tutti gli host di una rete**. Di 2 tipi:
###### Limitato
Avente IP 255.255.255.255, il pacchetto è mandato a **tutti gli host della subnet in cui è inviato** ed è *non routable*, ovvero <u>non viene inoltrato dal gateway ad altre subnet/reti</u>,
###### Diretto
Questo è il broadcast di una rete ed è detto **diretto** perché usa **l’indirizzo + alto di una rete** con tutti i suoi **bit dell’host ID a 1**. Al contrario del limitato è *routable*, e viene usato per <u>mandare broadcast ad altre reti</u> (ponendo l'indirizzo broadcast della rete a cui si vuole inviare il pacchetto come IP di destinazione).
##### Loopback
Indirizzo **127.0.0.1** e indica l’indirizzo stesso di un host (usato in app client/server sullo stesso per comunicare).
##### Link local
Usati dagli OS per riferirsi a host **senza IPv4**, da **169.254.0.0** e **169.254.255.255**.
<!--SR:!2024-04-30,2,200-->

### Tipi di IP
Hint: pubblici e privati.
::
##### Pubblici
Instradati a **livello globale** tra i router degli **ISP** e permettono di <u>identificare e raggiungere un host globalmente</u>. I dispositivi in una LAN usano tutti lo **stesso IP pubblico** (dato al **gateway**).
##### Privati
Usati per assegnare IPv4 a **livello locale**, rendono accessibili gli host in una LAN e <u>non sono visibili dall’esterno</u>. Al fine di far comunicare quindi un host di una rete privata con un host in internet è necessario il **[[3 NAT]]**.
<!--SR:!2024-05-01,3,220-->