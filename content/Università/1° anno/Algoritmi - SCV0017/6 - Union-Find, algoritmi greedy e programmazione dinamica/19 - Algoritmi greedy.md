# Lezione 19

##### Sistemi di indipendenza e problemi di ottimizzazione

Un **sistema di indipendenza** è semplicemente una **coppia** $(E,F)$ dove $E$ è un **insieme** ed $F$ è un insieme contenente dei **sottoinsiemi "*validi*"** di $E$ ovvero che <u>rispettano una certa regola</u> (per esempio: $E$ = archi di un grafo ed $F$ = archi che non formano cicli).

In un **problema di ottimizzazione** invece abbiamo una <u>funzione "peso"</u> ${} w$ la quale <u>indica</u> il "peso" (<u>valore</u>) <u>di ogni elemento</u> di $E$; e vogliamo trovare un sottoinsieme $M \in E$ che:

- Sia **valido** $M \in F$,
- Abbia **peso totale** (valore totale tutti i suoi elementi) **massimo**.

### Procedura greedy

Un *algoritmo greedy* risolve un problema di ottimizzazione ciclando su ogni elemento di $E$ ed aggiungendo alla soluzione $M$ l'elemento con peso massimo. In generale:

```java
public static Set Greedy(Set E, Set F, func w) {

	Set M = emptyset();

	while (E.length > 0) {    // Finché E ha elementi
	
		var m = max(E, w);    // Prendo elemento con peso max usando w
		E -= {m};             // Rimuovo da E
		
		if ((M+{m}) in F)     // Se soluzione + m è valida
			M.add(m);         // Aggiunge m a soluzione

	}

	return M;

}
// Procedura con ordinamento
public static Set Greedy(Set E, Set F, func w) {

	Set M = emptyset();

	sort(E, w);                              // Ordina E

	for (int i = 1; i <= E.length; i++) {
		if ((M+{E[i]}) in F)                 // Se soluzione + m è valida
			M.add(E[i]);                     // Aggiunge m a soluzione
	}

	return M;

}
```

###### Complessità

In caso $n = \#E$, si ha che:

- `sort()`: costa $O(n \log n)$,
- `... in F`: (ovvero vedere se soluzione + max è valida) costa $\alpha(n)$,
- `Greedy()`: costa $O(n \log n + n \cdot \alpha(n))$,

###### Matroidi

Un **matroide** è un <u>sistema di indipendenza</u> con anche la **proprietà di scambio**; la quale, dati 2 sottoinsiemi validi (in $F$) $A$ e $B$ tali che $A$ ha meno elementi di $B$ allora <u>esiste un elemento che posso "scambiare"</u> da $B$ ad $A$ <u>senza perdere la validità</u>. Esempio: $A = \{a,b\} \; B = \{a,b,c\}$, scambiando $c$ da $B$ ad $A$. 

Un altro esempio è dato con un **matroide grafico** $(E,F)$ dove $E$ è un grafo non orientato ed $F$ contiene insiemi di archi che non formano cicli.

> [!important] Teorema di Rado
> Se il sistema di indipendenza di un problema di ottimizzazione è un **matroide**, la <u>procedura greedy restituisce sempre la soluzione ottima</u>.

#### Esempi di algoritmi greedy

##### Algoritmo di Kruskal

L'algoritmo di Kruskal si usa per risolvere il problema di ottimizzazione **MST** (*Minimum Spanning Tree*), ovvero trovare l'**albero di copertura** (albero <u>che connette tutti i nodi</u> senza cicli) con **peso minimo** di un grafo non orientato pesato e connesso $G(V,E)$.

```java
public static Set Kruskal(Set V, Set E, func w) {

	Set MST = emptyset();
	UnionFind P = new UnionFind(V.size());       // Inizializza tante partizioni (della classe UnionFind) quanti i nodi

	while (P.size() != 1) {                      // Scorre finche non unisce tutto

		Edge e = E.min()                         // Prende l'arco con peso minimo (+ lo cancella da E)
		E.delete(e);

		if (P.find(e.from) != P.find(e.to)) {    // Se i nodi di tale arco sono in 2 partizioni diverse
		
			P.union(e.from, e.to);               // Unisco e aggiungo alla soluzione
			MST.add(e);
		
		}
	
	}

	return MST;

}
```

![](https://thealgoristsblob.blob.core.windows.net/thealgoristsimages/kruskals-algorithm-anim-1.gif)

###### Complessità Kruskal

Dati $n$ nodi e $m$ archi: 1) si itera al max $m$ volte, poi per ogni arco 2) (se si usa un min-heap) `E.min()` costa $O(1)$ (come anche `MST.add()`), 3) `E.delete()` costa $O(\log m)$ (cerca l'arco nel min-heap), 4) `union()` e `find()` costano entrambi $O(\log n)$ (visto in lezione 18); perciò il costo totale è:

$$O(m) \cdot ( O(1) + O(\log m) + 2\,O(\log n)) = O(m \log m)$$

($O(1)$ e $2\,O(\log n)$) si ignorano di fronte a $O(\log m)$ in quanto quest'ultimo è (generalmente) sempre maggiore di essi.

##### Algoritmo di Prim

L'algoritmo di prim serve sempre ad ottenere un MST da un grafo non orientato, connesso e pesato, solo che invece di visitare tutti gli archi, parte da un nodo sorgente $n$ a scelta collegando, ad ogni step, alla soluzione parziale il nodo più vicino tra quelli non ancora raggiunti.

```java
public static Set Prim(Set V, Set E, func w, Node n) {

	Set MST = emptyset();
	Set D = emptyset();                         // Set di nodi adiacenti scoperti (dist != inf) 
	Set R = V - {n}                             // Set di nodi non ancora visitati

	Map<Node, Integer> dist = new HashMap();    // Array delle distanze in termini di peso (init con tutte a infinito)
    Map<Node, Node> near = new HashMap();       // 

	for (node in R)                             // Init: non si conoscono distanze --> setta tutto a INF
		dist[node] = Integer.MAX_VALUE;

	for (node in n.getAdjacentNodes()) {        // Per ogni nodo adiacente a n
		near[node] = n;                         // - Gli assegni n come vicino
		dist[node] = w({n,node}));              // - Assegna distanza tra sorgente (n) e nodo corrente in termini di peso (w)
		D.add(node);                            // - Lo aggiungi ai nodi scoperti
	}

    while (!D.isEmpty()) {                                  // Finché ce ne sono di adiacenti con distanza != infinito
    
        Node v = nearest(D, dist);                          // Prende il candidato più vicino (in termini di peso dell'arco con dist)
        D.remove(v);                                        // + lo rimuove dai nodi scoperti
        R.remove(v);                                        // + lo rimuove dai nodi non visitati
        MST.add({v, near[v]});                              // + aggiunge arco v-nearest a soluzione

		for (node in v.getAdjacentNodes()) {
		
			if (node in R && w({node,v}) < dist[node]) {    // Se adiacente non visitato + new peso < old peso
			
				if (dist[node] == Integer.MAX_VALUE)        // Se nuovo (peso infinito) aggiunge a quelli scoperti
					D.add(node);
					
				dist[node] = w({node,v});                   // Aggiorna il peso
				near[node] = v;                             // Aggiorna array vicini
				
			}
		
		}
		
    }

    return MST;

}
```

 ![](https://youtu.be/oDnlIP5pe5o)

###### Complessità Prim

Dati $n$ il n° di nodi ed $m$ il n° di archi, ogni lista di adiacenza è attraversata 1 volta ($O(m)$) mentre per aggiungere ogni nodo è $O(\log n)$ il che sommato da:

$$O(m \log n)$$

##### Algoritmo di Dijkstra

L'algoritmo di Dijkstra è molto simile a quello di Prim, solo che non serve per costruire un MST, bensì per trovare il percorso minore tra un nodo sorgente $n$ e gli altri tramite 2 array. La differenza principale consiste nel fatto che in Prim, `dist` ora contiene il peso totale minimo di ogni percorso da $n$ a un nodo nell'array.

```java
public static Set Dijkstra(Set V, Set E, func w, Node n) {

	Set D = emptyset();                         // Set di nodi adiacenti scoperti (dist != inf) 
	Set R = V - {n}                             // Set di nodi non ancora visitati

	Map<Node, Integer> pcam = new HashMap();    // dist // Array dei pesi dei percorsi (init con tutti a infinito)
    Map<Node, Node> pred = new HashMap();       // near // Array di nodi dei percorsi ???

	for (node in R)                             // Init: non si conoscono path --> setta tutto a INF
		pcam[node] = Integer.MAX_VALUE;

	for (node in n.getAdjacentNodes()) {        // Per ogni nodo adiacente a n
		pred[node] = n;                         // - Gli assegni n come vicino
		pcam[node] = w({n,node}));              // - Assegna distanza tra sorgente (n) e nodo corrente in termini di peso (w)
		D.add(node);                            // - Lo aggiungi ai nodi scoperti
	}

    while (!D.isEmpty()) {                                  // Finché ce ne sono di adiacenti con distanza != infinito

		Node v = nearest(D, dist);                          // Prende il candidato più vicino (in termini di peso dell'aSco con dist)
        D.remove(v);                                        // + lo rimuove dai nodi scoperti
        R.remove(v);                                        // + lo rimuove dai nodi non visitati

		for (node in v.getAdjacentNodes()) {
		
			if (node in R && pcam[v] + w({v,node}) < pcam[node]) {    // Se adiacente non visitato + new peso < old peso
			
				if (pcam[node] == Integer.MAX_VALUE)                  // Se nuovo (peso infinito) aggiunge a quelli scoperti
					D.add(node);
					
				pcam[node] = pcam[v] + w({v, node});                  // Aggiorna il peso
				pred[node] = v;                                       // Aggiorna array vicini
				
			}
		}
    }

    return MST;

}
```

###### Complessità Dijkstra

Essendo praticamente uguale a Prim, il costo dell'algoritmo di Dijkstra è:

$$O(m \log n)$$

---

Prossima lezione: [[20 - Programmazione dinamica]]

