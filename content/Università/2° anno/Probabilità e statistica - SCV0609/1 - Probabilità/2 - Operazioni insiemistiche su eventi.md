# Lezione 2

### Operazioni insiemistiche su eventi

##### Unione

L'**unione** tra eventi è composta da tutti gli esiti (non ripetuti) contenuti in tali eventi. Si indica con $A \cup B$ e corrisponde all'operazione logica `OR`.

![](https://i.imgur.com/67AQG2S.png)

> [!important] Probabilità unione
> La probabilità dell'**unione** è composta dalla <u>somma delle probabilità dei singoli eventi</u> **meno** la <u>probabilità dell'intersezione</u> tra gli eventi coinvolti:
> $$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

###### Proprietà unione

Proprietà commutativa: $A \cup B = B \cup A$

Proprietà associativa: $(A \cup B) \cup C = A \cup (B \cup C)$

Proprietà distributiva: $A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$

> [!info] Eventi esaustivi
> Degli eventi si dicono **esaustivi** se la loro unione corrisponde ad $\Omega$, ovvero se: $A \cup B = \Omega$ (ogni evento esaustivo costituisce una partizione di esiti di ${} \Omega {}$).

##### Intersezione

L'**intersezione** tra eventi è composta solamente dagli esiti contenuti in entrambi gli eventi. Si indica con $A \cap B$ e corrisponde all'operazione logica `AND`.

![](https://i.imgur.com/HnMZX11.png)

> [!important] Probabilità intersezione
> La probabilità dell'**intersezione** invece dipende da come sono gli eventi:
> - Indipendenti: $P(A \cap B) = P(A) \cdot P(B)$
> - Dipendenti: $P(A \cap B) = P(A|B) \cdot P(B)$

###### Proprietà intersezione

Proprietà commutativa: $A \cap B = B \cap A$

Proprietà associativa: $(A \cap B) \cap C = A \cap (B \cap C)$

Proprietà distributiva: $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$

> [!info] Eventi incompatibili
> 2 eventi si dicono **incompatibili** (o *disgiunti*) se la loro <u>intersezione è vuota</u>, ovvero se: $A \cap B = \emptyset$ (si dicono invece **compatibili** se hanno un'intersezione).

##### Differenza

La **differenza** tra eventi è composta dagli esiti contenuti in $A$ eccetto quelli di $B$. Si indica con $A \setminus B$.

![](https://i.imgur.com/hg8Ysmd.png)

> [!important] Probabilità differenza
> La probabilità della **differenza** è semplicemente la probabilità del 1° evento meno l'intersezione dei 2:
> $$P(A \setminus B) = P(A) - P(A \cap B)$$

##### Complemento

Il **complemento** di un evento è costituito dagli esiti non appartenenti ad $A$. Si indica con $A^{c}$ e corrisponde all'operazione logica `NOT`.

![](https://i.imgur.com/GrLV8rJ.png)

> [!important] Probabilità complemento
> La probabilità del **complemento** è semplicemente 1 - la probabilità dell'evento:
> $$P(A^{c}) = 1 - P(A)$$

###### Proprietà complemento

$(A^{c})^{c} = A$

$A \cup A^{c} = \Omega$

$A \cap A^{c} = \emptyset$

$(A \cup B)^{c} = A^{c} \cap B^{c}$

$(A \cap B)^{c} = A^{c} \cup B^{c}$

---

Prossima lezione: [[3 - Conteggio]]

