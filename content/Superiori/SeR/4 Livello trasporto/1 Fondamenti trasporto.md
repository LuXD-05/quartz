---
public: true
modified_at: 16/06/2024 14:55:25
edited_seconds: 40
---
### Fondamenti
Hint: intro, lato mittente e destinatario, segmentazione
::
Il livello trasporto esegue una consegna ***process-to-process*** perché fornisce servizi ai <u>processi applicativi</u>. I protocolli di livello trasporto sono implementati <u>negli host</u> (non nei router).
##### Lato mittente
Il livello riceve <u>dati del livello applicativo</u> e li **incapsula in segmenti** poi passati al livello rete (***multiplexing***, tanti messaggi diversi ad un unico pacchetto livello rete).
##### Lato destinatario
Il livello <u>riceve i segmenti dal livello rete</u> sottostante, fa il ***checksum***, estrae il **messaggio** (dati) e lo da al processo applicativo a cui è indirizzato (***demultiplexing***, dal protocollo rete a + applicazioni diverse).
#### Segmentazione
Le reti trasportano pacchetti di <u>dimensione limitata</u>, quindi i protocolli di livello trasporto li **segmentano** a dimensioni adatte. 
I segmenti sono <u>incapsulati in pacchetti</u> e gli viene aggiunto un **header** con le info necessarie a riassemblarli quando arriveranno al destinatario.
<!--SR:!2024-05-01,3,220-->

### Tipo di servizio
Hint: UDP (3) e TCP (5), TCP o UDP?
::
App diverse richiedono, insieme al servizio da usare, cose diverse, quindi TCP/IP prevede 2 protocolli livello trasporto:
##### UDP
(*User Datagram Protocol*):
- ***Connectionless***, quindi <u>inaffidabile</u>;
- <u>Non segmenta i dati</u>;
- Fa solo il *checksum* (se ok passa il *payload* al processo destinatario, se no lo scarta).
##### TCP
(*Transmission Control Protocol*):
- ***Connection oriented***, quindi <u>affidabile</u> (offre anche [[3.1 Controllo di flusso|controllo di flusso]] e [[3.2 Controllo di congestione|controllo di congestione]]);
- <u>Segmenta i dati</u>;
- <u>Numera e traccia i segmenti trasmessi</u> da un certo processo di un certo host,
- <u>Fa ACK</u> per riconoscere i dati ricevuti,
- <u>Ritrasmette ogni segmento non riconosciuto/valido</u> dopo un *timeout*.
#### TCP o UDP?
I dev scelgono quale protocollo usare in base all’app da fare: 
- App con db, web browser o client di posta che hanno necessità che tutti i dati arrivino <u>senza perdite, duplicazioni e in ordine</u>, usano **TCP** (comunicazione + robusta tra app, ma generano *overhead* e ritardi in trasmissione). 
- Quelle che invece che <u>tollerano qualche perdita ma non ritardi nella consegna</u>, (telefonia, radio o tv internet) usano **UDP** (funzioni di base di consegna + check e overhead minimi; detto *best-effort*).
(*Streaming* non *real-time* tipo YouTube usano <u>TCP</u> perché trasmettono video non generato subito, quindi in caso di calo di banda l’app sospende la riproduzione lasciando tempo a TCP di ristabilire una banda adeguata).
<!--SR:!2024-04-30,2,200-->

### Identificazione delle app
Hint: intro, porta sorgente e destinazione, client cosa fa, tipi (well-known, registered e ephimeral), socket (+ socket pair)
::
Un host può avere <u>+ processi</u> (app) che comunicano in rete <u>simultaneamente</u> con altri su 1 o + host remoti. Il livello trasporto deve quindi identificare le app a cui consegnare i pacchetti e usa i **numeri di porta**.
#### Numeri di porta
Nell’*header* dei segmenti ci sono dei campi che permettono a TCP e UDP di gestire + conversazioni:
- **N° di porta sorgente** (porta associata al processo sull’host **locale**),
- **N° di porta destinazione** (porta associata al processo sull’host **remoto**).
La comunicazione è **sempre iniziata dal client** (verso il server) che **genera dinamicamente un n° di porta sorgente univoco** per ogni conversazione (così sono possibili + di 1 in contemporanea, tipo per mandarne + a 1 un web server).
##### Tipi di numeri di porta
###### Well-Known (0 – 1023)
Riservate a app **server** cosicché i client richiedano servizi a una porta specifica nei server.
###### Registrate (1024 – 49151)
Sempre per app server, assegnati dalla IANA a un’entità richiedente per usi specifici.
###### Dinamiche (49152 – 65535)
(O *ephimeral port)* assegnati dall’OS di un host quando un client inizia una comunicazione con un server.
![](https://i.imgur.com/1RiYFOE.png)
#### Socket
È la combinazione tra **IP** e **n° di porta** in formato \[**IP**]:\[**port**] sia **sorgente** sia **destinazione**. Identifica un processo su un host. Il socket ha l’IP dell’host e la porta generata (casuale nel client) mentre a destinazione la porta è specifica.
###### Socket pair
La corrispondenza tra <u>socket sorgente e socket destinatario</u> è detta ***socket pair***, e discrimina una comunicazione.
<!--SR:!2024-05-01,3,220-->
