---
public: true
edited_seconds: 50
modified_at: 09/04/2024 16:15:31
---
### Uso
L'EVM si fa durante il progetto, rispetto a una data detta "*timenow*", ovvero un tempo nel progetto in cui si fanno delle stime per capire l'andamento del progetto.
### Indicatori
Premessa: 
- BT = Budget Totale.
- TT = Tempo Totale.
##### PV
(O *Planned Value* / valore pianificato), quello che dovresti aver speso in base ai tempi
##### AC
Quello che ho veramente speso.
##### EV
Quello che si dovrebbe aver speso in base alla % di completamento del progetto.
### Esempio
Si hanno 10000 € per la costruzione di negozi + 5000€ per marketing e consulenze in 12 mesi. 
(Qui 5000€ non è detto che sia suddiviso in 12 mesi. si capisce che non è una spessa vincolata dal tempo dal fatto che in PV ed EV sia messo 100%. in altri es va esploicitato)
##### CPI
(O *Cost Performance Index*) con $CPI \;=\; \dfrac{EV}{AC}$. Un valore < 1 indica che i costi sono oltre il budget, altrimenti rispettano le previsioni o anche meglio ne sono inferiori.
##### SPI
(O *Schedule Performance Index*) con $SPI \;=\; \dfrac{EV}{PV}$. Un valore < 1 indica che i tempi sono oltre il limite, altrimenti rispettano le previsioni o anche meglio ne sono inferiori.
##### EAC
(O *Estimated cost At Completion*) con $EAC \;=\; AC + (BT - EV) / CPI$. Questa è una stima del futuro costo totale del progetto fatta al timenow, se l'andamento dei costi rimanesse quello ricavato al timenow.
##### SAC
(O *Schedule At Completion*) con $SAC \;=\; \dfrac{TT}{SPI}$. Questa è una stima fatta al timenow della durata totale del progetto, se l'andamento dei costi rimanesse quello ricavato al timenow.
### Considerazioni
Poi dipende tutto dall'importanza delle variabili. Se i costi sono + importanti e l'EAC supera il BT, allora conviene allungare i tempi e ridurre i costi.
### Esercizio
74000€ è progettazione, quindi è al 100% (finita) perché poi inizia la realizzazione.
Meglio fare un 100% di 75000€ sia in PV sia in EV in quanto l'attività progettazione finisce prima della realizzazione, quindi 100% perché è finita (anche se spesi solo 74000, 75000 è il costo pianificato prima)