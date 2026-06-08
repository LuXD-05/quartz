# Lezione 32

##### Presupposti

Data una <u>matrice quadrata</u> $A \in M_{n}$, sappiamo che, per il [[27 - Inversa#Teorema di Binet|teorema di Binet]], se $det(A) \neq 0$, $A$ è **[[27 - Inversa#Invertibilità|invertibile]]**, perciò: 

$$det(A^{-1}) = \dfrac{1}{det(A)} \;\;\;\rightarrow\;\;\; A^{-1} = \dfrac{A_{cof}^{T}}{det(A)}$$

### Metodo di Cramer

Abbiamo un generico sistema scritto in forma matriciale:

$$B = A \cdot X$$

Per ottenere il vettore colonna delle incognite $X$ bisogna moltiplicare (a sinistra) da entrambe le parti dell'equazione per $A^{-1}$, siccome:

$$A^{-1} \cdot B = A^{-1} \cdot (A \cdot X) \;\;\;\rightarrow\;\;\; A^{-1} \cdot B = I_{n} \cdot X \;\;\;\rightarrow\;\;\; X = A^{-1} \cdot B$$

Si nota che $A^{-1} \cdot A = I_{n}$, e anche che $I_{n} \cdot X = X$ (*trasformazione neutra*). Sostituendo poi $A^{-1}$ si ha:

$$X = \dfrac{A_{cof}^{T}}{det(A)} \cdot B$$

Sappiamo però che $X$ è un **vettore colonna** corrispondente a $[x_{1}, \;\ldots,\; x_{n}]^{T}$; perciò, per trovare le singole incognite $x_{i}$ è necessario *espandere* la formula per ogni *i*-esimo elemento di $X$:

$$x_{i} = \dfrac{\sum\limits^{n}_{j=1} cof_{ji}(A) \cdot B_{j}}{det(A)}$$

Prestiamo attenzione al numeratore: 

Innanzitutto usiamo $cof_{ji}(A)$ in quanto corrisponde al $cof_{ij}(A^{T})$, siccome la ***trasposizione*** <u>fa corrispondere</u> la ***i*-esima riga** di $A^{T}$ con la ***j*-esima colonna** di $A$:

$$A = \begin{bmatrix} {\color{yellow}{1}} & {\color{yellow}{2}} \\ 3 & 4 \end{bmatrix} \;\;\;\rightarrow\;\;\; A^{T} = \begin{bmatrix} {\color{yellow}{1}} & 3 \\ {\color{yellow}{2}} & 4 \end{bmatrix}$$

Ricordiamo poi che, col [[23 - Determinante#Metodo di Laplace|metodo di Laplace]], il **determinante** di una matrice $A$ è la <u>somma dei cofattori di una riga/colonna di</u> $A$ <u>moltiplicati per gli elementi della stessa</u>:

$$det(A) = \sum\limits^{n}_{i \textfractionsolidus j=1} cof(a_{ij}) \cdot a_{ij}$$

Perciò è intuibile la corrispondenza tra questo e l'intero numeratore della formula di $x_{i}$. Più precisamente, dato che stiamo <u>moltiplicando i cofattori di una colonna</u> per gli <u>elementi del vettore colonna dei termini noti</u> $B$, la formula di *Laplace* risulta <u>corretta</u> quando **sostituiamo la *i*-esima colonna in esame con gli elementi di** $B$.

Ciò ci da che per una colonna $i$:

$$det(A_{i}) = \sum\limits^{n}_{j=1} cof_{ji}(A) \cdot B_{j}$$

Quindi la formula di $x_{i}$ si può riscrivere così:

$$x_{i} = \dfrac{det(A_{i})}{det(A)}$$

Per concludere, considerando le matrici $A_{i}$ ottenute sostituendo ogni *i*-esima colonna con $B$ (*vettore colonna delle soluzioni*), la soluzione del sistema (ovvero i valori del *vettore colonna delle incognite* $X$) è:

$$X = \left(\dfrac{det(A_{1})}{det(A)}, \;\ldots,\; \dfrac{det(A_{n})}{det(A)}\right)$$

# Esercizi

# Soluzioni

---

Prossima lezione: [[34 - Spazi vettoriali]]

