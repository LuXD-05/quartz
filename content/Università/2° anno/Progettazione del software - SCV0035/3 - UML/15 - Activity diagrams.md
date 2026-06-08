# Lezione 15

### Activity diagrams

Gli ***activity diagrams*** sono dei diagrammi dinamici simili agli *[[14 - State diagrams#State diagrams|state diagrams]]* che però non rappresentano stati, bensì il <u>processo/flusso di un'attività o azione</u> complessa, indicandone i singoli step e le più piccole unità di elaborazione e come si susseguono nel flusso (applicabili anche a classi o *use-case*).

Questi sono quindi più utilizzati per descrivere <u>elaborazioni interne e</u> anche <u>workflow</u> (agevolando la visione della concorrenza e la suddivisione delle responsabilità) rispetto agli *state diagrams*, che sono più adatti a descrivere eventi e transizioni tra stati di un sistema.

##### Elementi

Gli elementi grafici corrispondono circa a quelli degli *state diagrams*:

- **Attività**: (corrisponde a uno stato negli *state diagrams*) può contenere <u>sotto-attività</u> ed avere più <u>copie</u> di se stessa <u>eseguite in parallelo</u> contrassegnandola con `*`:

  ![](https://i.imgur.com/2phv6wA.png),

- **Fork** e **join**: separano e ricongiungono rispettivamente più flussi di esecuzione concorrenti:

  ![](https://i.imgur.com/HDqP07g.png),

- **Branch** e **merge**: delineano e ricongiungono rispettivamente più flussi di esecuzione alternativi in base ad una condizione (`if/else`):

  ![](https://i.imgur.com/dspVZ4A.png),

- ***Entry/exit points***: rispettivamente indicano *entry point* di attività, *exit point* di attività e punto di terminazione dell'intero flusso:

  ![](https://i.imgur.com/2ehCLXn.png),

- **Oggetti** e **stereotipi**: oggetti e stereotipi scambiabili tra varie attività:

  ![](https://i.imgur.com/QhaPj4l.png)

##### Altre caratteristiche

###### Condizioni

C'è la possibilità di definire precondizioni e postcondizioni rispetto ad una certa azione così:

![](https://i.imgur.com/5N00NXm.png)

###### Class notation

Si possono indicare certe attività come classi usando la loro stessa notazione:

![](https://i.imgur.com/ipaxtHU.png)

###### Wormholes

Con diagrammi grandi e complessi è possibile, per non "pasticciare" troppo con le frecce, farle entrare ed uscire da un punto con lo stesso nome come in esempio:

![](https://i.imgur.com/sCWxDor.png)

###### Parametri

Le attività possono avere parametri (ed eccezioni) che si indicano così:

![](https://i.imgur.com/FlYXzem.png)

C'è analogia tra parametri e valori di ritorno di una funzione e quelli delle attività:

![](https://i.imgur.com/TZYSHZg.png)

###### Responsabili

Si può indicare il responsabile di un'attività tra parentesi:

![](https://i.imgur.com/VAqeMsT.png)

Alternativamente si possono usare delle ***swimlanes*** per indicare la distribuzione delle responsabilità:

![](https://i.imgur.com/VQyoOjf.png)

Le quali possono anche essere multidimensionali:

![](https://i.imgur.com/So3y5YX.png)

###### Race

Possono verificarsi condizioni di ***race***, ovvero quando si hanno più flussi paralleli che evolvono verso una conclusione (che possono anche condividere dati):

![](https://i.imgur.com/sgkOxgj.png)

In tal caso il 1° flusso che raggiunge la fine fa abortire l'altro.

###### Eccezioni

Per gestire eccezioni invece si usano:

![](https://i.imgur.com/q3DV76d.png)

---

Prossima lezione: [[16 - Other diagrams]]

