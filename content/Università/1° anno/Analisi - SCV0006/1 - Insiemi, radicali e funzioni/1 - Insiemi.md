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

#### Insiemi numerici

Per gli insiemi numerici $\mathbb{N}, \mathbb{Z}, \mathbb{Q}, \mathbb{R}$ possono essere definite delle **operazioni**; queste associano ad ogni coppia ordinata $(x,y) \in X \times X$ un solo elemento $z \in X$ per mezzo di un'operazione tra $x$ e $y$. Per questi abbiamo:

- **Somma**: $\forall x,y \in X \implies x+y \in X$,
- **Prodotto**: $\forall x,y \in X \implies x \cdot y \in X$.

Tali insiemi diventano quindi delle [[1° anno/Algebra e geometria - SCV0002/5 - Strutture algebriche/18 - Strutture algebriche|strutture algebriche]] in base alle proprietà delle operazioni che rispettano.

##### Proprietà (campo)

Si dice che $\mathbb{Q}$ sia un **campo** in quanto rispetta tutte le seguenti proprietà:

**Chiusura** (somma e prodotto di 2 elementi sempre all'interno dell'insieme):

- $x+y \in \mathbb{Q}$,
- $x \cdot y \in \mathbb{Q}$.

**Commutatività** (ordine degli operandi indifferente e risultato sempre uguale):

- $x+y = y+x$,
- $x \cdot y = y \cdot x$,

**Associatività** (indifferente se si sommano/moltiplicano elementi in ordine diverso):

- $(x+y)+z = x+(y+z)$
- $(x \cdot y) \cdot z = x \cdot (y \cdot z)$

**Elemento neutro**:

- $\exists 0 \in \mathbb{Q} \implies x + 0 = x$
- $\exists 1 \in \mathbb{Q} \implies x \cdot 1 = x$

**Elementi opposti e invertibili**:

- $-x \in \mathbb{Q} \implies x + (-x) = 0$
- $x^{-1} \in \mathbb{Q} - \{0\} \implies x \cdot x^{-1} = 1$

**Distributività**:

$(x+y) \cdot z = xz + yz$

###### Campo ordinale

Un campo si dice ***ordinale*** se <u>è possibile determinare un ordine confrontando i suoi elementi</u>, ovvero:

$$\left.\begin{aligned}
& \forall x,y,z \;|\; x \leq y \implies x+z \leq y+z \\
& \forall x,y,z \;|\; x \leq y \land z \geq 0 \implies x \cdot z \leq y \cdot z
\end{aligned}\right.$$

Dalle precedenti seguono:

1) $\forall x \in \mathbb{Q} \;|\; x \geq 0 \implies -x \leq 0$, 

   $\forall x, y \in \mathbb{Q} \;|\; x \geq y \implies -x \leq y$

2) $\forall x \in \mathbb{Q} \;|\; x > 0 \implies x^{-1} > 0$, 

   $\forall x, y \in \mathbb{Q} \;|\; x \geq y > 0 \implies 0 < x^{-1} \leq y^{-1}$

3) $\forall x,y,z \in \mathbb{Q} \;|\; x \leq y \land z \leq 0 \implies xz > yz$
4) $\forall x \in \mathbb{Q} \;|\; x^{2} > 0$

> [!info] Ordinamento totale
> L'ordinamento di dice **totale** quando <u>tutti</u> gli elementi del campo sono confrontabili e quindi ordinabili.

#### Rappresentazione grafica insiemi numerici

$\mathbb{N}$:

![](https://i.imgur.com/RkcjDJq.png)

$\mathbb{Z}$:

![](https://i.imgur.com/OCnPl9G.png)

$\mathbb{Q}$:

![](https://i.imgur.com/3pEV3em.png)

Se si provano a rappresentare solo i numeri tra 0 e 1 si nota come si può trovare sempre un valore intermedio tra 2 valori scelti.

Perciò $\mathbb{Q}$ si dice che sia ***denso*** in quanto: $\;\forall x,y \in \mathbb{Q} \;|\; \exists n \implies x < n < y\;$ (tra 2 numeri razionali ne esistono infiniti tra essi).

### Numeri reali

I numeri reali (insieme $\mathbb{R}$) sono in corrispondenza biunivoca con i punti della retta orientata in quanto corrispondono a: $\mathbb{Q} \cup \mathbb{I}$ (unione tra razionali e irrazionali).

... 0,9 periodico = 1 ...

###### Intervalli

Per indicare degli intervalli si usano parentesi tonde e quadre contenenti 2 **estremi**:

$$\left.\begin{aligned}
(a,b) &= \{ x \in \mathbb{R} \;|\; a < x < b \} \\
[a,b] &= \{ x \in \mathbb{R} \;|\; a \leq x \leq b \}
\end{aligned}\right.$$

Se un estremo è $+\infty$ o $-\infty$, la sua parentesi può essere solo tonda.

###### Maggiorante e minorante

Dato un insieme non vuoto $A \subseteq \mathbb{R}$, un numero $n \in \mathbb{R}$ si dice:

- **Maggiorante** di $A$ se $\forall x \in A \implies n \geq x$ (numero che è maggiore di tutti i numeri in $A$),
- **Minorante** di $A$ se $\forall x \in A \implies n \leq x$ (numero che è minore di tutti i numeri in $A$).

> [!info] Nota
> Tendendo all'infinito, possono esistere <u>infiniti maggioranti e minoranti</u> di $A$.
> ![](https://i.imgur.com/KmMDeFo.png)
> Inoltre, si indicano:
> - $A^{*} =$ l'insieme dei maggioranti di $A$,
> - $A_{*} =$ l'insieme dei minoranti di $A$.

###### Limiti

In base a maggioranti e minoranti, si dice che:

- $A$ è **limitato superiormente** se <u>ammette almeno 1 maggiorante</u>,
- $A$ è **limitato inferiormente** se <u>ammette almeno 1 minorante</u>,
- $A$ è **limitato** se si verificano entrambe le precedenti.

> [!example] Esempio
> Usando le parentesi <u>quadre</u> per definire un intervallo di un insieme, gli estremi fanno parte dei maggioranti/minoranti; mentre con le <u>tonde</u> no. Prendendo per esempio l'intervallo $(-\infty,3)$, l'insieme dei suoi maggioranti sarà $[3,+\infty)$ mentre quello dei suoi minoranti sarà: $\emptyset$
> ![](https://i.imgur.com/rVGWMQy.png) 

###### Massimo e minimo

Per i [[#Limiti|limiti]] suddetti:

- Se $n$ è un <u>maggiorante</u> di $A$ incluso nello stesso, allora si dice **massimo** di $A$,
- Se $n$ è un <u>minorante</u> di $A$ incluso nello stesso, allora si dice **minimo** di $A$.

> [!info] Nota
> Massimi e minimi sono **unici** negli insiemi dato che in essi solo 1 maggiorante/minorante può essere maggiore/minore degli altri.
> Gli unici casi in cui ci sono più massimi/minimi è quando tali sono lo <u>stesso numero</u> (segue dimostrazione per assurdo con 2 numeri generici $m_{1}$ e $m_{2}$):
> ![](https://i.imgur.com/IfmPgHn.png)

###### Estremi

Dato un insieme non vuoto $A \subseteq \mathbb{R}$, se $A$ è <u>limitato</u>:

- Si dice **estremo superiore** ($sup(A)$) il <u>più piccolo maggiorante</u> di $A$,
- Si dice **estremo inferiore** ($inf(A)$) il <u>più grande minorante</u> di $A$.

> [!info] Nota
> Per quanto riguarda gli estremi:
> - Se $sup(A) \in A \implies sup(A) = max(A)$,
> - Se $inf(A) \in A \implies inf(A) = min(A)$.

##### Teorema di completezza di ${} \mathbb{R}$

Se $A \subset \mathbb{R}$ (e $A \neq \emptyset$), allora se $A$ è:

- Limitato superiormente $\implies \exists \; sup(A)$,
- Limitato inferiormente $\implies \exists \; inf(A)$,

# Esercizi

##### 1) Esercizi su insiemi

![](https://i.imgur.com/9CzTv84.png)

##### 2) Esercizi su numeri reali

![](https://i.imgur.com/DnZAPiu.png)

# Soluzioni

##### 1)

##### 2)

---

Prossima lezione: [[2 - Radici e potenze]]

