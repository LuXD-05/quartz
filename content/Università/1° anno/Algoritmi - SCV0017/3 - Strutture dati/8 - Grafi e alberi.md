# Lezione 8

### Grafi

Un **grafo** è una struttura composta da **nodi** (gli <u>elementi</u> coi valori del grafo) e **lati** (che <u>collegano</u> tra loro i nodi). 

Formalmente, con $G$ il grafo, ${} N$ i nodi ed $L$ i lati: $\;\;G(N,L)\;\;$ ed $\;\;L \subseteq N \times N\;\;$ (ogni elemento di $L$ è una coppia di vertici collegati da un lato).

> [!important] Sottografo
> $G'(N',L')$ è un sottografo di $G(N,L)$ se e solo se:
> - ${} N' \subseteq N$,
> - ${} L' \subseteq L \cap N' \times N' {}$

###### Orientamento

Un grafo $G(V,E)$ è ***non orientato*** se i <u>lati non hanno una direzione</u> (negli elementi di $E$ <u>non importa l'ordine</u>):

![](https://i.imgur.com/CahrOKg.png)

Un grafo $G(V,E)$ si dice invece ***orientato*** se gli ***archi*** (lati con direzione) <u>hanno una direzione</u> (gli elementi di $E$ sono <u>coppie</u> e <u>importa l'ordine</u>):

![](https://i.imgur.com/NHhvci5.png)

> [!important] Adiacenza e cappi
> Due nodi $x$ e $y$ si dicono **adiacenti** se collegati dallo stesso lato/arco.
> L'**insieme di adiacenza** di un nodo $x$ contiene tutti <u>i nodi al quale è collegato</u>: $Ad(x) = \{ x \;|\; (x,y) \in L \}$ (anche per grafi non orientati).
> In <u>grafi orientati</u>, la coppia $(x,x)$ (arco da un nodo a se stesso), si dice **cappio**:
> ![](https://i.imgur.com/y1iNBoC.png)

##### Caratteristiche

Prendiamo un grafo $G$ con $n$ nodi e $l$ lati:

- Con $G$ **orientato**: $\; 0 \leq l \leq n^{2} \;$ (n° lati è sempre < o = al n° dei nodi al quadrato),
- Con $G$ **non orientato**: $\; 0 \leq l \leq \dfrac{n(n-1)}{2} \;$ (n° lati è sempre < o = a $\dfrac{n(n-1)}{2}$).

###### Densità

Un grafo $G(n,l)$ è **sparso** se $l = O(n)$, ovvero se il ci sono <u>pochi lati rispetto al massimo</u> possibile.

Uno stesso grafo $G(n,l)$ si dice **denso** se $l = \Theta(n^{2})$, ovvero se il <u>n° di lati si avvicina al massimo</u> possibile.

###### Percorsi

Un **percorso** (o cammino) di **lunghezza** $n-1$ è una <u>sequenza di nodi collegati da archi consecutivi</u>, così denotato:

$$x_{1} \rightarrow x_{2} \rightarrow \ldots \rightarrow x_{n}$$

O, a livello di coppie:

$$(x_{1},x_{2}) \rightarrow (x_{2},x_{3}) \rightarrow \ldots \rightarrow (x_{n-1},x_{n})$$

Un percorso è **semplice** se <u>non ammette ripetizioni</u>.

> [!info] Grafo connesso
> Un grafo si dice **connesso** se esiste un **percorso** che <u>collega tutti i suoi nodi</u>.

###### Cicli

Un **ciclo** invece è un percorso nel quale l'ultimo nodo si ricollega al 1° (senza altre ripetizioni).

(Diverso dal **percorso chiuso**, dove più ripetizioni sono ammesse).

##### Rappresentazioni

Un grafo può essere rappresentato tramite <u>liste o matrici di adiacenza</u>. Consideriamo il seguente esempio:

![](https://i.imgur.com/fybH9xT.png)

###### Liste di adiacenza

Le **liste di adiacenza** sono strutture nelle quali ogni nodo è rappresentato in una colonna ed in un'altra si hanno i corrispondenti nodi collegati ad esso:

![](https://i.imgur.com/MK6HYHf.png)

**Vantaggio**: la rappresentazione occupa poco spazio in memoria ($\Theta(n+m)$).

**Svantaggio**: la ricerca è nell'ordine di $O(n)$ (esempio: cercando se 4 è in relazione con 2, devo verificare ogni elemento della lista di 2).

Perciò le liste di adiacenza sono adatte alla rappresentazione di grafi **[[#Densità|sparsi]]**.

###### Matrici di adiacenza

Le matrici di adiacenza invece rappresentano i nodi di partenza nella 1a colonna, quelli di destinazione nella 1a riga (o viceversa) e gli archi nelle celle (nelle corrispondenze con `1` c'è un arco tra i 2 nodi, mentre se c'è `0` i nodi non sono collegati):

![](https://i.imgur.com/Nrh5gTl.png)

**Vantaggio**: la ricerca è nell'ordine di $O(1)$ (esempio: cercando se 4 è in relazione con 2, si vede subito in `m[4][2]`).

**Svantaggio**: la rappresentazione occupa tanto spazio in memoria ($\Theta(n^{2})$).

Perciò le matrici di adiacenza sono adatte alla rappresentazione di grafi **[[#Densità|densi]]**.

#### Alberi

Un **albero** è un grafo **non orientato**, **connesso** (ammette 1 solo percorso tra qualunque coppia di nodi) e **aciclico**; quindi ha $n$ nodi e $n-1$ lati. Negli alberi si hanno 3 tipi di nodi:

- La **radice** di un albero è il 1° nodo dal quale partono tutti gli altri,
- I nodi finali dei percorsi si dicono **foglie** (non hanno figli),
- Il resto (tra radice e foglie) sono <u>nodi interni</u> (hanno figli).

> [!info] Relazioni tra nodi
> - $x$ è **padre** di $y$ se lo precede nel percorso dalla radice ad esso,
> - $y$ è **figlio** di $x$ se $x$ è padre di $y$,
> - $x$ è **fratello** di $y$ se hanno lo stesso padre,
> - $x$ è **antenato** di $y$ se $x$ compare nel percorso dalla radice a $y$,
> - $y$ è **discendente** di $x$ se $x$ è antenato di $y$.

###### Grado e profondità

Il **grado** di un nodo è il <u>n° di figli posseduti</u>.

La **profondità** (o **livello**) di un nodo è la <u>lunghezza del percorso che collega la radice ad esso</u>.

> [!info] Alberi $n$-ari
> Un albero $n$-ario è uno il cui grado massimo dei nodi è $n$.
> In un albero $n$-ario al livello $x$ ci saranno sempre massimo $n^{x}$ nodi.
> Un livello è **saturo** se presenta il <u>n° massimo possibile di nodi</u>.
> ![](https://i.imgur.com/4tub4qF.png)

###### Altezze e lunghezze

L'**altezza** di un qualsiasi nodo $x$ è la lunghezza del percorso più lungo da $x$ a una foglia (l'altezza dell'albero è l'altezza della radice).

Ci sono poi 3 lunghezze di un albero:

- $L_{i}$ = la lunghezza del percorso <u>interno</u> è la somma dei livelli di tutti i nodi interni,
- ${} L_{e}$ = la lunghezza del percorso <u>esterno</u> è la somma dei livelli di tutte le foglie,
- $L$ = la <u>lunghezza del percorso</u> è data da $L_{i} + L_{e}$.

###### Calcolare n° max di nodi in albero $n$-ario data $h$

Per calcolare il n° max di nodi di un albero $n$-ario data $h$ (altezza) si usa una funzione chiamata **serie geometrica troncata**:

$$f_{h}(n) = \sum\limits_{i=0}^{h} k^{i} = \dfrac{n^{h+1} - 1}{n-1}$$

##### Alberi binari

Un **albero binario** è uno orientato con radice dove <u>ogni nodo ha max 2 figli</u>: quello sinistro e quello destro.

Dati alberi binari completi di altezza $h$ e con $n$ nodi si ha che: $2^{h} \leq n \leq 2^{h+1} - 1$ (quindi $h$ soddisfa la relazione $h \sim \log_{2}{n}$).

Un albero binario è:

- **Pieno** quando è <u>saturo ad ogni livello</u> (eccetto l'ultimo eventualmente),

  ![](https://i.imgur.com/eWugBwM.png)

- **Completo** se è pieno e le foglie sono tutte il più a sinistra possibile,

  ![](https://i.imgur.com/nZAvbt6.png)

- **Degenere** se ha $n$ nodi e $h = n-1$ (il n° di alberi binari degeneri con $n$ nodi è $2^{n-1}$),
- **Localmente completo** quando ogni suo nodo ha 0 o 2 figli. Inoltre, lo stesso con $n$ nodi interni ha $n+1$ foglie.

###### Numeri di Catalano

Il n° di alberi binari localmente completi con $n$ nodi interni è:

$$\dfrac{1}{n+1}\dbinom{2n}{n}$$
Equazione:
![](https://i.imgur.com/aAYMYZo.png)
> [!info] Nota
> In un albero binario localmente completo con $n$ nodi interni vale:
> $$L_{e} = L_{i} + 2n$$

---

Prossima lezione: [[9 - Tabelle hash]]

