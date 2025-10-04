# Lezione 14

### Binary search trees

Un BST (albero binario di ricerca) è un albero binario tale che:

- Ogni nodo $v$ contiene un elemento $u$,
- Se $x$ è l'elemento di un nodo del sottoalbero **sinistro** di $v$, allora $u > x$,
- Se $x$ è l'elemento di un nodo del sottoalbero **destro** di $v$, allora $u < x$.

###### Visita

I BST vanno visitati in ordine simmetrico (algoritmo ***[[11 - Attraversamento degli alberi#Inorder traversal|inorder]]***) siccome è con esso che si ottiene la sequenza ordinata.

![](https://i.imgur.com/dvLVYQl.png)

> [!info] Nota
> La costruzione di un BST con $n$ nodi ha un costo di $\Omega(n \log n)$ (per ogni valore, si fanno $\log(n)$ confronti per posizionarlo nel nodo corretto).

###### Sequenze di inserimento

Per creare un BST si prendono 1 a 1 gli elementi di una sequenza e li si inseriscono nei nodi corrispondenti in base a confronti (tipo se < del nodo, vai a sinistra). Però, ci possono essere <u>più ordinamenti di una sequenza che restituiscono la stessa struttura del BST</u> ed essi sono **tanti quante le foglie del BST**.

> [!important] Altezza BST
> L'altezza $h$ di un BST (dati $n$ nodi) è:
> $$\log_{2}(n) < h \leq n - 1$$
> Da un albero qualsiasi ad un **albero degenere** (sempre $h = n-1$), che ha anche sempre 1 sola sequenza associata.

###### Cancellazione in BST

La **cancellazione** di un valore in un BST si compone di 1) la **ricerca del valore** e 2) la **cancellazione del nodo** che lo contiene (<u>immediata se è una foglia</u>, altrimenti diventa necessario <u>trovare un sostituto</u>). Se il nodo ha 1 solo figlio, esso è il sostituto, altrimenti lo è il nodo che contiene `minmax(x)` o `maxmin(x)`.

###### Rotazione

La rotazione è un'operazione che coinvolge 2 nodi in relazione padre-figlio e li inverte:

- Rotazione destra: $x$ figlio sinistro di $y \;\rightarrow\; y$ diventa figlio destro di $x$:

  ![](https://i.imgur.com/ihWtOrV.png)

- Rotazione sinistra: $x$ figlio destro di $y \;\rightarrow\; y$ diventa figlio sinistro di $x$:

  ![](https://i.imgur.com/6aSRzSF.png)

###### Complessità

Dato un BST qualsiasi già ordinato:

Per il <u>caso peggiore</u> $O(n)$ per ogni operazione se il BST è un'albero degenere (vanno fatti al massimo $n$ confronti).

Per il <u>caso migliore</u> $O(1)$ (anche per `min()` e `max()`) e:

- **Ricerca**: quando si cerca la radice,
- **Inserimento**: quando si inserisce un valore < della radice e il minimo dell'albero è la radice stessa (inserisco subito dopo 1 confronto) e viceversa con > a destra,
- **Cancellazione**: quando si cancella una foglia.

> [!important] Complessità date sequenze casuali (in media)
> Data una sequenza casuale di lunghezza $n$:
> - Per <u>costruire il BST</u> la complessità è: $\Theta(n \log n)$,
> - Mentre il costo di <u>1 inserimento</u> è: $\Theta(\log n)$ (che è anche l'altezza media del BST).

##### Codici di operazioni

###### Search

```java
// Versione ricorsiva
public static Node BinarySearch(Node n, T x) {

	if (n == null) return null;

	// Ritorna valore se trova il nodo
	if (x == n.value)
		return n;

	// Se valore cercato minore ? cerca sinistra : cerca destra
	if (x < n.value)
		return BinarySearch(n.left, x);
	else 
		return BinarySearch(n.right, x);
		
}
// Versione iterativa
public static Node BinarySearch(Node n, T x) {

	Node m = n;

	while (m != null) {
	
		if (x == m.value)
			return m;

		if (x < n.value)
			m = n.left;
		else 
			m = n.right;
	
	}
		
}
```

###### Min e Max

```java
public static Node Min(Node n) {

	if (n == null)
		return null;

	Node m = n;

	while (m.left != null)    // Se ha nodo a sinistra, vuol dire che è < del corrente --> quindi lo prende come corrente
		m = m.left;

	return m;

}
public static Node Max(Node n) {

	if (n == null)
		return null;

	Node m = n;

	while (m.right != null)    // Se ha nodo a destra, vuol dire che è > del corrente --> quindi lo prende come corrente
		m = m.right;

	return m;

}
```

###### Visit

```java
// Corrisponde ad una vista inorder
public static void PrintTree(Node n) {

	if (n != null) {
	
		PrintTree(n.left);     // Stampa sottoalbero sinistro
		print(n.value);        // Stampa valore
		PrintTree(n.right);    // Stampa sottoalbero destro
	
	}

}
```

###### Insert

```java
// Versione ricorsiva
public static void Insert(Node n, T x) {

	if (x < n.value) {                // Se x < valore corrente
		if (n.left != null)           // Se ha già nodo a sinistra --> richiama insert
			Insert(n.left, x);
		else
			n.left = new Node(x);     // Lo assegna a n.left
	}

	if (x > n.value) {                // Se x > calore corrente
		if (n.right != null)          // Se ha già nodo a destra --> richiama insert
			Insert(n.right, x);
		else
			n.right = new Node(x);    // Lo assegna a n.right
	}
		

}
// Versione iterativa
public static void Insert(Node n, T x) {

	if (n == null)
		n = new Node(x);              // n == null --> crea nodo
	else {

		while (n != null) {           // Trova iterativamente l'ultimo nodo > o < di x
			Node m = n;
			if (x < n.value)
				m = n.left;
			else
				m = n.right;
		}

		if (x < m.value)              // Se ultimo > x ? mette a sinistra : mette a destra
			m.left = new Node(x);
		else
			m.right = new Node(x);

	}

}

// Insert con rotazioni (tipico di Treap Trees o Tango Trees)
public static Node InsertR(Node n, T x) {

	if (n == null)
		return new Node(x);                  // n == null --> crea nodo
	
	if (x <= n.value) {
		n.left = InsertRoot(n.left, x);      // 
		n = Rdx(n);
	} else {
		n.right = InsertRoot(n.right, x);    // 
		n = Rsx(n);
	}

	return n;

}
```

###### Remove

```java
// Cancella un nodo qualsiasi nel BST
public static void Delete(T x, Node n) {

	if (v != null) {
	
		if (x < n.value)                  // Cerca di cancellare a sinistra se <
			Delete(x, n.left);
			
		else if (x > n.value)             // Cerca di cancellare a destra se >
			Delete(x, n.right);
			
		else { // x == n.value

			if (n.children.length < 2)    // Remove(n) --> se ha 0 o 1 figlio
				Remove(n);
			
			else {
				Node max = Max(n.left)    // Massimo dei minimi (poteva anche fare "min = Min(n.right)" per minmax)
				n = max;
				Remove(max);
			}

		}
	
	}

}
// Cancella un nodo con 1 o 0 figli
public static void Remove(Node n) {

	if (n.children.length == 0)    // Nessun figlio --> rimuove
		Replace(n, null);

	else {

		Node m;

		if (n.left != null)        // Prende il figlio (sx o dx che sia)
			m = n.left;
		else
			m = n.right;

		if (n.parent == null)      // Se è root (non ha padre) rimpiazza con figlio
			n = m;
		else
			Replace(n, m);         // Se ha padre --> rimpiazzo a sx o a dx (in base a n se è a sx o a dx)

	}

}
// Sostituisce nodo n con nodo m
public static void Replace(Node n, Node m) {

	if (n.parent.left == n)    // Se n < padre (n è a sx) --> rimpiazza sx di padre con m | altrimenti rimpiazza dx di padre
		n.parent.left = m;
	else 
		n.parent.right = m;

	// Faccio finta che si aggiornino i riferimenti nel nodo cambiato cosi non devo riassegnare il padre
	
}
```

###### Rotate

```java
public static Node Rdx(Node n) {

	Node m = n.left;     // m = figlio sinistro di n
	n.left = m.right;    // figlio sinistro di n = figlio destro di m
	m.right = n;         // figlio destro di m = n
	return n;

}
public static Node Rsx(Node n) {

	Node m = n.right;    // m = figlio destro di n
	n.right = m.left;    // figlio destro di n = figlio sinistro di m
	m.left = n;          // figlio sinistro di m = n
	return n;

}
```

---

Prossima lezione: [[15 - Alberi 2-3]]

