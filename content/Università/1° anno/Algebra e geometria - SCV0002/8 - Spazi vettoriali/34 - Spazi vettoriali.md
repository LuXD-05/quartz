# Lezione 34

### Spazi vettoriali

Uno **spazio vettoriale** è una struttura algebrica definita per un insieme $V$ (i cui elementi sono chiamati "***vettori***") con le seguenti 2 operazioni:

$$(V, +, \cdot)$$

In ogni spazio vettoriale:

- "$+$" è l'operazione binaria di **somma** su $V$ ($+: V \times V \rightarrow V$) tra 2 vettori,
- "$\,\cdot\,$" rappresenta invece il **prodotto esterno** ($\cdot\,: \mathbb{R} \times V \rightarrow V$) fatto tra un vettore ed uno scalare.

> [!info] Nota
> Anche per gli **spazi vettoriali**, come per matrici, funzioni ed altri elementi algebrici, è necessario dichiarare un **campo** <u>sul quale essi sono definiti</u>. Per comodità prendiamo per partito preso che per i nostri esempi, esso sarà l'insieme $\mathbb{R}$.
> Gli elementi del campo su cui è definito uno spazio vettoriale sono detti "***scalari***".

###### Verificare spazi vettoriali

Per verificare se una struttura è uno spazio vettoriale bisogna:

1) <u>Definire l'insieme</u> $V$, l'<u>operazione di somma</u> ($+$) e quella di <u>prodotto per uno scalare</u> ($\,\cdot\,$),
2) Verificare la validità delle seguenti proprietà:

##### Proprietà della somma

1) **Stabilità**: $\forall x, y \in V \implies x + y \in V$,
2) **Commutatività**: $\forall x, y \in V \implies x + y = y + x$,
3) **Associatività**: $(x + y) + z = x + (y + z)$,
4) **Elemento neutro**: $\forall x \in V, \;\; 0 \in V \implies x + 0 = x$,
5) **Elemento opposto**: $\forall x \in V, \;\; -x \in V \implies x + (-x) = 0$.

##### Proprietà del prodotto esterno

1) **Stabilità**: se $x \in \mathbb{R}$ e $v \in V$ $\implies x \cdot v \in V$,
2) **Elemento neutro**: $\forall x \in V, \;\; 1 \in V \implies x \cdot 1 = x$,
3) "**Associatività**" (*compatibilità con prodotto scalare*): $(x \cdot y) \cdot v = x \cdot (y \cdot v)$, dove $x$ e $y$ sono scalari, mentre $v$ è un vettore,
4) **Distributività rispetto alla somma** (dove $x$ e $y$ sono scalari e $v_{n}$ sono vettori): 

   - Sia di **scalari**: $v \cdot (x + y) = v \cdot x + v \cdot y$,

   - Sia di **vettori**: $x \cdot (v_{1} + v_{2}) = x \cdot v_{1} + x \cdot v_{2}$.

# Esercizi

###### 1) Verifica di spazio vettoriale

Dire se l'insieme $\mathbb{R}^{2}$ (contenente coppie ordinate di numeri reali $(x,y)$) è uno spazio vettoriale.

###### 2) Verifica di spazio vettoriale

Dire se l'insieme $\mathbb{N}$ è uno spazio vettoriale.

# Soluzioni

###### 1)

Definiamo somma e prodotto scalare di $\mathbb{R}^{2}$:

- $+ : \mathbb{R}^{2} \times \mathbb{R}^{2} \rightarrow \mathbb{R}^{2}$
- $\cdot\, : \mathbb{R} \times \mathbb{R}^{2} \rightarrow \mathbb{R}^2$

Ogni proprietà di somma e prodotto scalare in $\mathbb{R}^{2}$ è valida. perciò $\mathbb{R}^{2}$ è uno spazio vettoriale.

###### 2)

Definiamo somma e prodotto scalare di ${} \mathbb{N} {}$:

- ${} + : \mathbb{N} \times \mathbb{N} \rightarrow \mathbb{N} {}$
- $\cdot\, : \mathbb{R} \times \mathbb{N} \rightarrow \mathbb{N}$

$\mathbb{N}$ non è uno spazio vettoriale, in quanto:

- Per la somma, in $\mathbb{N}$ non ci sono opposti dei suoi elementi che appartengono sempre a $\mathbb{N}$,
- Per il prodotto scalare, non tutti gli elementi di $\mathbb{N}$ moltiplicati per uno scalare in $\mathbb{R}$ danno un risultato ancora contenuto in $\mathbb{N}$.

---

Prossima lezione: [[35 - Sottospazi]]

