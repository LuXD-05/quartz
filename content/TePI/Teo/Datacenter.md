# Datacenter

### Datacenter

Un **Datacenter** è lo spazio fisico che ospita le infrastrutture tecnologiche usate per elaborazione, memorizzazione e condivisione delle informazioni.

- Dal punto di vista **fisico** un datacenter da: spazio e alloggiamenti per i dispositivi, energia, sistemi di raffreddamento e sicurezza fisica oltre a interconnessioni con operatori per accesso a internet e sicurezza logica.
- Da quello **logico** invece, un datacenter da: servizi come hosting, cloud privato e/o pubblico, applicazioni web, posta elettronica, gestione domini e altre attività non necessariamente tipiche di un datacenter.

##### Tipi

- **Aziendali** (**CED**): Proprietà di un’azienda e forniscono servizi relativi alla struttura interna.
- **Offerti da terzi** (**hosting, housing, cloud**): Strutture per gestione ed erogazione di servizi accessibili in internet.

##### Componenti

###### Infrastruttura operativa

(O *white space*), ospita i rack con i server, i sistemi di storage, gli apparati di monitoraggio e gli apparati per trasmettere dati in rete.

###### Infrastrutture di supporto

Dispositivi di backup, sistemi ridondanti, gruppi di continuità, impianti di climatizzazione, sistemi di raffreddamento, impianti antincendio e sistema di distribuzione dell’energia.

###### Personale operativo

Le figure professionali che gestiscono il centro: system admin, tecnici, sistemisti, programmatori e security.

##### Obiettivi

- **Mantenere la disponibilità dei dati garantendo continuità di elaborazione**. Quindi serve monitorare il rischio e adottare misure di protezione, tenere da conto l’errore umano e impostare logiche di controllo degli accessi oltre a garantire la protezione da minacce dalla rete (tipo malware).
- **Proteggere le info** considerando eventuali attacchi di cyber-criminalità e adottando misure internazionali per la privacy, per questo si usano firewall e sistemi anti-intrusione (IDS).

##### Evoluzione

1) **Portare all’esterno** dell’azienda i **server e lo storage** (*collocation*) rivolgendosi a terzi ed eliminando il CED;
2) Creare **datacenter virtuali** facilmente manipolabili e scalabili con la **virtualizzazione** per ridurre costi e spazi;
3) Affidarsi a un **fornitore di servizi cloud** (*serverless approach*) che gestisca da sé le problematiche fisiche.

##### Rischi

Portando tutti i servizi su un’unica struttura determina un **punto di criticità** detto **SPoF** (*Single Point of Failure)* perché un **guasto compromette l’intero sistema**; e quindi > il *downtime*, > la ripercussione economica.

Serve garantire ***High Availability*** (alta disponibilità di servizio), con ridondanze, duplicazioni, cluster e repliche datacenter.

##### Garanzie

###### Fault Tolerance

**Tolleranza ai guasti**, ovvero **evitare l’interruzione dei servizi a fronte di essi**, fatto con diverse tecniche come: RAID e la duplicazione di server e apparati di rete. È complementare insieme alla *disaster recovery*.

###### Disaster Recovery

**Recupero e ripristino** di applicazioni e dati **in caso di disastro** (di qualsiasi tipo, dal naturale all’errore umano) fatto spesso con duplicazione di interi datacenter. Determinante è il tempo di ripristino.

###### Business Continuity

**Continuità del servizio** che garantisce continuità operativa anche durante disastri o guasti.

### Tiers

##### Tier 1 – Basic Site Infrastructure

**Operatività** = **99.67%** | **Fermo macchina** = **28,8h/anno**

Data center con **gruppo di continuità** con funzioni **minime**, un **unico percorso di distribuzione** e **ridondanze nulle** o **limitate**. Protezione limitata contro eventi fisici.

##### Tier 2 – Reduntant Capacity Site Infrastructure

**Operatività** = **99.75%** | **Fermo macchina** = **22h/anno**

Ha **maggiori** capacità **ridondanti**, migliori **gruppi di continuità**, sistemi di **raffreddamento** e un **unico percorso di distribuzione non ridondante**. Protezione da eventi fisici migliorata.

##### Tier 3 – Concurrently Maintainable Site Infrastructure

**Operatività** = **99.98%** | **Fermo macchina** = **1,6h/anno**

Aggiunge componenti di **ridondanza** e **percorsi** di **distribuzione indipendenti multipli**. Il sito è **contemporaneamente mantenibile**, quindi se sospendo qualche componente di capacità, il sito dà ancora servizi mentre lo mantengo. Ha protezione contro la maggior parte degli eventi fisici.

##### Tier 4 – Fault Tolerant Site Infrastructure

**Operatività** = **99.99%** | **Fermo macchina** = **0,8h/anno**

Alla manutenzione simultanea aggiunge **l’elaborazione continua** in caso di guasto di componenti (elaborazione influenzata solo se si guastano più componenti identici).

