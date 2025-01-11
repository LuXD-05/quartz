# Lezione 20

##### Sottoinsiemi stabili

Le **sottostrutture** di strutture algebriche si basano sul concetto di **stabilità** dei sottoinsiemi:

> [!important] Sottoinsieme stabile
> Un sottoinsieme $B$ di $A$ è **stabile** (rispetto ad un operatore $*$) se per ogni coppia $x,y \in B \;\rightarrow\; x * y \in B$.
> La stabilità si riferisce quindi ad un qualsiasi <u>sottoinsieme</u> di una data struttura.

### Sottostrutture algebriche

Se $B \subseteq A$ è [[#Sottoinsiemi stabili|stabile]] rispetto a $*$, allora $(B,*)$ è una **sottostruttura** di $(A,*)$.

###### Sottomonoide

Se $(A,*)$ è un [[18 - Strutture algebriche#Strutture algebriche|monoide]] e $B \subseteq A$ è <u>stabile</u> e contiene l'<u>elemento neutro</u> di $A$, allora $(B,*)$ è un **sottomonoide**.

###### Sottogruppo

Se $(A,*)$ è un [[18 - Strutture algebriche#Strutture algebriche|gruppo]] e $B \subseteq A$ è stabile e contiene i <u>simmetrici dei suoi elementi</u>, allora $(B,*)$ è un **sottogruppo**.

##### Omomorfismo

Date 2 strutture algebriche $(A_{1},*_{1})$ e $(A_{2},*_{2})$, consideriamo $f : A_{1} \rightarrow A_{2}$; essa si dice **omomorfismo** se:

$$\forall x,y \in A \;\rightarrow\; f(x *_{1} y) = f(x) *_{2} f(y)$$

##### Isomorfismo

Detto anche *omomorfismo biettivo*, è si verifica semplicemente quando sono rispettate le regole per l'omomorfismo, ma la funzione definita è **biettiva** (quindi le tabelle operative delle 2 strutture avranno i propri elementi corrispondenti nelle stesse posizioni).

# Esercizi

##### 1) Esercizi sottoinsiemi stabili

Quali di questi sottoinsiemi sono stabili rispetto alle proprie strutture?

- Data la struttura $(\mathbb{N},+)$, sottoinsieme $2\mathbb{N}$,
- Data la struttura $(\mathbb{N},+)$, sottoinsieme $2\mathbb{N}+1$,
- Data la struttura ${} (\mathbb{Q},\cdot) {}$, sottoinsieme $\mathbb{Q}$,
- Data la struttura ${} (\mathbb{Q},\cdot) {}$, sottoinsieme $\mathbb{Q} - \{0\}$,
- Data la struttura $(A^{*},\circ)$, sottoinsieme $S = \{x \in A^{*} \;|\; x.startsWith('a') \}$,

##### 2) Esercizi omomorfismo

- Determinare se $f : n \in \mathbb{N} \rightarrow 2^{n} \in \mathbb{N}$ è un omomorfismo di $(\mathbb{N},+)$ in ${} (\mathbb{N},\cdot) {}$.
- Determinare se $f : n \in \mathbb{N} \rightarrow \#n \in \mathbb{N}$ è un omomorfismo di $(\mathbb{N},+)$ in $(A^{*},+)$, dove $\#$ = n° di lettere della parola che corrisponde al numero $n$.

##### 3) Esercizi isomorfismo

Determinare se una funzione $f : A \rightarrow \mathbb{Z}_{3}$ (definita di seguito) è un isomorfismo di ${} (A,*) {}$ in $(\mathbb{Z}_{3},\cdot)$?

![](https://i.imgur.com/nPT4yob.png)

# Soluzioni

##### 1)

##### 2)

###### 1) omomorfismo

Per $(\mathbb{N},+)$: $f(n+m) = 2^{n+m}$,

Per $(\mathbb{N},\cdot)$: ${} f(n) \cdot f(m) = 2^{n} \cdot 2^{m} {}$.

${} 2^{n+m} = 2^{n} \cdot 2^{m} \;\rightarrow\; f(n+m) = f(n) \cdot f(m) {}$

Perciò $f$ <u>è un omomorfismo</u> di $(\mathbb{N},+)$ in ${} (\mathbb{N},\cdot) {}$.

###### 2) omomorfismo

Per $(\mathbb{N},+)$: ${} \#(3+5) = \#(8) = 4$,

Per $(A^{*},+)$: $\#(3)+\#(5) = 3 + 6 = 9$.

$4 \neq 9$

Perciò $\#$ <u>non è un omomorfismo</u> di $(\mathbb{N},+)$ in $(A^{*},+)$.

##### 3)

###### 1) isomorfismo

Dati $A = \{a,b,c\}$, $\mathbb{Z}_{3}$ e la funzione $f$ (definita [[#3) Esercizi isomorfismo|qui]]):

![](https://i.imgur.com/xME1zWC.png)

${} f$ già è un omomorfismo in quanto (per esempio) ${} f(b*c) = f(b) \cdot f(c) {}$; in più ogni elemento di $A$ corrisponde a 1 solo elemento di $\mathbb{Z}_{3}$ (biettiva).

Perciò $f$ è un isomorfismo di ${} (A,*) {}$ in $(\mathbb{Z}_{3},\cdot)$.

---

Prossima lezione: [[21 - Matrici]]

