### Caratteristiche

Usato per app che non tollerano perdite o alterazioni nell’ordine di pacchetti ma che tollerano ritardi.

##### Connection oriented

Il TCP è un protocollo ***connection oriented*** che stabilisce una connessione permanente (detta **sessione**) tra gli host prima di trasmettere dati. Prima (e durante) la sessione, TCP:

- <u>Riceve dati</u> dall’app trasmittente,
- <u>Accumula i dati in un buffer</u> di trasmissione,
- Quando una certa quantità di dati è nel buffer, <u>vi crea un segmento e lo invia</u>.

Durante l’instaurazione della sessione (con un ***[[#3-way handshake|handshake]]***), trasmittente e destinatario stabiliscono la ***window size*** (anche diversa nelle 2 direzioni), ovvero la <u>quantità di dati inviabile in un certo periodo di tempo</u>.

##### Reliable

Essendo **affidabile**, TCP <u>garantisce che ciascun segmento inviato dal trasmittente arrivi a destinazione</u>. Nel caso in cui un segmento <u>si perda o risulti corrotto</u>, TCP <u>lo ritrasmette</u>. 

Dato che le reti presentano percorsi multipli di lunghezza diversa, i segmenti possono raggiungere la destinazione in <u>ordine diverso</u> dall'originale, perciò TCP fornisce un servizio di **numerazione** dei segmenti per poterne ricostruire la corretta sequenza.

##### Controllo del flusso

(O *flow control*), per questo TCP è in grado di accorgersi se un **destinatario** che riceve pacchetti **è sovraccaricato** e nel caso **riduce il tasso di trasmissione dei pacchetti**.

##### Controllo della congestione

(O *congestion control*), per questo TCP è in grado di accorgersi se la **rete è sovraccaricata** e nel caso **riduce il tasso di trasmissione dei pacchetti**.

##### Stateful

Il TCP è ***stateful***, ovvero tiene traccia dello stato delle sessioni, memorizzando varie info utili per implementare servizi.

##### Altro

Il TCP è **full-duplex** e **unicast** (<u>no multicast</u>).

### Segmento TCP

Il pacchetto TCP è detto segmento e ha un *overhead* di 20 byte (opzioni di solito non c’è); i campi sono:

- ***Source port*** (16 bit) e ***Destination port*** (16 bit): usati per <u>identificare l’app</u> e realizzare le attività di *multiplexing* e *demultiplexing* del livello trasporto.
- ***Sequence number*** (32 bit): usato per <u>riordinare i segmenti</u> di una trasmissione.
- ***Acknowledgement number*** (32 bit): indica il dato che viene riscontrato.
- ***Data offset*** (4 bit): è la <u>lunghezza dell’header</u> (bit di offset prima del payload/dati, se > 5 ci sono opzioni).
- ***Reserved*** (3 bit): bit riservati.
- ***Control bits*** (9 bit): <u>flags</u> usate da TCP per diversi scopi, tra cui:
	- **SYN**, **ACK** e **FIN**: usati per <u>gestire la connessione</u> (*[[#3-way handshake]]*).
	- **RST**: *reset*, usato per <u>resettare una connessione in caso di errore</u> o *timeout*.
	- **URG**: a 1 indica che il <u>campo urgent pointer è valido</u>.
	- **PSH**: usato in app soggette a <u>ritardi</u> (*real-time*) per la <u>bufferizzazione</u> dei dati presso sia TCP trasmittente sia TCP ricevente, chiede di inviare i dati nel buffer all’applicazione ricevente.
- ***Window size*** (16 bit): apertura della finestra di ricezione, indica il <u>n° max di byte trasmissibili prima di 1 ACK positivo</u>.
- ***Checksum*** (16 bit): <u>campo di controllo errori</u> di *header*, *payload* e alcuni campi IP (IP sorgente, IP destinazione, n° protocollo…).
- ***Urgent pointer*** (16 bit): individua l’<u>ultimo byte di dati urgenti nel payload</u>.
- ***Options*** (0-320 bit, in unità di 32 bit): con:
	- Negoziazione opzionale di MSS (default 536 byte, max 65535 byte): tipo opzione 2 (con SYN impostato).
	- Negoziazione Window scale: tipo opzione 3 (con SYN impostato).
	- Selective acknowledgement (SACK invece di go-back-N) possibile: tipo opzione 4 (con SYN impostato).
	- Selective acknowledgement (SACK), in opzioni ci sono i blocchi di dati riconosciuti (anche non contigui) riconosciuti: tipo opzione 5 (con SYN impostato).

### Connessione

##### 3-way handshake

Una connessione TCP è stabilita quando un client contatta un server e richiede 3 step:

1) Il TCP client invia al TCP server un segmento **SYN** che non ha dati ma ha: 

   - **SYN a 1**,

   - ***sequence number* casuale** (*numSeqClient*).

2) Dopo aver ricevuto il segmento SYN, il TCP server alloca i buffer per ricezione/invio e le altre variabili TCP per la connessione. Poi riscontra il SYN precedente con un segmento **SYNACK** che non ha dati ma ha:

   - **SYN e ACK a 1**,

   - ***acknowledgement number*** = *numSeqClient* + 1,

   - ***sequence number* casuale** (*numSeqServer*).

3) Dopo aver ricevuto il segmento SYNACK, il TCP client alloca i buffer per ricezione/invio e le altre variabili TCP per la connessione. Poi crea un segmento **ACK** che non ha dati ma ha:

   - **SYN a 0, ACK a 1**,

   - **acknowledgement number** = *numSeqServer* + 1,

   - ***sequence number*** = *numSeqClient* + 1.

###### Quindi

Il *3-way handshake* permette di:

- Dire se il <u>destinatario è presente in rete</u>,
- Dire se sul destinatario c’è un <u>server che accetta richieste</u> client,
- Dire al destinatario che un <u>client vuole comunicare su un n° di porta</u>,
- <u>Stabilire parametri di sessione</u> (*sequence numbers* iniziali, *window size*…).

##### Terminazione

La **terminazione** di una connessione <u>può essere iniziata sia da client sia da server</u>.

Per chiuderla è usato il **flag FIN** e dato che la connessione è **full-duplex**, la terminazione deve avvenire in <u>entrambe le direzioni</u> (non per forza insieme). 

Ogni **pacchetto FIN** (o *shutdown*) va riscontrato con un **ACK**; perciò, per chiudere una connessione, servono **4 pacchetti** (<u>2 coppie di FIN+ACK in entrambe le direzioni</u>).

Al termine, client e server TCP <u>deallocano le risorse</u> (buffer e variabili) usate.

#### Attacchi SYN flood

I ***SYN flood attacks*** sono degli attacchi alla rete che sfruttano le vulnerabilità del **3-way handshake**. In questi sono mandati tanti **SYN** all’obiettivo <u>senza poi fare il 3° passo (ACK)</u>. 

Quindi, poiché per ogni SYN ricevuto il server <u>alloca buffer e variabili</u> per rispondere col **SYNACK**, il server potrebbe <u>esaurire le sue risorse e non riuscire a gestire le connessioni legittime</u> (attacco **DoS**, *Denial of Service*).

### Servizio affidabile

##### Sequence number

Il ***sequence number*** di un segmento è il <u>n° del 1° byte del segmento rispetto al flusso di byte trasmesso</u> (con segmenti da 1000 byte: il 1° = "1", il 2° = "1001", il 3° = "2001"...). Dato che il TCP vede i dati solo come un flusso di byte ordinati, i *sequence number* contano i <u>byte trasmessi</u> e non i segmenti inviati.

Ad ogni segmento, il *sequence number* è <u>incrementato del n° dei byte trasmessi</u>, perciò:

- Ogni segmento è <u>identificabile e riscontrabile senza ambiguità</u>,
- I segmenti sono <u>riordinabili</u> (se arrivano in ordine diverso),
- Si possono <u>rilevare le perdite</u>.

###### Prevenzione di attacchi

Per prevenire certi ***malicious attacks***, durante il *3-way handshake* è stabilito un <u>valore casuale</u> da cui partire per contare i byte, che sarà il ***sequence number* iniziale** (quindi non per forza 1).

##### Acknowledgement number

L’***acknowledgement number*** invece è il <u>n° del prossimo byte che ci si aspetta di ricevere</u> (si riferisce sempre al flusso di byte).

Se un host che riceve un segmento (tipo con byte da 1 a 1000) deve inoltrare un <u>ACK</u> al trasmittente tramite un segmento con <u>acknowledgement number aumentato di 1</u> (1001, che sarà) perché quello è il <u>n° del prossimo byte aspettato</u> (tenendo anche qui conto del valore casuale stabilito all’inizio, non per forza 1001).

###### Perdite

Per le **perdite** si può usare sia ***[[2 Trasferimento affidabile#Go-back-N|go-back-N]]*** sia ***[[2 Trasferimento affidabile#Selective repeat|selective repeat]]***; ma alcuni usano **SACK** (*selective acknowledgement*). 

Essendo ***full-duplex***, TCP può usare il ***piggybacking*** per riscontrare segmenti ricevuti (di solito 1 ACK per segmento ricevuto).

