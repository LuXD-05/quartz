# Web e HTTP

### Server web

Il server web è un’**applicazione in esecuzione su un** pc **server** ch**e fornisce contenuti web** richiesti, è chiamato anche **Daemon HTTP** o **HTTPd**. Questo è costantemente in attesa di richieste da client, e se arriva una, cerca di evaderla il più velocemente possibile cercando e restituendo il file richiesto se trovato. In ambienti Unix/Linux il Daemon si può **duplicare** con la fork(), mandando il figlio a gestire una determinata richiesta e poi muore.

### HTTP

(Le app web lavorano con il protocollo **HTTP**, che stabilisce le regole di comunicazione tra client e server. Questo trasmette i dati in formato testuale (ASCII) con i protocolli IP (liv 3) e TCP (liv 4), il cui compito è di instaurare e mantenere la comunicazione.)

La comunicazione inizia con una richiesta di connessione **TCP** con **porta 80** (o **443** se **HTTPS**).

**URI** (Uniform Resource Identifier)

**Identifica univocamente una risorsa** tramite uno schema universale e una sintassi generica.

**URL** (Uniform Resource Locator)

(Sottoinsieme di URI) **identifica univocamente l’indirizzo web di una risorsa**, tipo pagina HTML. Metaforicamente una stringa URL risponde alle domande: “***Come**?*”, “***A*chi****?*”, “***Che cosa****?*” così:

1) **Protocollo** usato per la richiesta (*Come?*)
2) **Host** a cui fare la richiesta (*A chi?*)
3) **File** richiesto (*Che cosa?*)

Forma: \[**protocollo**\]://\[**host**\]/\[**file**\]: \http://www.gildown.it/interroghiamo.html

HTTP Requests

Fatte per **accedere a una risorsa identificata da un URI presente su un server** in Internet. Sono **stringhe ASCII** così:

![[Pasted image 20240304163221.png]]

**Metodo**: GET, POST… + **Versione HTTP** + **Metainformazioni** con **valori** + **body**.

HTTP Responses

Anche queste consistono di stringhe di testo ASCII:

![[Pasted image 20240304163342.png]]

**Versione HTTP** + **status code** + **descrizione status code** + **Metainformazioni** con **valori** + **body**.

Status Code

- **200** – **299** = **Success**,
- **300** – **399** = **Redirect**,
- **400** – **499** = **Client Error**,
- **500** – **599** = **Server Error**.

Passaggio di parametri

Client passa parametri al server nell’URL con il protocollo HTTP, in formato: \[**URL**\]?\[**NomePar**\]=\[**ValorePar**\]&…

GET

**Invia dati in formato ASCII aggiungendo i parametri all’URL** come suddetto. Si può fare digitando i parametri giusti nell’URL oppure compilando un form e facendo submit (così appaiono in automatico).

Col GET il server assegna i parametri dopo il “?” a una variabile chiamata **QUERY_STRING**, poi il **GET non passa body** e la stringa è visibile e ha una **lunghezza max** di **2048 char**.

POST

I parametri sono passati col body della richiesta, quindi non visibili nell’URL e senza limiti.

Caratteristiche

- **HTTP non ha memoria** (*stateless*), perché le **richieste sono uniche per il server** e **non salvano dati di navigazione** (risolto con **sessione** e **cookies**),
- **HTTP è asimmetrico** (*pull-based*), ovvero **solo il client chiama il server,**
- **HTTP è nato per trasmettere pagine web**,
- **HTTP non è sicuro**, ma **HTTPS** usa **SSL** (Secure Socket Layer) che **crittografa** e **protegge** i **dati** tra client e server.
