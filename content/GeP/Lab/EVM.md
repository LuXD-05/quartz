### Cos'è

L'**EVM** (*Earned Value Method*) è un metodo di controllo di costi e tempi (2 delle variabili + rilevanti) di un progetto.

Esso si fa durante il progetto e opera calcolando 3 valori di costo rispetto a una data prefissata detta "*timenow*" nella quale si vogliono fare delle stime per capire l'andamento del progetto.

I 3 valori di costo sono: [[#PV]], [[#AC]] ed [[#EV]].

#### Indicatori 1

Premessa: 

- **BT** = <u>Budget totale</u>.
- **TT** = <u>Tempo totale</u>.

##### PV

(O *Planned Value*, <u>quanto si dovrebbe aver speso in base ai tempi</u>), corrisponde alla **somma di tutte le stime dei costi prima del *timenow*** <u>in base al tempo trascorso rispetto al TT</u> (per attività incompiute se ne calcola la <u>% effettuata sempre in base al tempo</u>, anche se non corrisponde alla % effettivamente compiuta).

##### AC

(O *Actual Cost*, <u>quanto si ha veramente speso</u>), la **somma effettiva dei costi fino al *timenow*** (<u>per ogni costo</u> sostenuto, <u>riportare la % di completamento dell'attività</u> associata di fianco al costo).

##### EV

(O *Earned Value*, <u>quanto si dovrebbe aver speso in base alla % di completamento delle attività</u>), corrisponde alla **somma di tutte le stime dei costi fino al *timenow*** in base alla % di completamento di ogni singola attività (sul costo totale stimato all'inizio, non su quello effettivamente sostenuto).

#### Indicatori 2

##### CPI

(O *Cost Performance Index*) con $CPI \;=\; \dfrac{EV}{AC}$. 

Un valore **< 1** indica che i **costi sono oltre il budget**, altrimenti rispettano le previsioni o anche meglio ne sono inferiori.

##### SPI

(O *Schedule Performance Index*) con $SPI \;=\; \dfrac{EV}{PV}$. 

Un valore **< 1** indica che i **tempi sono oltre il limite**, altrimenti rispettano le previsioni o anche meglio ne sono inferiori.

##### EAC

(O *Estimated cost At Completion*) con $EAC \;=\; AC + (BT - EV) / CPI$. 

Questa è una **stima del futuro costo totale del progetto fatta al *timenow***, <u>se l'andamento dei costi rimanesse quello ricavato al timenow</u>.

##### SAC

(O *Schedule At Completion*) con $SAC \;=\; \dfrac{TT}{SPI}$. 

Questa è una **stima della durata totale del progetto fatta al *timenow***, <u>se l'andamento dei costi rimanesse quello ricavato al timenow</u>.

#### Considerazioni

Poi dipende tutto dall'importanza delle variabili. Se i costi sono + importanti e l'EAC supera il BT, allora conviene allungare i tempi e ridurre i costi.

### Esercizi

##### 1

Si hanno 10000 € per la costruzione di negozi + 5000€ per marketing e consulenze in 12 mesi. 

(Qui 5000€ non è detto che sia suddiviso in 12 mesi; si capisce che non è una spessa vincolata dal tempo dal fatto che in PV ed EV sia messo 100%, in altri es va esplicitato)

###### Analisi

Dal testo si notano diverse cose:

- TT = 1 anno = 12 mesi
- BT = 105000 €
- (Negozi da aprire = 3)
- Timenow = 2 mesi = 16.666% di 12 mesi
- Spese marketing al timenow = 6800 € = 100% di 5000 €
- Spese negozi al timenow = 28500 € = circa 28.5% di 100000 €
- Completamento = quasi 1 su 3 negozi (quasi 33%, quindi un 30%)

###### Indicatori 1

**PV** = 100% 5000 + 16.6% 100000 = 5000 + 16660 = 21660 €

**AC** = 6800 + 28500 = 35300 €

**EV** = 100% 5000 + 30% 100000 = 5000 + 30000 = 35000 €

Il 100% di marketing in PV significa che tutto il budget del marketing è stato usato (sempre su 5000, non su quello effettivamente speso), mentre in EV significa che l'attività è stata portata al termine.

Il 16.6% in PV in quanto su 12 mesi, 2 sono il 16.6%; mentre il 30% in EV indica il "quasi" completamento di 1 negozio su 3 (poco meno di 33%).

###### Indicatori 2

$CPI \;=\; \dfrac{35000}{35300} \;=\; 0.99 \;\rightarrow\;$ < 1, i costi sono leggermente + alti delle stime.

$SPI \;=\; \dfrac{35000}{21660} \;=\; 1.62 \;\rightarrow\;$ > 1, per quanto riguarda i tempi invece il progetto è piuttosto avanti rispetto alle stime.

${} EAC \;=\; 35300 + (105000 - 35000) / 0,99 \;=\; 106000 {}$€$\;\rightarrow\;$ il costo finale previsto di progetto con tale andamento supererà di poco quello previsto all'inizio.

$SAC \;=\; \dfrac{12}{1,62} \;=\; 7,4 \; mesi \;\rightarrow\;$ il progetto durerà poco più della metà del tempo previsto originariamente.

##### Esercizio 2

###### Analisi

74000€ è progettazione, quindi è al 100% (finita) perché poi inizia la realizzazione.

Meglio fare un 100% di 75000€ sia in PV sia in EV in quanto l'attività progettazione finisce prima della realizzazione, quindi 100% perché è finita (anche se spesi solo 74000, 75000 è il costo pianificato prima)

...

##### Verifica

Azienda con 5 ospedali vuole rifare l'infrastruttura di rete di tutti in 1 anno. Budget di 250k con 35% in cablaggio e 65% in rete. Valutare l'avanzamento del progetto a 7 mesi sapendo che la rete è stata installata in 3 ospedali al costo di 96k, mentre il cablaggio è stato completato dappertutto con 86k totali.

###### Analisi

(5 strutture tot)

TT = 12 mesi

BT = 250k

35%BT = cablaggio = 87500

65%BT = rete = 162500

Timenow = 7 mesi

(3 strutture al timenow completate) 

Cablaggio = 100% 86000€

Rete = 60% 96000€

###### Indicatori 1

PV = 100% 86000 + 58,3% 96000 (56000) = 142000€

AC = 86000 + 96000 = 182000€

EV = 100% 86000 + 60% 96000 (57.600) = 143600€

###### Indicatori 2

CPI = 143600/182000 = 0,79

SPI = 143600/142000 = 1,01

EAC = 182000 + (250000 - 143600) / 0,79 = 365063,3€

SAC = 12 / 1,01 = 11,9 mesi

