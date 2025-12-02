# Lezione 9

### Insieme delle parole

Dato $A$ un insieme "alfabeto", una parola di $A$ è una sequenza (finita) di simboli di $A$ (anche singole lettere); perciò si definisce $A^{+}$ come l'**insieme delle parole** su $A$.

Se $x \in A^{+}$, la **lunghezza** della parola $x$, definita con $\#x$, è il <u>n° di lettere in essa</u>.

> [!info] Nota
> Anche se $|A| = 3$, l'insieme $A^{+}$ ha infiniti elementi.
> $\forall x \in \mathbb{N}$ esistono parole di lunghezza $x$.

###### Esempio insieme delle parole

Consideriamo una relazione $R$ su $A^{+} \times A^{+}$ dove le parole hanno la stessa lunghezza.

$$R = \{(x,y) \in A^{+} \times A^{+} \;|\; \#x = \#y\}$$

Riflessiva? Si, $\forall x \in A^{+} \;\rightarrow\; \#x = \#x$

Simmetrica? Si, $\forall (x,y) \in A^{+} \;\rightarrow\; \#x = \#y \land \#y = \#x$

Transitiva? Si, $\forall (x,y,<) \in A^{+} \;\rightarrow\; \#x = \#y \land \#y = \#z \land \#z = \#x$

Quindi è una <u>relazione di equivalenza</u>. Scriviamo le <u>classi di equivalenza</u>:

$[a]_{R} = \{x \in A^{+} \;|\; \#x = \#a = 1\} = \{a,b,c\} = [b]_{R} = [c]_{R}$

$[aa]_{R} = \{x \in A^{+} \;|\; \#x = \#aa = 2\}$

$[aaa]_{R} = \{x \in A^{+} \;|\; \#x = \#aaa = a\}$

E così via, risultando quindi in infinite classi di equivalenza. 

L'insieme quoziente sarà l'insieme di tutte le parole di $A$ ($A^{+}$ aventi la stessa lunghezza):

$A^{+}$/$R = \{[x]_{R} \;|\; x \in A^{+}\} =$

### Partizioni

Una **partizione** di $A$ è un insieme $F$ di **sottoinsiemi** di $A$, con $F \subseteq P(A)$ tali che:

- $\emptyset \not{\in} \;F$,
- $(x,y) \in F \; (x \neq y \implies x \cap y = \emptyset)$ (i *blocchi* devono essere **disgiunti**),
- $\underset{x\,\in\,F}{U}\,x = A\;$ (ovvero $\underset{x\,\in\,F}{U}\,x$, l'[[5 - Operazioni tra insiemi#Unione|unione]] di tutti gli insiemi $F$, deve essere = $A$).

> [!info] Quindi
> Quindi si può dire che una partizione di un insieme $A$ è un insieme di suoi sottoinsiemi tali che (oltre a non avere $\emptyset$) nessun elemento di $A$ è in nessun blocco o condiviso tra 2 ***blocchi*** (così chiamati gli elementi di una partizione).

##### Proprietà partizioni

- Se $R$ è una relazione di equivalenza su $A$, allora $A$/$R$ è una partizione di $A$ (quindi: se $R$ ... su $A$, le classi di equivalenza di $A$ (in base a $R$) sono partizione di $A$).
- Se $F$ è partizione di $A$, $\forall x \in A$ esiste un solo blocco $B$ di $F$ tale che $x \in B$ (nessun elemento è condiviso tra + blocchi),
- Se $F$ è partizione di $A$, esiste una relazione di equivalenza $R_{F}$ per cui 2 elementi $x,y$ sono in relazione se appartengono allo stesso blocco; ciò porta <u>blocchi</u> di $F$ e <u>classi di equivalenza</u> di $R_{F}$ a coincidere.

##### Esempi

###### Esempio partizioni 1

$A = \{a,b,c\}$, $F = \{\{a\},\{b,c\}\}$.

$F$ rispetta le regole suddette, quindi è una partizione di $A$. Controesempi:

- $\{\{a\},\{a,b\},\{c\}\}$ NO ($\cap$ tra 2 blocchi da qualcosa).
- $\{\{a\},\{b\}\}$ NO (manca c).

###### Esempio partizioni 2

Esempio $\mathbb{Z}$:

Consideriamo la partizione $F = \{2\mathbb{Z},2\mathbb{Z}+1\}$ (partizione di numeri pari e dispari).

$F$ è partizione di $\mathbb{Z}$ perché:

- $F \not\in \emptyset$,
- $2\mathbb{Z} \cap 2\mathbb{Z}+1 = \emptyset$,
- $2\mathbb{Z} \cup 2\mathbb{Z}+1 = \mathbb{Z}$.

Allora qual è la relazione $R_{F}$? Dalla formula, $\forall n,m \in Z \;\rightarrow\; nR_{F}m$ se sono nello stesso blocco.

... (riga di cui non si è capito un cazzo)

Esempio 2:

$A = \{a,b,c\}$, quante partizioni (o relazioni di equivalenza) ha $A$? Si vanno a contare tutti i modi di partizionare $A$.

(foto insiemi (partizioni))

(foto insiemi (relazioni d'equivalenza))

###### Esempio partizioni 3

Definiamo un insieme con parole di 3 lettere (a,b,c): $A^{3} = \{x \in A^{+} \;|\; \#x = 3\}, A = \{a,b,c\}$. Questo insieme ha 27 elementi.

Poi: $R = \{(x,y) \in A^{3} \times A^{3} \;|\; x,y$ hanno la stessa lettera iniziale $\}$, quindi:

$[aaa]_{R} = \{x \in A^{3} \;|\; x$ inizia con "a" $\}$,

${} [bbb]_{R} = \{x \in A^{3} \;|\; x$ inizia con "b" $\}$,

$[ccc]_{R} = \{x \in A^{3} \;|\; x$ inizia con "c" $\}$.

# Esercizi

# Soluzioni

---

Prossima lezione: [[10 - Antisimmetria e relazioni d'ordine]]

