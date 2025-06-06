# Lezione 13

### Algoritmi elementari

##### Selection sort

Il ***selection sort***, per ogni elemento (1° ciclo esterno), si scorre tutto l'array in cerca del minimo (2° ciclo interno) e lo mette alla posizione corrispondente all'indice del 1° ciclo esterno (quindi li ridispone in ordine dal 1° all'ultimo elemento).

Perciò al 1° ciclo esterno inizia salvandosi il 1° elemento e scorre dal 2° all'ultimo per trovare il minimo. Quando lo trova lo inserisce in 1a posizione e riparte salvando ora l'elemento in 2a posizione e scorrendo dal 3° alla fine per trovare il minimo e così via fino alla fine.

```java
public class Selection {

	public static void sort(Comparable[] arr) {

		int n = arr.length;
		for (int i = 0; i < n; i++) {
		
			int min = i;                       // Salvo l'indice dell'elemento corrente (x forza il minimo dato che è il 1°)
			
			for (int j = i+1; j < n; j++)      // Dal successivo alla fine:   se arr[j] < minimo   -->   minimo = arr[j]
				if (less(arr[j], arr[min]))
					min = j;
			
			exchange(arr, i, min);             // Metto arr[min] in posizione i
			
		}

	}

}
```

![](http://www.xybernetics.com/techtalk/SortingAlgorithmsExplained/images/SelectionEg02.gif)

> [!info] Complessità *selection sort*
> Considerando tutti i casi la complessità del <u>selection sort</u> è $\Theta(n^{2})$, siccome:
> - Fa $\dfrac{n(n-1)}{2} = \Theta(n^{2})$ confronti,
> - Fa $n-1 = \Theta(n)$ scambi.

###### Caratteristiche selection sort

**Stabile**: `less()` non scambia valori uguali.

##### Insertion sort

L'***insertion sort*** per ogni elemento confronta esso ed il precedente e li scambia se non sono ordinati.

```java
public class Insertion {

	public static void sort(Comparable[] arr) {

		int n = a.length;

		for (int i = 1; i < n; i++) {

			int j = i;                                   // Prende l'indice dell'elemento corrente

			while (j > 0 && less(arr[j], arr[j-1])) {    // Scambia dall'indice all'indietro finché arr[j-1] < arr[j] (o arriva a fine)
				exchange(arr, j, j-1);
				j--;
			}

		}

	}

}
```

![](https://markbowman.org/LCC/SortInsertion.gif)

> [!info] Complessità *insertion sort*
> Caso migliore (vettore ordinato): $\Theta(n)$ confronti e $0$ scambi.
> Caso peggiore (vettore al contrario): $\Theta(n^{2})$ confronti e scambi.
> In ogni caso la complessità è: $O(n^{2})$.

###### Caratteristiche insertion sort

**Stabile**: `less()` non scambia valori uguali.

**Adattivo**: con `less(arr[j], arr[j-1])`, si ferma prima di confrontare tutti i valori dell'array all'indietro e smette di scambiare dove è arrivato.

##### Bubble sort

Il ***bubble sort*** per ogni elemento `i`, parte dall'ultimo della sequenza e lo scambia al max fino ad `i` fino ad ordinare la sequenza.

```java
public class Bubble {

	public static void sort(Comparable[] arr) {

		int n = arr.length;

		for (int i = 0; i < n; i++) {          // Scorre ogni elemento dal 1° a ultimo
		
			for (int j = n-1; j > i; j--) {    // (Per ogni elemento) ri-scorre da ultimo ad arr[i]
		
				if (less(arr[j], arr[j-1]))    // Se arr[j] < arr[j-1] --> li scambia
					exchange(arr, j, j-1);
		
			}
		
		}

	}

}
```

> [!info] Complessità *bubble sort*
> Complessità: $\Theta(n^{2})$.

###### Bubble sort adattivo

La versione adattiva del ***bubble sort*** lo rende capace di "accorgersi" di quando non può più scambiare l'elemento corrente coi precedenti e lì passa all'elemento successivo.

```java
public class Bubble {

	public static void sort(Comparable[] arr) {

		int n = arr.length;
		boolean ex;                            // Tiene conto di uno scambio

		for (int i = 0; i < n; i++) {          // Scorre ogni elemento dal 1° a ultimo

			ex = false;

			for (int j = n-1; j > i; j--) {    // (Per ogni elemento) ri-scorre da ultimo ad arr[i]
		
				if (less(arr[j], arr[j-1])) {  // Se arr[j] < arr[j-1] --> li scambia
					exchange(arr, j, j-1);
					ex = true;
				}

				if (!ex) break;                // Se non scambia (elemento già in ordine) --> passa al ciclo successivo
		
			}
		
		}

	}

}
```

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*7seGXJi3te9beNfpAvFXEQ.gif)

> [!info] Complessità *bubble sort* (adattivo)
> Caso migliore: $\Theta(n)$.

###### Caratteristiche bubble sort

**Stabile**: `less()` non scambia valori uguali.

**Adattivo**: (solo la versione adattiva) quando arriva ad elementi già ordinati all'inizio della sequenza passa al ciclo successivo.

##### Merge sort

Il ***merge sort*** si basa sulla tecnica di progettazione e risoluzione di algoritmi nota come ***divide et impera*** dove *divide* significa <u>spezzare un problema in sottoproblemi più piccoli</u> mentre *impera* significa <u>risolvere (ricorsivamente) i sottoproblemi ed unirne le soluzioni parziali alla fine per risolvere il problema di partenza</u>.

L'algoritmo infatti spezza una sequenza a metà ricorsivamente e ricomponendola la riordina.

```java
public class Merge {

	// Funzione mergesort --> Iterable<T> è per gestire sia array che liste (usare Comparable[] in esame)
	public static void sort(Iterable<T> arr, int low, int high) {

		if (high <= low) {
		
			int mid = low + (high - low) / 2;    // Calcola il punto medio
			
			sort(arr, low, mid);                 // (ri)splitta la 1a metà
			sort(arr, mid+1, high);              // (ri)splitta la 2a metà
			
			merge(arr, low, mid, high);          // (ri)mergia le 2 metà appena splittate
		
		}

	}

	// Merge di array
	public static void merge(Comparable[] arr, int low, int mid, int high) {

		Comparable[] temp = new Comparable[arr.length];
		int i = low, j = mid + 1;               // i = counter all'inizio della 1a metà | j = counter all'inizio della 2a metà

		for (int k = low; k <= high; k++)       // Carico tutto temp[] coi valori di arr[]
			temp[k] = arr[k];
			
		for (int k = low; k <= high; k++) {
		
			if (i > mid)                        // 3) finito di ciclare sulla 1a metà --> prendo la 2a
				arr[k] = temp[j++];
				
			else if (j > high)                  // 4) finito di ciclare sulla 2a metà --> prendo la 1a
				arr[k] = temp[i++];
				
			else if (less(temp[j], temp[i]))    // 1) temp[j] < temp[i] --> lo metto prima (e incremento j)
				arr[k] = temp[j++];
				
			else                                // 2) temp[i] < temp[j] --> lo metto prima (e incremento i)
				arr[k] = temp[i++];
		
		}

	}

	// Merge di liste
	public static List<Comparable> merge(List<Comparable> a, List<Comparable> b) {

		List<Comparable> c = new ArrayList<>();

		// Ritorna a se b vuota e viceversa
		if (a.isEmpty()) return b;
		if (b.isEmpty()) return a;

		// Prende 1° elemento di a e b
		Comparable x = a.get(0);
		Comparable y = b.get(0);

		while (x != null && y != null) {
		
			if (less(x,y)) {    // x < y --> 1) metto x in c 2) rimuovo il 1° elemento (x) da a 3) (ri)prendo il 1° elemento in a
				c.add(x);        
				a.remove(0);     
				x = a.get(0);
			} else {            // y < x --> 1) metto y in c 2) rimuovo il 1° elemento (y) da b 3) (ri)prendo il 1° elemento in b
				c.add(y);
				b.remove(0);
				y = b.get(0);
			}
		
		}

		if (x == null)          // Se finita a --> c + b
			c.addall(b);
		else                    // Se finita b --> c + a
			c.addAll(a);

		return c;

	}

}
```

![](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif)

> [!info] Complessità *merge sort*
> `merge()` = $O(a+b)$ (con $a$ e $b$ 2 sequenze siccome le unisce).

###### Caratteristiche merge sort

**Stabile**: `less()` non scambia valori uguali.

###### Merge sort ricorsivo

```java
public static void sort(Comparable[] arr) {

	int n = arr.length, length, low, mid, high;
	Comparable[] temp = new Comparable[n];
	
	for (length = 1; length < n; length *= 2) {
	
		for (low = 0; low < n - length; low += length + length) {
		
			mid = low + length - 1;
			high = Math.min(low + length + length - 1, n - 1);
			merge(a, temp, low, mid, high);

		}
	
	}

}
```

Complessità in tempo: $\Theta(n \log n)$ e in spazio: $\Theta(n)$.

##### Quick sort

Il ***quick sort*** rientra negli algoritmi che usano la tecnica *divide et impera* e funziona così: si sceglie un elemento della sequenza detto `pivot` (che spesso viene messo all'inizio o fine della sequenza) poi si trova il 1° elemento < del `pivot` da sinistra e il 1° > del `pivot` da destra; se il maggiore è a sinistra del minore (o viceversa) li si scambia fin quando non si arriva all'ultimo elemento rimasto, il quale si scambia col `pivot`. 

A quel punto si avranno la partizione sinistra con elementi tutti minori del `pivot`, il `pivot` stesso e la partizione destra con elementi maggiori del `pivot`; da qui si procede ricorsivamente richiamando *quicksort* per le 2 partizioni.

```java
public class Quick {

	public static void sort (Comparable[] arr) {
		sort(arr, 0, arr.length - 1);
	}

	// Ricorsiva
	public static void sort(Comparable[] arr, int l, int r) {

		if (r <= l) return;                // Esce se arr da 0 o 1 elementi

		int pivot = partition(a, l, r);    // Mette il pivot nella posiz. giusta e crea 2 partizioni: left < pivot e right > pivot

		sort(arr, l, pivot - 1);           // Sorta da inizio (left) al pivot
		sort(arr, pivot + 1, r);           // Sorta dal pivot a fine (right)

	}

	// Iterativa
	public static void sort(Comparable[] arr, int l, int r) {

		int i;
		Stack<Integer> s = new Stack<>();

		if (r <= l) return;              // Esce se arr da 0 o 1 elementi

		s.push(l);                       // Metto il 1° range nello stack (da l a r)
		s.push(r);

		while (!s.isEmpty()) {
		
			r = s.pop();                 // Prendo l'ultima coppia di indici nello stack (= range da ordinare)
			l = s.pop();

			i = partition(arr, l, r);    // Partiziona: pivot in posiz. giusta, con elementi < a sinistra e > a destra

			if (i - l > r - i) {         // Ordina sinistra se > di destra e viceversa
			
				s.push(l);               // Metto in stack il range di sinistra
				s.push(i-1);
				
				if (i + 1 < r) {
					s.push(i+1);         // Aggiunge anche il range di destra eventualmente (lo fa prima perché + piccolo?)
					s.push(r);
				}
			
			} else {
			
				s.push(i+1);             // Metto in stack il range di destra
				s.push(r);
				
				if (i - 1 > 1) {
					s.push(l);           // Aggiunge anche il range di destra eventualmente (lo fa prima perché + piccolo?)
					s.push(i-1);
				}
			
			}
			
		
		}

	}

	public static int partition(Comparable[] arr, int l, int r) {
	
		int i = l, j = r + 1;
		Comparable v = arr[l];           // Prende il 1° elemento di arr come pivot

		while (true) {
		
			while (less(arr[++i], v))    // Trova il 1° elemento da sinistra ≥ pivot (il suo indice in i)
				if (i == r) 
					break;
					
			while (less(v, arr[--j]))    // Trova il 1° elemento da destra ≤ pivot (il suo indice in j)
				if (j == l) 
					break;
					
			if (i >= j)                  // Se elemento sx > elemento dx --> esce (sono ordinati)
				break;
				
			exchange(arr, i, j);         // Se elemento sx < elemento dx --> li scambia e continua
		
		}

		exchange(arr, l, j);             // Scambia il pivot e l'ultimo elemento fuori posto (ordinato)
		return j;
	
	}

}
```

Nela versione ricorsiva l'altezza dello stack è $n$, mentre nella iterativa è $\log_{2}n$.

![](http://www.xybernetics.com/techtalk/SortingAlgorithmsExplained/images/quick2.gif)

###### Versione Bentley-Mcilroy

```java
class Quick {

	// Versione Bentley-Mcilroy
	public static List<Comparable> sort(List<Comparable> l) {

		if (l.length() <= 1)                    // Lista <= 1 già ordinata
			return l;
	
		List<Comparable> c[] = partition(l);    // Partiziona: ritorna list con c[0] = sinistra, c[1] = pivots, c[2] = destra

		if (c[0] != null)                       // Ri-sorta se non null (c[0] e poi c[2])
			c[0] = sort(c[0]);
		if (c[2] != null)
			c[2] = sort(c[2]);

		c[0].addAll(c[1]);                      // Mergia le liste e le ritorna in 1
		c[0].addAll(c[2]);
		return c[0];

	}

	public static List<Comparable> partition(List<Comparable> l) {
	
		List<Comparable>[] c = new List[3];    // (i 3 elementi sono liste) | c[0] < pivot, c[1] = pivot, c[2] > pivot
		Comparable x, pivot; 
		
		x = pivot = a.get(0);                  // Prende il 1° elemento come pivot (e lo salva in x)
		c[1].add(x);                           // e lo aggiunge alla lista in mezzo
		l.remove(0);                           // + lo rimuove da l
		x = a.get(0);                          // poi rilegge 1° valore

		while (x != null) {
		
			if (less(x, pivot))                // x < pivot --> mette a sinistra
				c[0].add(x);
			else if (less(pivot, x))           // x > pivot --> mette a destra
				c[2].add(x);
			else                               // x = pivot --> mette in mezzo
				c[1].add(x);

			l.remove(0);                       // Rimuove 1° elemento
			x = l.get(0);                      // e prende il prossimo in x (altrimenti x = null sottinteso)
		
		}

		return c;
	
	}

}
```

> [!info] Complessità *quick sort*
> Caso migliore: $O(n \log n) \;\rightarrow\;$ lo si ha quando il pivot è la mediana per ogni esecuzione di partition.
> Caso peggiore: $O(n^{2}) \;\rightarrow\;$ lo si ha quando il pivot è il minimo o il massimo.
> Versione Bentley-Mcilroy: $O(kn) \;\rightarrow\;$ dati $n$ elementi e $k$ chiavi ($\Theta(n)$ confronti e $k$ chiamate complessive).

###### Caratteristiche quick sort

Né stabile né adattivo.

Alcune versioni avanzate prevedono:

- Selezionare il pivot come mediana tra 3 (o 5) elementi (*median of three*),
- Chiamare [[#Insertion sort|insertion sort]] per sequenze brevi alla fine.

###### Equazioni di ricorrenza

![](https://i.imgur.com/CGQ2Ltc.png)

![](https://i.imgur.com/6JXSpbD.png)

![](https://i.imgur.com/E4sZEDX.png)

##### Heap sort

(Prima di parlare dell'ordinamento) un ***heap*** è una struttura dati simile a una <u>coda</u> ma che serve per gestire <u>elementi con priorità</u> (immagina un albero dove i nodi padre hanno priorità > dei figli) e supporta le seguenti operazioni: `insert(obj, priority)` per inserire un elemento con una certa priorità, `delete()` che cancella l'elemento con priorità max (o min) e `read()` per leggerlo.

Un vettore *heap-ordinato* `arr` avrà, per ogni elemento `i`, elemento sinistro `arr[2i]` e destro `arr[2i+1]` (se tali sono nell'array).

```java
// Classe MaxPriorityQueue --> classe di supporto dell'Heap (max perche esistono anche in min-heap che funzionano al contrario)
public class MaxPQ<T extends Comparable<T>> {

	private T[] pq;
    private int n = 0;

    public MaxPQ(int dim) {
        pq = (T[]) new Comparable[dim + 1];  // Parte da index 1 perché pq[0] non usato (non rispetta regole arr[2i] e arr[2i+1])
    }

    public boolean isEmpty() {
        return n == 0;
    }

    public int size() {
        return n;
    }

    public void insert(T v) {
        pq[++n] = v;             // Inserisce elemento in fondo all'heap
        swim(n);                 // Prova a farlo "risalire" nell'albero finché non è in index giusto
    }

    public T read() {            // Ottiene sempre il max
        return pq[1];
    }

    public T delete() {          // Elimina (e restituisce) max per portare l'ultimo elemento all'inizio e ribilanciare l'albero
        T max = pq[1];           // Salva max (per poi ritornarlo alla fine)
        exchange(1, n--);        // Scambia max con ultimo elemento
        pq[n + 1] = null;        // Elimina ultimo elemento (prima max)
        sink(1);                 // Fa scendere max (che era ultimo elemento) 
        return max;
    }

    private boolean less(int i, int j) {
        return pq[i].compareTo(pq[j]) < 0;    // Confronta i VALORI agli index specificati
    }

    private void exchange(int i, int j) {
        T t = pq[i];
        pq[i] = pq[j];
        pq[j] = t;
    }

	// Elemento a index i risale l'albero di priorità fino alla posizione giusta
    private void swim(int i) {
        while (i > 1 && less(i / 2, i)) {     // Se pq[i] > pq[i/2] (o se figlio > padre in albero) 
            exchange(i, i / 2);               // Figlio risale e padre scende
            i = i / 2;                        // (dimezza indice effettivo se spostato --> per continuare a risalire in caso)
        }
    }

	// Elemento a index i scende l'albero di priorità fino alla posizione giusta
    private void sink(int i) {
        while (2 * i <= n) {                  // Finché ha un figlio (j è il suo index (sinistro))
            int j = 2 * i;
            if (j < n && less(j, j + 1))      // Se c'è figlio destro maggiore --> usa quello
	            j++;
            if (!less(i, j))                  // Se padre >= figlio esce
	            break;
            exchange(i, j);                   // Altrimenti li scambia (e continua)
            i = j;
        }
    }

	// Costruisce un heap bottom-up
    public void buildBU(T[] arr) {
        if (arr.length < pq.length) {                 // Se elementi di arr ci stanno in heap (se struttura statica)
            n = arr.length;
            for (int i = 0; i < arr.length; i++) {    // Copia elementi da arr in heap
                pq[i + 1] = arr[i];
            }
            for (int i = n / 2; i >= 1; i--) {        // Ribilancia l'albero sinkando nodi da metà in su (foglie già sinkate)
                sink(i);
            }
        }
    }

	public static void sort(Comparable[] arr) {

		// Creo heap
		MaxPQ<Integer> pq = new MaxPQ<Integer>(arr.length + 1);
		
		// Costruisce heap da arr
		pq.buildBU(arr);
		
		for(int i = arr.length - 1; i >= 0; i--)    // Carica in modo simil-stack
			arr[i] = pq.delete();                   // Prende (e rimuove) il max dall'heap e lo mette da fine a inizio arr

	}

}
```

![](http://www.xybernetics.com/techtalk/SortingAlgorithmsExplained/images/heap1.gif)

> [!info] Complessità *heap sort*
> In generale:
> - `swim()`/`insert()`: caso migliore $O(1)$ (1 solo confronto padre-figlio), caso peggiore $O(\log_{2}n)$ (risale albero fino a root),
> - `sink()`/`delete()`: caso migliore $O(1)$ (1 solo confronto padre-figlio), caso peggiore $O(\log_{2}n)$ (scende albero fino a una foglia),
> - `read()`: sempre $O(1)$,
> - ***Top-down***: caso migliore $O(n)$ ($n$ inserimenti già corretti), caso peggiore $\Theta(n\log_{2}n)$ (ogni elemento deve risalire l'intero albero),
> - ***Bottom-up***: sempre $\Theta(n)$ (invece di inserire e bilanciare, costruisce già bilanciato),
> - **Heapsort**: $T(n) = c_{1} + \Theta(n) + n \cdot (c_{2} + O(\log n)) = O(n \log n)$

###### Caratteristiche heap sort

Non stabile: 2 elementi uguali in 2 sottoalberi diversi, potrebbe fare `swim()` prima su elemento a destra rispetto che a elemento a sinistra (invertendone quindi l'ordine).

> [!faq] Vettore *heap-ordinato*
> Un vettore si dice *heap-ordinato* quando la priorità dell'elemento `i` è $\geq$ di quella degli elementi `2i` e `2i+1`, come si vede qui:
> ![](https://i.imgur.com/a8PfYOC.png)

### Algoritmi digitali

##### Distribution counting

Il ***distribution counting*** (o ***counting sort***) si applica nei casi in cui la sequenza contiene numeri con ripetizioni. Esso: 1) prende il massimo e il minimo nella sequenza, 2) per ogni valore nel range tra essi ne conta le occorrenze in un array 3) per poi rendere quest'ultimo un array cumulativo (somma ad ogni valore il valore del precedente) così da 4) ricreare l'array originale ordinato disponendo ogni numero tante volte quante le occorrenze nella rispettiva posizione dell'array delle occorrenze.

(Una versione migliore farebbe uso di una `Map` o di un dizionario che salva nelle chiavi i numeri e nei valori le occorrenze).

```java
public class Counting {

	public static void sort(int[] arr) {

		int n = arr.length, min = arr[0], max = arr[0], range;
		int[] count, temp;

		for (int i = 0; i < N; i++) {                   // Trova minimo e massimo in tutta la sequenza
			if (min > arr[i])
				min = arr[i];
			else if (max < arr[i])
				max = arr[i];
		}

		range = max - min + 1;                          // Ottengo il n° di valori distinti nel range (tipo da 2 a 11 = 10 val)
		count = new int[range];                         // Count conta le occorrenze di ogni valore
		temp = new int[n];                              // Array temporaneo per salvare numeri ordinati

		for (i = 0; i < range; i++)                     // Inizializza ogni valore di count a 0
			count[i] = 0;
			
		for (i = 0; i < n; i++)                         // Per ogni num --> ne aumenta il n° di occorrenze all'indice giusto di count
			count[arr[i] - min]++;
			
		for (i = 1; i < range; i++)                     // Somma ad ogni elemento il precedente (lo rende un array cumulativo)
			count[i] += count[i-1];
			
		for (i = 0; i < n; i++)                         // Prende l'index del valore corrente in count, mette il valore in temp
			temp[count[arr[i] - min]-- -1] = arr[i];    // a quell'index - 1 e ne decrementa l'occorrenza in count
			
		for (i = 0; i < n; i++)                         // Copia l'array ordinato nell'originale
			arr[i] = temp[i];

	}

}
```

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20210219152324/ezgif.com-gif-maker2.gif)

> [!info] Complessità *distribution counting*
> Complessità: $\Theta(n + range)$

##### Bucket sort

Il ***bucket sort*** permette di ordinare una qualsiasi sequenza di parole (di uguale lunghezza) in **[ordine lessicografico](https://it.wikipedia.org/wiki/Ordine_lessicografico)** (alfabetico per lettera) confrontandone i caratteri.

```java
public class Bucket {

	final static int N_CHAR = 256;         // Esempio di numero possibile di simboli della stringa (ASCII)
	final static int WORD_LENGTH = 24;     // Esempio di lunghezza delle stringhe ordinabili

	public static void sort(Deque<String> dq) {

		String word;
		Deque<String>[] buckets = new Deque[N_CHAR];

		for (int i = WORD_LENGTH - 1; i > 0; i--) {

			while (!dq.isEmpty()) {                // Svuota la deque salvando le word nei bucket
				word = dq.front();                 // Ottiene (ed elimina) la 1a parola nella deque
				dq.delete(1);
				int e = (int)word.charAt(i);       // Ne prende il char all'indice i come intero
				buckets[e].enqueue(word);          // Mette la word nel bucket all'indice e (valore numerico del char preso)
			}

			for (int j = 1; j < N_CHARM; j++) {
				buckets[0].chain(buckets[j]);      // Accoda il bucket all'index [j] ad buckets[0] (e setta quello in j a null)
				buckets[j] = null;
			}

			dq = buckets[0];                       // Pulisce dq e buckets
			buckets[0] = new Deque<>();

	    }

	}

}
```

> [!info] Complessità *bucket sort*
> Complessità: $\Theta(k\cdot(n + m))$ dove: 
> - $k$ = `WORD_LENGTH`,
> - $m$ = n° di char nell'alfabeto in considerazione,
> - $n$ = n° di parole della sequenza.

###### Caratteristiche bucket sort

Stabile: parole uguali nello stesso bucket.

### Riepilogo complessità

![](https://i.imgur.com/18UJ4hu.png)

---

Prossima lezione: [[14 - BST]]

