# Lezione 1

### Introduzione

#### Terminologia

- **Computer**: macchina elettronica programmabile al fine di svolgere + funzioni.
- **Programmazione**: attività che consiste in organizzare istruzioni elementari direttamente comprensibili dall'esecutore in strutture complesse (programmi) al fine di svolgere compiti.
- **Informatica**: disciplina che si occupa dell'informazione e del suo trattamento in maniera automatica. Essa coinvolge:
  - Mezzi fisici (pc...)
  - Mezzi logici (algoritmi...)
- **Algoritmo**: insieme ordinato di passi eseguibili e non ambigui che definiscono un processo che termina. Un algoritmo è un oggetto *astratto*.
- **Programma**: sequenza di istruzioni elementari che un pc può capire ed eseguire. Espressione di un algoritmo in un linguaggio che l'esecutore è in grado di comprendere. Un programma è un'espressione concreta dell'algoritmo.

##### Algoritmo di Euclide

L'**algoritmo di Euclide** è usato per calcolare l'MCD tra 2 variabili $x$ e $y$. Steps:

```C#
int r;
init:
r = x % y;
if (r != 0) {
	x = y;
	y = r;
	goto init;
}
// y = MCD
```

##### Assembly

Ogni CPU ha un proprio <u>linguaggio macchina</u> ($ML$, di basso livello) con un proprio formato di istruzioni che codificano:

- Le operazioni da eseguire,
- Gli operandi su ciò tale op va eseguita (registri, locazioni di memoria, costanti...).

Il linguaggio ***assembly*** è la versione simbolica del $ML$; esso dispone di:

###### Istruzioni

<u>Istruzioni di trasferimento</u>:

```assembly
LOAD R, n
STORE R, n
```

<u>Istruzioni aritmetiche</u>:

```assembly
ADD R1, R2
MUL R1, R2
SUB R1, R2
DIV R1, R2
```

<u>Istruzioni di salto</u>:

```assembly
JUMP label
JZERO label
```

###### Portabilità assembly

Ogni processore ha il proprio linguaggio *assembler*; perciò, passare un programma assembler da una CPU ad un'altra diversa, è impossibile.

Al contrario, i <u>linguaggi di alto livello</u> mirano proprio a <u>rendere la programmazione indipendente dalle</u> caratteristiche peculiari della <u>macchina</u> usata.

I linguaggi hanno una **semantica** ed una **semantica operazionale** per essere correttamente "capiti" dalle macchine. Le macchine reali $M$ su cui viene eseguito il codice al più basso livello implementano macchine astratte ($VM$) le quali "capiscono" programmi scritti in linguaggi di più alto livello grazie a degli appositi <u>traduttori</u>.

##### Compilatori e interpreti

Tali traduttori possono essere di 2 tipi:

- **Compilatori**: programma che traduce un intero programma del linguaggio $L_{vm}$ in un programma equivalente nel linguaggio macchina $ML$ di $M$,
- **Interpreti**: programma che 1) legge un'istruzione nel linguaggio $L_{vm}$, 2) la traduce in linguaggio macchina ($ML$) per poi eseguirla e 3) passa alla successiva

###### Vantaggi

**Portabilità del sorgente**: a patto che sulle varie macchine sia presente un compilatore o interprete adatto, è possibile eseguirlo su ognuna di queste.

![](https://i.imgur.com/8pfdtU9.png)

##### Workflow

![](https://i.imgur.com/5n2Wxff.png)

Qui sono introdotti altri elementi:

- ***Linker***: permette di "agganciare" le librerie al programma (permette al programma di referenziare correttamente funzionalità importate dalle librerie esterne),
- **Esecutore**: è ciò che permette di eseguire il programma in un certo OS.
- **Errori**: scaturiti da varie problematiche, di diversi tipi:

###### Errori

- <u>Di compilazione</u>: (tipo dimentichi un ";" a fine riga), l'IDE te lo evidenzia,
- <u>Del linker</u>: (dipendenze di librerie),
- <u>Di esecuzione</u>: (crash durante l'esecuzione, tipo per divisione di un numero per 0).

#### Programmazione strutturata

Introdotta negli anni '70, in questa l'esecutore è guidato alla sequenza di esecuzione opportuna tra tutte quelle possibili, mediante <u>strutture di controllo</u> fondamentali:

- **Sequenza**: permette di <u>eseguire le istruzioni nell'ordine in cui sono scritte</u>,
- **Selezione**: permette di <u>eseguire</u> una o un'altra parte di <u>codice in base a delle condizioni</u>,
- **Iterazione**: permette di <u>ripetere l'esecuzione di certe istruzioni in base a delle condizioni</u>.

L'impiego di queste strutture:

- Migliora la leggibilità dei programmi,
- Da un solo *entry point* (punto d'ingresso) e un solo *exit point* (punto d'uscita),
- Il flusso di esecuzione è evidente dalla struttura del codice.

Per questo, tutti i programmi esprimibili tramite espressioni di salto (`goto`) o *flow-chart* (diagrammi di flusso).

##### Java

Java è un linguaggio di programmazione ad alto livello. I suoi file hanno estensione `.java` e, per essere usati, devono essere prima compilati e poi eseguiti:

1) I file `.java` si compilano con il comando "`javac file.java`", il che genera un file "`file.class`", ovvero un file in un linguaggio intermedio detto ***bytecode***,
2) Per eseguire il ***bytecode*** basta eseguire il comando "`java file`" con solo il nome della <u>classe</u> da eseguire (interna al file, tipo un file `file` avente la classe principale chiamata `Class` non funzionerà se fatto "`java file`" bensì bisognerà usare "`java Class`", per questo è meglio chiamare i file con lo stesso nome della loro classe).

###### JVM

La **JVM** (*Java Virtual Machine*) è ciò che permette di eseguire il codice java sulle macchine:

![](https://i.imgur.com/ldKrqpo.png)

###### Package

I ***package*** permettono di raggruppare logicamente classi e interfacce in unità di compilazione, ovvero file con codice sorgente Java.

Ogni file può contenere al massimo 1 classe o interfaccia `public`, la quale determina il nome del file.

Con l'istruzione `package ...` all'inizio del file java si specifica che esso appartiene a un certo package. Tuttavia, supponendo di scrivere `package pack`, il file dovrà essere in una cartella di nome "pack" nel progetto, dovrà essere compilata con `javac pack/Class.java` ed eseguita con `java pack.Class`; il tutto con la root del progetto nel *classpath*. 

###### Import

Si possono importare dei ***namespace*** con l'istruzione `import ...`, per esempio `import prog.io.*` importa tutte le classi e interfacce presenti nel package "prog/io".

# Esercizi

# Soluzioni

---

Prossima lezione: [[2 - Variabili e lessico]]

