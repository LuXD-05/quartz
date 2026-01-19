# Lezione 15

### Artefatti e relazioni

![](https://i.imgur.com/ZPvk2Vu.png)

L'immagine sopra raffigurata indica i vari tipi di relazioni che ci sono tra reti combinatorie, espressioni booleane e tavole di verità.

##### Da espressione booleana a tavola di verità

Avendo un'espressione booleana, è possibile passare alla relativa tabella di verità mediante la **tabellazione**:

1) Si prendono le singole variabili che costituiscono l'espressione booleana e si mettono in colonne separate,
2) Si scrivono sotto tali variabili tutte le possibili combinazioni che possono generare un output,
3) In base all'operatore logico tra le variabili, si scrive nella colonna dell'output il risultato dell'espressione logica per ogni combinazione di input.

![](https://i.imgur.com/jOY1r0W.png)

##### Da espressione booleana a rete combinatoria

Per ottenere una rete combinatoria da un'espressione booleana si fa il processo chiamato **implementazione**:

1) Le variabili dell'espressione sono gli input,
2) Gli operatori vanno a costituire le porte che agiscono sugli input,
3) Si ha il valore dell'espressione in output.

Tipo, $A +$ /$A$ /$B$:

![](https://i.imgur.com/pok6x1V.png)

> [!info] Nota
> Espressioni differenti (purché equivalenti) producono circuiti differenti. Spesso quindi è necessario ottimizzare l'espressione (attenzione, espressioni con meno operatori sono generalmente meno costose ma non necessariamente più veloci).

##### Da rete combinatoria a tavola di verità

Per arrivare alla tavola di verità da una rete combinatoria si fa la **simulazione** della rete stessa, ovvero:

1) Si applicano (virtualmente) i valori 0 e 1 agli ingressi,
2) Combinazione per combinazione, si computa l'output.

Tipo:

![](https://i.imgur.com/D8TjPH2.png)

![](https://i.imgur.com/jKCVD2k.png)

##### Da rete combinatoria ad espressione booleana

Da una rete combinatoria è possibile ricavare la relativa espressione booleana con l'**analisi** della rete:

1) Si applica una lettera alle porte della rete,
2) Si esprimono le lettere in funzione degli input (scrivendoci le lettere legate dall'operatore corrispondente alla porta),
3) Si semplifica e si esprime l'output in funzione delle espressioni delle lettere.

Quindi, partendo da questa rete:

![](https://i.imgur.com/Zas1nOT.png)

Si ha: $p = \lnot{A}\;B$, $q = \lnot{C}$, $r = \lnot{A}\;C$

E quindi: $F(A,B,C) = \lnot{A}\;B + \lnot{C} + \lnot{A}\;C$

##### Dalla tavola di verità alla rete combinatoria

Per passare da una tavola di verità alla rispettiva rete combinatoria bisogna fare un processo di **sintesi di rete combinatoria**:

1) Bisogna trovare <u>una</u> espressione booleana che esprima la funzione logica data (sottoforma di tavola di verità) attraverso metodi come la **[[16 - SoP e PoS#Sum of Products|Somma di Prodotti]]** o il **[[16 - SoP e PoS#Product of sums|Prodotto di Somme]]**,
2) Si costruisce la rete combinatoria corrispondente all'espressione trovata grazie ad un modello di schema simile:

   - Per la **SoP**: ![](https://i.imgur.com/5PnToCA.png)

   - Per il **PoS**: (corrispettivo ma con AND al posto di OR e viceversa)

Dato che <u>per una tavola di verità possono esistere più espressioni booleane</u> (quindi anche <u>più reti</u>), la soluzione al problema non è unica, rendendo così prioritario <u>trovare l'espressione booleana / rete migliore</u> in quanto, anche se funzionalmente equivalenti, le reti hanno diversi costi e prestazioni.

Per sintetizzare una rete combinatoria bisogna stare attenti a: <u>complessità della tecnica</u> e <u>qualità della rete risultante</u> (per costo, velocità, dimensioni...).

# Esercizi

# Soluzioni

---

Prossima lezione: [[16 - SoP e PoS]]

