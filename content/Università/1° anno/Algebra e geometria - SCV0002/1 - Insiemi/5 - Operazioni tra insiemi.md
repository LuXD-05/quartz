# Lezione 5

### Operazioni tra insiemi

##### Unione

Abbiamo 2 insiemi $A$ e $B$; l'**unione** (detta anche *disgiunzione*) permette di ottenere tutti gli elementi che compaiono in $A$ o in $B$ 1 sola volta e corrisponde all'operazione di **OR logico**:

$$A \cup B$$

![](https://i.imgur.com/9J6jEud.png)

###### Esempio unione

$$A = \{ 1, 2, 3 \}, \;\; B = \{ 2, 3, 4 \} \;\; \rightarrow \;\; A \cup B = \{ 1, 2, 3, 4 \}$$

###### Proprietà dell'unione

$A \cup \emptyset = A$

$A \cup B = B \cup A$

> [!important] Regola
> Dato che l'unione prende gli <u>elementi di entrambi gli insiemi non ripetendoli</u>, essa **non potrà mai avere più elementi della somma tra gli elementi di $A$ e $B$**:
> $$|A \cup B| \leq |A| + |B|$$

###### Unione tra insiemi delle parti

Supponiamo (ancora) di avere 2 insiemi: $A = \{a,b\}, \; B = \{b,c\}$; adesso:

$|A| = 2 \;\rightarrow\; |P(A)| = 2^{|A|} = 2^{2} = 4$

$|B| = 2 \;\rightarrow\; |P(B)| = 2^{|B|} = 2^{2} = 4$

(fatto fino a qui, integrare)

$P(A) = \{ \emptyset, \{a\}, \{b\}, \{a,b\} \}$

$P(B) = \{ \emptyset, \{b\}, \{c\}, \{b,c\} \}$

##### Intersezione 

Riprendendo i 2 insiemi precedenti $A$ e $B$, l'**intersezione** (detta anche *congiunzione*) permette di ottenere tutti gli elementi che compaiono sia in $A$ sia in $B$ e corrisponde all'operazione di **AND logico**:

$$A \cap B$$

![](https://i.imgur.com/YbAz4tf.png)

###### Esempio intersezione

$$A = \{ 1, 2, 3 \}, \;\; B = \{ 2, 3, 4 \} \;\; \rightarrow \;\; A \cap B = \{ 2, 3 \}$$

> [!important] Regola
> Dato che l'intersezione prende solo gli elementi in comune tra 2 insiemi, essa non potrà mai avere più elementi né di $A$ e né di $B$:
> $$|A \cap B| \leq |A| \;\;\;\; |A \cap B| \leq |B|$$

###### Proprietà dell'intersezione

$A \cap \emptyset = \emptyset$

$A \cap B = B \cap A$

Se $A \cap B = \emptyset \;\rightarrow\;$ ($A$ e $B$ si dicono *disgiunti*).

Se $A \subseteq B \;\rightarrow\; A \cap B = A$ e viceversa.

###### Intersezione tra insiemi delle parti

Supponiamo di avere 2 insiemi: $A = \{a,b\}, \; B = \{b,c\}$; adesso:

$P(A) = \{ \emptyset, \{a\}, \{b\}, \{a,b\} \}$

$P(B) = \{ \emptyset, \{b\}, \{c\}, \{b,c\} \}$

Dato che:

$P(A \cap B) = \{ \emptyset, \{b\} \}$

$P(A) \cap P(B) = \{ \emptyset, \{b\} \}$

Allora:

$$P(A \cap B) = P(A) \cap P(B)$$

###### Principio di inclusione-esclusione

(Detto anche *principio di addizione-sottrazione*), sancisce che la **cardinalità** dell'**unione** tra 2 insiemi (ovvero il n° di elementi in $A$ e $B$ non ripetuti) corrisponderà alla **somma** tra le cardinalità dei 2 insiemi meno la loro **intersezione** (ovvero il n° di singoli elementi ripetuti in $A$ e $B$):

$$|A \cup B| = |A| + |B| - |A \cap B|$$

##### Differenza

Sempre tenendo da conto i 2 insiemi di prima ($A$ e $B$), l'insieme **differenza** (o **complemento relativo**) fra i 2 è l'insieme degli elementi di $A$ che <u>non appartengono</u> a $B$:

$$A - B$$(in realtà si scrive A\\B, ma LaTeX non fa scrivere "\\")

![](https://i.imgur.com/BngP6Fj.png)

###### Proprietà della differenza

$A - B \neq B - A$

$A - (A \cap B) = A - B$ e viceversa

##### Complemento assoluto

Dal concetto di **insieme universo** ($U$) si sa che qualunque operazione tra insiemi si svolge e risulta in qualcosa all'interno di esso. 

Perciò, considerando un insieme $A$ e $U$, se $A \subseteq U$, allora viene definito **complemento assoluto** l'insieme differenza tra $U$ e $A$ (semplificabile descrivendolo come "<u>tutto ciò che non appartiene ad A</u>"); ed è definito così:

$$\overline{A} = U - A$$

![](https://i.imgur.com/zGoFvwL.png)

###### Proprietà complemento assoluto

$A \cap B = \emptyset \;\rightarrow\; A - B = A$

$A - (A \cap B) = A - B$ e viceversa

##### Prodotto cartesiano

Prima di definire il prodotto cartesiano, è necessario approfondire il concetto di **coppia** di elementi:

> [!important] Coppia
> Una **coppia** di elementi (di un insieme $A$) è così denotata:
> $(a,b) := \{ a, \{ a, b \} \}$
> Dato ciò, la coppia $(a,b)$ è diversa dalla coppia $(b,a)$, in quanto nelle coppie si fissa e diventa importante l'<u>ordine degli elementi</u>, perciò:
> $(a,b) := \{ a, \{ a, b \} \} \;\; \neq \;\; (b,a) := \{ b, \{ a, b \} \}$ (mentre tra gli insiemi: $\{a,b\} = \{b,a\}$).

Dati 2 insiemi $A$ e $B$, il **prodotto cartesiano** è l'insieme di tutte le coppie che hanno come 1a componente (elemento della coppia) in $A$ e come 2a componente in $B$, e si scrive così:

$$A \times B = \{ (x,y) \;|\; x \in A,\, x \in B \}$$

Dall'esempio si può anche dire che il prodotto cartesiano è l'insieme delle coppie (quindi distinte e con un ordine preciso) composte da 2 componenti $x$ e $y$ in cui $x$ è un elemento di $A$ e $y$ è un elemento di $B$.

###### Esempio prodotto cartesiano

$A = \{a,b\}, \;\;\rightarrow\;\; A = \{1,2\}$

$A \times B = \{(a,1),(a,2),(b,1),(b,2)\}$

$B \times A = \{(1,a),(1,b),(2,a),(2,b)\}$

###### Proprietà del prodotto cartesiano

Se $A = \emptyset \;\rightarrow\; A \times B = \emptyset \;\rightarrow\; |A \times B| = 0$

$A \times B \neq B \times A\;$ , però $\;|A \times B| = |B \times A|$

$|A \times B| = |A| * |B|$

$|P(A \times B)| = 2^{|A| * |B|}$

# Esercizi 

$|P(A) * B| =$ ?

$|P(A \times P(B))| =$ ?

$P(A) \times B =$ ?

# Soluzioni

---

Prossima lezione: [[6 - Definizione e rappresentazioni]]

