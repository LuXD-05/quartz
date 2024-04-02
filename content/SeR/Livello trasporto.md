---
public: true
edited_seconds: 140
modified_at: 02/04/2024 11:16:33
---
# Fondamenti
Il livello trasporto esegue una consegna **process-to-process** perché fornisce servizi ai **processi applicativi**.
I protocolli di livello trasporto sono implementati **negli host** (non nei router).
##### Lato mittente
Il livello riceve i **messaggi** del livello applicativo e li **incapsula** in **segmenti** poi passati al livello rete (**_multiplexing_**, tanti messaggi diversi ad un unico pacchetto livello rete).
##### Lato destinatario
Il livello riceve i **segmenti** dal livello rete sottostante, fa il **checksum**, ed estrae il **messaggio** (dati) che va al processo applicativo a cui è indirizzato (**_demultiplexing_**, dal protocollo rete a + applicazioni).
Un host può avere **+ processi** (app) che comunicano in rete **simultaneamente** con altri su 1 o + host remoti; e il compito del livello trasporto è tenere traccia di queste conversazioni.
### Segmentazione
Le reti trasportano pacchetti di dimensione **limitata**, quindi i protocolli di livello trasporto li **segmentano** a dimensioni adatte. I segmenti sono incapsulati in pacchetti e gli viene aggiunto un **header** con le info necessarie a riassemblarli quando arriveranno al destinatario.
### Identificazione delle applicazioni
Il livello trasporto deve **identificare le applicazioni** a cui consegnare i pacchetti; ciò è fatto con il **n° di porta**, un **identificatore unico per ogni processo in un host**.
### Tipo di servizio
App diverse richiedono, insieme al servizio da usare, cose diverse, quindi TCP/IP prevede 2 protocolli livello trasporto:
##### UDP (_User Datagram Protocol_)
- **_Connectionless_**, quindi inaffidabile;
- **Non segmenta** i dati;
- Fa solo il **checksum** (se ok passa il payload al processo destinatario, se no lo scarta e non avvisa nessuno).
##### **TCP** (_Transmission Control Protocol_)
- **_Connection oriented_**, quindi affidabile (offre anche **controllo di flusso e di congestione**);
- **Segmenta** i dati;
- Esegue 3 operazioni base:
- Numera e tiene **traccia** dei **segmenti trasmessi** da un certo processo di un certo host,
- Esegue **_ack_** per riconoscere i dati ricevuti,
- **Ritrasmette** ogni **segmento** **non riconosciuto/valido** dopo un **_timeout_**.
### TCP o UDP?
I developer scelgono quale protocollo usare in base all’app da fare. App con db, web browser o client di posta che hanno necessità che **tutti i dati** arrivino **senza perdite, duplicazioni e in ordine**, usano **TCP**. Quelle che invece che **tollerano** **qualche perdita** ma **non ritardi nella consegna**, (telefonia, radio o tv internet) usano **UDP**.
**TCP**: vantaggio di comunicazione + robusta tra app, ma generano **_overhead_** e **ritardi in trasmissione**.
**UDP**: funzioni di base di consegna + check e overhead minimi; detto **_best-effort_** perché **inaffidabile**.
(_Streaming_ non _real-time_ tipo YT usano TCP perché trasmettono video non generato subito, quindi in caso di calo di banda l’app sospende la riproduzione lasciando tempo a TCP di ristabilire una banda adeguata)
### Numeri di porta
Nell’header del pacchetto TCP ci sono dei campi che permettono a TCP e UDP di gestire + conversazioni:
- **N° di porta sorgente** (porta associata al processo sull’host **locale**),
- **N° di porta destinazione** (porta associata al processo sull’host **remoto**).
La comunicazione è **sempre iniziata dal client** (verso il server) che **genera dinamicamente un n° di porta sorgente** **univoco** per ogni conversazione (così sono possibili + di 1 in contemporanea, tipo per mandarne + a 1 un web server).
(Porta sorgente e destinazione nel pacchetto livello trasporto poi incapsulati in IP avente IP sorgente e destinazione)
### Socket
È la combinazione tra **IP** e **n° di porta** in formato [**_IP_**]:[**_port_**] sia **sorgente** sia **destinazione**. Identifica in processo su un host. Il socket ha l’IP dell’host e la porta generata (a cazzo) mentre a destinazione la porta è specifica.
La corrispondenza tra socket sorgente e socket destinatario è detta **_socket pair_**, e discrimina una conversazione.
### Tipi di numeri di porta
Gestiti dalla IANA () e sono:
###### **Well-Known** (0 – 1023)
Riservate a app **server** cosicché i client richiedano servizi a una porta specifica nei server.
###### **Registrate** (1024 – 49151)
Sempre per app server, assegnati dalla IANA a un’entità richiedente per usi specifici.
###### **Dinamiche** (49152 – 65535)
(O _ephimeral port_) assegnati dall’OS di un host quando un client inizia una comunicazione con un server.
# Trasferimento affidabile
Un protocollo è **affidabile** quando ritrasmette pacchetti alterati/persi, quindi detto **ARQ** (**_Automatic Repeat reQuest_**). Un protocollo ARQ garantisce l’affidabilità tramite:
1) **Rilevamento degli errori**: con un campo di controllo (checksum o CRC in base al livello del protocollo),
2) **Feedback dal ricevente**: che informa il trasmettitore sull’esito della ricezione, di 2 tipi:
   - **ACK**: _**positive** acknowledgement_,
   - **NAK**: _**negative** acknowledgement_.
3) **Ritrasmissione** dei **pacchetti** riscontrati con NAK.
### Protocollo send-and-wait
I protocolli **_send-and-wait_** o **_stop-and-wait_**, prevedono che il trasmittente invii (**_send_**) un pacchetto e si ponga poi in attesa (**_wait_**) del riscontro dal ricevente (**ACK** se checksum/CRC corretti, altrimenti **NAK**).
Nel caso di perdita del pacchetto in rete (ricevente non riceve) si usa un **_countdown timer_** che parte dopo l’invio del pacchetto.
Il <u>trasmittente</u> è in attesa del **riscontro** e:
- Se questo arriva **prima** che il timer scada, il timer è resettato e si gestisce il riscontro,
- Se scade il timer e questo **non** è ancora **arrivato**, il pacchetto è ritrasmesso.
Il <u>ricevente</u>, ricevuto il pacchetto e verificato che riscontro inviare, è in attesa del **prossimo** **pacchetto** e:
- Se questo arriva prima che il timer scada, il timer è resettato e si gestisce il nuovo pacchetto,
- Se scade il timer e questo non è ancora arrivato, il riscontro è ritrasmesso.
In entrambe le situazioni è possibile che un pacchetto abbia invece preso un percorso lungo o lento, quindi nasce il problema della **duplicazione dei pacchetti** in rete, che si risolve con **n° di sequenza** dato a ogni pacchetto, cosi che il ricevente capisca se lo ha già ricevuto (duplicato) o no. (Nei protocolli **_send-and-wait_** il ricevente aspetta **1 pacchetto alla volta** perché il trasmittente **non può trasmettere** se prima non arriva **l’ACK** o scade il **_countdown_ _timer_**, quindi i pacchetti numerati solo con **0** o **1**).
### Protocolli sliding window
I protocolli **_sliding window_** prevedono di trasmettere **_N_ pacchetti** (**N** = **apertura della finestra**) prima di attendere riscontri. Il momento in cui sono riscontrati gli _N_ pacchetti dipende dal tipo di trasmissione, che può essere:
- **Half-duplex**: il ricevente deve aver ricevuto tutti gli _N_ pacchetti prima di inviare il riscontro,
- **Full-duplex**: il ricevente può inviare riscontri senza dover attendere l’arrivo di tutti i pacchetti (se il riscontro è inserito in un **pacchetto di dati** reinviato al trasmittente, si parla di **_piggybacking_**, “portare in groppa”).
Capita che alcuni degli _N_ pacchetti trasmessi si **perdano** o arrivino **alterati**, per risolvere ciò ci sono 2 tecniche:
##### Go-back-N
Il ricevente, quando riceve un pacchetto errato (CRC/checksum) o fuori sequenza (qualche pack prima perso), **ignora** i pacchetti **successivi** e reinvia al trasmittente un riscontro del pacchetto **_N-1_** (sequenza di pacchetti precedente) che comporterà la ritrasmissione di tutti i pacchetti a partire dal pacchetto **_N_**. Riscontrando il pacchetto _N-1_ è implicito il riscontro positivo (ACK) di tutti i pacchetti precedenti (N-1, N-2…), ciò è detto **_acknowledgement cumulativo_**.
##### Selective repeat
Il ricevente accetta e memorizza tutti i pacchetti ricevuti corretti (sia in sequenza sia non) poi agisce in 2 modi:
- Manda un **ACK** specifico per ogni **pacchetto** ricevuto **corretto**,
- Manda un **NAK** per i singoli **pacchetti** **corrotti** o **fuori sequenza**.
(Diversi modi provocano problemi tra trasmittente e ricevente; ricevente deve anche pensare al riordino pacchetti fuori sequenza).
# Controllo di flusso e della congestione
I protocolli, oltre a offrire servizi affidabili/inaffidabili e con/senza connessione, possono offrire servizi aggiuntivi:
### Controllo del flusso 
(Un servizio _host-to-host_) **capacità** di un trasmittente **di** **rallentare la trasmissione di pacchetti** quando si accorge che il **destinatario non riesce ad elaborarli con la dovuta velocità**.
I motivi di lentezza possono essere: scarsità di memoria nel buffer, eccessiva multiprogrammazione o lentezza CPU.
Il controllo di flusso evita la perdita di pacchetti presso il destinatario causata dall’**_overflow_ di buffer di ricezione**.
### Controllo della congestione
(Un servizio _host-to-network_) **capacità** di un trasmittente **di** **rallentare la trasmissione di pacchetti** quando si accorge che la **rete** (**router** di infrastruttura) **non riesce ad elaborarli con la dovuta velocità**.
Il motivo di lentezza è solitamente l’eccessivo traffico in rete.
Il controllo di congestione evita la perdita di pacchetti nei router per l’**_overflow_ dei loro buffer di ricezione o inoltro**.
# TCP
Usato per app che non tollerano perdite o alterazioni nell’ordine di pacchetti ma che tollerano ritardi.
### Caratteristiche
##### Connection oriented
Il TCP è un protocollo **_connection oriented_** che stabilisce una connessione permanente (detta **sessione**) tra gli host prima di trasmettere dati. Prima di stabilire la sessione, TCP:
- Riceve dati dall’applicazione trasmittente,
- Accumula i dati in un buffer di trasmissione,
- Periodicamente (o in presenza di particolari condizioni) crea un segmento con parte dei dati nel buffer. Il protocollo attende fino a quando la giusta quantità di dati è nel buffer in quanto **dimensione** del segmento è importante per le **prestazioni**.
Durante l’instaurazione della sessione (**_handshake_**), trasmittente e destinatario stabiliscono la **_window size_** (anche diversa nelle 2 direzioni), ovvero la **quantità di dati** che può essere **inviata** **in un** certo **periodo di tempo**.
##### Reliable
Essendo **affidabile**, TCP garantisce che ciascun segmento inviato dal trasmittente arrivi a destinazione. Nel caso in cui un segmento si perda o risulti corrotto, TCP lo **ritrasmette**. Dato che le reti presentano percorsi multipli di lunghezza diversa, i segmenti possono raggiungere la destinazione in **ordine diverso** da come sono trasmessi, perciò TCP fornisce un servizio di **numerazione** dei segmenti per poterne ricostruire la corretta sequenza.
##### Controllo del flusso 
(O _flow control_), per questo TCP è in grado di accorgersi se un **destinatario** che riceve pacchetti **è sovraccaricato** e nel caso **riduce il tasso di trasmissione dei pacchetti** (previene la necessità di ritrasmissione di segmenti persi per **_buffer overflow_**).
##### Controllo della congestione 
(O _congestion control_), per questo TCP è in grado di accorgersi se la **rete** **è sovraccaricata** e nel caso **riduce il tasso di trasmissione dei pacchetti**.
##### Stateful
Il TCP è **_stateful_**, ovvero tiene traccia di stato delle sessioni, memorizzando varie info utili per implementare servizi.
##### Altro
Il TCP è **full-duplex** e **unicast tra trasmittente e ricevente** (multicast non permesso).
### Segmento TCP

Il pacchetto TCP è detto segmento e ha un _overhead_ di 20 byte (opzioni di solito non c’è); i campi sono:
- **_Source port_** (16 bit) e **_Destination port_** (16 bit), usati per **identificare l’applicazione** e realizzare le attività di **multiplexing** e **demultiplexing** del livello trasporto.
- **_Sequence number_** (32 bit), usato per **riordina**re i **segmenti** di una trasmissione.
- **_Acknowledgement number_** (32 bit), o **n° di riscontro**, indica il dato che viene riscontrato.
- **_Data offset_** (4 bit), è la **lunghezza dell’header** (bit di offset prima del payload/dati, se > 5 ci sono opzioni).
- **_Reserved_** (3 bit), bit riservati.
- **_Control bits_** (9 bit), **flags** usate da TCP per diversi scopi, tra cui:
  - **SYN**, **ACK** e **FIN**, usati per gestire la connessione (**_3-way handshake_**).
  - **RST**, _reset_, usato per resettare una connessione in caso di errore o _timeout_.
  - **URG**, a **1** indica che il campo **_Urgent pointer_** è valido.
  - **PSH**, usato in app soggette a **ritardi** (**_real-time_**) per la bufferizzazione dei dati presso sia TCP trasmittente sia TCP ricevente, chiede di inviare i dati nel buffer all’applicazione ricevente.
- **_Window size_** (16 bit), apertura della **finestra di ricezione**, indica il **n° max di byte trasmissibili prima di 1 ACK positivo**.
- **_Checksum_** (16 bit), campo di controllo con errori di **_header_**, **_payload_** e alcuni **campi IP** (IP sorg, IP dest, n° protocollo…).
- **_Urgent pointer_** (16 bit), individua **l’ultimo byte di dati urgenti** nel payload.
- **_Options_** (0-320 bit, in unità di 32 bit), con:
  - Negoziazione opzionale di MSS (default 536 byte, max 65535 byte) --> tipo opzione 2 (con SYN impostato).
  - Negoziazione Window scale --> tipo opzione 3 (con SYN impostato).
  - Selective acknowledgement (SACK invece di go-back-N) possibile --> tipo opzione 4 (con SYN impostato).
  - Selective acknowledgement (SACK), in opzioni ci sono i blocchi di dati riconosciuti (anche non contigui) riconosciuti --> tipo opzione 5 (con SYN impostato).
### Gestione della connessione
##### 3-way handshake
Una connessione TCP è stabilita quando un client inizia a comunicare con un server e richiede 3 step:
1) Il TCP **client** **invia** al TCP **server** un segmento **SYN** che non ha dati ma **ha** il **SYN** a **1** e il suo ***sequence number*** a un valore **casuale** (*numSeqClient*).
2) **Dopo** aver **ricevuto** il segmento **SYN**, il TCP **server** **alloca** i **buffer** per ricezione/invio **e** le altre **variabili** TCP per la connessione. Poi **crea** un segmento **SYNACK** che non ha dati ma **ha SYN e ACK a 1**, l’***acknowledgement number*** uguale a *numSeqClient* + 1 e il suo ***sequence number*** a un valore **casuale** (*numSeqServer*).
    Ogni pacchetto TCP deve essere riscontrato, quindi **questo ACK riscontra il SYN prima ricevuto**).
3) **Dopo** aver **ricevuto** il segmento **SYNACK**, il TCP **client** **alloca** i **buffer** per ricezione/invio **e** le altre **variabili** TCP per la connessione. Poi **crea** un segmento **ACK** che non ha dati ma ha **SYN a 0, ACK a 1**, l’**acknowledgement number** uguale a *numSeqServer* + 1 e ***sequence number*** a *numSeqClient* + 1.
Il **_3-way handshake_** permette di:
- Dire se il **destinatario** è **presente** sulla **rete**,
- Dire se **sul** **destinatario** c’è **un server** **che** **accetta** **richiesta** del client,
- **Dire al destinatario** che **client vuole comunicare su** un **n° di porta**,
- **Stabilire** **parametri** di **sessione** (*sequence numbers* iniziali, *window size*…).
### Terminazione della connessione
La **terminazione** di una connessione può essere iniziata sia da **client** sia da **server**.
Per chiuderla è usato il **flag FIN** (*finish*) e dato che la connessione è ***full*-duplex**, la terminazione deve avvenire in **entrambe le direzioni** (non per forza insieme). Ogni **pacchetto** **FIN** (o **_shutdown_**) **va riscontrato con** un **ACK**; perciò, per chiudere una connessione, servono **4 pacchetti** (**2 coppie di FIN+ACK in entrambe le direzioni**).
**Al** **termine**, **client** e **server** TCP **deallocano** le **risorse** (buffer e variabili) usate.
### Attacchi SYN flood
I ***SYN flood attacks*** sono degli attacchi alla rete che sfruttano le vulnerabilità dell’**handshake** del TCP. In questi si mandano **tanti SYN** all’obiettivo **senza** poi **fare** il 3° passo (**l’ACK**); e, poiché **per ogni SYN** ricevuto il **server** **alloca** **buffer** e **variabili** **per** rispondere col **SYNACK**, il **server** potrebbe **esaurire** le sue **risorse** e **non** **riuscire** a **gestire** le **connessioni** giuste/**legittime** (attacco DoS, ***Denial of Service***).
### Servizio affidabile
##### Sequence number
Il **_sequence number_** di un segmento è il **n° del 1° byte del segmento** **rispetto al flusso** di byte **trasmesso** (per **segmenti** da **1000 byte**: **1°** sequence number = **1**, **2°** … = **1001**, **3°** … = **2001** e così via). Dato che il TCP vede i dati solo come un flusso di byte ordinati, i _sequence number_ contano i **byte** trasmessi e non i segmenti inviati.
Per prevenire certi **_malicious attacks_**, il TCP, durante l’instaurazione della connessione (**3-way handshake**) stabilisce un **valore casuale** da cui partire per contare i byte, che sarà il **_sequence number_** **iniziale** (quindi non per forza 1).
**Quando** un **segmento** è **trasmesso**, il **_sequence number_** è **incrementato** **del** **n°** dei **byte trasmessi**. Ciò rende ogni segmento identificabile e riscontrabile senza ambiguità; ed è anche possibile rilevare i segmenti persi.
Il TCP ricevente riceve i dati, li mette nel buffer di ricezione rispettando l’ordine, li riassembla e li dà al livello applicativo.
##### Acknowledgement number
L’**_acknowledgement number_** invece è il **n° del prossimo byte che ci si aspetta di ricevere** (si riferisce sempre al flusso di byte).
Se un host che riceve un segmento (con byte da 1 a 1000) deve inoltrare un ACK al trasmittente, esso incrementerà l’_acknowledgement number_ di **1** (1001) perché quello è il _sequence number_ del byte aspettato (tenendo anche qui conto del valore casuale stabilito all’inizio, non per forza 1001).
L’**_acknowledgement number_** è **valido** solo **quando** il flag **ACK** è a **1** (di solito è a 0 solo nei segmenti SYN).
Per le **perdite** si può usare sia **_go-back-N_** sia **s_elective repeat_**; ma alcuni usano la **_selective acknowledgement_** (**SACK**). (Se entrambi supportano **SACK**, il destinatario può riscontrare segmenti non contigui e richiedere di ritrasmettere solo quelli persi).
Essendo **_full-duplex_**_,_ TCP può usare il **_piggybacking_** per riscontrare segmenti ricevuti (di solito 1 ACK per segmento ricevuto).
# Controllo di flusso
### Cos'è?
**Controllo di flusso** significa: **regolare** **l’invio** di **segmenti** del trasmittente, per **diminuirne l’afflusso alla destinazione**.
##### Situazione
Durante il _3-way handshake_ gli host riservano dei **buffer** di **invio** e **ricezione**, e quando sono ricevuti dei dati corretti, il TCP li mette nel buffer di ricezione in ordine. I processi applicativi però **non leggono il buffer sempre**, ma **solo** **quando** è **pieno**, **e** **non** lo fanno **necessariamente** **quando** **lo** **diventa**. Quindi se una app è lenta a leggere il buffer, si rischia che il trasmittente mandi in **_overflow_** il **buffer di ricezione** (se troppo veloce).
##### Soluzione
Il trasmittente ha una variabile detta **_send window_** (finestra di spedizione) che indica quanto **spazio libero** c’è **nel buffer** **di ricezione** del **destinatario** (dato **preso dal campo _window size_ dei segmenti** inviati **dal destinatario**) e proverà a trasmettere una quantità di dati **minore** di questo valore.
Il destinatario invia un **ACK** non appena **processa** dei **dati** **ricevuti** (**ogni volta**, non aspetta tutti i byte) cosicché il trasmittente possa **riadattare** la sua **_send window_** al valore di **_window size_ ricevuto** aumentandola o riducendola in base allo spazio nel buffer di ricezione del destinatario. Questo riaggiustamento è detto **_sliding window_**.
##### Problemi
Un **problema** è legato alla **_sliding window_**, la quale prevede che ogni host **mantenga i pacchetti inviati nel buffer di** **trasmissione** nel caso si debbano ritrasmettere, **scartandoli** **solo** **dopo** averne ricevuto il relativo **ACK**.
Nelle reti a **banda** **molto** **larga** ma con **elevata** **latenza** il trasmittente potrebbe **inviare** un’intera **_window_** in segmenti **prima** ancora **che** l’**ACK** **del** **1°** **segmento** sia **tornato**, lasciando il **trasmittente** in attesa e con **buffer di invio pieno**.
Per questo nella **RFC 1323** sono state introdotte le **opzioni di scala** della **_window_ TCP** per aumentare la **dimensione** **della** **_window_** **di** **ricezione** **oltre** i **65535** **byte** (**ora** fino a **1 GB**), valore negoziato nei **SYN** del **_3-way handshake_**.
##### Zero window
Un valore **_zero window_** indica che il **buffer in ricezione è esaurito** (spesso per processi bloccanti, poche risorse o app lente), quindi il **trasmittente** **interrompe** **l’invio** **di** **segmenti** finché non ottiene un nuovo segmento con **_window size_ > 0**. Il ricevitore può anche **sparare cazzate** (tipo quando il suo **buffer si svuota lentamente**) per impedire al trasmittente di mandare **segmenti corti** con **molto overhead**.
### Indicatori di dimensione
- **_Window size_**: quantità di byte trasmissibili senza attendere un ACK.
- **MTU** (_Maximum Transport Unit_): dimensione max di un datagram IP (senza bisogno di frammentarlo) in byte. 
  Ovvero la **dimensione** del **payload** del **protocollo datalink usato** (Ethernet = 1500), IPv4 = 576, IPv6 = 1280.
- **MSS** (_Maximum Segment Size_): dimensione max del payload dei segmenti TCP da inviare (in byte).
(foto)
L’**MSS** è stabilita con il **SYN** del _3-way handshake_ e **non** può essere **modificata**. Il valore di default è stabilito dagli OS:
**MTU** – (**_header_ TCP** + **_header_ IP**) = **MSS** (molti hanno 1500 – 20 – 20 = 1460 byte).
Se nel percorso vi è un **link** con **MTU < MSS**, il **pacchetto IP** è **scartato** e il router informa il mittente con un **pacchetto** **ICMP** (type 3, code 4) “**Need to Fragment**”, che contiene il **valore** dell’**MTU** **accettato** (mittente lo userà per **l’MSS**).
# Controllo di congestione
### Cos'è?
La **congestione** riguarda la rete e i router di infrastruttura e si ha in 2 situazioni:
- All’**inizio** di essa, quando il **tempo di transito** nella rete (**RTT**) **aumenta**.
- All’**aumento** di essa, quando i **pacchetti si perdono** per il **_timeout_** (**_countdown timer_** che **scade**). 
  (Per esempio passando da collegamenti più veloci ad altri più lenti, tipo da gigabit ad ADSL, pacchetti rallentano).
### Approfondimenti
TCP impone al mittente un **limite alla frequenza di invio dei segmenti** in base al **livello** “percepito” della **congestione**, grazie al **RTT** (usato dato che è a livello rete, di router e non trasporto).
Il **throughput** (quantità di dati trasmessi nell’unità di tempo) di una comunicazione TCP è limitato da:
##### Finestra di congestione
Contiene la **qta di byte trasmissibili in 1 segmento** e cerca di non superare la capacità di rete. È **dinamica** e varia in base alla congestione della rete adattandosi ai sovraccarichi. Variabile **_cwnd_**, è = al **n° di pacchetti inviabili per volta**.
##### Finestra di ricezione
Contiene la **qta di byte trasmissibili prima di** aspettare **1 ACK** e cerca di non superare la capacità del ricevitore di elaborare dati. Variabile **_rwnd_**, è = al **limite max che la _cwnd_ può assumere** (dimensione finestra ricezione destinatario).
### Modalità di invio pacchetti
TCP usa le variabili _cwnd_ (**_congestion window_**) e **_ssthresh_** (**_slow-start threshold_**, soglia/limite) per le modalità di invio pacchetti:
##### Slow start
All’avvio la **_cwnd_** è messa a **1** MSS e ad ogni **ACK positivo** (quindi non c’è congestione e c’è banda) il suo valore è **raddoppiato** (IF _cwnd_ < _ssthresh_ THEN **_cwnd_ $*$= 2**) fino al valore max di **_ssthresh_** (fase **_slow start_**).
##### Congestion avoidance
Superato l’**_ssthresh_**, si passa dal raddoppiamento all’**incremento** della cwnd (IF _cwnd_ >= _ssthresh_ THEN **_cwnd_++**), (fase **_congestion avoidance_**).
Quando TCP rileva **perdite**, considera la rete **congestionata** e cambia **modalità** (ciò per **timeout** o **3 o + ACK duplicati**).
### Rilevamento perdite
Si vede come in entrambi i casi i pacchetti spediti in 1 volta **aumentano**, di conseguenza aumenta anche il **n°** degli **ACK** **da** **riscontrare**. Quando la rete si congestiona, qualche pacchetto **si** **perde**; e ognuno ha il suo **_acknowledgement number_**, che indica il **successivo** **_sequence number_** aspettato.
Quando alla destinazione arriva un pacchetto fuori sequenza, l’**_acknowledgement number_** **rimane** quello **precedente** anche per i successivi, ad indicare che quello non è arrivato (ES: pack 6, ACK non c’è).
# UDP
### Caratteristiche
- **_Connectionless_**
- **_Unreliable_**
- **Non** **_full-duplex_**
- Sia **_unicast_** che **_multicast_**
### Ambiti applicativi
Usato in:
- App che **tollerano perdite** ma non **ritardi** e che richiedono l’**elaborazione** **senza** **buffer** (**_real-time_**).
- App che **inviano pacchetti piccoli** (quindi non richiedono segmentazione) o **notifiche** (tipo DHCP e DNS).
- App che **spediscono pacchetti a + destinatari** (IP **multicast**), tipo Skype, UPnP, auto-config e attività di _discovery_.
### Descrizione
Definito nella **RFC 768**, **UDP** (_User Datagram Protocol_) fornisce un servizio simile a IP ma al livello applicativo.
(User perché UDP è usato dagli utenti, mentre IP dagli OS).
##### Come lavora
Essendo un protocollo di livello trasporto esegue le attività di **_multiplexing_** (in **uscita**) e **_demultiplexing_** (in **entrata**), per mezzo dei **n° di porta**. Con **UDP** **non** c’è **bufferizza**zione (al contrario di TCP), quindi permette un controllo più preciso a livello applicativo su quanti dati inviati e su quando sono stati inviati ed elaborati.
Con controllo di flusso e congestione del TCP, una app non può sapere se i dati sono stati inviati o ancora nel buffer; al contrario **UDP**, impacchetta i dati e li trasferisce al livello inter-rete **appena li riceve** dal livello applicativo.
Inoltre l’**UDP** **non** **fa** nessun **_handshake_** e quindi **non** **introduce** **ritardi**.
##### Unreliable
UDP è **inaffidabile**, quindi esegue l’incapsulamento dei dati ma **non** **controlli** **in ricezione** (oltre al **_checksum_**), quindi riassembla i pacchetti nell’**ordine di arrivo**, non di partenza, senza controllare se vi siano **perdite** o **duplicazioni**. Se l’app ritiene importante l’ordine dei segmenti, dovrà gestirne la corretta sequenza, stabilendo come processare i dati. Una **app UDP** può essere resa **affidabile** inserendo nell’app stessa dei meccanismi di **notifica** e **ritrasmissione**.
##### Stateless
**UDP** è **stateless**, **non memorizza informazioni sulle sessioni di comunicazione** (1 server UDP può gestire molti + client UDP).
##### Altro
L’**_header_** dell’**UDP** è di **8 byte** al contrario dei 20 del TCP.
Anche se presenta vantaggi in **velocità**, mandare pacchetti alla loro frequenza di produzione nella rete **senza** **controllo di congestione** implica **sovraccarichi** della rete e il **rischio** che tanti pacchetti vengano **persi**.
### Datagram UDP
Il pacchetto UDP è detto **datagram**, per sottolineare il servizio **_best-effort_** dato. Il suo **overhead** è di **8 byte**. I campi:
- **Source port** e **Destination port** (16 + 16 bit) --> usati per identificare l’app e per multiplexing e demultiplexing,
- **Length** (16 bit) --> **Lunghezza** dell’intero **datagram** (_header_ + dati),
- **Checksum** (16 bit) --> **Campo** di **controllo** dell’**errore** (check di header + payload).