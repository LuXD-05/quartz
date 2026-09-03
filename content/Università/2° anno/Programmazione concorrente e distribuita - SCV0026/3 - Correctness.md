# Lezione 3

### Correctness

La ***correctness*** (<u>correttezza</u>) è una proprietà dei programmi concorrenti che garantisce che, nonostante l'ordine di esecuzione delle operazioni (deciso dallo *scheduler*), l'output è lo stesso che si avrebbe ottenuto da un programma sequenziale (con stessi input e operazioni) *single-thread*. Questa si divide in:

- ***Safety***: proprietà che garantisce che i thread non operino mai con dati/risorse **inconsistenti** (ovvero che stanno venendo modificate da altri thread).
- ***Liveness***: proprietà che garantisce che il sistema <u>progredisce</u>, ovvero che un'operazione che rispetta la ***safety*** verrà eseguita in un tempo finito.

##### Race condition

Si dicono *race condition* quelle situazioni in cui <u>thread diversi operano in competizione su una risorsa comune</u> (senza misure che prevengano l'accesso contemporaneo) in una maniera tale che il risultato sia <u>non deterministico</u> e dipendente dall'ordine in cui sono eseguite le operazioni. Esempio:

```java
public class Counter {
	private long count = 0;
	public void add(long value) {
		this.count += value;  // --> [tmp = count] --> [tmp = tmp + value] --> [count = tmp]
	}
	public long getValue() { return count; }
}

public void main() throws InterruptedException {
	Counter c = new Counter();
	Thread t1 = new Thread((c) -> { 
		for (int i = 0; i < 1000; i++)
			c.add(1);
	});
	Thread t2 = new Thread((c) -> { 
		for (int i = 0; i < 1000; i++)
			c.add(1);
	});
	
	t1.start(); t2.start();
	t1.join(); t2.join();
	
	System.out.println("counter = " + counter.getValue());
}
```

In questo caso il *counter* finale dovrebbe essere a 2000; tuttavia, a causa delle *race condition*, alcuni incrementi possono andare <u>persi</u>:

![](https://i.imgur.com/ORJkhjR.png)

`tmp` è una variabile locale e unica per ogni thread, ma `count` (sul quale vanno applicati gli incrementi) è <u>condiviso</u> tra i thread perché appartiene all'oggetto `Counter`, il cui riferimento (istanza `c`) è uguale per `t1` e `t2`.

###### Come si verificano

Purché vi siano *race conditions* si devono verificare 2 condizioni:

- Una <u>risorsa</u> deve essere <u>condivisa tra almeno 2 thread</u> (`Counter c`),
- Deve esserci del codice che esegue <u>letture</u> (`tmp = count`) e <u>scritture</u> (`count = tmp`) sulla risorsa condivisa in modo <u>non sicuro</u>.

###### Come si prevengono

Per prevenire le *race conditions* bisogna soddisfare la proprietà di ***safety*** attraverso strutture e strategie note, bloccando gli accessi non sicuri alle risorse.

Le parti di codice prone a *race condition* si dicono ***critical sections*** e bisogna <u>bloccarle e sbloccarle</u> facendo in modo che solo <u>1 thread per volta</u> possa eseguirle:

![260](https://i.imgur.com/cmHErH2.png)

#### Semafori

I **semafori** sono 1 dei modi per bloccare l'accesso alle risorse condivise, in pratica:

1) Un semaforo viene inizializzato ad un intero positivo `n` (che indica il <u>n° di thread che possono accedere alla risorsa condivisa in contemporanea</u>),
2) Ogni volta che un thread accede ad una risorsa condivisa, `n` <u>è decrementato di 1</u> con il metodo `wait()`,
3) Quando `n` arriva a 0 e un altro thread fa `wait()` esso viene posto <u>in attesa</u> finché 1 thread non lascia la risorsa,
4) Quando un thread ha finito di usare la risorsa, la rilascia con il metodo `signal()`, che incrementa `n` di 1.

> [!info] Tipi di semafori
> Ci sono 2 "tipi" di semafori: i **contatori** che hanno `n` > 1 e contano quanti processi possono accedere ad una risorsa e quelli **binari** (o ***mutex***) che hanno `n` = 1.

##### In Java

Java fornisce un semaforo mediante la classe `java.util.concurrent.Semaphore` con 2 metodi analoghi a `wait` e `signal`:

- `acquire()`: che richiede l'accesso alla risorsa come `wait()`,
- `release()`: che rilascia la risorsa come `signal()`.

###### Correzione esempio

Per correggere l'esempio precedente e risolvere le *race condition*, basta rendere ***thread-safe*** la classe `Counter` con un semaforo che blocca la risorsa condivisa `count` durante `add()`:

```java
public class Counter {
	private Semaphore mutex = new Semaphore(1);
	private long count = 0;
	public void add(long value) {
		try { 
			mutex.acquire(); 
		} catch (InterruptedException e) { /* gestire interrupt() */ }
		this.count += value;
		mutex.release();
	}
	public long getValue() { return count; }
}
```

> [!important] Nota
> Viene usato un `try-catch` su `acquire()` per gestire una eventuale `InterruptedException` in quanto, quando un thread esegue `acquire()` con un semaforo a 0, esso va in ***waiting***, quindi è soggetto ad `interrupt()` chiamati da altri thread.

#### Synchronized

Con i semafori è possibile commettere degli errori, chiamando `acquire()` o `release()` più volte del necessario; perciò Java ha fatto in modo che <u>ad ogni oggetto</u> (ogni istanza di qualsiasi classe) è associato un <u>semaforo binario</u> (detto ***intrinsic lock***) che si utilizza con la *keyword* `synchronized`.

Ogni thread che accede ad una risorsa condivisa attraverso un metodo `synchronized` prova ad acquisire l'***intrinsic lock*** dell'oggetto; se tale *lock* è già stato acquisito da un altro thread, quello corrente va in attesa, altrimenti acquisisce il *lock* ed usa la risorsa. Quando si finisce il metodo `synchronized` si rilascia automaticamente il *lock*.

```java
// Sintassi normale
synchronized(obj) {  // anche synchronized(this) per bloccare risorsa corrente
	// codice in mutua esclusione
}

// Modificatore metodo
public synchronized void func() {
	// codice in mutua esclusione
}
```

Esempio:

```java
public class AssegnatorePosti {
    private int posti = 20;
	// synchronized per non incorrere in race condition
    public synchronized boolean assegna(int n) {
		if (n <= posti) {  // critical section
            posti -= n;    // critical section
            return true;
        }
        return false;
    }

    public int getPosti() { return posti; }
}

public static void main() throws InterruptedException {
	AssegnatorePosti a = new AssegnatorePosti();
	Thread[] threads = new Thread[4];

	for (int i = 0; i < 4; i++) {
		threads[i] = new Thread((a) -> {
			if (a.assegna(6)) System.out.println("t" + i + " richiede e ottiene 6 posti");
			else System.out.println("t" + i + " richiede e NON ottiene 6 posti");
		});
		threads[i].start();
	}
	
	for (Thread t : threads)
		t.join();

	System.out.println("Rimasti: " + a.getPosti());
}
```

Usando `synchronized`, un esempio tipico di output è:

![288](https://i.imgur.com/MhoYien.png)

Senza di esso invece si rischia di ottenere:

![288](https://i.imgur.com/L5JqgEe.png)

###### Variabili statiche

L'uso normale di `synchronized` <u>non assicura la mutua esclusione</u> per le variabili <u>statiche condivise</u> in quando ogni istanza di una classe con una variabile statica ha un ***intrinsic lock*** diverso per lo stesso dato statico condiviso tra tutte le istanze, quindi 2 istanze diverse che accedono ad una variabile statica con `synchronized` acquisiscono il proprio lock e vi accedono comunque concorrentemente.

Ci sono 2 modi per risolvere questo problema:

```java
public class StaticSharedVariable {
	private static int shared;
	
	// 1) Usare un metodo statico con synchronized per l'accesso
	public static synchronized void write(int i) {
		shared = i;
	}
	
	// 2) Usare synchronized sulla classe (invece che sull'istanza)
	public int read() {
		synchronized (StaticSharedVariable.class) {
			return shared;
		}
	}
}
```

###### Ereditarietà

Vi è la possibilità di ridefinire metodi `synchronized` come non `synchronized` e viceversa grazie all'ereditarietà delle classi:

```java
public class AssegnatoreSequenziale {
    private int posti = 20;
    public boolean assegna(int n) {
		if (n <= posti) {
            posti -= n;
            return true;
        }
        return false;
    }
}
public class AssegnatoreConcorrente extends AssegnatoreSequenziale {
	public synchronized boolean assegna(int n) {
		return super.assegna(n);
	}
}
```

##### Cooperazione

`synchronized` in sé non dice ai thread in attesa quando hanno finito di usare una risorsa, quindi (invece di ciclare finché una risorsa non è libera), Java mette a disposizione `wait()`, `notify()` e `notifyAll()` della classe `Object` (questi sono chiamabili solo un thread che ha il *lock* di un oggetto, ovvero all'interno di `synchronized` su esso).

###### Wait

Quando un thread in un lock chiama `wait()` esso <u>rilascia il lock e va in attesa</u> in una ***wait list*** specifica <u>dell'oggetto</u>, mentre quando verrà risvegliato verrà messo nella ***ready list*** <u>generale</u> (gestita dallo scheduler).

```java
synchronized (this) { // lock
	try {
		this.wait();  // unlock (finché non svegliato)
		// lock
	} catch (InterruptedException e) { /* ... */ }
} // unlock
```

Solitamente `wait()` si usa quando un thread determina che non può più proseguire (gli manca qualche risorsa o non ci sono le condizioni necessarie) e deve attendere fino a quando il problema viene risolto (da altri thread).

###### Notify

`notify()` sposta un thread qualsiasi (determinato dallo scheduler) dalla *wait list* dell'oggetto alla *ready list* dello scheduler (lo risveglia e lo rende di nuovo schedulabile); mentre `notifyAll()` sposta <u>tutti</u> i thread nella *wait list* dell'oggetto alla *ready list*.

##### Monitor

Un ***monitor*** è un costrutto di programmazione concorrente nel quale <u>tutti</u> i metodi di una classe sono `synchronized` cosicché ogni istanza di tale classe sia usabile solo da 1 thread alla volta. A livello di potere espressivo è identico a un **semaforo**, infatti un semaforo è implementabile con questo costrutto:

```java
public class SemaphoreMonitor {
	private int value;
	public Semaphore(int v) {
		value = v;
	}
	public synchronized void acquire() throws InterruptedException {
		while (value == 0)
			wait();
		value--;
	}
	public synchronized void release() {
		value++;
		notify();
	}
}
```

#### Problemi

Prevenendo le *race conditions* è possibile che si verifichino altri problemi all'interno dei programmi concorrenti.

##### Deadlock

Si ha un ***deadlock*** (**stallo**) quando 2 o più thread rimangono bloccati indefinitamente ognuno in attesa di una risorsa trattenuta da un altro.

La seguente rappresenta un caso (semplice) di *deadlock*:

![351](https://i.imgur.com/VBu2Lf8.png)

In un caso del genere nessun thread potrà mai creare un evento di sblocco di una risorsa che sblocca l'intero sistema in deadlock; quindi si avrà attesa infinita.

> [!important] Condizioni
> Ci sono 4 condizioni necessarie affinché si verifichi un deadlock:
> - ***Mutual exclusion***: solo 1 thread per volta deve poter accedere ad una risorsa,
> - ***Hold & wait***: esistono dei thread che trattengono risorse e al contempo aspettano che se ne liberino altre,
> - ***No preemption***: non è possibile forzare un thread a rilasciare una risorsa,
> - ***Circular wait***: esiste una catena circolare di thread in *hold & wait* (`t1` attende una risorsa occupata da `t2`, `t2` ... da `tn` e `tn` da `t1`).

###### Esempio

```java

```

###### Deadlock prevention

Si può effettuare della ***deadlock prevention*** per appunto prevenire il deadlock facendo in modo che 1 delle 4 condizioni non si verifichi.

Per esempio si potrebbe prevenire la *hold & wait* facendo in modo che non si possa detenere una risorsa mentre si è in attesa di un'altra:

```java
synchronized (a) {
	// blocca a (hold)
	synchronized (b) {
		// attende b bloccata (wait)
	}
}

// Deve diventare

synchronized (a) {
	//...
}
synchronized (b) {
	//...
}
```

Soluzione facile da applicare ma non funziona se il thread richiede sia `a` sia `b` per operare.

L'altra opzione è eliminare la circolarità facendo in modo che l'acquisizione delle risorse segua sempre un ordine (prima `a`, poi `b`...), però se un thread si accorge che ha bisogno di `a` dopo aver acquisito `b` allora deve fare tutto da capo (il che è costoso e difficile).

###### Deadlock removal

Con il ***deadlock removal*** invece si va a risolvere il deadlock quando ci si accorge che è avvenuto, rendendo *preemptive* delle risorse, quindi consentendone il rilascio forzato.

Questa opzione è più complicata in quanto serve un modo per <u>rilevare il verificarsi di un deadlock</u> e bisogna <u>riportare i thread a cui sono state sottratte delle risorse</u> forzatamente <u>allo stato in cui erano prima</u> che le acquisissero.

---

Prossima lezione: [[]]

