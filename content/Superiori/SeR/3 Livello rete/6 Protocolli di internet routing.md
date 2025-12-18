### Protocolli di internet routing

I **protocolli di internet routing** servono a trovare un buon percorso tra router mittente e router destinatario e si basano sul **costo** dei link. Il <u>costo del link</u> è un fattore che è scaturito da:

- **Larghezza di banda** del link, **livello** e **prezzo del traffico**,
- **N° di hop** che separano <u>mittente</u> e <u>destinatario</u>.

##### Algoritmi di routing decentralizzato

Con questi i **router** <u>non conoscono tutti i percorsi</u> con cui un pacchetto può arrivare a <u>destinazione</u>, ma <u>conoscono i costi dei link a 1 hop di distanza</u>; quindi il <u>percorso</u> per raggiungere il destinatario è <u>calcolato gradualmente</u>. L'algoritmo è detto "*Distance-Vector Algorithm*" ed è usato da **RIP** (*Routing Information Protocol*).

##### Algoritmi di routing centralizzato (globale)

Questi <u>calcolano il percorso migliore </u>in base a una **conoscenza completa della rete** di router (ciò fatto <u>inviando e ricevendo pacchetti sullo stato dei link a/da tutti gli altri router</u>). L'algoritmo è detto "*Link-state Algorithm*", usato da **OSPF** (*Open Shortest Path First*).

### AS

I router in internet sono organizzati in **AS** (*Autonomous Systems*), i quali definiscono un <u>gruppo di router e reti IP sotto</u> il controllo di una singola <u>entità amministrativa</u>. Gli AS sono identificati da un **ASN** (*AS Number*) assegnatogli da un **RIR** (*Registro Internet Regionale*). All'**interno di un AS** i router eseguono tutti lo <u>stesso algoritmo di routing</u>. Gli algoritmi sono:

###### Intra-AS Routing Protocols

Questi sono gli <u>algoritmi di routing eseguiti all'interno dei singoli AS</u>; e sono **RIP** e **OSPF** (detti anche <u>IGP</u>, *Interior Gateway Protocols*).

###### Inter-AS Routing Protocols

Questi sono gli <u>algoritmi di routing eseguiti dai router degli AS</u> (detti **router gateway**) che instradano i pacchetti al di fuori dagli stessi e verso altri AS; e internet usa **BGP** (*Border Gateway Protocol*).

### RIP

(O *Routing Information Protocol*) è un protocollo ***distance-vector***: (periodicamente o per cambiamenti topologici) **invia l'intera tabella di routing ai router distanti 1 hop**. <u>Non conosce</u> quindi il <u>percorso verso la destinazione, ma</u> ne conosce:

- **Direzione** data dal <u>router vicino</u> (next hop),
- **Distanza**: data dal <u>n° di router da attraversare per</u> arrivare a <u>destinazione</u> (hop count; max 15, quindi usato con reti con - di 15 host).

RIP usa dei **pacchetti broadcast UDP** per lo scambio di **info di routing** (contenenti fino a 25 descrittori di route), inviati ogni **30 secondi** (processo detto ***advertising***). I router che li ricevono, <u>aggiornano una tabella di routing RIP</u> con:

- **Subnet** di **destinazione**,
- **Router adiacente** a cui inoltrare i pacchetti,
- **N° di hop alla destinazione**.

Se un router <u>non riceve notizie da un vicino per 180 secondi</u>, lo **contrassegna come irraggiungibile**, **eliminandolo dalla tabella RIP** e **diffondendo la notizia**. <u>Svantaggio</u> del RIP è la **convergenza lenta** per il fatto che i <u>router aggiornano solo i vicini</u>.

### OSPF

Protocollo ***link-state***: <u>trasferisce</u> le <u>info di routing</u> a **tutti i router della rete** (che usano l'**algoritmo di Dijkstra** per trovare il percorso migliore).

Dopo l'inizializzazione o dopo cambiamenti di routing, un **router OSPF** genera annunci detti **LSA** (*Link-State Advertisements*) con info topologiche di rete che vengono <u>scambiati tra tutti i router della rete</u> tramite ***flooding***.

Al contrario di RIP, **OSPF** è usato per <u>reti grandi</u> e ha <u>maggiore convergenza</u> (in quanto aggiorna lo stato dei collegamenti ogni 30 minuti). Inoltre consente anche l'**auth dei messaggi tra i router** (solo quelli fidati usano **OSPF**).

<u>Svantaggi</u>: necessario l'uso di ***flooding***, necessario il **riscontro dei pacchetti** inviati e **difficile** da implementare.

### BGP

(O *Border Gateway Protocol*) è un protocollo di routing dinamico che **connette router gateway di AS diversi**. Si basa su ***path-vector***: ottiene il <u>percorso migliore</u> per la destinazione dal **n° di AS da attraversare** in quanto i **router BGP confinanti** <u>si scambiano info sui percorsi invece che sui costi</u> (*BGP fra pari*).

**BGP** è un protocollo **distribuito** siccome i <u>router BGP comunicano solo con quelli adiacenti</u>. BGP funziona con **annunci sui percorsi**, mandati tra pari router BPG su connessioni punto-punto e che contengono: un <u>indirizzo di rete</u> destinazione (in CIDR) e un'insieme di <u>attributi</u> associati al percorso verso la destinazione.

### Metodi di relazione AS

##### Transit

Quando un **ISP** (detto ***transit provider***) accetta di **trasportare** il **traffico** tra un altro **ISP** e gli **altri *transit providers*** e viene pagato in base ai **BPS** (bit per second).

##### Peering

<u>2 AS di 2 ISP diversi si accordano per far transitare il traffico l'uno dall'altro</u> (gratis o con costi <). La connessione è:

- **Diretta**: con coppie di router collegate direttamente con link multipli a 10/100 Gb; questo è detto ***Private Peering*** o **PNI** (*Private Network Interconnection*).
- **Indiretta**: con **IX** (*Internet Exchange Switches*) che collegano molti router tramite insiemi di switch ethernet.

