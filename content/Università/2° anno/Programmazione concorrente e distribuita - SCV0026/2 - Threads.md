# Lezione 2

### Thread

Un <u>programma</u> è un'insieme di istruzioni, un <u>processo</u> è un programma in esecuzione con uno <u>spazio di indirizzi proprio</u>, mentre un ***thread*** è un processo "leggero" che <u>condivide</u> lo stesso <u>spazio di indirizzi con altri thread</u> e tali possono <u>eseguire al contempo</u>, consentendo multipli flussi di esecuzione (<u>programmazione concorrente</u>):

![425](https://i.imgur.com/ONSLyxY.png)

##### Stati

Un thread può trovarsi in 1 di questi stati in ogni momento:

![](https://i.imgur.com/I4KkUma.png)

Lo ***scheduler*** (JVM) è ciò che determina quali thread in stato ***ready*** possono passare a ***running*** (*dispatch*, ovvero esegue il metodo `run()`) e quali invece vanno interrotti (*yield*).

###### Preemption

L'algoritmo di schedulazione della JVM è ***preemptive***, ovvero può decidere arbitrariamente (in base alla priorità) di sottrarre la CPU a certi thread ed assegnarla ad altri. 

Se non lo fosse, un thread con un codice simile al seguente:

```java
public class BusyThread extends Thread {
	public void run() {
		int a = 0;
		while (true) {
			if (a < 1) { a = a + 1; }
			else { a = a - 1; }
		}
	}
}
```

Se avviato, non cederebbe mai più la CPU agli altri processi (siccome non fa `sleep()`, `wait()` o fa operazioni di I/O).

#### In Java

In Java esiste la classe `Thread`, il metodo `main()` è associato al *thread* principale dell'app in esecuzione e lo si ottiene con `currentThread()`:

```java
public static void main() {
	// Istanze di Thread hanno: nome, priorità e gruppo di appartenenza
	Thread t = Thread.currentThread();  // name = "main"
	t.setName("...");                   // Cambia il nome di t
}
```

> [!important] Daemon threads
> I ***daemon threads*** sono dei thread con priorità bassa che di solito forniscono servizi, ma la caratteristica principale è che questi <u>vengono terminati quando termina la JVM</u> (al contrario dei <u>thread normali</u>, che la <u>JVM aspetta che finiscano prima di terminare</u>).
> Per impostare un thread come *daemon*, si usa `Thread.setDaemon(bool b)`.

##### Creazione

In Java è possibile creare thread in 2 modi:

###### Estensione Thread

Estendendo la classe `Thread` in una sottoclasse nella quale si fa l'*override* di `run()` riscrivendone il codice:

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Ciao");
    }
}
MyThread t = new MyThread();
t.start();
```

###### Implementazione Runnable

Implementando l'interfaccia `Runnable` e passandola come parametro ad un thread:

```java
// Esplicitamente
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Ciao");
    }
}
MyRunnable r = new MyRunnable();
Thread t = new Thread(r);
t.start();

// Implicitamente (thread anonimo + lambda)
new Thread(() -> System.out.println("Ciao")).start();
```

##### Avvio

Il metodo che contiene il codice di un thread è `run()` e tale è richiamabile quante volte si vuole in un programma, tuttavia sarà eseguito **sequenzialmente** (non concorrente):

```java
Thread t = new Thread(() -> System.out.print("Ciao"));
t.run();
t.run();
// Output: "CiaoCiao" --> sempre nello stesso ordine
```

Per avviare un thread concorrente, si usa `start()` (che richiama `run()`) che <u>può eseguire 1 sola volta</u> (alla 2a chiamata da `IllegalThreadStateException`):

```java
Thread t = new Thread(() -> System.out.print("Ciao"));
t.start();
t.start();
// Output: "Ciao" + IllegalThreadStateException
```

Avendo invece:

```java
Thread t1 = new Thread(() -> System.out.print("1"));
Thread t2 = new Thread(() -> System.out.print("2"));
Thread t3 = new Thread(() -> System.out.print("3"));
t1.start();
t2.start();
t3.start();
// Output: "123" / "132" / "213" / "231" / "312" / "321"
```

L'output può essere una delle suddette sequenze in base a che precedenze da lo *scheduler*, infatti è **non deterministico**.

> [!important] Non determinismo
> Chiamando `t.start()`, il thread `t` va in stato ***ready*** e il controllo torna subito al chiamante in quanto sarà lo ***scheduler*** a determinare quando invocare `run()`. Il **non determinismo** deriva da ciò, infatti seppur le istruzioni di ogni thread hanno un ordine (all'interno di ogni `run()`), l'<u>ordine</u> in cui saranno eseguite è <u>indeterminato</u>.

##### Sleep

Il metodo statico `Thread.sleep(long ms)` permette di mettere in pausa il thread corrente per un certo numero di millisecondi:

```java
public static void main() throws InterruptedException {
	Thread t = new Thread();
	t.start();
	Thread.sleep(1000); // Mette in pausa il main, non t!
	// t.sleep(1000);   // Errore: per mettere in pausa t bisogna fare Thread.sleep() nel suo run()
}
```

> [!warning] Attenzione
> Un thread in *timed waiting* (o stato ***sleeping***) può comunque venire interrotto da un altro thread con `interrupt()`, caso in cui il 1° genera `InterruptedException`.

###### Busy waiting

La pratica sconsigliata per simulare `sleep()` è implementare un ***busy loop***, ovvero un codice con un ciclo che termina dopo un certo tempo:

```java
public void run() {
	long start = System.currentTimeMillis();
	long end = start + 1000;                      // end = adesso + 1 secondo
	while (System.currentTimeMillis() < end) { }  // cicla finché tempo corrente < end
}
```

Questa soluzione <u>impegna la CPU</u> (che potrebbe essere lasciata ad altri thread) e alla fine del loop il <u>thread va rischedulato</u> (non riparte subito come dopo `sleep()`).

##### Join

Per determinare se un thread è ***alive*** (vivo, tra la call di `start()` e il return di `run()`) c'è il metodo `isAlive()`; e combinando questo con `sleep()` si può <u>attendere la terminazione di un thread</u> (in modo comunque inefficiente):

```java
// Se vivo --> pausa per 100 ms (finché non termina)
while (t.isAlive()) { Thread.sleep(100); }
```

La maniera corretta per attendere la terminazione di un thread è con `join([long ms, int ns])` (`ms` e `ns` specificano il *timeout*, un tempo max di attesa, omissibili) che <u>blocca il thread corrente finché non termina il thread che ha chiamato</u> `join()`:

```java
public class MyThread extends Thread {
	public MyThread(String name) {
		super(name);
	}
	public void run() {
		System.out.println(getName() + " ");
		Thread.sleep(200);
	}
}
public static void main() throws InterruptedException {
	System.out.println("start | ");
	Thread t1 = new MyThread("t1").start();
	Thread t2 = new MyThread("t2").start();
	Thread t3 = new MyThread("t3").start();
	
	/* ERRATO (spreca tempo)
	while (t1.isAlive() || t2.isAlive() || t3.isAlive()) { 
		Thread.sleep(100); 
	} */
	
	// CORRETTO
	t1.join();
	t2.join();
	t3.join();
	
	System.out.println("| end");
	System.exit(0); // Termina TUTTI i thread del programma
	// Es. output (con join) --> "start | t2 t1 t3 | end" (thread output non deterministico)
	// Es. output (no join)  --> "start | | end"          (termina tutto subito; t1, t2, t3 non partono)
}
```

> [!info] Nota
> L'ordine di call di `join()` non cambia in quanto, anche se `t2` terminasse prima di `t1`, quando `t1` termina `t2.join()` non bloccherebbe il main (`t2` già terminato).
> Ah e anche `join()` può lanciare `InterruptedException`.

##### Terminazione

La terminazione di un thread non è forzabile, ma va indotta con il metodo `interrupt()`, che imposta un flag di interruzione nel thread e ritorna; sta poi al thread stesso controllare il flag e uscire da `run()` (quindi non si può essere certi che il thread è terminato dopo `interrupt()`).

Quando un thread interrotto chiama un metodo che lo mette in pausa (tipo `sleep()`, `join()`...), tale controlla anche il flag e lancia `InterruptedException` se settato (poi termina in base a come è gestita l'eccezione). 

L'altro modo è usare `Thread.interrupted()` che ritorna lo stato del flag e lo azzera a falso (o `.isInterrupted()` per ritornarlo e basta).

```java
public static void main() throws InterruptedException {
    // .sleep() check
    Thread t1 = new Thread(() -> {
	    while (true) {
		    //...
			try { Thread.sleep(200); }  // Controlla il flag e lancia ex se settato
			catch (InterruptedException ex) { break; }
		}
    });
    
    // .interrupted() check
    Thread t2 = new Thread(() -> {
	    // o !Thread.currentThread().isInterrupted(), usabile anche da fuori
        while (!Thread.interrupted())   // Controlla se flag settato o no
            //...
    });

    t1.start();     t2.start();
    t1.interrupt(); t2.interrupt();
    t1.join();      t2.join();
    
    System.exit(0);
}
```

> [!warning] *Don't swallow interrupts*
> In caso venga intercettata una `InterruptedException` in un `try-catch` di un thread e ci sono delle cose che il thread deve ancora fare (fuori dal blocco), la soluzione Java è <u>risettare il flag di interruzione a vero</u> (come detto [qui](https://web.archive.org/web/20210301203607/http://www.ibm.com/developerworks/java/library/j-jtp05236/index.html?ca=drs-#:~:text=Don%27t%20swallow%20interrupts)):
> ```java
> try { Thread.sleep(200); }
> catch (InterruptedException ex) {
> 	// Risetta il flag di interruzione a true
> 	Thread.currentThread().interrupt();
> }
> ```

##### Yield

Chiamando `Thread.yield()` viene suggerito allo scheduler che il thread chiamante è disposto a cedere la CPU ad altri thread (con la stessa priorità). Tale metodo è utile per i thread che vanno poco spesso in attesa in quanto `Thread.yield()` previene la ***starvation*** nei sistemi senza *preemption* e in certi casi ottimizza anche quelli preemptive. 

```java
// Il seguente codice avvia 3 thread che fanno un countdown da 3,
// a meno che non rimanga 1 thread, nessuno stamperà 2 volte di fila
public class CountDown implements Runnable {
	private final int id;
	private int countDown = 3;
	
	public CountDown(int id) { this.id = id; }
	public void run() {
		while (countDown > 0) {
			System.out.println(id.toString() + (countDown > 0 ? String.valueOf(countDown--) : "End"));
			Thread.yield();  // Cede CPU ad un altro thread
		}
	}
}

public static void main() {
	for (int i = 0; i < 3; i++)
		new Thread(new CountDown(i)).start();
	
	System.out.println("Start");
}
```

#### SMM

Architettura

Single-thread

Multi-thread

---

Prossima lezione: [[]]

