# Lezione 5

### Metodologie di progettazione

Progettare un db significa definirne struttura e contenuti ed è strutturata in fasi ognuna basata su un **modello** che permette di rappresentare il db ad un certo livello di astrazione in modo standard. Le fasi della progettazione di un db sono:

##### Raccolta e analisi dei requisiti

In questa fase sono definite le caratteristiche del db e del contesto (di solito in maniera informale) e viene prodotto un documento di specifica dei requisiti, il quale contiene:

- **Requisiti informativi**: le caratteristiche dello schema del db,
- **Requisiti operazionali**: che tipo di operazioni dovranno essere svolte e quindi realizzate,
- **Requisiti di vincoli e autorizzazioni**: le proprietà di correttezza e protezione da assicurare ai dati,
- **Requisiti sul volume dei dati**: quali e quanti dati ci si aspetta nel db.

##### Progettazione concettuale

La progettazione concettuale fa uso di un modello concettuale detto **ER** (*entity-relationship*) che permette di definire lo schema concettuale del db, specificando anche:

- **Entità**: descritte da insiemi omogenei di oggetti, caratterizzate da proprietà comuni...
- **Generalizzazioni**: casi in cui un oggetto è un caso particolare di un altro,
- **Attributi**: proprietà specifica di un'entità che la caratterizza,
- **Associazioni**: legami logici tra più entità che rappresentano una certa azione,
- **Vincoli**: limiti e restrizioni imposte ad entità e relazioni,
- ...

###### Generazione di ER

Spesso gli ER sono costruiti mediante raffinamento/integrazione di più schemi intermedi e ci sono 2 strategie per farlo:

![](https://i.imgur.com/dk9EvKK.png)

Anche se la più usata è una strategia mista, che parte individuando entità e associazioni principali per integrarle in una sorta di <u>schema scheletro</u>, per poi integrare ogni singolo sotto-schema derivato dallo scheletro nell'ER finale.

##### Progettazione logica

La progettazione logica consiste nel tradurre lo schema ER in uno **schema logico**, definito in base al modello logico del DBMS scelto, considerando anche integrità, sicurezza ed efficienza della soluzione.

##### Normalizzazione

Tramite appositi strumenti è quindi possibile verificare la qualità dello schema logico prodotto, talvolta attraverso la ristrutturazione dello schema. Questo processo (nel caso di db relazionali) è detto **normalizzazione** e verifica (principalmente) che non ci siano dati ridondanti dallo schema logico.

##### Progettazione fisica

In quest'ultima fase vengono effettuate alcune scelte circa la memorizzazione fisica dei dati, producendo uno schema fisico che descrive le strutture di memorizzazione ed accesso ai dati sui supporti fisici.

---

Prossima lezione: [[6 - Progettazione concettuale]]

