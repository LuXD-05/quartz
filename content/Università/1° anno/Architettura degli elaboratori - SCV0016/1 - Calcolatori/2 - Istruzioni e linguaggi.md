# Lezione 2

### Istruzioni e operazioni

Un'esecutore è definito in base a 3 elementi:

1) Il **linguaggio** (insieme di istruzioni elementari che è capace di compiere),
2) La **sintassi** (le istruzioni che capisce),
3) La **semantica** (le operazioni che associa ad ogni istruzione).

##### Operazioni fisse e proprie delle istruzioni

Un calcolatore, per ogni istruzione, esegue diverse <u>operazioni fisse</u>:

1) **Preleva dalla memoria l'istruzione** da eseguire,
2) **Esamina l'istruzione** e capisce cosa deve fare,
3) **Esegue l'istruzione** (quindi le <u>operazioni elementari proprie</u> dell'istruzione corrispondenti al suo significato).

Esempio: ipotizziamo che un'istruzione o comando sia "prendi un caffe", in questo caso le operazioni comprendono: alzarsi, camminare verso la macchinetta, ordinare il caffe...

##### Linguaggio

> [!important] Linguaggio 
> **Insieme delle istruzioni** (o comandi) **che un esecutore è in grado di comprendere ed eseguire**.

###### Caratteristiche del ML

Il **linguaggio macchina** (o **ML/L0**) è un linguaggio compreso dalle **CPU** (<u>non univoco</u> per tutti ma unico per CPU). 

Caratteristiche:

- **Binario**: le <u>istruzioni</u> sono <u>codificate in sequenze di 0 e 1</u>,
- **Di basso livello**: ogni <u>istruzione ha effetti elementari</u>,
- **Di poca complessità**: scrivere <u>programmi lunghi è tedioso e prono a errori</u> (proprio per questo l'[[1 - Astrazione e macchine virtuali#Astrazione|astrazione]] è fondamentale).

### Da L0 a L1

Il calcolatore (come macchina fatta da transistor) "capisce" (riesce a interpretare) le istruzioni in ML ma, per le [[#Caratteristiche del ML|caratteristiche]] appena citate più complessità e costi eccessivi, ci si prepone l'obiettivo di definire una **VM** che capisca un linguaggio **L1**, più potente e facile da usare di **ML**. 

Perciò i passi sono:

1) Definire l'insieme di <u>istruzioni</u> che fanno parte di <u>L1</u>,
2) Usare le <u>istruzioni di L0 come operazioni di L1</u> (ricordiamo: \[1 istruzione] = \[+ operazioni]),
3) Definire <u>quali</u> di queste <u>operazioni L1</u> sono <u>associate a quali istruzioni L1</u>.

##### Esempio di realizzazione di $M_{1}$

Sono definiti:

$M_{0}$ = **macchina fisica** (preconfigurata/data non ci interessa come funziona),

$M_{1}$ = **macchina astratta**,

${} L_{0}$ = **linguaggio della macchina fisica**,

$L_{1}$ = **linguaggio della macchina astratta**,

$M_{0}$ capisce $L_{0}$, che comprende le istruzioni $\{\; I_{0}, I_{1}, I_{2} \;\}$

$M_{1}$ capisce $L_{1}$, che comprende le istruzioni ${} \{\; J_{0}, J_{1}, J_{2} \;\}$

$M_{1}$ è una macchina di + alto livello di $M_{0}$, ovvero le sue istruzioni sono + potenti e facili da usare.

Dato che le istruzioni di ${} L_{1}$ sono definite in termini di istruzioni di $L_{0}$, sappiamo che ogni istruzione $J_{k}$ corrisponde a una sequenza di istruzioni in $L_{0}$, quindi ipotizziamo:

$J_{0} = I_{0},I_{1},I_{1},I_{2}$

$J_{1} = I_{1},I_{2}$

$J_{2} = I_{2},I_{0},I_{1}$

Quindi, definendo a quali istruzioni di $L_{0}$ quelle di $L_{1}$ corrispondono, allora:

$J_{2},J_{0},J_{1} =$ $I_{2},I_{0},I_{1},I_{0},I_{1},I_{1},I_{2},I_{1},I_{2}$

###### Possibile modo per realizzare $M_{1}$?

Una soluzione potrebbe essere incorporare direttamente $M_{0}$ in $M_{1}$; cosicché ogni volta che esegue un'istruzione in $L_{1}$ si richiede a $M_{0}$ di eseguire le corrispondenti istruzioni di $L_{0}$.

![](https://i.imgur.com/S7LDmIZ.png)

Il nuovo problema che sorge è quindi capire come tradurre le istruzioni in $L_{1}$ ad istruzioni in $L_{0}$.

# Esercizi

# Soluzioni

---

Prossima lezione: [[3 - Traduzione tra linguaggi]]

