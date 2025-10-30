# App e sistemi distribuiti

### Sistema distribuito

Un **insieme di nodi interconnessi** in una rete che **si scambiano messaggi per eseguire algoritmi distribuiti**.

Sito = luogo fisico di una macchina.

Nodo = macchina o sistema in un sito (detto anche host).

Client = nodo che consuma risorse da un server.

Server = nodo che fornisce risorse ad altri nodi.

### Sistemi distribuiti avanzati

###### Resource sharing

Condivisione di file in siti remoti, informazioni processate in un db distribuito e uso di dispositivi hw remoti.

###### Load sharing

Maggiore potenza di calcolo e velocità e load balancing (gestione e suddivisione del carico).

##### Vantaggi

- Reliability: **Identificazione** di siti in failure, **trasferimento** funzioni da un sito in failure e **ripristino** di esso.
- Communication: Scambio di messaggi.
- Flexibility: Rimpiazzo di mainframe con reti di host e < costi.

### Applicazione distribuita

**Applicazione costituita da 2 o + processi eseguiti in parallelo su pc diversi connessi in una rete**.

I processi di una app distribuita cooperano sfruttando i servizi forniti dalla rete e si devono mettere in contatto.

### Layer applicativi

1) Livello presentazione o Front End

Gestisce la logica di presentazione, ovvero le modalità di interazione con l'utente (interfacciamento grafico e rendering delle info).

2) Livello di logica applicativa

Gestisce le funzioni da mettere a disposizione all'utente.

3) Livello di accesso ai dati

Gestisce le informazioni ed eventualmente l'accesso ai db.

Questi (livelli software) possono essere installati su vari livelli hardware, detti **Tier**.

##### Tiers

App può essere configurata come:

###### Single Tiered

Tutti i **livelli ospitati su 1 host**

###### Two Tiered

**Livelli divisi tra 1 client** (che ha il livello **Presentazione**) e **1 server** (che ha il **livello** di **accesso** ai **dati**). Il livello di **logica applicativa** può stare **o sul client o sul server**.

###### Three Tiered

**3 macchine dedicate 1 per livello** (client x presentazione e 2 server per altri 2)

Architettura multi-tier = usati 2 o 3 tier come arch di una app (ES: **browser** \[*Presentazione*] che fa richieste a un **server** \[*Logica applicativa*] che fa richieste a un **DBMS Server** \[*Logica accesso ai dati*]) i livelli adiacenti assumono i ruoli di **client e server** (il **+ vicino a utente è sempre client**, mentre il **più lontano sempre server**)

##### Clients

Thin Client: quando a **livello utente** c'è **solo** livello **presentazione**

Fat Client: quando a **livello utente la logica applicativa si appoggia su quella di accesso ai dati**

##### Ends

Backend: Livello **middleware** che contiene la **combo di logica di accesso ai dati e logica applicativa**

Frontend: Livello **presentazione**

##### Sistemi

###### Centralizzato

Quando **dati e applicazioni sono su un unico nodo elaborativo**. (Tipo architettura a mainframe?)

###### Distribuito

**Insiemi di applicazioni logicamente indipendenti che cooperano per raggiungere obiettivi comuni tramite infrastruttura** di comunicazione **HW** e **SW**

Esso realizza almeno 1 delle seguenti situazioni:

1) Elaborazione distribuita: **applicazioni cooperanti** distribuite su + nodi elaborativi
2) Base di dati distribuita: **database** ospitato su + nodi elaborativi

### Server Farm

**Insieme** (molto grandi) **di pc interconnessi che condividono app e dati**.

Realizzate secondo 2 principi progettuali:

##### Cloning

**Su ogni nodo della farm sono installate le stesse app (duplicandole).**

Le richieste sono poi inviate ai vari client tramite un sistema di **load-balancing** (tecnica che distribuisce il carico di elaborazione tra diversi server).

Per cui: **> scalabilità e affidabilità** di arch nel complesso. I sistemi di load-balancing integrano anche **sistemi di monitoraggio** che **escludono** automaticamente **cluster non raggiungibili**

##### RACS (Reliable Array of Cloned Services)

**Insieme di cloni dedicati a svolgere un certo servizio**, in cui **se 1 si guasta**, **un altro** continua a **erogare** il **servizio**.

Presenti in 2 configurazioni:

###### Shared Nothing

**Dati memorizzati sono duplicati e stanno sul disco di ogni clone.**

**Ottime prestazioni** per **app read-only.**

###### Shared Disk (cluster)

I **cloni condividono un server che gestisce i dischi fissi**.

### Partitioning

**Prevede duplicazione di HW o SW, ma non dei dati, ripartiti tra nodi**.

**Ogni nodo svolge una funzione specifica** (tipo ogni nodo assegnato un endpoint di un ito)

**Dati** però **sono su 1 singolo server**, quindi **se esplode**, c'è il **degrado parziale** dei sistemi distribuiti (non tutto il sistema, **ma solo alcune funzionalità**)

Per risolvere questo si usano i:

##### RAPS (Reliable Array of Partitioned Services)

**Permette di ottenere piena scalabilità e disponibilità del servizio**.

