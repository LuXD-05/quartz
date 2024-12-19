# Lezione 27

### Invertibilità

Una matrice quadrata $A \in M_{n}$ è invertibile se esiste una matrice $A^{-1} \in M_{n}$ tale che $A \cdot A^{-1} = I_{n}$. ${} \;A^{-1} {}$ si dice quindi ***inversa*** di $A$.

Quando si parla di inversa di una matrice ci sono 2 teoremi principali:

##### Teorema di Binet

Questo definisce semplicemente delle relazioni tra 2 matrici quadrate dello stesso ordine; ed è applicabile anche tra una matrice $n \times n$ e la sua inversa.

Se 2 matrici $A, B \in M_{n}$ allora:

$$det(A \cdot B) = det(A) \cdot det(B)$$

Se poi $A$ è [[#Invertibilità|invertibile]], allora:

$$det(A \cdot A^{-1}) \;=\; det(A) \cdot det(A^{-1}) \;=\; det(I_{n}) \;=\; 1$$

perciò:

$$det(A) = \dfrac{1}{det(A^{-1})} \;\;\land\;\; det(A^{-1}) = \dfrac{1}{det(A)}$$

Infine (per le condizioni di esistenza delle frazioni) se $A$ è invertibile, allora ${} det(A) \neq 0 {}$ e anche $det(A^{-1}) \neq 0$.

###### Proprietà

Dato $GL_{n} = \{A \in M_{n} \;|\; det(A) \neq 0\}$, la struttura algebrica $(GL_{n}, \cdot)$ è un gruppo non commutativo detto ***gruppo lineare***.

###### Inversa con Binet

Sfruttando il **teorema di Binet** è possibile calcolare l'**inversa** di una matrice quadrata grazie a questa formula:

$$A^{-1} = \dfrac{A_{cof}^{T}}{det(A)}$$

In pratica, partendo da una matrice $A \in M_{n}$ qualunque:

- Se ne calcola la [[23 - Determinante#Complemento algebrico|matrice dei cofattori]] (come per *Laplace*) [[21 - Matrici#Trasposta|trasposta]],
- La si moltiplica per $\dfrac{1}{det(A)}$ e si ottiene l'inversa $A^{-1}$.

##### Teorema di Gauss-Jordan

Quando si ha una matrice $A \in M_{n}$ con $det(A) \neq 0$, l'inversa di $A$ è calcolabile col **teorema di Gauss-Jordan**.

Se $A \in M_{n}$, consideriamo la matrice $(A|I_{n})$ (questa dicitura rappresenta una matrice $n \times 2n$ composta da $A$ con affiancata $I_{n}$), tipo:

$$(A|I_{n}) = \begin{bmatrix} 2 & 3 \;\; | \;\; 1 & 0 \\ 1 & 1 \;\; | \;\; 0 & 1\end{bmatrix}$$

Il teorema prevede di utilizzare le [[26 - Metodo di riduzione di Gauss#Procedimento|mosse di Gauss]] per trasformare $A$ in $I_{n}$. Unica cosa è che i cambiamenti valgono per l'intera matrice $(A|I_{n})$, la quale diventa poi $(I_{n}|B)$; la matrice risultante $B$ è l'inversa di $A$ (vedi l'[[#1) Gauss-Jordan|esempio]]).

# Esercizi

###### 1) Binet e Gauss-Jordan

Trovare l'inversa di:

$$A = \begin{bmatrix} 2 & 3 \\ 1 & 1 \end{bmatrix}$$

col teorema di Binet e poi con quello di Gauss-Jordan.

###### 2) Gauss-Jordan

Trovare l'inversa di:

$$A = \begin{bmatrix} 1 & 0 & 1 \\ 2 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

col teorema di Gauss-Jordan.

# Soluzioni

###### 1) Binet

Per l'inversa di:

$$A = \begin{bmatrix} 2 & 3 \\ 1 & 1 \end{bmatrix}$$

Calcoliamone il determinante:

$$det(A) = (2) - (3) = -1 \neq 0$$

Troviamone la matrice dei cofattori:

$$Cof(a_{ij}) = (-1)^{i+j} \cdot det(A_{ij})$$

$$A_{cof} = \begin{bmatrix} 1 \cdot det(1) & -1 \cdot det(1) \\ -1 \cdot det(3) & 1 \cdot det(2) \end{bmatrix} = \begin{bmatrix} 1 & -1 \\ -3 & 2 \end{bmatrix}$$

Trasponiamo la matrice dei cofattori:

$$A_{cof}^{T} = \begin{bmatrix} 1 & -3 \\ -1 & 2 \end{bmatrix}$$

E moltiplichiamola per $\dfrac{1}{det(A)}$:

$$A^{-1} = \dfrac{1}{det(A)} \cdot \begin{bmatrix} 1 & -3 \\ -1 & 2 \end{bmatrix} = \begin{bmatrix} {\color{aqua}{-1}} & {\color{aqua}{3}} \\ {\color{aqua}{1}} & {\color{aqua}{-2}} \end{bmatrix}$$

###### 1) Gauss-Jordan

Innanzitutto scriviamo la matrice $(A|I_{2})$:

$$(A|I_{2}) = \begin{bmatrix} 2 & 3 \;\; | \;\; 1 & 0 \\ 1 & 1 \;\; | \;\; 0 & 1\end{bmatrix}$$

Ora procediamo con le mosse di Gauss:

$$\begin{bmatrix} {\color{red}{2}} & 3 \;\; | \;\; 1 & 0 \\ {\color{orange}{1}} & 1 \;\; | \;\; 0 & 1\end{bmatrix}$$

Normalizziamo la prima riga (avremmo potuto anche scambiare le 2 righe):

$$\begin{bmatrix} {\color{yellow}{2}} & {\color{yellow}{3}} \;\; | \;\; {\color{yellow}{1}} & {\color{yellow}{0}} \\ 1 & 1 \;\; | \;\; 0 & 1\end{bmatrix} \rightarrow \begin{aligned} & / 2 \\ & \end{aligned} \rightarrow \begin{bmatrix} {\color{red}{1}} & \frac{3}{2} \;\; | \;\; \frac{1}{2} & 0 \\ {\color{orange}{1}} & 1 \;\; | \;\; 0 & 1\end{bmatrix}$$

Procediamo con la seconda:

$$\begin{bmatrix} {\color{red}{1}} & \frac{3}{2} \;\; | \;\; \frac{1}{2} & 0 \\ {\color{orange}{1}} & 1 \;\; | \;\; 0 & 1\end{bmatrix} \rightarrow \begin{aligned} & \\ + (-1) \cdot (R_{1}) \end{aligned} \rightarrow \begin{bmatrix} 1 & \frac{3}{2} \;\; | \;\; \frac{1}{2} & 0 \\ 0 & -\frac{1}{2} \;\; | \;\; -\frac{1}{2} & 1 \end{bmatrix}$$

Trasformiamo ora la seconda (moltiplicandola per un numero) per fare in modo che la matrice originale $A$ si avvicini sempre di più a $I_{2}$:

$$\begin{bmatrix} 1 & \frac{3}{2} \;\; | \;\; \frac{1}{2} & 0 \\ {\color{yellow}{0}} & {\color{yellow}{-\frac{1}{2}}} \;\; | \;\; {\color{yellow}{-\frac{1}{2}}} & {\color{yellow}{1}} \end{bmatrix} \rightarrow \begin{aligned} & \\ \cdot \;(-2) \end{aligned} \rightarrow \begin{bmatrix} 1 & \frac{3}{2} \;\; | \;\; \frac{1}{2} & 0 \\ 0 & 1 \;\; | \;\; 1 & -2 \end{bmatrix}$$

Per ottenere infine $(I_{2}|B)$ è necessaria una sola mossa di Gauss aggiuntiva, ovvero fare la combinazione lineare della 1a riga con la seconda moltiplicata per un numero tale che (in questo caso) $(A|I_{2})_{12} \rightarrow 0$:

$$\begin{bmatrix} {\color{yellow}{1}} & {\color{yellow}{\frac{3}{2}}} \;\; | \;\; {\color{yellow}{\frac{1}{2}}} & {\color{yellow}{0}} \\ 0 & 1 \;\; | \;\; 1 & -2 \end{bmatrix} \rightarrow \begin{aligned} + (-\tfrac{3}{2}) \cdot (R_{2}) \\ & \end{aligned} \rightarrow \begin{bmatrix} {\color{aqua}{1}} & {\color{aqua}{0}} \;\; | \;\; {\color{aqua}{-1}} & {\color{aqua}{3}} \\ 0 & {\color{aqua}{1}} \;\; | \;\;\;\;\, {\color{aqua}{1}} & {\color{aqua}{-2}} \end{bmatrix} = (I_{2}|B) = (I_{2}|A^{-1})$$

Controlliamo infine che $A \cdot A^{-1} = I_{2}$:

$$A \cdot A^{-1} = \begin{bmatrix} 2 & 3 \\ 1 & 1 \end{bmatrix} \cdot \begin{bmatrix} -1 & 3 \\ 1 & -2 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$

###### 2)

---

Prossima lezione: [[28 - Equazioni lineari]]

