# Lezione 9

#### Algebra eterogenea

Con "algebra eterogenea" si denota una struttura composta da vari insiemi di con tipi di dati diversi ed un'insieme di operazioni che agiscono su questi. Prendiamo ad esempio un insieme $A$; per rappresentare esso e le sue parti ($P(A)$) abbiamo bisogno di 3 operazioni: `member(x, A)` che dice se $x \in A$, `insert(x, A)` che inserisce $x$ in $A$ e `delete(x, A)` che rimuove $x$ da $A$.

Continuando si introduce $P(A)_{O}$, ovvero l'insieme delle parti di $A$ ordinato, il quale dispone di altre operazioni quali `min()`, `max()`... Per implementare algebre eterogenee come l'insieme $P(A)$ si possono usare:

- ***Linked lists***: semplici, ma in media le operazioni costano $O(n)$,
- ***Hash tables***: in media le operazioni costano $O(1)$ (se non si sbaglia ad impostare certi parametri, in quel caso $O(n)$).

### Tabelle hash

---

Prossima lezione: [[10 - Attraversamento degli alberi]]

