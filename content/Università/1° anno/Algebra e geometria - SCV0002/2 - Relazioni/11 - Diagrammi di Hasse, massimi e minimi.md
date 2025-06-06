# Lezione 11

### Diagrammi di Hasse

I **diagrammi di Hasse** sono un metodo usato per rappresentare **relazioni d'ordine** in maniera più semplificata rispetto ai diagrammi di Venn; infatti per essi si usano delle regole specifiche:

- <u>Non si disegnano le relazioni riflessive</u>,
- <u>Non si disegnano le relazioni ricavabili tramite transitività</u>,
- Gli <u>elementi più piccoli</u> della relazione si scrivono <u>in basso</u>.

> [!important] Copertura
> Data $R$ una **relazione d'ordine** su $A$:
> $y$ "***copre***" $x$ se $xRy$ e NON ci sono elementi $z \in A$ tali che $xRz$ e $zRy$.

##### Rappresentazione

Rappresentiamo la <u>relazione di inclusione</u> su $P(\{a,b,c\})$:

![](https://i.imgur.com/ZZrLj6O.png)

> [!important] Incomparabilità
> 2 elementi $x$ e $y$ (nella foto per esempio $\{a,b\}$ e $\{b,c\}$) si dicono **incomparabili** rispetto ad una relazione d'ordine $R$ se $x \not R y \land y \not R x$.
> Una relazione che <u>non ha elementi incomparabili</u> è **totale**.

###### Esempi diagrammi di Hasse

Abbiamo: $A = \{a,b,c\}, \; B = \{1,2\}, \;\; A \times B = \{\{a,1\}, \{a,2\}, \{b,1\}, \{b,2\}, \{c,1\}, \{c,2\}\}$

Consideriamo: $R = \{(a,a), (b,b), (c,c), (a,b), (b,c), (a,c)\}$

![](https://i.imgur.com/Rnj4dVb.png)

Questo è denotabile come $a < b < c$ ($a < b \land b < c$).

> [!info] Quindi ???
> Definisco una relazione su $A \times B$ così:
> $$(x,y)R(x_{1},y_{1})$ se $x \leq x_{1} \land y \leq y_{1}$$

### Max e min

> [!important] Definizioni per le relazioni d'ordine
> - $x \in A$ è il **massimo** rispetto a $R$ se $\forall y \in A \;\rightarrow\; yRx$ (**elemento più in alto** <u>di tutti</u>, ce n'è 1 oppure nessuno).
> - $x \in A$ è il **minimo** rispetto a $R$ se $\forall y \in A \;\rightarrow\; xRy$ (**elemento più in basso** <u>di tutti</u>, ce n'è 1 oppure nessuno).
> - $x \in A$ è **massimale** rispetto a $R$ se <u>non esiste</u> $y \in A \;|\; xRy$ (elementi più in alto in generale, possono essere 1 o più).
> - $x \in A$ è **minimale** rispetto a $R$ se <u>non esiste</u> $y \in A \;|\; yRx$ (elementi più in basso in generale, possono essere 1 o più).

##### Proprietà max e min

> [!info] Proprietà
> - Se c'è un **massimo** (può essere solo 1) allora è anche **massimale** (quindi se c'è un unico massimale, esso è il massimo).
> - Se c'è un **minimo** (può essere solo 1) allora è anche **minimale** (quindi se c'è un unico minimale, esso è il minimo).

##### Esempi max e min

###### Esempio maxmin 1

Riprendiamo l'esempio dell'<u>inclusione</u>:

![](https://i.imgur.com/ZZrLj6O.png)

- **Minimo**: $\emptyset$, perché è contenuto in tutti gli altri insiemi,
- **Massimo**: $\{a,b,c\}$, perché contiene tutti gli altri insiemi,
- **Minimale**: $\emptyset$, dato che non ci sono insiemi contenuti in esso,
- **Massimale**: $\{a,b,c\}$, dato che non ci sono insiemi che lo contengono.

###### Esempio maxmin 2

$A = \{a,b,c,d,e\}, \;\; R = \{(a,a),(b,b),(c,c),(d,d),(e,e),(a,b),(b,c),(a,c),(a,d),(d,e),(a,e)\}$

![](https://i.imgur.com/kPOCLKH.png)

- Massimo: non esiste
- Massimali: $c,e$ (incomparabili)
- Minimo: $a$
- Minimali: $a$

###### Esempio maxmin 3

In ${} \mathbb{N} {}$, relazione $\leq$:

![](https://i.imgur.com/EdApXYA.png)

- **Minimo** e **minimale** = 0,
- **Massimo** e **massimale** = <u>non esistono</u> (no elementi > di altri dato che tende a $\infty$).

Questa è una <u>relazione totale</u> (detta anche ***catena***), dato che <u>tutti gli elementi sono comparabili</u>.

<u>Non</u> sarebbe una relazione totale quella di **divisibilità** (su $\mathbb{N}$) in quanto (per esempio) 2 e 3 non sarebbero in relazione l'uno con l'altro in nessun caso.

###### Esempio maxmin 4

Relazione divisibilità:

![](https://i.imgur.com/8vh9U6b.png)

- Minimo: non esiste, 
- Massimo: non esiste,
- Minimali: 2, 3, 5
- Massimali: 8, 12, 9, 5

Se la relazione di divisibilità comprendesse tutti gli elementi di $\mathbb{N}$, allora:

- **Minimo** e **minimale** = 1,
- **Massimo** e **massimale** = 0 (divisibile per qualsiasi numero $n$ dato che $\frac{0}{n} = 0$).

###### Esempio maxmin 5

Sull'insieme delle parole, $R \{(x,y) \in (A^{+})^{2} \;|\; \#x \leq \#y\}$:

- Riflessiva? Si ...
- Transitiva? Si ...
- Non è ne simmetrica ne antisimmetrica (quindi nemmeno d'equivalenza o d'ordine) perché ... .

###### Esempio maxmin 6

Sull'insieme delle parole, relazione $R$ dove $x$ è prefisso di $y$:

Innanzitutto, per convenzione ci si prefigge che ogni parola è prefisso di se stessa.

...

$R$ è una relazione d'ordine

# Esercizi

# Soluzioni

---

Prossima lezione: [[12 - Funzioni]]

