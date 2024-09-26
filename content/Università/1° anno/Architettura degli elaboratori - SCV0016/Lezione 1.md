### Intro

> [!important] Calcolatore
> Sistema digitale che esegue una sequenza di istruzioni dette programma, operando su dei dati per ottenere dei risultati.
> I calcolatori sono caratterizzati da una complessa organizzazione interna.

I circuiti elettronici di un calcolatore consentono l'esecuzione di un set di istruzioni limitato, di bassa complessità (tipo caricare un dato in una locazione di memoria, sommare 1 interi...).

L'utente è colui che adatta il comportamento del calcolatore alle sue esigenze, modificando: i programmi e i dati.

##### Astrazione

> [!important] Astrazione
> Nascondere (ignorare) dettagli per semplificare un problema.
> Molto utile per affrontare problemi complessi, per esempio coi DBMS e database: le tabelle sono solo una struttura astratta su cui l'utente si concentra, trascurando la già configurata struttura fisica.

Il calcolatore può essere descritto e costruito come una gerarchia di macchine astratte o virtuali (VM?), dove ogni livello maschera i gettagli dei livello sottostanti. Ciò permette di concentrarsi sul funzionamento di singoli livelli in esame ("trascurando" i sottostanti se già funzionanti).

(Già solo un programma moderno si basa completamente sull'astrazione: 1) si costruisce la macchina fisica con istruzioni elementari, 2) si costruisce un OS basato sulle istruzioni della macchina e 3) si scrive il programma basato sulle caratteristiche dell'OS e non della macchina).

##### Istruzioni e operazioni

Un'esecutore è definito in base a:

1) L'insieme delle operazioni elementari che è capace di compiere,
2) La sintassi (insieme delle istruzioni che capisce),
3) La semantica (le operazioni che associa ad ogni istruzione che riconosce).

Un calcolatore, per ogni istruzione, esegue diverse operazioni:

1) Preleva dalla memoria l'istruzione da eseguire,
2) Esamina l'istruzione e capisce cosa deve fare,
3) Esegue l'istruzione (ovvero le operazioni elementari corrispondenti al suo significato).

Quindi, in parole semplici, ipotizziamo che un'istruzione o comando sia "prendi un caffe", in questo caso le operazioni comprendono: alzarsi, camminare verso la macchinetta, ordinare il caffe...

##### Linguaggio

> [!important] Linguaggio 
> Insieme delle istruzioni (o comandi) che un esecutore è in grado di comprendere ed eseguire.

Il **linguaggio macchina** (o **ML/L0**) è un linguaggio compreso dalle CPU (non univoco per tutti ma unico per CPU); caratteristiche:

- Binario: le istruzioni sono codificate in sequenze di 0 e 1,
- Di basso livello: ogni istruzione ha effetti elementari,
- Scrivere programmi lunghi è tedioso e prono a errori (proprio per questo l'[[#Astrazione|astrazione]] è fondamentale).

Il calcolatore "capisce" (riesce a interpretare) le istruzioni che fanno parte del ML; perciò l'obiettivo è definire una macchina che capisca un linguaggio L1 + potente e facile da usare di L0. Quindi:

1) Definire l'insieme di istruzioni che fanno parte di L1,
2) Usare le istruzioni di L0 come operazioni di L1,
3) Definire quali operazioni sono associate a quali istruzioni.

###### Esempio

Sono definiti:

$M_{0}$ = macchina fisica (preconfigurata/data non ci interessa come funziona),

$M_{1}$ = macchina astratta,

${} L_{0}$ = linguaggio della macchina fisica,

${} L_{1}$ = linguaggio della macchina astratta,

$M_{0}$ capisce $L_{0}$, che comprende le istruzioni $\{\; I_{0}, I_{1}, I_{2} \;\}$

$M_{1}$ capisce $L_{1}$, che comprende le istruzioni ${} \{\; J_{0}, J_{1}, J_{2} \;\} {}$

$M_{1}$ è una macchina di + alto livello di $M_{0}$, ovvero le sue istruzioni sono + potenti e facili da usare.

Dato che le istruzioni di ${} L_{1}$ sono definite in termini di istruzioni di ${} L_{1}$, ipotizziamo:

$J_{0} = I_{0},I_{1},I_{1},I_{2}$

$J_{1} = I_{1},I_{2}$

$J_{2} = I_{2},I_{0},I_{1}$

Quindi, definendo a quali istruzioni di $L_{0}$ quelle di $L_{1}$ corrispondono, allora:

$J_{2},J_{0},J_{1} = ...$

##### Come realizzare $M_{1}$?

Una soluzione potrebbe essere incorporare $M_{0}$ in $M_{1}$

Ogni volta che si deve eseguire un0istruzione di L1 si richiede a M0 di eseguire le corrispondenti istruzioni di L0.

...

Ci sono quindi diverse possibilità per passare da L1 a L0:

###### Compilazione

- (O traduzione), in questa un apposito programma (detto **compilatore**) traduce il programma $P_{L_{1}}$ scritto in $L_{1}$ in un programma $P_{L_{0}}$ scritto in $L_{0}$,
- Il nuovo programma PL0 viene quindi eseguito

(i 2 programmi fanno la stessaa cosa ma sono scritti in lignuaggi diversi)

Il compilatore mantiene il controllo solo nella 1a fase (passando da PL1 in input a PL0 in output) e non serve più una volta fatta la traduzione

Questo processo (mapping?) da buone prestazioni (al prog da far girare?)

Vantaggi:

- Buone prestazioni: si esegue PL0 direttamente in L=
- Ottimizzazione: durante la traduzione si puo ottimizzare del codice,

Svantaggi:

- In caso di modifica ddel codicee (tipo x debugging) è necessario ricompilare il programma modificato.

Si può fare un compilatore da L1 a L0 oppure uno che fa da L1 a Lx (meglio farlo per uno scopo o se ne si ha uno già da Lx a L0).

###### Interpretazione

Un apposito programma (interprete) esamina PL1 scritto in L1 e, istruzione per istruzione, lo traduce in L0 e lo esegue.

- Il controllo è sempre nelle mani dell'interprete (solitameente scritto in L0 e parte integrante di M1)

Vantaggi:

- Se si trova un errore si può cambiare il codice e proseguire senza ripartire da zero,

Svantaggi: 

- Prestazioni ridotte: ogni istruzione è tradotta ogni volta che è eseguita

##### Macchina virtuale M1

Il calcolatore **reale** (M0) riconosce solo comandi in L0 (realizzare una macchina M0 che comprenda L1 sarebbe troppo costoso e poco efficiente).

La compilazione o l'interpretazione permettono di realizzare una macchina virtuale M1 capace di comprendere L1.

###### Problema

- Per rendere efficiente la traduzione tra L1 e L0, la distanza tra i 1 linguaggi non può essere troppo elevato (altrimenti programmi poco efficienti),
- Non è detto che M1 sia la soluzione desiderata (potrebbe ancora essere troppo distante da un livello comprensibile da un umano).

###### Soluzione

Per questo è possibile adottare lo stesso procedimento di astrazione/virtualizzazione usato per passare da M0 a M1 anche per passare da M1 a M2 capace di comprendere un linguaggio L2.

Per tradurre un linguaggio L2:

- O lo si traduce in L1 per eseguirli con M1,
- O lo si traduce direttamente in L0 cosicché si possa eseguire il programma direttamente su M0 (+ oneroso > i livelli)

Ovviamente l'iterazione dell'astrazione delle macchine virtuali tende all'"infinito", o almeno finché non è comprensibile dall'uomo.

Per scrivere i programmi per il livello *n* non è necessario conoscere come le istruzioni vengono tradotte. Solo chi vuole capire come funziona un calcolatore o come si progetta una macchina virtuale ha necessità di conoscere come funzionano i livelli intermedi/inferiori.

### Livelli dei calcolatori

\5) Applicativo

\4) Livello del linguaggio assemblatore

\3) Livello dell'OS

\2) Livello dell'ISA (*Instruction Set Architecture*)

\1) Livello della microarchitettura

\0) Livello logico

\-1) Livello dei dispositivi

\-2) Livello fisico

##### Livello dei dispositivi

Dei dispositivi: composto da **transistor** che formano i circuiti elettronici di cui è composto un calcolatore.

Fisico: si occupa della struttura degli stessi transistor.

##### Livello logico

La macchina è formata da **porte logiche**, ognuna delle quali riceve in ingresso dei segnali binari e calcola una semplice funzione (AND, OR...)

Combinando le porte si realizzano circuiti (detti anche circuiti combinatori) che formano i calcolatori.

Certe porte, opportunamente collegate (latch), possono formare una **memoria di un bit** (memoria **bistabile**).

Combinando N memorie di un bit si può formare un **registro** capace di memorizzare un <u>numero in formato binario</u> (che potrebbe essere qualsiasi cosa, in base al n° dei bit).

##### Livello della microarchitettura

Composta da:

###### Elaborazione (data path)

Fatto da:

- Registri *general purpose* come memoria locale,
- ALU capace di eseguire semplici operazioni aritmetico-logiche,
- Elementi di connessione tra registri e ALU.

###### Controllo

Fatto da:

- Registri dedicati al controllo (PC, IR...),
- Control Unit microprogrammata o cablata.

##### Livello ISA

Insieme delle istruzioni che possono essere comprese dalla microarchitettura (la quale agisce da interprete dell'*Instruction Set*)

...

##### Livello dell'OS

Comprende molte istruzioni che si trovano già al livello ISA ed anche istruzioni aggiuntive; inoltre ha una diversa organizzazione della memoria e consente l'esecuzione di + programmi contemporaneamente).

###### Livello ibrido (?)

Le nuove funzionalità sono eseguite da un interprete detto OS, e le istruzioni identiche a quelle del livello 2 sono eseguite direttamente dalla microarchitettura.

##### Livello del linguaggio assemblatore

Qui la rappresentazione è **simbolica** (linguaggio assembler) (al contrario dei livelli precedenti in cui il linguaggio usato era il linguaggio macchina) in quanto:

- Per i programmatori i linguaggi binari dei livelli + bassi sono difficili da usare,
- A ogni istruzione del linguaggio assembler corrisponde <u>una</u> istruzione del ML.

I programmi in assembly sono tradotti in un linguaggio di livello inferiore e poi eseguiti. Il programma che li traduce è detto ***assembler*** (o assemblatore).

##### Livello applicativo

Usati linguaggi ancora di + alto livello per creare programmi applicativi (traduzione affidata a compilatori/interpreti).

> [!important] Architettura
> Insieme delle funzionalità e delle caratteristiche di un livello.

