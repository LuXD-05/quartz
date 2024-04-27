# Fondamenti

Il livello trasporto esegue una consegna **process-to-process** perché fornisce servizi ai **processi applicativi**.

I protocolli di livello trasporto sono implementati **negli host** (non nei router).

##### Lato mittente

Il livello riceve i **messaggi** del livello applicativo e li **incapsula** in **segmenti** poi passati al livello rete (***multiplexing***, tanti messaggi diversi ad un unico pacchetto livello rete).

##### Lato destinatario

Il livello riceve i **segmenti** dal livello rete sottostante, fa il **checksum**, ed estrae il **messaggio** (dati) che va al processo applicativo a cui è indirizzato (***demultiplexing***, dal protocollo rete a + applicazioni).

Un host può avere **+ processi** (app) che comunicano in rete **simultaneamente** con altri su 1 o + host remoti; e il compito del livello trasporto è tenere traccia di queste conversazioni.

### Segmentazione

Le reti trasportano pacchetti di dimensione **limitata**, quindi i protocolli di livello trasporto li **segmentano** a dimensioni adatte. I segmenti sono incapsulati in pacchetti e gli viene aggiunto un **header** con le info necessarie a riassemblarli quando arriveranno al destinatario.

### Identificazione delle applicazioni

Il livello trasporto deve **identificare le applicazioni** a cui consegnare i pacchetti; ciò è fatto con il **n° di porta**, un **identificatore unico per ogni processo in un host**.

### Tipo di servizio

App diverse richiedono, insieme al servizio da usare, cose diverse, quindi TCP/IP prevede 2 protocolli livello trasporto:

##### UDP

(*User Datagram Protocol*):

- ***Connectionless***, quindi inaffidabile;
- **Non segmenta** i dati;
- Fa solo il **checksum** (se ok passa il payload al processo destinatario, se no lo scarta e non avvisa nessuno).

##### TCP

(*Transmission Control Protocol*):

- ***Connection oriented***, quindi affidabile (offre anche **controllo di flusso e di congestione**);
- **Segmenta** i dati;
- Esegue 3 operazioni base:
- Numera e tiene **traccia** dei **segmenti trasmessi** da un certo processo di un certo host,
- Esegue ***ack*** per riconoscere i dati ricevuti,
- **Ritrasmette** ogni **segmento non riconosciuto/valido** dopo un ***timeout***.

### TCP o UDP?

I developer scelgono quale protocollo usare in base all’app da fare. App con db, web browser o client di posta che hanno necessità che **tutti i dati** arrivino **senza perdite, duplicazioni e in ordine**, usano **TCP**. Quelle che invece che **tollerano qualche perdita** ma **non ritardi nella consegna**, (telefonia, radio o tv internet) usano **UDP**.

**TCP**: vantaggio di comunicazione + robusta tra app, ma generano ***overhead*** e **ritardi in trasmissione**.

**UDP**: funzioni di base di consegna + check e overhead minimi; detto ***best-effort*** perché **inaffidabile**.

(*Streaming* non *real-time* tipo YT usano TCP perché trasmettono video non generato subito, quindi in caso di calo di banda l’app sospende la riproduzione lasciando tempo a TCP di ristabilire una banda adeguata)

### Numeri di porta

Nell’header del pacchetto TCP ci sono dei campi che permettono a TCP e UDP di gestire + conversazioni:

- **N° di porta sorgente** (porta associata al processo sull’host **locale**),
- **N° di porta destinazione** (porta associata al processo sull’host **remoto**).

La comunicazione è **sempre iniziata dal client** (verso il server) che **genera dinamicamente un n° di porta sorgente univoco** per ogni conversazione (così sono possibili + di 1 in contemporanea, tipo per mandarne + a 1 un web server).

(Porta sorgente e destinazione nel pacchetto livello trasporto poi incapsulati in IP avente IP sorgente e destinazione)

### Socket

È la combinazione tra **IP** e **n° di porta** in formato \[**IP**]:\[**port**] sia **sorgente** sia **destinazione**. Identifica in processo su un host. Il socket ha l’IP dell’host e la porta generata (a cazzo) mentre a destinazione la porta è specifica.

La corrispondenza tra socket sorgente e socket destinatario è detta ***socket pair***, e discrimina una conversazione.

### Tipi di numeri di porta

###### **Well-Known** (0 – 1023)

Riservate a app **server** cosicché i client richiedano servizi a una porta specifica nei server.

###### **Registrate** (1024 – 49151)

Sempre per app server, assegnati dalla IANA a un’entità richiedente per usi specifici.

###### **Dinamiche** (49152 – 65535)

(O *ephimeral port)* assegnati dall’OS di un host quando un client inizia una comunicazione con un server.

![](https://i.imgur.com/1RiYFOE.png)

