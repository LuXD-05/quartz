# Lezione 4

### Limited buffer problem

Il ***limited buffer problem*** (o problema dei produttori e consumatori) è caratterizzato un **buffer** di <u>dimensioni limitate</u>, da 1 o più thread **produttori** che <u>scrivono</u> dei dati e da 1 o più thread **consumatori** che <u>prelevano</u> i dati scritti dai produttori nel buffer.

Il problema nasce dal fatto che la <u>frequenza</u> con cui produttori/consumatori scrivono/prelevano dati nel buffer è <u>non determinabile</u> (dato che i thread sono gestiti dallo scheduler); quindi ci sono vari aspetti da gestire:

- **Accesso concorrente al buffer** (che è una <u>sezione critica</u>) quindi va implementata la <u>mutua esclusione</u>,
- Il comportamento dei **produttori** quando il buffer è pieno (produttori aspettano di essere risvegliati da un consumatore),
- Il comportamento dei **consumatori** quando il buffer è vuoto (consumatori aspettano di essere risvegliati da un produttore).

##### Produttore/consumatore singoli

In questo caso la cella condivisa avrà una dimensione di 1 e ci saranno solamente 1 consumatore e 1 produttore a concorrere per produrre/consumare:

```java
public class Cella {
	private static final int SIZE = 1;  // Buffer size = 1
	private int nItems = 0;           // Counter parte da 0
	private int value;                  // (value parte vuoto)
	
	// sync permette 1 set x volta sul value
	public synchronized void setItem(int v) {
		if (nItems == SIZE)  // non produce se buffer pieno
			wait();
		value = v;
		nItems++;
		notify();    // sveglia il consumer
	}
	
	// sync permette 1 get x volta sul value
	public synchronized int getItem() {
		if (nItems == 0)  // non consuma se buffer vuoto
			wait();
		nItems--;
		notify();    // sveglia il producer
		return value;  // siccome 1 solo item lo si fa sovrascrivere
	}
}

public class Produttore extends Thread {
	private Cella cella;
	public Produttore(Cella c) {
		cella = c;
	}
	public void run() {
		for (int i = 1; i <= 10; i++) {
			try {
				cella.setItem(i);
			} catch(InterruptedException _) { break; } 
		}
	}
}

public class Consumatore extends Thread {
	private Cella cella;
	public Consumatore(Cella c) {
		cella = c;
	}
	public void run() {
		int v;
		for (int i = 1; i <= 10; i++) {
			try {
				v = cella.getItem(i);
			} catch(InterruptedException _) { break; } 
		}
	}
}

public static void main() {
	Cella c = new Cella();
	new Produttore(c).start();
	new Consumatore(c).start();
}
```

Seppur ci si aspetti un output lineare (se si stampasse qualcosa nei `run()` dei thread) non è detto che tale sia il caso a causa dello scheduling e/o del buffering dell'output.

Inserendo delle stampe nelle sezioni critiche si può verificare la correttezza di un'esecuzione se non vi sono mai scritture/letture consecutive ma sempre alternate.

###### Buffer più grande

Se cambia la grandezza del buffer ma non il numero di thread basta semplicemente aumentare `SIZE` e usare una struttura adatta:

```java
public class Cella {
	private final int size;
	private final int[] buffer;
	//...
	public Cella(int s) {
		size = s;
		buffer = new int[size];
	}
	//...
}
```

Comunque `size` non è indispensabile in questo caso in quanto se la si usa come dimensione del buffer, allora nei confronti basterà sostituirla con `buffer.length`.

##### Più produttori/consumatori

Avendo più produttori/consumatori (e un array invece di buffer singolo) bisogna solo cambiare la gestione di `wait()` e `notify()`:

```java
public class Cella {
	private final int size;
	private final int[] buffer;
	private int nItems = 0;
	// ctor --> come sopra
	// Variabili "first" e "last" sono implementate dopo (qua è solo esempio)
	public synchronized void setItem(int v) {
		while (nItems == buffer.length)
			wait();
		//buffer[?] = v;  // buffer[?] = 1a cella libera del buffer
		nItems++;
		notifyAll();  // notifica TUTTI i thread in attesa
	}
	public synchronized int getItem() {
		while (nItems == 0)
			wait();
		nItems--;
		notifyAll();  // notifica TUTTI i thread in attesa
		//return buffer[?];  // buffer[?] = 1a cella occupata del buffer (e deve anche consumarla)
	}
}

public class Produttore extends Thread {
	private Cella cella;
	public Produttore(String name, Cella c) {
		super(name);
		cella = c;
	}
	public void run() {
		int i = 1;
		while (true) {
			try {
				cella.setItem(i++);
			} catch(InterruptedException _) { break; } 
		}
	}
}

public class Consumatore extends Thread {
	private Cella cella;
	public Consumatore(String name, Cella c) {
		super(name);
		cella = c;
	}
	public void run() {
		int v;
		while (true) {
			try {
				v = cella.getItem();
			} catch(InterruptedException _) { break; } 
		}
	}
}

public static void main() {
	Cella c = new Cella(5);
	for (int i = 1; i <= 3; i++) {
		new Produttore("p"+i, c).start();
		new Consumatore("c"+i, c).start();
	}
}
```

#### Altre soluzioni

##### Con semafori

Si può implementare un monitor anche usando 3 semafori: 1 per la <u>sezione critica</u>, 1 per <u>bloccare i consumatori</u> quando il buffer è **vuoto** e 1 per i <u>produttori</u> quando è **pieno**.

```java
// Tali semafori dovranno essere dichiarati nella classe del main() (in questo esempio Program)
public class Program {
	public static final Semaphore mutex = new Semaphore(1);  // mutex init a 1
	public static final Semaphore full  = new Semaphore(0);  // full init a 0 (all'inizio buffer vuoto)
	public static final Semaphore empty = new Semaphore(n);  // empty init a n (dimensione del buffer)

	public static void main() { 
		Cella c = new Cella(n);
		new Produttore("p"+i, c).start();
		new Consumatore("c"+i, c).start();
	}
}

public class Cella {
	private int nItems = 0;
	private int value;
	public void setItem(int v) throws InterruptedException {
		Program.mutex.acquire();
		value = v;
		nItems++;
		Program.mutex.release();
	}
	public int getItem() throws InterruptedException {
		Program.mutex.acquire();
		int v = value;
		nItems--;
		Program.mutex.release();
		return v;
	}
}

// Produttore
public void run() {
	int i = 1;
	while (true) {
		try {
			Program.empty.acquire();
			cella.setItem(i++);
		} catch(InterruptedException _) { break; } 
		Program.full.release();
	}
}

// Consumatore
public void run() {
	int v;
	while (true) {
		try {
			Program.full.acquire();
			v = cella.getItem();
		} catch(InterruptedException _) { break; } 
		Program.empty.release();
	}
}
```

##### Con coda FIFO

Di solito il buffer ha dimensione > 1 e gli elementi sono consumati nell'ordine in cui sono prodotti, perciò si realizza un monitor con una ***queue*** FIFO (*First In First Out*).

###### Artigianale

Il seguente codice realizza una *queue* "artigianale" *thread-safe* (non soggetta a race condition) ma <u>non bloccante</u> (thread che sarebbero in attesa per produrre/consumare non ci vanno ma viene generato un'errore, perciò questo lato va gestito nel codice):

```java
public class Program {
	public static final Semaphore mutex = new Semaphore(1);  // mutex init a 1
	public static final Semaphore full  = new Semaphore(0);  // full init a 0 (all'inizio buffer vuoto)
	public static final Semaphore empty = new Semaphore(n);  // empty init a n (dimensione del buffer)

	public static void main() { 
		Cella c = new Cella(n);
		for (int i = 1; i <= 3; i++) {
			new Produttore("p"+i, c).start();
			new Consumatore("c"+i, c).start();
		}
	}
}

public class Cella {
	private int nItems = 0;
	// inizializzati in ctor in base a parametro x SIZE
	private int SIZE;
	private int[] values;
	// I seguenti index indicano la 1a e l'ultima posizione consumabile dell'array
	// Se first == last --> array vuoto
	private int first = 0;  // 1° index del buffer contenente un valore
	private int last = 0;   // Ultimo index del buffer avente un valore
	
	public void setItem(int v) throws InterruptedException {
		Program.mutex.acquire();
		if (nItems == SIZE)
			// ERR --> scrittura in buffer pieno
		values[last] = v;
		last = (last + 1) % SIZE;
		nItems++;
		Program.mutex.release();
	}
	public int getItem() throws InterruptedException {
		Program.mutex.acquire();
		if (nItems == 0)
			// ERR --> lettura di buffer vuoto
		int v = values[first];
		first = (first + 1) % SIZE;
		nItems--;
		Program.mutex.release();
		return v;
	}
}

// Produttore
public void run() {
	int i = 1;
	while (true) {
		try {
			Program.empty.acquire();
			cella.setItem(i++);
		} catch(InterruptedException _) { break; } 
		Program.full.release();
	}
}

// Consumatore
public void run() {
	int v;
	while (true) {
		try {
			Program.full.acquire();
			v = cella.getItem();
		} catch(InterruptedException _) { break; } 
		Program.empty.release();
	}
}
```

###### BlockingQueue

La soluzione "non artigianale" prevede l'uso dell'interfaccia `java.util.concurrent.BlockingQueue`, corrispondente alla cella condivisa ma non da implementare come essa. 

Al posto di `setItem()` e `getItem()` si usano nei thread `void put(T value)` e `T take()` (`T` è un tipo qualsiasi ma <u>non primitivo</u>) che mettono i thread in attesa, alternativamente ci sono altri metodi:

![561](https://i.imgur.com/Xojjpph.png)

```java
public static void main() { 
	BlockingQueue<String> q = new ArrayBlockingQueue<>(n); // o LinkedBlockingQueue = linked list
	for (int i = 1; i <= 3; i++) {
		new Producer(q).start();
		new Consumer(q).start();
	}
}

public class Producer extends Thread {
	private BlockingQueue<String> q;
	public Produttore(BlockingQueue<String> queue) {
		q = queue;
	}
	public void run() {
		int i = 1;
		try {
			while (true) {
				q.put(String.valueOf(i++));
			} 
		} catch(InterruptedException _) { break; } 
	}
}

public class Consumer extends Thread {
	private BlockingQueue<String> q;
	public Consumatore(BlockingQueue<String> queue) {
		q = queue;
	}
	public void run() {
		try {
			while (true) {
				String s = q.take();
			} 
		} catch(InterruptedException _) { break; } 
	}
}
```

---

Prossima lezione: [[]]

