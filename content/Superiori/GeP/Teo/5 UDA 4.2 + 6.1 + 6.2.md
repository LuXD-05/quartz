### Scomposizione del progetto

##### 1) Attività

###### Individuazione

Un progetto è **scomponibile in attività** tramite <u>processo</u> iterativo di <u>definizione di attività sempre + semplici</u> (per realizzare prodotti scomposti in sottoprodotti).

Questo processo termina con la definizione di **compiti elementari** per <u>prodotti + elementari possibile</u>.

###### Definizione

Le attività sono definite in [[4 UDA 4.1#1) Pianificazione|pianificazione]], ma possono sempre subire **revisioni** durante il progetto.

##### 2) Obiettivi

Le attività devono comprendere **obiettivi SMART** che descrivano il <u>contesto da realizzare</u> ed i <u>risultati da ottenere</u>. Deve essere definito anche l'**ambito** del progetto (con stato dell'arte, soggetti interessati, vincoli, situazioni...).

##### 3) Prodotti

Ogni attività deve realizzare dei **prodotti** (*deliverable*) definiti e ogni prodotto necessita di:

1) Essere <u>identificato da un codice univoco</u>,
2) Essere <u>descritto</u> nei dettagli ed eventualmente <u>scomposto in sottoprodotti</u>.

###### Tipi di prodotti

- **Documenti**: progetti, relazioni, report, verbali…
- **Tool**: hw, sw, beni generali;
- **Impianti**: impianti elettrici, di dati, di sorveglianza, di elaborazione…
- **Attività**: (iniziative) funzionali al progetto (eventi di promozione, formazione, riunioni tecniche…)...

###### Sottoprodotti, compiti ed effort

I prodotti sono scomponibili in:

> [!important] Sottoprodotti
> <u>Componenti elementari per realizzare prodotti</u>.

Per sottoprodotti (ma anche prodotti) si possono definire dei:

> [!important] Compiti
> <u>Attività elementari per realizzare prodotti o sottoprodotti</u>.

Per ogni compito è quantificabile il necessario:

> [!important] Effort
> <u>Quantità di tempo usato da 1 o + HR per realizzare un compito</u>.

**Prodotti** $\rightarrow$ **sottoprodotti** $\rightarrow$ **compiti** $\rightarrow$ **effort**.

##### 4) Prerequisiti

(O **input/vincoli**) sono elementi indispensabili per un'attività, tipo: prodotti, tool, UR, tempi, costi… In particolare i prodotti di altre attività (input) che determinano la sequenza delle attività e i tempi totali.

###### Input incerti

Nella [[4 UDA 4.1#1) Pianificazione|pianificazione]] potrebbero <u>mancare delle info</u> sugli **input** (effort attività, tempi, costi imprevisti…), quindi si inseriscono <u>dati temporanei</u> basati sull'<u>esperienza del PM</u> e si attende fino alla <u>progettazione o alla realizzazione per ridefinirli</u>.

##### 5) Tempi

Per calcolare la **durata del progetto** è richiesta la **durata di ogni attività**; per quella di ogni attività va calcolata la **durata di tutti i suoi compiti** e per ogni compito vanno definiti **effort, team e vincoli**.

Attraverso gli **input** si definisce l'<u>ordine delle attività</u> e il <u>tempo minimo di realizzazione</u> ([[12 UDA 9#Gantt|Gantt]]).

##### 6) Costi

###### Tipi

I **costi di progetto** ([[11 UDA 8#Il budget|budget]]) sono di solito divisi per **tipo**:

- **Generali**: spese viaggio, materiale di consumo…
- **Interni**: personale interno o infrastrutture dedicate al progetto;
- **Beni**: materiali, immateriali e infrastrutture;
- **Servizi**: telefonici, dati, assicurazioni…
- **Consulenza**: personale esterno specializzato impegnato nel progetto...

##### 7) Team

Analizzando i **compiti** se ne individuano le **competenze** necessarie; e in base a queste si individuano le **figure** richieste.

Quantificando l'**effort** per ogni attività invece, se ne trovano le **risorse** necessarie e quindi il **tempo** previsto.

##### 8) Responsabilità

Dopo aver individuato le **figure**, gli si assegnano le **responsabilità e autorità d'iniziativa** (<u>da definire in documenti</u>).

### PBS

> [!important] Project Breakdown Structure
> È una <u>struttura analitica e gerarchica che scompone il progetto in</u> **attività** (non gestisce durate, costi, vincoli…).
> Se arriva a dettagliare anche i singoli *work packages* (unità di lavoro) diventa **WBS** (*Work Breakdown Structure*).

È buona norma non scomporre ogni attività in più di **5 sotto-attività**, (distribuibili) per un massimo di **4 livelli**.

##### Codifica

Ogni **attività, prodotto, documento...** di progetto va **codificato univocamente**. I codici mettono in relazione tali elementi e, una corretta codifica, ne consente l'<u>identificazione e la collocazione nel progetto</u>.

###### Composizione dei codici

I **codici** (distinti da altre codifiche di progetto tipo contabilità) sono fatti da:

- **Prefisso**, che identifica il **tipo di elemento**:
	- **A** = <u>attività</u>,
	- **C** = <u>compito</u>,
	- **P** = <u>prodotto</u>…
- **Posizione** nella PBS...

Esempio:  **P1.2\_03** = prodotto 03 della sotto-attività 2 dell'attività 1.

##### PBS per obiettivi realizzativi

Alcuni <u>obiettivi</u> potrebbero prevedere dei <u>macro-prodotti complessi</u> al punto da dover essere realizzati con **sotto-progetti**.

In questi casi, la **PBS** può essere suddivisa in base agli **obiettivi realizzativi** (che diventano <u>attività principali</u>); mentre attività tipo <u>progettazione, realizzazione, dispiegamento…</u> diventano **sotto-attività di ogni obiettivo**.

###### Esempio

--- start-multi-column: ID_lszr
```column-settings
Number of Columns: 2
Largest Column: standard
Border: off
Alignment: center
```

**Fasi** (obiettivi: portale, registro elettronico, piattaforma e-learning):

![](https://i.imgur.com/NIJxT79.png)

--- column-break ---

**Sotto-attività** delle nuove fasi-obiettivo:

![](https://i.imgur.com/clCgepe.png)

--- end-multi-column

