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

