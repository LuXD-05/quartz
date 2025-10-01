# Esami

### Notazioni asintotiche

##### Notazioni

Eventualmente dire definizioni delle notazioni asintotiche $O$, $\Omega$ e $\Theta$.

##### Asserzioni

Seguire gli step:

1) Semplificare le espressioni mantenendo solo i termini di crescita più alta,
2) Confrontare i tassi di crescita (stabilire se $O$, $\Omega$ o $\Theta$) e vedere se combacia con l'asserzione,
3) Basta.

###### Esempi asserzioni

![](https://i.imgur.com/z7OLusq.png)

### RAM e RASP

##### Differenza tra RAM e RASP

Le macchine RAM e RASP sono entrambe composte da nastri di input e output, registri e un programma da eseguire fatto di istruzioni elementari, le uniche differenze sono che la RAM ha programma fisso e dispone di indirizzamento indiretto (`*i`), mentre RASP permette la modifica delle istruzioni a runtime (dato che il programma è salvato nei registri) e non ha indirizzamento indiretto.

##### Criteri di costo

Differenza tra CCU e CCL? Quando applicare il 1° e quando il 2°? Esempio di istruzione RAM differente nei 2 modelli?

Secondo il CCU, il costo di ogni istruzione RAM è 1 in termini di tempo, stessa cosa per i registri dove ognuno costa 1 in spazio; questa metodologia è affidabile solo quando la dimensione dei dati del programma è trascurabile e/o non cresce troppo.

In caso contrario è più indicativo l'utilizzo del CCL, in quanto tiene conto della dimensione degli operandi (intesa come il numero di bit, ovvero il logaritmo in base 2 di essa).

Un esempio di istruzione RAM può essere `LOAD 8` (con R8 che contiene 128), la quale in CCU costa 1, mentre in CCL il costo sarà: $\log_{2} 8 + \log_{2} 128 = 3+7 = 10$.

##### Stati

###### Stati 1

Considerando uno stato $S$ dove $S(0) = 128$, $S(8) = 256$ e $S(256) = 512$, determinare il costo dell'istruzione RAM `add *8` secondo CCU e CCL.

CCU = 1

CCL = log 128 + log 8 + log 256 + log 512 = 7 + 3 + 8 + 9 = 27?

###### Stati 2

Considerando uno stato $S$ dove $S(0) = 16$, $S(8) = 32$ e $S(32) = 64$, determinare il costo dell'istruzione RAM `sub *8` secondo CCU e CCL.

##### Programma RAM/RASP

Scrivere un programma RAM che accetta in input un intero $n$ e restituisce $n^{n}$ + complessità secondo i 2 costi.

![](https://i.imgur.com/wVcUTEj.png)

### Grafi

##### Rappresentazioni

Metodi di rappresentazione di grafi + vantaggi e svantaggi?

Un grafo può essere rappresentato attraverso liste o matrici di adiacenza:

![](https://i.imgur.com/XLOqCKS.png)

Dove $n$ è il n° di nodi, $m$ è il n° lati. Grafo è denso se $m > n$ e sparso se viceversa.

##### Algoritmo visita grafo

Se viene chiesto algoritmo di visita di un grafo o è specificato il BFS o è meglio scrivere il BFS, quindi domanda: mostrare procedura di visita in ampiezza di un grafo + analizzarne la complessità (tempo) con $n$ nodi e $m$ lati.

###### Codice

```java
public static void BFS(Graph g) {

	// Coda nodi da visitare + array che segna se nodo visitato
	Queue<Node> q = new Queue<Node>();
	boolean[] visited = new boolean[g.nodes.size()]
	
	// No nodes visited
	for (n in g.nodi)
		visited[n] = false;
		
	// Except 1st (visited)
	Node n = g.nodes[0];
	visited[n] = true;
	q.enqueue(n);

	while (!q.isEmpty()) {

		// Gets (removes from q) & visits 1st node
		n = q.remove();
		n.visit();

		// Adds adjacents in q (+ sets as visited)
		for (m in n.getAdjacentNodes())
			if (!visited[m]) {
				q.enqueue(m);
				visited[m] = true;
			}
	}

}
```

In pratica:

1) Si setta un array `visited` tutto a false per dire che nessun nodo ancora visitato (eccetto per la root che si visita subito),
2) Finché coda di nodi da visitare (`q`) ha nodi da visitare: prendi da coda, visita nodo preso e aggiungi gli adiacenti non ancora visitati (+ setta `visited` a true per essi).

###### Complessità

Dall'algoritmo si hanno:

- 1 ciclo `for` che segna tutti gli $n$ nodi a non visitati (eccetto il primo) = $\Theta(n)$,
- 1 ciclo `for` che per ogni nodo visita gli adiacenti, ovvero visita ognuno degli $m$ lati = $\Theta(m)$

Quindi la complessità finale sarà $\Theta(n + m)$.

### Alberi

#### Esercizi alberi

Semplici esercizi di costruzione di alberi + cancellazione finale.

##### 2-3

Label con sempre 2 valori e 2-3 figli. Le lettere di ogni label sono la maggiore del 1° sottoalbero e del 2° sottoalbero (3° non interessa mai).

Si parte con nodo con 2 valori e si inserisce ogni volta ripartendo a ricostruirlo dal basso (per semplicità).

##### 2-3-4

Nodi con 1, 2 o 3 valori e figli sempre = a n° valori + 1.

##### RB

Nodi con collegamento rosso o nero. Da root a ogni foglia bisogna avere sempre lo stesso numero di lati neri.

Ogni nodo che si inserisce è una foglia rossa, poi si ricolora e ribilancia eventualmente.

Se un sottoalbero necessita di + collegamenti neri dell'altro (dello stesso livello) allora va ribilanciato l'albero con rotazioni.

##### Altri

Tipo alberi binari o dire quale sequenza produce il seguente albero binario (soluzione: BFS dell'albero stesso).

#### Teoria alberi

##### Attraversamento

Mostrare codice di una procedura per l'attraversamento di un albero:

```java
public void Preorder(Node n) {

	if (n != null)
		n.visit();
	 
	if (n.children.length() > 0) {
		for (Node child in n.children)
			Preorder(child);
	}
	
}

public void Postorder(Node n) {

	if (n.children.length() > 0) {
		for (Node child : n.children)
			Postorder(child);
	}
	
	if (n != null)
		n.visit();
		
}

public void Inorder(Node n) {

	if (n.children.length() > 0) {
		Inorder(n.left);
		n.visit();
		Inorder(n.right);
	} else if (n != null) {
		n.visit()
	}
	
}

public void Levelorder(Node n) {

	Queue<Node> q = new Queue<Node>();
	
	if (n != null)
		q.enqueue(n);

	Node x;

	while (!q.isEmpty()) {
	
		x = q.front();
		q.dequeue();
		x.visit();

		if (x.left != null)
			q.enqueue(x.left);
		if (x.right != null)
			q.enqueue(x.right);
			
	}

}
```

Tutti tempo e spazio: $\Theta(n)$ e $O(n)$.

- **Preorder**: visita prima di passare al figlio sinistro e se non deve più visitare niente a sinistra passa a visitare a destra.
- **Postorder**: scende finché non c'è un nodo con figli già visitati o nulli, lo visita e torna indietro.
- **Inorder**: visita sottoalbero sinistro, visita il nodo, visita il sottoalbero destro.
- **Levelorder**: visita i nodi di un livello nel mentre che si segna quelli del prossimo, poi rifà per quelli segnati fino alle foglie.

##### Altezze e altro

###### Albero n-ario di altezza h

Quanti nodi al massimo può contenere un albero n-ario di altezza $h$?

Il n° massimo di nodi dell'albero = ai nodi di un albero completo di grado $n$ con tutti i livelli saturi. Dato che ogni livello $i$ ha $n^{i}$ nodi si ha:

$$\sum\limits_{i=0}^{h} n^{i} = \dfrac{k^{h+1}-1}{k-1}$$

###### Albero binario pieno con n nodi

Albero binario = ogni nodo max 2 figli, pieno significa saturo in tutti i livelli tranne eventualmente l'ultimo, quindi, ipotizzando un'altezza $h$ e n° nodi $n$:

$$2^{h} -1 < n \leq 2^{h+1} - 1$$

Quindi l'altezza è $h \approx \log_{2}(n)$.

###### Albero binario degenere

Definisci albero binario degenere e quanti ce ne sono con $n$ nodi.

Un albero binario degenere è un albero che ha $n$ nodi ed altezza $n-1$ (ogni nodo ha un solo figlio, in pratica è una lista). Dati $n$ nodi possono esistere massimo $2^{n-1}$ alberi binari degeneri perché dopo aver inserito il 1° nodo, posso scegliere solo il nodo destro o sinistro per tutti i prossimi $n-1$ inserimenti, quindi le possibili combinazioni diventano $2^{n-1}$.

###### Altezza max e min di albero 2-3-4

Un albero 2-3-4 con $n$ nodi ha altezza massima solo se ogni nodo ha 2 figli, ovvero corrisponde ad un albero binario completo; perciò dato $2^{h}-1 <n \leq 2^{h+1}-1$ si ha che:

$$h = \log_{2}n$$

Uno con l'altezza minima invece ha solo nodi con 4 figli (albero quaternario completo), quindi dato $\frac{4^{h}-1}{3} < n \leq \frac{4^{h+1}-1}{3}$ si ha che:

$$3n + 1 \leq 4^{h+1} \;\;\;\rightarrow\;\;\; \log_{4}(3n+1) \leq h + 1 \;\;\;\rightarrow\;\;\; h \geq \log_{4}(n) + \log_{4}(3) -1$$

###### Altezza di RB con n valori

![](https://i.imgur.com/Jz6Spk7.png)

###### Altezza 2-3

$$2^{h} \leq n \leq 3^{h}$$

##### Definizioni

###### BST

Un BST è un albero binario con le seguenti caratteristiche:

- Ogni nodo contiene un valore,
- Ogni nodo ha 2 figli,
- Figlio sx < padre < figlio dx (e questo vale per ogni valore dell'albero).

###### 2-3-4

Un albero 2-3-4 è un'albero con radice ordinato in cui:

- Ogni nodo contiene $i$ valori (da 1 a 3) e possiede max ${} i+1$ figli,
- Tutte le foglie sono allo stesso livello,
- I sottoalberi "prima" di un valore (padre) contengono solo valori < di esso, mentre quelli "dopo" un valore (padre) contengono solo valori >.

###### RB

Un albero RB è un albero binario di ricerca in cui:

- Ogni nodo ha un valore e un colore (rosso o nero) che indica il colore del lato che lo collega al padre,
- Non possono esserci 2 lati rossi consecutivi,
- Ogni percorso da radice a foglia deve avere lo stesso n° di lati neri.

### Algoritmi di ordinamento

#### Teoria algoritmi ordinamento

##### Caratteristiche

- **Stabile**: non scambia valori uguali,
- **Adattivo**: più è ordinato l'input meno confronti effettua,
- **Ottimale**: complessità $O(n \log n)$ nel caso peggiore.

##### Confronti e scambi

###### Teorema del lower bound

Qual è il numero minimo di confronti che qualunque algoritmo della classe "confronti e scambi" deve effettuare (nel caso peggiore) per ordinare un vettore di $n$ elementi?

Supponiamo di dover ordinare una sequenza di $n$ elementi indefiniti, i possibili ordinamenti di essa si dicono **permutazioni** e sono $n!$. Tali possono essere rappresentati come foglie di un albero (binario) decisionale, dove in ogni nodo interno vi sono delle condizioni che alla fine conducono ad una certa foglia (1 per percorso).

Dato che $2^{h} \geq n! \implies h \geq \log_{2}(n!)$, ovvero il n° di confronti di un percorso per arrivare ad una permutazione sarà sempre $\leq h$. Da ciò si ha che:

$$\log_{2}(n!) \approx n\log_{2}n + o(n\log_{2}n) \approx n\log n$$

Perciò, il minimo n° di confronti che un algoritmo ... nel caso peggiore è $\Omega(n \log n)$.

##### Digitali

###### Ordinamento elementi con ripetizioni

Qual è l'algoritmo migliore per ordinare i voti totali degli alunni in una scuola (con ripetizioni)?

#### Pratica algoritmi ordinamento

##### Complessità

![](https://i.imgur.com/7Uz7WjJ.png)

##### Equazioni di ricorrenza

###### Mergesort

Scrivere l'equazione di ricorrenza del mergesort.

### Hash

##### Funzione hash

###### Caratteristiche funzione hash

Una funzione hash è usata per trovare l'indice $i$ di una chiave $c$ in una tabella hash $T$ e ha 3 caratteristiche:

1) **Efficienza**: essere <u>facile/veloce da calcolare</u> (costo $O(|c|)$ che è la lunghezza di $c$),
2) **Distribuzione uniforme**: delle chiavi su $n$ indirizzi (hashando una chiave, <u>ogni indirizzo deve avere la stessa probabilità</u> $\tfrac{1}{n}$ <u>di essere scelto</u>),
3) **Determinismo**: l'indirizzo calcolato deve dipendere da tutti i bit di $c$, perciò la <u>stessa chiave da sempre lo stesso risultato</u>.

###### Esempio di funzione hash

Una funzione hash prende in ingresso chiavi che sono parole dell'alfabeto e per rispettare le regole: 1) basta ciclare per ogni carattere (no algoritmi pesanti) per avere complessità $O(n)$, 2) usare numeri primi come moltiplicatori (aiutano a non far finire le chiavi sempre negli stessi posti) e 3) usare la regola di Horner per dipendere da tutti i caratteri (facendo in modo che abbiano peso diverso):

```java
/*
1) Il for cicla per ogni lettera --> complessità O(n)
2) 17 e DIMTAB (si suppone che siano) primi fra loro
3) Con Horner (n = ... * n ...) ogni char è moltiplicato per il valore ricavato dai precedenti
*/
public int Hash(String s) {

	int n = 0;
	
	for (int i = 0; i <= s.length(); i++)
		n = (17 * n + (int)s.charAt(i))	% DIMTAB;
		
	return n;

}
```

##### Tipi di hash

###### Differenza tra indirizzamento diretto e concatenazioni separate

In una tabella hash ad **indirizzamento aperto** i dati risiedono direttamente nella tabella, mentre in quella a **concatenazioni separate** la tabella contiene in ogni posizione (un riferimento al 1° nodo di) una lista concatenata in cui vi si salvano i dati.

In concatenazioni separate l'unica preoccupazione è, a fronte di stima errata, il decadimento delle prestazioni (con liste più lunghe ci vuole più tempo per trovare i valori); mentre in indirizzamento aperto, oltre sempre al decadimento delle prestazioni in seguito alla crescita del fattore di carico $\alpha$, c'è un rischio sempre maggiore di collisioni man mano che si arriva alla sua saturazione ($\alpha = 1$).

Questi problemi non si pongono invece quando si usano tabelle hash dinamiche invece che statiche, in quanto prima della saturazione le tabelle vengono espanse.

### Union-Find

##### Teoria

###### Implementazione Union-Find

Mostrare un'implementazione <u>efficiente</u> (tip: con bilanciamento) di Union e Find (+ sottinteso dire costi/complessità?) (+ se non chiede path compression non farla).

```java
public class UnionFind {

	int[] father, size;
	int count;

	public UnionFind(int n) {

		father = new int[n];
		size = new int[n];
		count = n;

		for (int i = 0; i < n; i++) {
			father[i] = i;
			size[i] = 1;
		}

	}

	public static int Find(int x) {

		while (father[x] != x)
			x = father[x];

		return x;

	}

	public static void Union(int x, int y) {

		int rootX = Find(x);
		int rootY = Find(y);

		if (rootX == rootY) return;

		if (size[rootX] >= size[rootY]) {
			father[rootY] = rootX;
			size[rootX] += size[rootY];
		} else {
			father[rootX] = rootY;
			size[rootY] += size[rootX];
		}

		count--;

	}

}
```

Complessità `Union()` e `Find()` = $O(\log n)$

##### Pratica

###### Partizioni 1

Data la partizione identità $\{\{1\}, \ldots \{5\}\}$ dire se è possibile ottenere il seguente albero:

![](https://i.imgur.com/kmVTkyp.png)

L'albero in figura è teoricamente ottenibile solamente usando `Union()` <u>senza bilanciamento</u>, infatti tramite quelle sarebbe possibile unire (parlando di partizioni) 5 a 2 e poi "2 -> 4 -> 1 -> 3" con la serie di `Union`: $(2,5), (2,4), (4,1), (1,3)$). In caso le `Union()` fossero bilanciate, non sarebbe in alcun modo possibile costruire il sottoalbero degenere "4 -> 1 -> 3" in quanto ad ogni `Union()` al padre della partizione più piccola verrebbe assegnato come padre quello della partizione più grande.

###### Partizioni 2

Partendo da una partizione identità è possibile, solo tramite Union <u>con bilanciamento</u>, ottenere il seguente albero?

![](https://i.imgur.com/hkuAHTt.png)

No, usando solo `Union()` con bilanciamento non è possibile ottenere tale albero, men che meno un qualsiasi albero degenere in quanto, dato che è l'albero più piccolo che viene "collegato" a quello piu grande ogni volta, è praticamente impossibile ottenere una struttura del genere seguendo tale regola.

### Algoritmi greedy

##### Teoria

###### Sistemi di indipendenza e problemi di ottimizzazione

Definisci cos'è un sistema di indipendenza e un problema di ottimizzazione. Poi scrivi l'algoritmo di una procedura greedy generica che risolve un problema di ottimizzazione.

Un sistema di indipendenza è una coppia $(E,F)$ dove $E$ è un insieme di elementi ed $F$ contiene sottoinsiemi "validi" di $E$, ovvero che rispettano certe regole. Un problema di ottimizzazione coinvolge un sistema di indipendenza, una **funzione peso** $w$ che associa ad ogni elemento di $E$ un "peso" ed un insieme $M \in F$ avente il peso massimo tra tutti: l'obiettivo è trovare $M$ (formato dagli elementi con peso massimo) tra tutti gli elementi di $E$ in modo tale che esso sia valido.

```java
public Set Greedy(Set E, Set F, func w) {
	Set M = emptyset();

	while (!E.isEmpty()) {
		
		var m = max(E, w);
		E -= {m};

		if ((M+{m}) in F)
			M.add(m);
		
	}

	return M;
}
```

###### Kruskal

```java
public Set Kruskal(Set V, Set E, func w) {

	Set MST = emptyset();
	Partition p = new Partition(E.size());
	Edge e;

	while (p.count > 1) {
	
		e = min(E, w);
		E.delete(e);

		if (p.Find(e.from) != p.Find(e.to)) {
			p.Union(e.from, e.to);
			MST.add(e);
		}
	
	}

	return MST;

}
```

###### Prim e Dijkstra

Bigliettini fr.

Complessità Prim: dati $m$ lati e $n$ nodi si ha complessità: $\Theta(m \log n)$ siccome ogni lista di adiacenza è visitata una volta e l'aggiunta costa $\log n$.

##### Pratica

###### Kruskal 1

###### Prim 1

Esegui Prim con nodo sorgente **C** e mostra la soluzione parziale ad ogni iterazione. Complessità dati $m$ lati ed $n$ nodi e perché?

![](https://i.imgur.com/CpvRoo8.png)

$S1 = \{\{C,H\}\}$

$S2 = S1 \cup \{\{G,H\}\}$

$S3 = S2 \cup \{\{D,G\}\}$

$S4 = S3 \cup \{\{B,D\}\}$

$S5 = S4 \cup \{\{E,G\}\}$

$S6 = S5 \cup \{\{A,D\}\}$

$S7 = S6 \cup \{\{C,F\}\}$

$S8 = S7 \cup \{\{H,I\}\}$

### Programmazione dinamica

# Esercizi

# Soluzioni

```java
public (int,int) MinMax(int[] A, int left, int right) {
    
    // Caso 1 elemento
    if (left == right)
        return (A[left], A[left]);

    // Caso 2 elementi
    if (right == left + 1) {
        if (A[left] < A[right])
            return (A[left], A[right]);
        else
            return (A[right], A[left]);
    }

	// Calcola mid
    int mid = (left + right) / 2;

	// Trova min e max a sinistra e a destra di mid (ricorsivo)
    int (minSx,maxSx) = MinMax(A, left, mid);
    int (minRx,maxRx) = MinMax(A, mid+1, right);

	// Prende min e max confrontando i min e i max di sinistra e destra
	int min = (minSx < minRx ? minSx : minRx);
	int max = (maxSx > maxRx ? maxSx : maxRx);

    return (min, max);
    
}
```

