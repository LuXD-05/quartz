##### Definizione di chiave

Nel modello relazionale, una chiave è un'insieme di attributi che distingue (e univocizza) le tuple di una relazione. Ce ne sono di diversi tipi:

- PK: una chiave composta dal < n° possibile di attributi (minimalità) che univocizza ogni tupla di una relazione
- FK: chiave che mette in relazione 2 entità di un database
- CK: chiavi candidate ad essere PK
- AK: CK che non sono parte della PK

##### PK

Una PK è un vincolo che si impone a 1 o + attributi in modo tale che essi distinguano univocamente ogni tupla di una relazione. Essa rispetta 2 proprietà importanti:

- **Univocità**: non possono esistere più tuple con la stessa PK (univoca per ogni tupla)
- **Minimalità**: l'insieme degli attributi PK non contiene attributi "inutili", ovvero superflui al fine di garantire l'univocità.

##### FK

Date 2 relazioni $R1$ e $R2$ e 2 insiemi di attributi $A1$ e $A2$ di numero uguale e domini compatibili, $A1$ è una **FK** di $R1$ su $R2$ se ogni tupla $T$ di entrambe le relazioni, $T1(A1)$ è `NULL` oppure $T1(A1) = T2(A2)$.

##### DDL, DML, DQL, SDL

SQL è composto da diversi linguaggi:

- **DDL** (*Data Definition Language*): include le istruzioni per creare, modificare ed eliminare tabelle, definirne i campi, le chiavi e quindi permette la modifica dello schema del db (CREATE, ALTER, DROP),
- **DML** (*Data Manipulation Language*): include le istruzioni per inserire, modificare e cancellare i dati all'interno del database, quindi permette la modifica dell'istanza del db (INSERT, UPDATE, DELETE),
- **DQL** (*Data Query Language*): include le istruzioni per selezionare certi valori delle tabelle del database e ordinarli, restringerli, raggrupparli... in base a certe keyword (SELECT...),
- **SDL** (*Storage Definition Language*): definisce lo schema fisico del database, quindi le strutture fisiche con le quali salvare i dati sulla memoria fisica.

##### Principali soluzioni per sviluppo di app che si interfaccia su un db relazionale + vantaggi e gli svantaggi

SQL da solo non è sufficiente per sviluppare applicazioni in quanto non è <u>operazionalmente e computazionalmente completo</u>, perciò va integrato conn altri linguaggi di programmazione. 2 approcci:

- **Client-side**: logica applicativa nell'app e il DBMS è interrogato tramite API (tipo JDBC e ODBC o quelle standard del DBMS) o embedded SQL; > indipendenza dal DBMS ma < efficienza.
- **Server-side**: con questo SQL viene esteso con tutti i costrutti dei linguaggi di programmazione che gli mancano ma la logica rimane tutta all'interno del DBMS con possibilità di definire stored procedures richiamabili da qualsiasi app usando varie implementazioni come T-SQL...

##### Fasi della progettazione di un database + input e output

Le fasi di progettazione di un database sono 5 (ACLNF):

- **Analisi dei requisiti**: in questa sono definite le caratteristiche del database e del contesto, con anche i requisiti, raccolti in un documento di specifica dei requisiti (output della fase),
- **Progettazione concettuale**: questa (dai requisiti nel documento in input) definisce lo schema concettuale del database per mezzo del modello ER, descrivendo entità, associazioni, attributi, vincoli... (output)
- **Progettazione logica**: questa prende l'ER (input) e lo trasforma in uno schema logico definito in base al DBMS e al carico di lavoro (output)
- **Normalizzazione**: questa prevede un processo di traduzione dello schema logico (input) in uno schema logico normalizzato (output), ristrutturato in modo tale da eliminare le ridondanze,
- **Progettazione fisica**: in questa vengono effettuate delle scelte circa la memorizzazione fisica dei dati e l'accesso ad essi, il tutto descritto attraverso uno schema fisico (output)

##### Indipendenza fisica e logica in un DBMS

**Indipendenza fisica**: capacità di modificare la struttura fisica del database (quindi il supporto di memoria fisico) senza influire sulla struttura logica dello stesso.

**Indipendenza logica**: capacità di modificare il modello logico del database (quindi schemi e istanze del database) senza influire sulle applicazioni che lo utilizzano.

##### Transazioni

Una **transazione** (`TRANSACT`) è una sequenza di operazioni (batch) sul database che ha un inizio (BoT) e una fine (EoT) che può terminare con successo (`COMMIT`, le modifiche sono applicate al database) o insuccesso (`ROLLBACK`, viene segnalato l'errore e il database torna allo stato precedente prima dell'esecuzione della transazione).

Le transazioni assicurano (CRI) <u>correttezza, robustezza e isolamento</u>, proprietà fondamentali anche per il controllo degli accessi concorrenti al database.

##### Gerarchie di generalizzazione nel modello ER

Un'entità $E$ (padre) è una generalizzazione di altre entità $E1, ... E_{n}$ (figlie) se ogni istanza di queste è anche istanza di $E$. Questo meccanismo permette ai figli di ereditare tutte le proprietà del padre consentendo anche l'aggiunta di ulteriori attributi specializzati. Ce ne sono di diversi tipi:

- **Totale**: ogni istanza del padre è anche istanza di almeno 1 figlio
- **Parziale**: ci sono istanze del padre che possono non essere istanze di alcun figlio
- **Esclusiva**: ogni istanza del padre è al massimo istanza di 1 solo figlio
- **Condivisa**: ogni istanza del padre può essere istanza di più figli contemporaneamente

##### Cosa sono le view, a cosa servono e codice SQL con clausole

Una view è una relazione (tabella) virtuale definita su una query SQL che non memorizza alcun dato bensì mostra i dati selezionati dalla sua query ogni volta che viene interrogata. Il suo contenuto è quindi ricalcolato dinamicamente a partire dalla sua query di definizione ed è utilizzabile come una normale tabella.

Essa è utile per semplificare l'accesso ai dati (senza dover riscrivere ogni volta una query) e per fornire indipendenza logica e protezione ai dati (rende disponibile agli utenti solo i propri dati, senza dare l'accesso alle tabelle originali.

```mysql
CREATE VIEW <nome_view> [(<colonne>)]
AS <query>
[WITH [{LOCAL|CASCADE}] CHECK OPTION]
```

##### Cos'è il JDBC

JDBC è la CLI standard di Java, usata per interagire con database con tale linguaggio. Essa è portabile e platform-independent grazie ai driver: componenti software che traducono le call JDBC in call specifiche per la CLI di un certo DBMS gestiti con una classe `DriverManager`. In più, JDBC definisce tipi compatibili con SQL, una classe `Connection` per la connessione col db, `Statement` per l'esecuzione di query ed eccezioni particolari per SQL.

##### Differenza tra schema ed istanza e i linguaggi per gestirli

Lo **schema** rappresenta la struttura logica del db e come sono organizzati i dati; quindi definisce tabelle, attributi, tipi di dati, vincoli... esso è statico e cambia raramente nel tempo.

Gestito con il **DDL** (Data Definition Language), tipo con operazioni di CREATE, ALTER e DROP.

L'**istanza** di un db invece rappresenta il suo contenuto effettivo in un certo istante di tempo, quindi i dati memorizzati nelle tabelle sottoforma di tuple; essa è dinamica e cambia frequentemente nel tempo.

Gestito con il **DML** (Data Manipulation Language) per inserire, modificare e cancellare dati (INSERT, UPDATE, DELETE) e con il **DQL** (Data Query Language) per le interrogazioni (SELECT).

##### Valori nulli e gestione nel DBMS

In un database si usa un valore nullo `NULL` per rappresentare la mancanza di informazione (info mancante, sconosciuta o incompleta) per certi attributi nelle relazioni (solo quelli che lo permettono tramite constraint `NOT NULL`).

La gestione di tali valori nei DBMS è legata a una logica a 3 valori usata per valutare le espressioni che coinvolgono il valore NULL, composta da TRUE (T), FALSE (F) e UNKNOWN (?); quest'ultimo indica che il risultato di un predicato booleano non è determinabile a causa della presenza di un valore NULL.

##### Proprietà ACIDe

I DBMS relazionali rispettano delle proprietà dette ACIDe, che assicurano la corretta esecuzione delle operazioni; e sono:

- **Atomicità**: tutte le operazioni della transazione sono eseguite completamente, altrimenti nessuna di esse ha effetto sul database (se una fallisce, si fa il rollback che riporta il database allo stato prima della transazione; ciò garantito dal sottosistema di ripristino).
- **Consistenza**: garantisce che una transazione porti il database da uno stato iniziale ad uno finale consistenti (e che durante e dopo essa siano rispettati tutti i vincoli di integrità).
- **Isolamento**: questa assicura che l'esecuzione di una transazione non sia influenzata da altre concorrenti, cosi che nessuna transazione veda i risultati intermedi di un'altra.
- **Durabilità**: garantisce che dopo un commit, i risultati della transazione siano salvati permanentemente nel database (anche in caso di guasti o malfunzionamenti del sistema).

##### Identificatori nel modello ER

Un identificatore nel modello ER è un attributo (o insieme di attributi) che identificano univocamente ogni istanza di un'entità; e ce ne sono di vari tipi:

- **Semplice**: contiene 1 solo attributo
- **Composto**: contiene + attributi
- **Interno**: formato da 1 o + attributi stessi dell'entità
- **Esterno**: formato da 1 o + attributi di entità associate
- **Misto**: misto tra interno ed esterno

##### Cos'è il DBMS

UN DBMS (DataBase Management System) è un sistema software (centralizzato o distribuito) che fornisce gli strumenti per la gestione di collezioni di dati grandi, condivise e persistenti. Un DBMS ha anche varie caratteristiche (PESCAD+):

- **Persistenza**: i dati permangono sempre in memoria per le app che ne fanno uso,
- **Efficienza**: più veloce ed efficiente nella gestione dei dati (tempo e spazio),
- **Sicurezza**: grazie a meccanismi di autorizzazione e RBAC tramite GRANT,
- **Condivisione**: un DBMS permette l'accesso a dati comuni ad app diverse,
- **Affidabilità**: previene malfunzionamenti grazie a backup e meccanismi di recovery,
- (**Dimensioni > di memoria centrale** + riduzione inconsistenze + riduzione ridondanze).

##### Integrità referenziale in SQL

L'**integrità referenziale** è un vincolo imposto con la definizione di una FK e implica che i valori assunti dalla FK della relazione referente devono esistere come valori della PK nella relazione riferita (seppur può comunque assumere `NULL` per indicare che la tupla della relazione referente non è correlata ad alcuna tupla della relazione riferita).

##### Architettura a 3 livelli del DBMS

I DBMS presentano un'architettura a 3 livelli:

- **Livello esterno**: è il livello di astrazione più alto ed implementa *view* (porzioni dello schema del database) che mostrano certi dati agli utenti,
- **Livello logico**: descrive il database attraverso il suo schema logico indicando tipi di dato, possibili associazioni, vincoli di integrità...
- **Livello fisico**: è il livello più basso col quale viene definito lo schema fisico del database, quindi precisando con quali strutture fisiche i dati dello schema logico verranno memorizzati sul supporto fisico di memoria.

##### Come il DBMS risolve query con GROUP BY

Quando un DBMS deve risolvere query con funzioni di gruppo ed aggregazione (COUNT, SUM, AVG, MIN, MAX, GROUP BY...), esso segue un procedimento articolabile in fasi:

- Individua le tabelle dalla keyword `FROM` (+ tabelle joinate),
- Filtra le tuple con i predicati in `WHERE`,
- Crea (eventualmente) i gruppi per `GROUP BY`,
- Calcola (per ogni gruppo) le funzioni di aggregazione,
- Filtra (eventualmente) i gruppi coi predicati in `HAVING`,
- Ritorna il risultato di `SELECT`.
