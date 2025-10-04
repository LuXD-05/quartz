# Lezione 6

### Relazioni

Per comprendere i seguenti concetti sono fondamentali quelli di [[5 - Operazioni tra insiemi#Prodotto cartesiano|prodotto cartesiano e coppie]].

> [!important] Relazione
> Una **relazione** tra $A$ e $B$ è un **sottoinsieme del prodotto cartesiano** $A \times B$.

Esempi di relazioni identificate da $R$ (dove $R \subseteq A \times B$) tra $A = \{a,b,c\}$ e $B = \{1,2,3\}$ sono:

- $R = \{(a,1),(b,2),(c,3)\}$,
- $R = \emptyset$ (la cosiddetta "***relazione vuota***").

##### Numero di relazioni tra 2 insiemi

Per trovare il **n° di relazioni tra 2 insiemi**, bisogna semplicemente <u>contarne i sottoinsiemi del prodotto cartesiano</u>, facendo quindi:

$$|P(A \times B)| = 2^{|A \times B|} = 2^{|A| * |B|}$$

> [!important] Notazione infissa
> Avendo una relazione $R \subseteq A \times B$, se una coppia qualsiasi $(a,b) \in R$, allora si dice che $A$ è in relazione con $B$, e si scrive così:
> $$a R b$$

###### Esempio

Supponiamo di avere una relazione tra 2 insiemi $\mathbb{N}$ così definita:

$$R = \{ (n,m) \in \mathbb{N} \times \mathbb{N} \;|\; n \leq m \}$$

Ovvero la relazione di "*minore o uguale*" in $\mathbb{N}$, che corrisponde a:

$$R = \{(0,0), (0,1), ... (1,1) ...\}$$

##### Rappresentazione grafica delle relazioni

Se $R \subseteq A \times B$, si possono rappresentare $A$ e $B$ con i [[4 - Diagrammi di Venn|diagrammi di Venn]] e poi collegare con delle frecce gli elementi di $A$ che sono in relazione con quelli di $B$.

Quindi, se abbiamo una $R = \{ (a,1), (b,2), (c,3) \}$, allora:

![](https://i.imgur.com/AbSuvyk.png)

##### Matrice di adiacenza

Si possono rappresentare le relazioni con delle **matrici di adiacenza**, ovvero tabelle in cui:

- Elementi di $A$ sulle righe,
- Elementi di $B$ sulle colonne,
- Delle $\times$ nelle celle dove gli elementi sono in relazione $(a,b)$.

Ogni $\times$ che inserisco nella tabella corrisponde a una coppia (o a una freccia nel diagramma di Venn), quindi il n° di $\times$ = cardinalità.

# Esercizi

# Soluzioni

---

Prossima lezione: [[7 - Tipi di relazione]]

