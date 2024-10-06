---
public: true
edited_seconds: 290
modified_at: 20/06/2024 19:42:18
---

### a
**Modelli di descrizione fasi**
Tipi di fase
Macro-fasi (o macro-attività)
Sono **fasi/attività suddivise in sotto-attività nel PBS**. Nei diagrammi gerarchici sono i **rami** del grafo.
Fasi finali (o attività finali)
**Attività atomiche non più scomponibili** (dettagliano al max altre attività). Nei diagrammi gerarchici sono le **foglie**.
![](https://i.imgur.com/9RKNxGE.png)
Modelli di schede
Sono presentati **2 modelli di layout** per descrivere le **attività finali** e le **macro-attività**. Come per la progettazione di fasi, anche la compilazione delle schede avviene **per passi**. Se presenti nuove info è possibile **aggiornare le schede** e quella finale si può avere in momenti diversi in funzione dell'attività (o anche progetto) trattata.
Modello di scheda per attività finali
![](https://i.imgur.com/r25ArMT.png)
Codici
(*) I codici usati per la tipologia sono:
- **P** = Progetti e relazioni tecniche,
- **R** = Report di monitoraggio tecnico e amministrativo,
- **D** = Documentazione varia (corrispondenza, amministrativa…),
- **I** = Attrezzature e impianti,
- **S** = Software,
- **H** = Hardware,
- **A** = Servizi (formazione, assistenza, supporto, riorganizzazione…),
- **F** = Infrastrutture (facilities),
- **V** = Verbali (del comitato di programma, di collaudo…) …
VALGONO ANCHE PER SCHEDA MACRO-ATTIVITA'.
Modello di scheda per macro-attività
![](https://i.imgur.com/ZK9OTfC.png)
Differenze tra le 2 schede
- Prodotti macro-attività = elenco prodotti sotto-attività (senza il loro dettaglio),
- Inizio-fine macro-attività = inizio 1° sotto-attività – fine ultima sotto-attività,
- Durata macro-attività != somma durate sotto-attività, perché alcune possono essere parallele,
- Costo macro-attività = somma costi sotto-attività 1° livello inferiore,
- Prerequisiti macro-* dipendono da output esterni, mentre quelli di 1 sotto-* risolti all'interno di sotto-* stessa,
- Macro-attività possono avere anche vincoli propri oltre a quelli di sotto-attività,
- Processo realizzazione di macro-attività è un semplice workflow di sotto-attività del 1° livello inferiore.
Queste 2 schede sono il risultato di varie **rielaborazioni e integrazioni**; e si nota che alcuni elementi (sottoprodotti, compiti, vincolo, tempi…) non sono ancora stati analizzati/studiati.

### Schedulazioni di progetto
> [!important] Schedulazione
> **Suddivisione di info in componenti e sub-componenti rispetto a 1 o + elementi/criteri**.
 
Le schedulazioni sono **meccanismi** che consentono l'immediata **identificazione e collocazione di** tutti gli **elementi**. Di solito sono fatte con **tabelle** (dove le stesse info sono schedulabili a + livelli in funzione del dettaglio dei sub-componenti).
Il **PBS** (o schedulazione di progetto) è la **schedulazione di** un **progetto** secondo le **fasi temporali delle sue attività**; ed è il **presupposto per tutte le altre schedulazioni** di progetto.

### Tipi di schedulazione
##### Per prodotti
Questa **elenca i prodotti da realizzare in ogni attività**. È una di quelle fondamentali perché usata sia in pianificazione sia in monitoraggio/verifica delle attività. Permette di monitorare lo stato di avanzamento di un progetto secondo il principio che: consegna di prodotto = completamento attività.
![](https://i.imgur.com/uNtGgwA.png)
###### Per sotto-prodotti
A ogni **sottoprodotto** si può associare un'**attività elementare** per realizzarlo; e questa schedulazione facilita:
- **L'individuazione** di **sotto-attività**,
- **L'assegnazione di responsabilità** nel team,
- La **gestione** delle **attività** di **monitoraggio** durante 1 singola attività di progetto.
(stessa foto schedulazione per prodotti)
##### Per compiti
Compito elementare = **attività realizzabile in 1 o + giorni da 1 o + persone** specializzate in certi ambiti.
I compiti si ottengono **dettagliando le attività** fino ad avere **compiti specifici** per ogni singolo **prodotto**.
**Compiti** aventi altri **sotto-compiti** (= con livelli di dettaglio >), di solito **appesantiscono la gestione**.
La realizzazione di questa:
- Richiede **figure** competenti in grado di **individuare**, **definire** e **quantificare** i singoli **compiti**,
- Viene **completata quando** il **team** è in **fase avanzata di costruzione**.
È anche questa una schedulazione fondamentale perché **facilita**:
- La **definizione di competenze, effort e tempo per le attività**,
- **L'assegnazione** di **compiti** e **responsabilità** al **team**.
##### Per effort, durate e costi
(Si ipotizza che questa sia stata fatta quando **non ancora definiti vincoli e priorità**; quindi effort, durate e costi sono da verificare).
**Effort** e **costi di ogni macro-attività** sono la **somma di effort e costi delle sotto-attività**, mentre la **durata** è valutata **solo** per le **sotto-attività** in quanto quella delle **macro-attività non** è **definibile** perché dipende da vincoli non ancora finiti.
![](https://i.imgur.com/f7p85pb.png)
