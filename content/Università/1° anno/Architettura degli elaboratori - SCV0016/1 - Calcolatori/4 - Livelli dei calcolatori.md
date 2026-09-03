# Lezione 4

### Livelli dei calcolatori

I calcolatori sono progettati su una serie di livelli ognuno dei quali si basa sui precedenti, meno astratti ed aventi funzionalità diverse.

> [!important] Architettura
> Insieme delle funzionalità e delle caratteristiche di un livello.

#### Livelli

\5) Applicativo

\4) Livello del linguaggio assemblatore

\3) Livello dell'OS

\2) Livello dell'ISA (*Instruction Set Architecture*)

\1) Livello della microarchitettura

\0) Livello logico

\-1) Livello dei dispositivi

\-2) Livello fisico

##### Livelli fisici

###### Livello fisico

Si occupa della struttura dei **transistor**.

###### Livello dei dispositivi

Si occupa dei circuiti elettronici (fatti da **transistor**) che compongono un calcolatore.

##### Livello logico

La macchina è formata da **porte logiche**, ognuna delle quali riceve in ingresso dei **segnali binari** e calcola una semplice **funzione** (AND, OR...).

Combinando le porte è possibile realizzare dei **circuiti**:

- **Combinatori** (ottengono un input e danno un output ma <u>non a se stessi</u>),
- **Sequenziali** (l'<u>output di questi è riutilizzato negli stessi</u>).

  Esempio: coi ***latch***, si può formare una memoria di 1 bit o memoria bistabile, mentre combinandone N (*latch*) si forma un **registro** capace di memorizzare un <u>numero binario</u> (che potrebbe essere qualsiasi cosa, in base al n° dei bit).

##### Livello della microarchitettura

###### Elaborazione (data path)

Fatto da:

- **Registri** *general purpose* come memoria locale,
- **ALU** (*Arithmetic Logic Unit*) capace di eseguire semplici operazioni aritmetico-logiche,
- (Elementi di connessione tra registri e ALU).

###### Controllo

Fatto da:

- **Registri** dedicati al controllo (PC, IR...),
- **CU** (*Control Unit*) microprogrammata o cablata.

##### Livello ISA

Insieme delle istruzioni comprensibili dalla microarchitettura (la quale agisce da interprete dell'*Instruction Set*)

Facciamo riferimento a questo quando si descrive il **ML** (linguaggio macchina) di un calcolatore.

##### Livello dell'OS

Comprende molte istruzioni che si trovano già al livello ISA ed anche istruzioni aggiuntive; inoltre ha una diversa organizzazione della memoria e consente l'esecuzione di + programmi al contempo).

###### Livello ibrido

Vi è un **livello ibrido** tra questo e il precedente, e:

- Le istruzioni identiche a quelle del livello 2 sono eseguite direttamente dalla **microarchitettura**,
- Le nuove funzionalità/istruzioni sono eseguite da un interprete detto **OS** (sistema operativo).

##### Livello del linguaggio assemblatore

(O *linguaggio assembly*), qui la rappresentazione è **simbolica** (dato che nei livelli precedenti si usava il ML) in quanto:

- Per i programmatori, i linguaggi binari dei livelli + bassi sono troppo difficili da usare,
- A ogni istruzione dell'*assembly* corrisponde <u>una (e solo una)</u> istruzione del ML.

I programmi in *assembly* sono tradotti in un linguaggio di livello inferiore da un programma detto ***assembler*** (o assemblatore), per poi essere eseguiti.

##### Livello applicativo

Qui vengono usati linguaggi ancora di + alto livello per creare programmi applicativi (traduzione affidata a compilatori/interpreti).

---

Prossima lezione: [[5 - Numeri e notazioni]]

