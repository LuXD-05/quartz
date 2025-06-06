# Lezione 1

### Insiemi

Ripassare la sezione "[[1° anno/Algebra e geometria - SCV0002/1 - Insiemi/1 - Definizioni e proprietà generali|insiemi]]" del corso di algebra e geometria; da qui seguiranno solo considerazioni nuove.

###### Simboli

![](https://i.imgur.com/PiM93vs.png)

###### Proprietà

![](https://i.imgur.com/KmLZGiI.png)

##### Differenza e complementari

Ricordiamo le operazioni tra insiemi di:

- **Differenza**: "$A - B$", ovvero tutti gli elementi in $A$ che non appartengono a $B$,
- **Complementare**: "$A - B$", ma qui sono gli elementi in $B$ che non appartengono ad $A$ (**complemento *assoluto*** se si riferisce all'insieme universo $U$, mentre ***relativo*** se si riferisce ad un insieme $B \neq U$),

###### Legge del doppio complementare

Il <u>complementare del complementare</u> di un insieme coincide con l'insieme stesso:

$$(A^{c})^{c} = U^{c} = A$$

###### Leggi di De Morgan

$$(A \cap B)^{c} = A^{c} \cup B^{c}$$

$$(A \cup B)^{c} = A^{c} \cap B^{c}$$

### Insiemi numerici

Per gli insiemi numerici $\mathbb{N}, \mathbb{Z}, \mathbb{Q}, \mathbb{R}$ possono essere definite delle **operazioni**; queste associano ad ogni coppia ordinata $(x,y) \in X \times X$ uno ed un solo elemento $z \in X$. Per questi abbiamo:

- **Somma**: $\forall x,y \in X \implies x+y \in X$,
- **Prodotto**: $\forall x,y \in X \implies x \cdot y \in X$.

Tali insiemi diventano quindi delle [[1° anno/Algebra e geometria - SCV0002/5 - Strutture algebriche/18 - Strutture algebriche|strutture algebriche]] in base alle proprietà delle operazioni che rispettano.

L'insieme $Q$ è un ***campo***, dato che:

- $x+y \in \mathbb{Q}$,
- $x \cdot y \in \mathbb{Q}$.

È anche ***commutativo***:

- $x+y = y+x$,
- $x \cdot y = y \cdot x$,

Associativo: $\mathbb{Q}$

- $(x+y)+z = x+(y+z)$
- $(x \cdot y) \cdot z = x \cdot (y \cdot z)$

Elem neutro:

$\exists 0 \in \mathbb{Q} \implies x + 0 = x$

$\exists 1 \in \mathbb{Q} \implies x \cdot 1 = x$

Esistenza dell'opposto e dell'inverso:

- $-x \in \mathbb{Q} \implies x + (-x) = 0$
- $x^{-1} \in \mathbb{Q} - \{0\} \implies x \cdot x^{-1} = 1$

Distributiva:

$(x+y) \cdot z = xz + yz$

###### Campo ordinale

Un campo si dice ***ordinale*** se è possibile determinare un ordine confrontando i suoi elementi, ovvero:

$\forall x,y,z \;|\; x \leq y \land ...$

$\forall x,y,z \;|\; ...$

Altro:

1) $\forall x \in \mathbb{Q} \;|\; x \geq 0 \implies -x \leq 0$, $\forall x, y \in \mathbb{Q} \;|\; x \geq y \implies -x \leq y$
2) $\forall x \in \mathbb{Q} \;|\; x > 0 \implies x^{-1} > 0$, $\forall x, y \in \mathbb{Q} \;|\; x \geq y > 0 \implies 0 < x^{-1} \leq y^{-1}$
3) $\forall x,y,z \in \mathbb{Q} \;|\; x \leq y \land z \leq 0 \implies xz > yz$
4) $\forall x \in \mathbb{Q} \;|\; x^{2} > 0$

#### Rappresentazione grafica insiemi numerici

(linee per ogni insieme n, z, q)

$\mathbb{Q}$ è ***denso*** in quanto: $\forall x,y \in \mathbb{Q} \;|\; \exists n \implies x < n < y$

###### Dimostrazione per assurdo

Esistono numeri non razionali, tipo $\sqrt{2}$ e ciò è dimostrabile **per assurdo**.

Si suppone il contrario di quello che si vuole dimostrare (quindi si suppone che $\sqrt{2}$ sia un numero razionale).

Per questo $\sqrt{2}$ deve rispettare tutte le proprietà di $\mathbb{Q}$, quindi:

$\sqrt{2} = \dfrac{x}{y}$ (con ...)

$$2 = (\dfrac{x}{y})^{2} \rightarrow x^{2} = 2y^{2} \;\;\rightarrow\;\; ...$$

### Numeri reali

...

###### Maggiorante e minorante

Dato un insieme non vuoto $A \subseteq \mathbb{R}$, un numero $n \in \mathbb{R}$ si dice:

- **Maggiorante** di $A$ se $\forall x \in A \implies n \geq x$ (numero che è maggiore di tutti i numeri in $A$),
- **Minorante** di $A$ se $\forall x \in A \implies n \leq x$ (numero che è minore di tutti i numeri in $A$).

> [!info] Nota
> Tendendo all'infinito, possono esistere <u>infiniti maggioranti e minoranti</u> di $A$:
> (foto linea numeri (pag 27 ?))
> Inoltre, si indicano:
> - $A^{*} =$ l'insieme dei maggioranti di $A$,
> - $A_{*} =$ l'insieme dei minoranti di $A$.

###### Limiti

In base a maggioranti e minoranti, si dice che:

- $A$ è **superiormente limitato** se <u>ammette almeno 1 maggiorante</u>,
- $A$ è **inferiormente limitato** se <u>ammette almeno 1 minorante</u>,
- $A$ è **limitato** se si verificano entrambe le precedenti.

###### Massimo e minimo

Per i [[#Limiti|limiti]] suddetti:

- Se $n$ è un <u>maggiorante</u> di $A$ incluso nello stesso, allora si dice **massimo** di $A$,
- Se $n$ è un <u>minorante</u> di $A$ incluso nello stesso, allora si dice **minimo** di $A$.

> [!info] Nota
> Massimi e minimi sono **unici** negli insiemi dato che in essi non possono essere inclusi più di 1 maggiorante/minorante (siccome uno sarebbe già maggiore/minore degli altri).
> (foto?)
> Gli unici casi in cui ci sono più massimi/minimi è quando tali sono lo <u>stesso numero</u> (segue dimostrazione per assurdo con 2 numeri generici $m_{1}$ e $m_{2}$).

###### Estremi

Dato un insieme non vuoto $A \subseteq \mathbb{R}$, se $A$ è <u>limitato</u>:

- Si dice **estremo superiore** ($sup(A)$) il <u>più piccolo maggiorante</u> di $A$,
- Si dice **estremo inferiore** ($inf(A)$) il <u>più grande minorante</u> di $A$.

> [!info] Nota
> Per quanto riguarda gli estremi:
> - Se $sup(A) \in A \implies sup(A) = max(A)$,
> - Se $inf(A) \in A \implies inf(A) = min(A)$.

##### Teorema di completezza di ${} \mathbb{R}$

Per ogni insieme non vuoto ${} A \subseteq {}$

Se $A \subseteq \mathbb{R}, A \neq \emptyset$:

- È limitato superiormente $\implies \exists \; sup(A)$,
- È limitato inferiormente $\implies \exists \; inf(A)$,

### Radici e potenze

gao

# Esercizi

![](https://i.imgur.com/9CzTv84.png)

# Soluzioni

---

Prossima lezione: [[]]

