---
public: true
modified_at: 28/04/2024 00:25:45
edited_seconds: 50
---
### IPv6
Hint: intro, perché, rappresentazione e regole (per cifre)
::
È il successore di IPv4 e come esso è best-effort, connectionless e media independent. Spazio di indirizzi = 128 bit.
Il suo header è di 40 byte a lunghezza fissa (mentre IPv4 20 a lunghezza variabile) e sono rimossi dei campi:
- **Header length**: perché è ora a lunghezza fissa,
- **Checksum**: perché il controllo errori è fatto da altri livelli,
- **Bit di frammentazione**: perché frammentazione fatta solo da mittente e gestita in extension headers (pacchetto IPv6 può trasportare 0, 1 o + extension header, identificati nel campo next header).
##### Perché IPv6?
- Perché gli **IPv4 sono esauriti** (nonostante IPv4 privati, NAT e CIDR),
- Per l’**IoT**, in quanto ogni elemento IoT deve avere un **IP pubblico globalmente instradabile**.
#### Rappresentazione IPv6
Rappresentato in esadecimale, dove ogni cifra = 4 bit, quindi su 128 bit si ha una stringa di 32 cifre esadecimali.
Formato = HHHH:HHHH:HHHH:HHHH:HHHH:HHHH:HHHH:HHHH (8 hextetti).
###### Regole per ridurre n° cifre
- Gli 0 all’inizio di ogni hextetto possono essere omessi,
- Si può usare il blocco “::” per rappresentare una sequenza di hextetti.
IPv6 non usa subnet mask, ma rappresentazione **CIDR con prefisso**, dove il **prefisso** rappresenta la parte di **rete** (0-128).
<!--SR:!2024-04-30,2,200--> 

### Tipi di IPv6
Hint: unicast (global unicast, loopback, unspecified e link local), anycast, multicast (+ formato)
::
##### Unicast
Identifica 1 **singola interfaccia** a cui inviare pacchetti.
###### Global unicast
Simili agli IPv4 pubblici, sono globalmente unici e instradabili. Ce ne sono di 2 tipi:
- IPv4 embedded: indirizzi che iniziano con "000" e sono usati per la transizione da IPv4 a IPv6.
- Gli altri: indirizzi che <u>non</u> iniziano con "000" e che hanno un interface ID da 64 bit (/64).
Un global unicast si compone di:
- Global routing prefix: la porzione di rete assegnata dall'ISP (48 bit = 3 hextetti).
- Subnet ID: parte dell'indirizzo usata per il subnetting (16 bit = 1 hextetto).
- Interface ID: parte che identifica le interfacce di rete (64 bit = 4 hextetti).
###### Loopback
("::1" o "::1/128") è un indirizzo usato da un host per inviare un pacchetto a se stesso e non può essere assegnato a un'interfaccia fisica.
###### Unspecified address
("::" o "::/128") indica l'assenza di indirizzo. Non è assegnabile a interfacce e può essere solo usato da mittenti.
###### Link local
Usati per comunicare su un ***local link*** (unico per interfaccia router, non per rete), che in IPv6 è = a una subnet, infatti i pacchetti mandati sui *link local* sono ***non routable***. Ogni interfaccia deve avere un link local (ma non per forza un global unicast).
I link local sono nel range "**FE80::/10**" (anche se usato /64 per renderli *non routable*). Per configurare default gateway si usa il suo link local. Per la loro univocità in interfaccia, ogni interfaccia potrebbe aver lo stesso link local (tipo tutte FE80::1/64).
##### Anycast
Identifica un **gruppo di interfacce** e un pacchetto su questo è mandato alla più “**vicina**” in base ai ***routing protocols***.
##### Multicast
Identifica sempre un **gruppo di interfacce** ma un pacchetto su questo arriva a **tutte le interfacce che identifica** (non vanno usati come IPv6 sorgente nei pacchetti).
IPv6 <u>non ha broadcast</u> ma presenta dei multicast speciali detti ***all-node addresses*** a sostituirli come broadcast limitati (nel range "FF02::1").
###### Formato
- FF \[8 bit\] = i primi 8 bit, tutti posti a 1 (per indicare che è un indirizzo multicast: "FF00::/8").
- Flag \[4 bit\] = i seguenti 4 bit, indicano le flag (1 di questi dice se l'indirizzo è ***well-known*** o no).
- Scop \[4 bit\] = gli ultimi 4 bit, specificano l'ambito di validità del gruppo (***scope***: 1 = interface local | 2 = link local | 8 = org. local | E = global ...)
I router non devono inoltrare i pacchetti al di fuori del loro *scope*.
<!--SR:!2024-04-30,2,200-->

### NDP
::
Neighbor Discovery Protocol è un protocollo usato per risolvere un IPv6 in un MAC (analogamente ad ARP per IPv4) e questo crea (con ICMPv6) delle ***neighbor cache***, contenenti i MAC delle interfacce vicine + altre informazioni.
(foto) (IPv4 vs IPv6 table?)
<!--SR:!2024-04-30,2,200-->

### Transizione da IPv4 a IPv6
Hint: dual-stack routers, tunneling e NAT-PT
::
Non è nativamente possibile in quanto IPv6 non è retrocompatibile con IPv4. Per far comunicare IPv6 e IPv4 ci sono 3 tecniche:
##### Dual-stack routers
Sono dei router che condividono delle interfacce IPv6 e altre IPv4 usate rispettivamente per i relativi scopi (il router inoltra i pacchetti alle rispettive reti senza accorgersi di niente).
##### Tunneling
Prevede che i pacchetti IPv6 siano incapsulati in pacchetti IPv4 all'invio e deincapsulati alla ricezione, permettendogli di viaggiare attraverso reti IPv4 senza alcun problema o bisogno di aggiornare l'infrastruttura.
##### Traduzione con NAT-PT
Si traducono gli indirizzi con un dispositivo abilitato NAT-PT (*NAT - Protocol Translation*) che ricorre a un pool di IPv4 dinamicamente per mappare l'indirizzo IPv6 di un nodo su uno di questi (global unicast) quando deve comunicare con un nodo IPv4. NAT-PT mappa gli IPv6 sugli IPv4 fornendo un instradamento trasparente, proprio come NAT mappa IPv4 privati su IPv4 pubblici.
<!--SR:!2024-04-30,2,200-->

### Datagram IPv6
Hint: VTFPNHSD + extension headers
::
- ***Version*** \[4 bit\]: contiene il valore binario "0110" che indica che il pacchetto è IPv6.
- ***Traffic class*** \[8 bit\]: usato per il [[Livello trasporto#Controllo di flusso|controllo di flusso]].
- ***Flow label*** \[20 bit\]: usato come etichetta dal mittente per dire ai router come trattare i pacchetti (sperimentale, tipo per servizi *real-time*).
- ***Payload length*** \[16 bit\]: lunghezza (max) del payload IPv6.
- ***Next header*** \[8 bit\]: (= al campo ***protocol*** IPv4), indica quale protocollo di livello superiore ha creato il pacchetto e quindi anche a quale dovrà essere consegnato.
- ***Hop limit*** \[8 bit\]: (= al campo ***TTL*** IPv4), decrementato di 1 a ogni hop, quando arriva a 0 è scartato e il router manda un messaggio ICMPv6 ***time_exceeded*** all'origine.
- ***Source / destination IP address*** \[16 byte\]: IPv6 origine e destinazione di 128 bit ognuno.
Un datagram IPv6 può avere degli ***extension headers***, eventualmente posti tra header IPv6 e payload, e sono usati per gestire la frammentazione e la sicurezza.
<!--SR:!2024-04-30,2,200-->