---
public: true
---
# Web e HTTP
### Server web
Il server web è un’**applicazione in esecuzione su un** pc **server** ch**e fornisce contenuti web** richiesti, è chiamato anche **Daemon HTTP** o **HTTPd**. Questo è costantemente in attesa di richieste da client, e se arriva una, cerca di evaderla il più velocemente possibile cercando e restituendo il file richiesto se trovato. In ambienti Unix/Linux il Daemon si può **duplicare** con la fork(), mandando il figlio a gestire una determinata richiesta e poi muore.
### HTTP
(Le app web lavorano con il protocollo **HTTP**, che stabilisce le regole di comunicazione tra client e server. Questo trasmette i dati in formato testuale (ASCII) con i protocolli IP (liv 3) e TCP (liv 4), il cui compito è di instaurare e mantenere la comunicazione.)
La comunicazione inizia con una richiesta di connessione **TCP** con **porta** **80** (o **443** se **HTTPS**).
**URI** (Uniform Resource Identifier)
**Identifica univocamente una risorsa** tramite uno schema universale e una sintassi generica.
**URL** (Uniform Resource Locator)
(Sottoinsieme di URI) **identifica univocamente l’indirizzo web di una risorsa**, tipo pagina HTML. Metaforicamente una stringa URL risponde alle domande: “**_Come_**_?_”, “**_A chi_**_?_”, “**_Che cosa_**_?_” così:
1) **Protocollo** usato per la richiesta (_Come?_)
2) **Host** a cui fare la richiesta (_A chi?_)
3) **File** richiesto (_Che cosa?_)
Forma: \[**protocollo**\]://\[**host**\]/\[**file**\] --> \http://www.gildown.it/interroghiamo.html
HTTP Requests
Fatte per **accedere a una risorsa** **identificata da un URI** **presente su un server** in Internet. Sono **stringhe ASCII** così:
![[Pasted image 20240304163221.png]]
**Metodo**: GET, POST… + **Versione** **HTTP** + **Metainformazioni** con **valori** + **body**.
HTTP Responses
Anche queste consistono di stringhe di testo ASCII:
![[Pasted image 20240304163342.png]]
**Versione HTTP** + **status code** + **descrizione status code** + **Metainformazioni** con **valori** + **body**.
Status Code
-    **200** – **299** = **Success**,
-    **300** – **399** = **Redirect**,
-    **400** – **499** = **Client Error**,
-    **500** – **599** = **Server Error**.
Passaggio di parametri
Client passa parametri al server nell’URL con il protocollo HTTP, in formato: [**URL**]?[**NomePar**]=[**ValorePar**]&…
GET
**Invia dati in formato ASCII aggiungendo i parametri all’URL** come suddetto. Si può fare digitando i parametri giusti nell’URL oppure compilando un form e facendo submit (così appaiono in automatico).
Col GET il server assegna i parametri dopo il “?” a una variabile chiamata **QUERY_STRING**, poi il **GET** **non** **passa** **body** e la stringa è visibile e ha una **lunghezza max** di **2048 char**.
POST
I parametri sono passati col body della richiesta, quindi non visibili nell’URL e senza limiti.
Caratteristiche
-    **HTTP non ha memoria** (_stateless_), perché le **richieste sono uniche per il server** e **non salvano dati di navigazione** (risolto con **sessione** e **cookies**),
-    **HTTP è asimmetrico** (_pull-based_), ovvero **solo il client chiama il server,**
-    **HTTP è nato per trasmettere pagine web**,
-    **HTTP non è sicuro**, ma **HTTPS** usa **SSL** (Secure Socket Layer) che **crittografa** e **protegge** i **dati** tra client e server.
# Evoluzione delle reti
### Rete
**Insieme di sistemi** (da almeno 2 o + dispositivi) **in comunicazione tra loro e che si scambiano dati.**
Modello Mainframe-Terminal
Le prime erano costose, sviluppate in università e in aziende, e il 1° obiettivo era **condividere** **poche** **risorse** **tra** + **persone**. L'architettura prevedeva:
-    **mainframe** potente
-    semplici **terminali** (associati al mainframe e inutilizzabili se disconnessi da esso)
In seguito si è passati alle moderne reti di computer, fatte da tanti pc che erano:
-    **autonomi** (Non ci sono dipendenze tra i vari pc, quindi se 1 muore l'altro continua ad andare.)
-    **interconnessi** (Capaci di scambiarsi informazioni)
Rete di computer
**Insieme di 2 o + dispositivi in grado di trasmettere dati tra loro**
Problematiche
Elettroniche
Serve stabilire come verranno collegati fisicamente i sistemi (cavi/no cavi, fibra/rame/wi-fi...) in base a vari fattori (tipo n sistemi da connettere, distanza tra sistemi...)
Informatiche
Serve un OS in grado di sfruttare l'hardware 
Telematiche
Serve tener conto che potrebbero già esserci reti di trasmissione di info sfruttabili sul territorio (tipo rete telefonica)
Tutto ciò va risolto rendendo **irrilevante/ininfluente la distanza tra i sistemi** da connettere.
Vantaggi
-    **Condivisione delle risorse**
-    **Miglior rapporto prestazioni/costo**
-    **Scalabilità** (investimenti mirati per migliorare prestazioni complessive nei sistemi usati)
-    **Maggior Fault Tolerance** (affidabilità rispetto ai guasti)
Dimensione e nomi
-    **LAN** (Local Area Network) --> con cavi   |   **WLAN** (Wireless Local Area Network) --> con wifi
Piccole reti grande da ufficio a edificio per condividere dati tra utenti con:
- Alta velocità di trasmissione (essendo piccole)
- Sicurezza + easy
-    **WAN** (Wide Area Network)
Dimensioni estese da città a pianeta
Internetworking
**Interconnessioni di reti diverse** (tipo LAN con WAN o 2 WLAN...)
# Reti Client/Server e P2P
Tipi di reti
In condivisione c'è sempre 1 pc che mette a disposizione roba e un altro che riceve.
Client/Server
Dei pc (**server**) che **mettono a disposizione delle risorse** o offrono servizi **ad** altri pc (**client**).
Se client non può diventare server e viceversa, il server è detto **server dedicato**.
In altri casi (come in **> parte delle reti locali**) **non vi è** una **distinzione** predefinita **tra client e server**, perché un pc può condividere dati e al contempo usare quelli di un altro pc.
_In reti grandi spesso pc + potente è il server, detto host (distribuisce servizi e risorse a rete) ma pc obsoleti possono fare da server_
P2P
Tutti i **pc** sono **sullo stesso livello** e condividono risorse comuni. Qui tutti i pc sono sia client sia server.
Messaggi
**Insieme di caratteri e dati che devono essere trasferiti da un sistema a un altro**.
_(Quindi un insieme di info organizzate in modo da formare un'entità trasmissibile tra 2 sistemi di rete)_
Pacchetti
Per favorire la trasmissione, i messaggi sono suddivisi in **pacchetti** (perché un mess piccolo è + semplice che trovi una linea che abbia spazio per lui e può lasciare spazio ad altri mess)
I pacchetti hanno anche info riguardanti: il **destinatario** e **l'ordine di ricomposizione** una volta giunti a destinazione.
Reti C/S (Client-Server)
Quando si stabilisce una comunicazione tra client e server, inizia l'erogazione del servizio richiesto, con 2 possibilità:
Esecuzione lato client o locale
**Il programma è trasmesso dal server, caricato in RAM ed eseguito dal client stesso**
1) _Client_: invia richiesta x prog
2) _Server_: elabora e invia il prog
3) _Client_: riceve e usa il prog per avere risultati
Esecuzione lato server o remota
**Il programma è eseguito sul server che trasmette i dati al client**
1) _Client_: invia richiesta per una elaborazione
2) _Server_: elabora richiesta, la esegue, risponde con il dato
3) _Client_: riceve il dato
Vantaggi esecuzione lato server
-      **unica installazione** --> prog installato solo su server e non su tutti i client
-      **aggiornamenti e manutenzione + easy** --> siccome è su 1 macchina, e lo stesso livello di update tra tutti i sistemi
-      **diminuzione costi** --> di licenze
-      **> sicurezza di dati** --> solo 1 backup da fare
Cloud
**Insieme di risorse, applicazioni e servizi disponibili e distribuiti su tutta la rete**. (vantaggi di prima sono alla base del cloud computing)
Reti P2P (+ usata in reti locali dove ogni pc condivide dati)
Non vi è distinzione tra client e server, bensì i pc di una rete sono detti **nodi** (ovvero, **ogni pc è sia client sia server**)
Un pc è client quando riceve dati e server quando li fornisce.
Esempio comune è il file-sharing tramite internet., fatto con programmi tipo eMule o bitTorrent, dove un pc si connette a un altro per scaricare dei file che lui mette a disposizione.
Vantaggi
-      **semplice da gestire** (dato che non necessita amministrazione)
Svantaggi
-      **meno sicura nel controllo di accessi e utenti** (dato che non c'è amministrazione)
Differenze
Client/Server
-      **L'accesso** alle risorse è **gestito** **da** un **database** **di** **sicurezza** centralizzato
-      **Whitelist** del server **con** **utenti** **e** rispettive **password**
-      Gli **utenti** possono **accedere** **solo** a **determinate** **risorse** a cui sono autorizzati
-      **Pochi** **problemi** **al** **ridimensionamento**
P2P
-      Implementano una **rete overlay astratta** a **livello applicazione** sulla topologia fisica
-      Idea di base è **condividere** **risorse** in **modo** **economico**
-      Solo gli **utenti** finali possono **controllare l'accesso** alle **risorse** (con password in punti di condivisione che creano)
-      **< prestazioni al ridimensionamento**
# Protocolli
### Protocollo
**Insiemi di regole e convenzioni usate nel dialogo tra livelli.**
TCP
Il TCP è un protocollo livello **trasporto** che fornisce supporto a altri protocolli liv applicativo (HTTP, FTP, SMTP, SSH…).
È importante perché **permette** di **operare** **contemporaneamente** **con applicativi distinti**. (Tipo utenti in internet possono usare + app internet, non solo TCP ma anche UDP)
Ciò avviene grazie alle **porte**, numeri interi di 16 bit (0-65535). (nelle trasmissioni viene dopo l'IP destinatario separato da ":", tipo: 192.168.0.1:80)
È **orientato alla connessione** (stabilire connessione prima di trasferimento) al contrario di **UDP**. (_Both use IP_)
Porte
**Identificano univocamente l'applicazione a cui instradare i pacchetti**, soprattutto in caso ci siano tante applicazioni che vanno riconosciute in rete. Divise in:
Well-Known (0 – 1023)
Riservate per servizi e app standard dei server, e settate di default sui client per essi. (client non dovrebbero usarle)
Registrate (1024 – 49151)
Usate per servizi privati, il client le usa per farci quello che vuole
Dinamiche (49152 – 65535)
Libere per essere assegnate dinamicamente da processi applicativi, usate per servizi passivi, tipo P2P.
Porte di default
TCP 80
Abbiamo 2 pc, 1 client e 1 server. Il server attende sempre per 1° una richiesta dal client, ma questo deve sapere il suo IP e la porta del servizio che deve usare. Il server non può usare una porta casuale per quel servizio, se no il client come lo raggiunge? Per questo si è definita la porta TCP 80 come predefinita per accedere a un qualsiasi server HTTP.
- TCP 25 --> Server SMTP
- TCP21 --> Server FTP
- UDP 53 --> Server DNS
- TCP 443 --> HTTPs
# Socket
Perché?
Per lo scambio di messaggi tra processi su host diversi, serve un modo per i processi di identificare il destinatario, quindi le applicazioni in rete vanno riconosciute in qualche modo; ciò grazie al port address.
Port address
**N° che identifica** le **porte logiche** (su 2 byte, da 0 a 65535) e **individua** un **canale** da usare **per la comunicazione**.
I **n° di porta logica** sono **univocamente assegnati al relativo protocollo** (porta TCP != porta UDP, anche se a volte usata una unica per entrambi). La sola **porta** **non** **rende** una **connessione** **univoca**, perché processi di host diversi potrebbero ascoltare tutti sulla stessa. Per questo **la** **porta viene combinata con l’indirizzo IP** (socket).
**Socket**
È scritto così --> “**[IP]:[port]**”. La coppia è:
**IP** --> che identifica l’host avente il processo destinatario con cui comunicare.
**Port** --> identifica la porta usata dal processo dell’host destinatario.
Permette di comunicare in rete con la pila TCP/IP (mess esce da socket mittente e arriva a socket dest).
In un server TCP abbiamo 2 tipi di socket:
-    1 per accettare le connessioni (condiviso) che si chiama _connection socket_,
-    1 per funzioni send() e receive() (non condiviso) detto _data socket_.
Socket & client/server
In rete ci sono client e server. Il **server** (o meglio **processi server** che girano **su un host che erogano servizi ad altri processi** in rete) ha più controllo perché lui **crea i socket**. Più client possono comunicare sullo stesso socket.
Un processo **client deve conoscere il socket del server** (con eventuale richiesta), mentre il **server deve acquisire le info sull’host client**, come il suo **n° di porta** per inviare le risposte. Passaggi:
1)       **Inizializzazione** dei **processi** (si **crea un socket**),
2)       **Client** **effettua** la **richiesta di collegamento** (nel socket ci sono delle **code** con le **richieste** in logica **FIFO**),
3)       Il server accetta la richiesta e stabilisce il collegamento (**se esaurisco la coda**, il **server** **rischia di crashare** per troppe richieste, quindi **controlla** il **socket** e **vede quante** **ne** **arrivano** **e da quali IP**. Se ne arrivano troppe da un IP magari può essere un DDoS e prendere contromisure).
Il server quando accetta la richiesta realizza un canale virtuale tra il client e un suo nuovo socket, al fine di lasciare libero il primo per ulteriori richieste?????
Processi si scambiano dati con funzioni **read()** e **write()** fino a **chiusura** del **canale** o a chiamata della primitiva **close()**.
Famiglie di socket
Ci sono 2 famiglie di socket (o domini):
-    Unix Domain Socket (AF_UNIX) --> pathname valido nel file system della macchina, permette trasferimento dati tra processi sulla stessa macchina UNIX;
-    Internet socket (AF_INET) --> usato nelle applicazioni per il trasferimento dati tra processi su macchine remote connesse tramite una LAN o internet; specificato da 2 valori:
-    **Indirizzo IP** (32 bit), che individua un unico host Internet,
-    **N° di porta** (16 bit), che specifica una porta dell’host.
Tipi di socket
Ci sono 3 tipi di socket:
-    Stream Socket --> **Protocollo TCP/IP** (affidabile con connessione, quindi connessioni punto-punto unicast),
-    Datagram Socket --> **Protocollo UDP** (non affidabile, usato anche per multicast),
-    Raw Socket --> Usati per realizzare protocolli.
# App e sistemi distribuiti
Sistema distribuito
Un **insieme di nodi interconnessi** in una rete che **si scambiano messaggi per** **eseguire algoritmi distribuiti**.
Sito = luogo fisico di una macchina.
Nodo = macchina o sistema in un sito (detto anche host).
Client = nodo che consuma risorse da un server.
Server = nodo che fornisce risorse ad altri nodi.
Sistemi distribuiti avanzati
Resource sharing
Condivisione di file in siti remoti, informazioni processate in un db distribuito e uso di dispositivi hw remoti.
Load sharing
Maggiore potenza di calcolo e velocità e load balancing (gestione e suddivisione del carico).
Vantaggi
Reliability --> **Identificazione** di siti in failure, **trasferimento** funzioni da un sito in failure e **ripristino** di esso.
Communication --> Scambio di messaggi.
Flexibility --> Rimpiazzo di mainframe con reti di host e < costi.
Applicazione distribuita
**Applicazione costituita da 2 o + processi eseguiti in parallelo su pc diversi connessi in una rete**.
I processi di una app distribuita cooperano sfruttando i servizi forniti dalla rete e si devono mettere in contatto.
Layer applicativi
1) Livello presentazione o Front End
Gestisce la logica di presentazione, ovvero le modalità di interazione con l'utente (interfacciamento grafico e rendering delle info).
2) Livello di logica applicativa
Gestisce le funzioni da mettere a disposizione all'utente.
3) Livello di accesso ai dati
Gestisce le informazioni ed eventualmente l'accesso ai db.
Questi (livelli software) possono essere installati su vari livelli hardware, detti **Tier**.
Tiers
App può essere configurata come:
Single Tiered
Tutti i **livelli ospitati** **su** **1 host**
Two Tiered
**Livelli divisi tra 1 client** (che ha il livello **Presentazione**) e **1 server** (che ha il **livello** di **accesso** ai **dati**). Il livello di **logica** **applicativa** può stare **o sul client o sul server**.
Three Tiered
**3 macchine dedicate 1 per livello** (client x presentazione e 2 server per altri 2)
Architettura multi-tier = usati 2 o 3 tier come arch di una app (ES: **browser** [_Presentazione_] che fa richieste a un **server** [_Logica applicativa_] che fa richieste a un **DBMS Server** [_Logica accesso ai dati_]) i livelli adiacenti assumono i ruoli di **client e server** (il **+ vicino a utente è sempre client**, mentre il **più lontano sempre server**)
Clients
Thin Client --> quando a **livello utente** c'è **solo** livello **presentazione**
Fat Client --> quando a **livello utente la logica applicativa** **si appoggia su quella di accesso ai dati**
Ends
Backend --> Livello **middleware** che contiene la **combo di logica di accesso ai dati e logica applicativa**
Frontend --> Livello **presentazione**
Sistemi
Centralizzato
Quando **dati e applicazioni sono su un unico nodo elaborativo**. (Tipo architettura a mainframe?)
Distribuito
**Insiemi di applicazioni logicamente indipendenti che cooperano per raggiungere obiettivi comuni tramite** **infrastruttura** di comunicazione **HW** e **SW**
Esso realizza almeno 1 delle seguenti situazioni:
1) Elaborazione distribuita --> **applicazioni cooperanti** distribuite su + nodi elaborativi
2) Base di dati distribuita --> **database** ospitato su + nodi elaborativi
Server Farm
**Insieme** (molto grandi) **di pc interconnessi che condividono app e dati**.
Realizzate secondo 2 principi progettuali:
Cloning
**Su ogni nodo della farm sono installate le stesse app (duplicandole).**
Le richieste sono poi inviate ai vari client tramite un sistema di **load-balancing** (tecnica che distribuisce il carico di elaborazione tra diversi server).
Per cui: **> scalabilità e affidabilità** di arch nel complesso. I sistemi di load-balancing integrano anche **sistemi di** **monitoraggio** che **escludono** automaticamente **cluster non raggiungibili**
RACS (Reliable Array of Cloned Services)
**Insieme di cloni dedicati a svolgere un certo servizio**, in cui **se 1 si guasta**, **un altro** continua a **erogare** il **servizio**.
Presenti in 2 configurazioni:
Shared Nothing
**Dati memorizzati sono duplicati e stanno sul disco di ogni clone.**
**Ottime** **prestazioni** per **app read-only.**
Shared Disk (cluster)
I **cloni condividono un server che gestisce i dischi fissi**.
Partitioning
**Prevede duplicazione di HW o SW**, **ma non dei dati**, **ripartiti tra nodi**.
**Ogni nodo svolge una funzione** **specifica** (tipo ogni nodo assegnato un endpoint di un ito)
**Dati** però **sono su 1 singolo server**, quindi **se esplode**, c'è il **degrado parziale** dei sistemi distribuiti (non tutto il sistema, **ma solo alcune funzionalità**)
Per risolvere questo si usano i:
RAPS (Reliable Array of Partitioned Services)
**Permette di ottenere piena scalabilità e disponibilità del servizio**.
# Datacenter
### Datacenter
Un **Datacenter** è lo spazio fisico che ospita le infrastrutture tecnologiche usate per elaborazione, memorizzazione e condivisione delle informazioni.
- Dal punto di vista **fisico** un datacenter da: spazio e alloggiamenti per i dispositivi, energia, sistemi di raffreddamento e sicurezza fisica oltre a interconnessioni con operatori per accesso a internet e sicurezza logica.
- Da quello **logico** invece, un datacenter da: servizi come hosting, cloud privato e/o pubblico, applicazioni web, posta elettronica, gestione domini e altre attività non necessariamente tipiche di un datacenter.
##### Tipi
- **Aziendali** (**CED**) --> Proprietà di un’azienda e forniscono servizi relativi alla struttura interna.
- **Offerti da terzi** (**hosting, housing, cloud**) --> Strutture per gestione ed erogazione di servizi accessibili in internet.
##### Componenti
###### Infrastruttura operativa
(O _white space_), ospita i rack con i server, i sistemi di storage, gli apparati di monitoraggio e gli apparati per trasmettere dati in rete.
###### Infrastrutture di supporto
Dispositivi di backup, sistemi ridondanti, gruppi di continuità, impianti di climatizzazione, sistemi di raffreddamento, impianti antincendio e sistema di distribuzione dell’energia.
###### Personale operativo
Le figure professionali che gestiscono il centro: system admin, tecnici, sistemisti, programmatori e security.
##### Obiettivi
-    **Mantenere la disponibilità dei dati garantendo continuità di elaborazione**. Quindi serve monitorare il rischio e adottare misure di protezione, tenere da conto l’errore umano e impostare logiche di controllo degli accessi oltre a garantire la protezione da minacce dalla rete (tipo malware).
-    **Proteggere le info** considerando eventuali attacchi di cyber-criminalità e adottando misure internazionali per la privacy, per questo si usano firewall e sistemi anti-intrusione (IDS).
##### Evoluzione
1) **Portare all’esterno** dell’azienda i **server e lo storage** (_collocation_) rivolgendosi a terzi ed eliminando il CED;
2) Creare **datacenter virtuali** facilmente manipolabili e scalabili con la **virtualizzazione** per ridurre costi e spazi;
3) Affidarsi a un **fornitore di servizi cloud** (_serverless approach_) che gestisca da sé le problematiche fisiche.
##### Rischi
Portando tutti i servizi su un’unica struttura determina un **punto di criticità** detto **SPoF** (*Single Point of Failure)* perché un **guasto** **compromette** **l’intero** **sistema**; e quindi > il _downtime_, > la ripercussione economica.
Serve garantire **_High Availability_** (alta disponibilità di servizio), con ridondanze, duplicazioni, cluster e repliche datacenter.
##### Garanzie
###### Fault Tolerance
**Tolleranza ai guasti**, ovvero **evitare l’interruzione dei servizi a fronte di essi**, fatto con diverse tecniche come: RAID e la duplicazione di server e apparati di rete. È complementare insieme alla _disaster recovery_.
###### Disaster Recovery
**Recupero e ripristino** di applicazioni e dati **in caso di disastro** (di qualsiasi tipo, dal naturale all’errore umano) fatto spesso con duplicazione di interi datacenter. Determinante è il tempo di ripristino.
###### Business Continuity
**Continuità del servizio** che garantisce continuità operativa anche durante disastri o guasti.
### Tiers
##### Tier 1 – Basic Site Infrastructure
**Operatività** = **99.67%**   |   **Fermo macchina** = **28,8h/anno**
Data center con **gruppo di continuità** con funzioni **minime**, un **unico percorso di distribuzione** e **ridondanze nulle** o **limitate**. Protezione limitata contro eventi fisici.
##### Tier 2 – Reduntant Capacity Site Infrastructure
**Operatività** = **99.75%**   |   **Fermo macchina** = **22h/anno**
Ha **maggiori** capacità **ridondanti**, migliori **gruppi di continuità**, sistemi di **raffreddamento** e un **unico percorso di distribuzione non ridondante**. Protezione da eventi fisici migliorata.
##### Tier 3 – Concurrently Maintainable Site Infrastructure
**Operatività** = **99.98%**   |   **Fermo macchina** = **1,6h/anno**
Aggiunge componenti di **ridondanza** e **percorsi** di **distribuzione** **indipendenti** **multipli**. Il sito è **contemporaneamente** **mantenibile**, quindi se sospendo qualche componente di capacità, il sito dà ancora servizi mentre lo mantengo. Ha protezione contro la maggior parte degli eventi fisici.
##### Tier 4 – Fault Tolerant Site Infrastructure
**Operatività** = **99.99%**   |   **Fermo macchina** = **0,8h/anno**
Alla manutenzione simultanea aggiunge **l’elaborazione continua** in caso di guasto di componenti (elaborazione influenzata solo se si guastano più componenti identici).
# Virtualizzazione
### Storia
Benché la virtualizzazione risalga agli anni 60, si è diffusa soltanto all'inizio degli anni 2000. 
Le tecnologie di virtualizzazione, sono state sviluppate decenni fa, per risolvere il problema dell'accesso simultaneo di + utenti a 1 pc, dapprima con l'elaborazione batch attiva (in questa le richieste di servizio non sono subito assolte, ma accodate finché le risorse di cui necessitano non sono disponibili), adottata da molte aziende per la sua velocità. Però nel tempo, l'uso di tecniche di virtualizzazione fu sempre meno usato per questo problema.
Ciò fino agli anni 90, quando si iniziò ad usare la virtualizzazione per risolvere 2 problemi dei "commodity server" aziendali con hardware fisici poco utilizzati, permettendo di:
- Partizionare i server,
- Eseguire le app su + tipi e versioni di OS.
Con ciò la virtualizzazione ha contribuito a ridurre il vendor lock-in e ha posto le basi del cloud computing.
### Che cos’è?
È una **tecnica per nascondere e astrarre delle risorse fisiche** (pc, server, rete…) **rendendole disponibili come risorse virtuali**, (risultando, nel caso di pc, in **hw fisici** che **condividono risorse tra** dei loro **guest**).
### Scopo
Lo scopo della virtualizzazione (di pc) è quello di **eseguire in contemporanea + istanze di un OS guest in 1 unico host fisico**. Questi, detti "**guest**", interagiscono con le risorse fisiche dell’host tramite un sw intermedio: l’**hypervisor** o **VMM** (virtual machine monitor).
##### Vantaggi (per persone)
-    Uno **sviluppatore** può eseguire un’app in diversi ambienti senza necessità di + pc fisici,
-    Un **system** **admin** può testare uno scenario complesso con + servizi su + host diversi, fattibile con + VM diverse.
-    Gli **utenti finali** traggono maggiori benefici:
-    **Aumento dell’affidabilità del sistema**, perché possibile dedicare VM a servizi che non vanno in conflitto e isolare i vari guest cosicché eventuali problemi di una VM non influenzino la stabilità di altre.
-    **Consolidamento dei server**, con la virtualizzazione si eseguono + VM sulla stessa macchina, riducendo il n° dei server necessari per l’erogazione di servizi aziendali di 10 volte o +.
-    **Riduzione dei costi**, meno server significa meno costi energetici, di acquisto e di manutenzione dei server.
-    **Disaster recovery**, un OS guest è facilmente ripristinabile riducendo i tempi di indisponibilità per guasto.
-    **Alta disponibilità**, se ci sono + server fisici con hw compatibili e questi condividono uno storage su cui risiedono delle VM, in caso di failure è possibile spostare l’esecuzione delle VM di un host su un altro.
##### Vantaggi (per Datacenter)
-    Riduzione numero di server da gestire,
-    Riduzione spazio fisico necessario,
-    Riduzione costi energetici,
-    Riduzione costi di manutenzione.
##### Benefici
-    **Esecuzione di app legacy**, virtualizzando OS si possono continuare a usare sw aziendali fatti per sistemi obsoleti.
-    **Sviluppo e testing**, è possibile predisporre ambienti di sviluppo/testing senza intaccare l’ambiente principale.
**Riassumendo: - costi, gestione infrastruttura IT + semplice, > affidabilità e > flessibilità.**
### Cosa si virtualizza?
Si riferisce in generale all’astrazione delle **risorse di calcolo** (_computing resources_):
##### Platform virtualization
(Concetto di **VM**) ovvero virtualizzazione di piattaforme hw, poi esteso a storages, namespaces e network resources.
-    **Emulation/Simulation**
-    **Native/Full virtualization**
-    Hardware Enabled Virtualization
-    Partial virtualization
-    **Paravirtualization**
-    **OS-level virtualization**
-    Application virtualization
##### Resource virtualization
(Concetto di **qualità del servizio**) ovvero virtualizzazione di risorse.
-    RAID
-    SAN
-    Channel Bondings
-    VPN/NAT
-    Multiprocesssor e multi-core
-    Cluster e grid computing
-    Partitioning
### **Hypervisor** (VMM)
È un programma **che crea ed esegue VM** **guest** **su** **una** **macchina** **fisica** **host,** che **astrae l’hw di un pc** e che:
-    **Crea e** **controlla** **molti** ambienti di esecuzione (**VM**) diversi e:
-    **Ciascuno** di questi può avere un **proprio** e diverso **OS**
-    **Ciascuno** di questi **crede** **di controllare** **l’intero** sistema **hw**.
Principali hypervisors: VirtualBox, KVM, QEMU, Parallel, Xen, VMWare, Xbox 360.
###### VirtualBox
La **VMM è un processo** che gira nell’host (anche app utente) e il suo **OS** **non sa che si sta virtualizzando** un guest.
##### Virtual Machine (VM)
**Ambiente di esecuzione creato dall’hypervisor**.
##### Tipi di hypervisor
###### Type-1 (_Bare-Metal_ o _Native_)
Il sw di virtualizzazione è **OS-like**, ovvero si **integra direttamente con il kernel del OS** e si **interfaccia con l’hardware** **direttamente**, consentendo gestione di risorse + efficiente, veloce e stabile per i guest. Tipica nella **virtualizzazione di server** (consolidamento di + server in 1) e per la **distribuzione di OS desktop remoti** per utenti in rete.
###### Type-2 (_Hosted_)
**L’hypervisor è** una vera e propria **applicazione** che si **gira sull’OS fisico** e **virtualizza** degli **ambienti** **compatibili** con esso a più alto livello, **facendo da tramite** per le operazioni tra guest e host.
**Svantaggio**: essendo un’applicazione, **non ha la stessa efficienza del Type-1**.
**Vantaggio**: **installazione del sw e creazione dei guest senza difficoltà**, spesso **gratis**.
#### **Principali metodologie**
##### Emulation
L’**hypervisor** **emula un intero set di hw** in modo **standard** **per eseguire l’OS guest** senza modifiche. L'hypervisor presenta al OS guest un hw completo, indipendentemente da quello dell'host. Limiti:
- Hw presentato è **standard**, magari non include funzionalità già implementate in hw dell’host.
- **Necessario interfacciare** la **CPU**, la **memoria** e l’**I/O** tra sistema host e guest.
Emulazione è difficile perché bisogna emulare sistemi guest con processori di velocità = al processore dell’host. Quindi emulazione fattibile quando ho **+ processori**.
##### Full Virtualization
Gli **OS guest** virtualizzati devono essere **compatibili con l’hw dell’host**, quindi **non necessario interfacciare** **CPU**, **memoria** e **I/O** perché **tutto** fatto sull’hw **direttamente**, con > prestazioni.
##### Paravirtualization
L’hypervisor mostra un’**hw sottostante modificato ai guest**, ma ne mantiene l’architettura. Gli **OS delle VM** **sono modificati** (differenza con la full, evitano certe system call, per cui prestazioni vicine all’OS non virtualizzato, siccome istruzioni eseguite su CPU direttamente); (virtualizza - hw fisico, quindi possibili + VM perché ho + memoria free).
##### OS level virtualization
**Non usa hypervisor**, ma si **virtualizzano copie dell’OS dell’host**. I **guest saranno istanze dell’OS dell’host** con un proprio file system, configurazione di rete e applicazioni. VM non necessitano di kernel privati, ma usano lo stesso dell’host con < utilizzo di memoria, quindi semplice condivisione e gestione della memoria). Non adatto a OS **diversi** sullo stesso host, poca stabilità e isolamento.
#### Supporto hardware alla virtualizzazione
Aziende produttrici di hw (come Intel e AMD) hanno iniziato a distribuire CPU con supporto di virtualizzazione per diminuire intervento Hypervisor.
- Intel, che ha implementato (in CPU Xeon e Itanium) le tecnologie **VT-d**, **VT-x** e **VT-i**, che **limitano o eliminano l’intervento** **dell’hypervisor**, eseguendo direttamente e automaticamente operazioni e context switches tra guest e CPU host.
- AMD, con **AMD-V**, un **insieme di estensioni hw** dell’architettura **x86** **per ridurre o eliminare**, **l’intervento dell’hypervisor**.
#### Componenti di virtualizzazione
- CPU scheduling: sono possibili **+ CPU virtuali** **che CPU fisiche** (**_overcommitment_**) e la **VMM** deve **condivide**re **risorse fisiche** **tra** i **guest**. 
	- Overcommitment (CPU e memoria): allocazione di + CPU o memoria virtuale di quella fisica per poter avere + guest. (rischi di stabilità di sistema).
	- Thin provisioning (storage): allocazione di storage flessibile e ottimizzato dando l’impressione che guest ne abbiano disponibile + di quello fisico.
- Memory management: il **VMM overcommitta memoria tra i guest** e **decide quanta ognuno ne può usare** (anche se il guest pensa che la stia usando tutta) oltre a **fare da sé l’allocazione di pagine di memoria**.
- I/O management: il **VMM dedica dispositivi I/O ai guest** e può fornirgli **device drivers astratti** (mappando le richieste a quelli veri).
- Storage management: il VMM assicura che **ogni guest può accedere** **solo** alla parte di **storage assegnatagli**.
- Networking: il VMM fornisce: **a ogni guest** **almeno 1 IP**, **routing tra** il **guest** **e** la **rete** e il **NAT**.
### RAID
Gestendo la memoria vanno gestite le **ridondanze**, quindi considerare possibilità di guasti o situazioni che mettano in pericolo l’integrità dei dati. Ciò è fatto con il **RAID** (_Reduntant Array of Independent Disks_) che **raggruppa gli HDD in un grande disco logico** (**volume**) suddiviso in **sottovolumi** dedicati ai server. Tipi di RAID più usati:
##### RAID 1 o _mirroring_
Si configurano **2 dischi con 1 la copia dell’altro**; se 1 si rompe l’altro continua e quando sostituito si ricostruiscono i dati in esso con quelli dell’altro. **Ottime prestazioni** ma consente di sfruttare solo il **50% dello spazio disponibile**.
##### RAID 5
Si usano **3 o + HDD** e i **dati sono scritti vettorialmente su 2 di essi**, mentre **nel 3° vengono scritti i bit di parità** per ciò che è stato scritto nei primi 2 così che in caso di guasto di 1 disco, le info possono essere **ripristinate** **ricalcolando** **i valori**. Questo presenta un **< spreco di risorse** ma ogni **operazione** **di** **scrittura** **richiede** il **calcolo** dei **bit di parità**.
### Virtual Networking
Una rete virtuale è un **insieme di VM in esecuzione su una singola macchina fisica e collegate logicamente tra loro** **così** **che** **possano scambiarsi dati**. Le VM forniscono le funzionalità di **vNIC**, **virtual switches**, **virtual routers**…
Un virtual switch rileva le VM logicamente collegate alle sue porte virtuali e indirizza il traffico; ciò consente di gestire la connettività a livello datalink, con possibilità di impostare **VLAN** multiple secondo lo standard 802.1q.
###### LACP
Per avere la max disponibilità dei collegamenti, lo switch virtuale può configurare + NIC fisiche associandole a esso in modalità **LACP** (_Link Aggregation Control Protocol_), che rende visibile allo switch le NIC fisiche come un'unica scheda logica e tra queste ripartisce il traffico.
###### Uplink port
Gli switch virtuali devono potersi connettere alle reti fisiche per comunicare con l’esterno, per cui sono usati alcuni adattatori software (**uplink port** o **pNIC**) associati a quelli fisici (che forniscono connessione tra rete fisica e virtuale).
###### VM driver
L’OS si interfaccia con i dispositivi sull’hw virtuale installando i relativi driver software.
###### Altro
- La VM funziona come un file di dati: usabile da + pc e spostabile tra essi.
- Quando la VM fa richiesta all’host, l’hypervisor riporta la richiesta sul fisico e salva le modifiche in cache, fatte in tempo pressoché reale.
### Tipi di Virtualizzazione
##### Virtualizzazione di dati
Qui, dati distribuiti su più ambienti sono consolidati su uno solo, così da gestirli dinamicamente rendendoli disponibili su richiesta.
##### Virtualizzazione di desktop
Questa consente ad un admin centrale di distribuire desktop virtualizzati su diversi host, oltre a permettere di eseguire in bulk aggiornamenti, configurazioni e controlli su tutti i desktop.
##### Virtualizzazione di server
I server devono elaborare un n° elevato di attività diverse. Questa permette di partizionarli e distinguerne le caratteristiche e le funzioni.
##### Virtualizzazione di OS
Si fa nel kernel (è utile per affiancare ambienti con OS diversi) e distribuisce degli OS virtuali nella macchina, permettendo di:
-    Ridurre costo tot dell’hw (ne serve meno perché si hanno VM), 
-    Aumentare la sicurezza,
-    Limitare il tempo impiegato per servizi IT (tipo aggiornamenti…)
##### Virtualizzazione di funzioni di rete (NFV)
Separa le funzioni chiave di rete (file sharing, IP configuration...) per distribuirle tra + ambienti. È possibile riunire funzioni in una rete e assegnarle a un (sotto)ambiente, per esempio: in una rete fisica virtualizzo una sottorete per load balancing e controllo di accessi. Questa è la base della "cittadella" in #crittografia.
# Sicurezza informatica
La sicurezza ha il compito di mantenere un sistema funzionante e operativo in ogni momento, garantendo l'accesso ai dati solo al personale autorizzato. Chi minaccia la sicurezza di un sistema è detto generalmente "*hacker*", termine spesso inteso in senso negativo. Gli hacker si dividono in: 
- *White hat* (o *ethical hackers*), che vengono assunti dalle aziende per testare i loro sistemi e la loro difesa,
- *Black hat* (o *crackers*), hacker che compiono azioni illegali e penetrano nei sistemi approfittando delle loro vulnerabilità per un certo tornaconto (personale o meno),
- (*Grey hat*, una via di mezzo tra i precedenti).
### Risk management
Col tempo gli attacchi sono evoluti e incrementati, trovando dalla parte di chi subisce una generale impreparazione e mancanza di infrastrutture di sicurezza. Comunque, nonostante la sicurezza assoluta non esista, le aziende devono fare il possibile per difendersi; quindi si ricorre al ***risk management***.
La gestione del rischio è legata a: 1) la probabilità che un evento accada, e 2) al danno che ne deriverebbe; quindi questa, per la protezione di un sistema informatico, prevede un piano per valutare il rischio di attacchi e i danni che ne deriverebbero. Da ricordare poi è il grado di fiducia (*assurance*) che si è disposti a dare a qualcosa (tipo alla protezione di un firewall o a un software), per cui gli standard della famiglia ISO 27000 impongono criteri a cui attenersi.
### Il Cybersecurity Cube
All'inizio degli anni 90, John McCumber, allora grande esperto di sicurezza informatica, realizzò un modello (detto il "*Cybersecurity Cube*") in cui sono rappresentate graficamente le leve su cui agire per garantire cybersecurity. Questo cubo ha 3 dimensioni:
- 1° dimensione: evidenzia i 3 principi della sicurezza: Confidentiality (Riservatezza), Integrity (Integrità) e Availability (Disponibilità).
- 2° dimensione: si occupa della protezione dei dati nelle loro fasi: durante la Trasmissione, la Memorizzazione e l'Elaborazione.
- 3° dimensione: si concentra sul fattore umano e su competenze/abilità per proteggere i dati: padronanza delle Tecnologie, capacità di definire linee guida e pratiche di sicurezza e la consapevolezza delle minacce sempre dietro l'angolo.
(foto)
### Il triangolo CIA
Il triangolo CIA ha ai suoi vertici 3 elementi che rappresentano gli obiettivi della sicurezza informatica, ovvero:
##### Confidentiality (riservatezza)
Garantisce che i dati siano disponibili solo a chi è autorizzato, cosicché gli altri non possano intercettarli e manipolarli/usarli. Ciò è fatto con crittografia, auth, privilegi e controllo degli accessi.
##### Integrity (Integrità)
I dati, durante tutte le loro fasi e modalità d'uso, non devono essere alterati e devono essere riconducibili a un'origine certa (non ripudio, questo grazie a *checksum* e *hashing*).
##### Availability (Disponibilità)
Bisogna garantire che i dati siano sempre accessibili nonostante la situazione nei modi e tempi prestabiliti. Le minacce sono varie, ma per evitare problemi di indisponibilità si usano sistemi ridondanti e di backup + manutenzione e aggiornamento di hw e sw + piani di *disaster recovery*.
### Vulnerabilità
Questa è legata ai punti deboli di un sistema (quali pw debole, configurazioni sbagliate, errato controllo degli accessi...) che creano delle falle nella sicurezza (*security hole*) attraverso cui è facile attentare alla sicurezza dei dati. Questi:
- Da una parte potrebbero essere fonti di minacce che cercano di compiere azioni mirate al fine di compromettere le risorse,
- E dall'altra errori involontari o disastri naturali che danneggiano i dati o le infrastrutture.
Il MITRE fornisce un elenco di **vulnerabilità** (*Common Vulnerabilities and Exposures* - **CVE**) e di **debolezze** (*Common Weaknesses and Exposures* - **CWE**) sempre aggiornato.
##### Termini di cybersecurity
- **Asset**: insieme di beni necessari che vanno protetti,
- **Risk**: prodotto di probabilità che un evento dannoso si verifichi e il suo impatto,
- **Vulnerability**: è una debolezza interna e intrinseca di un sistema informatico (tipo CVE-2016-5195, le *race conditions* in Linux),
- **Weakness**: sono errori che possono condurre a vulnerabilità (tipo CVE-120, il *Classic Buffer Overflow*),
- **Threat**: le minacce sono eventi esterni a un sistema che violano qualche obiettivo di sicurezza (volontariamente o meno),
- **Exploit**: è il tentativo di sfruttare una vulnerabilità,
- **Attack**: attività volontaria svolta da un hacker che concretizza una minaccia sfruttando una vulnerabilità. Divisi in:
	- Passivi: rubano info riservate spiando il traffico e non compiendo azioni dirette, tipo *sniffing* o *port scanning*,
	- Attivi: prevedono azioni intenzionali, come alterazioni di messaggi o attacchi DoS (*Denial of Service*).
- **Contromisure**: azioni e processi che permettono di ridurre o eliminare le vulnerabilità.
##### Minacce
- Fisiche: sono tutti i possibili malfunzionamenti verificabili nei dispositivi + eventi naturali distruttivi,
- Di rete: sono i malfunzionamenti della rete (danni a cavi, nodi non auth in rete, danni a router e switch, assenza di crittografia, *sniffing*...),
- Al sw di sistema (OS e DBMS): sono eventuali carenze nella gestione della sicurezza dell'OS (errori di periferiche, dischi o memoria) che possono danneggiare anche i DBMS e interrompere il servizio,
- Di fattore umano: ovvero rischi legati all'intervento umano sul sistema; è il livello + critico per l'imprevedibilità del comportamento delle persone, sia intenzionali che non.
###### Dove colpisce un attacco
Anni fa gli attacchi sfruttavano le debolezze dei dispositivi (USB, dischi, Wi-Fi non protette...) e le aziende si difendevano come potevano con firewall e DMZ. Oggi la situa è cambiata per l'aumento di rischi e minacce, soprattutto per l'IoT.
### Tipi di attacchi
Gli attacchi informatici si classificano in 2 (3) categorie:
##### Malware (e keylogger)
I *malware* sono programmi malevoli con varie funzioni pericolose; ci si protegge da essi con antimalware e antivirus.  Si distinguono in:
- Virus: si agganciano a programmi esistenti variandone la dimensione e si caricano in memoria centrale dove stanno residenti per poi infettare altri programmi e file con cui si diffondono. 
- Worm: programmi autonomi che sfruttano bug di programmazione e usano l'OS della macchina per eseguiti (o anche l'utente li esegue).
- Trojan: sw che si spacciano per programmi utili ma che nascondono altre intenzioni, come alterare dati e programmi e sono spesso scaricati inconsapevolmente perché contenuti in giochi, applicazioni non attendibili...
- Ransomware (o CryptoLocker): infettano i sistemi, ne crittografano i contenuti e richiedono un pagamento per decrittarli.
- Keylogger: sono programmi molto leggeri che registrano ciò che l'utente scrive sulla tastiera passando inosservati; quindi rendono semplice il furto di password e dati sensibili. Sono di 2 tipi:
	- Hardware: questi si collegano al cavo della tastiera intercettando ciò che passa,
	- Software: questi sono installati di nascosto nel pc.
##### Attività di hacking
- Spyware: sw che raccolgono in segreto info sugli utenti tramite internet, per scopi pubblicitari.
- Adware: sw integrati in programmi gratuiti che inseriscono annunci pubblicitari in essi. talvolta fungono anche da spywares.
- Phishing: consiste nell'invio di email fraudolente a utenti, spacciandosi per banche o enti, cercando di truffarli o rubargli l'identità (vittima clicca link e mandata su un sito clone dove mette info personali).
- Backdoor: sono installate da malware su OS, app e servizi, e aprono una "porta" per accedervi da remoto o raccoglierne i dati (anche per usi leciti di debug).
- Spam: sono email non richieste con materiale pubblicitario e link pericolosi, spesso sgrammaticate.
- SQL injection: consiste nello sfruttare errori di programmazione e la superficialità dei dev nel controllo dei dati immessi nelle app (soprattutto tramite campi input di form web). Senza controllo, qualunque cosa ci sia scritta nel campo è iniettata nel db e con certi parametri può anche permettere di visualizzare l'intero db.
- Man in the Middle (MITM): è un attacco basato sullo spionaggio che prevede un *middleman* che si pone tra mittente e destinatario di una conversazione e che ne intercetta i dati, eventualmente alterandoli.
- Zero-day exploit: è un attacco che si basa sulla rapidità di attacco da quando si scopre una vulnerabilità, sperando che la vittima non abbia ancora aggiornato (o avuto il tempo di aggiornare) il sistema.
- Denial of Service (DoS): è un attacco di *brute force* che sovraccarica un server inondandolo di richieste e impedendogli di rispondere a quelle legittime. Se tanti pc sferrano un'attacco coordinato, allora si parla di DDoS (Distributed DoS).
- Ping of death: si invia una serie ripetitiva di ping di dimensioni + grandi del max previsto bloccando l'host ricevente.
- Mail bomb: si invia una grande quantità di email di grosse dimensioni così da affossare il mail server e impedire agli utenti l'accesso al servizio.
- Attacchi TCP/IP:
	- IP spoofing: si altera il valore del campo "Source Address" di IP per far credere che il pacchetto sia stato inviato da un host attendibile.
	- Hijacking: modifica gli header TCP e IP dirottando l'utente su un sito pirata.
	- Port scanning: sono inviati dei messaggi che sondano (*probing*) e trovano i servizi associati alle porte well-known.
- SYN flood: qui un client ostile inonda un server di pacchetti TCP con il flag SYN attivo e IP falsi, facendo rispondere con SYN/ACK e quindi allocare risorse al server, però non rispondendo con il pacchetto ACK; quindi non si completa il 3-way handshake e le comunicazioni rimangono aperte fino alla paralisi del server.
- Social engineering: è la capacità di spacciarsi per ciò che non si è, convincendo e manovrando gli altri per estrapolare loro info riservate (per contrastarla servono precauzioni: non dare pw, chiedere tessere e id...).
- Advanced Persistent Threats (APT): è un tipo di attacco complesso e mirato il cui scopo è introdursi nei sistemi per rimanervi e strappare le informazioni senza che la vittima ne sia consapevole. Questi attacchi sfruttano l'ingegneria sociale al massimo per penetrare nei sistemi e aprirvi delle backdoor così da rimanere in essi il + possibile e controllarli.
### Input vulnerabilities
L'input utente è spesso ciò che viene usato per sfruttare vulnerabilità di sistemi; alcuni esempi sono:
##### Buffer overflow
Questo è una debolezza che è legato alla gestione della memoria e si riscontra quando in un programma si tenta di scrivere oltre la dimensione del buffer (tipo quando eccedi i limiti di un array) andando a scrivere nelle aree di memoria adiacenti e provocando danni devastanti.
##### SQL injection
Come già detto, con la SQL injection si rischia di poter ottenere l'intero db; basta infatti inserire "OR 1 = 1" in un campo username di un form e la query, se non parametrizzata, verrà eseguita nel db ritornando tutti gli utenti in quanto la condizione è sempre vera per ogni riga. Per proteggersi è necessario parametrizzare le query o fare diversi controlli sui dati inseriti.
##### OS command injection
Bisogna prestare attenzione anche alle applicazioni che eseguono dei file per esempio ".sh", che eseguono delle istruzioni di OS e che se intercettati, potrebbero venir alterati e far eseguire codice fraudolento con privilegi.
##### Cross-site scripting (XSS)
Queste vulnerabilità permettono a hacker di inserire script dannosi in siti e app, per inserire malware nei browser e raccogliere info.
### Strumenti di monitoraggio e attacco
Wireshark, shodan, ping sweep, port scan, NMAP e ZENMAP.
### Progettare la sicurezza
Il problema della **sicurezza** va affrontato a livello **manageriale** definendo un piano con politiche di sicurezza non solo **tecniche** (tipo antivirus e crittografia) ma anche **organizzative** (se impiegati scrivono pw su foglietti e li lasciano in giro cosa si fa?). Serve quindi un metodo preciso e strutturato, che è rappresentato in un documento che definisce quali sono i problemi e come risolverli (+ why piano, parti coinvolte, comportamenti, metodi auth, storico e come gestire attacchi).
#### Politiche di sicurezza
Plan (identifica/analizza problema + pianifica azioni correttive) - Do (si attuano le azioni + si attivano test) - Check (si verificano risultati confrontandoli con aspettative) - Act (rileva/controlla risultati buoni + add fattori correttivi x migliorare).
#### Analisi dei rischi
Per identificare la chance di incidenti o attacchi, un'azienda analizza il rischio concentrandosi sulle **probabilità che l'evento accada** e sul **danno che ne deriverebbe**. Per questo occorre:
- Stimare il valore degli asset e le loro vulnerabilità,
- Considerare minacce intenzionali/accidentali e interne/esterne assegnando loro un grado d'importanza.
Mettendo in relazione la probabilità di incidente e il relativo danno, si ottiene un grafico con una curva che discrimina il rischio accettabile da quello che non lo è.
(foto)
##### Modalità di approccio del rischio
Il ***risk management*** presuppone **5 modalità** di approccio del rischio, sancendo che esso può essere:
- **Evitato**: non attuando l'attività o delegando il servizio a esterni (*outsourcing*), (per rischio inevitabile, ridurne l'impatto con *disaster recovery*),
- **Accettato**: se il rischio è sostenibile,
- **Mitigato**: riducendone l'impatto (tipo con firewall e regole di accesso),
- **Affrontato**: preparandosi a fronteggiarlo con delle contromisure (tipo backup),
- **Trasferito**: delegando ad altri soggetti l'attivitò.
### Standard
I dati sensibili sono 1 dei maggiori fattori di rischio per le aziende poiché soggetti ad attacchi e incidenti. La famiglia di standard **ISO 27000** (46 standard) definisce delle norme per migliorare la sicurezza dei dati aziendali. Comprende:
- **ISO 27001**: avente i requisiti di implementazione per un ISMS (*Information Security Management System*),
- **ISO 27002**: discute i controlli di sicurezza attuabili dalle aziende per implementare la valutazione del rischio,
- **ISO 27017 e 27018**: con regole per la protezione di dati sensibili nel cloud e online,
- **ISO 27701**: copre il PIMS (*Privacy Security Management System*).
### GDPR
Il **GDPR** (o *General Data Protection Regulation*) è in funzione dal **2018** in tutti gli stati UE e contiene diverse novità, in particolare si rivolge alle imprese che trattano i dati di cittadini europei sia che siano nell'UE sia che siano estere.
# Cloud Computing
### Cos'è?
Il **cloud computing** è una tecnologia che permette (a dei provider) di **fornire dei servizi on-demand** agli utenti finali attraverso **internet** e per mezzo di risorse hw e sw (dei provider).
**On-demand** = a richiesta, ovvero, l'utente paga solo per ciò che usa.
##### Chi è coinvolto?
Da una parte c'è il **provider dei servizi cloud**, colui che li rende disponibili tramite internet, mentre dall'altra c'è l'**utente finale** che può accedervi dovunque e in qualsiasi momento.
##### Dove si trova?
Le infrastrutture di cloud computing di solito sono situate in **datacenters** (o in spazi dei provider), dove è possibile offrire continuità di servizio e < costi di esercizio e manutenzione per l'uso di tecniche di virtualizzazione, ridondanza e disponibilità.
##### Caratteristiche + On-premise vs Cloud computing
Caratteristiche fondamentali del cloud computing sono l'**affidabilità** e la **scalabilità**. È possibile aumentare i nodi o potenziare CPU/RAM dei server a seconda delle necessità. Tutto ciò grazie alla virtualizzazione delle risorse e alle VM su cui si basa l'infrastruttura.
Non tutto è cloud computing, infatti sono possibili:
- **App on-premise**, ovvero distribuite su server o pc locali,
- **App cloud**, distribuite in internet e hostate nell'infrastruttura di un provider.
### NIST Documentation
Il **NIST** (*National Institute of Standards and Technology*) ha definito in un documento dei principi e metodi per lo sviluppo di sw come servizi cloud. Al suo interno vi sono **5 caratteristiche base**:
#### Modello dei servizi
Definisce i **tipi di servizio** forniti da un cloud provider, aggregabili in 3 classi:
##### IaaS
(O *Infrastructure-as-a-Service*) è un modello di distribuzione in cui viene fornita l’**intera infrastruttura informatica** come servizio **on-demand**. In questo l'utente può ottenere gestire delle **VM** coi relativi **storage** e componenti di **rete** nell'infrastruttura fornita, così da poterci anche installare le proprie app ed erogare servizi propri. 
##### PaaS
(O *Platform-as-a-Service*) è un modello di distribuzione col quale si mettono a disposizione intere **piattaforme di elaborazione**, dotate di **OS** e linguaggi per lo sviluppo di app (con anche database e librerie). L’utente gestisce il sistema e sviluppa applicazioni senza doversi preoccupare di mantenere l’infrastruttura hw e sw.
##### SaaS
(O *Software-as-a-Service*) è un modello di distribuzione di <u>app</u> **on-demand** come servizi. In questo, la sicurezza e l'infrastruttura hw sottostante sono a carico del **provider**, mentre gli utenti possono accedere all'app tramite **browser** e usarla (+ eventualmente configurarla), ma non possono controllarne l'infrastruttura o le funzionalità.
#### Modello di distribuzione
Definisce delle **caratteristiche del cloud** (tipo natura, scopo, luogo...) e NIST ne da **4**:
##### Cloud pubblico
Qui i **servizi cloud** sono **pubblici e accessibili da una piattaforma del provider**. L'hw risiede in una **sede del provider**, il quale fornisce le risorse tramite internet. (Un esempio è AWS).
Il *public cloud* è il modello **più comune**, è molto flessibile ed un’ottima soluzione per le aziende che non possono permettersi un datacenter. Ci sono però utenti che temono **vulnerabilità** e perdite di dati in quanto non si ha controllo diretto sull’infrastruttura.
##### Cloud privato
Questo fornisce servizi a una **specifica azienda**. L'**infrastruttura** (di solito un datacenter virtuale) può essere **sia di un provider sia dell'azienda** e può trovarsi **all'interno o all'esterno di quest'ultima**; tuttavia, questa e i servizi sono **sempre** gestiti **in una rete privata dell'azienda**. 
**Vantaggio**: mantiene i dati all'interno della struttura organizzativa aziendale, risolvendo quindi il problema di privacy e sicurezza dei cloud pubblici. **Svantaggio**: non è facilmente accessibile a possibili utenti esterni.
##### Cloud ibrido
Questo è composto dall'**unione delle caratteristiche di cloud pubblico e privato**, cercando al contempo di ponderarne gli svantaggi. Esempi:
- Si possono **dividere i servizi gestiti in un'azienda**, destinando al **cloud pubblico** quelli con **< esigenze di sicurezza** (tipo servizio email...); mentre quelli che eseguono operazioni **critiche** (tipo trattamento dati sensibili o transazioni) verranno gestiti nel **cloud privato**.
- Si può mantenere il **cloud privato** per la **normale gestione delle applicazioni** e **aggiungere** le funzionalità del **cloud pubblico quando vi sono picchi** nelle richieste alle applicazioni.
- Un'azienda può anche scegliere una soluzione in **multi-cloud** (usare + provider di cloud pubblici diversi) per > flessibilità e distribuzione delle informazioni.
L'ibrido sembra essere la moda in quanto si possono lasciare info strategiche all'interno (private cloud) e gestire all'esterno (public cloud) le attività meno critiche.
##### Cloud comunitario
Simile al cloud privato con la differenza che i servizi sono riservati a una **comunità di utenti** di aziende che condividono interessi (politiche, sicurezza...). Sia interno che esterno all'azienda.
#### Attributi dei servizi
- **On-demand self-service** 
  Gli utenti finali possono richiedere e accedere ai servizi offerti automaticamente e senza alcun intervento umano necessario,
- **Broad network access**
  I servizi cloud devono essere disponibili in internet e accessibili da diversi sistemi e piattaforme client,
- **Resource pooling**
  Le risorse fornite sono sottoposte a pooling, ovvero assegnate dinamicamente in funzione delle esigenze agli utenti finali,
- **Rapid elasticity**
  Le funzionalità devono essere assegnate e rilasciate elasticamente con costi commisurati in base alle risorse usate,
- **Measured service**
  I servizi devono poter essere misurati/monitorati (come l'attività degli utenti) così da ottimizzarne l'uso e calcolare i consumi.
#### Risorse
Server di elaborazione, storage, reti, servizi, applicazioni...
#### Organizzazione dell'infrastruttura
Architettura distribuita, virtualizzazione...
### Problemi e rischi
I sistemi di cloud computing sono criticati per vari **rischi** legati a:
##### Sicurezza e privacy
Usare servizi di cloud computing espone a vari problemi legati alla **privacy** in quanto:
- I dati sono salvati in ***server farm*** spesso <u>non</u> nello stesso paese dell'utente e in questi casi si ha meno certezza del rispetto della privacy da parte del provider,
- Con i collegamenti <u>wireless</u> il rischio di sicurezza aumenta per la pirateria oltre a rendere difficile il raggiungimento di soluzioni giuridiche in caso di atti illegali,
- Per aziende invece i dati potrebbero essere esposti a eventuale **spionaggio industriale**.
###### Esempio:
Il problema è la pubblica amministrazione, perché in casi dove le forze dell’ordine devono accedere a dei dati per avere informazioni sensibili, essendo questi protetti da password per esempio in un IPhone, la Apple non riconosce il diritto di questi di accedere ai dati in quanto non è tenuta a seguire norme di altri paesi se non la sua aziendale.
##### Problemi di interazione politico-economici
- Sempre causati dal fatto che dati pubblici sono raccolti in archivi privati **delocalizzati** dal paese degli utenti in quanto non vi sono garanzie per questi ultimi che i dati siano sempre accessibili.
- Se poi gli archivi sono situati in paesi **ricchi** si rischia l'aumento del ***digital divide*** a scapito dei paesi più poveri.
Maggiori sicurezze vi sono quando il provider è dello stesso paese o di uno con legislazioni simili per privacy e sicurezza.
##### Continuità del servizio
Delegando la gestione dei dati ad esterni, gli utenti si trovano fortemente limitati nel caso in cui i servizi non siano operativi (*out of service*) in quanto tutti i sistemi nonostante ridondanze e personale qualificato sono soggetti a questi tipi di problemi.
##### Difficoltà di migrazione dei dati
Non esistono standard definiti tra gestori di servizi, quindi un eventuale cambio di operatori può risultare complesso e molto dannoso se fallisce.
### Web hosting e housing
**ISP** (*Internet Service Provider*) sono fornitori di **connettività internet** (possono essere **isp**).
**Isp** (stesso ma minuscolo) sono fornitori di **servizi in internet** (hosting, email...).
Web **hosting** e web **housing** sono dei servizi con cui un utente può pubblicare un sito web.
##### Hosting
Prevede la collocazione di un **sito** web **all'interno dei server dell'isp**. Di 2 tipi:
- **Hosting condiviso**, quando il server in cui un sito è hostato ne può accogliere molti altri,
- **Hosting dedicato**, quando il sito (perlopiù aziendale) ha le risorse di un server dedicate e garantite per sfruttare tutte le potenzialità del sw e dell'hw dell'isp.
##### Housing
Questo servizio permette di **ospitare un server del cliente presso l'isp** (sia proprietarie che in affitto) con possibilità di configurarli come si vuole.
# Crittografia
La **crittografia** è la **disciplina che studia le tecniche matematiche per rendere sicuri i dati** in termini di **confidenzialità**, **integrità**, **auth** e **non ripudio**. Strumenti usati sono **cifrari** e funzioni **hash**.
Il suo **scopo** è **mantenere segrete le info**, trasformando il messaggio originale (in chiaro) in uno cifrato per mezzo di algoritmi di crittografia.
## Tipi di crittografia
### Crittografia simmetrica
Gli algoritmi a **crittografia simmetrica** (a **chiave segreta**) sono degli algoritmi noti che prevedono che la **codifica** e la **decodifica** dei **dati** avvengano usando la **stessa chiave** (per questo "chiave **simmetrica**"), detenuta da entrambi gli interlocutori.
<font color="#aaaaaa">(Un messaggio (m) viene crittografato (C) con un algoritmo con chiave (k), ottenendo il messaggio crittografato $D_k(m)$. Questo viene decriptato (D) usando lo stesso algoritmo con la stessa chiave (k), ottenendo il messaggio originale: $D_k(C_k(m))=m)$</font>.
![[Pasted image 20240305192435.png]]
Questa crittografia però necessita dello **scambio di chiavi**, il che **non è sicuro**.
### Crittografia asimmetrica
Nel 1976 venne introdotta la **crittografia asimmetrica** (o a **chiave pubblica**), che adotta sempre algoritmi pubblici, ma che usano **2 chiavi diverse per cifrare e decifrare il messaggio**. Qui vi sono 2 tipi di chiavi:
- Quelle **pubbliche** (*kpb*), chiavi di cifratura che il **destinatario** ricava e **condivide**. Il destinatario invia la sua al mittente così che questo **critti il messaggio con essa**, rendendolo **decrittabile solo con la sua *kpr***. 
- Quelle **private** (*kpr*), chiavi segrete di decodifica **non condivisibili** posseduta **solo dal destinatario**. Sono **associate ad altre *kpb*** e vengono usate dal destinatario per **decrittare messaggi crittati con la *kpb* associata**.
La sicurezza del metodo si basa sul fatto che ricavare la chiave privata dalla chiave pubblica sia troppo **complesso**. Quindi: $D_{kpr}(C_{kpb}(m))=m$.
![[Pasted image 20240305192755.png]]
### L'algoritmo RSA
L'algoritmo **RSA** (Rivest, Shamir, Adleman) si basa sulla teoria di scomposizione in **fattori primi** di un numero e usa sempre una coppia di chiavi generate in modo che sia impossibile ricavare una dall'altra. Pubblicato nel 1978, era considerato sicuro fino a poco tempo fa e prevede 3 passi:
##### Determinazione *kpb* e *kpr*
Si trovano chiave pubblica e privata in 5 step:
1) Si scelgono 2 numeri *p* e *q* primi e molto grandi (almeno 300 cifre, così grandi per rendere impossibile ricavare i fattori dal prodotto),
2) Si trova $n = p * q$
3) Si trova $m = (p-1) * (q-1)$
4) Si determina un numero *e* primo rispetto a *m* (senza divisori in comune con *m*),
5) Si trova *k* tale che: $[(e * k) |m|] = 1 \rightarrow k = (m * h + 1)/e$ con *h* intero e positivo.
Quindi:
- La *kpb* è data dalla coppia (*e, n*),
- La *kpr* è data dalla coppia (*k, n*).
##### Cifratura del messaggio
Il messaggio viene cifrato con la *kpb*. 
Per evitare attacchi basati sull'analisi delle frequenze, il messaggio è convertito in binario e diviso in blocchi di *g* bit, con *2g* < *m*; e ogni blocco è cifrato con la *kpb*. Se *M* è un blocco, un blocco cifrato *C* è: $C = (M_{e}|n|)$.
##### Decifratura del messaggio
Il messaggio ricevuto viene infine decifrato dal destinatario con la sua *kpr*, questo anche per i blocchi, che decifrati sono: $M = (C_{k}|n|)$.
#### Crittografia a chiave di sessione
Poiché gli **algoritmi a chiave asimmetrica** sono molto **complessi** e **onerosi**, alcune applicazioni li usano per scambiarsi **solo 1 chiave segreta** da usare per la **sessione** (**chiave di sessione**, che cambia ad ogni sessione).
## Sicurezza delle reti
### I dati
La sicurezza in archiviazione e trasmissione dati richiede adeguate misure di protezione. La tecnica di base è la **crittografia** nelle sue 2 forme più diffuse: **simmetrica** e **asimmetrica**; a questa sono legati argomenti come la **firma digitale** e la **certificazione**. 
Il problema è rilevante quando si vanno a trattare **dati sensibili** (tipo per i pagamenti digitali) con operazioni che richiedono un certo livello di sicurezza. Garantire la protezione è possibile con delle funzionalità implementate nel punto di accesso tra il provider e l'internet (secondo la ISO Security Architecture) divise in 5 classi:
##### Autenticazione
**Verifica che chi richiede un servizio sia effettivamente chi dichiara di essere**; infatti si basa sul fatto che chi deve autenticarsi deve dimostrarlo con qualcosa di riservato.
Auth con usr e pwd è poco affidabile per un sistema di rete in quanto, a differenza di auth in app, qui la trasmissione di pwd a chi autentica espone a rischi; perciò è necessaria la **crittografia**.
##### Controllo degli accessi
Quando l’auth è fatta, è possibile **limitare gli accessi degli utenti alle risorse**:
- In caso di pc, ciò è riferito a risorse del file system (directory, file, driver, permessi di lettura, scrittura, esecuzione…),
- In caso di rete invece,  si controlla l'accesso e la visibilità degli altri pc in rete (e quindi i loro servizi) mediante firewall.
##### Riservatezza
Quando si usa un servizio, bisogna **assicurarsi che i dati scambiati tra mittente e destinatario non siano usati da terzi**. Anche se mira ad evitare che i dati siano estraibili dal traffico, la riservatezza è generalmente interpretata come **crittografia** dei dati.
##### Integrità
I dati devono comunque poter **raggiungere la destinazione senza modifica di terzi**; quindi anche per info pubbliche, bisogna verificare la corrispondenza di quanto ricevuto con quanto trasmesso.
C'è quindi bisogno di un **codice di controllo** che rileva alterazioni dei dati il quale, per garantire l'integrità, può viaggiare anche non protetto; ma per garantire la sicurezza, bisogna fare in modo che solo il mittente lo possa generare per evitare manomissioni.
##### Non ripudio
Per le comunicazioni (tipo transazioni) bisogna **garantire che le parti di uno scambio non neghino di aver preso parte allo stesso**. Ciò si risolve con **firme digitali** sempre crittografate.
#### Sicurezza delle comunicazioni
Di queste: **auth, riservatezza e integrità**, riguardano aspetti di protezione **indipendenti dai dati**. Perciò le loro funzionalità sono fornite e **implementate da apparati di rete** (firewall...) o **programmi** generici (browser...).
#### Sicurezza delle applicazioni
Le restanti: **controllo degli accessi e non ripudio**, sono **legate alle app e ai dati** scambiati.
- Le modalità di controllo degli accessi variano in base al OS usato, dall'applicazione...
- Per il non ripudio invece le modalità per eseguire la **firma digitale** sono standard, le infrastrutture necessarie sono diffuse e sono usate per proteggere comunicazioni interpersonali e transazioni.
### Firme digitali
Queste funzionalità però non garantiscono del tutto l'affidabilità dei documenti perché bisogna sapere **chi ne è l'autore**, per garantirne l'**integrità e impedirne il ripudio**.
Una soluzione a ciò è la **firma digitale** (*digital signature*), che usa l'algoritmo **RSA a chiave pubblica** per **cifrare un documento con la *kpr* del mittente** rendendolo **decifrabile con la *kpb* associata** in modo da essere certi dell'identità del mittente.
Dato che il messaggio è crittato con la *kpr* del mittente, chiunque potrà leggerlo (dato che la *kpb* è pubblica); quindi per garantire sia segretezza che autenticazione, il **mittente** deve:
- **Crittare** il messaggio **con la propria *kpr*** (autenticità),
- **Crittare** il messaggio firmato **con la *kpb* del destinatario** (segretezza).
Mentre il **destinatario** dovrebbe:
- **Decrittare** il messaggio con la **propria *kpr*** (segretezza),
- **Decrittare** il messaggio con la ***kpb* del mittente** (autenticità).
#### Digest
**Crittografare l'intero messaggio è oneroso e troppo lungo**, perciò si usa il ***digest***: un **riassunto** estratto dal messaggio originale che **crittato va a costituire la firma**. Questo si ottiene applicando funzioni di ***hash*** al messaggio originale, ottenendo quindi una stringa molto **+ corta**, **dipendente da esso** e che **identifica univocamente il documento e il mittente** (siccome è **impossibile modificare il messaggio senza modificarne l'hash**).
##### Step
- **Si ricava il *digest*** dal messaggio,
- Il ***digest* viene cifrato con la *kpr* del mittente** (autenticità),
- Il **messaggio +** la firma (***digest*** cifrato) sono **trasmessi**,
- Il **ricevitore ricalcola il *digest* dal messaggio** e lo **confronta con quello estratto dalla firma** (ottenuto con la *kpb* del mittente),
- **Se** i 2 *digest* sono **uguali**, il **documento è integro e la firma è autentica**.
![[Pasted image 20240305221655.png]]
###### Approfondimento
Per scoprire modifiche apportate da esterni si usano funzioni di *hash*, che rendono impossibile modificare il testo senza modificarne l'*hash* e hanno bassissima probabilità di avere 2 *hash* uguali.
Tra gli algoritmi più usati c'è **MD5** (Message Digest Algorithm 5, oggi non del tutto sicuro) e **SHA** (Secure Hash Algorithm). Quest'ultimo produce un *digest* di lunghezza fissa da un messaggio di lunghezza variabile ed è sicuro perché:
- La funzione **non è reversibile** (**non si può tornare al messaggio dal *digest***),
- **Non deve essere possibile creare 2 messaggi diversi con lo stesso *digest***.
A questa famiglia appartengono SHA-1, SHA-256 e SHA-512.
### Certificati digitali
Sono dei **file** con **validità temporale limitata**, che **garantiscono l’identità di un soggetto** (dispositivo o persona che sia) **assicurando l'auth della sua *kpb***. (In pratica sono degli alter ego dei documenti d'identità nella vita reale). Sono usati ogni volta per problemi di sicurezza tipo:
- Quando si forniscono/usano servizi online con pagamenti e consultazione di dati riservati,
- Quando si scambiano email, dove il mittente che compare non assicura niente, ma è riconosciuto con la firma digitale,
- Quando si vuole verificare la validità di documenti caricati in / scaricati da internet.
##### CA
I certificati digitali sono rilasciati dalle **CA** (*Certification Authorities*) o da enti detti "autorità di rilascio certificati autonome". Le CA rilasciano certificati agli utenti che ne fanno richiesta dopo una verifica della loro identità e mantengono:
- Un **registro pubblico dei certificati**, che permette a chiunque di verificare la validità di un certificato,
- Una ***Certification Revocation List***, una lista dei certificati revocati.
### Protocollo SSL/TLS
Garantisce la **sicurezza** di un collegamento garantendone:
- **Privatezza**: con la crittografia usata dopo un **handshake iniziale** per definire una **key segreta** (perché per crittografare i dati si usa la crittografia simmetrica, tipo DES, RC4...).
- **Autenticazione**: l’identità delle connessioni è autenticata con la **crittografia asimmetrica o a key pubblica** (tipo RSA...) così che client sono sicuri di parlare col server giusto (entrambi da certificare).
- **Affidabilità**: il livello trasporto include un ***integrity check*** del mess basato su un **MAC** (*Message Authentication Code*) che usa funzioni **hash sicure** (SHA, MD5...) per verificare che i dati non siano stati alterati durante la trasmissione.
L'SSL/TLS ha lo scopo di fornire **riservatezza** e **affidabilità** alle comunicazioni. Si compone di 2 strati:
- **SSL Record Protocol** (inferiore), usato per la **trasmissione dei messaggi protetti**,
- **SSL Handshake Protocol** (superiore), che si **interfaccia sull'SSL Record Protocol e permette a client e server di autenticarsi a vicenda negoziando algoritmi di crittografia e chiavi**.
# VPN
### Cosa sono?
Una **VPN** (*Virtual Private Network*) è una **rete privata virtuale** che **usa una rete pubblica** per **collegare** tra loro **pc remoti come se** appartenessero alla **stessa rete locale**. Le VPN sono:
- "**Private**" perché la comunicazione fa apparire le **LAN remote come se comunicassero su una stessa rete privata** (condividendo gli stessi indirizzamenti privati e le policy di sicurezza).
- "**Virtuali**" perché i **collegamenti sono logici (non dedicati/fisici) sopra un'infrastruttura di rete pubblica** (solito internet, ma aziende si appoggiano a reti fornite da un operatore con specifici protocolli).
Le VPN permettono di creare dei "**tunnel virtuali**" in cui i dati viaggiano **cifrati** per garantire **sicurezza** in una rete pubblica come internet.
### Vantaggi
I vantaggi delle VPN sono tanti:
- **Riduzione dei costi**: non serve affittare linee dedicate e costose per comunicare tra sedi in sicurezza,
- **Uso di risorse preesistenti**: si usano i normali collegamenti ad internet già presenti,
- **Flessibilità di accesso alle risorse**: (con permessi), si può accedere a una risorsa aziendale indipendentemente dalla sede,
- **Connessioni sicure**: le trasmissioni sono cifrate,
- **Scalabilità**: è semplice aggiungere sedi alla rete aziendale,
- (Supporto **voce e video cifrati**),
- (**Semplicità**).
### Perché usare una VPN?
Sono 2 i motivi principali per usare una VPN:
- **Necessità di proteggere la privacy con l'anonimato** e di **aggirare *region locks*** che bloccano l'accesso a risorse (questo con ***VPN ad accesso remoto***),
- **Esigenza di collegare sedi lontane** da quella centrale dell'azienda **in modo sicuro** (questo con ***VPN site-to-site***).
##### VPN ad accesso remoto
Le **VPN ad accesso remoto** consentono (garantendo privacy) di **raggiungere risorse in rete altrimenti irraggiungibili**. Prevedono la creazione di un **tunnel VPN** (**crittografato**) tra: 
- Un **client che acquista il servizio VPN da un ISP** e che **installa** un "**VPN client**" **impostandoci** il **server del provider**,
- Un **server VPN del fornitore** a cui sono **mandati i messaggi crittografati** che **decritterà e invierà in internet dal proprio IP, mascherandone l'origine**. 
(Questo è utile per **eludere** le risorse protette da ***region lock*** e pere i dipendenti fuori sede che possono accedere alle risorse aziendali tramite un client VPN aziendale).
##### VPN site-to-site
Le **VPN site-to-site collegano** (garantendo sicurezza) **2 o + LAN dislocate utilizzando internet**. Il tunnel qui è stabilito tra dei **CPE** (*Customer Premises Equipment*, ovvero **router**/gateway) **delle sedi remote** per impedire l'intercettazione dei messaggi trasmessi. Qui i dispositivi **non necessitano di un client VPN**, ma inoltrano i messaggi attraverso i **router VPN**. Le VPN site-to-site sono ulteriormente classificabili in:
- **Intranet**, reti di uffici/sedi di una stessa azienda collegati per mezzo di una VPN,
- **Extranet**, dove la VPN connette l'azienda a un partner o cliente.
### Tipi di VPN
Le VPN possono usare **2 tipi di meccanismi per trasferire dati** (la combinazione di queste 2 origina una *hybrid VPN*):
##### Trusted VPN
Questo prevede di **appoggiarsi a un ISP che crea dei tunnel sui i suoi circuiti privati come se fossero virtuali**. (La soluzione + diffusa si basa sul protocollo **MPLS**, in cui a ogni pacchetto è assegnata una label che rende il traffico efficiente in quanto ordina i pacchetti fornendogli delle priorità).
**Vantaggi**:
- Il clie**nte non si preoccupa del servizio** (fa tutto l'ISP),
- Garantire la **sicurezza è a carico dell'ISP**,
- La **QoS è anch'essa gestita dal fornitore**,
- **Tempi** di ***fault recovery* brevi** per algoritmi di rete basati su priorità,
- **Cliente gestisce l'indirizzamento IP** (come se fosse tutto su una LAN privata logica).
**Svantaggi**: **costi elevati e rigidità**.
##### Secure VPN
Questo prevede di **sfruttare la rete pubblica crittografando i dati che viaggiano**. Sulle funzioni di rete fornite da un ISP, l'utente sovrappone una propria ***overlay network***, una topologia logica in cui definisce lui dei collegamenti punto-punto. (Quindi i dati viaggiano in un tunnel virtuale protetto, ma non ci sono imposizioni su quale percorso devono seguire). La **sicurezza è data da altri protocolli tipo IPsec**.
In questa categoria di VPN rientrano le ***clientless* o *web* VPN**, che usano **SSL** per permettere a utenti dislocati di accedere a risorse in internet da ovunque. Non necessitano aperture di porte... ma solo auth.
### La sicurezza nelle VPN
Le VPN devono garantire:
- **Riservatezza**, fatta **crittografando i dati**. Per questa si usano dei protocolli tra cui **IPsec, L2TP e SSL**.
- **Integrità**, (**non permettere alterazioni** di dati nel transito). Esempio: IPsec impedisce modifiche ed elimina i pacchetti compromessi.
Serve poi anche **accertarsi dell'identità del mittente** per proteggersi da *spoofing*; infatti quando un utente remoto richiede la creazione di un tunnel, un server AAA verifica certe cose:
- **Autenticazione** ("chi sei"): si verifica l'identità di un utente (tipo con username e password),
- **Autorizzazione** ("cosa puoi fare"): si verifica a quali risorse l'utente può accedere e gli si da l'accesso solo a quelle,
- **Accounting** ("cosa hai fatto"): traccia l'uso delle risorse dell'utente per fini di sicurezza, statistici e di tariffazione.
In sostanza è la crittografia che garantisce la sicurezza in generale e questa, se applicata a protocolli del modello TCP/IP rende anche quelli superiori sicuri.
#### VPN IPsec
(***Internet Protocol Security***), implementa la **crittografia a livello rete** (quindi fornendo sicurezza al protocollo IP) e permette di creare un **percorso sicuro tra 2 host comunicanti** per mezzo di una **VPN** in una rete non sicura.
##### Protocolli di sicurezza IPsec
IPsec garantisce la sicurezza (riservatezza e auth) con 2 protocolli.
- **AH** (***Authentication Header***), garantisce **auth del mittente e integrità** (ovvero che la sua **identità non sia stata cambiata** da un attacco di *spoofing*), <u>senza</u> però garantire **riservatezza/crittografia**.
- **ESP** (***Encapsulation Security Protocol***), opera sul **messaggio** (**non sul mittente come AH**) e del suo **payload** (**no header**) garantisce **autenticità**, **integrità** e **riservatezza**/**crittografia**.
##### Modalità di incapsulamento IPsec
<u>Entrambi</u> i protocolli (AH e ESP) possono essere implementati nelle **2 modalità di incapsulamento** previste da **IPsec**:
###### Transport mode
Questa è usata per **collegamenti sicuri tra 2 host** (*end-to-end*) **aventi IP pubblico**. **Non** **crea** alcun **tunnel**. Se usata **con AH, garantisce autenticità e integrità di tutto il messaggio**, se no con **ESP garantisce in + la riservatezza ma solo del payload**. Funzionamento: **tra l'header IPv4 e l'header TCP è aggiunto un *IPsec header*** (questi collegati da *next header*) che può essere o **AH o ESP**.
(foto?)
###### Tunnel mode
Questa è usata per i collegamenti **VPN tra reti private che accedono a router pubblici** (*gateway-to-gateway*). Viene creato un **tunnel** per il transito sicuro dei pacchetti IP, che vengono completamente **cifrati** e **incapsulati** in un altro pacchetto, **nel cui header sono contenuti gli IP mittente e destinatario dei 2 router che sono gli estremi del tunnel**. (Con ESP si impedisce di conoscere la sorgente del pacchetto, ottimo grado di riservatezza).
(foto?)
##### Funzioni e protocolli di supporto alla sicurezza
- **SA** (*Security Association*): proprietà che definiscono come realizzare una comunicazione sicura tra 2 host. SA descrive: tipo connessione sicura da instaurare + meccanismi, algoritmi di cifratura e la *kpr* (+ transport o tunnel e AH o ESP).
- **SAD** (*SA Database*): Database delle SA attive di un sistema.
- **SP** (*Security Policy*): regole che informano IPsec di quali flussi di dati devono essere usati da una SA (IP source e dest, porte, AH/ESP, transport/tunnel).
- **SPD** (*SP Database*): db con politiche per gestione pacchetti. Sono: 1) "scarta", scarta pacchetto entrata/uscita, 2) "non applicare", non applica sicurezza in entrata/uscita e 3) "applica", applica sicurezza in entrata/uscita.
- **IKE** (*Internet Key Exchange*): (porta 500 UDP) permette la configurazione automatica delle SA generando dinamicamente chiavi di sessione diverse per ogni blocco dati inviato (se hacker ottiene dato e chiave non fa niente perché il resto dei pacchetti è crittato con chiavi diverse). Scambio di keys IPsec avviene con l'algoritmo DH (Diffie-Hellman, dove le parti si scambiano info su generazione della chiave che poi è protetta con hash).
#### (VPN) SSL
**TLS** (*Transport Layer Security*) / **SSL** (*Secure Socket Layer*) è un protocollo che si colloca tra i livelli **trasporto** e **applicazione**, garantendo una comunicazione sicura (riservatezza e integrità) ai protocolli livello trasporto e applicazione relativi. La sicurezza è data da un meccanismo che configura una **key simmetrica con una crittografia a key asimmetrica** (client critta con una **key segreta di sessione random ogni volta crittografando** il **tutto con la *kpb* del server**). Obiettivo è **garantire**:
- **Riservatezza**, dati protetti con crittografia simmetrica (DES o RC4),
- **Auth**, client e server sono autenticati con crittografia asimmetrica (RSA) e si scambiano certificati,
- **Integrità**, effettuati check sull'integrità del messaggio con funzioni hash (SHA o MD5).
##### Architettura di SSL
SSL opera su **2 strati**:
###### SSL Handshake
Il **livello + alto** che si interfaccia col livello **applicazione**; è **usato per l'handshake** iniziale e si divide in 4 fasi:
1) **Avvio di una nuova connessione**: consente a **client e server di negoziare l'algoritmo di generazione di chiavi**. Client manda un messaggio "*client hello*" con la sua **versione di SSL** e gli **algoritmi** supportati (a volte dopo esser stato sollecitato dal server che gli manda "*hello request*") e il server risponde con un "*server hello*" con **versione SSL e l'algoritmo scelto**.
2) **Auth del server**: qui server manda al client un **certificato** (rilasciato e con firmato digitalmente da una CA) contenente la **sua *kpb*** con "*server certificate*" (ed **eventualmente richiede auth client**). Quando entrambi hanno inviato il proprio certificato e verificato quello dell'altro, il server finisce con un "*server hello done*".
3) **Scambio chiavi di sessione**: il **client genera una chiave di sessione**, la **critta con la *kpb* del server** e gliela **invia** con "*client key exchange*". Poi manda "*change cipher spec*" per dire che i **prossimi messaggi codificati con la chiave inviata**.
4) **Chiusura dell'handshake**: Il **server risponde** al "*change cipher spec*" con lo stesso messaggio, poi il **client chiude** mandando un "*client finished message*" e **stessa cosa fa il server** con un "*server finished message*".
###### SSL Record Protocol
Si poggia sul **livello trasporto** e permette una **conversazione sicura tra le 2 parti**. Prevede che i **dati** siano **frammentati in blocchi**, **compressi e integrati con un MAC** (*Message Authentication Code*) generato con **hash** per l'integrità. Il messaggio prodotto è poi **cifrato con la chiave di sessione**, gli viene **aggiunto un header SSL e viene mandato al livello trasporto**. Il ricevente applicherà il **processo inverso ai blocchi**, quindi li decifra, decomprime, riassembla e passa all'app. 





