# Lezione 23

### Determinante

Ad ogni [[21 - Matrici#Matrice quadrata|matrice quadrata]] corrisponde un numero reale detto **determinante**.

##### Proprietà

1) $det([n]) = n$
2) $det(I_{n}) = 1$ (matrice identica)
3) Se $A$ ha 1 riga o 1 colonna con tutti $0$, $det(A) = 0$
4) Se $A$ ha 2 righe o 2 colonne uguali, $det(A) = 0$
5) Se scambiando 2 righe o 2 colonne di $A$ si ottiene $B$, allora $det(B) = -det(A)$
6) Se moltiplicando tutti gli elementi di una riga di $A$ per $k$, allora $det(B) = k \cdot det(A)$,
7) Se sommando 2 righe di $A$ tra loro si ottiene $B$, allora $det(B) = det(A)$
8) Se una riga/colonna è una combinazione lineare delle altre, $det(A) = 0$

#### Calcolo

Aldilà delle proprietà appena definite, è possibile calcolare il determinante in altri modi in base all'ordine della matrice che si ha di fronte:

##### Determinante di matrici di ordine 2

Per calcolare il **determinante** di matrici quadrate di **ordine 2**, basta semplicemente <u>moltiplicare i valori delle diagonali</u> e <u>sottrarre i risultati</u> come nell'esempio:

$$det\begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22}\end{bmatrix} = (a_{11} \cdot a_{22}) - (a_{12} \cdot a_{21})$$

##### Metodo di Sarrus

Il metodo di Sarrus è applicabile solo a <u>matrici quadrate di ordine 3</u> ed è molto semplice. 

###### Procedimento Sarrus

Partiamo dalla seguente matrice di esempio:

$$A = \begin{bmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{bmatrix}$$

Innanzitutto basta bisogna ricopiare la 1a e la seconda colonna a destra di questa matrice, rendendola una $3 \times 5$:

$$\begin{bmatrix} a_{11} & a_{12} & a_{13} & a_{11} & a_{12} \\ a_{21} & a_{22} & a_{23} & a_{21} & a_{22} \\ a_{31} & a_{32} & a_{33} & a_{31} & a_{32} \end{bmatrix}$$

Ora tracciamo delle righe lungo delle diagonali:

![](https://i.imgur.com/SBj73VW.jpeg)

Per ogni **diagonale verde**, <u>moltiplicarne i valori e sommarne i risultati</u>; poi fare la stessa cosa per ogni **antidiagonale rossa**. Infine <u>sottrarre alla somma delle diagonali verdi la somma delle antidiagonali rosse</u>; quello sarà il **determinante**:

$$det(A) = (a_{11} \cdot a_{22} \cdot a_{33}) + (a_{12} \cdot a_{23} \cdot a_{31}) + (a_{13} \cdot a_{21} \cdot a_{32}) - (a_{11} \cdot a_{23} \cdot a_{32}) - (a_{12} \cdot a_{21} \cdot a_{33}) - (a_{13} \cdot a_{22} \cdot a_{31})$$

##### Metodo di Laplace

Il metodo descritto dal teorema di Laplace permette di calcolare il determinante di una matrice di <u>qualsiasi ordine</u> tramite formule ricorsive dette *sviluppi di Laplace*.

###### Complemento algebrico

Prima è necessario conoscere il seguente concetto: dato un qualsiasi elemento $a_{ij} \in A$, si dice **complemento algebrico** (o **cofattore**) dello stesso il numero dato da:

$$cof(a_{ij}) = (-1)^{i+j} \cdot det(A_{ij})$$

Attenzione: $(-1)^{i+j}$, serve semplicemente per associare ad ogni (determinante di ogni) elemento della matrice un segno, che è:

- "$+$" se la somma tra $i$ e $j$ è **pari**,
- "$-$" se la somma tra $i$ e $j$ è **dispari**.

$A_{ij}$ invece è una sottomatrice di $A$ che è stata creata rimuovendo da $A$ una riga ed una colonna scelta.

> [!info] Pro tip
> La configurazione dei segni di qualsiasi matrice prevede un'alternarsi dei 2 segni (partendo dal "$+$") da sinistra a destra e dall'alto verso il basso:
> $$\begin{bmatrix} \overset{\color{lightgreen}{+}}{a_{11}} & \overset{\color{red}{-}}{a_{12}} & \overset{\color{lightgreen}{+}}{a_{13}} \\ \overset{\color{red}{-}}{a_{21}} & \overset{\color{lightgreen}{+}}{a_{22}} & \overset{\color{red}{-}}{a_{23}} \\ \overset{\color{lightgreen}{+}}{a_{31}} & \overset{\color{red}{-}}{a_{32}} & \overset{\color{lightgreen}{+}}{a_{33}} \end{bmatrix}$$

###### Procedimento Laplace

La formula generale è:

$$det(A) = \sum\limits^{n}_{i \textfractionsolidus j=1} a_{ij} \cdot cof(a_{ij})$$

Partiamo dalla seguente matrice di esempio:

$$A = \begin{bmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{bmatrix}$$

È sufficiente fare il procedimento scegliendo **1 riga o 1 colonna** di $A$ (siccome il <u>risultato è uguale qualunque si scelga</u>).

Il vettore scelto bisognerà "*scorrerlo*" e calcolarne, per ogni elemento $a_{ij}$, il [[#Complemento algebrico|cofattore]]:

$$cof(a_{ij}) = (-1)^{i+j} \cdot det(A_{ij})$$

Per $(-1)^{i+j}$ basta guardare la <u>matrice dei segni</u> descritta precedentemente e si ottiene il segno; mentre, per il $det(A_{ij})$ bisogna:

- <u>Cancellare dalla matrice iniziale</u>, oltre alla riga/colonna scelta in precedenza, la <u>colonna/riga corrispondente all'elemento in esame</u> $a_{ij}$,
- Ne risulterà la **sottomatrice** $A_{ij}$; lì, se $det(A_{ij})$ non è calcolabile direttamente ($M_{2}$) o con [[#Metodo di Sarrus|Sarrus]] ($M_{3}$), <u>ripetere il passo precedente</u> scegliendo nuovamente una riga o una colonna di $A_{ij}$.

Avendo quindi fatto ciò per ogni elemento della riga/colonna scelta, oltre ai segni (da $(-1)^{i+j}$) si otterranno le corrispondenti sottomatrici (organizzabili anche in un vettore).

Rimane quindi solo da <u>moltiplicare</u> (per ogni elemento della riga/colonna scelta): il **valore** ($a_{ij}$) **corrente** per il relativo **segno** ($(-1)^{i+j}$) per la relativa **sottomatrice** $A_{ij}$.

Sommando i valori ottenuti per ogni elemento si otterrà il **determinante della matrice**.

###### Esempio Laplace

Sempre considerando la suddetta matrice di esempio, scegliamo la prima riga della stessa per calcolare il determinante con Laplace.

Valori: $[a_{11}, a_{12}, a_{13}]$,

Segni: $[ {\color{lightgreen}{+}}, {\color{red}{-}}, {\color{lightgreen}{+}} ]$,

Sottomatrici: $\displaystyle \left[ \begin{bmatrix} a_{22} & a_{23} \\ a_{32} & a_{33} \end{bmatrix}, \begin{bmatrix} a_{21} & a_{23} \\ a_{31} & a_{33} \end{bmatrix}, \begin{bmatrix} a_{21} & a_{22} \\ a_{31} & a_{32} \end{bmatrix} \right]$

cofattori: $\displaystyle \left[ {\color{lightgreen}{+}} a_{11} \cdot det\begin{pmatrix} a_{22} & a_{23} \\ a_{32} & a_{33} \end{pmatrix} \, {\color{red}{-}} a_{12} \cdot det\begin{pmatrix} a_{21} & a_{23} \\ a_{31} & a_{33} \end{pmatrix} \, {\color{lightgreen}{+}} a_{13} \cdot det\begin{pmatrix} a_{21} & a_{22} \\ a_{31} & a_{32} \end{pmatrix} \right] = det(A)$

# Esercizi

###### ?) Determinante con Sarrus

Calcolare il determinante della seguente matrice quadrata di ordine 3:

$$A = \begin{bmatrix} 2 & -1 & 4 \\ 1 & 2 & 0 \\ 3 & 5 & 4 \end{bmatrix}$$

# Soluzioni

---

Prossima lezione: [[24 - Rank]]

