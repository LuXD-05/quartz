# Lezione 8

### Classi di equivalenza

> [!important] Classe di equivalenza
> Se $R$ è una relazione di equivalenza su $A$, si dice **classe di equivalenza di $x \in A$ modulo $R$** <u>l'insieme degli elementi di A in relazione con x</u>, ovvero:
> $$[x]_{R} = \{y \in A \;|\; xRy\}$$
> Quindi: $$[x]_{R} \subseteq A$$
> Semplicemente, la **classe di equivalenza** di un elemento corrisponde all'<u>insieme di tutti gli elementi in relazione con l'elemento stesso</u> (sia raggiunti e sia che raggiungono), quindi agli oggetti con una stessa proprietà.

###### Esempio classi di equivalenza

$A = \{(a,a),(b,b),(c,c),(d,d),(a,b),(b,a),(a,c),(c,a),(b,c),(c,b)\}$

La classe di equivalenza di $a$ (che corrisponde a quelle di $b$ e $c$) è: 

$$[a]_{R} = \{y \in A \;|\; aRy \} = \{a,b,c\}$$

Dato che $a$ è in relazione con se stessa, con $b$ e con $c$, ma non con ${} d$.

###### Proprietà classi di equivalenza

- Ogni classe di equivalenza è sempre $\neq \emptyset$,
- $[a] = [b]$ se $aRb$,
- $[a] \neq [b]$ se $[a] \cap [b] = \emptyset$,

Se $y \in [x]_{R} \;\rightarrow\;$

$...$

### Insieme quoziente

> [!important] Insieme quoziente
> Data la relazione di equivalenza $R$ su $A$, l'**insieme quoziente** è l'<u>insieme di tutte le classi di equivalenza dei suoi elementi</u>:
> $$\frac{A}{R} = \{[x]_{R} \;|\; x \in A\}$$
> Questo insieme comprende tutte le classi di equivalenza ma **non duplicate** (se $[a]_{R} = [b]_{R}$ allora $\frac{A}{R}$ conterrà solo $[a]_R$).

###### Proprietà

1) $\forall x \in A \;\rightarrow\; x \in [x]_{R}$ (R riflessiva)
2) Se $xRy \;\rightarrow\; [x]_{R} = [y]_{R}$ (stessa classe di equivalenza)
3) Se $x \not R y \;\rightarrow\; [x]_{R} \;e\; [y]_{R}$ sono disgiunte (diverse classi di equivalenza)

##### Classi di resto

Le **classi di resto** sono delle particolari classi di equivalenza, tipo $[x]_{y}$, in cui

- ${} x$ è il **resto**,
- $y$ è il **divisore**.

Per esempio, le classi di resto di $\mathbb{Z}_{4} = \{[0]_{4}, [1]_{4}, [2]_{4}, [3]_{4}\}$.

#### Esempi

###### Esempio classi di equivalenza 1

Esempio studenti:

$A = \{$ studenti in aula $\}$

$R = \{ (x,y) \in A \times A \;|$ x e y hanno lo stesso colore di capelli $\}$

- Riflessiva? Si (ognuno ha lo stesso colore di capelli di se stesso)
- Simmetrica? Si (se 1° ha i capelli di un 2°, il 2° stesso ha gli stessi capelli del 1°).
- Transitiva? Si (se un 1° ha un colore di capelli = a quello di un 2° e il 2° = col 3° allora anche il 3° col 1°).

Quindi è una **relazione di equivalenza**.

Data la classe di equivalenza: $[mario]_{R} = \{ x \in A \;|$ x ha lo stesso colore di capelli di mario $\}$, se si prendono tutte le classi di equivalenza per tutti gli elementi (studenti) dell'insieme (aula) ecco che si ottiene l'insieme quoziente:

$\frac{A}{R} =$ biondi, castani ...

###### Esempio classi di equivalenza 2

Esempio multipli di 4:

$R_{4}= \{(x,y) \in \mathbb{Z} \times \mathbb{Z} \;|\; x - y \;\%\; 4 = 0\}$ è di equivalenza; classi di equivalenza:

Per ogni $x \in \mathbb{Z}$ si scrive $[x]_{R_{4}}$, ma in realtà si usa la notazione $[x]_{4}$, detta "**classe di ${} x$ modulo 4**".

$[0]_{4} = \{x \in \mathbb{Z} \;|\; 0 R_{4} x\} = \{x \in \mathbb{Z} \;|\; 0 - x \;\%\; 4 = 0\} = \{0, 4, -4, 8, -8 ...\} \;\rightarrow\; \{4k \;|\; k \in \mathbb{Z}\} =$ multipli di 4 $\rightarrow\; [0]_{4} = [4]_{4}...$

$[1]_{4} = \{x \in \mathbb{Z} \;|\; x R_{4} 1\} = \{x \in \mathbb{Z} \;|\; x - 1 \;\%\; 4 = 0\} = \{1, 5, -3, 7 ...\} \;\rightarrow\; \{4k + 1 \;|\; k \in \mathbb{Z}\}$

...

$$\frac{\mathbb{Z}}{R_{4}} = \{[x]_{4} \;|\; x \in \mathbb{Z}\} = \{[0]_{4}, [1]_{4}, [2]_{4}, [3]_{4}\}$$

E si scrive quindi $\mathbb{Z}_{4} =$ insieme delle classi di resto modulo 4.

###### Esempio insieme quoziente

$R_{2}= \{(x,y) \in \mathbb{Z} \;|\; x-y \;\%\; 2 = 0\}$

$R_{2}$ (come precedente $R_{4}$) è una relazione di equivalenza; perciò esistono:

- La classe di equivalenza per i numeri pari (che vale per tutti i numeri pari): 

  $[0]_{2} = \{x \in \mathbb{Z} \;|\; 0R_{2}x\} = \{x \in \mathbb{Z} \;|\; 0 - x \;\%\; 2 = 0\}$

- La classe di equivalenza dei numeri dispari (che vale sempre per tutti i dispari):

  $[1]_{2} = \{x \in \mathbb{Z} \;|\; 0R_{2}x\} = \{x \in \mathbb{Z} \;|\; 0 - x \;\%\; 2 \ne 0\}$

Quindi l'insieme quoziente:

$2$/$R_{2} = \mathbb{Z}_{2} = \{[0]_{2},[1]_{2}\}$

(confrontandolo con:)

$4$/$R_{4} = \mathbb{Z}_{4} = \{[0]_{4},[1]_{4},[2]_{4},[3]_{4}\}$

per definire le classi di resto:

In $\mathbb{Z}_{2}$ si hanno 2 classi di resto: quella dei numeri con resto 0 (pari) nella divisione per 2 e quella dei numeri con resto 1 (dispari) nella divisione per 2.

In $\mathbb{Z}_{4}$ se ne hanno 4 (di seguito con ${} k \in \mathbb{Z}$):

- Resto 0: $n = 4k + 0$ (multipli di 4),
- Resto 1: $n = 4k + 1$,
- Resto 2: $n = 4k + 2$,
- Resto 3: $n = 4k + 3$.

E queste sono classi di resto che sono **disgiunte**.

Classi di resto che hanno sempre resto $n$.

$|Z_{n}| = n$

$Z_{1} = \{Z\}$

# Esercizi

# Soluzioni

---

Prossima lezione: [[9 - Insieme delle parole e partizioni]]

