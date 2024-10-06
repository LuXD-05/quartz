---
public: true
modified_at: 23/06/2024 19:05:45
edited_seconds: 30
---
# Virtualizzazione
### Storia
Benché la virtualizzazione risalga agli <u>anni 60</u>, si è diffusa soltanto all'inizio degli <u>anni 2000</u>. 
Le tecnologie di virtualizzazione, sono state sviluppate decenni fa, per risolvere il problema dell'accesso simultaneo di + utenti a 1 pc, dapprima con l'elaborazione batch attiva (in questa le richieste di servizio non sono subito assolte, ma accodate finché le risorse di cui necessitano non sono disponibili), adottata da molte aziende per la sua velocità. Però nel tempo, l'uso di tecniche di virtualizzazione fu sempre meno usato per questo problema.
Ciò fino agli anni 90, quando si iniziò ad usare la virtualizzazione per risolvere 2 problemi dei "commodity server" aziendali con hardware fisici poco utilizzati, permettendo di:
- Partizionare i server,
- Eseguire le app su + tipi e versioni di OS.
Con ciò la virtualizzazione ha contribuito a ridurre il *vendor lock-in* e ha posto le basi del [[10 Cloud Computing|Cloud Computing|cloud computing]].

### Che cos’è?
Hint: 
::
È una **tecnica per nascondere e astrarre delle risorse fisiche** (pc, server, rete…) **rendendole disponibili come risorse virtuali**, (risultando, nel caso di pc, in hw fisici che condividono risorse tra dei loro *guest*).
### Scopo
Lo <u>scopo</u> della virtualizzazione (di pc) è quello di **eseguire in contemporanea + istanze di un OS *guest* in 1 unico host fisico**. Questi OS, detti "***guest***", interagiscono con le risorse fisiche dell’host tramite un sw intermedio: l’**hypervisor** o **VMM** (virtual machine monitor).
#### Hypervisor
È un programma **che crea ed esegue VM guest su una macchina fisica host**. Ciascuna VM ha un OS proprio e crede di controllare l'intero hw.
Principali hypervisors: VirtualBox, KVM, QEMU, Parallel, Xen, VMWare, Xbox 360.
##### Tipi di hypervisor
###### Type-1
(Detto: *Bare-Metal* o *Native*), in cui il sw di virtualizzazione è *OS-like*, ovvero si **integra direttamente con il kernel del OS** e si **interfaccia con l’hardware direttamente**, consentendo gestione di risorse + efficiente, veloce e stabile per i guest. 
Tipica nella **virtualizzazione di server** (consolidamento di + server in 1) e per la **distribuzione di OS desktop remoti** per utenti in rete.
###### Type-2
(Detto: *Hosted*), in cui l'**hypervisor** è un <u>programma</u> eseguito sull'OS fisico e <u>virtualizza degli ambienti compatibili</u> con esso a più alto livello, <u>facendo da tramite</u> per le operazioni tra guest e host.
**Svantaggio**: essendo un’applicazione, <u>non ha la stessa efficienza del Type-1</u>.
**Vantaggio**: installazione del sw e creazione dei guest <u>+ semplice</u>, spesso <u>gratis</u>.

### Tipi di virtualizzazione
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

### RAID
Gestendo la memoria vanno gestite le **ridondanze**, quindi considerare possibilità di guasti o situazioni che mettano in pericolo l’integrità dei dati. Ciò è fatto con il **RAID** (*Reduntant Array of Independent Disks*) che **raggruppa gli HDD in un grande disco logico** (detto <u>volume</u>) suddiviso in <u>sottovolumi</u> dedicati ai server. Tipi di RAID più usati:
##### RAID 1
(O *mirroring*), si configurano **2 dischi con 1 la copia dell’altro**; se 1 si rompe l’altro continua e quando sostituito si ricostruiscono i dati in esso con quelli dell’altro. <u>Ottime prestazioni</u> ma consente di sfruttare solo il **50% dello spazio disponibile**.
##### RAID 5
Si usano **3 o + HDD** e i **dati sono scritti vettorialmente su 2 di essi**, mentre **nel 3° vengono scritti i bit di parità** per ciò che è stato scritto nei primi 2 così che in caso di guasto di 1 disco, le info possono essere ripristinate ricalcolando i valori. Questo presenta un < spreco di risorse ma ogni <u>operazione di scrittura</u> richiede il <u>calcolo dei bit di parità</u>.

### SAN
(*Storage Area Network*), è una tecnologia che permette di **gestire lo storage esterno rendendolo visibile agli host come un insieme di dischi configurati in modo che appaiano come uno unico**.
I dischi del SAN sono di solito <u>interconnessi tramite uno switch</u>, <u>scalabili</u> e <u>gestiti da un controller</u> con un proprio OS.
##### NAS
(*Network Attached Storage*) la tecnologia **NAS** permette ai pc di una rete di **condividere il proprio storage con altri** dispositivi, e quindi di <u>interagire con una SAN</u> (con connessioni *Fiber Channel* o SCSI).

### Virtual Networking
Una rete virtuale è un **insieme di VM in esecuzione su una singola macchina fisica e collegate logicamente tra loro così che possano scambiarsi dati**. Le VM forniscono le funzionalità di vNIC, virtual switches, virtual routers…
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

### ?
#### Supporto hardware alla virtualizzazione
Aziende produttrici di hw (come Intel e AMD) hanno iniziato a distribuire CPU con supporto di virtualizzazione per diminuire intervento Hypervisor.
- **Intel**, che ha implementato (in CPU Xeon e Itanium) le tecnologie **VT-d**, **VT-x** e **VT-i**, che **limitano o eliminano l’intervento dell’hypervisor**, eseguendo direttamente e automaticamente operazioni e context switches tra guest e CPU host.
- **AMD**, con **AMD-V**, un **insieme di estensioni hw** dell’architettura **x86 per ridurre o eliminare**, **l’intervento dell’hypervisor**.
#### Componenti di virtualizzazione
- CPU scheduling: sono possibili **+ CPU virtuali che CPU fisiche** (***overcommitment***) e la **VMM** deve **condivide**re **risorse fisiche tra** i **guest**. 
	- Overcommitment (CPU e memoria): allocazione di + CPU o memoria virtuale di quella fisica per poter avere + guest. (rischi di stabilità di sistema).
	- Thin provisioning (storage): allocazione di storage flessibile e ottimizzato dando l’impressione che guest ne abbiano disponibile + di quello fisico.
- Memory management: il **VMM overcommitta memoria tra i guest** e **decide quanta ognuno ne può usare** (anche se il guest pensa che la stia usando tutta) oltre a **fare da sé l’allocazione di pagine di memoria**.
- I/O management: il **VMM dedica dispositivi I/O ai guest** e può fornirgli **device drivers astratti** (mappando le richieste a quelli veri).
- Storage management: il VMM assicura che **ogni guest può accedere solo** alla parte di **storage assegnatagli**.
- Networking: il VMM fornisce: **a ogni guest almeno 1 IP**, **routing tra** il **guest e** la **rete** e il **NAT**.