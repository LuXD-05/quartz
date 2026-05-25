# Lezione 18

### Operazioni

> [!important] Operazione binaria
> Un'**operazione binaria** su $A$ è una funzione ${} A \times A \rightarrow A {}$ in cui:
> - Il dominio è formato da coppie di $A$,
> - Il codominio è $A$.

###### Esempio

Un'esempio è la somma di numeri (operazione binaria su $\mathbb{N}$):

$$+ : \mathbb{N} \times \mathbb{N} \rightarrow \mathbb{N}$$

Che corrisponde (tipo) a: $(n,m) \rightarrow n + m$.

> [!info] Notazione infissa
> Se $* : A \times A \rightarrow A$ è un'operazione, allora si usa la **notazione infissa** e scrive $a * b$ invece di $*(a,b)$ ($a * b \in A$).

##### Proprietà

Se $* : A \times A \rightarrow A$ è un'operazione, $*$ ha delle proprietà:

- $*$ è **commutativa** se $\forall (a,b) \in A \rightarrow a * b = b * a$ (verificabile in tabella affinché ci sia <u>simmetria rispetto alla sua diagonale</u>),
- $*$ è **associativa** se $\forall (a,b,c) \in A \rightarrow a * (b * c) = (a * b) * c = a * b * c$.

###### Elemento neutro

L'operazione $* : A \times A \rightarrow A$ ha **elemento neutro** $x$ se esiste $x \in A$ tale che per ogni $a \in A \rightarrow \; a * x = a \;\land\; x * a = a$.

Si verifica se si trova nella tabella una riga ed una colonna (di uno stesso indice) in cui tutti i valori corrispondono agli indici stessi.

> [!info] Per somme e prodotti
> Rispetto alla somma di numeri interi $\mathbb{Z}$, l'elemento neutro è **0** ($n+0 = n \;\land\; 0+n = n$).
> Rispetto al prodotto invece, l'elemento neutro è **1** ($n*1 = n \;\land\; 1*n = n$).

###### Simmetrizzabilità

Se $(A,*)$ ha l'**elemento neutro** $x$, allora $a \in A$ è **simmetrizzabile** (o *invertibile*) se esiste $a' \in A$ tale che:

- $a * a' = x$
- $a' * a = x$

Quindi $a'$ si dice **simmetrico** (o *inverso*) di $a$.

> [!info] Quindi
> La simmetrizzabilità si riferisce all'<u>indice di riga/colonna</u>.
> Nell'esempio, gli indici $[1]_{4}, [3]_{4}$ sono simmetrizzabili perché nella riga/colonna (simmetrizzabile) compaiono gli indici stessi delle rispettive colonne/righe.

### Strutture algebriche

Una **struttura algebrica** è <u>un'insieme</u> e <u>un'operazione sullo stesso</u> $(A,*)$. 

$(A,*)$ è un **semigruppo** se $*$ è <u>associativa</u>,

$(A,*)$ è un **monoide** se è un <u>semigruppo</u> e ha <u>elemento neutro</u>.

$(A,*)$ è un **gruppo** se è un <u>monoide</u> e <u>ogni elemento è simmetrizzabile</u>

##### Strutture algebriche avanzate

Le seguenti serviranno all'inizio per il corso di analisi.

###### Anello

Sia $A$ un insieme sul quale sono definite le 2 operazioni $+$ e $\cdot$ : $(A,+,\cdot)$ ([[34 - Spazi vettoriali#Spazi vettoriali|spazio vettoriale]]).

###### Campo

# Esercizi

##### Proprietà

###### 1) Esercizio generico 1

$A = \{a,b,c\}, * : A \times A \rightarrow A$, e lo rappresentiamo in tabella:

![](https://i.imgur.com/r3hN3i1.png)

###### 2) Esercizio generico 2

$A = \{a,b,c,d\},\;* : A \times A \rightarrow A,$ in tabella:

![](https://i.imgur.com/qAiSgHo.png)

###### 3) Unione powerset

$A = \{a,b\},\;P(A),\;\cup : P(A) \times P(A) \rightarrow P(A),\,$ quindi:

![](https://i.imgur.com/U3FC4NZ.png)

###### 4) Intersezione powerset

###### 5) Elementi simmetrizzabili in $\mathbb{Z}$ e $\mathbb{Q}$

Esistono elementi simmetrizzabili, rispetto a somma e prodotto, in $\mathbb{Z}$? E in $\mathbb{Q}$?

##### Strutture algebriche

###### 6) Concatenazione

Consideriamo $A^{+}$ come l'insieme delle parole di $A$ e la struttura algebrica di concatenazione in $A^{+}$ è: $\;\;\circ : A^{+} \times A^{+} \rightarrow A^{+}\;\; = \;\;(A^{+},\circ)$.

Che tipo di struttura algebrica è $A^{+}$? E $A^{*} = A^{+} \cup \{\varepsilon\}$ (con $\varepsilon$ = parola vuota di lunghezza 0) invece? $A^{*}$ è o non è simmetrizzabile e perché?

###### 7) Classi di equivalenza in $\mathbb{Z}$

Considera le classi di resto in $\mathbb{Z}_{4}$ e le operazioni "$+$" e "$*$" sempre in esso. Determina se tali operazioni sono gruppi o no.

# Soluzioni

###### 1)

**Commutativa**? No, siccome $b * c \neq c * b$

**Associativa**? Boh (non so cosa "\*" implica)

**Elemento neutro**? $a$

###### 2)

**Commutativa**? Si (esempio) e la tabella è simmetrica,

**Associativa**? Boh (non so cosa "\*" implica)

**Elemento neutro**? $a$, si vede anche dalla tabella che la riga e la colonna in $a$ riproducono gli indici $a,b,c,d$ e $a * (indice\;qualsiasi) = indice$.

###### 3)

**Commutativa**? Si (si vede dalla tabella),

**Associativa**? Si (?)

**Elemento neutro**? $\emptyset$ (si vede dalla tabella).

###### 4)

###### 5)

In $\mathbb{Z}$:

- Somma: ogni elemento è simmetrizzabile ($n + (-n) = 0$),
- Prodotto: solo $1$ è simmetrizzabile (solo $1*1=1$).

In $\mathbb{Q}$:

- Somma: (stessa cosa di $\mathbb{Z}$?),
- Prodotto: ogni elemento è simmetrizzabile ($\frac{n}{m} * \frac{m}{n} = 1$).

###### 6)

Consideriamo $(A^{+},\circ)$ e poi $(A^{*},\circ)$ ($A^{*} = A^{+} \cup \{\varepsilon\}$  o ***epsilon***, supponendo che corrisponda alla parola vuota di lunghezza 0):

- **Commutativa**? No: $\;x \circ y = xy, \; y \circ x = yx\;$ (dato che <u>non è commutativa</u> scrivo $xy$ invece di $x \circ y$)
- **Associativa**? Si: $\;(xy)z = x(yz) = xyz\;$
- **Elemento neutro**? No (però $A^{*}$ si: $\varepsilon$).

Se $(A^{+},\circ)$ è un [[#Strutture algebriche|semigruppo]], allora $(A^{*},\circ)$ è un [[#Strutture algebriche|monoide]] detto ***monoide delle parole***.

$(A^{*},\circ)$ non è un [[#Strutture algebriche|gruppo]] perché, seppure ha l'elemento neutro $\varepsilon$, non esiste nessun $a' \;|\; a \circ a' = \varepsilon \lor a' \circ a = \varepsilon$ (nessun elemento che concatenato ad un altro da $\varepsilon$; sarebbe un gruppo se esistessero parole con lunghezza negativa).

###### 7)

Consideriamo le classi di resto di $\mathbb{Z}_{4} = \{[0]_{4},[1]_{4},[2]_{4},[3]_{4}\}$. Queste sono date da:

- $[0]_{4} = \{4n \;|\; n \in \mathbb{Z}\}$
- $[1]_{4} = \{4n+1 \;|\; n \in \mathbb{Z}\}$
- $[2]_{4} = \{4n+2 \;|\; n \in \mathbb{Z}\}$
- $[3]_{4} = \{4n+3 \;|\; n \in \mathbb{Z}\}$

Definiamo ora le strutture di <u>addizione</u> e <u>moltiplicazione</u>: 

- "${} +$" = $[x]_{n} + [y]_{n} = [x+y]_{n} \;\;\rightarrow\;\; (\mathbb{Z}_{4},+)$,
- "$*$" = $[x]_{n} * [y]_{n} = [x*y]_{n} \;\;\rightarrow\;\; (\mathbb{Z}_{4},*)$.

Quindi abbiamo:

![](https://i.imgur.com/n9QcOex.png)

**Addizione**:

- **Commutativa**? Si, perché $x+y = y+x$,
- **Associativa**? Si, perché $(x+y)+z = x+(y+z) = x+y+z$,
- **Elemento neutro**? $[0]_{4}$ siccome $x + [0]_{4} = [0]_{4} \;\land\;[0]_{4} + x = [0]_{4}$,
- **Simmetrizzabile**? Si, perché $[1]_{4}$ è l'inverso di $[3]_{4}$, mentre $[2]_{4}$ e $[0]_{4}$ sono l'inverso di se stessi.

Perciò ($\mathbb{Z},+$) è un <u>gruppo commutativo</u>.

**Moltiplicazione**:

- **Commutativa**? Si, perché ${} x \cdot y = y \cdot x {}$,
- **Associativa**? Si, perché ${} (x \cdot y) \cdot z = x \cdot (y \cdot z) = x \cdot y \cdot z {}$,
- **Elemento neutro**? $[1]_{4}$ siccome ${} x \cdot [1]_{4} = [1]_{4} \;\land\;[1]_{4} \cdot x = [1]_{4} {}$,
- **Simmetrizzabile**? No, perché (anche se $[1]_{4}$ e $[3]_{4}$ se moltiplicati per se stessi danno $[1]_{4}$) qualsiasi elemento moltiplicato per $[0]_{4}$ o $[2]_{4}$ restituisce (rispettivamente) $[0]_{4}$ o $[2]_{4}$ (e non l'elemento neutro $[1]_{4}$).

Perciò ($\mathbb{Z},\cdot$) <u>non è un gruppo</u>.

---

Prossima lezione: [[19 - Funzione di Eulero]]

