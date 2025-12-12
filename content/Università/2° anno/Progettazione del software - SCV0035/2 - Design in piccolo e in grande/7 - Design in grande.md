# Lezione 7

### Design in grande

##### Obiettivi

L'obiettivo principale del design è comprendere al meglio la complessità nello sviluppo di software; e ciò si ottiene scomponendo il problema in sottoproblemi più piccoli, riducendo così la complessità complessiva. Nello specifico:

- **Design per modifiche**: <u>anticipare</u> eventuali <u>modifiche</u>, <u>concentrarsi</u> di più sull'<u>evoluzione del software</u> piuttosto che al suo <u>stato corrente</u> (esempi di modifiche: in algoritmi, in strutture dati, in hardware sottostante tipo OS o DB, strategia di programmazione...).
- **Design per varianti** (*program family*): considerare e pianificare le <u>varianti di un software</u> fin dall'inizio invece che progettarne ognuna individualmente (esempio: programma per hotel che gestisce le prenotazioni ma camere, tempi, tariffe... tutte diverse).

> [!info] Risultati
> La progettazione "in grande" produce l'architettura del software (*software design*) che definisce il sistema come componenti computazionali e interazioni tra essi.

#### Prospettive

Ci sono 2 prospettive complementari che descrivono il software design:

##### Meccanismi

<u>Descrivono un'architettura in base ai componenti coi quali è costruita</u>, identificando <u>moduli, interfacce e le relazioni</u> tra essi. Per esempio, è come descrivere una macchina come motore, ruote, sedili... tutti messi insieme.

###### Principi chiave

I moduli dovrebbero essere <u>unità auto-contenute</u> (massimizzare coesione) con <u>poche relazioni con altri</u> moduli (minimizzare interconnessioni), con focus sull'***information hiding*** così da <u>rendere chiaro cosa fa</u> il modulo anche attraverso la sua interfaccia ma sempre <u>nascondendo comportamenti e modifiche ai suoi attributi interni</u> privati (così che tali non influenzino *client* esterni che fanno uso del modulo).

![](https://i.imgur.com/5O7ffRp.png)

> [!example] Esempio
> Un esempio è una **tabella** nella quale uno può <u>inserire, cancellare o stampare informazioni</u> tramite i metodi d'<u>interfaccia</u> `insert`, `delete` e `print`; infatti il modulo è usabile sempre e i comportamenti al suo interno possono essere modificati senza influire sul *client* intaccando i risultati.

###### Relazioni tra moduli

I **[[6 - Design in piccolo#Moduli|moduli]]** sono legati da delle relazioni. Innanzitutto le definiamo come <u>non riflessive e non transitive</u> cosicché vadano a creare una gerarchia di moduli anche rappresentabile tramite **DAG** (*Directed Acyclic Graphs*):

![](https://i.imgur.com/y6ZwEMb.png)

Esistono 3 tipi di relazioni tra moduli:

- "***Uses***": Quando un modulo $A$ utilizza i servizi dell'interfaccia di un altro $B$: la relazione è "statica" ed $A$ dipende da $B$ (quindi la qualità di $B$ influisce su quella di $A$).
- "***Is component of***": Descrive quando un modulo di livello superiore $B$ è composto da altri di livello inferiore $A_{n}$; in questo modo si forma una gerarchia di moduli, tuttavia i moduli superiori sono puramente nominali, nel senso che il prodotto finito sarà composto solo dalle "foglie" della gerarchia (moduli finali di livello più basso).
- "***Inherits from***": Nelle architetture con OOP, quando un componente $A$ estende le funzionalità di un altro $B$ (qui l'erede $A$ può accedere a certi servizi non esposti a tutti di $B$, quindi è una relazione più "forte" rispetto a *uses*).

##### Stili

<u>Distinguono le architetture dalle altre in base alla loro tipologia</u>, definendo i tipi di componenti (client, server, db, filtri, livelli...) e le interazioni (chiamate di funzioni, multicast di eventi, pipe...). Riprendendo l'esempio di prima, sarebbe come descrivere la macchina in base al tipo: coupé, van, station wagon...

Alcuni esempi di stili di progettazione software:

###### Functional architecture

In un'architettura funzionale il sistema è appunto scomposto in varie **funzioni** (viste come *subroutines*) che si richiamano a vicenda; alcune dette ***connettori*** ritornano o interagiscono con dati condivisi dalle varie funzioni. Questo è lo stile tradizionale di programmazione o usato anche con la OOP (funzioni = metodi, dati = classi).

![](https://i.imgur.com/7drJwjk.png)

###### Layered system

I sistemi a strati sono organizzati in livelli di astrazione come una gerarchia di componenti astratti definita con "***Uses***", la quale va a creare la famosa ***[onion-layer architecture](https://medium.com/expedia-group-tech/onion-architecture-deed8a554423)***.

![](https://i.imgur.com/qfFq7Pw.png)

###### Pipes & filters

Questo modello si compone di **filtri** (componenti che ricevono e ritornano dati) e ***pipes*** (connettori che permettono il flusso di dati); architettura semplice e modificabile ma tipica di processi batch e del "modello Unix".

![](https://i.imgur.com/KZdnsx6.png)

###### Event-based system

Sistemi che si basano sugli **eventi** trasmessi a tutti i componenti (registrati per tale evento, tipo modello pub/sub) senza esplicita nomina del componente target. Modello flessibile e usato sempre di più in software moderni come quelli con interfaccia grafica, unica complessità può essere l'ordinamento degli eventi.

![](https://i.imgur.com/R9D2FhO.png)

###### Repository-based system

Sistemi che si basano su ***repository*** centralizzate attraverso le quali i componenti comunicano:

![](https://i.imgur.com/piFXFJa.png)

Ci sono 2 casi:

- ***Database***: la *repository* è passiva e i componenti sono attivi (sono loro che iniziano e terminano le operazioni di lettura/scrittura sul db).
- ***Blackboard***: qui cambia solo che la *repository* è attiva, ovvero i suoi cambiamenti di stato attivano certi componenti (tipo *webhooks*?).

---

Prossima lezione: [[8 - Linguaggi descrittivi]]

