# Lezione 24

### Rank

Il ***rank*** (o **rango**) di una matrice è <u>il più grande ordine di una sottomatrice quadrata con determinante</u> $\neq 0$ e qualsiasi matrice $n \times m$ ce l'ha.

> [!info] In generale
> Il rango di una matrice $A$ con $n$ righe e $m$ colonne è sempre:
> $$0 \leq rank(A) \leq min(n,m)$$

##### Proprietà

- Una matrice ha ***rank* = 0** solo se è interamente <u>composta da 0</u>,
- Il *rank* di una matrice è <u>sempre positivo</u>, infatti se $A = \begin{bmatrix} 0 & 2 \\ 1 & 0 \end{bmatrix}$ $det(A) = -2 \;\rightarrow\; rank(A) = 2$,
- Una matrice ha ***rank* massimo** se esso coincide con il <u>minore</u> tra il suo <u>n° di righe e di colonne</u>.

#### Calcolo del rank

Per calcolare il *rank* di una matrice la strategia più intuitiva è seguire il ***criterio dei minori***, secondo il quale:

1) Si considera $x$ il <u>minimo tra il n° di righe e di colonne della matrice</u> in esame e si cerca una <u>sottomatrice quadrata di quell'ordine</u> al suo interno,
2) Se una tra tutte le sottomatrici trovate ha determinante $\neq 0$ allora si stabilisce che la matrice originale ha $rank = x$,
3) Se tutte le sottomatrici di ordine $x$ hanno determinante $= 0$, allora si ricomincia dallo step 1 ma con $x = x - 1$.

##### Teorema di Kronecker

Il **Teorema di Kronecker** (o *teorema degli orlati*) fornisce un altro procedimento per il calcolo del rango di una matrice; tuttavia è necessario conoscere i concetti di [[#Minori|minore]] e [[#Orlati|minore orlato]] di una matrice.

###### Minori

> [!important] Minore
> Data una matrice $A$ con $n$ righe e $m$ colonne, un suo **minore di ordine** $k$ è il <u>determinante di una sua sottomatrice quadrata</u> (sempre di ordine $k$) ottenuta <u>eliminando</u> $n - k$ <u>righe e</u> $m - k$ <u>colonne</u> (non per forza adiacenti).
> Strano ma vero, in questa situazione anche i determinanti hanno un ordine 😥, ma per alcuni il **minore** è il <u>determinante</u> mentre per altri è la <u>sottomatrice</u> (dipende dalla fonte o dall'insegnante).
> Comunque per chiarire sull'adiacenza, consideriamo la seguente matrice:
> $$\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}$$
> Un minore può essere (eliminando la riga 3 e colonna 3):
> $$\begin{bmatrix} {\color{lime}{1}} & {\color{lime}{2}} & {\color{grey}{3}} \\ {\color{lime}{4}} & {\color{lime}{5}} & {\color{grey}{6}} \\ {\color{grey}{7}} & {\color{grey}{8}} & {\color{grey}{9}} \end{bmatrix}$$
> Come anche (eliminando la riga 1 e colonna 2):
> $$\begin{bmatrix} {\color{grey}{1}} & {\color{grey}{2}} & {\color{grey}{3}} \\ {\color{lime}{4}} & {\color{grey}{5}} & {\color{lime}{6}} \\ {\color{lime}{7}} & {\color{grey}{8}} & {\color{lime}{9}} \end{bmatrix}$$

###### Orlati

"*Orlare*", nel contesto delle sottomatrici, significa espandere una sottomatrice di 1 riga e 1 colonna.

> [!important] Minore orlato
> Si parla di **minore orlato** quando ci si riferisce ad un [[#Minori|minore]] la cui <u>sottomatrice è stata espansa di 1 riga e 1 colonna</u> all'interno della matrice in cui è contenuta. In pratica, consideriamo la seguente matrice (con un minore in verde):
> $$\begin{bmatrix} {\color{grey}{1}} & {\color{grey}{2}} & {\color{grey}{3}} & {\color{grey}{4}} \\ {\color{grey}{5}} & {\color{lime}{6}} & {\color{lime}{7}} & {\color{grey}{8}} \\ {\color{grey}{9}} & {\color{lime}{10}} & {\color{lime}{11}} & {\color{grey}{12}} \end{bmatrix}$$
> Orlando tale minore è possibile ottenere (per esempio) questa matrice (verde + blu):
> $$\begin{bmatrix} {\color{grey}{1}} & {\color{lightblue}{2}} & {\color{lightblue}{3}} & {\color{lightblue}{4}} \\ {\color{grey}{5}} & {\color{lime}{6}} & {\color{lime}{7}} & {\color{lightblue}{8}} \\ {\color{grey}{9}} & {\color{lime}{10}} & {\color{lime}{11}} & {\color{lightblue}{12}} \end{bmatrix}$$
> Anche qui è possibile orlare un minore per una riga/colonna qualsiasi, non necessariamente per una adiacente.

###### Procedimento

Il teorema di Kronecker dice che una matrice $n \times m$ ha rango $k$ se:

- Esiste un **minore di ordine** $k$ <u>non nullo</u>,
- Tutti i **minori** di ordine ${} k+1$ ottenuti <u>orlando il minore precedente con qualunque altra riga/colonna sono nulli</u>.

Questo è importante in quanto, al contrario del *criterio dei minimi*, permette generalmente di <u>ridurre il numero totale di minori da calcolare</u>.

# Esercizi

# Soluzioni

---

Prossima lezione: [[25 - Vettori linearmente indipendenti]]

