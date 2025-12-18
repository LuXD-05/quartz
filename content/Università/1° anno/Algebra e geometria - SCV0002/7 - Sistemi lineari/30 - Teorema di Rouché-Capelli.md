# Lezione 30

### Teorema di Rouché-Capelli

Il **teorema di Rouché-Capelli** permette di capire se un sistema con un qualsiasi numero di equazioni ed incognite è compatibile o meno.

###### Matrice completa

Data la [[29 - Sistemi lineari#Matriciale|forma matriciale]] di un sistema $B = A \cdot X$, si definisce ***matrice completa*** quella formata da quella dei termini noti ($B$) affiancata a quella delle equazioni ($A$), ovvero:

$$(A|B) \in M_{m,n+1} = \begin{bmatrix} a_{11} & a_{12} & \dots & a_{1n} \;\;|\;\; b_{1} \\ a_{21} & a_{22} & \dots & a_{2n} \;\;|\;\; b_{2} \\ \vdots & \vdots & \ddots & \;\vdots \;\;\;\,\lvert\,\;\; \vdots \\ a_{m1} & a_{m2} & \dots & a_{mn} \;\;|\;\; b_{m} \end{bmatrix}$$

##### Teorema

Sia ${} B = A \cdot X {}$ un sistema lineare di $m$ equazioni in $n$ incognite:

- Se ${} rank(A) \neq rank(A|B) {}$, allora il sistema è **incompatibile** (0 soluzioni),
- Se ${} rank(A) = rank(A|B) {}$, allora il sistema è **compatibile**:
  - Se $rank = n$ (${} rank = rank(A) = rank(A|B) {}$, $n =$ incognite in $X$), allora il sistema ammette <u>1 sola soluzione</u>,
  - Se $rank < n$, il sistema ammette <u>infinite soluzioni che dipendono da</u> $n - rank$ <u>parametri</u> (si dice quindi che ci sono $\infty^{n-rank}$ soluzioni)

# Esercizi

# Soluzioni

---

Prossima lezione: [[31 - Risolvere sistemi con Gauss]]

