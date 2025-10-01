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

1) esercitazione-2024-11-20 = contatore modulo 8 su 3 bit (int positivi)
2) esercitazione-2024-11-27 = contatore modulo 4 su 2 bit (CP2)
3) esercitazione-2024-11-20-esame = semaforo

##### Registri paralleli

CIRCUITO PARTE DA 0 = Reset negato (ma dove va?)

###### FSM

Innanzitutto si disegna la FSM, nella quale:

- **Stati**: contengono l'output intero e binario ed eventualmente la codifica in singolo 1 ($n$ stati $\rightarrow n$ bit con 1 bit diverso a 1 per stato),
- **Frecce**: vi si scrive vicino il valore dell'input dal quale dipende lo stato successivo.

###### Tavola di verità

Si procede con la tavola di verità, in cui si hanno generalmente 2/3 gruppi di colonne:

1) Stato iniziale in binario (o in codifica a singolo 1),
2) Variabile/input di transizione (di solito insieme al 1° gruppo),
3) Stato successivo.

Questa descrive come, in base ai bit della variabile/input di transizione, si passi da uno stato iniziale a quello successivo.

In codifica a singolo 1 si avranno $2^{n}$ bit nel 1° gruppo (+ variabile di transizione) e $n$ bit di output nel 2° gruppo (4 bit a singolo 1 = 2 bit di uscita).

###### Funzione logica

Grazie alla suddetta sarà quindi possibile ricavare la funzione logica corrispondente ad ogni **stato successivo** in base a quello iniziale e la variabile/input di transizione.

Cercare di trovare la funzione logica degli stati successivi in base a quelli precedenti e alla variabile/input di transizione; in caso sia complesso, raggruppare parte della funzione logica e ricostruire una tavola di verità con essa ed il resto delle variabili (per semplificare).

Soprattutto per funzioni complesse, potrebbe essere utile la sintesi con <u>mappe di Karnaugh</u> seguita da semplificazioni varie.

###### Circuito

Con la funzione logica per ogni bit di stato rimane solo da costruire il circuito, secondo questi step:

1) Disegnare 1 registro parallelo per ogni bit di stato (successivo o in output),
2) Costruire la funzione logica che, in base allo stato precedente, pone nei flip-flop i bit dello stato successivo tramite blocchi funzionali combinatori,
3) Collegare l'uscita di ogni flip-flop agli input dei circuiti combinatori appena creati corrispondenti,
4) (eventuale rete combinatoria di output)

##### Registri a scorrimento

###### Cose comuni

Modulo $n$, significa che il circuito ha $n$ stati totali e procedendo dall'ultimo (più grande) si ritorna a quello iniziale (più piccolo).

Ingressi in CP2 perché, generalmente, è richiesto di andare indietro con gli stati (serve un modo di rappresentazione di numeri negativi per sottrazioni).

Tavole di verità (colonne): bit di stato, numero di stato (int), bit scelta (input), bit stato successivo, numero stato successivo (int).

###### Dilemmi

Cosa mettere nella FSM (all'interno degli stati e sulle frecce)?

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

