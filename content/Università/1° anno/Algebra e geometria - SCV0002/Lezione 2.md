### Coppie

Prima di approfondire il concetto di relazione bisogna introdurre quello di **coppia**. Una coppia $(a, b)$ è così denotata:

$(a,b) := \{ a, \{ a, b \} \}$

Dato ciò, la coppia $(a,b)$ è diversa dalla coppia $(b,a)$, in quanto nelle coppie si fissa e diventa importante l'<u>ordine degli elementi</u>, perciò:

$(a,b) := \{ a, \{ a, b \} \} \;\; \neq \;\; (b,a) := \{ b, \{ a, b \} \}$

Tra le coppie: $(a,b) \neq (b,a)$, mentre tra gli insiemi: $\{a,b\} = \{b,a\}$

Dati 2 insiemi $A$ e $B$, il [[2. School/Università/1° anno/Algebra e geometria - SCV0002/Lezione 1#Prodotto cartesiano|prodotto cartesiano]] è l'insieme di tutte le coppie che hanno come 1a componente (elemento della coppia) in $A$ e come 2a componente in $B$, e si scrive così:

$$A \times B = \{ (x,y) \;|\; x \in A,\, x \in B \}$$

Dall'esempio si può anche dire che il prodotto cartesiano è l'insieme delle coppie (quindi distinte e con un ordine preciso) composte da 2 componenti $x$ e $y$ in cui $x$ è un elemento di $A$ e $y$ è un elemento di $B$.

Volete un'analogia con l'informatica? Il prodotto cartesiano si ottiene mettendo insieme gli elementi di 2 array di char (ovviamente in stringa) mediante un doppio ciclo for (2 for innestati).

###### Esempio

$A = \{a,b\}, \;\;\rightarrow\;\; A = \{1,2\}$

$A \times B = \{(a,1),(a,2),(b,1),(b,2)\}$

$B \times A = \{(1,a),(1,b),(2,a),(2,b)\}$

Quindi: 

$A \times B \neq B \times A\;$ , però $\;|A \times B| = |B \times A|$

###### Proprietà

Se $A = \emptyset \;\rightarrow\; A \times B = \emptyset \;\rightarrow\; |A \times B| = 0$

$|A \times B| = |A| * |B|$

$|P(A \times B)| = 2^{|A| * |B|}$

###### Esercizi

$|P(A) * B| =$ ?

$|P(A \times P(B))| =$ ?

$P(A) \times B =$ ?

### Relazioni

> [!important] Relazione
> Una relazione tra $A$ e $B$ è un sottoinsieme del prodotto cartesiano $A \times B$.

Esempi di relazioni identificate da $R$ (dove ${} R \subseteq A \times B$) tra $A = \{a,b,c\}$ e $B = \{1,2,3\}$ sono:

$a$

...

##### Numero di relazioni tra 2 insiemi

Per trovare il n° di relazioni tra 2 insiemi, bisogna semplicemente contarne i sottoinsiemi del prodotto cartesiano, facendo quindi:

$$|P(A \times B)| = 2^{|A \times B|} = 2^{|A| * |B|}$$

> [!important] Notazione infissa
> Avendo una relazione $R \subseteq A \times B$, se $(a,b) \in R$, allora si dice che $A$ è in relazione con $B$, e si scrive così:
> $$a R b$$

###### Esempio

Supponiamo di avere una relazione tra 2 insiemi di numeri (appartenenti ad $\mathbb{N}$):

$A = B = \mathbb{N}$ e $R \subseteq \mathbb{N} \times \mathbb{N}$

Sarebbe quindi:

$R = \{(0,0), (0,1), ... (1,1) ...\}$

Allora, in notazione infissa si scrive:

$\{(n,m) \;|\; n < m\}$

...

##### Rappresentazione grafica delle relazioni

Se $R \subseteq A \times B$ rappresento $A$ e $B$ con i diagrammi di Venn e poi collego con delle frecce gli elementi di $A$ che sono in relazione con gli elementi di $B$.

Quindi, se $R = \{ (a,1), (b,2), (c,3) \}$, allora:

(diagramma di venn)

##### Matrice di adiacenza

Si scrivono gli elementi di $A$ sulle righe di una tabella e gli elementi di $B$ sulle colonne e dove gli elementi sono in relazione si fa una $\times$ nelle celle.

> [!important] Matrice di adiacenza
> Rappresentazione di una relazione $R \subseteq A \times B$ con una tabella in cui le righe sono etichettate con elementi di $A$ e le colonne con elementi di $B$. 
> In corrispondenza di $(a,b) \in R$ si mette una $\times$ nella cella.

###### Proprietà

Ogni $\times$ che inserisco nella tabella corrisponde a una coppia (o a una freccia nel diagramma di Venn), quindi il n° di $\times$ = cardinalità.

#### Tipi di relazione

##### Relazione binaria

Se $A = B$ e $R \subseteq A \times A$, $R$ è detta **relazione binaria su A**.

(rapp venn)

(rapp matrix)

###### Relazione riflessiva

Una relazione $R$ **binaria** su $A$ è **riflessiva** se:

$$\forall a \in A \;\rightarrow\; aRa \;\; (o\;(a,a) \in R)$$

Quindi se <u>ogni</u> elemento di $A$ è in relazione con se stesso; $R$ non è riflessiva se esiste almeno 1 elemento $(a,a) \not{\in} R$.

(rapp venn)

(rapp matrix)

> [!important] Proprietà ?
> Se $R$ è riflessiva allora $|R| \geq |A|$

> [!important] Proprietà simmetrica
> $R$ è simmetrica se:
> $$\forall x,y \in A \;\rightarrrow\; xRy | yRx$$
> Quindi se le relazioni vanno in "2 direzioni", ovvero esistono, per ogni $x$ e $y$, tutte le coppie $(x,y)$ e $(y,x)$

> [!important] Attenzione
> $R$ è riflessiva se e solo se contiene la diagonale $(D = \{(a,a) \;|\; a \in A\})$.

###### Relazione diagonale (identità)

La relazione diagonale (o identità) tra $A$ e $B$ è:

$$R = \{(1,1),(2,2)(3,3)\}$$

Oppure:

$$R = \{(x,y) \;|\; x = y\}$$

(rapp venn)

(rapp matrix)

> [!important] Attenzione
> La relazione diagonale è sempre anche riflessiva.

###### Relazione totale

La relazione totale è la relazione data da tutte le coppie di $A \times B$.

(rapp venn)

(rapp matrix)

##### Relazione transitiva

R su A è transitiva se:

$\forall x,y,z \in A$ se $xRy$ e $yRz$ allora $xRz$.

Se $xRy$ e $yRz$ ma $x\not{R}z$ allora non è transitiva.

In parole povere, tutti gli elementi che sono relazionati con un altro devono poterlo raggiungere per mezzo di una relazione fatta con tutti gli altri elementi con cui il traguardo è collegato; ciò vale anche quelli relazionati solo con se stessi in quanto:

$aRa, aRa \;\rightarrow\; aRa$ (dimostra che anche le relazioni diagonali sono transitive).

Esempio 1:

$R = \{ (x,y) \in \mathbb{N} \;|\; x \leq y \}$

Riflessiva? Si perché ogni elemento è = a se stesso,

Simmetrica? No, perché 1 < 2 ma 2 > 1,

Transitiva? Si, perché ogni elemento è relazionato con tutti i successivi e con se stesso.

Esempio 2:

$R = \{ (x,y) \in \mathbb{Z} \;|\; x - y \;\% = 0\}$

Riflessiva? Si, $\forall x \in Z \;\rightarrow\; x-x = 0$ che è multiplo di 4.

Simmetrica? Si, $\forall x,y \in Z$ se $x-y \;\% 4 = 0$

...

