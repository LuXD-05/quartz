---
public: true
edited_seconds: 10
modified_at: 02/04/2024 11:16:51
---
# Fondamenti
Il livello applicativo riguarda le applicazioni di rete, progettate con architetture client/server o P2P.
I processi applicativi inviano messaggi in rete e li ricevono da essa attraverso un socket, un’interfaccia software tra il livello applicativo e il livello trasporto all’interno di un host (mezzo usato da app per richiedere l’uso di 1 protocollo liv. trasporto).
### Sevizi necessari
Alle app sono offerti dei servizi a livello trasporto, con TCP (affidabile) e UDP (inaffidabile). Questi però non garantiscono:
-	Throughput (alto) --> frequenza con cui un processo invia bit al ricevente (app sensibili a throughput = sensibili alla banda).
-	Temporizzazione --> molte app tollerano ritardi end-to-end solo nell’ordine di decimi di secondo.
-	Sicurezza --> potrebbe essere necessario rendere i dati riservati con crittografia end-to-end.
### SSL/TLS
Riservatezza, auth e integrità dei dati sono ora critiche per molte app di rete, quindi per garantirle si usa un protocollo appena sopra (liv. app) il TCP: il SSL/TLS (Secure Socket Layer / Transport Layer Security). (HTTPS = TCP + SSL/TLS).
### Web
Una app web è una app che permette la navigazione tra pagine web. È composta da:
-	Web server --> o HTTPd (HTTP Daemon), è il programma HTTP server (tipo Apache o IIS),
-	Web browser --> (tipo Chrome, Safari, Opera, Firefox…),
-	HTTP --> HyperText Transfer Protocol, è il programma HTTP client.
# HTTP
È definito dalla RFC 1945 e dalla RFC 2616. È un protocollo implementato nei programmi:
- Client HTTP, dove l’HTTP implementa i messaggi request (richiesta),
- Server HTTPd, dove l’HTTP implementa i messaggi response (risposta).
### Caratteristiche
- HTTP usa TCP,
- HTTP è stateless, perché (il server web) non memorizza info (tipo sessione e cookie) del client e delle sue richieste,
- HTTP è pull-based, perché è il client che richiede i dati al server (pagine web),
- HTTP è un protocollo in-band, perché invia messaggi di controllo con connessione di trasferimento dati,
- HTTP è creato per il trasferimento di pagine web (ora usato per interfacciare l’utente ad app web, tipo social, giochi, e-commerce…),
- HTTP non è sicuro, manda tutto in chiaro (ma c’è HTTPS con SSL/TLS che ovvia al problema),
- L’app web è client/server; e il web server è installato nell’ISP, è sempre attivo, ha IP fisso e port n° 80 (well-known),
- HTTP permette 2 tipi di connessioni:
- Non persistenti, uniche e possibili con HTTP/1.0 (server HTTP chiude connessione ad ogni oggetto inviato),
- Persistenti, con HTTP/1.1 (server HTTP chiude la connessione dopo un certo periodo di inattività).
### Struttura dei messaggi HTTP
#### Richieste
Una richiesta HTTP è composta da: [metodo] [URI della risorsa] [versione HTTP] --> “GET / HTTP/1.1”.
È usato il metodo GET per ottenere la risorsa richiesta. Si usa anche POST. “/” è l’URI della risorsa richiesta all’host. 
HTTP/1.1 indica che si sta usando la versione 1.1 del protocollo HTTP. Il resto sono linee di header, in forma [campo]: [valore].
###### Campi dell’header
-	Host --> È il nome di dominio del server (virtuale) a cui è fatta la richiesta. Necessario per l’hosting condiviso, dove 1 pc hosta + domini, per riconoscerli anche se il TCP usa solo l’IP del pc (comune a tutti i siti del pc).
-	User-Agent --> Campo con informazioni sul client (di solito browser) che origina la richiesta.
-	Referer --> Contiene l’URL da cui è stata generata la richiesta HTTP (così server web sa da dove viene la richiesta). 
L’URL è quello della pagina con il link che ha generato la richiesta, quindi è 2M.html se ho cliccato sul suo link CIAO.jpg.
-	Accept --> Campo che specifica i tipi di contenuto che il client accetta (interpreta) e i suoi valori sono detti media type o tipi MIME (Multipurpose Internet Mail Extensions). I tipi MIME più comuni sono:
text/plain
testo non formattato	text/html
pagine html	text/xml
documenti xml	image/jpeg
immagini jpeg	application/xhtml+xml
documenti xhtml	multipart/form-data
x campi di form html	application/octet-stream
x dati binari arbitrari
L’header HTTP deve essere in US-ASCII a 7 bit, ma il campo MIME definisce la forma del contenuto del body.
-	Accept-(…) --> 3 campi:
-	Language --> indica le preferenze di lingua usate (in ordine).
-	Encoding --> indica le tecniche di compressione dati supportate.
-	Charset --> indica le codifiche dei caratteri accettabili.
-	Keep-Alive --> Tempo in millisecondi di durata della connessione,
-	Connection --> Indica il tipo di connessione usata:
- Keep-Alive (persistente, HTTP/1.1).
- Close (non persistente, HTTP/1.0).
#### Risposte
Una risposta HTTP è composta da: [versione HTTP] [Status] [Desc] --> “HTTP/1.1 200 OK”.
Qui si usano gli status codes e le loro descrizioni. Tra i più frequenti ci sono:
-	200 = OK,
-	301 = Moved Permanently (URI cambiato),
-	304 = Not Modified,
-	400 = Bad Request,
-	401 = Unauthorized,
-	403 = Forbidden (manca il permesso per l'accesso),
-	404 = Not Found (errore di digitazione o, spesso, il server non ci vuole rivelare la vera ragione del rifiuto),
-	503 = Service Unavailable (carico eccessivo o manutenzione server).
###### Campi dell’header
-	Date --> Data e ora di arrivo,
-	Server --> Informazioni sul software in esecuzione sul server,
-	Content-length --> Dimensione in byte dei dati allegati,
-	Content-type --> Indica il tipo del contenuto.
### Autenticazione
Molte app web (= usano HTTP) limitano l’accesso ad utenti autorizzati. Una tecnica è l’HTTP Basic (auth integrato in HTTP).
1)	Un client richiede una risorsa che necessita di auth e il server risponde con 401 Unauthorized, che ha sto campo:
                                                    “WWW-Authenticate: `<type>` realm = `<realm>`.
Con `<type>` che è il tipo di tecnica (in questo caso Basic) e `<realm>` che descrive l’area protetta da auth.
2)	Il browser client fa quindi visualizzare una pagina per l’immissione di credenziali (questa è detta challenge) e, una volta inserite, vengono inoltrate al server con un messaggio simile all’originale ma con l’aggiunta del campo:                                                     “**Authorization: Basic** {YWxleDpwaXBwbw==}”.
Dove la stringa tra […] sono usr e pw (alex:pippo) codificati (non crittografati) in base64 (ASCII 7 bit richiesto da HTTP).
3)	Il server riceve i dati, verifica l’auth e invia la pagina richiesta se credenziali valide. Nelle richieste successive il browser invia direttamente l’header Authorization senza intervento dell’utente.
### Caching
Client e server mantengono una cache dei dati recenti, per evitare richieste superflue per ottenere dati già ottenuti. Si trovano anche cache addizionali nella rete nel percorso tra client e server (tipo nei proxy). HTTP/1.1 fornisce delle funzioni per il controllo della cache tramite il campo “Cache-Control”, che può assumere diversi valori (nelle risposte):
-	no-store --> impedisce al client destinatario di salvare in cache il messaggio (però lo può salvare in memoria),
-	no-cache --> il messaggio è salvabile in cache, ma il client è forzato a convalidarlo col server per ogni richiesta futura,
-	public --> consente anche ai proxy nel percorso tra C/S il salvataggio del body del messaggio in cache,
-	private --> consente il salvataggio in cache del messaggio solo al destinatario,
-	max-age --> definisce il tempo massimo di permanenza in cache del messaggio.
Con il campo If-Modified-Since è possibile fare una richiesta condizionata di una pagina solo se ha subito modifiche dopo una certa data. In caso di nessuna modifica dalla data specificata, il server risponde con 304 Not modified. 
(Per verificare ciò si usa il campo Last-Modified dei messaggi di risposta a una richiesta fatta a una risorsa).
Cookies
HTTP è stateless, ma a volte serve mantenere delle informazioni relative all’utente per la navigazione. Soluzioni:
-	Sessioni --> informazioni di navigazione salvate e gestite dal server,
-	Campi hidden --> informazioni immagazzinate in campi di form nascosti,
-	Cookie --> informazioni di navigazione salvate e gestite dal client (a differenza degli altri, supportati da HTTP).
Uso
I cookie sono usati per 3 funzionalità:
-	Gestione sessione --> login, carrello, punteggi o cose che server ricorda (o x dire se 2 richieste vengono da stesso browser),
-	Personalizzazione --> user preferences, temi e altre impostazioni,
-	Tracciamento --> registrazione e analisi di comportamenti dell’utente.
Funzionamento
L’uso dei cookie prevede 4 componenti:
-	Cookie --> campo header nei messaggi di richiesta,
-	Set-cookie --> campo header nei messaggi di risposta,
-	Un file temporaneo nel file system del client e gestito da browser,
-	(db sul web server / sito, facoltativo).
Quindi:
1)	Il browser accede a un sito e manda una richiesta al suo web server,
2)	Il server crea un identificativo univoco che invia al client con una risposta avente: “Set-Cookie: <cookie>=<value>”, 
dove <cookie> è il nome del cookie dato dal server, mentre <value> è il datetime in cui è creato (ma sempre?).
 
3)	Da adesso in poi il valore del cookie è incluso in tutte le richieste nel campo “Cookie: …”. Server monitora attività client.
Tipi di cookie
I cookie possono essere:
-	Di sessione --> cancellati quando il client termina / browser si chiude (non specificati Expires o Max-Age),
-	Permanenti --> salvati nel client e scadono ad un certo datetime (Expires) o dopo un certo tempo (Max-Age).
Sicurezza
I cookie non sono sicuri, quindi info riservate o sensibili non vanno mai archiviate o trasmesse con cookie HTTP, anche perché il furto di cookie può comportare il dirottamento di una sessione dell’utente autenticato. I metodi di furto più comuni sono la social engineering e lo sfruttamento di vulnerabilità per XSS (Cross-Site Scripting).
Una volta i cookie erano salvati solo nello storage del client, perché era l’unico modo, mentre ora è consigliato usare delle Web storage API (API di salvataggio), dato che i cookie sono inviati ad ogni richiesta riducendo le performance.
Direttiva UE cookie
La direttiva 2009/136/EC del parlamento europeo in vigore dal 25/05/2011 sancisce (non impone) i requisiti per i cookie in tutti gli stati dell’UE. In breve indica che prima di memorizzare qualsiasi cookie, l’utente deve darne il consenso esplicito, questo perché i cookie possono essere considerati una violazione della privacy degli utenti; e tramite una combo di essi ed info date dall’utente, un sito può apprendere molto sul suo conto e vendere ciò a terzi.
FTP
L’FTP permette il trasferimento di file tra host su una rete senza bisogno di loggarsi o saper usare il sistema remoto destinatario, dando l’accesso a file system remoti con comandi molto semplici. È un servizio client/server, i cui trasferimenti di file sono sia in download che in upload. Utenti client interfacciati col servizio con FTP User Agent.
FTP prevede il controllo degli accessi per chi accede a files, per mezzo di una auth (username e password) non cifrata, per questo è un protocollo non sicuro (al contrario di SFTP); ed è il server FTP che verifica i privilegi di accesso.
FTP usa TCP (come HTTP), però usa 2 connessioni TCP separate:
-	Connessione di controllo --> per l’invio di info di controllo tra gli host (per auth e comandi),
-	Connessione dati --> per il trasferimento di file.
Per questo si dice che FTP è out-of-band (fuori banda), al contrario di HTTP, che invece invia le info di controllo negli header dei messaggi e usa una connessione unica (in-band).
Modalità
L’FTP ha 2 modalità di funzionamento:
Modalità attiva
All’apertura della porta di comando (client), il client dice al server di voler usare la modalità attiva inviandogli un n° di porta non privilegiata e casuale (> 1024) aperta sullo stesso. Il server apre quindi 2 collegamenti:
-	Tra la porta well-known 20 e l’IP del server,
-	Tra porta specificata dal client e l’IP del client.
In modalità attiva:
-	La connessione di controllo è aperta dall’FTP client,
-	La connessione dati è aperta dall’FTP server.
Il client deve essere abilitato ad accettare collegamenti tramite qualsiasi porta > 1024; ma i firewall impediscono spesso le connessioni in entrata dai server FTP, per cui è stata definita la modalità passiva.
Modalità passiva
All’apertura della porta di comando (client), il client richiede di voler usare la modalità passiva, quindi il server gli fornisce un n° di porta non privilegiata e casuale (> 1024) aperta sullo stesso. Il client apre quindi 2 collegamenti:
-	Tra la porta specificata dal server e l’IP del server,
-	Tra una porta non privilegiata casuale e l’IP del client.
In modalità passiva
-	La connessione di controllo è aperta dall’FTP client,
-	La connessione dati è aperta dall’FTP client.
Con la modalità passiva viene limitato il range delle porte non privilegiate del server FTP, riducendo le porte aperte sul server e semplificando la creazione delle regole del firewall per il server. 
Per entrambe le modalità
La connessione dati non è persistente, è aperta e chiusa per ogni trasferimento di file.
La connessione di controllo è persistente, ovvero mantenuta attiva per tutta la sessione di trasferimento dei file; inoltre è anche stateful, mantiene gli stati, perché il server deve associarla con un utente specifico e la sua directory.
Il salvataggio di informazioni comporta l’uso di RAM, quindi a parità di risorse, un server FTP può mantenere in contemporanea molte meno connessioni rispetto ad un server HTTP.
Remote desktop 
Protocollo che permette a un client (locale) di funzionare come terminale di un pc remoto server.
-	Tutto ciò che è fatto dal client viene inviato al server, che lo interpreta come se fosse stato fatto su di sé,
-	Tutto ciò che il server mostra in output (allo schermo), è trasmesso al client via internet e questo lo visualizza.
Il pc server usa la console del client per l’I/O, quindi ciò che il client scrive in console è interpretato e eseguito su server.
Telnet
È un protocollo client/server basato su TCP (server port 23) e il nome del prog che avvia sessioni con l’host remoto. Per la progettazione del protocollo e la sua flessibilità, con programmi Telnet è possibile stabilire connessioni a altri servizi internet, come SMTP (port 25) o HTTP (port 80). 
Telnet è insicuro, quindi di default è disabilitato sui server in rete (anche su windows) e i dati sono trasmessi in chiaro.
PuTTY
PuTTY è un programma client per remote desktop per OS windows e implementa protocolli client, tipo Telnet e SSH.
SSH
SSH (Secure Shell) dà agli amministratori di rete un modo sicuro per accedere a un host remoto. Usa la porta 22.
È molto usato per: gestione remota di sistemi e app, accedere ad host in rete, eseguire comandi e spostare file tra pc… 
Se serve, SSH usa la crittografia a chiave pubblica per autenticare l’host remoto e consentirgli di autenticare l’utente (ovviamente tutti i dati di auth, i comandi, l’output e i file trasferiti sono crittati).
Posta elettronica
L’email è un sistema di comunicazione asincrono: l’utente invia e riceve messaggi senza sincronizzarsi con altri.
Il sistema di email presenta 3 componenti principali:
MUA (Mail User Agent)
Sono dei programmi che interfacciano l’utente con il sistema di posta (tipo Outlook, Gmail…). I MUA eseguono SMPT client per contattare SMTP server sul mail server in uso dall’utente.
Mail servers
Server di posta, sono il nucleo dell’infrastruttura del servizio e: ricevono le email da consegnare, le inoltrano a destinazione, hanno delle mailbox (deposito email ricevute) e delle message queue (code di email in transito) (tipo Exchange, Exim e Sendmail).
Eseguono il protocollo SMTP:
-	SMTP server per rispondere a SMTP client del MUA utente.
-	SMTP client per contattare il mail server destinatario di 1 mail.
Protocollo SMTP (Simple Mail Transfer Protocol)
È un protocollo push (di invio) che definisce le regole di invio del messaggio da un client a un mail server.
Uso
1)	Il Mail User Agent del client invia l’email al mail server del mittente, proseguendo poi in internet.
2)	L’email arriva al mail server destinatario (recipient mail server per la mailbox) che la salva nella mailbox del destinatario. 
Se il mail server mittente non riesce a consegnare la mail al mail server destinatario, la trattiene nella sua message queue e, periodicamente, riprova a trasferirla. Dopo un n° di tentativi falliti, email rimossa e notificato il fallimento.
SMTP
Protocollo definito nella RFC 821 del 1982. Caratteristiche:
-	I messaggi (pacchetti a livello applicativo) devono essere in US-ASCII a 7 bit,
-	Sono usate connessioni TCP permanenti (+ messaggi trasferibili tra 2 mail server in 1 connessione),
-	Usa la porta 25. È un protocollo full-duplex, stateful, in-band, affidabile, push e sincrono (non come il servizio di posta).
-	Definisce la procedura di trasparenza dei dati, così che ci sia sempre il delimitatore di fine email “<CRLF>.<CRLF>”. Ogni carattere che inserisco nel messaggio (tipo caratteri speciali o sequenze come la precedente) non influisce sul riconoscimento delle sequenze da parte del protocollo né invalida la mail.
SMTP è orientato alla connessione e la comunicazione prevede queste fasi:
1)	Apertura con handshake e identificazione del mittente (comando “HELO hostname”),
2)	Identificazione mittente delle mail (comando “MAIL FROM”),
3)	Identificazione destinatario delle mail (comando “RCPT TO”),
4)	Invio di tutte le mail (comando “DATA”),
5)	Invio di “<CRLF>.<CRLF>” per indicare la fine dei dati,
6)	Chiusura della connessione (comando “QUIT”).
RFC 1869 e 2821 definiscono l’ESMTP (Extended SMTP) che permette l’uso di tipi MIME (supporto multimedialità). Quindi:
-	Permessi char diversi da US-ASCII a 7 bit,
-	Permessi ancora più tipi di allegati, non solo file di testo,
-	Permesse mail composte da più parti.
Attenzione: i messaggi SMTP (pacchetti del protocollo, PDU) sono diversi dai messaggi di posta (email).
Formato delle email
RFC 822 definisce il formato delle email (come già detto solo a char ASCII 7 bit) che hanno svariati campi di intestazione seguiti dal corpo del messaggio. I campi base di un’intestazione sono:
From: <mittente>	To: <destinatario>	Subject: <oggetto>
Lettura della posta
Servono dei protocolli pull per ricevere le email scaricandole dal mail server. Questi sono: POP3 e IMAP.
POP3
Prevede che le email siano tutte inviate al client e memorizzate in locale, rimuovendole dalla mailbox del mail server. Inoltre Post Office Protocol usa la porta 110, offre un servizio affidabile con TCP e richiede l’auth dell’utente.
IMAP
Internet Message Access Protocol memorizza la posta nella mailbox del mail server senza salvare nulla in locale ma garantendo l’accesso alla posta d’ovunque. Fornisce anche strumenti per la gestione della mailbox e usa la porta 143.
Webmail
Esistono siti che offrono un servizio di posta detto webmail. Il sistema è composto da:
-	Un server webmail, che funge da interfaccia tra l’utente e il servizio di posta e usa SMTP + POP3/IMAP,
-	Il browser col quale l’utente accede al servizio webmail usando HTTP o HTTPS.
DNS
