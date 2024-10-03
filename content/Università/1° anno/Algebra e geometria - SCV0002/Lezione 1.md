# Insiemi

### Definizioni

> [!important] Insieme
> Collezione di oggetti. Sono indicati con lettere maiuscole (al contrario dei propri elementi, indicati con lettere minuscole).
> Un insieme può essere: 
> - **Finito**: se i suoi elementi sono contabili e se il loro n° non è infinito,
> - **Infinito**: se i suoi elementi non sono contabili perché il loro n° è infinito.

> [!important] Singleton
> Si dice ***singleton*** un insieme composto da 1 solo elemento.

> [!important] Insieme vuoto
> Si dice **insieme vuoto** un insieme senza elementi; e si rappresenta con ${} \emptyset {}$ o $\{\;\}$

> [!important] Insiemi numerici
> $\mathbb{N}$ = insieme dei numeri **naturali** ${} \{ 0, 1, 2, 3 ... \} {}$
> $\mathbb{Z}$ = insieme dei numeri **interi relativi** ${} \{ ... -1, 0, 1 ... \} {}$
> $\mathbb{Q}$ = insieme dei numeri **razionali** $\{ \frac{n}{m} | m \neq n,m \in \mathbb{Z} \}$
> $\mathbb{R}$ = insieme dei numeri **reali** $Q \cup \{ x con espansione decimale infinita non periodica \}$
> Quindi: $\{\; \mathbb{N} \subseteq \mathbb{Z} \subseteq \mathbb{Q} \subseteq \mathbb{R} \;\}$

Se N è **discreto** (ogni numero ha un successore) come anche Z, Q invece è **denso**, ovvero non c'è un successore per ogni numero, infatti tra uno e il suo prossimo esistono in mezzo infiniti numeri.

> [!important] Cardinalità (o ordine)
> La **cardinalità** di un insieme finito di elementi è il n° di elementi dello stesso e si indica con $|A|$. Inoltre:
> $|\emptyset| = 0$
> $|singleton| = 1$
> $A \subseteq B \rightarrow |A| \leq |B|$ 

> [!important] Insieme universo
> L'insieme universo ($U$) è un insieme "teorico" (come $\emptyset$) che contiene qualunque altro insieme. In pratica qualunque insieme venga definito in un qualsiasi contesto è un sottoinsieme di questo.

#### Proprietà

> 1) Non è importante in che ordine sono disposti gli elementi di un insieme:
>    $A = \{ a, b \} \rightarrow A = \{ b, a \}$ 
> 2) Solo i singoli elementi contano, le ripetizioni non sono importanti:
>    $A = \{ a,a,b \} \rightarrow A = \{ a,b \}$

### Appartenenza

Introduciamo il concetto di appartenenza di un elemento ad un insieme: $x \in A$; con:

- $x$: **elemento** generico,
- $\in$: "**appartiene**" (indica che ciò che c'è prima si trova in ciò che c'è dopo),
- $A$: **insieme** generico.

Per dire che un elemento non appartiene ad un insieme si dice invece: $x \not\in A$.

### Notazioni

##### Notazione estensionale

Questo tipo di notazione (detta anche per elencazione) consiste nell'elencare tutti (e soli) gli elementi dell'insieme scrivendoli tra { ... } e separati da ",".

Per esempio, un insieme $A$ composto da 4 elementi: $a, b, c, d$ è così rappresentato:

$$A = \{ a, b, c, d \}$$

Tale notazione è ottima al fine di rappresentare **insiemi piccoli** e **finiti**.

##### Notazione intensionale

Molti insiemi però, non sono rappresentabili con la precedente notazione (per ovvi motivi di grandezza eccessiva); perciò si rappresentano per mezzo di **proprietà**, ad esempio:

$$A = \{\; x \;|\; x \;è\; pari \;\}$$

che si legge "insieme $A$ di <u>x tale che x</u> (*x | x*) è pari"; e che è come scrivere:

$$A = \{ 0, 2, 4, \ldots \}$$

(L'insieme dei numeri pari corrisponde a $2\mathbb{N}$, mentre l'insieme dei numeri dispari corrisponde a $2\mathbb{N} + 1$; e ciò vale anche per $\mathbb{Z}$).

###### Notazioni più avanzate

Supponiamo di avere ora un insieme $B$ con dentro delle persone ($B = \{\; Mario,\; \ldots \;\}$)

E indichiamo $C$ come $C = \{\; x \in B \;|\; x \;è\; simpatico \;\}$

Questa è una notazione astratta, che però aiuta a comprendere il seguente concetto:

$$C = \{\; x \in B \;|\; f(x) \;\}$$

Dire "*x è simpatico*" non è una condizione immediatamente verificabile, però permette di capire quali elementi fanno parte di $C$, ovvero quelli che rispettano la proprietà $f(x)$ (o $P(x)$).

### Contenimento

Introduciamo ora il concetto di **contenimento**: quando tutti gli elementi di un insieme $A$ sono presenti anche in un altro $B$ (il quale ha altri elementi) si dice che il $A$ è contenuto/incluso in $B$ (o che $A$ è un sottoinsieme di $B$) e si indica così:

$$A \subseteq B$$

Quindi per ogni $x$ che appartiene ad $A$, $x$ appartiene (anche) a $B$, oppure:

$$\forall x \in A \rightarrow x \in B$$

###### Esempio

$$A = \{a,b\},\; B = \{a,b,c\} \; \rightarrow \; A \subseteq B$$

##### Sottoinsiemi propri e impropri

Dato un insieme $A$, l'**insieme vuoto** e l'**insieme $A$ stesso** sono comunque <u>sottoinsiemi di A</u> e si dicono **sottoinsiemi impropri**, mentre tutti gli altri sottoinsiemi di A si dicono **sottoinsiemi propri**.

##### Insiemi innestati

Si consideri l'insieme $A = \{ gao, \{a, b\}, 1 \}$

Si deduce subito che $\{a,b\} \subseteq A$; però $|A| = 3$ in quanto quell'insieme è considerato come un elemento.

Si potrebbe fare un'analogia con delle scatole, considerando $A$ come uno scatolone che contiene gli elementi $gao$, $1$ e un'altra scatola più piccola, la quale a sua volta contiene $a$ e $b$.

##### Insieme delle parti

L'**insieme delle parti** (o *powerset*) di un insieme $A$ è l'<u>insieme di tutti (e soli) i sottoinsiemi di A</u> e si rappresenta con $P(A)$. Dato quanto detto [[#Sottoinsiemi propri e impropri|qui]], si ha:

$$\emptyset \in P(A), \;\; A \in P(A)$$

###### Esempio

Con $A = \{ 1, 2, 3 \}$, i sottoinsiemi di $A$ sono:

- $\emptyset$ con 0 elementi,
- $\{1\}, \{2\}, \{3\}$ con 1 elemento,
- $\{1,2\}, \{2,3\}, \{1,3\}$ con 2 elementi,
- $\{1,2,3\} = A$ con 3 elementi.

> [!important] Regola
> Se un insieme $A$ ha $n$ elementi, allora ${} A$ ha $2^{n}$ sottoinsiemi.
> In altre parole, se $|A| = n \;\rightarrow\; |P(A)| = 2^{n}$

### Diagrammi di Venn

Dato un insieme $S = \{\; Mario, 3, \pi, * \;\}$, è possibile definirlo con un diagramma di Venn:

![](https://i.imgur.com/aJds3Vv.png)

Per quanto riguarda il contenimento di insiemi, tali sono anch'essi rappresentabili con i diagrammi di Venn:

![](https://i.imgur.com/YJ0qr12.png)

### Operazioni tra insiemi

##### Unione

Abbiamo 2 insiemi $A$ e $B$; l'**unione** (detta anche *disgiunzione*) permette di ottenere tutti gli elementi che compaiono in $A$ o in $B$ 1 sola volta e corrisponde all'operazione di **OR logico**:

$$A \cup B$$

![](https://i.imgur.com/9J6jEud.png)

###### Esempio

$$A = \{ 1, 2, 3 \}, \;\; B = \{ 2, 3, 4 \} \;\; \rightarrow \;\; A \cup B = \{ 1, 2, 3, 4 \}$$

> [!important] Regola
> Dato che l'unione prende gli elementi di entrambi gli insiemi non ripetendoli, essa non potrà mai avere più elementi della somma tra gli elementi di $A$ e $B$:
> $$|A \cup B| \leq |A| + |B|$$

###### Proprietà dell'unione

$A \cup \emptyset = A$

$A \cup B = B \cup A$

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

###### Esempio

$$A = \{ 1, 2, 3 \}, \;\; B = \{ 2, 3, 4 \} \;\; \rightarrow \;\; A \cap B = \{ 2, 3 \}$$

> [!important] Regola
> Dato che l'intersezione prende solo gli elementi in comune tra 2 insiemi, essa non potrà mai avere più elementi né di $A$ e né di $B$:
> $$|A \cap B| \leq |A| \;\;\;\; |A \cap B| \leq |B|$$

###### Proprietà dell'intersezione

$A \cap \emptyset = \emptyset$

$A \cap B = B \cap A$

$A \cap B = \emptyset \;\rightarrow\;$ ($A$ e $B$ si dicono *disgiunti*).

Se $A \subseteq B \;\rightarrow\; A \cap B = A$ e viceversa.

###### Intersezione tra insiemi delle parti

Supponiamo di avere 2 insiemi: $A = \{a,b\}, \; B = \{b,c\}$; adesso:

$P(A) = \{ \emptyset, \{a\}, \{b\}, \{a,b\} \}$

$P(B) = \{ \emptyset, \{b\}, \{c\}, \{b,c\} \}$

Dato che:

$A \cap B = \{ \emptyset, \{b\} \}$

$P(A) \cap P(B) = \{ \emptyset, \{\emptyset\}, \{b\}, \{\emptyset,b\} \}$

Allora:

$$P(A \cap B) = P(A) \cap P(B)$$

###### Principio di inclusione-esclusione

(Detto anche principio di somma e sottrazione), ...

$$|A \cup B| = |A| + |B| - |A \cap B|$$

##### Differenza

Sempre coi 2 insiemi di prima, l'insieme **differenza** (o **complemento relativo**) fra i 2 ($A$ e $B$) è l'insieme degli elementi di $A$ che non appartengono a $B$:

$$A - B$$   (in realtà si scrive A\\B, ma LaTeX non fa scrivere "\\")

![](https://i.imgur.com/BngP6Fj.png)

##### Complemento assoluto

Dal concetto di **insieme universo** ($U$) si sa che qualunque operazione tra insiemi si svolge e risulta in qualcosa all'interno di esso. 

Perciò se $A \subseteq U$, allora viene definito **complemento assoluto** l'insieme differenza tra $U$ e $A$ (semplificabile descrivendolo come "tutto ciò che non appartiene ad $A$"); ed è definito così:

$$\overline{A} = U - A$$

![](https://i.imgur.com/zGoFvwL.png)

###### Proprietà

$A \cap B = \emptyset \;\rightarrow\; A - B = A$

$A - (A \cap B) = A - B$ (anche se $A \cap B = \emptyset$)

$A - B \subseteq A \;\rightarrow\; A - (A \cap B) = A - B$ ???$

##### Prodotto cartesiano

Prima di definire il prodotto cartesiano, è necessario approfondire il concetto di **coppia** di elementi:

> [!important] Coppia
> Una coppia di elementi (di un insieme $A$) è così denotata:
> $(a,b) := \{ a, \{ a, b \} \}$
> Dato ciò, la coppia $(a,b)$ è diversa dalla coppia $(b,a)$, in quanto nelle coppie si fissa e diventa importante l'<u>ordine degli elementi</u>, perciò:
> $(a,b) := \{ a, \{ a, b \} \} \;\; \neq \;\; (b,a) := \{ b, \{ a, b \} \}$
> Tra le coppie: $(a,b) \neq (b,a)$, mentre tra gli insiemi: $\{a,b\} = \{b,a\}$

Dati 2 insiemi $A$ e $B$, il **prodotto cartesiano** è l'insieme di tutte le coppie che hanno come 1a componente (elemento della coppia) in $A$ e come 2a componente in $B$, e si scrive così:

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

