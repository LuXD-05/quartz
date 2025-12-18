# Lezione 4

### Applicazioni

Supponiamo di dover gestire un sistema bancario: gli utenti (clienti e personale) non eseguono istruzioni SQL arbitrarie ma usano un'applicazione come tramite; questo perché (oltre a complessità del linguaggio e problemi di sicurezza) SQL da solo non basta per fare tutto ciò che serve.

Questo perché SQL non è né **computazionalmente completo** né **operazionalmente completo**:

##### Completezza

###### Computazionale

La **completezza computazionale** si riferisce alla capacità di un linguaggio di gestire possibili flussi e computazioni; questo a SQL manca in quanto non è dotato di costrutti di scelta (`if`) o di iterazione (`for`) al contrario dei linguaggi di programmazione.

###### Operazionale

La completezza operazionale invece è relativa alla capacità di un linguaggio di esprimere certe operazioni, in particolare quelle con il SO e l'hardware; per esempio SQL non è dotato di costrutti per scrivere file, sviluppare interfacce utente...

#### Soluzione

La soluzione è quindi combinare SQL con i linguaggi di programmazione computazionalmente ed operazionalmente completi cosicché colmino le sue mancanze. Per garantire tale integrazione ci sono 2 approcci:

##### Client side

Questo è l'approccio più usato e prevede che le istruzioni SQL siano eseguite all'infuori del DBMS in un ambiente ***client-side*** per garantire completezza; possibile con 2 tecnologie.

> [!example] Caratteristiche
> - Maggiore indipendenza dal DBMS
> - Minore efficienza

###### API

Viene resa disponibile al linguaggio un'API che definisce l'interfaccia di comunicazione tra gli applicativi scritti col **linguaggio ospite** e il DBMS. Oltre alle API proprietarie dei DBMS esistono alcune standard (tipo ODBC o JDBC); e queste forniscono funzioni per la connessione al database e per l'esecuzione di comandi.

###### Embedded SQL

Qui i comandi SQL sono utilizzati direttamente all'interno di un linguaggio di programmazione ospite ed un particolare pre-copilatore produce istantaneamente delle righe di codice equivalenti nel linguaggio ospite.

##### Server side

Con questo invece SQL viene esteso con i costrutti dei linguaggi di programmazione che gli mancano, ma la logica rimane tutta all'interno del DBMS con la possibilità di definire funzioni e procedure richiamabili da qualsiasi app (***stored procedures***). SQL standard ne propone un'implementazione procedurale detta SQL/PSM, ma i DBMS non la recepiscono pienamente (si hanno tipo Transact-SQL, PL/SQL, PLpgSQL...).

> [!example] Caratteristiche
> - Dipendente dal DBMS
> - Maggiore efficienza
> - Minore espressività

##### Integrazione

Per l'integrazione alla fine si tende a preferire una combinazione tra i 2 approcci, così da poter definire *stored procedures* server-side per le operazioni più frequenti ed al contempo avere la flessibilità dei linguaggi di programmazione per certe operazioni particolari.

###### Impedance mismatch

Quando si integra SQL con un qualsiasi linguaggio di programmazione ci sono sempre 2 problemi principali per i quali servono soluzioni specifiche:

- **Tipi di dato diversi**: `string` in SQL è `VARCHAR`, tipi del genere devono essere **mappati** correttamente.
- **Modalità di elaborazione diverse**: SQL lavora su insiemi (*set-oriented*) mentre i linguaggi sulle tuple, perciò nelle app bisogna scorrere i risultati riga per riga tipo con [[#Cursore|cursori]].

#### SQL nei linguaggi

Eseguire un comando SQL da codice coinvolge diversi passaggi:

1\) **Preparazione**: vengono generate le strutture dati necessarie per la comunicazione col DBMS e quest'ultimo ottimizza il comando,

2\) **Esecuzione**: il comando viene eseguito usando le strutture e le informazioni generate in preparazione,

3\) **Output**: il risultato del comando viene tradotto nelle strutture dati del linguaggio e viene manipolato dal programma. 

##### Risultati

I comandi SQL possono restituire diversi risultati:

- **Valori numerici**: con l'esecuzione di query scalari, comandi `INSERT`, `UPDATE`, `DELETE` o comandi DDL,
- **Insiemi di tuple**: in seguito a interrogazioni; in caso di 1 tupla si possono salvare i campi in variabili, mentre in caso di più tuple se sono abbastanza poche da poter restare in memoria vengono salvate in una struttura dati e manipolati, altrimenti vi è la necessità di un **[[#Cursore|cursore]]**.

###### Cursore

Un **cursore** è un puntatore ad una tupla nel risultato di una query che permette di utilizzarne i valori degli attributi per usarli nel programma finché non si passa alla successiva.

![](https://i.imgur.com/JNc2VRu.png)

##### Tipi di SQL

I comandi SQL eseguibili da codice possono essere statici o dinamici:

###### SQL statico

Le istruzioni SQL **statiche** sono già note prima dell'esecuzione del programma e al massimo contengono delle variabili valutate a runtime.

> [!info] Caratteristiche
> - La struttura dei risultati è nota a priori,
> - Utilizzabile più volte senza doverlo ricostruire,
> - Permette all'applicazione e al DBMS di ottimizzare le query.

###### SQL dinamico

I comandi SQL dinamici invece sono costruiti a runtime e possono variare in base al flusso di esecuzione e dipendere da input utente (esempio: una query dove la clausola `WHERE` è costruita dinamicamente).

> [!info] Caratteristiche
> - Sono molto migliori in termini di flessibilità (rispetto agli statici),
> - Tuttavia devono sempre essere ri-preparati ogni qualvolta che si vogliono usare.

#### CLI

Una **CLI** (*Call Level Interface*) è una API contenente un insieme di funzioni per l'interazione con le basi di dati usate dal linguaggio ospite (generalmente le CLI sono offerte dai DBMS e sono specifiche, standard più importanti sono ODBC e JDBC).

##### JDBC

JDBC è la CLI standard di Java per interagire con SQL ed è *platform-independent* e portabile:

![](https://i.imgur.com/vaoahHK.png)

Ciò è ottenuto grazie ai ***driver***: un componente software che traduce tutte le chiamate JDBC in chiamate specifiche per la CLI di un certo DBMS.

###### Driver Manager

JDBC mette a disposizione la classe `DriverManager`, la quale gestisce la comunicazione tra app e driver senza lasciare alla prima problematiche quali scelta, caricamento e chiamate del driver.

###### Types

JDBC definisce un insieme di tipi di dato SQL e come vengono mappati in tipi Java:

![](https://i.imgur.com/oWA5pcx.png)

###### Connection

Come anche altre CLI, `DriverManager` mette a disposizione un oggetto `Connection`, che rappresenta la connessione al database ottenibile (e apribile) con il metodo `getConnection(...)` ma si può anche interrompere con `close()` per risparmiare risorse (questa chiude tutti gli *statement* e di conseguenza i loro `ResultSet`).

###### Statement

La classe `Statement` (e sottoclassi) invece, permette l'esecuzione di istruzioni SQL. Ogni `Statement` è associato a una `Connection` usando `conn.createStatement()` e i comandi (eseguibili con `execute()` e varianti) possono essere:

- **Non preparati**: SQL statico e dinamico (generici),
- **Preparati**: SQL statico,
- ***Callable statements***: *stored procedures*.

> [!important] Comandi preparati
> Un comando preparato è compilato 1 sola volta all'inizio dell'app ed eseguito più volte (eventualmente anche con ridefinizione dei parametri `?` ogni volta tramite metodi `set[type]()` tipo `setString()`) ed è istanza della classe `PreparedStatement` (che richiede un comando SQL in stringa).
> I risultati sono restituiti in un oggetto `ResultSet` legato allo statement ed è possibile accedervi con un cursore usando `next()` per spostarsi alla prossima tupla (`next()` ritorna `true` finché riesce a passare a una tupla successiva, mentre dopo quella finale diventa `false`).
> Per ottenere i risultati si usano metodi `get[type]()` tipo `getString()` dove il parametro indica o il nome di colonna o la posizione dell'attributo da ottenere.

###### Eccezioni

In Java la classe `java.lang.Exception` è estesa da `java.sql.SQLException` così da fornire informazioni più dettagliate sugli errori, comandi utili sono `getErrorCode()` (per codice errore specifico del DBMS) e `getMessage()` (per una descrizione dell'errore).

---

