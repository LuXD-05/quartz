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

##### Tipi di review

Esistono diversi tipi di *review* (dalla più formale alla più informale):

![](https://i.imgur.com/AEq5mWO.png)

###### Inspection

###### Team review

###### Walkthrough

###### Pair programming

###### Peer desk-check

###### Ad-hoc review

#### Static analysis tools

![](https://i.imgur.com/ZErqfdU.png)

---

Prossima lezione: [[]]

