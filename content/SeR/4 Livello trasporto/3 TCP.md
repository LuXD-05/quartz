### Caratteristiche

Usato per app che non tollerano perdite o alterazioni nell’ordine di pacchetti ma che tollerano ritardi.

##### Connection oriented

Il TCP è un protocollo ***connection oriented*** che stabilisce una connessione permanente (detta **sessione**) tra gli host prima di trasmettere dati. Prima di stabilire la sessione, TCP:

- Riceve dati dall’applicazione trasmittente,
- Accumula i dati in un buffer di trasmissione,
- Periodicamente (o in presenza di particolari condizioni) crea un segmento con parte dei dati nel buffer. Il protocollo attende fino a quando la giusta quantità di dati è nel buffer in quanto **dimensione** del segmento è importante per le **prestazioni**.

Durante l’instaurazione della sessione (***handshake***), trasmittente e destinatario stabiliscono la ***window size*** (anche diversa nelle 2 direzioni), ovvero la **quantità di dati** che può essere **inviata in un** certo **periodo di tempo**.

##### Reliable

Essendo **affidabile**, TCP garantisce che ciascun segmento inviato dal trasmittente arrivi a destinazione. Nel caso in cui un segmento si perda o risulti corrotto, TCP lo **ritrasmette**. Dato che le reti presentano percorsi multipli di lunghezza diversa, i segmenti possono raggiungere la destinazione in **ordine diverso** da come sono trasmessi, perciò TCP fornisce un servizio di **numerazione** dei segmenti per poterne ricostruire la corretta sequenza.

##### Controllo del flusso

(O *flow control*), per questo TCP è in grado di accorgersi se un **destinatario** che riceve pacchetti **è sovraccaricato** e nel caso **riduce il tasso di trasmissione dei pacchetti** (previene la necessità di ritrasmissione di segmenti persi per ***buffer overflow***).

##### Controllo della congestione

(O *congestion control*), per questo TCP è in grado di accorgersi se la **rete è sovraccaricata** e nel caso **riduce il tasso di trasmissione dei pacchetti**.

##### Stateful

Il TCP è ***stateful***, ovvero tiene traccia di stato delle sessioni, memorizzando varie info utili per implementare servizi.

##### Altro

Il TCP è **full-duplex** e **unicast tra trasmittente e ricevente** (multicast non permesso).

### Segmento TCP

Il pacchetto TCP è detto segmento e ha un *overhead* di 20 byte (opzioni di solito non c’è); i campi sono:

- ***Source port*** (16 bit) e ***Destination port*** (16 bit), usati per **identificare l’applicazione** e realizzare le attività di **multiplexing** e **demultiplexing** del livello trasporto.
- ***Sequence number*** (32 bit), usato per **riordina**re i **segmenti** di una trasmissione.
- ***Acknowledgement number*** (32 bit), o **n° di riscontro**, indica il dato che viene riscontrato.
- ***Data offset*** (4 bit), è la **lunghezza dell’header** (bit di offset prima del payload/dati, se > 5 ci sono opzioni).
- ***Reserved*** (3 bit), bit riservati.
- ***Control bits*** (9 bit), **flags** usate da TCP per diversi scopi, tra cui:
	- **SYN**, **ACK** e **FIN**, usati per gestire la connessione (***3-way handshake***).
	- **RST**, *reset*, usato per resettare una connessione in caso di errore o *timeout*.
	- **URG**, a **1** indica che il campo ***Urgent pointer*** è valido.
	- **PSH**, usato in app soggette a **ritardi** (***real-time***) per la bufferizzazione dei dati presso sia TCP trasmittente sia TCP ricevente, chiede di inviare i dati nel buffer all’applicazione ricevente.
- ***Window size*** (16 bit), apertura della **finestra di ricezione**, indica il **n° max di byte trasmissibili prima di 1 ACK positivo**.
- ***Checksum*** (16 bit), campo di controllo con errori di ***header***, ***payload*** e alcuni **campi IP** (IP sorg, IP dest, n° protocollo…).
- ***Urgent pointer*** (16 bit), individua **l’ultimo byte di dati urgenti** nel payload.
- ***Options*** (0-320 bit, in unità di 32 bit), con:
	- Negoziazione opzionale di MSS (default 536 byte, max 65535 byte): tipo opzione 2 (con SYN impostato).
	- Negoziazione Window scale: tipo opzione 3 (con SYN impostato).
	- Selective acknowledgement (SACK invece di go-back-N) possibile: tipo opzione 4 (con SYN impostato).
	- Selective acknowledgement (SACK), in opzioni ci sono i blocchi di dati riconosciuti (anche non contigui) riconosciuti: tipo opzione 5 (con SYN impostato).

### Connessione

##### 3-way handshake

Una connessione TCP è stabilita quando un client inizia a comunicare con un server e richiede 3 step:

1) Il TCP **client invia** al TCP **server** un segmento **SYN** che non ha dati ma **ha** il **SYN** a **1** e il suo ***sequence number*** a un valore **casuale** (*numSeqClient*).
2) **Dopo** aver **ricevuto** il segmento **SYN**, il TCP **server alloca** i **buffer** per ricezione/invio **e** le altre **variabili** TCP per la connessione. Poi **crea** un segmento **SYNACK** che non ha dati ma **ha SYN e ACK a 1**, l’***acknowledgement number*** uguale a *numSeqClient* + 1 e il suo ***sequence number*** a un valore **casuale** (*numSeqServer*).

    Ogni pacchetto TCP deve essere riscontrato, quindi **questo ACK riscontra il SYN prima ricevuto**).

3) **Dopo** aver **ricevuto** il segmento **SYNACK**, il TCP **client alloca** i **buffer** per ricezione/invio **e** le altre **variabili** TCP per la connessione. Poi **crea** un segmento **ACK** che non ha dati ma ha **SYN a 0, ACK a 1**, l’**acknowledgement number** uguale a *numSeqServer* + 1 e ***sequence number*** a *numSeqClient* + 1.

Il ***3-way handshake*** permette di:

- Dire se il **destinatario** è **presente** sulla **rete**,
- Dire se **sul destinatario** c’è **un server che accetta richiesta** del client,
- **Dire al destinatario** che **client vuole comunicare su** un **n° di porta**,
- **Stabilire parametri** di **sessione** (*sequence numbers* iniziali, *window size*…).

##### Terminazione

La **terminazione** di una connessione può essere iniziata sia da **client** sia da **server**.

Per chiuderla è usato il **flag FIN** (*finish*) e dato che la connessione è **full-duplex**, la terminazione deve avvenire in **entrambe le direzioni** (non per forza insieme). Ogni **pacchetto FIN** (o ***shutdown***) **va riscontrato con** un **ACK**; perciò, per chiudere una connessione, servono **4 pacchetti** (**2 coppie di FIN+ACK in entrambe le direzioni**).

**Al termine**, **client** e **server** TCP **deallocano** le **risorse** (buffer e variabili) usate.

#### Attacchi SYN flood

I ***SYN flood attacks*** sono degli attacchi alla rete che sfruttano le vulnerabilità dell’**handshake** del TCP. In questi si mandano **tanti SYN** all’obiettivo **senza** poi **fare** il 3° passo (**l’ACK**); e, poiché **per ogni SYN** ricevuto il **server alloca buffer** e **variabili per** rispondere col **SYNACK**, il **server** potrebbe **esaurire** le sue **risorse** e **non riuscire** a **gestire** le **connessioni** giuste/**legittime** (attacco DoS, ***Denial of Service***).

### Servizio affidabile

##### Sequence number

Il ***sequence number*** di un segmento è il **n° del 1° byte del segmento rispetto al flusso** di byte **trasmesso** (per **segmenti** da **1000 byte**: **1°** sequence number = **1**, **2°** … = **1001**, **3°** … = **2001** e così via). Dato che il TCP vede i dati solo come un flusso di byte ordinati, i *sequence number* contano i **byte** trasmessi e non i segmenti inviati.

Per prevenire certi ***malicious attacks***, il TCP, durante l’instaurazione della connessione (**3-way handshake**) stabilisce un **valore casuale** da cui partire per contare i byte, che sarà il ***sequence number* iniziale** (quindi non per forza 1).

**Quando** un **segmento** è **trasmesso**, il ***sequence number*** è **incrementato del n°** dei **byte trasmessi**. Ciò rende ogni segmento identificabile e riscontrabile senza ambiguità; ed è anche possibile rilevare i segmenti persi.

Il TCP ricevente riceve i dati, li mette nel buffer di ricezione rispettando l’ordine, li riassembla e li dà al livello applicativo.

##### Acknowledgement number

L’***acknowledgement number*** invece è il **n° del prossimo byte che ci si aspetta di ricevere** (si riferisce sempre al flusso di byte).

Se un host che riceve un segmento (con byte da 1 a 1000) deve inoltrare un ACK al trasmittente, esso incrementerà l’*acknowledgement number* di **1** (1001) perché quello è il *sequence number* del byte aspettato (tenendo anche qui conto del valore casuale stabilito all’inizio, non per forza 1001).

L’***acknowledgement number*** è **valido** solo **quando** il flag **ACK** è a **1** (di solito è a 0 solo nei segmenti SYN).

Per le **perdite** si può usare sia ***go-back-N*** sia ***selective repeat***; ma alcuni usano la ***selective acknowledgement*** (**SACK**). (Se entrambi supportano **SACK**, il destinatario può riscontrare segmenti non contigui e richiedere di ritrasmettere solo quelli persi).

Essendo ***full-duplex***, TCP può usare il ***piggybacking*** per riscontrare segmenti ricevuti (di solito 1 ACK per segmento ricevuto).

