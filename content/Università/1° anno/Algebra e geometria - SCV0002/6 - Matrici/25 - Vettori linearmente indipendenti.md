# Lezione 25

### Vettori

Un vettore è un'insieme di numeri reali che può essere anche rappresentato da un punto di vista geometrico. In pratica è una matrice con una riga singola di $n$ elementi (vedi [[21 - Matrici#Principali|matrice riga]]): $M_{1,n}$, indicata anche con $\mathbb{R}^{n}$ (quindi $n$ = lunghezza vettori di $\mathbb{R}$).

> [!important] Vettore nullo
> Il vettore nullo è un vettore le cui componenti sono tutte $= 0$.

##### Operazioni

> [!error] Attenzione
> Se i vettori $\in \mathbb{R}^{n}$, gli scalari (numeri) appartengono a $\mathbb{R}$.

###### Somma (e sottrazione)

L'operazione di **somma** (e **sottrazione**) è possibile solo tra <u>2 vettori aventi entrambi lo stesso numero di elementi</u>; e consiste nel <u>sommarne i valori agli indici uguali</u>, così da ottenere un **vettore di somme** lungo quanto i precedenti.

> [!info] Struttura algebrica somma
> Dati $x, y \in \mathbb{R}^{n}$, con:
> - ${} x = [x_{1}, x_{2}, \ldots x_{n}] {}$
> - ${} y = [y_{1}, y_{2}, \ldots y_{n}] {}$
> Si definisce la seguente struttura algebrica:
> $$+ : \mathbb{R}^{n} \times \mathbb{R}^{n} \rightarrow \mathbb{R}^{2}$$
> Tale che:
> $$x + y = [x_{1} + y_{1}, \; x_{2} + y_{2}, \; ... \; x_{n} + y_{n}]$$

###### Prodotto esterno

L'operazione di **prodotto esterno** è possibile solo tra <u>2 vettori aventi entrambi lo stesso numero di elementi</u>; e consiste nel <u>moltiplicarne i valori agli indici uguali</u>, così da ottenere un **vettore di prodotti** lungo quanto i precedenti.

> [!info] Struttura algebrica prodotto
> Dati $x, y \in \mathbb{R}^{n}$, con:
> - ${} x = [x_{1}, x_{2}, \ldots x_{n}] {}$
> - ${} y = [y_{1}, y_{2}, \ldots y_{n}] {}$
> Si definisce la seguente struttura algebrica:
> $$\cdot : \mathbb{R}^{n} \times \mathbb{R}^{n} \rightarrow \mathbb{R}^{2}$$
> Tale che:
> $$x \cdot y = [x_{1} \cdot y_{1}, \; x_{2} \cdot y_{2}, \; ... \; x_{n} \cdot y_{n}]$$

### Combinazione lineare

Dati:

- Dei **vettori** $\in \mathbb{R}^{n}$: $v_{1}, v_{2}, \ldots v_{n}$,
- Degli **scalari** $\in \mathbb{R}$: $x_{1}, x_{2}, \ldots x_{n}$,

Si definisce **combinazione lineare** di tali vettori una qualsiasi espressione tipo:

$$x_{1}v_{1} + x_{2}v_{2} + \ldots + x_{n}v_{n}$$

Spesso questa è definita anche usando la <u>sommatoria</u>:

$$\sum\limits^{n}_{i=1} x_{i}v_{i}$$

Quindi è un vettore ottenuto sommando dei vettori moltiplicati per degli scalari.

###### Risoluzione di esercizi

Esercizi tipici potrebbero essere simili a [[#1) Dire se un vettore è una combinazione lineare di 2 vettori|questo]]; e il modo per risolverli è:

1) Prendo $n$ incognite quanti sono i vettori da verificare,
2) Moltiplico ogni vettore per la relativa incognita,
3) Sommo i vettori risultanti così da averne 1 solo sempre con incognite,
4) Creo e risolvo un sistema lineare dove pongo il 1° elemento del vettore iniziale = al 1° elemento del vettore calcolato e così via per tutti gli $n$ valori dei 2 vettori.

Se il sistema è risolvibile allora il vettore iniziale è una combinazione lineare dei vettori dati in base alle incognite scelte.

#### Indipendenza lineare

Un'insieme di vettori $\{v_{1}, v_{2}, \ldots v_{n}\} \in \mathbb{R}^{n}$ si dice **linearmente indipendente** se <u>nessun vettore dell'insieme è una combinazione lineare degli altri</u>; quindi se nessuno moltiplicato per 1 scalare è = a un altro vettore dell'insieme.

Più precisamente, l'<u>unico modo</u> per cui la <u>combinazione lineare dei vettori</u> dell'insieme <u>= 0</u> deve essere quando <u>tutti gli scalari sono = 0</u>. Se c'è anche <u>1 solo altro modo</u> di ottenere 0 dalla combinazione lineare dei vettori, <u>allora l'insieme è</u> **linearmente dipendente**.

> [!info] Nota
> L'**indipendenza lineare** non si basa su confronti tra i <u>singoli vettori dell'insieme</u>, bensì per ogni elemento bisogna verificare <u>tutte le possibili combinazioni lineari</u> fatte con altri vettori (non necessariamente tutti, ma 1 solo potrebbe non bastare purché vi sia una combinazione). ([[#2)|Esempio]]).

##### Proprietà

1) Qualsiasi insieme di vettori $\in \mathbb{R}^{n}$ che contiene un vettore nullo (tutti gli $n$ elementi = 0) è sempre **linearmente dipendente**.
2) Il **[[24 - Rank|rank]]** di una matrice $m \times n$ è il **n° di righe linearmente indipendenti di essa**.
3) Se una matrice $A \in M_{n}$ (è quadrata) e $det(A) = 0$, allora gli $n$ vettori riga della matrice sono <u>linearmente dipendenti</u> e $rank(A) < n$.

# Esercizi

###### 1) Dire se un vettore è una combinazione lineare di 2 vettori

Il vettore $v = [-\frac{3}{2}, 1, \frac{5}{2}]$ per quali valori è una combinazione lineare di $[1,2,3]$ e $[-1, 0, \frac{1}{2}]$ (se tali valori esistono)?

###### 2) Dire se un insieme di vettori è linearmente indipendente

Stabilire se l'insieme $A = \{[1,0,0], [0,1,0], [1,1,0]\}$ è linearmente indipendente o no.

###### 3) Dire se i vettori riga di una matrice sono linearmente indipendenti

Stabilire se i vettori riga di $A = \begin{bmatrix} 1 & 2 & 0 \\ 0 & 1 & 2 \\ 1 & 3 & 2 \end{bmatrix}$ sono linearmente indipendenti e confrontarli con il rango di $A$.

# Soluzioni

###### 1) 

$v = \left[-\dfrac{3}{2}, 1, \dfrac{5}{2}\right]$.

$v = a \cdot \left[1,2,3\right] + b \cdot \left[-1,0,\dfrac{1}{2}\right]$

$\left[-\dfrac{3}{2}, 1, \dfrac{5}{2}\right] = \left[a,2a,3a\right] + \left[-b,0,\dfrac{b}{2}\right]$

$\left[-\dfrac{3}{2}, 1, \dfrac{5}{2}\right] = \left[a-b, \; 2a, \; 3a+\dfrac{b}{2}\right]$

Sistema:

$\left\{\begin{aligned} -\dfrac{3}{2} &= a-b \\ 1 &= 2a \\ \dfrac{5}{2} &= 3a + \dfrac{b}{2} \end{aligned}\right.$

Da qui: $a = \dfrac{1}{2}$ e $b = 2$ (date in ordine la 2a e 1a riga). Confrontando ciò con la 3a riga $\dfrac{5}{2} = 3\left(\dfrac{1}{2}\right) + \dfrac{2}{2}$, il che risulta corretto.

Perciò il vettore $v$ è una combinazione lineare di $[1,2,3]$ e $[-1, 0, \frac{1}{2}]$ per gli scalari $\dfrac{1}{2}$ e $2$.

###### 2)

Dato $A = \{[1,0,0], [0,1,0], [1,1,0]\}$:

- $v_{1}$ non è una combinazione lineare di $v_{2}$, 
- $v_{2}$ non è una combinazione lineare di $v_{3}$, 
- $v_{3}$ non è una combinazione lineare di $v_{1}$.

Potrebbe sembrare indipendente, ma ciò è errato e sottolinea l'importanza di una verifica completa: $v_{3} = x_{1}v_{1} + x_{2}v_{2} \;\rightarrow\; [1,1,0] = x_{1}[1,0,0] + x_{2}[0,1,0]$.

Con $x_{1} = 1$ e $x_{2} = 1$ è evidente come l'insieme in esame sia **linearmente dipendente**.

###### 3)

Calcoliamo $rank(A)$ con Kronecker:

$A_{1} = \begin{bmatrix} {\color{lightgreen}{1}} & {\color{gray}{2}} & {\color{gray}{0}} \\ {\color{gray}{0}} & {\color{gray}{1}} & {\color{gray}{2}} \\ {\color{gray}{1}} & {\color{gray}{3}} & {\color{gray}{2}} \end{bmatrix} \;\rightarrow\; det(A_{1}) = 1 \;\rightarrow\; rank(A) = 1$

$A_{2} = \begin{bmatrix} {\color{lightgreen}{1}} & {\color{lightgreen}{2}} & {\color{gray}{0}} \\ {\color{lightgreen}{0}} & {\color{lightgreen}{1}} & {\color{gray}{2}} \\ {\color{gray}{1}} & {\color{gray}{3}} & {\color{gray}{2}} \end{bmatrix} \;\rightarrow\; det(A_{2}) = 1 - 0 \neq 0 \;\rightarrow\; rank(A) = 2$

$A_{3} = \begin{bmatrix} {\color{lightgreen}{1}} & {\color{lightgreen}{2}} & {\color{lightgreen}{0}} \\ {\color{lightgreen}{0}} & {\color{lightgreen}{1}} & {\color{lightgreen}{2}} \\ {\color{lightgreen}{1}} & {\color{lightgreen}{3}} & {\color{lightgreen}{2}} \end{bmatrix} \;\rightarrow\; det(A) = (sarrus) = 0 \;\rightarrow\; rank(A) = 2$

Questo indica che solo 2 vettori sono linearmente indipendenti e che l'altro dei 3 è la combinazione lineare degli altri. Prendiamo per esempio il 1° vettore riga.

$[1,2,0] = a[0,1,2] + b[1,3,2]$

$[1,2,0] = [0,a,2a] + [b,3b,2b]$

$[1,2,0] = [b,a+3b,2(a+b)]$

$\left\{\begin{aligned} 1 &= b \\ 2 &= a+3b \\ 0 &= 2(a+b) \end{aligned}\right. \;\rightarrow\; \left\{\begin{aligned} 1 &= b \\ 2 &= a+3 \\ 0 &= 2a+2 \end{aligned}\right. \;\rightarrow\; \left\{\begin{aligned} 1 &= b \\ -1 &= a \\ 0 &= -2+2 \end{aligned}\right. \;\rightarrow\; [1,2,0] = -[0,1,2] + [1,3,2]$

---

Prossima lezione: [[26 - Metodo di riduzione di Gauss]]

