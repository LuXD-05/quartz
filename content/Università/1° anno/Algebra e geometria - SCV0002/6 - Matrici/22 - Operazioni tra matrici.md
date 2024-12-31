# Lezione 22

### Operazioni tra matrici

##### Somma

(Vale anche per la **sottrazione**), la **somma** di 2 matrici $A_{n,m}$ e $B_{n,m}$ da come risultato una <u>matrice</u> $n \times m$ i cui <u>elementi = somme degli elementi</u> di $A$ e $B$.

> [!error] Attenzione
> La somma di 2 matrici ${} A$ e $B$ è possibile solo quando <u>entrambe</u> hanno lo <u>stesso numero di righe e di colonne</u>.

###### Struttura algebrica somma

Si definisce quindi la struttura algebrica $(M_{n,m},+)$, che:

- È commutativa e associativa,
- Ha come elemento neutro la [[21 - Matrici#Matrice nulla|matrice nulla]] $0_{m,n}$,
- È simmetrizzabile se esiste una matrice ${} A'$ tale che $a_{ij} = -a'_{ij}$ e viceversa.

Perciò $(M_{n,m},+)$ è un **[[18 - Strutture algebriche#Strutture algebriche|gruppo]]**.

##### Prodotto

(Non so se vale anche per la divisione), il **prodotto** (righe $\times$ colonne) di 2 matrici $A_{n,m}$ e $B_{m,n}$ da come risultato una matrice quadrata [[21 - Matrici#Matrice quadrata|matrice quadrata]] di **ordine** $n$.

In generale, la matrice risultante $C_{n}$ è data da:

$$C_{n} = \sum\limits^{n}_{m=1}(a_{im} \cdot b_{mj})$$

Ovvero la 1a riga di $A$ moltiplicata per la 1a colonna di $B$ sarà il valore di $C_{1,1}$ e così via. In pratica i valori di $c_{ij}$ sono il prodotto della riga $a_{i}$ per la colonna $b_{j}$ (quando si parla di prodotto anche tra 2 vettori righe/colonne si intende moltiplicare i valori con indici uguali e sommare tutti i risultati ottenuti).

![](https://github.com/mrdbourke/pytorch-deep-learning/raw/main/images/00-matrix-multiply-crop.gif)

> [!error] Attenzione
> Il prodotto di 2 matrici $A_{n,m}$ e $B_{m,n}$ è possibile solo quando il <u>n° di righe della 1a = n° di colonne della 2a</u>.

###### Struttura algebrica prodotto

Si definisce quindi la struttura algebrica $(M_{n,m},\cdot)$, che:

- È associativa ma NON commutativa,
- Ha elemento neutro $I_{n}$ se si considerano le matrici quadrate $\in M_{n}$,
- NON è simmetrizzabile per ogni caso.

Perciò $(M_{n,m},\cdot)$ è un [[18 - Strutture algebriche#Strutture algebriche|monoide]] non commutativo.

# Esercizi

# Soluzioni

---

Prossima lezione: [[23 - Determinante]]

