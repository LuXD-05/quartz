### Cos'è?

È definito dalla **RFC 1945** e dalla **RFC 2616**. È un protocollo implementato nei programmi:

- **Client HTTP**, dove l’HTTP implementa i messaggi request (richiesta),
- **Server HTTPd**, dove l’HTTP implementa i messaggi response (risposta).

##### Caratteristiche

- HTTP **usa TCP**,
- HTTP è ***stateless***, perché (il server web) non memorizza info (tipo sessione e cookie) del client e delle sue richieste,
- HTTP è ***pull-based***, perché è il client che richiede i dati al server (pagine web),
- HTTP è un protocollo ***in-band***, perché invia messaggi di controllo con connessione di trasferimento dati,
- HTTP è **creato per il trasferimento di pagine web** (ora usato per interfacciare l’utente ad app web, tipo social, giochi, e-commerce…),
- HTTP **non è sicuro**, manda tutto in chiaro (ma c’è HTTPS con SSL/TLS che ovvia al problema),
- L’app web è **client/server**; e il web server è installato nell’ISP, è sempre attivo, ha IP fisso e port 80 (well-known),
- HTTP permette **2** tipi di **connessioni**:
	- **Non persistenti**, uniche e possibili con **HTTP/1.0** (server HTTP chiude connessione ad ogni oggetto inviato),
	- **Persistenti**, con **HTTP/1.1** (server HTTP chiude la connessione dopo un certo periodo di inattività).

### Struttura dei messaggi HTTP

##### Richieste

Una **richiesta HTTP** è composta da: \[**metodo**\] \[**URI** della risorsa\] \[**versione** HTTP\]: “GET / HTTP/1.1”.

Usati i metodi **GET** e **POST** per ottenere la risorsa richiesta. “/” è l’URI della risorsa richiesta all’host. 

HTTP/1.1 indica che si sta usando la versione 1.1 del protocollo HTTP. Il resto sono linee di **header**, in forma: "\[campo\]: \[valore\]".

###### Campi dell’header

- ***Host*** = È il **nome di dominio** del **server** (virtuale) a cui è fatta la richiesta. Necessario per l’<u>hosting condiviso</u>, dove 1 pc hosta + domini, <u>per riconoscerli anche se il TCP usa solo l’IP del pc</u> (comune a tutti i siti del pc).
- ***User-Agent*** = Campo con **informazioni sul client** (di solito browser) che origina la richiesta.
- ***Referer*** = Contiene l’**URL** da cui è stata **generata la richiesta HTTP** (così server web sa da dove viene). 
- ***Accept*** = Campo che specifica i **tipi di contenuto** che il client **accetta** (interpreta) e i suoi valori sono detti ***media type*** o **tipi MIME** (*Multipurpose Internet Mail Extensions*). I tipi MIME più comuni sono:

| text/plain | text/html | text/xml | image/jpeg | application /xhtml+xml | multipart/form-data | application/octet-stream |
| :--------: | :-------: | :------: | :--------: | :--------------------: | :-----------------: | :----------------------: |
|   testo    | pag html  | doc xml  |  img jpg   |       doc xhtml        |     campi form      |       dati binari        |

L’header HTTP deve essere in US-ASCII a 7 bit, ma il campo MIME definisce la forma del contenuto del body.

- ***Accept*-...**:
	- ***Language*** = indica le **preferenze di lingua** usate (in ordine).
	- ***Encoding*** = indica le **tecniche di compressione** dati supportate.
	- ***Charset*** = indica le **codifiche dei caratteri** accettabili.
- ***Keep-Alive*** = Tempo in **millisecondi di durata** della **connessione**,
- ***Connection*** = Indica il **tipo di connessione** usata:
	- ***Keep-Alive*** (**persistente**, HTTP/1.1).
	- ***Close*** (**non persistente**, HTTP/1.0).

![](https://i.imgur.com/LNpGZqM.png)

##### Risposte

Una **risposta HTTP** è composta da: \[versione HTTP\] \[Status\] \[Desc\]: “HTTP/1.1 200 OK”.

Qui si usano gli ***status codes*** e le loro descrizioni. Tra i più frequenti ci sono:

- **200** = OK,
- **301** = Moved Permanently (URI cambiato),
- **304** = Not Modified,
- **400** = Bad Request,
- **401** = Unauthorized,
- **403** = Forbidden (manca il permesso per l'accesso),
- **404** = Not Found (errore di digitazione o, spesso, il server non ci vuole rivelare la vera ragione del rifiuto),
- **503** = Service Unavailable (carico eccessivo o manutenzione server).

###### Campi dell’header

- ***Date***: Data e ora di arrivo,
- ***Server***: Informazioni sul software in esecuzione sul server,
- ***Content-length***: Dimensione in byte dei dati allegati,
- ***Content-type***: Indica il tipo del contenuto.

![](https://i.imgur.com/xnZJyEq.png)

### Autenticazione

Molte app web limitano l’accesso a utenti autorizzati. Una tecnica è l’***HTTP Basic*** (**auth** integrato in **HTTP**).

1) Un client richiede una risorsa che necessita di auth e il server risponde con un *401 Unauthorized*, con campo:
