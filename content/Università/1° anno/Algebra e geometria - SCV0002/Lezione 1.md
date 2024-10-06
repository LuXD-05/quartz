---
modified_at: 04/10/2024 20:18:10
edited_seconds: 11840
public: true
---
# Insiemi
### Definizioni
Hint: insieme def (fin/inf), singleton, $\emptyset$, insiemi numerici + discreto/denso, cardinalità, insieme universo, proprietà base (2)
::
> [!important] Insieme
> Collezione di oggetti. Sono indicati con lettere maiuscole (al contrario dei propri elementi, indicati con lettere minuscole). Un insieme può essere: 
> - **Finito**: se i suoi elementi sono contabili e se il loro n° non è infinito,
> - **Infinito**: se i suoi elementi non sono contabili perché il loro n° è infinito.
> [!important] Singleton
> Si dice ***singleton*** un insieme composto da 1 solo elemento.
  
> [!important] Insieme vuoto
> Si dice **insieme vuoto** un insieme senza elementi; e si rappresenta con $\emptyset$ o $\{\;\}$
  
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
Hint: appartenenza (def), notazioni (estensionale, intensionale (+ avanzata/astratta)) + considerazione $\mathbb{N}$
::
Si dice che un elemento **appartiene** ad un insieme quando è "dentro" ad esso.
Ciò si descrive con: $x \in A$, dove:
- $x$: **elemento** generico,
- $\in$: "**appartiene**" (indica che ciò che c'è prima si trova in ciò che c'è dopo),
- $A$: **insieme** generico.
Per dire che un elemento <u>non appartiene</u> ad un insieme si scrive invece: $x \not\in A$.
Un'analogia di esempio consiste nel considerare l'insieme come una <u>scatola</u>, mentre gli elementi che vi appartengono come degli <u>oggetti</u> all'interno della stessa.
> [!info] Attenzione
> L'appartenenza è ***diretta***. Consideriamo l'insieme $A = \{a,\{b,c\}\}$, allora:
> - Corretto: $a \in A$
> - Errato: $b \in A$
### Notazioni
##### Notazione estensionale
La **notazione estensionale** (detta anche <u>per elencazione</u>) consiste nell'<u>elencare tutti (e soli) gli elementi dell'insieme scrivendoli tra "{ }" e separandoli con ","</u>.
Per esempio, un insieme $A$ composto da 4 elementi: $a,b,c,d$ è così rappresentato:
$$A = \{ a,b,c,d \}$$
Tale notazione è ottima al fine di rappresentare **insiemi piccoli** e **finiti**.
##### Notazione intensionale
Degli insiemi però, non sono rappresentabili con la notazione estensionale (per ovvi motivi di grandezza eccessiva o infinita); perciò si rappresentano per mezzo di **proprietà** e con quella che è detta **notazione intensionale**, ad esempio:
$$A = \{\; x \;|\; x \;è\; pari \;\}$$
Che si legge "insieme $A$ di <u>x tale che x</u> (*x | x*) è pari" ("è pari" = <u>proprietà</u>); e che è come scrivere:
$$A = \{ 0, 2, 4, \ldots \}$$
> [!info] Considerazione
> $2\mathbb{N}$ corrisponde all'insieme dei numeri pari,
> $2\mathbb{N} + 1$ corrisponde all'insieme dei numeri dispari.
> (Ciò vale anche per $\mathbb{Z}$).
###### Notazioni più avanzate
Supponiamo di avere ora un insieme $P$ con dentro delle persone ($P = \{\; Mario,\; \ldots \;\}$) e indichiamo $C$ come ${} S = \{\; x \in P \;|\; x \;è\; simpatico \;\}$. Questa è una notazione astratta, che però aiuta a comprendere il seguente concetto:
$$S = \{\; x \in P \;|\; f(x) \;\}$$
Dire "*x è simpatico*" non è una condizione immediatamente verificabile, però permette di capire quali elementi fanno parte di $C$, ovvero quelli che rispettano tale **proprietà** $f(x)$ (o $P(x)$).

### Contenimento
Hint: contenimento (def + formula), sottoinsiemi propri e impropri, insiemi innestati (+ cardinalità + esempio scatola), insieme delle parti (def + esempio + regola cardinalità powerset)
::
Introduciamo ora il concetto di **contenimento**: quando tutti gli elementi di un insieme $A$ sono presenti anche in un altro $B$ (il quale ha altri elementi) si dice che il $A$ è **contenuto/incluso** in $B$ (o che $A$ è un **sottoinsieme** di $B$) e si indica così:
$$A \subseteq B$$
Quindi per ogni $x$ che appartiene ad $A$, $x$ appartiene (anche) a $B$, oppure:
$$\forall x \in A \rightarrow x \in B$$
###### Esempio contenimento
$$A = \{a,b\},\; B = \{a,b,c\} \; \rightarrow \; A \subseteq B$$
> [!info] Sottoinsiemi propri e impropri
> Dato un insieme $A$:
> - I suoi sottoinsiemi **impropri** di $A$ sono: l'**insieme vuoto** ($\emptyset$) e l'**insieme $A$ stesso**,
> - Tutti gli altri (contenuti in $A$) sono i suoi sottoinsiemi **propri**.
##### Insiemi innestati
Si consideri l'insieme $A = \{ gao, \{a, b\}, 1 \}$
Si deduce subito che $\{a,b\} \subseteq A$; però $|A| = 3$ in quanto quell'insieme è considerato come un elemento.
Riprendendo l'analogia delle scatole, $A$ è lo scatolone che contiene gli elementi $gao$, $1$ e un'altra scatola più piccola, la quale a sua volta contiene $a$ e $b$.
> [!info] Attenzione
> Il contenimento è ***diretto***. Consideriamo l'insieme ${} A = \{a,b\{c,d\}\}$, allora:
> - Corretto: $\{a,b\} \subseteq A$ dato che $a,b \in A$.
> - Errato: $\{c,d\} \subseteq A$ dato che $a,b \not{\in} A$.
##### Insieme delle parti
L'**insieme delle parti** (o *powerset*) di un insieme $A$ è l'<u>insieme di tutti (e soli) i sottoinsiemi di A</u> e si rappresenta con $P(A)$; inoltre si ha:
$$\emptyset \in P(A), \;\; A \in P(A)$$
###### Esempio insieme delle parti
Con $A = \{ 1, 2, 3 \}$, i sottoinsiemi di $A$ sono:
- $\emptyset$ con 0 elementi,
- $\{1\}, \{2\}, \{3\}$ con 1 elemento,
- $\{1,2\}, \{2,3\}, \{1,3\}$ con 2 elementi,
- $\{1,2,3\} = A$ con 3 elementi.
> [!important] Regola
> Se un insieme $A$ ha $n$ elementi, allora ${} A$ ha $2^{n}$ sottoinsiemi.
> In altre parole, se $|A| = n \;\rightarrow\; |P(A)| = 2^{n} = 2^{|A|}$

### Diagrammi di Venn
Dato un insieme $S = \{\; Mario, 3, \pi, * \;\}$, è possibile definirlo con un diagramma di Venn:
![](https://i.imgur.com/aJds3Vv.png)
Per quanto riguarda il contenimento di insiemi, tali sono anch'essi rappresentabili con i diagrammi di Venn:
![](https://i.imgur.com/YJ0qr12.png)

### Operazioni tra insiemi
Hint: unione (def, graph, esempio, regola, proprietà, unione tra powerset), intersezione (def, graph, esempio, regola, proprietà, intersezione tra powerset, principio di inclusione/esclusione), differenza (def, graph, proprietà), complemento assoluto (def, graph, proprietà), prodotto cartesiano (coppia, def, esempio, proprietà)
::
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

### Esercizi 
$|P(A) * B| =$ ?
$|P(A \times P(B))| =$ ?
$P(A) \times B =$ ?