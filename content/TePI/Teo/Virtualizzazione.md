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

- Uno **sviluppatore** può eseguire un’app in diversi ambienti senza necessità di + pc fisici,
- Un **system admin** può testare uno scenario complesso con + servizi su + host diversi, fattibile con + VM diverse.
- Gli **utenti finali** traggono maggiori benefici:
- **Aumento dell’affidabilità del sistema**, perché possibile dedicare VM a servizi che non vanno in conflitto e isolare i vari guest cosicché eventuali problemi di una VM non influenzino la stabilità di altre.
- **Consolidamento dei server**, con la virtualizzazione si eseguono + VM sulla stessa macchina, riducendo il n° dei server necessari per l’erogazione di servizi aziendali di 10 volte o +.
- **Riduzione dei costi**, meno server significa meno costi energetici, di acquisto e di manutenzione dei server.
- **Disaster recovery**, un OS guest è facilmente ripristinabile riducendo i tempi di indisponibilità per guasto.
- **Alta disponibilità**, se ci sono + server fisici con hw compatibili e questi condividono uno storage su cui risiedono delle VM, in caso di failure è possibile spostare l’esecuzione delle VM di un host su un altro.

##### Vantaggi (per Datacenter)

- Riduzione numero di server da gestire,
- Riduzione spazio fisico necessario,
- Riduzione costi energetici,
- Riduzione costi di manutenzione.

##### Benefici

- **Esecuzione di app legacy**, virtualizzando OS si possono continuare a usare sw aziendali fatti per sistemi obsoleti.
- **Sviluppo e testing**, è possibile predisporre ambienti di sviluppo/testing senza intaccare l’ambiente principale.

**Riassumendo: - costi, gestione infrastruttura IT + semplice, > affidabilità e > flessibilità.**

### Cosa si virtualizza?

Si riferisce in generale all’astrazione delle **risorse di calcolo** (*computing resources*):

##### Platform virtualization

(Concetto di **VM**) ovvero virtualizzazione di piattaforme hw, poi esteso a storages, namespaces e network resources.

- **Emulation/Simulation**
- **Native/Full virtualization**
- Hardware Enabled Virtualization
- Partial virtualization
- **Paravirtualization**
- **OS-level virtualization**
- Application virtualization

##### Resource virtualization

(Concetto di **qualità del servizio**) ovvero virtualizzazione di risorse.

- RAID
- SAN
- Channel Bondings
- VPN/NAT
- Multiprocesssor e multi-core
- Cluster e grid computing
- Partitioning

### **Hypervisor** (VMM)

È un programma **che crea ed esegue VM guest su una macchina fisica host,** che **astrae l’hw di un pc** e che:

- **Crea e controlla molti** ambienti di esecuzione (**VM**) diversi e:
- **Ciascuno** di questi può avere un **proprio** e diverso **OS**
- **Ciascuno** di questi **crede di controllare l’intero** sistema **hw**.

Principali hypervisors: VirtualBox, KVM, QEMU, Parallel, Xen, VMWare, Xbox 360.

###### VirtualBox

La **VMM è un processo** che gira nell’host (anche app utente) e il suo **OS non sa che si sta virtualizzando** un guest.

##### Virtual Machine (VM)

**Ambiente di esecuzione creato dall’hypervisor**.

##### Tipi di hypervisor

###### Type-1 (*Bare-Metal* o *Native*)

Il sw di virtualizzazione è **OS-like**, ovvero si **integra direttamente con il kernel del OS** e si **interfaccia con l’hardware direttamente**, consentendo gestione di risorse + efficiente, veloce e stabile per i guest. Tipica nella **virtualizzazione di server** (consolidamento di + server in 1) e per la **distribuzione di OS desktop remoti** per utenti in rete.

###### Type-2 (*Hosted*)

**L’hypervisor è** una vera e propria **applicazione** che si **gira sull’OS fisico** e **virtualizza** degli **ambienti compatibili** con esso a più alto livello, **facendo da tramite** per le operazioni tra guest e host.

**Svantaggio**: essendo un’applicazione, **non ha la stessa efficienza del Type-1**.

**Vantaggio**: **installazione del sw e creazione dei guest senza difficoltà**, spesso **gratis**.

#### **Principali metodologie**

##### Emulation

L’**hypervisor emula un intero set di hw** in modo **standard per eseguire l’OS guest** senza modifiche. L'hypervisor presenta al OS guest un hw completo, indipendentemente da quello dell'host. Limiti:

- Hw presentato è **standard**, magari non include funzionalità già implementate in hw dell’host.
- **Necessario interfacciare** la **CPU**, la **memoria** e l’**I/O** tra sistema host e guest.

Emulazione è difficile perché bisogna emulare sistemi guest con processori di velocità = al processore dell’host. Quindi emulazione fattibile quando ho **+ processori**.

##### Full Virtualization

Gli **OS guest** virtualizzati devono essere **compatibili con l’hw dell’host**, quindi **non necessario interfacciare CPU**, **memoria** e **I/O** perché **tutto** fatto sull’hw **direttamente**, con > prestazioni.

##### Paravirtualization

L’hypervisor mostra un’**hw sottostante modificato ai guest**, ma ne mantiene l’architettura. Gli **OS delle VM sono modificati** (differenza con la full, evitano certe system call, per cui prestazioni vicine all’OS non virtualizzato, siccome istruzioni eseguite su CPU direttamente); (virtualizza - hw fisico, quindi possibili + VM perché ho + memoria free).

##### OS level virtualization

**Non usa hypervisor**, ma si **virtualizzano copie dell’OS dell’host**. I **guest saranno istanze dell’OS dell’host** con un proprio file system, configurazione di rete e applicazioni. VM non necessitano di kernel privati, ma usano lo stesso dell’host con < utilizzo di memoria, quindi semplice condivisione e gestione della memoria). Non adatto a OS **diversi** sullo stesso host, poca stabilità e isolamento.

#### Supporto hardware alla virtualizzazione

Aziende produttrici di hw (come Intel e AMD) hanno iniziato a distribuire CPU con supporto di virtualizzazione per diminuire intervento Hypervisor.

- Intel, che ha implementato (in CPU Xeon e Itanium) le tecnologie **VT-d**, **VT-x** e **VT-i**, che **limitano o eliminano l’intervento dell’hypervisor**, eseguendo direttamente e automaticamente operazioni e context switches tra guest e CPU host.
- AMD, con **AMD-V**, un **insieme di estensioni hw** dell’architettura **x86 per ridurre o eliminare**, **l’intervento dell’hypervisor**.

#### Componenti di virtualizzazione

- CPU scheduling: sono possibili **+ CPU virtuali che CPU fisiche** (***overcommitment***) e la **VMM** deve **condivide**re **risorse fisiche tra** i **guest**. 
	- Overcommitment (CPU e memoria): allocazione di + CPU o memoria virtuale di quella fisica per poter avere + guest. (rischi di stabilità di sistema).
	- Thin provisioning (storage): allocazione di storage flessibile e ottimizzato dando l’impressione che guest ne abbiano disponibile + di quello fisico.
- Memory management: il **VMM overcommitta memoria tra i guest** e **decide quanta ognuno ne può usare** (anche se il guest pensa che la stia usando tutta) oltre a **fare da sé l’allocazione di pagine di memoria**.
- I/O management: il **VMM dedica dispositivi I/O ai guest** e può fornirgli **device drivers astratti** (mappando le richieste a quelli veri).
- Storage management: il VMM assicura che **ogni guest può accedere solo** alla parte di **storage assegnatagli**.
- Networking: il VMM fornisce: **a ogni guest almeno 1 IP**, **routing tra** il **guest e** la **rete** e il **NAT**.

### RAID

Gestendo la memoria vanno gestite le **ridondanze**, quindi considerare possibilità di guasti o situazioni che mettano in pericolo l’integrità dei dati. Ciò è fatto con il **RAID** (*Reduntant Array of Independent Disks*) che **raggruppa gli HDD in un grande disco logico** (**volume**) suddiviso in **sottovolumi** dedicati ai server. Tipi di RAID più usati:

##### RAID 1 o *mirroring*

Si configurano **2 dischi con 1 la copia dell’altro**; se 1 si rompe l’altro continua e quando sostituito si ricostruiscono i dati in esso con quelli dell’altro. **Ottime prestazioni** ma consente di sfruttare solo il **50% dello spazio disponibile**.

##### RAID 5

Si usano **3 o + HDD** e i **dati sono scritti vettorialmente su 2 di essi**, mentre **nel 3° vengono scritti i bit di parità** per ciò che è stato scritto nei primi 2 così che in caso di guasto di 1 disco, le info possono essere **ripristinate ricalcolando i valori**. Questo presenta un **< spreco di risorse** ma ogni **operazione di scrittura richiede** il **calcolo** dei **bit di parità**.

### Virtual Networking

Una rete virtuale è un **insieme di VM in esecuzione su una singola macchina fisica e collegate logicamente tra loro così che possano scambiarsi dati**. Le VM forniscono le funzionalità di **vNIC**, **virtual switches**, **virtual routers**…

Un virtual switch rileva le VM logicamente collegate alle sue porte virtuali e indirizza il traffico; ciò consente di gestire la connettività a livello datalink, con possibilità di impostare **VLAN** multiple secondo lo standard 802.1q.

###### LACP

Per avere la max disponibilità dei collegamenti, lo switch virtuale può configurare + NIC fisiche associandole a esso in modalità **LACP** (*Link Aggregation Control Protocol*), che rende visibile allo switch le NIC fisiche come un'unica scheda logica e tra queste ripartisce il traffico.

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

- Ridurre costo tot dell’hw (ne serve meno perché si hanno VM), 
- Aumentare la sicurezza,
- Limitare il tempo impiegato per servizi IT (tipo aggiornamenti…)

##### Virtualizzazione di funzioni di rete (NFV)

Separa le funzioni chiave di rete (file sharing, IP configuration...) per distribuirle tra + ambienti. È possibile riunire funzioni in una rete e assegnarle a un (sotto)ambiente, per esempio: in una rete fisica virtualizzo una sottorete per load balancing e controllo di accessi. Questa è la base della "cittadella" in crittografia.

