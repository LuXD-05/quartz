# Lezione 11

### Tree Traversal Algorithms

Esistono degli algoritmi specifici per gli alberi detti **TTA** (*Tree Traversal Algorithms*) che sono adatti solo ad <u>alberi con radice ordinati</u> (alberi che hanno una radice da cui partono tutte le foglie e in cui l'ordine dei nodi conta). Per esempio:

![](https://i.imgur.com/YqPSu3H.png)

##### Preorder traversal

Il ***preorder*** si comporta in modo simile al [[10 - Attraversamento dei grafi#DFS|DFS]] ma visita subito ogni nodo per cui passa; quindi parte visitando la radice, continua per il percorso più a sinistra leggendo fino ad arrivare ad una foglia, momento in cui torna indietro e legge fino alla foglia il percorso a destra e così via fino a leggere tutto l'abero.

![](https://skilled.dev/images/pre-order-traversal.gif)

###### Preorder ricorsivo

```java
public void Preorder(Node n) {
	if (n != null)
		n.visit();    // Visita il nodo se != null
	 
	if (n.children.length() > 0) {
		for (Node child in children)
			Preorder(child);            // Applica preorder ricorsivamente ad ogni figlio
	}
}
```

###### Preorder iterativo

```java
public void Preorder(Node n) {
	Stack<Node> s = new Stack<Node>();
	
	if (n != null)
		s.push(n);              // Mette la root nello stack
		
	while (!s.isEmpty()) {
	
		n = s.peek();           // Prendo l'elemento in cima allo stack ("n = s.pop();" funziona già)
		s.pop();                // Rimuove l'elemento in cima allo stack
		
		n.visit();              // Visita l'elemento appena rimosso
		
		if (n.right != null)
			s.push(n.right);    // Se c'è un figlio a destra --> push in stack
		if (n.left != null)
			s.push(n.left);     // Se c'è un figlio a sinistra --> push in stack
			
	}
}
```

##### Postorder traversal

Il ***postorder*** è quasi uguale al *[[#Preorder traversal|preorder]]* solo che visita il nodo quando non ci sono più lati al di sotto di esso; quindi legge i nodi a sinistra finché non è ad una foglia, lì la visita e torna indietro andando a destra fino ad un'altra foglia, quando non ci sono più foglie non visitate in un sottoalbero ne legge la radice e così via fino a leggere la radice.

![](https://skilled.dev/images/post-order-traversal.gif)

###### Postorder ricorsivo

```java
public void Postorder(Node n) {
	if (n.children.length() > 0) {
		for (Node child : children)
			Postorder(child);        // Fa prima il postorder dei figli se il nodo ne ha
	}
	
	if (n != null)
		n.visit();                   // Poi visita i nodi
}
```

###### Postorder iterativo

```java
public void Postorder(Node n) {
	Stack<Node> s = new Stack<Node>();
	Stack<boolean> nonVisited = new Stack<boolean>();    // Non serve se classe Node ha prop "visited"

	if (n != null) {
		s.push(n);                  // Pusho root e segno come non visitata
		b.push(true);
	}

	while (!s.isEmpty()) {
		n = s.peek();               // Prendo e rimuovo il nodo in cima allo stack
		s.pop();
		
		if (b.pop()) {              // Se il bool in cima allo stack == true (+ lo rimuovo)
			s.push(n); 
			b.push(false);
			
			if (n.left != null)
				s.push(n.left);     // Se ha figlio a sx --> lo mette in stack
				b.push(true);
			if (n.right != null)
				s.push(n.right);    // Se ha figlio a dx --> lo mette in stack
				b.push(true);
			
		} else
			n.visit()               // Visito se n è da visitare
		
	}
}
```

##### Inorder traversal

L'***inorder*** è ancora simile ai precedenti solo che visita un nodo dopo aver visitato il suo sottoalbero sinistro e prima di visitare il sottoalbero destro.

![](https://skilled.dev/images/in-order-traversal.gif)

###### Inorder ricorsivo

```java
public void Inorder(Node n) {
	if (n.children.length() > 0) {
		Inorder(n.left);
		n.visit();
		Inorder(n.right);
	} else if (n != null) {
		n.visit()
	}
}
```

###### Inorder iterativo

```java
public void Inorder(Node n) {
	Stack<Node> s = new Stack<Node>();
	
	if (n != null)
		s.push(n);              // Mette la root nello stack
		
	while (!s.isEmpty()) {
		n = s.peek();           // Prendo l'elemento in cima allo stack ("n = s.pop();" funziona già)
		s.pop();                // Rimuove l'elemento in cima allo stack

		while (r != null) {
			s.push(n);
			n = n.left;         // Metto tutti i nodi del percorso a sinistra nello stack
		}

		if (!s.isEmpty()) {     // (Se ce ne sono di nodi a sinistra del precedente)
			n = s.peek();
			s.pop();            // Prendo e rimuovo il nodo in cima
			n.visit();          // Lo visito
			n = n.right;
			s.push(n);          // Metto il suo figlio a destra nello stack (e riparte il ciclo)
		}
		
	}
}
```

##### Levelorder traversal

Il ***levelorder*** invece è identico all'algoritmo [[10 - Attraversamento dei grafi#Graph Traversal Algorithms|BFS]] che è applicabile anche a certi tipi di grafi, seleziona i nodi ad ogni livello da sinistra a destra o viceversa.

###### Levelorder ricorsivo

###### Levelorder iterativo

```java
public void Levelorder(Node n) {
	Queue<Node> q = new queue<Node>();
	
	if (n != null)
		q.enqueue(n);              // Mette la root nella queue

	Node x;

	while (!q.isEmpty()) {
		x = q.front();             // Prendo il 1° elemento in coda + lo rimuovo + lo visito
		q.dequeue();
		x.visit();

		if (x.left != null)        // Se ha figlio sinistro --> lo aggiunge in coda
			q.enqueue(x.left);
		if (v.right != null)       // Se ha figlio destro --> lo aggiunge in coda
			q.enqueue(x.right);
	}
}
```

#### Complessità

Per ogni algoritmo dei precedenti: 

- Ogni nodo fa parte di 1 sola chiamata ricorsiva/iterazione,
- Ogni nodo viene visitato solo 1 volta, quindi le operazioni sui nodi hanno tutte costo $O(1)$.

> [!info] Quindi
> La complessità in tempo è $\Theta(n)$, mentre quella in spazio è $O(n)$.

---

Prossima lezione: [[12 - Intro ordinamento]]

