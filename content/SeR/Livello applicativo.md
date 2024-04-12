---
public: true
edited_seconds: 11350
modified_at: 11/04/2024 21:59:53
---
# Fondamenti
### Il livello applicativo
Il livello applicativo riguarda le applicazioni di rete, progettate con architetture client/server o P2P.
I processi applicativi inviano messaggi in rete e li ricevono da essa attraverso un socket, un’interfaccia software tra il livello applicativo e il livello trasporto all’interno di un host (mezzo usato da app per richiedere l’uso di 1 protocollo liv. trasporto).
### Sevizi necessari
Alle app sono offerti dei servizi a livello trasporto, con **TCP** (affidabile) e **UDP** (inaffidabile). Questi però non garantiscono:
- **Throughput alto**: frequenza con cui un processo invia bit al ricevente (app sensibili a throughput = sensibili alla banda). 
- **Temporizzazione**: molte app tollerano ritardi end-to-end solo nell’ordine di decimi di secondo. 
- **Sicurezza**: potrebbe essere necessario rendere i dati riservati con crittografia end-to-end.
### SSL/TLS
Riservatezza, auth e integrità dei dati sono critiche per molte app, quindi per garantirle si usa un protocollo appena sopra il TCP: l'SSL/TLS (*Secure Socket Layer / Transport Layer Security*). (HTTPS = TCP + SSL/TLS).
### Web
Una app web è una **app** che permette la **navigazione tra pagine web**. È composta da:
- **Web server**: o **HTTPd** (*HTTP Daemon*), è il programma **HTTP server** (tipo Apache o IIS), 
- **Web browser**: (tipo Chrome, Safari, Opera, Firefox…),
- **HTTP**: (*HyperText Transfer Protocol*), è il programma **HTTP client**.
# HTTP
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
- ***Accept*** = Campo che specifica i **tipi di contenuto** che il client **accetta** (interpreta) e i suoi valori sono detti ***media type*** o **tipi MIME** (*Multipurpose Internet Mail Extensions*). I tipi MIME più comuni sono: (in tab)

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
   "**WWW-Authenticate: \<type> realm = \<realm>**", dove:
   - "**type**" = tipo di tecnica (in questo caso Basic)
   - "**realm**" = descrive l’area protetta da auth.
2) Il browser client esegue la ***challenge***, ovvero fa visualizzare la pagina per l’immissione di credenziali e queste, se inserite, vengono inoltrate al server con un messaggio simile all’originale ma con l’aggiunta del campo:
   “**Authorization: Basic {YWxleDpwaXBwbw\==}**”, dove
   - La **stringa tra {...}** = username e password codificati (<u>non</u> crittografati) in *base64* (ASCII 7 bit per HTTP).
3) Il server riceve i dati, verifica l’auth e invia la pagina richiesta se credenziali valide. Nelle richieste successive il browser invia direttamente l’header ***Authorization*** senza intervento dell’utente.
### Caching
Client e server mantengono una ***cache*** dei dati recenti, per evitare richieste superflue per ottenere dati già ottenuti. Si trovano anche *cache* addizionali nella rete nel percorso tra client e server (tipo nei ***proxy***). 
HTTP/1.1 fornisce delle funzioni per il controllo della cache tramite il campo “**Cache-Control**”, che può assumere diversi valori (nelle risposte):
- ***no-store***: <u>impedisce al client destinatario di salvare in cache</u> il messaggio (però lo può salvare in memoria),
- ***no-cache***: il messaggio è <u>salvabile in cache</u>, ma il client è forzato a <u>convalidarlo</u> col server per ogni richiesta futura,
- ***public***: consente anche ai **proxy** nel percorso tra C/S il <u>salvataggio</u> del body del messaggio <u>in cache</u>,
- ***private***: consente il <u>salvataggio in cache</u> del messaggio solo al <u>destinatario</u>,
- ***max-age***: definisce il <u>tempo massimo di permanenza in cache</u> del messaggio.
Con il campo ***"If-Modified-Since"*** è possibile fare una <u>richiesta condizionata di una pagina</u> solo se ha subito <u>modifiche dopo una certa data</u>. In caso di nessuna modifica dalla data specificata, il server risponde con *"304 Not modified"*. 
(Per verificare ciò si usa il campo *Last-Modified* dei messaggi di risposta a una richiesta fatta a una risorsa).
### Cookies
HTTP è **stateless**, ma a volte serve mantenere delle informazioni relative all’utente per la navigazione. Soluzioni:
- **Sessioni**: informazioni di navigazione salvate e gestite dal server,
- **Campi hidden**: informazioni immagazzinate in campi di form nascosti,
- **Cookie**: informazioni di navigazione salvate e gestite dal client (a differenza degli altri, supportati da HTTP).
##### Uso
I cookie sono usati per 3 funzionalità:
- Gestione sessione: login, carrello, punteggi o cose che server ricorda (o x dire se 2 richieste vengono da stesso browser),
- Personalizzazione: user preferences, temi e altre impostazioni,
- Tracciamento: registrazione e analisi di comportamenti dell’utente.
##### Funzionamento
L’uso dei cookie prevede 4 componenti:
- Cookie: campo header nei messaggi di richiesta,
- Set-cookie: campo header nei messaggi di risposta,
- Un file temporaneo nel file system del client e gestito da browser,
- (db sul web server / sito, facoltativo).
###### Step
1) Il browser accede a un sito e manda una richiesta al suo web server,
2) Il server crea un identificativo univoco che invia al client con una risposta avente:
   “Set-Cookie: \<cookie>=\<value>”, 
   dove \<cookie> è il nome del cookie dato dal server, mentre \<value> è il datetime in cui è creato (ma sempre?). 
![](https://i.imgur.com/673BORY.png)
3) Da adesso in poi il valore del cookie è incluso in tutte le richieste nel campo “Cookie: …”.
##### Tipi di cookie
I cookie possono essere:
- **Di sessione**: <u>cancellati quando il client termina / browser si chiude</u> (non specificati *Expires* o *Max-Age*),
- **Permanenti**: <u>salvati nel client e scadono</u> ad un certo datetime (Expires) o dopo un certo tempo (Max-Age).
##### Sicurezza
I cookie non sono sicuri, quindi info riservate o sensibili non vanno mai archiviate o trasmesse con cookie HTTP, anche perché il furto di cookie può comportare il dirottamento di una sessione dell’utente autenticato. I metodi di furto più comuni sono la social engineering e lo sfruttamento di vulnerabilità per XSS (Cross-Site Scripting).
Una volta i cookie erano salvati solo nello storage del client, perché era l’unico modo, mentre ora è consigliato usare delle Web storage API (API di salvataggio), dato che i cookie sono inviati ad ogni richiesta riducendo le performance.
##### Direttiva UE cookie
La direttiva 2009/136/EC del parlamento europeo in vigore dal 25/05/2011 sancisce (non impone) i requisiti per i cookie in tutti gli stati dell’UE. In breve indica che prima di memorizzare qualsiasi cookie, l’utente deve darne il consenso esplicito, questo perché i cookie possono essere considerati una violazione della privacy degli utenti; e tramite una combo di essi ed info date dall’utente, un sito può apprendere molto sul suo conto e vendere ciò a terzi.
# FTP
### Cos'è?
L’**FTP** (*File Transfer Protocol*) permette il **trasferimento di file** tra host su una rete senza bisogno di loggarsi o saper usare il sistema remoto destinatario, dando l’accesso a file system remoti con comandi molto semplici. È un servizio <u>client/server</u>, i cui trasferimenti di file sono <u>sia in download che in upload</u>. Utenti client interfacciati col servizio con ***FTP User Agent***.
FTP prevede il **controllo degli accessi** per chi accede a files, per mezzo di una **auth** (username e password) **non cifrata**, per questo è un protocollo <u>non sicuro</u> (al contrario di **SFTP**); ed è il **server FTP** che verifica i privilegi di accesso.
FTP usa TCP (come HTTP), però usa <u>2 connessioni TCP separate</u>:
- **Connessione di controllo**: per l’invio di <u>info di controllo</u> tra gli host (per auth e comandi),
- **Connessione dati**: per il <u>trasferimento di file</u>.
Per questo si dice che **FTP** è ***out-of-band***, al contrario di **HTTP**, che invece invia le <u>info di controllo negli header</u> dei messaggi e usa una <u>connessione unica</u> (***in-band***).
### Modalità
L’FTP ha **2 modalità** di funzionamento:
##### Modalità attiva
All’apertura della porta di comando (client), il client dice al server di voler usare la **modalità attiva** inviandogli un **n° di porta non privilegiata e casuale** (> 1024) **aperta** sullo stesso. Il <u>server</u> apre quindi 2 collegamenti:
- Tra la porta **well-known 20** e l’**IP del server**,
- Tra **porta** specificata dal **client** e l’**IP del client**.
In modalità attiva:
- La **connessione di controllo** è aperta dall’**FTP client**,
- La **connessione dati** è aperta dall’**FTP server**.
Il client deve essere abilitato ad accettare collegamenti tramite qualsiasi porta > 1024; ma i **firewall** impediscono spesso le connessioni in entrata dai server FTP, per cui è stata definita la **modalità passiva**.
##### Modalità passiva
All’apertura della porta di comando (client), il client richiede di voler usare la **modalità passiva**, quindi il <u>server gli fornisce</u> un **n° di porta non privilegiata e casuale** (> 1024) **aperta** sullo stesso. Il <u>client</u> apre quindi 2 collegamenti:
- Tra la **porta** specificata dal **server** e l’**IP del server**,
- Tra una **porta non privilegiata casuale** e l’**IP del client**.
In modalità passiva
- La **connessione di controllo** è aperta dall’**FTP client**,
- La **connessione dati** è aperta dall’**FTP client**.
Con la modalità passiva viene limitato il range delle porte non privilegiate del server FTP, riducendo le porte aperte sul server e semplificando la creazione delle regole del firewall per il server. 
##### Per entrambe le modalità
La **connessione dati** <u>non è persistente</u>, è aperta e chiusa per ogni trasferimento di file.
La **connessione di controllo** <u>è persistente</u>, ovvero mantenuta attiva per tutta la sessione di trasferimento dei file; inoltre è anche ***stateful***, mantiene gli stati, perché il server deve associarla con un utente specifico e la sua directory.
Il salvataggio di informazioni comporta l’uso di RAM, quindi <u>a parità di risorse</u>, un <u>server FTP può mantenere in contemporanea molte meno connessioni rispetto ad un server HTTP</u>.
# Remote desktop 
### Cos'è?
Protocollo che permette a un client (locale) di funzionare come terminale di un pc remoto server.
- Tutto ciò che è fatto dal client viene inviato al server, che lo interpreta come se fosse stato fatto su di sé,
- Tutto ciò che il server mostra in output (allo schermo), è trasmesso al client via internet e questo lo visualizza.
Il pc server usa la console del client per l’I/O, quindi ciò che il client scrive in console è interpretato e eseguito su server.
### Telnet
È un protocollo client/server basato su TCP (server port 23) e il nome del prog che avvia sessioni con l’host remoto. Per la progettazione del protocollo e la sua flessibilità, con programmi Telnet è possibile stabilire connessioni a altri servizi internet, come SMTP (port 25) o HTTP (port 80). 
Telnet è insicuro, quindi di default è disabilitato sui server in rete (anche su windows) e i dati sono trasmessi in chiaro.
### PuTTY
PuTTY è un programma client per remote desktop per OS windows e implementa protocolli client, tipo Telnet e SSH.
### SSH
SSH (Secure Shell) dà agli amministratori di rete un modo sicuro per accedere a un host remoto. Usa la porta 22.
È molto usato per: gestione remota di sistemi e app, accedere ad host in rete, eseguire comandi e spostare file tra pc… 
Se serve, SSH usa la crittografia a chiave pubblica per autenticare l’host remoto e consentirgli di autenticare l’utente (ovviamente tutti i dati di auth, i comandi, l’output e i file trasferiti sono crittati).
# Posta elettronica
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
# DNS
### Scopo
Il **DNS** (*Domain Name System*) da la possibilità agli utenti in internet di riferirsi alle risorse (siti, caselle di posta, servizi cloud su una macchina avente IP) attraverso nomi mnemonici e non tramite i loro indirizzi IP.
Per fare questo è stata predisposta una rubrica (*directory*) che associa i nomi mnemonici (detti **nomi di dominio**) ai corrispondenti IP. Questa è implementata con un database distribuito si vari pc detti ***name server***, i quali eseguono un programma server che risponde alle richieste di risoluzione dei nomi.
DNS quindi realizza il servizio di directory di internet. Si risolve un nome di dominio in un IP quando un utente cerca di accedere a un sito, in quanto, usando HTTP o HTTPS, la connessione (socket) che si deve creare con il server web necessita del suo IP.
## Componenti
Il DNS riguarda vari componenti e processi:
### 1) Richiesta della risoluzione
##### Step
1) Viene mandata una richiesta di risoluzione di un nome di dominio da una applicazione (tipo browser) al ***Resolver*** (software DNS client e punto di accesso al DNS system) fornito dall'OS. 
2) Il *Resolver* fa la richiesta al ***Recursor*** (o DNS server locale), il quale avvia il processo di ricerca dell'IP corrispondente al nome. L'informazione, se trovata, viene rimandata al *Resolver* come risposta alla richiesta, altrimenti questo riceverà un codice di errore.
##### Altro
Ogni host deve essere configurato con l'IP del default DNS server locale (manualmente in modo statico o col DHCP in modo dinamico, come per il *default gateway*).
I ***Recursor*** sono ridondati per rendere il sistema + robusto/disponibile; infatti ci sono sempre un ***name server*** primario e uno secondario, i cui IP sono solitamente forniti dall'ISP.
Esistono però dei DNS server locali alternativi a quelli dell'ISP, tipo:
- Google: 8.8.8.8 (primario) e 8.8.4.4 (secondario).
- Cloudflare: 1.1.1.1 (primario) e 1.0.0.1 (secondario). (Logga solo per 24 ore e ha RTT bassi).
Ci sono varie ragioni per scegliere il *Recursor* di Cloudflare (rispetto a quello dell'ISP):
###### Sicurezza
- Non tutti gli ISP usano tecniche di cifratura forte o supportano il protocollo [[#DNSSEC]] sui loro *name server*; per questo (le query di) molti utenti sono esposti ad attacchi tipo *[[TePI#Attività di hacking|man-in-the-middle]]*.
###### Prestazioni
- Spesso gli ISP usano i record DNS per tracciare le attività e i comportamenti degli utenti.
- La velocità dei *Recursor* degli ISP può non essere molto alta.
- Gli ISP possono eseguire politiche di filtraggio per certi siti bloccandone la risoluzione dei nomi.
### 2) Ricerca della soluzione
Il *Recursor* inizia la ricerca degli IP interrogando i *name server* aventi il db distribuito. Ci sono 3 tipi di *name server*:
![](https://i.imgur.com/Lv0WA1k.png)
##### Root
Il ***Root name server*** è il 1° *name server* cui si rivolge il *Recursor* per risolvere un nome (ogni *Recursor* deve conoscere tutti i *root name server*). Questo accetta le query del Recursor e risponde indirizzandolo verso il *TLD name server*.
Risposta: RR NS.
##### TLD
Un ***Top Level Domain name server*** memorizza i dati per tutti i nomi che condividono un dominio *top level* (tipo ".com"). Un *TLD name server* può essere ***authoritative*** per 1 o + nomi di dominio e può non esserlo per altri.
##### Authoritative
> [!important] Authoritative
> Un *name server* è ***authoritative*** (autorevole) per un nome di dominio se questo è registrato presso di lui (quindi se nel suo db è presente l'IP ("RR A" o "AAAA") per quel nome + le altre info necessarie alla registrazione).

Un ***Authoritative name server*** amministra (possiede (nel db)) i dati di un nome di dominio, quindi è detto *authoritative* solo per i nomi che gestisce.
### 3) Gerarchia dei nomi di dominio
I nomi di dominio hanno una struttura gerarchica ad albero che rispecchia la gerarchia dei *name server*:
![](https://i.imgur.com/VATKQKO.png)
Un nome di dominio è costituito da tutte le parole della gerarchia collegate con un ".". Ogni parola (parte) del nome di dominio è detta ***label*** e può essere di max 63 byte; inoltre:
- Ad un certo livello della gerarchia, non ci potranno essere 2 etichette uguali.
- C'è sempre una **label riservata** *null* di lunghezza 0, usata per la ***root***.
###### Esempio
Prendiamo il nome di dominio "example.com." (in foto). Per leggere i livelli si fa da destra a sinistra e:
1) "**.**": è il 1° e + alto livello (***root***),
2) "**com**": è il livello **TLD**,
3) "**example**": è il livello **SLD**.
Un nome di dominio che presenta anche il "." finale di *root* è detto ***fully qualified domain name***. La gerarchia dei nomi costituisce il ***namespace***. I dati per risolvere i nomi sono memorizzati nella **gerarchia di *name server***.
##### Zona e Zone file
> [!important] Zona
> Insieme dei dati relativi sotto una certa amministrazione

Le **zone** sono salvate in dei file di testo detti ***zone file***. Una zona può riguardare 1 o + domini e sottodomini:
![](https://i.imgur.com/L29pxu2.png)
##### Root zone
I dati della ***root zone*** sono gestiti dai ***root name server*** e sono salvati nel ***[root zone file](https://www.internic.net/domain/root.zone)***. 
Ci sono 13 IP diversi riservati per i *root name server* (per i limiti dell'architettura DNS originale) e ognuno è associato a vari *name server* ridondati ([root-servers.org](https://root-servers.org/), 1757 distribuiti nel mondo) i quali usano l'***anycast routing***.
L'***anycast routing*** permette di assegnare a + pc lo **stesso IP**, così da **distribuire** le richieste in base al **carico** e alla **vicinanza**, fornendo un servizio **uniforme** su vaste aree geografiche. Per questo e la **ridondanza**, i *root name server* sono molto affidabili.
I 13 IP sono gestiti da varie organizzazioni e sono etichettati da una lettera dalla **A** alla **M**.
![](https://i.imgur.com/Lt2lo50.png)
Dato che i *root name server* sono in cima alla gerarchia dei *name server*, i loro IP non possono essere risolti tramite DNS; quindi ogni *Recursor* contiene implementati nel sw, i 13 IP.
##### Albero dei nomi di dominio
I nomi di dominio sono organizzati in una struttura ad albero:
1) Dominio di **root** ("**.**" = null)
2) **TLD** (*Top Level Domains*, tipo ".com", ".it"...), domini di 1° livello, a loro volta suddivisi in:
   - **Nazionali** o **ccTLD** (*country-code TLD*), usati da stati o territori e costituiti da 2 lettere (it, eu...),
   - **Generici** o **gTLD** (*generic TLD*), usati da particolari classi di organizzazioni e fatti da 3 o + lettere.
     La > parte dei gTLD sono disponibili in tutto il mondo, ma .gov, .mil e .edu sono riservati a governo, militari ed enti educativi statunitensi.
3) **SLD** (*Second Level Domains*), domini di 2° livello e corrispondenti ad aziende, enti e persone.
4) ***Subdomains*** (sottodomini), nomi definiti sotto un dominio SLD (tipo "**mail**.google.com").
Oltre al *namespace* pubblico, un'azienda può definire un *namespace* privato per i domini locali dell'azienda, così di rendere identificabili i server interni con nomi e non con IP.
##### Zone file e name server primario e secondario
I dati di una zona sono usati da **1** *name server* primario <u>e</u> da **almeno 1** *name server* secondario:
- Il *name server* **primario** gestisce i dati (**RR *authoritative***) di dominio o i domini della zona controllata. I dati sono salvati in uno *zone file* nel file system locale. **Modifiche** a record DNS di una zona possono essere fatte solo sul **server primario** della stessa (*zone file* in lettura/scrittura).
- I *name server* **secondari** lavorano sui dati acquisiti dal primario tramite una procedura automatica detta ***zone-transfer*** (DNS port 53 TCP), dove lo *zone file* è una copia *readonly*. I *name server* secondari forniscono **ridondanza** aumentando la **robustezza** del sistema e, grazie al ***load balancing***, aumentano la **disponibilità del servizio**.
##### Zone file e dati DNS - RR
I dati DNS sono organizzati in **RR** (***Resource Record***), contenuti negli *zone file* e forniscono info riguardo a un certo dominio. Ogni RR contiene dati formattati secondo le regole dell'RFC 1035.
Struttura generale di un RR: \[Name] \[TTL] \[Class] \[Type] \[Resource data] $\;\rightarrow\;$ "google.com. 300 IN A 74.125.131.138". Campi:
- **Name**: nome di cui l'RR fornisce info,
- **TTL**: per quanti secondi l'info può restare in cache,
- **Class**: in internet è sempre "IN",
- **Type**: tipo di RR fornito, a sua volta (per capirne le funzioni: [[#5) Servizi aggiuntivi|link]]):
	- **A** (*IPv4*): record con in "Resource data" l'IPv4 corrispondente a "Name";
	- **AAAA** (*IPv6*): record con in "Resource data" l'IPv6 corrispondente a "Name";
	- **CNAME** (*Canonical name*): in "Resource data" vi è il nome ***vero*** (<u>canonico</u>) del nome (<u>alias</u>) in "Name" (per arrivare all'IP risolvere il nome canonico);
	- **MX** (*Mail eXchange*): in "Resource data" vi è il **nome** del **mail server** associato a "Name";
	- **NS** (*Name Server*): da il ***referral*** (riferimento) a un ***authoritative name server*** ("Resource data" quindi contiene il nome del prossimo *name server* di livello inferiore da contattare);
- **Resource data** (*RDATA*): è il valore dell'info fornita (dipende da Type). 
##### Esempi di "Type"
###### A
Fornisce l'**IPv4 cercato**. Solitamente i siti hanno <u>1 solo record A</u>, ma alcuni ne hanno di + siccome il sito è <u>replicato su + web server</u>; questo al fine di usare il ***load balancing*** di DNS, che (in ***round-robin***) fa ruotare gli RR e usa il 1° in lista.
###### AAAA
Fornisce l'**IPv6 cercato** (resto come "A").
###### CNAME
Fornisce il **nome canonico** di un ***alias*** (<u>non contiene un IP</u>, ma **un altro nome da risolvere**). Il nome canonico è fornito quando un dominio è un *alias* di un altro, ovvero è un nome pubblico diverso da quello privato interno ad un'azienda.
###### MX
Questo permette di risolvere un nome di dominio di un *mail server*. (Come "CNAME") un record MX <u>non contiene un IP</u>, ma il nome del ***mail server*** da **risolvere**.
###### NS
Fornisce il nome di un ***authoritative name server*** per un certo nome di dominio. <u>Non contiene IP</u>, bensì i nomi dei ***name server*** contenenti **RR** per i **nomi di dominio** con quell'**estensione**.
Un dominio di solito ha **+ record NS**: **1** per il *name server* **primario** e **almeno 1** per il **secondario**. <u>Senza NS configurati correttamente</u>, una <u>risorsa sarà irraggiungibile</u>.
I **record NS** sono dati da un *name server* di livello superiore (**root** o **TLD**) per raggiungere, prima o poi, l'*authoritative name server* per il nome cercato. Questi record sono detti ***referral*** perché sono un rinvio ad un altro nome.
### 4) Risoluzione
##### Tipi di query
Un nome di dominio viene risolto accedendo ai dati (RR) del db distribuito per mezzo di ***query*** (interrogazioni), che in DNS possono essere di 2 tipi:
![](https://i.imgur.com/DYPVm2h.png)
###### Ricorsive
- A una richiesta, si ha in risposta:
	- O la soluzione (l'indirizzo IP: "*A*" o "*AAAA*"),
	- O un errore.
- Sono fatte dal ***Resolver*** al ***Recursor***.
###### Iterative
- A una richiesta si ha in risposta:
	- O la soluzione (l'indirizzo IP: "*A*" o "*AAAA*"), 
	- O un suggerimento per ottenerla (*referral* NS al *name server* successivo).
- Sono fatte dal ***Recursor*** a un ***name server***.
##### Query e protocollo di trasporto
Il protocollo DNS usa (in **porta 53**):
- **UDP** per payload **< 512** byte, quindi, per le **query di risoluzione** dei nomi.
- **TCP** per payload **> 512** byte, quindi, per trasferire ***zone files*** (tra server primari e secondari).
##### Query e caching
Il processo di risoluzione di un nome di dominio in IP prevede vari passi e quindi molto tempo. Per <u>limitare i tempi di risposta</u> (velocizzarlo), il DNS prevede un sistema di ***caching* delle risposte alle query**.
**Scopo**: memorizzazione <u>temporanea</u> dei dati, per migliorare le prestazioni della ricerca DNS. 
Il ***caching*** è fatto <u>il + vicino possibile a chi fa le richieste</u>, per limitare il n° di query necessarie alla risoluzione di un nome. I record in *cache* sono mantenuti per un certo tempo (**TTL**).
Il salvataggio in cache dei RR può avvenire:
- Nei browser,
- Nei *Resolver* (OS),
- Nei *Recursor*,
- Nei *name server* della gerarchia.
### 5) Servizi aggiuntivi
Tramite le info nei RR e le query, il DNS offre:
- ***DNS Lookup***: (o risoluzione dei nomi di dominio) con i record "**A**" e "**AAAA**".
- ***Host aliasing***: differenziazione tra il nome pubblico e quello privato interno all'organizzazione tramite i record "**CNAME**".
- ***Mail server aliasing***: (come gli host ma) uso dello stesso nome sia per *web server* che per *mail server* tramite i record "**MX**".
- "***Load balancing***": tramite la tecnica ***round-robin*** usata nella distribuzione delle query tra il server primario e i secondari.
### 6) Registrare nomi di dominio
Per pubblicare un sito serve scegliere un **nome di dominio** e un **TLD**. Ci sono delle parti che hanno un ruolo nel processo di pubblicazione di un sito:
##### Registrant
<u>Entità</u> (individuo, azienda...) a cui <u>serve un certo nome di dominio</u> per un servizio. 
Quando un ***Registrant*** registra un dominio, esso diventa **proprietario del diritto di usare il nome**, <u>non del nome in sé</u>. Inoltre la registrazione ha una **durata definita** ma **rinnovabile**.
Per registrare un nome di dominio, il *Registrant* si dovrà rivolgere al ***Registrar***, il quale si occuperà del **TLD** scelto.
##### Registrar
<u>Azienda</u>, accreditata dalla **ICANN** (*Internet Corporation for Assigned Names & Numbers*), che 1) <u>"vende" nomi di dominio</u> e 2) <u>raccoglie e invia le info di registrazione ad un ***Registry***</u>.
I *Registrar* registrano i TLD; alcuni si occupano dei **gTLD** e altri dei **ccTLD**. 
##### Registry
(O ***Registry Operator***) è un'<u>organizzazione che amministra i TLD di una zona</u>. Riceve dai *Registrar* dei **RR** (info) di un nome e **aggiorna** con essi lo ***zone file***.
**Obiettivo**: mantenere funzionante l'infrastruttira (*name server* + db) che rende possibile il *DNS Lookup*.
## DNSSEC
### Esempio
##### Problema
Quando si accede a un sito, il *Recursor* dell'ISP interrogherà tutti i livelli della gerarchia dei DNS *name server* (dal *Root name server* all'*authoritative name server* per quel sito) ottenendo infine l'IP.
Gli hacker potrebbero eseguire del ***cache poisoning***, ovvero modificare dei dati (RR authoritative o in cache) inserendo dei valori falsi e far risolvere il nome di dominio con un IP che porta ad un altro sito web invece che all'originale.
##### Soluzione
**DNSSEC** (*DNS Secure*) protegge il DNS basandosi su delle ***signatures* crittografate** (firme), con cui si firmano i record negli *authoritative name server*.
Come <u>HTTPS cifra il traffico</u>, <u>DNSSEC firma gli RR</u> cosicché i falsi siano rilevabili.