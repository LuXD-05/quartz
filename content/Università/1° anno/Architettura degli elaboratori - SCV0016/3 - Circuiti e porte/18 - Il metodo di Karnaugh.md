# Lezione 18

### Ottimizzazione e mintermini

Si considerino 2 ***mintermini*** di una [[16 - SoP e PoS#SoP|SoP]], cioè 2 addendi che condividono tutte le variabili tranne 1. Tali mintermini (<u>in generale</u>: $XY + X\lnot{Y}$) si dicono **adiacenti** e possono essere ridotti alle sole variabili condivise.

##### Mintermini

Tipo in una funzione con $k = 4$:

- <u>2 mintermini</u> che <u>non condividono 1 variabile</u> diventano un solo mintermine a <u>3 variabili</u> (prima condivise),
- <u>4 mintermini</u> che <u>non condividono 2 variabili</u> diventano un solo mintermine a <u>2 variabili</u> (prima condivise),
- <u>8 mintermini</u> che <u>non condividono 3 variabili</u> diventano un solo mintermine a <u>1 variabile</u> (prima condivisa),

> [!info] In generale
> In una funzione booleana a $k$ variabili, quando $2^{n}$ mintermini condividono tutte le variabili **eccetto** $n$:
> 1) Si <u>riscrivono le variabili condivise</u> (di numero: $k-n$),
> 2) Il <u>resto</u> diventa una costante e <u>scompare</u>,
> 3) Rimane solo 1 mintermine con le $k-n$ variabili condivise.

###### Esempio

\1) 2 mintermini condividono tutte le variabili tranne 1 (B):

$AB\lnot{C} + A\lnot{B}\lnot{C}$

Ottimizzando si avrebbe:

$A\lnot{C}$

\2) 4 mintermini condividono tutte le variabili tranne 2 (A e C):

$A\lnot{B}C + A\lnot{B}\lnot{C} + \lnot{A}\lnot{B}C + \lnot{A}\lnot{B}\lnot{C}$

Ottimizzando si avrebbe:

$\lnot{B}(AC + A\lnot{C} + \lnot{A}C + \lnot{A}\lnot{C}) =$

![](https://i.imgur.com/zvtKLnn.png)

$\lnot{B}$

##### Limiti del metodo

Il metodo di Karnaugh è generalmente migliore della semplice derivazione dell'espressione logica in 1a forma normale, ma esso presenta un evidente svantaggio: l'esclusione di alcune ottimizzazioni logiche.

Per esempio: con Karnaugh si può dedurre che $F = AB + BC$, il che richiede 3 porte. Tuttavia, semplificando $F$ ulteriormente a $B(A+C)$, diventano necessarie solo 2 porte.

### Mappe di Karnaugh

Si predispongono le righe della tavola di verità in modo che l'*adiacenza logica* corrisponda all'*adiacenza fisica*, così da <u>facilitare la ricerca di gruppi di mintermini</u> (che condividono tutte le variabili tranne $n$); la tabella risultante è detta **mappa di Karnaugh** (o *k-map*).

Nelle mappe di Karnaugh si raggruppano mintermini adiacenti tramite, per l'appunto, dei "***gruppi***" che racchiudono i mintermini all'interno di essi (esempio poi).

> [!info] Regole
> 1) Si possono raggruppare $2^{x}$ mintermini per volta in gruppi con <u>forme precise</u>, le quali devono prevedere $2^{n}$ mintermini in <u>orizzontale</u> e $2^{m}$ mintermini in <u>verticale</u> (quadrati/rettangoli tipo: 1x1, 1x2, 1x4... 2x2, 2x4... 4x8...),
> 2) I gruppi possono **sovrapporsi**,
> 3) I gruppi sono adiacenti anche **da una parte all'altra della mappa** e in qualsiasi **direzione**,
> ![](https://i.imgur.com/iJ1PDxx.png)
> Va ricordato che <u>più i gruppi sono grandi</u> e <u>più variabili non condivise verranno eliminate</u> (meglio, così si semplifica ancora di più l'espressione risultante).

##### Procedimento

###### Dalla tavola di verità alla k-map

Per passare da una **tavola di verità** ad una ***k-map*** in pratica bisogna:

1) Disegnare la *k-map* in base al <u>n° di variabili in input</u> ($n$, quindi il n° di celle sarà $2^{n}$) sempre in forma quadrata/rettangolare, (con `00 01 11 10` nelle colonne (vedi [[#Inversione righe/colonne 3 e 4|qui]])),
2) Scrivere **1** nella *k-map* nelle celle che corrispondono alle combinazioni che nella tavola di verità danno **1** in output (e nel caso scrivere $0$ nel resto delle celle),
3) **Raggruppare** secondo le regole suddette.

![](https://i.imgur.com/WSLLvrK.png)

![](https://i.imgur.com/ZHGvwhp.png)

###### Risolvere una k-map

Per risolvere una *k-map*, per ogni gruppo:

1) Considerare i **valori di colonna** che <u>non cambiano</u> comuni agli elementi del gruppo,
2) Se essi sono a **1**, si trascriverà la variabile <u>positiva</u> come fattore dell'addendo della risultante SoP; altrimenti, se essi sono a **0**, riportare sempre come fattore di tale addendo la stessa variabile però <u>negata</u>,
3) Collegare tutti gli addendi con dei "**+**" (OR) per ottenere la funzione logica risultante.

Dall'esempio di prima si ottiene quindi:

![](https://i.imgur.com/QhsH64G.png)

##### K-maps su tavole di verità

Un 1° metodo per trovare mintermini adiacenti consiste nell'usare una normale tavola di verità in questo modo (esempio con 2 variabili di input):

![](https://i.imgur.com/gmkuoc5.png)

Qui sono mostrate tutte le possibili combinazioni di mintermini e si vede come l'adiacenza vi sia seppur nell'ultimo caso le 2 celle non lo sembrino.

##### K-maps a 2 variabili

Le k-maps a 2 variabili sono rappresentate nei seguenti modi e le combinazioni possibili sono varie ...

![](https://i.imgur.com/4u4X2q7.png)

##### K-maps a 3 variabili

Le k-maps a 3 variabili invece si rappresentano così (o in verticale, in base a come si decide di disporre le variabili e quante disporne per righe e colonne).

![](https://i.imgur.com/P7tZJhp.png)

##### K-maps a 4 variabili

![](https://i.imgur.com/r17lAqd.png)

![](https://i.imgur.com/gBoZmOm.png)

###### Inversione righe/colonne 3 e 4

> [!error] Attenzione
> Si nota come i valori binari delle <u>righe/colonne 3 e 4</u> siano **invertiti** rispetto ad una normale tavola di verità. Questo è fatto per fare in modo che i valori siano in qualche modo ***contigui*** nella *k-map* (questo `00 01 11 10` invece che `00 01 10 11`) e ciò è fondamentale affinché la *k-map* sia corretta.
> ![](https://i.imgur.com/Ay6wBv1.png)

##### K-maps a 5 variabili o più

Le mappe di Karnaugh aventi + di 4 variabili sono più complesse da rappresentare e per farlo ci sono 2 modi:

###### Metodo classico

Con il metodo classico, si disegnano $2^{n-4}$ *k-maps* (supponendo che 4 sia il numero di variabili di una *k-map* base) **congiunte** in un <u>certo modo</u>.

Tipo, per le mappe a 5 variabili, si fanno 2 k-maps a 4 variabili dove:

- Nella 1a (per tutte le celle) bisognerà tenere conto della 5a variabile ponendola a 0,
- Stessa cosa nella 2a (per tutte le celle) solo che la 5a variabile sarà posta a 1.

![](https://i.imgur.com/ZM2QIVp.png)

Per **congiungerle**, bisogna <u>speculare la 2a</u> ed <u>appendere</u> (prima dei valori tipo di AB o CD) i <u>valori della 5a variabile</u> alle colonne (o righe) di ogni tabella rispettivamente (4 zeri alla 1a e 4 uni alla 2a).

(In questo caso la 5a variabile è $A$, riquadrata in rosso, mentre in verde sono sottolineati i valori di $BC$ normali nella k-map a sinistra e specchiati nella k-map a destra):

![](https://i.imgur.com/1D18OOa.png)

Per le mappe a 6 variabili invece bisognerà fare 4 mappe per ogni combinazione binaria delle variabili 5 e 6 (`/E/F /EF EF E/F = 00 01 11 10`):

![](https://i.imgur.com/Ur4HIg3.png)

La corrispondente congiunta a 6 variabili sarà così:

![](https://i.imgur.com/3BpM2Uu.png)

###### Metodo 3D

Per meglio visualizzare le k-maps a più di 4 variabili, è possibile rappresentarle (senza specchiarle o altro) come una **matrice in 3D** composta da $2^n-4$ "piani":

![](https://i.imgur.com/jQOymB1.png)

![](https://i.imgur.com/01UhwGw.png)

#### K-maps in PoS

Stessa identica cosa solo che:

1) Si **scrivono e raggruppano 0** al posto di 1,
2) Ogni gruppo si traduce in un <u>fattore di somme</u> per formare un **PoS**.

![](https://i.imgur.com/cZGPnFw.png)

![](https://i.imgur.com/hVpeYeb.png)

### Condizioni di indifferenza

Esistono dei casi in cui non si sa il valore che una variabile assume per certe combinazioni, ovvero quando:

- Tali combinazioni non si presentano in input,
- Non importa che valore sia stabilito per l'output di quella combinazione.

In quel caso, sono detti condizioni di indifferenza i mintermini/maxtermini non specificati di una funzione; e, al posto di rappresentarli con 1 o 0, sono rappresentati con una $X$.

###### Esempio

$F = BC + A$

![](https://i.imgur.com/LyjLkC9.png)

# Esercizi

# Soluzioni

---

Prossima lezione: [[19 - Blocchi funzionali combinatori]]

