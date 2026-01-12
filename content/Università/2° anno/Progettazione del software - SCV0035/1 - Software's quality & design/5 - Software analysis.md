# Lezione 5

### Analysis

L'analisi del software è **statica** al contrario del [[4 - Software testing|testing]], infatti esamina gli **artefatti** del software (documenti, specifiche, ma anche codice) senza eseguire nulla. Esistono tecniche manuali (***reviews***) e automatizzate (***static analysis tools***) per portarla a termine:

#### Reviews

Una **revisione** valuta un prodotto o uno stato di progetto al fine di identificare incongruenze rispetto ai risultati pianificati e suggerire miglioramenti. In più è applicabile a qualsiasi artefatto (requisiti, specifiche, codice, test, piano, guide...).

> [!important] Obiettivi
> Come obiettivi, la *review* si prefigge di: 
> - **Esaminare l'artefatto e trarne conclusioni** (non serve/manca la funzionalità, il codice dovrebbe essere più veloce/comprensibile...),
> - (Quindi) **trovare difetti** (enfasi sul **trovare**, <u>non correggere</u>).

##### Fasi della review

La *review* si articola in diverse fasi:

![](https://i.imgur.com/EbwkwaQ.png)

###### Planning

Con la **pianificazione** il ***manager*** seleziona il personale (allocandone i ruoli) che prenderà parte alla *review* e di quest'ultima definisce il tempo e i criteri di inizio e di fine.

###### Kick-off

Con il ***kick-off*** il *manager* distribuisce i documenti base della *review* e spiega al personale processi e obiettivi della review. Qui subentrano 2 figure:

- **Autori**: coloro che hanno la responsabilità per il documento da revisionare,
- **Recensori**: figure con uno specifico *background* tecnico o di business in grado di identificare e descrivere difetti.

###### Preparazione individuale

Qui ogni membro analizza individualmente il materiale a disposizione traendone: potenziali difetti, domande, commenti, suggerimenti...

###### Meeting di revisione

Alla **riunione di revisione** si discute quanto analizzato nei documenti col resto del personale, in più vi si aggiungono:

- **Moderatore**: figura centrale che gestisce la review e modera i POV del personale trovando accordi,
- **Scribi**: mettono per iscritto quanto viene discusso nella riunione (POV, problemi, requisiti...).

> [!important] Regole
> Come per ogni *meeting* bisogna seguire delle regole:
> - Per gli autori non bisogna discutere o difendersi ma confrontarsi a mente aperta,
> - Cercare di mantenere la riunione entro le 2 ore,
> - Non tentare di risolvere i problemi trovati nelle review al meeting.

###### Rework & Follow-up

Nel ***rework*** l'autore corregge i difetti identificati e nel ***follow-up*** si verifica effettivamente che tali siano stati risolti e si raccolgono dati per il miglioramento del processo.

##### Gradi di formalità

Esistono diversi tipi di *review* (dalla più formale alla più informale):

![](https://i.imgur.com/AEq5mWO.png)

![](https://i.imgur.com/8Iy7tfQ.png)

###### Inspection

L'**ispezione** è la più sistematica e formale, comprende tutte le fasi e l'obiettivo principale è **trovare *faults*** (con regole, misure, checklist, criteri di inizio e fine, report e follow-up). Tra i partecipanti c'è un moderatore, l'autore, i reviewer e gli scribi; inoltre esistono diversi tipi e variazioni dell'ispezione:

- ***Fagan's code inspection***: specifica per l'**ispezione di codice**, prevede che i <u>team</u> (dev e tester) <u>espongano il loro codice</u> procedura per procedura <u>al</u> resto dei <u>partecipanti</u> cosicché gli altri possano fare considerazioni e trovare eventualmente *faults* (non correggerli). Incentivante in quanto gli errori trovati con l'ispezione non affliggono la valutazione personale dei dev (al contrario di quelli post-ispezione), quindi non c'è neanche la necessità di nasconderli.
- ***Active design reviews***: questo è un modello più simile ad un *brainstorming* in cui l'<u>autore</u>, per evitare che <u>reviewer</u> impreparati non facciano/dicano niente, <u>li sceglie lui e fa delle domande</u> così da avere una risposta e opinione da parte di tutti.
- ***Phased inspection***: semplicemente <u>si divide l'ispezione in più fasi</u>, ispettori singoli per controlli semplici e multipli per controlli complessi.

> [!info] Vantaggi e svantaggi
> L'ispezione è efficace, dettagliata con scrittura di documenti ed è un processo che si migliora ogni volta; tuttavia ha delle limitazioni: non è scalabile e incrementale.

###### Team review

La *team review* è più una discussione di gruppo il cui obiettivo è ottenere il consenso di tutti riguardo un certo approccio tecnico da usare. Un moderatore o l'autore fungono da leader, serve una preparazione *pre-meeting* e le attività sono le solite di review (discutere, fare decisioni, valutare alternative, trovare difetti, definire linee guida...); ha circa i $\frac{2}{3}$ della produttività dell'[[#Inspection|ispezione]] (inoltre il grado di formalità può variare).

###### Walkthrough

Un *walkthrough* prevede che un autore descriva un prodotto ad un gruppo di pari sollecitando commenti. Gli obiettivi sono i soliti delle review ma l'atmosfera è decisamente più informale (50% dell'efficacia nel trovare difetti rispetto all'[[#Inspection|ispezione]]).

###### Pair programming

Quando 2 dev lavorano insieme ad 1 sola *workstation*: 1 scrive codice e l'altro gli dice cosa scrivere. Seppur più costoso, è un metodo che fomenta comunicazione e review continue del codice oltre ad essere meno pesante.

![](https://i.imgur.com/RhK4e0P.png)

###### Peer desk-check

Quando un *reviewer* analizza da solo il codice e poi ne discute con l'autore. Con il ***pass-around*** tra diverse persone ci sono multipli *desk-check* concorrenti e alla fine l'autore mette insieme i risultati (ci sono dei *tool* software per questo, tipo GitHub e GitLab).

###### Ad-hoc review

Qui semplicemente un dev chiede ad un altro di guardare il suo codice e dirgli se tutto va bene.

#### Static analysis tools

Oltre alle modalità manuali di *review* che abbiamo appena visto, è possibile fare delle **analisi statiche automatizzate** grazie a dei tool di analisi statica: <u>strumenti che scansionano il codice per rilevare eventuali difetti senza eseguirlo</u>; alcuni sono: compilatori, *bug pattern detectors*, *style checkers*, *design analyzers*, *data/control flow analyzers*...

Questi permettono di rilevare tanti difetti velocemente, tra cui: loop con più punti di ingresso/uscita o codice irraggiungibile, variabili non inizializzate o mai usate, inconsistenza in dichiarazione e uso di metodi, vulnerabilità, duplicati, *style conventions*, violazione di sintassi, eccezioni ed errori (tipo divisione per 0)...

> [!info] Falsi positivi e negativi
> - **Falsi positivi**: "errori" riportati che non causano problemi $\rightarrow$ non ha senso spendere risorse per sistemarli, meglio concentrarsi su problemi veri.
> - **Falsi negativi**: problemi non riportati che poi rimangono nel prodotto finito.

##### Alcuni strumenti

###### Compilatori

Presentano diversi livelli di avviso con possibilità di disabilitarli o cambiare di priorità certi errori (bilanciamento tra falsi positivi e negativi). Controllano sintassi, tipi, *cross references*, eccezioni...

###### Analizzatori di stile

Rilevano violazioni delle *naming conventions*, commenti mancanti, duplicati, difetti di design (in quanto uno stile consistente e pulite rende il codice più comprensibile e corretto).

###### Analisi di design e architettura

Necessario in sistemi complessi / senza documentazione o dev / architettura obsoleta o degradata... verifica se l'architettura è implementata, se il sistema è conforme e la testabilità. Identifica problemi come classi grandi, uso improprio di OOP, cicli e *bottlenecks*...

###### Analisi del flusso di dati

Analisi di un software in base agli eventi che una variabile attraversa: **definizione** (alla variabile viene dato un nuovo valore), **uso** (un'istruzione legge il valore della variabile e lo usa) e **annullamento** (il valore della variabile non esiste più). Esempio simile è fatto con gli eventi dei **file** (*open, close, read, write...*).

> [!example] Regole
> - L'uso deve sempre essere preceduto dalla definizione, senza annullamenti intermedi.
> - La definizione deve sempre essere seguita da almeno 1 uso prima di una ridefinizione o annullamento.

---

Prossima lezione: [[6 - Design in piccolo]]

