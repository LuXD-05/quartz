# Lezione 18

### Partizioni

Ricordando le [[9 - Insieme delle parole e partizioni#Partizioni|partizioni]] di un insieme in algebra, andiamo a definire una struttura dati $PA = (\;[A,P(A)]\;,$`union()`,`find()`$)$ dove $P(A)$ è l'insieme della partizioni di $A$ e:

- `union(x,y,P)`: <u>sostituisce</u> in $A$ le <u>partizioni</u> contenenti $x$ e $y$ (li chiamiamo $a_{x}$ e $a_{y}$) <u>con</u> $a_{x} \cup a_{y}$.
- `find(x,P)`: restituisce il <u>rappresentante della partizione</u> che contiene $x$.

> [!abstract] Implementazioni
> Possibili implementazioni di $PA$:
> - **Liste concatenate**: <u>semplici</u> ma il <u>costo medio di ogni operazione</u> è $O(A)$,
> - **Foreste di alberi**: <u>costo di ogni operazione</u> è $O(\log A)$ ma gli <u>alberi vanno bilanciati</u>.

##### Foreste di alberi

Così ad ogni **partizione** corrisponde un **albero** la cui <u>radice</u> ne è l'<u>elemento rappresentativo</u>. Perciò con $A = \{1 \ldots 9\}$ e partizioni $P = \{\{1,3,{\color{yellow}{7}}\}, \{{\color{yellow}{2}}\}, \{4,5,6,{\color{yellow}{8}},9\}\}$ si definisce un <u>array di padri</u> (o di radici) che per ogni elemento di $A$ indica il suo più alto antenato (root), ovvero l'<u>elemento rappresentativo</u>: $padri = [7,2,7,8,8,8,7,8,8]$.

Perciò nel caso specifico si hanno:

- `find(5,P) = 8` dato che l'elemento rappresentativo (root) della partizione in cui si trova 5 è 8.
- `union(1,2,P) =` $\{\{1,2,3,7\},\{4,5,6,8,9\}\}$ (unito le partizioni che contengono i valori 1 e 2).

##### Implementazione

```java
public class UnionFind {

	private int[] father, size;          // Father = array di padri / el. rappr. | size = contiene le size delle partizioni
	private int count;                   // N° partizioni
	
	public UnionFind(int n) {
		father = new int[n];
		size = new int[n];
		count = n;
		
		for (int i = 0; i < n; i++) {
			father[i] = i;                   // father contiene numeri da 1 a n (all'inizio n partizioni)
			size[i] = 1;                     // size contiene la lunghezza di ogni partizione (all'inizio tutte a 1)
		}
		
	}

	/*
	Facendo: " while (father[x] != x) { x = father[x]; } " ogni volta bisogna risalire il percorso per trovare il padre,
	perciò si usa la path compression per assegnare al valore cercato il suo padre finale
	*/
	public int Find(int x) {

		// while (father[x] != x)            // Finché x non è root (padre finale) --> ogni volta risale il path fino a root
		//     x = father[x];                // Assegna ad x il suo padre diretto

		if (father[x] != x)                  // Se x non è il padre
	        father[x] = Find(father[x]);     // Assegna al padre di x (corrente) il suo padre finale (cosi via ricorsivamente)
	        
		return x;
		
	}

	/*
	Prima senza il controllo della size delle partizioni si rischiava, in seguito ad una serie di Union() così:
	" Union(0,1); Union(0,2); ... Union(0,n); " di creare un albero degenere che non garantisce prestazioni O(log A).
	*/
	public void Union(int x, int y) {        // Unisce la partizione più piccola a quella più grande
		
		int rootX = Find(x);                 // Trova le partizioni di x e y
		int rootY = Find(y);

		if (rootX == rootY) 
			return;

		if (size[rootX] < size[rootY]) {     // Se part x < part y
			father[rootX] = rootY;           // padre di x = padre di y
			size[rootY] += size[rootX];      // Sommo a size part y la size della part x
		} else {
			father[rootY] = rootX;           // Viceversa ma x > y --> y vede padre sostituito e aumenta la size di x
			size[rootX] += size[rootY];
		}

		count--;                             // Unendo 2 partizioni ce n'è una in meno
			
	}

}
```

###### Bilanciamento

Grazie al **bilanciamento** fatto nella `Union()`, che garantisce che l'unione tra 2 partizioni avvenga sempre in modo che la minore sia unita alla maggiore, si risolve il problema delle `Union()` consecutive che portano ad un albero degenere, infatti col nuovo approccio si ottengono alberi con $n$ nodi e altezza max $\log_{2}(n)$.

> [!info] Nota
> Dato un **albero degenere** da 3 o + nodi, <u>NON esiste alcuna sequenza di union con bilanciamento che lo produca</u> (implica che dovrebbe agganciare un albero con 2 nodi sotto ad 1 con 1 nodo ma non è possibile in quanto il bilanciamento aggancia sempre le partizioni minori sotto quelle maggiori).

###### Path compression

In più, per merito della ***path compression*** implementata nella `Find()` adesso si risale l'intero albero solo 1 volta per trovare il padre della partizione in quanto durante la salita, ad ogni nodo incontrato si assegna come padre il padre finale della partizione.

##### Complessità Union-Find

`Union()` e `Find()`:

- Senza *path compression*: $O(\log n)$
- Con *path compression*: $O(\alpha(n))$, (dove $\alpha(n)$ è la ***funzione inversa di Ackermann***, una funzione che cresce molto lentamente tanto che con $n = 2^{65535} \rightarrow \alpha(n) \leq 5$).

> [!important] Teorema di Tarjan
> Avendo $\alpha(n)$ presa come funzione quasi costante e $m$ il numero di operazioni `Union()` e `Find()` eseguite, si ha che il costo di tali $m$ operazioni è:
> $$O(m \cdot \alpha(n))$$

#### Svolgimento esercizi

Gli esercizi generalmente prevedono che si facciano Union con bilanciamento su una sequenza illustrando alla fine l'albero risultante. Step:

1) Prendere i 2 parametri della union,
2) Per ognuno trovarne il padre (root),
3) Collegare il padre della partizione minore a quello della partizione maggiore (in caso size è uguale, usare il 1° parametro come il maggiore).

# Esercizi

###### 1) Union bilanciate

Partendo dalla partizione identità $\{\{1\} \ldots \{10\}\}$ esegui le seguenti `Union()` con bilanciamento:

Union(1,2)

Union(5,4)

Union(3,2)

Union(7,6)

Union(4,7)

Union(9,8)

Union(6,2)

Union(1,8)

Union(10,3)

# Soluzioni

###### 1)

Union(1,2), Union(5,4)

![](https://i.imgur.com/0wlNNY1.png)

Union(3,2), Union(7,6)

![](https://i.imgur.com/IHIrbq5.png)

Union(4,7), Union(9,8)

![](https://i.imgur.com/5Omc9sK.png)

Union(6,2)

![](https://i.imgur.com/NUXj7e0.png)

Union(1,8)

![](https://i.imgur.com/Uutghbj.png)

Union(10,3)

![](https://i.imgur.com/UIoDIAv.png)

---

Prossima lezione: [[19 - Algoritmi greedy]]

