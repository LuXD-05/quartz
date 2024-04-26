# Trasferimento affidabile

### Affidabilità

Un protocollo è **affidabile** quando ritrasmette pacchetti alterati/persi, quindi detto **ARQ** (*Automatic Repeat reQuest*). Un protocollo ARQ garantisce l’affidabilità tramite:

1) **Rilevamento degli errori**: con un campo di controllo (checksum o CRC in base al livello del protocollo),
2) **Feedback dal ricevente**: che informa il trasmettitore sull’esito della ricezione, di 2 tipi:

   - **ACK**: ***positive** acknowledgement*,

   - **NAK**: ***negative** acknowledgement*.

3) **Ritrasmissione** dei **pacchetti** riscontrati con NAK.

### Protocollo send-and-wait

I protocolli ***send-and-wait*** o ***stop-and-wait***, prevedono che il trasmittente invii (***send***) un pacchetto e si ponga poi in attesa (***wait***) del riscontro dal ricevente (**ACK** se checksum/CRC corretti, altrimenti **NAK**).

Nel caso di perdita del pacchetto in rete (ricevente non riceve) si usa un ***countdown timer*** che parte dopo l’invio del pacchetto.

Il <u>trasmittente</u> è in attesa del **riscontro** e:

- Se questo arriva **prima** che il timer scada, il timer è resettato e si gestisce il riscontro,
- Se scade il timer e questo **non** è ancora **arrivato**, il pacchetto è ritrasmesso.

Il <u>ricevente</u>, ricevuto il pacchetto e verificato che riscontro inviare, è in attesa del **prossimo pacchetto** e:

- Se questo arriva prima che il timer scada, il timer è resettato e si gestisce il nuovo pacchetto,
- Se scade il timer e questo non è ancora arrivato, il riscontro è ritrasmesso.

In entrambe le situazioni è possibile che un pacchetto abbia invece preso un percorso lungo o lento, quindi nasce il problema della **duplicazione dei pacchetti** in rete, che si risolve con **n° di sequenza** dato a ogni pacchetto, cosi che il ricevente capisca se lo ha già ricevuto (duplicato) o no. (Nei protocolli ***send-and-wait*** il ricevente aspetta **1 pacchetto alla volta** perché il trasmittente **non può trasmettere** se prima non arriva **l’ACK** o scade il ***countdown* *timer***, quindi i pacchetti numerati solo con **0** o **1**).

### Protocolli sliding window

I protocolli ***sliding window*** prevedono di trasmettere ***N* pacchetti** (**N** = **apertura della finestra**) prima di attendere riscontri. Il momento in cui sono riscontrati gli *N* pacchetti dipende dal tipo di trasmissione, che può essere:

- **Half-duplex**: il ricevente deve aver ricevuto tutti gli *N* pacchetti prima di inviare il riscontro,
- **Full-duplex**: il ricevente può inviare riscontri senza dover attendere l’arrivo di tutti i pacchetti (se il riscontro è inserito in un **pacchetto di dati** reinviato al trasmittente, si parla di ***piggybacking***, “portare in groppa”).

Capita che alcuni degli *N* pacchetti trasmessi si **perdano** o arrivino **alterati**, per risolvere ciò ci sono 2 tecniche:

##### Go-back-N

Il ricevente, quando riceve un pacchetto errato (CRC/checksum) o fuori sequenza (qualche pack prima perso), **ignora** i pacchetti **successivi** e reinvia al trasmittente un riscontro del pacchetto ***N-1*** (sequenza di pacchetti precedente) che comporterà la ritrasmissione di tutti i pacchetti a partire dal pacchetto ***N***. Riscontrando il pacchetto *N-1* è implicito il riscontro positivo (ACK) di tutti i pacchetti precedenti (N-1, N-2…), ciò è detto ***acknowledgement cumulativo***.

##### Selective repeat

Il ricevente accetta e memorizza tutti i pacchetti ricevuti corretti (sia in sequenza sia non) poi agisce in 2 modi:

- Manda un **ACK** specifico per ogni **pacchetto** ricevuto **corretto**,
- Manda un **NAK** per i singoli **pacchetti corrotti** o **fuori sequenza**.

(Diversi modi provocano problemi tra trasmittente e ricevente; ricevente deve anche pensare al riordino pacchetti fuori sequenza).

[[Controllo di flusso e della congestione]]

[[3 TCP]]

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

### Gestione della connessione

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

### Terminazione della connessione

La **terminazione** di una connessione può essere iniziata sia da **client** sia da **server**.

Per chiuderla è usato il **flag FIN** (*finish*) e dato che la connessione è ***full*-duplex**, la terminazione deve avvenire in **entrambe le direzioni** (non per forza insieme). Ogni **pacchetto FIN** (o ***shutdown***) **va riscontrato con** un **ACK**; perciò, per chiudere una connessione, servono **4 pacchetti** (**2 coppie di FIN+ACK in entrambe le direzioni**).

**Al termine**, **client** e **server** TCP **deallocano** le **risorse** (buffer e variabili) usate.

### Attacchi SYN flood

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

Per le **perdite** si può usare sia ***go-back-N*** sia **s*elective repeat***; ma alcuni usano la ***selective acknowledgement*** (**SACK**). (Se entrambi supportano **SACK**, il destinatario può riscontrare segmenti non contigui e richiedere di ritrasmettere solo quelli persi).

Essendo ***full-duplex****,* TCP può usare il ***piggybacking*** per riscontrare segmenti ricevuti (di solito 1 ACK per segmento ricevuto).

[[4 Controllo di flusso]] 

  Ovvero la **dimensione** del **payload** del **protocollo datalink usato** (Ethernet = 1500), IPv4 = 576, IPv6 = 1280.

- **MSS** (*Maximum Segment Size*): dimensione max del payload dei segmenti TCP da inviare (in byte).

(foto)

L’**MSS** è stabilita con il **SYN** del *3-way handshake* e **non** può essere **modificata**. Il valore di default è stabilito dagli OS:

**MTU** – (***header* TCP** + ***header* IP**) = **MSS** (molti hanno 1500 – 20 – 20 = 1460 byte).

Se nel percorso vi è un **link** con **MTU < MSS**, il **pacchetto IP** è **scartato** e il router informa il mittente con un **pacchetto ICMP** (type 3, code 4) “**Need to Fragment**”, che contiene il **valore** dell’**MTU accettato** (mittente lo userà per **l’MSS**).

![](https://i.imgur.com/zDgwGbu.png)

[[5 Controllo di congestione]] 

  (Per esempio passando da collegamenti più veloci ad altri più lenti, tipo da gigabit ad ADSL, pacchetti rallentano).

Il controllo di congestione evita la perdita di pacchetti nei router per l’***overflow* dei loro buffer di ricezione o inoltro**.

### Approfondimenti

TCP impone al mittente un **limite alla frequenza di invio dei segmenti** in base al **livello** “percepito” della **congestione**, grazie al **RTT** (usato dato che è a livello rete, di router e non trasporto).

Il **throughput** (quantità di dati trasmessi nell’unità di tempo) di una comunicazione TCP è limitato da:

##### Finestra di congestione

Contiene la **qta di byte trasmissibili in 1 segmento** e cerca di non superare la capacità di rete. È **dinamica** e varia in base alla congestione della rete adattandosi ai sovraccarichi. Variabile ***cwnd***, è = al **n° di pacchetti inviabili per volta**.

##### Finestra di ricezione

Contiene la **qta di byte trasmissibili prima di** aspettare **1 ACK** e cerca di non superare la capacità del ricevitore di elaborare dati. Variabile ***rwnd***, è = al **limite max che la *cwnd* può assumere** (dimensione finestra ricezione destinatario).

### Modalità di invio pacchetti

TCP usa le variabili *cwnd* (***congestion window***) e ***ssthresh*** (***slow-start threshold***, soglia/limite) per le modalità di invio pacchetti:

##### Slow start

All’avvio la ***cwnd*** è messa a **1** MSS e ad ogni **ACK positivo** (quindi non c’è congestione e c’è banda) il suo valore è **raddoppiato** (IF *cwnd* < *ssthresh* THEN ***cwnd* $*$= 2**) fino al valore max di ***ssthresh*** (fase ***slow start***).

##### Congestion avoidance

Superato l’***ssthresh***, si passa dal raddoppiamento all’**incremento** della cwnd (IF *cwnd* >= *ssthresh* THEN ***cwnd*++**), (fase ***congestion avoidance***).

Quando TCP rileva **perdite**, considera la rete **congestionata** e cambia **modalità** (ciò per **timeout** o **3 o + ACK duplicati**).

### Rilevamento perdite

Si vede come in entrambi i casi i pacchetti spediti in 1 volta **aumentano**, di conseguenza aumenta anche il **n°** degli **ACK da riscontrare**. Quando la rete si congestiona, qualche pacchetto **si perde**; e ognuno ha il suo ***acknowledgement number***, che indica il **successivo *sequence number*** aspettato.

Quando alla destinazione arriva un pacchetto fuori sequenza, l’***acknowledgement number* rimane** quello **precedente** anche per i successivi, ad indicare che quello non è arrivato (ES: pack 6, ACK non c’è).

