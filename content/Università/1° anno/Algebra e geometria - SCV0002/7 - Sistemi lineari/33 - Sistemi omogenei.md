# Lezione 33

### Sistemi omogenei

Un sistema lineare si dice ***omogeneo*** se il <u>vettore dei termini noti</u> $B$ è il **vettore nullo**. In forma matriciale è: $A \cdot X = 0$.

##### Proprietà

1) Tali sistemi hanno <u>sempre soluzione</u> la quale, per qualunque configurazione della matrice $A$, avrà sempre il <u>vettore delle incognite</u> $X$ **nullo**,
2) L'unico caso in cui un sistema omogeneo ha <u>infinite soluzioni</u> è quando $rank(A) < n$; in quei casi infatti, per il [[30 - Teorema di Rouché-Capelli#Teorema di Rouché-Capelli|teorema di Rouché-Capelli]], la soluzione sarà sempre $\infty^{n - rank}$.

   > [!info] Nota

   > Questo vale perché: poiché $A|B$ si ottiene aggiungendo una colonna di 0, rimane il fatto che $rank(A) = rank(A|B)$.

# Esercizi

###### 1) Conferma di sistema omogeneo

Confermare che l'unica soluzione del seguente sistema omogeneo è $X = [0,0,0]$:

$$
\left\{\begin{aligned}
& 2x + y + z = 0 \\
& y + 2z = 0 \\
& x + 2y = 0
\end{aligned}\right.
$$

Tip: calcolare il rango.

###### 2) Conferma di sistema omogeneo

Confermare che l'unica soluzione del seguente sistema omogeneo è $X = [0,0]$:

$$
\left\{\begin{aligned}
& x + 2y = 0 \\
& x + 3z = 0 \\
\end{aligned}\right.
$$

Tip: calcolare il rango.

# Soluzioni

###### 1)

Creiamo la matrice corrispondente:

$$A = \begin{bmatrix} 2 & 1 & 1 \\ 0 & 1 & 2 \\ 1 & 2 & 0 \end{bmatrix}$$

Calcoliamone il rango con Gauss:

$$rank(A) = \begin{bmatrix} {\color{red}{2}} & 1 & 1 \\ 0 & 1 & 2 \\ {\color{orange}{1}} & 2 & 0 \end{bmatrix} \; \begin{aligned}  \\  \\ -\tfrac{1}{2} \cdot R_{1} \end{aligned} \;\rightarrow\; \begin{bmatrix} 2 & 1 & 1 \\ 0 & {\color{red}{1}} & 2 \\ 0 & {\color{orange}{\tfrac{3}{2}}} & -\tfrac{1}{2} \end{bmatrix} \; \begin{aligned}  \\  \\ -\tfrac{3}{2} \cdot R_{2} \end{aligned} \;\rightarrow\; \begin{bmatrix} {\color{aqua}{2}} & {\color{aqua}{1}} & {\color{aqua}{1}} \\ 0 & {\color{aqua}{1}} & {\color{aqua}{2}} \\ 0 & 0 & {\color{aqua}{-\tfrac{7}{2}}} \end{bmatrix}$$

Secondo il teorema di Rouché-Capelli, il n° delle soluzioni del sistema è = $\infty^{n-rank}$ = $\infty^{3-3}$ = $\infty^{0} = 1$.

...

###### 2)

Scriviamo l'equazione in forma matriciale:

$$A = \begin{bmatrix} 1 & 2 & 0 \\ 1 & 0 & 3 \end{bmatrix}$$

Calcoliamo il rank:

$$det\begin{bmatrix} {\color{lime}{1}} & {\color{lime}{2}} & {\color{gray}{0}} \\ {\color{lime}{1}} & {\color{lime}{0}} & {\color{gray}{3}} \end{bmatrix} = -2 \;\implies\; rank(A) = 2$$

Secondo il teorema di Rouché-Capelli, il n° delle soluzioni del sistema è = $\infty^{n-rank}$ = $\infty^{3-2}$ = $\infty^{1} = \infty$.

A questo punto risolviamo il sistema in base ad un'incognita (tipo $x$):

$$
\left\{\begin{aligned}
& x + 2y = 0 \\
& x + 3z = 0 \\
\end{aligned}\right.
\;\rightarrow\;
\left\{\begin{aligned}
& 2y = -x \\
& 3z = -x \\
\end{aligned}\right.
\;\rightarrow\;
\left\{\begin{aligned}
& y = -\dfrac{x}{2} \\
& z = -\dfrac{x}{3} \\
\end{aligned}\right.
$$

A questo punto le soluzioni del sistema sono state scritte in base al parametro scelto: $x$; e si scrivono quindi i valori di $x, y$ e $z$ come soluzione:

$$A = \{(x,-\tfrac{x}{2},-\tfrac{x}{3} \;|\; x \in \mathbb{R}\}$$

---

Prossima lezione: [[34 - Spazi vettoriali]]

