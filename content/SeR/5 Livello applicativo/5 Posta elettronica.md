### Cos'è?

L’email è un sistema di comunicazione asincrono: l’utente invia e riceve messaggi senza sincronizzarsi con altri.

Il sistema di email presenta 3 componenti principali:

##### MUA (Mail User Agent)

Sono dei programmi che interfacciano l’utente con il sistema di posta (tipo Outlook, Gmail…). I MUA eseguono SMPT client per contattare SMTP server sul mail server in uso dall’utente.

##### Mail servers

Server di posta, sono il nucleo dell’infrastruttura del servizio e: ricevono le email da consegnare, le inoltrano a destinazione, hanno delle mailbox (deposito email ricevute) e delle message queue (code di email in transito) (tipo Exchange, Exim e Sendmail).

Eseguono il protocollo SMTP:

- SMTP server per rispondere a SMTP client del MUA utente.
- SMTP client per contattare il mail server destinatario di 1 mail.

##### Protocollo SMTP (Simple Mail Transfer Protocol)

È un protocollo push (di invio) che definisce le regole di invio del messaggio da un client a un mail server.

![](https://i.imgur.com/DZFU2P0.png)

### Uso

1) Il Mail User Agent del client invia l’email al mail server del mittente, proseguendo poi in internet.
2) L’email arriva al mail server destinatario (recipient mail server per la mailbox) che la salva nella mailbox del destinatario. 

Se il mail server mittente non riesce a consegnare la mail al mail server destinatario, la trattiene nella sua message queue e, periodicamente, riprova a trasferirla. Dopo un n° di tentativi falliti, email rimossa e notificato il fallimento.

### SMTP

Protocollo definito nella RFC 821 del 1982. Caratteristiche:

- I messaggi (pacchetti a livello applicativo) devono essere in US-ASCII a 7 bit,
- Sono usate connessioni TCP permanenti (+ messaggi trasferibili tra 2 mail server in 1 connessione),
- Usa la porta 25. È un protocollo full-duplex, stateful, in-band, affidabile, push e sincrono (non come il servizio di posta).
- Definisce la procedura di trasparenza dei dati, così che ci sia sempre il delimitatore di fine email “\<CRLF>.\<CRLF>”. Ogni carattere che inserisco nel messaggio (tipo caratteri speciali o sequenze come la precedente) non influisce sul riconoscimento delle sequenze da parte del protocollo né invalida la mail.

##### Fasi

SMTP è orientato alla connessione e la comunicazione prevede queste fasi:

1) Apertura con handshake e identificazione del mittente (comando “HELO hostname”),
2) Identificazione mittente delle mail (comando “MAIL FROM”),
3) Identificazione destinatario delle mail (comando “RCPT TO”),
4) Invio di tutte le mail (comando “DATA”),
5) Invio di “\<CRLF>.\<CRLF>” per indicare la fine dei dati,
6) Chiusura della connessione (comando “QUIT”).

RFC 1869 e 2821 definiscono l’ESMTP (Extended SMTP) che permette l’uso di tipi MIME (supporto multimedialità). Quindi:

- Permessi char diversi da US-ASCII a 7 bit,
- Permessi ancora più tipi di allegati, non solo file di testo,
- Permesse mail composte da più parti.

Attenzione: i messaggi SMTP (pacchetti del protocollo, PDU) sono diversi dai messaggi di posta (email).

#### Formato delle email

RFC 822 definisce il formato delle email (come già detto solo a char ASCII 7 bit) che hanno svariati campi di intestazione seguiti dal corpo del messaggio. I campi base di un’intestazione sono:

From: \<mittente> 

To: \<destinatario> 

Subject: \<oggetto>

### Lettura della posta

Servono dei protocolli pull per ricevere le email scaricandole dal mail server. Questi sono: POP3 e IMAP.

##### POP3

Prevede che le email siano tutte inviate al client e memorizzate in locale, rimuovendole dalla mailbox del mail server. Inoltre Post Office Protocol usa la porta 110, offre un servizio affidabile con TCP e richiede l’auth dell’utente.

##### IMAP

Internet Message Access Protocol memorizza la posta nella mailbox del mail server senza salvare nulla in locale ma garantendo l’accesso alla posta d’ovunque. Fornisce anche strumenti per la gestione della mailbox e usa la porta 143.

### Webmail

Esistono siti che offrono un servizio di posta detto webmail. Il sistema è composto da:

- Un server webmail, che funge da interfaccia tra l’utente e il servizio di posta e usa SMTP + POP3/IMAP,
- Il browser col quale l’utente accede al servizio webmail usando HTTP o HTTPS.
