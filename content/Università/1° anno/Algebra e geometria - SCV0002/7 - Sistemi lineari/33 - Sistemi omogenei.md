# Lezione 33

### Sistemi omogenei

Un sistema lineare si dice ***omogeneo*** se il <u>vettore dei termini noti</u> $B$ è il **vettore nullo**. In forma matriciale è: $A \cdot X = 0$.

##### Proprietà

1) Tali sistemi hanno <u>sempre soluzione</u> la quale, per qualunque configurazione della matrice $A$, avrà sempre il <u>vettore delle incognite</u> $X$ **nullo**,
2) L'unico caso in cui un sistema omogeneo ha <u>infinite soluzioni</u> è quando $rank(A) < n$; in quei casi infatti, per il [[30 - Teorema di Rouché-Capelli#Teorema di Rouché-Capelli|teorema di Rouché-Capelli]], la soluzione sarà sempre $\infty^{n - rank}$ (vale perché: poiché $A|B$ si ottiene aggiungendo una colonna di 0, rimane il fatto che $rank(A) = rank(A|B)$).

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

Confermare che l'unica soluzione del seguente sistema omogeneo è $X = [0,0,0]$:

$$
\left\{\begin{aligned}
& x + 2y = 0 \\
& x + 3z = 0 \\
\end{aligned}\right.
$$

Tip: calcolare il rango.

# Soluzioni

###### 1)

###### 2)

---

Prossima lezione: [[34 - Spazi vettoriali]]

