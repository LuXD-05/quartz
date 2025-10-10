# Lezione 21

### Matrici

Una **matrice** $n \times m$ è una "*tabella*" (un vettore di vettori tutti della stessa lunghezza) avente $n$ <u>righe</u> e $m$ <u>colonne</u> e contenente valori reali.

##### Rappresentazione

Una matrice con $i$ righe e $j$ colonne è rappresentata così:

$$m =

\begin{bmatrix}

    x_{11} & x_{12} & x_{13} & \dots  & x_{1j} \\

    x_{21} & x_{22} & x_{23} & \dots  & x_{2j} \\

    \vdots & \vdots & \vdots & \ddots & \vdots \\

    x_{i1} & x_{i2} & x_{i3} & \dots  & x_{ij}

\end{bmatrix}$$

###### Indici

Per riferirsi ad un **elemento** della matrice ad una certa <u>riga/colonna</u> si usa la seguente forma: $\;\;\;m_{ij}\;\;\;$, dove:

- $m$: <u>matrice</u>,
- $i$: <u>indice di riga</u> (parte da 1),
- $j$: <u>indice di colonna</u> (parte da 1).

###### Dimensione

Intuibilmente, la **dimensione** di una matrice è rappresentata dal <u>prodotto tra il suo numero di righe</u> $n$ <u>ed il suo numero di colonne</u> $m$.

> [!error] Attenzione
> La <u>dimensione di una matrice</u> è sempre espressa "**righe** $\times$ **colonne**" (e non "colonne $\times$ righe" o nemmeno col numero equivalente al prodotto tra esse).

###### Trasposta

Data una qualsiasi matrice $A \in M_{n,m}$, la sua **trasposta** è una matrice $A^{T} \in M_{m,n}$ ottenuta <u>scambiando le righe con le colonne</u>; quindi se $A = (a_{ij}) \rightarrow A^{T} = (a_{ji})$:

$$A = \begin{pmatrix} x_{11} & x_{12} & x_{13} \\ x_{21} & x_{22} & x_{23} \\ \end{pmatrix} \in M_{2,3} \;\;\;\rightarrow\;\;\; A^{T} = \begin{pmatrix} x_{11} & x_{21} \\ x_{12} & x_{22} \\ x_{13} & x_{23} \\ \end{pmatrix} \in M_{3,2}$$

##### Tipi di matrice

###### Principali

- **Matrice riga**: è una matrice con <u>1 sola riga</u> e <u>n colonne</u> (= a un **vettore**):

  ![](https://i.imgur.com/gls9pMX.png),

- **Matrice colonna**: ha <u>n righe</u> e <u>1 sola colonna</u> (detta anche *vettore colonna*):

  ![](https://i.imgur.com/vQKMEIH.png),

- **Matrice rettangolare**: ha <u>n righe</u> e <u>m colonne</u> (quindi in numero <u>diverso</u>):

  ![](https://i.imgur.com/XyDZy4w.png).

###### Matrice nulla

Una matrice nulla è una matrice rettangolare $n \times m$ i cui valori sono tutti = 0:

$$A = \begin{pmatrix} 0 & 0 & 0 \\ 0 & 0 & 0 \\ \end{pmatrix}$$

###### Matrice quadrata

Una **matrice quadrata** ha <u>lo stesso numero</u> $n$ <u>di righe e colonne</u>:

  ![](https://i.imgur.com/tEuUcBE.png)

> [!important] Ordine
> Quando si ha a che fare con matrici quadrate, invece di dire che tali hanno dimensione $n \times n$, si dice che sono di **ordine *n***.

###### Matrice diagonale

###### Matrice identità

La **matrice identità** è una qualsiasi matrice quadrata di ordine $n$ tale che ...

###### Matrice simmetrica

###### Matrice triangolare

Data una matrice quadrata $A$, essa è **triangolare** se tutti gli elementi in cui $i > j$ sono = 0, per esempio:

$$A =

\begin{bmatrix}

    a_{11} & a_{12} & a_{13} & a_{14} \\

    0 & a_{22} & a_{23} & a_{24} \\
    0 & 0 & a_{33} & a_{34} \\
    0 & 0 & 0 & a_{44}
\end{bmatrix}$$

> [!important] Proprietà
> Se $A$ è una matrice **triangolare**, allora:
> $$det(A) = \prod\limits^{n}_{i=1} a_{ii}$$

###### Matrice a scala

Innanzitutto, si dice ***pivot*** di una riga $i$ (di una matrice) il 1° elemento $p_{ij} \neq 0$ della riga.

Una matrice, invece, si dice ***a scala*** se, <u>per ogni sua riga</u> $i > 1$, il ***pivot*** $p_{ij}$ è **più a destra** del ***pivot*** della riga precedente ($j_{i} > j_{i-1}$), per esempio (*pivot* in rosso):

$$A =

\begin{bmatrix}

    {\color{red}{1}} & 2 & 0 & 3 \\

    0 & 0 & {\color{red}{1}} & 2 \\
    0 & 0 & 0 & {\color{red}{3}}
\end{bmatrix}$$

> [!info] Rank
> Il [[24 - Rank|rank]] di una matrice a scala è sempre il suo <u>n° di righe</u> **non nulle**.

##### Insiemi delle matrici

Le stesse matrici appartengono a degli insiemi i quali si basano sulle loro [[#Dimensione|dimensioni]]: 

> [!example] Insiemi
> | Matrice      | Insieme                   |
> | ------------ | ------------------------- |
> | Riga         | $M_{1,m}$                 |
> | Colonna      | $M_{n,1}$                 |
> | Rettangolare | $M_{n,m}$                 |
> | Quadrata     | $M_{n}$ (${} M_{n,n}$) |

##### Matrici con parametri

C'è la possibilità che delle matrici abbiano dei parametri al posto di alcuni valori e magari negli esercizi viene richiesto di studiare le proprietà delle matrici al variare di tali valori. Tipo:

$$A = \begin{bmatrix} 1 & k \\ 0 & k \\ 1 & 0 \end{bmatrix}$$

Qui con $k = 0$, la matrice ha rango 1, mentre con $k > 0$, la matrice ha rango 2.

# Esercizi

ES: calcolo rango in base a k

$$A = \begin{bmatrix} 1 & k & 0 \\ 1 & 1 & 0 \\ 0 & 1 & 1 \end{bmatrix}$$

# Soluzioni

---

Prossima lezione: [[22 - Operazioni tra matrici]]

