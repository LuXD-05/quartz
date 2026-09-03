# Lezione 15

### Alberi 2-3

Gli **alberi 2-3** sono degli alberi particolari in cui <u>tutti gli elementi sono ordinati</u> e <u>risiedono solo nelle foglie</u> le cui, a loro volta, hanno sempre la <u>stessa profondità</u>. Caratteristiche:

- Ogni nodo interno ha **2 *label***:
  - A **sinistra**: con il <u>valore più grande del suo 1° sottoalbero</u>,
  - A **destra**: con il <u>valore più grande del suo 2° sottoalbero</u>.
- Ogni nodo interno ha **2 o 3 figli**:
  - Il 1° sottoalbero contiene <u>valori</u> $\leq$ <u>label sx</u>,
  - Il 2° sottoalbero contiene <u>valori</u> $\gt$ <u>label sx</u> e $\leq$ <u>label dx</u>,
  - Il 3° sottoalbero contiene <u>valori</u> $\gt$ <u>label dx</u> (se esiste).

##### Proprietà

Avendo $n$ <u>dati</u> in un'albero 2-3 di altezza $h$ si ha:

$$2^{h} \leq n \leq 3^{h}$$

Perciò:

$$h = \log(n)$$

Gli alberi 2-3 sono **bilanciati** (quelli la cui altezza è $O(\log(n))$).

##### Operazioni

###### Inserimento

Per <u>inserire un valore in un albero</u> si scende fino al nodo con *label* che dovrà ospitare il nuovo elemento (grazie a confronti basati sulle regole degli alberi 2-3) e a quel punto:

1) Il nodo ha <u>2 figli</u>: si inserisce l'elemento alla posizione giusta ed eventualmente si aggiornano le *label* fino alla radice,

   ![](https://i.imgur.com/7D99oRo.png)

2) Il nodo ha <u>3 figli</u>: si **splitta il nodo in 2**, il 1° con i 2 elementi e *label* <u>minori</u> ed il 2° con elementi e *label* <u>maggiori</u>; il tutto si ripete ricorsivamente fino alla radice (in caso il livello superiore abbia già 3 nodi...),

   ![](https://i.imgur.com/a22Oa5m.png)

###### Cancellazione

Per <u>cancellare un valore in un albero</u> si cerca il nodo con *label* a cui appartiene e a quel punto:

1) L'elemento da cancellare ha <u>2 fratelli</u>: lo si cancella ed eventualmente si aggiornano le *label* fino alla radice,

   ![](https://i.imgur.com/yWmcUIJ.png)

2) L'elemento da cancellare ha <u>1 fratello</u> (e non è root):

   - Un <u>fratello del padre ha 3 figli</u>: un opportuno nodo di tale fratello sostituisce il figlio appena cancellato:

     ![](https://i.imgur.com/8ZDFkbV.png)

   - <u>Nessun fratello</u> del padre <u>ha 3 figli</u>: il padre cede il figlio non cancellato ad un suo fratello ed eventualmente si ribilancia l'albero:

     ![](https://i.imgur.com/34yCqcu.png)

##### Codici di operazioni

###### Min e max

```java
public static void Min(Node n) {

	if (n == null) return null;    // Da null se vuoto

	while (n.first != null)        // Finché 1° figlio non è null
		n = n.first;               // n = il suo 1° figlio (e cosi via fino a foglia)

	return n;

}
public static void Max(Node n) {

	if (n == null) return null;    // Da null se vuoto

	while (n.second != null) {     // Finché 2° figlio non è null
	
		if (n.third == null)       // n = 2° o 3° figlio se ce e cosi via
			n = n.second;
		else 
			n = n.third;
			
	}

	return n;

}
```

###### Find

```java
// Ritorna il nodo contenente la foglia cercata
public static Node Find(Node n, T x) {

	if (n.first.isLeaf())                             // Se 1° figlio è una foglia --> ritorna n
		return n;

	if (x <= n.leftLabel)                             // Se x <= label sinistra --> find in 1° sottoalbero
		return Find(n.first, x);

	else if (x <= n.rightLabel || n.third == null)    // Se x <= label destra --> find in 2° sottoalbero
		return Find(n.second, x);

	else                                              // Se x > label destra --> find in 3° sottoalbero
		return Find(n.third, x);

}
// Per dire se un valore esiste nell'albero si usa:
public stativ boolean isMember(Node n, T x) {

	Node m = Find(n, x);              // Cerca il nodo interno in cui dovrebbe essere x

	return m.children.contains(x);    // Vede se i figli del nodo hanno x (forse si fa con "...stream(x -> x.value).contains(x)")

}
```

###### Insert

```java
public static void Insert(Node n, T x) {

	Node m = Find(n, x);

	if (!m.children.contains(x)) {
	
		// m.children.add(new Node(x));    // --> facendo finta che add lo aggiunga in ordine (senza auto-ridurre se 4 figli)

		Reduce(m);                         // Riduce se 4 figli
	
	}

}
```

###### Delete

```java
public static void Delete(T x) {

	// ???

}
```

###### Reduce

Quando dopo una `insert()` un nodo ha 4 figli, bisogna eseguire una riduzione, ovvero: 

```java
public static void Reduce(Node n) {

	if (n.children.size() == 4) {      // Solo se nodo ha 4 figli (troppo pieno)
	
		Node m = new Node();           // Crea m con 1° = n.first e 2° = n.second
		m.first = n.first;
		m.second = n.second;

		// Pare rimuova 1° e 2° da n (3° e 4° vanno al loro posto)    // Aggiorna figli di n e m + i parent di first e second (???)

		Node root;

		if (n.parent == null) {
		
			root = new Node();
			
			root.first = m.first;
			root.second = n.second;    //

			// Aggiorna i riferimenti ???
		
		} else {
		
			root = n.parent;           // Prende il padre
			
			// Add m immediatamente a sinistra di n

			Reduce(root);              // Continua a ridurre verso l'alto
		
		}

	}

}
```

# Esercizi

##### 1) Costruire alberi 2-3

###### 1.1) Costruire albero 2-3

Costruire l'albero 2-3 data la sequenza: (4, 8, 1, 10, 3, 2, 5, 6, 7, 9)

###### 1.2)

...

##### 2) Cancellazione in 2-3

###### 2.1) Cancellazione albero 2-3

...

# Soluzioni

##### 1)

###### 1.1)

(Non ho step di risoluzione)

![](https://i.imgur.com/goGJFL6.png)

##### 2)

###### 2.1)

![](https://i.imgur.com/fCos8QY.png)

![](https://i.imgur.com/9YrJaDK.png)

---

Prossima lezione: [[16 - Alberi 2-3-4]]

