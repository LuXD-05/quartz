### Cos'è?

L’email è un sistema di comunicazione **asincrono**: l’utente invia e riceve messaggi senza sincronizzarsi con altri. Il sistema di email presenta 3 componenti principali:

##### MUA

(*Mail User Agent*), interfacciano l’utente con il sistema di posta (Outlook, Gmail…); e a tale scopo eseguono sw *SMTP client* per contattare un *SMTP server* sul **mail server** in uso.

##### Mail servers

Server di posta, sono il nucleo dell’infrastruttura del servizio e: 

- <u>Ricevono le email da consegnare</u> salvandole in ***mailbox*** (depositi di email ricevute),
- <u>Inoltrano le email a destinazione</u> salvandole in ***message queue*** (code di email in transito).

Eseguono poi dei sw:

- ***SMTP server*** per <u>rispondere a SMTP client del MUA utente</u>.
- ***SMTP client*** per <u>contattare il mail server destinatario</u> di 1 mail.

##### Protocollo SMTP

(*Simple Mail Transfer Protocol*), è un protocollo ***push*** (di invio) che definisce le <u>regole di invio del messaggio da un client a un mail server</u>.

![](https://i.imgur.com/DZFU2P0.png)

### Uso

1) Il **MUA client** invia l’email al ***mail server* mittente**, proseguendo poi in internet.
2) L’email arriva al ***mail server* destinatario** (*recipient mail server* per la mailbox) che la salva nella *mailbox* del destinatario. 

Se il *mail server* mittente <u>non riesce a consegnare la mail</u> al *mail server* destinatario, la <u>trattiene</u> nella sua *message queue* e, periodicamente, <u>riprova a trasferirla</u>. Dopo un n° di tentativi falliti, <u>email rimossa e notificato il fallimento</u>.

### SMTP

Protocollo definito nella RFC 821 del 1982. Caratteristiche:

- I messaggi (pacchetti a livello applicativo) devono essere in <u>US-ASCII a 7 bit</u>,
- Sono usate <u>connessioni TCP permanenti</u> (+ messaggi trasferibili tra 2 mail server in 1 connessione),
- Usa la <u>porta 25</u>. È un protocollo **full-duplex, stateful, in-band, affidabile, push e sincrono** (non come il servizio di posta).
- Definisce la procedura di **trasparenza dei dati**, così che ci sia sempre il **delimitatore di fine email “\<CRLF>.\<CRLF>”**. <u>Ogni carattere che inserisco</u> nel messaggio (tipo caratteri speciali o sequenze come la precedente) <u>non influisce sul riconoscimento delle sequenze da parte del protocollo né invalida la mail</u>.

##### Fasi

SMTP è *connection oriented* e la comunicazione prevede queste fasi:

1) Apertura con handshake e identificazione del mittente (comando “HELO hostname”),
2) Identificazione mittente delle mail (comando “MAIL FROM”),
3) Identificazione destinatario delle mail (comando “RCPT TO”),
4) Invio di tutte le mail (comando “DATA”),
5) Invio di “\<CRLF>.\<CRLF>” per indicare la fine dei dati,
6) Chiusura della connessione (comando “QUIT”).

##### ESMTP

RFC 1869 e 2821 definiscono l’**ESMTP** (*Extended SMTP*) che permette l’uso di **tipi MIME** (supporto multimedialità). Quindi:

- Permessi <u>char diversi da US-ASCII a 7 bit</u>,
- Permessi ancora <u>più tipi di allegati</u>, non solo file di testo,
- Permesse <u>mail composte da più parti</u>.

Attenzione: i messaggi SMTP (pacchetti del protocollo, PDU) sono diversi dai messaggi di posta (email).

#### Formato delle email

RFC 822 definisce il <u>formato delle email</u> (come già detto solo a char ASCII 7 bit) che hanno svariati campi di header seguiti dal corpo del messaggio. I campi base di un’header sono:

- From: \<mittente> 
- To: \<destinatario> 
- Subject: \<oggetto>

### Lettura della posta

Servono dei protocolli ***pull*** per ricevere le email scaricandole dal mail server: **POP3** e **IMAP**.

##### POP3

(*Post Office Protocol 3*) prevede che le <u>email siano tutte inviate al client e memorizzate in locale, rimuovendole dalla mailbox</u> del mail server. Inoltre usa la porta 110, offre un servizio affidabile con TCP e richiede l’auth dell’utente.

##### IMAP

(*Internet Message Access Protocol*) <u>memorizza la posta nella mailbox del mail server</u> senza salvare nulla in locale ma garantendo l’<u>accesso alla posta d’ovunque</u>. Fornisce anche strumenti per la gestione della mailbox e usa la porta 143.

#### Webmail

Esistono <u>siti</u> che offrono un servizio di posta detto **webmail**. Il sistema è composto da:

- Un **server webmail**, che funge da interfaccia tra l’utente e il servizio di posta e usa SMTP + POP3/IMAP,
- Il **browser** col quale l’utente accede al servizio webmail usando HTTP o HTTPS.
