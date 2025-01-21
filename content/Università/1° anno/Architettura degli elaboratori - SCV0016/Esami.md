# Esami

### Implementare funzione

##### CP2

F funzione che riceve in input un int n in ? bit in CP2 / codice eccesso ...

###### SoP

- Disegnare tabella
- Mappa di Karnaugh
- Sintetizzare in SoP/PoS
- Disegnare l'implementazione (circuito): 
  - 2 riga per input (una normale e una negata con NOT) 
  - Per ogni variabile della funzione logica sintetizzata tracciare riga perpendicolare alle suddette e collegarle al blocco funzionale corrispondente all'operando (in SoP, il "+" = AND, mentre in PoS il "\*" = OR), per poi connettere tutti gli output di questi ad un ultimo blocco (OR per SoP e AND per PoS).

###### PoS

### Riduzione di funzioni booleane

##### Regole di semplificazione

Per ridurre una qualsiasi funzione booleana applicare le seguenti regole:

![](https://i.imgur.com/FKwC9RH.png)

### Conversione decimale - IEEE 754

##### IEEE 754

###### Da decimale a IEEE 754

1\) Identificare MSB in base al segno ($- = 1$ e $+ = 0$),

2\) Convertire parte intera e decimale in binario puro (rispettivamente con algoritmi delle divisioni successive e delle moltiplicazioni successive),

3\) Normalizzare in forma $1,x\ldots x \;*\; 2^{n}$ per poi rimuovere l'$1$ iniziale (notazione scientifica binaria prevede mantissa tra 0 e 2 esclusi, come quella decimale ma tra 0 e 10) ottenendo così la mantissa e l'esponente della base (2),

4\) Aggiungere il bias 127 all'esponente trovato e convertire tale numero in binario,

5\) Riscrivere il numero col seguente formato: "\[MSB] \[esp + 127 binario] \[mantissa estesa con 0 fino a 23 bit totali]".

###### Da IEEE 754 a decimale

1\) Identificare il segno in base all'MSB ($- = 1$ e $+ = 0$),

2\) Convertire l'esponente (seguenti 8 bit) in binario e sottrarvi 127 ottenendolo in decimale,

3\) Nella mantissa, da sinistra a destra, sommare $2^{-n}$ per ogni posizione $n$ (partendo da 1) in cui il bit è 1 fino alla fine dei 23 bit ($1001\ldots = 2^{-1} + 2^{-4} + \ldots$),

3\) Oppure aggiungere ${} 1,$ davanti alla mantissa e spostare tale "," di `esp` posizioni a destra nella mantissa (se il numero è troppo piccolo),

4\) Riscrivere il numero col seguente formato: "\[segno]\[mantissa] \* 2^\[esp]".

### ALU

###### Analisi

Per la costruzione di un'ALU è necessario leggere e comprendere al meglio il testo dell'esercizio per capire quali funzioni andranno implementate e come; quindi:

- Capire quanti ingressi e uscite ci sono e da quanti bit sono,
- Capire quante funzioni/operazioni implementare (e di conseguenza i bit necessari a rappresentarle, tipo con 2 bit per 4 operazioni si avrà $F = F_{1}F_{0}$) più quindi il MUX finale collegato all'output.

###### Componenti

A questo punto (dopo aver eventualmente ridotto le funzioni alla loro forma più semplice) per ogni funzione (<u>singolarmente</u>) disegnarne il **blocco** (<u>coi rispettivi input</u>) col quale è possibile implementarla (anche duplicandoli).

In seguito costruire i circuiti che ritornano eventuali bit di overflow o di controllo.

###### Costruzione

A questo punto conglomerare i blocchi duplicati in singole unità e per i loro input che non "matchano" selezionarli condizionalmente (con MUX o usando $n$ cavi del totale) in base ad $F$ (o ad altre condizioni).

Facendo tutto ciò è possibile collegare gli input con le funzioni e queste con gli output.

### Circuito sequenziale sincrono

### Cache

##### Direct mapping

###### Dati iniziali

Sempre: RAM totale, lunghezza word, lunghezza blocchi...

A volte: cache size

###### Dati da calcolare

Necessari:

Non necessari: indirizzo di byte in RAM, indirizzo di word in RAM...

Length ind byte = $log_{2}($RAM size$)$,

Length ind word = length ind byte - $log_{2}($word size in bytes$)$,

##### Set-associative

# Esercizi

### 1

##### 2023-02-09

![](https://i.imgur.com/bwXhJjx.png)

##### 2024-01-09

![](https://i.imgur.com/8TBAmv3.png)

##### 2024-01-24

![](https://i.imgur.com/3SqZUcv.png)

##### 2024-02-08

![](https://i.imgur.com/YbHeZpG.png)

##### 2024-06-06

![](https://i.imgur.com/Y7JZYKR.png)

### 2

##### 2023-02-09

![](https://i.imgur.com/1NNRiNu.png)

##### 2024-01-09

![](https://i.imgur.com/biO0hHW.png)

##### 2024-01-24

![](https://i.imgur.com/aV0GU0x.png)

##### 2024-02-08

![](https://i.imgur.com/YVZxMgX.png)

##### 2024-06-06

![](https://i.imgur.com/gRg7Wyv.png)

### 3

##### 2023-02-09

![](https://i.imgur.com/QtNAz2O.png)

##### 2024-01-09

![](https://i.imgur.com/g4fVEE2.png)

##### 2024-01-24

![](https://i.imgur.com/sQrhxq8.png)

##### 2024-02-08

![](https://i.imgur.com/8GezvLU.png)

##### 2024-06-06

![](https://i.imgur.com/h8PNweo.png)

### 4

##### 2023-02-09

![](https://i.imgur.com/QuNGJNl.png)

##### 2024-01-09

![](https://i.imgur.com/lnUsLd8.png)

##### 2024-01-24

![](https://i.imgur.com/Bcvj3BJ.png)

##### 2024-02-08

![](https://i.imgur.com/Wpo421n.png)

##### 2024-06-06

![](https://i.imgur.com/DnhBG5U.png)

### 5

##### 2023-02-09

![](https://i.imgur.com/9QKr1GH.png)

##### 2024-01-09

![](https://i.imgur.com/bFcui7Q.png)

![](https://i.imgur.com/XGaKSCX.png)

##### 2024-01-24

![](https://i.imgur.com/PeQxmbl.png)

##### 2024-02-08

![](https://i.imgur.com/g6L1VPx.png)

##### 2024-06-06

![](https://i.imgur.com/kI5OylX.png)

### 6

##### 2023-02-09

##### 2024-01-09

##### 2024-01-24

##### 2024-02-08

##### 2024-06-06

![](https://i.imgur.com/O7mYquZ.png)

