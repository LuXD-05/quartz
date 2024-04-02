---
public: true
edited_seconds: 14530
modified_at: 30/03/2024 22:02:22
---
# Livello Rete
Il livello rete esegue una consegna **host-to-host** dei pacchetti. Tra gli host ci possono essere 1 o + reti (IPv4 o IPv6).
### Fondamenti
##### Addressing
Gli host sono configurati con un **indirizzo univoco** (**IP**) per identificarli in rete (unico anche nelle inter-reti).
##### Encapsulation
Il livello rete **incapsula i dati da inviare** in **pacchetti** a cui è aggiunto un **header** con **IP mittente e destinatario**.
##### Routing
Il livello rete **dirige i pacchetti a destinazione**. Il **destinatario** può essere:
- Il **mittente stesso** (*loopback*),
- Un **host locale** (sulla stessa rete del mittente),
- Un **host remoto** (su una rete diversa (remota) da quella del mittente). Qui i pacchetti sono inviati a un **router** che sceglie il percorso migliore per arrivare a destinazione.
##### De-encapsulation
Quando il pacchetto arriva al **livello rete** del **destinatario**, questo controlla l’**header IP** del pacchetto; e se l’IP di destinazione corrisponde col suo, l’header è rimosso e il pacchetto è deincapsulato a **PDU 4** e passato a livello **trasporto**. 
### Modelli di rete
##### A circuito virtuale
(Detto anche ATM, *Asynchronous Transfer Mode*), è un modello **orientato alla connessione** dove, prima di comunicare, tra i nodi va setuppato un **circuito virtuale** che verrà utilizzato durante la comunicazione. Può essere:
- **Permanente**, tipo connessioni preconfigurate e dedicate,
- **Temporaneo**, basato su servizi “*a chiamata*” e scartato al termine dello scambio dei dati.
##### A datagram
Qui i pacchetti sono immessi in rete senza handshake e raggiungono il destinatario con un IP destinazione. È:
- ***Connectionless***: nessuna connessione è stabilita prima di inviare un pacchetto, 
- ***Best-effort***: protocollo IP è <u>inaffidabile</u> perché non è garantita la consegna del pacchetto,
- ***Media independent***: indipendente dal mezzo su cui viaggia. Pacchetto è portato in frame diversi in base al link.
#### MTU e Frammentazione
L'**MTU** (*Maximum Transmission Unit*) è la dimensione max per i pacchetti trasportabili su ciascun link. È imposto dal livello **datalink** e se i frame che arrivano a un router sono **> dell’MTU** del link successivo, il router li **frammenterà** in dimensioni adatte. Il processo di frammentazione però causa **latenza**.
### Router
##### Porte di ingresso
Hanno una coda detta **buffer di ingresso** dove i segnali prelevati dal link sono prima **decodificati in binario**, e poi **organizzati in frames**. Dei frame integri (con *FCS* ok) e diretti al router ne viene estratto il payload. 
##### Switching fabric
**Connette** fisicamente le porte di **ingresso** a quelle di **uscita**.
##### Porte di uscita
**Memorizzano e trasmettono i frame** ottenuti dalla *switching fabric*. Per farlo il buffer datalink di uscita esegue il **framing**, ovvero crea frame giusto per il link e inserisce il datagram IP livello 3 in esso.
##### Routing processor
Fa **algoritmi di routing** e sceglie il percorso dei pacchetti aggiornando le corrispondenze della ***routing table***, di 2 tipi:
- **Rotte statiche**: fisse, create da amministratori di rete.
- **Rotte dinamiche**: dinamiche, gestite in base ai cambiamenti di rete con dei ***routing protocols***.
### Datagram IPv4
Composto da: 
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
### Indirizzi IP e IPv4
##### IP (Internet Protocol)
1) Identifica un host in una rete,
2) Fornisce il path per raggiungere gli host,
3) Rende possibile la comunicazione tra host.
##### IPv4
4 byte $\;\rightarrow\;$ ogni byte convertito in decimale $\;\rightarrow\;$ forma ***dotted decimal*** $\;\rightarrow\;$ 32 bit in 4 gruppi di 8 (Es: "192.168.0.1"). IPv4 è composto da:
- **Net ID**: parte che identifica la **rete** (per instradamento a livello **subnet**)
- **Host ID**: parte che identifica gli **host** (per instradamento a livello **host**).
#### Politiche di distribuzione IPv4
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
#### Indirizzo di rete
Serve per saper ese spedire pacchetti localmente o a gateway verso internet e a quale rete appartiene esso.
- Destinazione **locale**: pacchetto inviato sul link.
- Destinazione **remota**: pacchetto inviato a dispositivo livello 3 (router).
Cambia quindi il **MAC del frame datalink**: per dest locale = MAC destinatario e per remota = MAC gateway.
L'indirizzo di rete si ottiene facendo un **AND** tra i bit di un **IPv4** e la sua **subnet mask**.
### Assegnazione indirizzi a NIC
Gli IP sono assegnati alle **NIC** (*Network Interface Card*) dei dispositivi, e l’assegnazione può essere:
- **Statica**: per stampanti/server/dispositivi accessi per mezzo di un **IP fisso** (**rischio**: conflitti),
- **Dinamica**: Con il [[Livello rete#DHCP|DHCP]], per dispositivi locali che cambiano spesso. DHCP controlla gli IP della rete dando agli host quelli non statici e non crea conflitti.
### Indirizzamento
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
### Tipi di IP
##### Pubblici
Instradati a **livello globale** tra i router degli **ISP** e permettono di <u>identificare e raggiungere un host globalmente</u>. I dispositivi in una LAN usano tutti lo **stesso IP pubblico** (dato al **gateway**).
##### Privati
Usati per assegnare IPv4 a **livello locale**, rendono accessibili gli host in una LAN e <u>non sono visibili dall’esterno</u>. Al fine di far comunicare quindi un host di una rete privata con un host in internet è necessario il **NAT**.
### NAT
Il NAT (*Network Address Translation*) è una tecnica che consente di **mappare + IP privati su un IP pubblico**, permettendo quindi a + host di una rete privata di comunicare con l'esterno.
##### Perché?
- **Risparmio degli indirizzi IP**: gli ISP non devono più dare tanti IP tutti pubblici per gli host di una rete privata.
- **Facilità di amministrazione della rete**:
	- Gli IP privati sono modificabili liberamente senza dover notificare niente a nessuno.
	- Si può cambiare ISP senza dover cambiare la configurazione di IP privati.
- **Sicurezza**: gli host della LAN non sono visibili dall'esterno ma sono indirizzabili (dall'esterno).
### Funzioni del router NAT
Un router abilitato NAT:
- Sostituisce in ogni datagram uscente la coppia \[IPv4 sorgente (privato) : porta\] con \[IPv4 pubblico : nuova porta (generata da NAT)\],
- Registra nella **NAT Table** la corrispondenza tra le coppie.
Questo permette a NAT di gestire + richieste contemporaneamente da applicazioni **sullo stesso host** (<u>stesso IP ma porte diverse</u>) o su **host diversi** (<u>stessa porta ma IP diverso</u>).
##### Port forwarding
Per connettersi invece **dall'esterno alla LAN**, non è chiaro a quale host connettersi. Si potrebbero usare rotte **statiche** che inoltrano tutti i pacchetti a un host, ma è una soluzione poco pratica. 
Per questo si usa il ***port forwarding***, che permette a NAT di inoltrare i pacchetti a diversi host in LAN in base a **protocollo** e **porta** usati. Con le porte quindi, varie applicazioni da vari host possono comunicare distintamente con l'esterno. La coppia \[**IPv4:port**\] è detta **socket**.
### NAT Traversal
L’associazione di NAT (\[IPv4 sorgente : porta\] = \[IPv4 pubblico : nuova porta\]) è fatta sui pacchetti **in uscita** dalla LAN (quindi i **pacchetti in entrata** possono essere **accettati solo dopo quelli in uscita, in risposta ad essi**).
Quindi un utente in LAN con un NAT può connettersi a un server remoto, ma un utente remoto non può connettersi al server della LAN. Per ovviare a questo si usa il **NAT Traversal**.
##### UPnP e P2P
La tecnica di NAT Traversal + diffusa è **UPnP** (*Universal Plug & Play*, spesso usata da app P2P). Questa permette automaticamente a un **host LAN** (o a un'**app** su un host) di **richiedere**, **per una** qualsiasi **porta**, una **corrispondenza statica NAT** per un certo ***lease time*** tra l'app LAN e l'host/app remota. Se UPnP accetta, inserisce la corrispondenza nella sua tabella di traduzione e i 2 host possono istanziare connessioni TCP l'uno verso l'altro.
### DHCP
Il **DHCP** (*Dynamic Host Configuration Protocol*) assegna automaticamente gli IP agli host di una LAN, senza interventi umani necessari e senza creare conflitti. Esso, oltre all'IP, fornisce anche delle informazioni aggiuntive:
- **Subnet mask**,
- **IP** del **default gateway**,
- **IP** del **DNS server locale**,
- Un ***lease time*** (di connessione quando il DHCP sta comunicando con un nuovo host nella LAN per assegnargli un IP).
Il DHCP è un **protocollo client/server** ed è detto ***plug-&-play*** o ***0-conf*** in quanto automatizza la configurazione degli host in LAN.
##### Funzionamento
Di base ogni host deve essere fornito di un **DHCP client** (altrimenti non funziona).
1) Quando un host si collega alla rete, cerca il **DHCP server** mandando (col DHCP client) un **DHCP DISCOVER** in UDP e porta 67 dall'IP "0.0.0.0" a "255.255.255.255" (broadcast limitato).
2) Il DHCP server (o anche + di 1) risponde con una **DHCP OFFER** (con IP destinazione sempre il broadcast limitato), che contiene: IP offerto, subnet mask, IP del default gateway, IP del DNS server locale e *lease time*.
3) Il DHCP client (eventualmente sceglie 1 DHCP server e) risponde con una **DHCP REQUEST** (con gli stessi parametri precedenti per accettarli).
4) Il DHCP server conferma quindi i parametri con un **DHCP ACK**, chiudendo la conversazione.
Il DHCP può dare lo stesso IP sempre allo stesso host. Viene dato il *lease time* perché la validità della connessione è limitata nel tempo (ma è rinnovabile).
#### DHCP Relay Agent
Il DHCP Relay Agent sostituisce il DHCP server in una rete assegnando gli IP agli host della stessa comunicando con un DHCP server di un'altra rete.
(foto)
### ICMP
L'**ICMP** (*Internet Control Message Protocol*) è un protocollo che funge da **supporto** ad **IP** in quanto **segnala errori o scambia informazioni**; ma **non esegue correzioni** ai messaggi, perciò **non rende affidabile IP**. Esistono **ICMPv4** e **ICMPv6**.
##### Header ICMP
I messaggi ICMP sono incapsulati e inviati come pacchetti IP. Il loro header conta 8 byte di dati, che sono:
- **Tipo**: indica la **categoria** del messaggio ICMP.
- **Codice**: da un'ulteriore **descrizione** al messaggio (Esempio: tipo 3 indica destinazione non raggiungibile e i codici specificano: 0 = rete destinazione | 1 = host destinazione | 3 = porta destinazione ...).
- **Checksum**: verifica l'**integrità** dei dati.
###### Messaggi di errore
- ***Destination_Unreachable***: indica che la destinazione non è raggiungibile (per vari problemi: l'host è spento / l'host rifiuta i pacchetti per errori coi protocolli / il <u>pacchetto deve essere frammentato ma il flag DF = 1</u> ...).
- ***Redirect***: quando un gateway intermedio si accorge che il prossimo gateway è già nella stessa subnet del mittente (segnala una via + breve).
- ***Time_Exceeded***: indica che il TTL del pacchetto è stato decrementato a 0, per cui non può + essere inoltrato.
###### Messaggi di informazione
- ***Echo_Request***: il mittente chiede al destinatario di reinviare indietro lo stesso pacchetto.
- ***Echo_Reply***: la destinazione che ha ricevuto l'*echo request* rimanda indietro il pacchetto ricevuto.
- ***Timestamp*** e ***Timestamp_Reply***: (funzionano come i precedenti e) sono usati per sincronizzare i clock di 2 dispositivi.
### Ping
Il **ping** è un comando che invia **4 pacchetti ICMP** a un host per verificarne la raggiungibilità in rete e fa uso di *echo request* ed *echo reply*. Funzionamento:
1) **HostA** fa **ping** con **argomento HostB**,
2) Il programma manda una ***echo request*** al secondo da HostA a HostB,
3) Se HostB riceve le *echo request*, risponderà con ***echo reply*** (se HostA non riceve le *echo reply* entro un certo ***timeout***, verrà visualizzato un messaggio di richiesta scaduta).
##### Usi di ping
###### Loopback
Un ping a 127.0.0.1 (IPv4) o ::1 (IPv6) che ottiene risposta, indica che TCP/IP è installato e funzionante.
###### Ping locale
Pingando un altro host locale o il default gateway, un riscontro positivo indica che la rete + entrambi i dispositivi funzionano.
###### Ping remoto
Pingando un host remoto vi verifica, oltre la comunicazione locale, anche l'operatività del default gateway e degli altri router lungo il percorso.
### Traceroute
Genera l'**elenco dei router** attraversati **per** raggiungere un **destinatario** e usa il campo **TTL** / **Hop Limit** + il messaggio ***Time_Exceeded*** ICMP.
##### Funzionamento
Delle ***echo request*** sono inviate in successione **incrementando ogni volta il TTL** / Hop Limit, cosicché i pacchetti **scadano ad ogni router** ritornando varie informazioni al mittente, fino a raggiungere la **destinazione** finale che rimanda una *echo reply*.
Con **Traceroute** si ottiene l'RTT o ***Round-Trip Time***, ovvero il tempo necessario ad un pacchetto per raggiungere la destinazione e tornare indietro.
Quando l'*echo reply* non torna entro un certo **tempo limite**, il traceroute scrive "**\***" in console per indicare che il router è **sottodimensionato/sovraccaricato**. Con questo traceroute può trovare link problematici lungo i percorsi.
### Protocolli di internet routing
I protocolli di internet routing servono a trovare un buon percorso tra router mittente e router destinatario e si basano sul **costo** dei link. Il costo del link è un fattore che è scaturito da:
- Larghezza di banda del link, livello e prezzo del traffico,
- N° di hop che separano mittente e destinatario.
##### Algoritmi di routing decentralizzato
Con questi i router non conoscono tutti i percorsi con cui un pacchetto può arrivare a destinazione, ma conoscono i costi dei link a 1 hop di distanza; quindi il percorso per raggiungere il destinatario è calcolato gradualmente. L'algoritmo è detto "*Distance-Vector Algorithm*" ed è usato da RIP (*Routing Information Protocol*).
##### Algoritmi di routing centralizzato (globale) 
Questi calcolano il percorso migliore in base a una conoscenza completa della rete di router (ciò fatto inviando e ricevendo pacchetti sullo stato dei link a/da tutti gli altri router). L'algoritmo è detto "*Link-state Algorithm*", usato da OSPF (*Open Shortest Path First*).
### AS
I router in internet sono organizzati in AS (*Autonomous Systems*), i quali definiscono un gruppo di router e reti IP sotto il controllo di una singola entità amministrativa. Gli AS sono identificati da un ASN (*AS Number*) assegnatogli da un RIR (*Registro Internet Regionale*). All'interno di un AS i router eseguono tutti lo stesso algoritmo di routing. Gli algoritmi sono:
###### Intra-AS Routing Protocols
Questi sono gli algoritmi di routing eseguiti all'interno dei singoli AS; e sono RIP e OSPF (detti anche IGP, *Interior Gateway Protocols*).
###### Inter-AS Routing Protocols
Questi sono gli algoritmi di routing eseguiti dai router degli AS (detti **router gateway**) che instradano i pacchetti al di fuori dagli stessi e verso altri AS; e internet usa BGP (*Border Gateway Protocol*).
### RIP
Protocollo ***distance-vector***: (periodicamente o se ci sono cambiamenti topologici) invia l'intera tabella di routing ai router distanti 1 hop. Non conosce quindi il percorso verso la destinazione, ma ne conosce:
- Direzione data dal router vicino (next hop),
- Distanza: data dal n° di router da attraversare per arrivare a destinazione (hop count; max 15, quindi usato con reti con - di 15 host).
RIP usa dei pacchetti broadcast UDP per lo scambio di info di routing (contenenti fino a 25 descrittori di route), inviati ogni 30 secondi (processo detto ***advertising***). I router che li ricevono, aggiornano una tabella di routing RIP con:
- Subnet di destinazione,
- Router adiacente a cui inoltrare i pacchetti,
- N° di hop alla destinazione.
Se un router non riceve notizie da un vicino per 180 secondi, lo contrassegna come irraggiungibile, eliminandolo dalla tabella RIP e diffondendo la notizia. Svantaggio del RIP è la convergenza lenta per il fatto che i router aggiornano solo i vicini.
### OSPF
Protocollo ***link-state***: trasferisce le info di routing a tutti i router della rete (che usano l'algoritmo di Dijkstra per trovare il percorso migliore). 
Dopo l'inizializzazione o dopo cambiamenti di routing, un router OSPF genera annunci detti LSA (*Link-State Advertisements*) con info topologiche di rete che vengono scambiati tra tutti i router della rete tramite ***flooding***.
Al contrario di RIP, OSPF è usato per reti grandi e ha maggiore convergenza (in quanto aggiorna lo stato dei collegamenti ogni 30 minuti). Inoltre consente anche l'auth dei messaggi tra i router (solo quelli fidati usano OSPF).
Svantaggi: necessario l'uso di flooding, necessario il riscontro dei pacchetti inviati e difficile da implementare.
### BGP
**Border Gateway Protocol** è un protocollo di routing dinamico che connette router gateway di AS diversi. Si basa su ***path-vector***: ottiene il percorso migliore per la destinazione dal n° di AS da attraversare in quanto i router BGP confinanti si scambiano informazioni sui percorsi invece che sui costi (BGP fra pari).
BGP è un protocollo distribuito siccome i router BGP comunicano solo con quelli adiacenti. BGP funziona con annunci sui percorsi, mandati tra pari router BPG su connessioni punto-punto e che contengono: un indirizzo di rete destinazione (in CIDR) e un'insieme di attributi associati al percorso verso la destinazione.
### Metodi di relazione AS
##### Transit
Quando un **ISP** (detto ***transit provider***) accetta di **trasportare** il **traffico** tra un altro **ISP** e gli **altri *transit providers*** e viene pagato in base ai **BPS** (bit per second).
##### Peering
2 AS di 2 ISP diversi si accordano per far transitare il traffico l'uno dall'altro (gratis o con costi <). La connessione è:
- **Diretta**: con coppie di router collegate direttamente con link multipli a 10/100 Gb; questo è detto ***Private Peering*** o **PNI** (*Private Network Interconnection*).
- **Indiretta**: con **IX** (*Internet Exchange Switches*) che collegano molti router tramite insiemi di switch ethernet.
### IPv6
È il successore di IPv4 e come esso è best-effort, connectionless e media independent. Spazio di indirizzi = 128 bit.
Il suo header è di 40 byte a lunghezza fissa (mentre IPv4 20 a lunghezza variabile) e sono rimossi dei campi:
- **Header length**: perché è ora a lunghezza fissa,
- **Checksum**: perché il controllo errori è fatto da altri livelli,
- **Bit di frammentazione**: perché frammentazione fatta solo da mittente e gestita in extension headers (pacchetto IPv6 può trasportare 0, 1 o + extension header, identificati nel campo next header).
##### Perché IPv6?
- Perché gli **IPv4 sono esauriti** (nonostante IPv4 privati, NAT e CIDR),
- Per l’**IoT**, in quanto ogni elemento IoT deve avere un **IP pubblico globalmente instradabile**.
### Rappresentazione IPv6
Rappresentato in esadecimale, dove ogni cifra = 4 bit, quindi su 128 bit si ha una stringa di 32 cifre esadecimali.
Formato = HHHH:HHHH:HHHH:HHHH:HHHH:HHHH:HHHH:HHHH (8 hextetti).
###### Regole per ridurre n° cifre
- Gli 0 all’inizio di ogni hextetto possono essere omessi,
- Si può usare il blocco “::” per rappresentare una sequenza di hextetti.
IPv6 non usa subnet mask, ma rappresentazione **CIDR con prefisso**, dove il **prefisso** rappresenta la parte di **rete** (0-128). 
### Tipi di IPv6
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
### NDP
Neighbor Discovery Protocol è un protocollo usato per risolvere un IPv6 in un MAC (analogamente ad ARP per IPv4) e questo crea (con ICMPv6) delle ***neighbor cache***, contenenti i MAC delle interfacce vicine + altre informazioni.
(IPv4 vs IPv6 table?)
### Transizione da IPv4 a IPv6
Non è nativamente possibile in quanto IPv6 non è retrocompatibile con IPv4. Per far comunicare IPv6 e IPv4 ci sono 3 tecniche:
##### Dual-stack routers
Sono dei router che condividono delle interfacce IPv6 e altre IPv4 usate rispettivamente per i relativi scopi (il router inoltra i pacchetti alle rispettive reti senza accorgersi di niente).
##### Tunneling
Prevede che i pacchetti IPv6 siano incapsulati in pacchetti IPv4 all'invio e deincapsulati alla ricezione, permettendogli di viaggiare attraverso reti IPv4 senza alcun problema o bisogno di aggiornare l'infrastruttura.
##### Traduzione con NAT-PT
Si traducono gli indirizzi con un dispositivo abilitato NAT-PT (*NAT - Protocol Translation*) che ricorre a un pool di IPv4 dinamicamente per mappare l'indirizzo IPv6 di un nodo su uno di questi (global unicast) quando deve comunicare con un nodo IPv4. NAT-PT mappa gli IPv6 sugli IPv4 fornendo un instradamento trasparente, proprio come NAT mappa IPv4 privati su IPv4 pubblici.
### Datagram IPv6
- ***Version*** \[4 bit\]: contiene il valore binario "0110" che indica che il pacchetto è IPv6.
- ***Traffic class*** \[8 bit\]: usato per il [[Livello trasporto#Controllo di flusso|controllo di flusso]].
- ***Flow label*** \[20 bit\]: usato come etichetta dal mittente per dire ai router come trattare i pacchetti (sperimentale, tipo per servizi *real-time*).
- ***Payload length*** \[16 bit\]: lunghezza (max) del payload IPv6.
- ***Next header*** \[8 bit\]: (= al campo ***protocol*** IPv4), indica quale protocollo di livello superiore ha creato il pacchetto e quindi anche a quale dovrà essere consegnato.
- ***Hop limit*** \[8 bit\]: (= al campo ***TTL*** IPv4), decrementato di 1 a ogni hop, quando arriva a 0 è scartato e il router manda un messaggio ICMPv6 ***time_exceeded*** all'origine.
- ***Source / destination IP address*** \[16 byte\]: IPv6 origine e destinazione di 128 bit ognuno.
Un datagram IPv6 può avere degli ***extension headers***, eventualmente posti tra header IPv6 e payload, e sono usati per gestire la frammentazione e la sicurezza.
### VLAN
###### Problema
Una rete in cui sono presenti solo switch livello 2 costituisce un unico ***broadcast domain***, nel quale i pacchetti broadcast limitato ("255.255.255.255", che vengono incapsulati in frame broadcast "FF-FF-FF-FF-FF-FF") arrivano a tutte le interfacce sul link. In LAN grandi, con grandi domini broadcast, questi broadcast creano spesso traffico inutile e sovraccaricano la rete (+ comune che un host parla con un gruppo di host, non con tutti).
###### Soluzione
Per ovviare a ciò è stato definito lo standard IEEE 802.1q per gli switch 802.1q (diversi da switch di livello 3, questi non eseguono routing), che permette di suddividere una LAN in un insieme di VLAN (*Virtual LAN*). Ogni VLAN in sé costituisce un dominio di broadcast separato, quindi un broadcast mandato in una VLAN viene elaborato solo dagli host appartenenti alla stessa.
##### Definizione
> [!important] VLAN
> Una **VLAN** è una rete locale che raggruppa host **logicamente** e indipendentemente dal tipo di rete.

Le porte che collegano host a switch 802.1q sono diverse dalle porte che collegano 2 switch 802.1q (vedi [[Livello rete#Tipi di porte|Tipi di porte]]). Una singola VLAN può inoltre essere configurata su un solo switch 802.1q o su più.
### Modalità di raggruppamento VLAN
##### Per porte
Si possono associare delle VLAN a 1 o + porte (interfacce) di uno switch 802.1q.
**Problema**: questo metodo non è efficace per il fatto che è possibile cambiare manualmente la porta a cui è connesso un host e quindi cambiare la VLAN in cui è stato configurato.
##### Per indirizzi MAC
Si possono associare anche gli indirizzi MAC degli host a certe VLAN. 
**Problema**: esistono appositi programmi che permettono a un pc di modificare il proprio indirizzo MAC anche senza autorizzazione.
##### Per indirizzi IP
In questo modo è <u>come se la LAN fosse subnettata</u> e ad **ogni subnet è associata una VLAN**. Questo è il metodo + diffuso grazie alle minori criticità di sicurezza presentate.
###### Configurazione switch VLAN
La configurazione di uno switch VLAN può essere fatta in modo statico (reti piccole) o dinamico (reti grandi con tanti switch VLAN, in cui si usano software per il controllo delle VLAN tipo VTP, *VLAN Trunking Protocol*).
#### Fondamenti 802.1q
Le VLAN (secondo lo standard) sono identificate tramite un VID (*VLAN Identifier*); inoltre, le VLAN raggruppate per IP:
- Sono identificate da un VID (numero da 1 a 4096, 12 bit),
- Hanno un proprio range di indirizzi IP (con indirizzo rete e subnet mask, come le subnet),
- Vanno definite negli switch 802.1q (configurandone le interfacce assegnando ognuna a 1 sola VLAN),
- Ricevono solo il traffico trasmesso al loro interno.
### Tipi di porte
Ci sono 3 modi per configurare le porte di uno switch 802.1q:
##### Access port (untagged)
Queste porte sono configurate in modo che vi si possano collegare gli host, cosicché siano associati a una singola VLAN. I frame in uscita da una *access port* <u>non</u> hanno VLAN tag.
##### Trunk port (tagged)
A queste vi si collegano altri switch VLAN o router (per l'[[Livello rete#Routing inter-VLAN|inter-VLAN routing]]) e su esse viaggia il traffico qualsiasi VLAN. Sul ***trunk*** (cavo di collegamento ***cross*/incrociato**) viaggiano dei frame 802.1q aventi un VLAN tag (detto traffico 1Q) e il traffico delle ***native VLAN*** senza tag.
##### Native port
A queste si collegano gli switch legacy (non 802.1q) o hub, che non sanno taggare il traffico. Quando uno switch 802.1q riceve un frame *untagged*, lo invia a tutte le trunk e native ports (fino ad arrivare a vicoli ciechi, dove viene poi scartato).
Alla *native VLAN* va associato un certo VID, unico per tutti gli switch 802.1q in rete.
### Inoltro frame VLAN
Gli switch 802.1q usano delle tabelle d'inoltro (strutturate tipo: "**port | MAC | VID**") per inoltrare frame VLAN. Quando un frame ethernet arriva a uno switch VLAN viene esaminata la tabella d'inoltro e, prima di viaggiare per il *trunk*, lo switch rende il frame *tagged* inserendovi un tag con il VID della VLAN di destinazione. Arrivato allo switch VLAN di destinazione, questo gli toglierà il VLAN tag e lo invierà alla *access port* corretta.
Solo gli switch d'infrastruttura devono essere 802.1q-compatibili, al contrario di NIC degli host, hub, switch legacy...
### VLAN voce
Potrebbe essere necessario collegare anche dei telefoni VoIP a internet con cavo ethernet. Ci sono 2 modi:
- Usando 2 cavi (1 per pc e 1 per VoIP) collegati a 2 porte dello switch (poco pratico).
-  Usando lo switch a 3 porte ethernet integrato nel telefono VoIP, con 1 porta collegata allo switch di infrastruttura, 1 al telefono e l'altra al pc (migliore).
Col 2° metodo, la separazione tra il traffico del telefono da quello del pc è fatta con una ***aux VLAN***, che prevede che:
- Il link tra lo switch d'infrastruttura e quello del telefono è **trunk** (traffico ***tagged*** appartenente o al telefono o al pc),
- Il link tra lo switch del telefono e il pc è **access** (traffico ***untagged*** appartenente solo al pc).
### Routing inter-VLAN
L'***inter-VLAN routing*** (ovvero la comunicazione tra 2 VLAN) è possibile solo con un dispositivo di livello 3 (switch L3 o router) in quanto le VLAN sono reti IP diverse. Sono possibili 3 metodi per l'*inter-VLAN routing*:
##### Legacy inter-VLAN routing
Si usa un router di cui ogni interfaccia è una ***VLAN-subnet***, mentre il router stesso è il **default gateway** di ogni VLAN. Le porte che connettono il router agli switch sono **access**.
**Problema**: metodo poco usato per il n° limitato di interfacce presenti nei router.
##### Router-on-a-stick
Qui il traffico delle VALN è portato su un'unica interfaccia del router con un un **trunk**, alla quale sono connessi più switch 802.1q "in serie" (senza limiti sul n° di switch e quindi di subnet).
**Problema**: questo crea un ***bottleneck***, quindi serve un'interfaccia sufficientemente veloce.
##### Switch L3
Si collegano gli switch 802.1q da far comunicare a uno switch L3 con dei **trunk** (risolvendo il problema delle poche interfacce e del *bottleneck*). Sullo switch L3, pr ogni VLAN di cui instradare il traffico anche non direttamente collegata ad esso, vanno configurate delle SVI (*Switch Virtual Interface*), che fungono da default gateway per ogni VLAN.
#### Switch L2 vs Switch L3 vs Router

### Benefici VLAN
Le VLAN portano vari benefici:
- Separazione logica dei nodi in base al tipo di traffico (*workgroups*) e non in base alla distribuzione geografica,
- Aumento delle prestazioni per la suddivisione di un grande dominio di broadcast in parti + piccole,
- Elevata sicurezza:
	- Segmenti di rete isolati impediscono accessi senza auth,
	- Possibile l'impostazione di policy di accesso, di assegnazione IP...
	- Possibile implementazione di diverse politiche di sicurezza per ogni VLAN.
##### Esempi d'uso
Esempi d'uso contano:
- Separazione logica di aree di rete (tipo area clienti da area dipendenti),
- Costruzione di **DMZ** (*DeMilitarized Zones*)
