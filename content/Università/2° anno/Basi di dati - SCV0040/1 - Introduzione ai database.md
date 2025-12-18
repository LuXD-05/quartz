# Lezione 1

### Sistemi informativi e basi di dati

In ogni contesto applicativo è necessario gestire le informazioni; e per farlo si predispone ciò che prende il nome di **sistema informativo** (**SI**), che è formato da persone, procedure, tecnologie e **dati**, ed ha lo scopo di raccogliere, organizzare, elaborare e distribuire informazioni.

###### Dati

Nei SI, le informazioni sono rappresentate sottoforma di **dati**: simboli grezzi da interpretare correttamente per fornire informazioni. Per esempio, dire "37" è un dato senza alcun significato, mentre fornendo un contesto tipo: "Id Mario Rossi = 37" si ha l'informazione che Mario Rossi ha id = 37 nel database.

> [!info] Caratteristiche
> 1) I dati sono una risorsa strategica dell'organizzazione che li gestisce,
> 2) I dati sono più stabili nel tempo delle procedure che li gestiscono (più facile che cambino processi che interagiscono con i dati che i dati stessi).

#### Database e DBMS

In generale un **database** (*db* o base di dati) è una collezione di dati tra loro correlati e usati per rappresentare le informazioni di un SI; a livello tecnico invece è una collezione di dati gestiti da un **DBMS** (*DataBase Management System*).

> [!important] DBMS
> Un **DBMS** è un sistema software (centralizzato o distribuito) che fornisce vari strumenti per la gestione delle informazioni e delle collezioni che le contengono. Esso è in grado di gestire collezioni dati grandi, condivise e persistenti, assicurando affidabilità, sicurezza ed accesso efficiente.
> Inoltre i DBMS estendono le funzionalità dei file system, con più servizi ed in maniera più integrata:
> ![](https://i.imgur.com/5PHROVV.png)
> Il loro meccanismo più importante è lo ***[[#Schema e istanze|schema]]***, il quale descrive ad alto livello la struttura del db e quindi come i dati sono organizzati e collegati.

###### Caratteristiche DBMS

- **Dimensioni > della memoria disponibile**: (gestisce dati in una memoria secondaria),
- **Condivisione di dati** tra app e utenti: quindi si ha anche < ridondanza, < inconsistenze e controllo degli accessi concorrenti,
- **Persistenza dei dati**: i dati permangono per un tempo non limitato all'uso dei programmi che li usano,
- **Affidabilità contro malfunzionamenti**: per merito di funzionalità di *backup* e *recovery*,
- **Sicurezza**: tramite meccanismi di autorizzazione,
- **Efficienza**: (efficienti in termini di risorse spese per le operazioni).

##### Modelli di dati

I modelli di dati servono a rappresentare i dati di un db e sono composti da: strutture dati e linguaggi per gestire i dati tramite comandi specifici.

###### Modello relazionale

Il modello relazionale si basa sulla **relazione**, una struttura dati che organizza i dati in ***record*** <u>omogenei</u> (con struttura fissa). in pratica essa è vista come una tabella con righe dette ***tuple*** e colonne contenenti il nome e il tipo dei dati in esse.

![](https://i.imgur.com/AZcPytj.png)

###### Altri modelli

Prima si utilizzavano modelli di tipo gerarchico o reticolare, mentre dopo la nascita di quello relazionale sono nati altri modelli quali *object-oriented*, XML e NoSQL.

##### Schema e istanza

In ogni DBMS sono definiti 2 concetti fondamentali:

- **Schema**: descrive la struttura <u>logica</u> del db (statico, cambia raramente); in pratica sarebbero le tabelle e la loro struttura in colonne.
- **Istanza**: è l'insieme dei dati presenti in un db in un certo istante di tempo (dinamica, cambia spesso); in pratica sarebbero le righe delle tabelle.

##### Livelli di astrazione db

I database hanno <u>3 livelli di astrazione</u> secondo l'architettura standard ANSI/SPARC:

- **Livello esterno**: è il livello di astrazione più alto ed implementa varie ***view*** (porzioni dello schema del db) che mostrano certi dati agli utenti (si basa sullo schema logico),
- **Livello logico**: descrive il db tramite lo schema logico del DBMS, indica il tipo dei dati nel db, possibili associazioni tra essi ed eventuali vincoli di integrità, autorizzazione...
- **Livello fisico**: è il livello più basso in cui è definito lo schema fisico del db, ovvero come i dati nello schema logico sono memorizzati sulla macchina tramite strutture fisiche. 

![](https://i.imgur.com/Q7gpV5h.png)

##### Livelli di indipendenza dei dati

Questi 3 livelli garantiscono 2 proprietà ai dati che ne facilitano l'accesso e anche lo sviluppo di applicazioni:

###### Indipendenza fisica

Grazie a questa è possibile interagire con il db indipendentemente dalla sua struttura fisica (utenti e app accedono al livello esterno o logico e non sono affetti da eventuali cambiamenti al livello fisico).

###### Indipendenza logica

Questa si ottiene grazie alle viste, quindi con la possibilità di nascondere (fino a un certo punto) modifiche allo schema logico ad utenti e app senza che essi siano affetti da tali cambiamenti (va bene er aggiunte di attributi allo schema, ma non se si elimina un attributo che è anche all'interno della vista).

##### Linguaggi DBMS

Generalmente SQL, ma si divide in:

###### DML

La **DML** (*Data Manipulation Language*) permette l'interrogazione, modifica e creazione delle istanze del db (livello logico/esterno).

###### DCL e DDL

La **DCL** (*Data Control Language*) serve per gestire gli accessi al db e ai dati, mentre la **DDL** (*Data Definition Language*) permette di creare tabelle e relazioni (livello logico/esterno).

###### SDL

La **SDL** (*Storage Definition Language*) definisce invece lo schema fisico del db (livello fisico).

##### Vantaggi e svantaggi

![](https://i.imgur.com/o5ZvqVu.png)

---

Prossima lezione: [[2 - Modello relazionale]]

