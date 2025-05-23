# Lezione 11

### Graph Traversal Algorithms

Gli <u>algoritmi di attraversamento dei grafi</u> consistono nella visita di ogni singolo nodo di un grafo o albero (al fine di costruzioni di percorsi, cicli e altro). Vedremo:

![](https://skilled.dev/images/tree-dfs-vs-bfs.gif)

##### BFS

La <u>ricerca in ampiezza</u> (**BFS** o ***Breadth-first search***) parte dalla radice e <u>visita tutti i nodi fratelli in ogni livello</u> usando le loro liste di adiacenza e una coda. Quindi:

- **Input**: un **grafo** $G = (N,L)$ non orientato e connesso,
- **Output**: una sequenza che contiene tutti i **nodi in ordine in base al livello** (non si specifica ordinamento per nodi dello stesso livello).

###### Implementazione BFS

```java
public void BFS(Graph g) {
	// Variabili
	Queue<Nodo> q = new Queue<Nodo>();               // q = coda dei nodi da visitare
	List<Lato> l = new List<Lato>();                 // l = lista lati visitati
	boolean[] nuovo = new boolean[g.nodi.length()];  // nuovo = array che indica se nodo visitato (meglio HashMap<Nodo, boolean>)
	
	// Imposta tutti i nodi a "non visitato" (true)
	for (n in g.nodi)
		nuovo[n] = true;
	// (Tranne il 1°)
	nuovo[g.nodi[0]] = false;
	q.enqueue(g.nodi[0]);
	
	while (!q.isEmpty()) {
		// Ottiene il 1° nodo e lo rimuove dalla queue
		Nodo n = q.remove();
		n.visit();
		// (Se nuovo) Aggiunge in queue nodi adiacenti + li setta come visitati + inserisce nella lista il lato tra n e m
		for (m in n.getAdjacentNodes())
			if (nuovo[m]) {
				q.add(m);
				nuovo[m] = false;
				l.insert({n, m}, 1);
			}
	}
}
```

Si può passare alla funzione una lista di nodi come anche un albero. Poi generalmente la classe `Nodo` potrebbe implementare uno stato booleano `visited` che indica se il nodo è stato visitato o no (così da non mantenere l'array/hashmap `nuovo`).

###### Complessità BFS

Sempre dato il grafo $G = (N,L)$:

- Lo **spazio** è $\Theta(n)$ siccome il vettore `nuovo` ha $n$ elementi ($\Theta(n))$, che saranno sempre più del n° di lati (lista `l`) e del n° max di nodi nella queue `q` (min 1, max $n$ in caso di grafo a stella dove tutti i nodi sono adiacenti alla radice).
- Il **tempo** è $\Theta(n+m)$ siccome il `while` visita ciascun nodo nuovo (quindi $\Theta(n)$ o $n$ volte, tutti una volta sola), mentre il `for` interno visita gli adiacenti di ogni nodo, ovvero $m$ (perciò la complessità di questo è $\Theta(m))$.

> [!example] Esempio
> ![](https://i.imgur.com/qTP9E2i.png)

##### DFS

La <u>ricerca in profondità</u> (**DFS** o ***Depth-first search***) invece visita i nodi di ogni percorso del grafo, dalla radice ad una foglia, da quello più a sinistra. Quando si raggiunge una foglia, si torna indietro fino a trovare un lato (e quindi un percorso) nuovo e così via fin quando non si visita tutto l'albero. Quindi:

- **Input**: un **grafo** $G = (N,L)$ non orientato e connesso,
- **Output**: una sequenza che contiene tutti i **nodi in ordine in base al percorso** (da sinistra a destra ogni percorso possibile).

###### Implementazione DFS

```java
public void DFS(Graph g) {
	// Variabili
	Stack<Nodo> s = new Stack<Nodo>();               // q = coda dei nodi da visitare
	List<Lato> l = new List<Lato>();                 // l = lista lati visitati
	boolean[] nuovo = new boolean[g.nodi.length()];  // nuovo = array che indica se nodo visitato (meglio HashMap<Nodo, boolean>)
	
	// Imposta tutti i nodi a "non visitato" (true)
	for (n in g.nodi)
		nuovo[n] = true;
	// (Tranne il 1°)
	Nodo n = g.nodi[0];
	n.visit();
	nuovo[n] = false;

	do {

		for (Nodo m in n.getAdjacentNodes()) {
			if (nuovo[m]) {
				m.visit()
				nuovo[m] = false;
				l.insert({n, m}, 1);
				s.push(m);
				n = m;
			}
		}

		s.pop();
		if (!s.isEmpty()) n = s.peek();

	} while (!s.isEmpty())
}

```

> [!info] Implementazione ricorsiva
> ```java
> Graph g = new Graph()                            // Supponiamo di avere un grafo
> boolean[] nuovo = new boolean[g.nodi.length()];  // nuovo = array che indica se nodo visitato
> 
> // Imposta tutti i nodi a "non visitato" (true)
> for (n in g.nodi)
> 	nuovo[n] = true;
> 	
> public void DFS(Nodo n) {
> 	n.visit();
> 	nuovo[n] = false;
> 	for (m in n.getAdjacentNodes()) {
> 		if (nuovo[n]) {
> 			l.insert({n, m}, 1);
> 			DFS(m);
> 		}
>	}
> }
> ```

###### Complessità DFS

La complessità delle 2 versioni iterativa e ricorsiva è la medesima e, sempre dato il grafo $G = (N, L)$:

- Lo **spazio** necessario è $\Theta(n)$ sempre per il vettore `nuovo`, la lista `l` e i cicli (questi $O(n)$),
- Il **tempo** anche qua è $\Theta(n+m)$, sempre perché si visitano $n$ nodi e per ogni nodo si visitano gli adiacenti (alla fine $m$, ovvero $\Omega(n)$).

> [!example] Esempio
> ![](https://i.imgur.com/WYFSGME.png)

---

Prossima lezione: [[10 - Attraversamento degli alberi]]

