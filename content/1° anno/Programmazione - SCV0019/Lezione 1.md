---
modified_at: 24/09/2024 10:52:01
edited_seconds: 2340
public: true
---
### Terminologia
> [!important] Computer
> Macchina elettronica programmabile al fine di svolgere + funzioni.

> [!important] Programmazione
> Attività che consiste in organizzare istruzioni elementari direttamente comprensibili dall'esecutore in strutture complesse (programmi) al fine di svolgere compiti.

> [!important] Informatica
> Disciplina che si occupa dell'informazione e del suo trattamento in maniera automatica.
> L'informatica coinvolge: 
> - Mezzi fisici (pc...)
> - Mezzi logici (algoritmi...)

> [!important] Algoritmo
> Insieme ordinato di passi eseguibili e non ambigui che definiscono un processo che termina.
> Un algoritmo è un oggetto *astratto*.

> [!important] Programma
> Sequenza di istruzioni elementari che un pc può capire ed eseguire.
> Espressione di un algoritmo in un linguaggio che l'esecutore è in grado di comprendere.
> Un programma è un'espressione concreta dell'algoritmo.

##### Algoritmo di Euclide
L'algoritmo di Euclide è usato per calcolare l'MCD tra 2 variabili $x$ e $y$. Steps:
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

Ogni CPU ha un proprio linguaggio macchina con un proprio formato di istruzioni.
Istruzioni: sequenze di bit che codificano:
- Le operazioni da eseguire,
- Gli operandi su ciò tale op va eseguita (registri, locazioni di memoria, costanti...)
Il linguaggio ***assembler*** è la versione simbolica del linguaggio macchina.

##### Assembly
L'assembler è un linguaggio di basso livello.
Istruzioni di trasferimento:
```assembly
LOAD R, n
STORE R, n
```
Istruzioni aritmetiche:
```assembly
ADD R1, R2
MUL R1, R2
SUB R1, R2
DIV R1, R2
```
Istruzioni di salto:
```assembly
JUMP label
JZERO label
```
Ogni processore ha il suo proprio linguaggio assembler, quindi passare un programma assembler da una CPU ad un'altra diversa è impossibile (al contrario che con i linguaggi di alto livello).
Obiettivo dei linguaggi di alto livello è infatti rendere la programmazione indipendente dalle caratteristiche peculiari della macchina usata.
I linguaggi hanno una semantica ed una semantica operazionale.
##### Compilatori e interpreti
La macchina astratta (VM) è implementata sulla macchina reale M da un'opportuno strumento di traduzione.

> [!important] Compilatore
> Programma che traduce un programma del linguaggio L in un programma equivalente nel linguaggio macchina di M.

> [!important] Interprete
> Programma che simula direttamente la VM:
> - Legge un'istruzione nel linguaggio L,
> - La traduce in linguaggio macchina (ML) e la esegue,
> - Passa all'istruzione successiva.
###### Vantaggi
Portabilità del sorgente: a patto che sulle varie macchine sia presente un compilatore/interprete adatto, è possibile eseguirlo su ognuna di queste.
##### Workflow
1) Scrivo il sorgente,
2) Compilatore trasforma il codice in un linguaggio intermedio (se non trova errori)
3) Il linker aggancia le librerie al linguaggio intermedio (salvo errori)
4) Viene prodotto l'eseguibile (eseguibile salvo errori).
###### Errori
Ci sono vari tipi di errori:
- Di compilazione: (tipo dimentichi un ";" a fine riga), l'IDE te lo evidenzia,
- Del linker: (dipendenze di librerie),
- Di esecuzione: (crash durante l'esecuzione, tipo  per divisione di un numero per 0).
### JVM
La JVM (Java Virtual Machine):
1) Tramite il compilatore (comando `javac`) compila il linguaggio in un altro detto bytecode,
2) Il bytecode viene interpretato (comando `java`) ed eseguito sulla macchina.

### ?
##### Programmazione strutturata
Introdotta negli anni '70, in questa l'esecutore è guidato alla sequenza di esecuzione opportuna tra tutte quelle possibili, mediante strutture di controllo fondamentali:
- Sequenza: permette di eseguire le istruzioni nell'ordine in cui sono scritte,
- Selezione: permette di eseguire una o un0altra parte di codice in base a delle condizioni
- Iterazione: 
L'impiego di queste strutture:
- Migliora la leggibilità dei programmi,
- Da un solo *entry point* e un solo *exit point*,
- Il flusso di esecuzione è evidente dalla struttura del codice.
Completezza
Tutti i programmi esprimibili tramite le espressioni 

### Variabili
> [!important] Variabile
> Contenitore preposto a contenere valori. Per dare un valore a una variabile si usa un'operazione detta di "assegnamento".
> Di solito si assegna con: `variabile = valore`.
> Il valore da assegnare potrebbe anche essere un'espressione da valutare, tipo: `var = x + y`.

Variabile è semplicemente un0astrazione del concetto di locazione di memoria.
Assegnamento è invece un'astrazione dell'operazione di STORE.

> [!important] Tipo
> Il tipo di una variabile specifica determina:
> - L'insieme dei valori che in essa possono essere memorizzati,
> - L'insieme delle operazioni che è possibile effettuare con essa.

Tutte le variabili sono rappresentate in memoria come sequenze di bit, interpretate diversamente in base al tipo della variabile:
- 01000001 in 'char' = 'A'
- 01000001 in 'int' = '65'

Molti linguaggi richiedono la **dichiarazione** delle variabili prima del loro uso.









# Altro
Domanda esame: operazioni controllate e non controllate