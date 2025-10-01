# Lezione 3

### Contenimento

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

Si consideri l'insieme $A = \{a, b, \{x, 1\}\}$

Riprendendo l'analogia delle scatole, $A$ è lo scatolone che contiene gli elementi ${} x {}$, $1$ e un'altra scatola più piccola, la quale a sua volta contiene $a$ e $b$.

Potrebbe sembrare controintuitivo, ma $\{x,1\} \not\subseteq A$, perché la scatola è al pari di un elemento in $A$, quindi è corretto dire che: $\{x,1\} \in A$; infatti in questo caso ${} |A| = 3 {}$.

> [!info] Attenzione
> Il contenimento è ***diretto***. Consideriamo l'insieme $A = \{a,b,\{c,d\}\}$, allora:
> - Corretto: $\{a,b\} \subseteq A$ dato che $a,b \in A$.
> - Errato: $\{c,d\} \subseteq A$ dato che $c,d \not{\in} A$.

#### Insieme delle parti

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

# Esercizi

# Soluzioni

---

Prossima lezione: [[4 - Diagrammi di Venn]]

