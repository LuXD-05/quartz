# Lezione 29

### Sistemi lineari

Un sistema lineare è un'insieme di $m$ equazioni lineari a $n$ incognite descritto nel seguente modo:

$$\left\{\begin{aligned}
& b_{1} = a_{11}x_{1} + \ldots + a_{1n}x_{n} \\
& b_{2} = a_{21}x_{1} + \ldots + a_{2n}x_{n} \\
& \vdots \\
& b_{m} = a_{m1}x_{1} + \ldots + a_{mn}x_{n}
\end{aligned}\right.$$

###### Soluzione di un sistema

Una soluzione di un sistema lineare di $m$ equazioni in $n$ incognite è una *n-upla* di numeri che è soluzione di ogni equazione del sistema (dato che le incognite sono le stesse per tutte le equazioni). Però un sistema può avere solo:

- <u>Nessuna soluzione</u> (***sistema impossibile o incompatibile***),
- <u>1 sola soluzione</u> (***sistema compatibile*** a 1 soluzione),
- <u>Infinite soluzioni</u> (***sistema compatibile indeterminato***).

##### Matriciale

I sistemi di equazioni lineari sono rappresentabili in ***forma matriciale***; per la quale si hanno:

- $A \begin{bmatrix} a_{11} & a_{12} & \dots & a_{1n} \\ a_{21} & a_{22} & \dots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \dots & a_{mn} \end{bmatrix} \in M_{mn}$, la **matrice dei coefficienti** $n \times m$,
- $X = \begin{pmatrix} x_{1} \\ x_{2} \\ \vdots \\ x_{m} \end{pmatrix} \in M_{n1}$, il **vettore colonna delle incognite**,
- $B = \begin{pmatrix} b_{1} B\ b_{2} \\ \vdots \\ b_{m} \end{pmatrix} \in M_{m1}$, il **vettore colonna dei termini noti**.

Il sistema allora si potrà scrivere utilizzando il prodotto righe per colonne come:

$$B = A \cdot X$$

# Esercizi

# Soluzioni

---

Prossima lezione: [[30 - Teorema di Rouché-Capelli]]

