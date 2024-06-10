### Cos'è?

Il **controllo di flusso** è un servizio *host-to-host*, ed esso **regola l’invio di segmenti** del trasmittente, per **diminuirne l’afflusso alla destinazione**.

> [!important] Controllo di flusso
> **Capacità** di un trasmittente **di rallentare la trasmissione di pacchetti** quando si accorge che il **destinatario non riesce ad elaborarli con la dovuta velocità**.

I motivi di lentezza possono essere: scarsità di memoria nel buffer, eccessiva multiprogrammazione o lentezza CPU.

Il controllo di flusso evita la perdita di pacchetti presso il destinatario causata dall’***overflow* di buffer di ricezione**.

##### Situazione

Durante il *3-way handshake* gli host riservano dei **buffer** di **invio** e **ricezione**, e quando sono ricevuti dei dati corretti, il TCP li mette nel buffer di ricezione in ordine. I processi applicativi però **non leggono il buffer sempre**, ma **solo quando** è **pieno**, **e non** lo fanno **necessariamente quando lo diventa**. Quindi se una app è lenta a leggere il buffer, si rischia che il trasmittente mandi in ***overflow*** il **buffer di ricezione** (se troppo veloce).

##### Soluzione

Il trasmittente ha una variabile detta ***send window*** (finestra di spedizione) che indica quanto **spazio libero** c’è **nel buffer di ricezione** del **destinatario** (dato **inserito nel campo *window size* degli ACK** inviati **dal destinatario**) e proverà a trasmettere una quantità di dati **<** di questo valore.

Il destinatario invia un **ACK** non appena **processa** dei **dati ricevuti** (**ogni volta**, non aspetta tutti i byte) cosicché il trasmittente possa **riadattare** la sua ***send window*** al valore di ***window size* ricevuto** aumentandola o riducendola in base allo spazio nel buffer di ricezione del destinatario. Questo riaggiustamento è detto ***sliding window***.

##### Problemi

Un **problema** è legato alla ***sliding window***, la quale prevede che ogni host **mantenga i pacchetti inviati nel buffer di trasmissione** nel caso si debbano ritrasmettere, **scartandoli solo dopo** averne ricevuto il relativo **ACK**.

Nelle reti a **banda molto larga** ma con **elevata latenza** il trasmittente potrebbe **inviare** un’intera ***window*** in segmenti **prima** ancora **che** l’**ACK del 1° segmento** sia **tornato**, lasciando il **trasmittente** in attesa e con **buffer di invio pieno**.

Per questo nella **RFC 1323** sono state introdotte le **opzioni di scala** della ***window* TCP** per aumentare la **dimensione della *window* di ricezione oltre** i **65535 byte** (**ora** fino a **1 GB**), valore negoziato nei **SYN** del ***3-way handshake***.

##### Zero window

Un valore ***zero window*** indica che il **buffer in ricezione è esaurito** (spesso per processi bloccanti, poche risorse o app lente), quindi il **trasmittente interrompe l’invio di segmenti** finché non ottiene un nuovo segmento con ***window size* > 0**. Il ricevitore può anche **sparare cazzate** (tipo quando il suo **buffer si svuota lentamente**) per impedire al trasmittente di mandare **segmenti corti** con **molto overhead**.

### Indicatori di dimensione

- ***Window size***: quantità di byte trasmissibili senza attendere un ACK.
- **MTU** (*Maximum Transport Unit*): dimensione max di un datagram IP (senza bisogno di frammentarlo) in byte.

  Ovvero la **dimensione** del **payload** del **protocollo datalink usato** (Ethernet = 1500), IPv4 = 576, IPv6 = 1280.

- **MSS** (*Maximum Segment Size*): dimensione max del payload dei segmenti TCP da inviare (in byte).

(foto)

L’**MSS** è stabilita con il **SYN** del *3-way handshake* e **non** può essere **modificata**. Il valore di default è stabilito dagli OS:

**MTU** – (***header* TCP** + ***header* IP**) = **MSS** (molti hanno 1500 – 20 – 20 = 1460 byte).

Se nel percorso vi è un **link** con **MTU < MSS**, il **pacchetto IP** è **scartato** e il router informa il mittente con un **pacchetto ICMP** (type 3, code 4) “**Need to Fragment**”, che contiene il **valore** dell’**MTU accettato** (mittente lo userà per **l’MSS**).

![](https://i.imgur.com/zDgwGbu.png)

