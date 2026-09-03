# Lezione 7

### Paradigmi di comunicazione

Ci sono vari modi con cui i thread possono comunicare:

#### Signal

Un ***signal*** è una <u>struttura</u> che <u>tiene traccia di un evento</u>, o di un segnale che un thread (*sender*) invia ad un altro (*waiter*) e in generale se ne distinguono le interfacce:

```java
public interface SignalSender {
	void send();
}
public interface SignalWaiter {
	// Diverso da wait() java e la implementa
	void waits() throws InterruptedException;
	// void waits(long t) --> evita attese infinite con timeout t
}
```

Si accenna anche la classe astratta `Signal` dalla quale si deriveranno le seguenti concrete che realizzano 2 tipi diversi di *signal*:

```java
public abstract class Signal implements SignalSender, SignalWaiter {
	protected boolean arrived = false;  // serve x persistenza
	public synchronized void send() {
		arrived = true;
		notify();                       // basta questo x transienti
	}
	public abstract void waits() throws InterruptedException;
}
```

##### Persistent signal

Un ***persistent signal*** tiene traccia di un segnale che quando inviato, <u>rimane in "attesa"</u> (`arrived = true`) <u>finché un thread non lo legge</u> (+ lo consuma con `arrived = false`) e si usa per eventi persistenti da "ricordare" (in quanto bisogna fare in modo che il *waiter* lo legga senza perderlo).

Ci sono 2 modi per leggere il segnale: con `waits()` che blocca il thread chiamante (*waiter*) finché non vede che il segnale è arrivato, oppure con `watch()` che è come 1 singolo ciclo di `waits()` che consuma il segnale e ritorna `true` se arrivato (altrimenti ritorna `false`, ma in ogni caso non mette in attesa nessuno).

```java
public class PersistentSignal {
	// Serve x gestire persistenza
    private boolean arrived = false;

    public synchronized void send() {
        arrived = true;
        notify();
    }
    
	// Manda thread in pausa finché non arriva il signal
    public synchronized void waits() throws InterruptedException {
        while (!arrived)
            wait();
        arrived = false;  // consuma il segnale
    }
    // Versione con timeout (x evitare attese infinite)
    public synchronized boolean waits(long t) throws InterruptedException {
        long start = System.currentTimeMillis();
        long elapsed = 0;
        while (!arrived && elapsed < t) {  // se !arrived & passato meno tempo del timeout
	        wait(t - elapsed);             // wait() con timeout (- tempo passato)
	        // (dopo il timeout o notify())
	        if (arrived) {
		        arrived = false;
		        return true;
	        } else {
		        elapsed = System.currentTimeMillis() - start;  // aggiorna tempo passato dopo 1 ciclo
	        }
        }
        return false;
    }
    
	// Se signal arrivato --> consuma e ritorna true, altrimenti false (non bloccante)
    public synchronized boolean watch() {
        if (!arrived)
            return false;
        arrived = false;
        return true;
    }
}
```

###### Esempio persistent

Scrittura su disco asincrona: il main thread chiama un metodo che scrive in modo asincrono su disco (che a fine scrittura farà `send()`) che ritorna `PersistentSignal` <u>prima di fare</u> `send()`. In seguito il chiamante (main) fa `waits()` (o polling con `watch()`) di tale *signal* e quando viene invocato `send()` (scrittura finita) riceverà e consumerà il segnale (o gestirà l'eccezione in caso di `interrupt()`).

Tale segnale deve essere persistente in quanto il main non può perdere l'informazione che la scrittura è terminata (gli servirà per fare altro).

##### Transient signal

Un ***transient signal*** non rimane persistente finché un thread non lo legge ma <u>viene perso se nessun thread lo legge</u> e si usa per eventi istantanei che devono svegliare 1 o più thread in attesa in un certo momento (se nessuno in attesa, segnale perso).

Le implementazioni possibili sono 2: una che sveglia 1 solo thread (classe `TransientSignal`) e una che sveglia tutti i thread in attesa (classe `Pulse`).

```java
public class TransientSignal {
    private boolean arrived = false;
    private int waiting = 0;          // n° di thread in attesa

	// Fa notify() solo se ci sono thread in attesa
    public synchronized void send() {
        if (waiting > 0) {   // se nessuno in waiting --> segnale perso
            arrived = true;
            notify();
        }
    }

    // Busy waiting --> thread in waiting finché non arriva il segnale
    public synchronized void waits() throws InterruptedException {
        waiting++;            // (segnala che thread in waiting)
        try {
            while (!arrived)  // waiting finché non risvegliato + arrivato un mess
                wait();
            arrived = false;  // poi lo consuma
        } finally {
            waiting--;        // esce dalla coda (anche se arriva interrupt)
        }
    }
	// Versione con timeout
    public synchronized boolean waits(long timeout) throws InterruptedException {
        waiting++;
        try {
            long start = System.currentTimeMillis();
            long elapsed = 0;
            while (!arrived && elapsed < timeout) {
                wait(timeout - elapsed);
                elapsed = System.currentTimeMillis() - start;
            }
            if (arrived) {
                arrived = false;
                return true;
            }
            return false;   // timeout scaduto
        } finally {
            waiting--;
        }
    }

    // Non c'è watch() dato che i segnali transienti non possono essere controllati a posteriori
}

public class Pulse {
    private boolean arrived = false;
    private int waiting = 0;

    // Fa notifyAll() solo se ci sono thread in attesa
    public synchronized void sendAll() {
        if (waiting > 0) {   // se nessuno waiting --> tutti perdono segnale
            arrived = true;
            notifyAll();
        }
    }

    // Busy waiting --> il thread in waiting finché non arriva il segnale
    public synchronized void waits() throws InterruptedException {
        waiting++;
        try {
            while (!arrived) {
                wait();
            }
        } finally {
            waiting--;
            // L'ultimo thread che legge azzera il segnale (accerta che tutti hanno letto)
            if (waiting == 0)
                arrived = false;
        }
    }

    // Versione con timeout 
    public synchronized boolean waits(long timeout) throws InterruptedException {
        waiting++;
        try {
            long start = System.currentTimeMillis();
            long elapsed = 0;
            while (!arrived && elapsed < timeout) {
                wait(timeout - elapsed);
                elapsed = System.currentTimeMillis() - start;
            }
            // Non consuma subito, aspetta che tutti i thread finiscano
            return arrived;  // ritorna false se esce x timeout, altrimenti true (arrivato)
        } finally {
            waiting--;
            if (waiting == 0)     // Azzera sempre l'ultimo uscito
                arrived = false;
        }
    }
    
    // No watch() per lo stesso motivo
}
```

###### Esempio transient

Apertura di un negozio: un negozio (thread) apre le <u>porte</u> (da accesso a se stesso) solo a intervalli di `n` secondi mentre i clienti (sempre thread) possono accedervi solamente durante quegli intervalli; in più quando tutti i clienti in coda sono entrati le <u>porte</u> del negozio si chiudono.

Queste porte sono un oggetto `Pulse` sul quale i thread clienti fanno `waits()` per mettersi in coda, poi quando arriva il turno del thread negozio di fare `send()`, tutti i clienti escono da `wait()`, leggono il *signal* (entrano in negozio) e l'ultimo lo azzera (chiude la porta), sbloccando la mutex (di `synchronized`) e permettendo ad altri di mettersi in coda. Se il negozio apre le porte quando non ce nessuno in coda, le richiude senza che nessuno entri.

#### Buffer

Si definisce ***buffer*** (in questo caso) una struttura che contiene dei dati che verranno <u>consumati</u> (distrutti una volta letti).

L'implementazione è identica a quella del problema dei produttori e consumatori:

```java
public class Buffer<T> {
	// Variabile "size" sostituita da buffer.length"
	private final T[] buffer;
	private int nItems = 0;
	private int first = 0;
	private int last = 0;
	
	public BoundedBuffer(int s) {
		buffer = (T[]) new Object[s];
		//buffer = new T[s];  // ???
	}
	
	public synchronized void set(T item) throws InterruptedException {
		while (nItems == buffer.length)
			wait();
		buffer[last] = item;
		last = (last + 1) % buffer.length;
		nItems++;
		notifyAll();
	}
	public synchronized T get() throws InterruptedException {
		while (nItems == 0)
			wait();
		T item = buffer[first];
		first = (first + 1) % buffer.length;
		nItems--;
		notifyAll();
		return item;
	}
}

public class Produttore extends Thread {
	private Buffer<T> buffer;
	public Produttore(String name, Buffer<T> b) {
		super(name);
		buffer = b;
	}
	public void run() {
		int i = 1;
		while (true) {
			try {
				cella.set(i++);
			} catch(InterruptedException e) { break; } 
		}
	}
}

public class Consumatore extends Thread {
	private Buffer<T> buffer;
	public Consumatore(String name, Buffer<T> b) {
		super(name);
		buffer = b;
	}
	public void run() {
		int v;
		while (true) {
			try {
				v = buffer.get();
			} catch(InterruptedException e) { break; } 
		}
	}
}
```

#### Blackboard

Una ***blackboard*** è una struttura molto simile a un *buffer*, solo che i dati in essa non vengono consumati ma vi permangono finché non sono sovrascritti/cancellati/invalidati. Rispetto al *buffer*: `get()` e `set()` sono sostituiti da `read()` e `write()`, si usa un flag `valid` che (impostato a `true` da `write()`) permette la lettura o meno (quando impostato a `false` dal metodo `clear()` che fa solo quello) ed infine `dataAvailable()` è come `watch()`: singolo check che ritorna `valid`.

```java
public class Blackboard<T> {
	private T message;
	private boolean valid;
	
	public Blackboard() {  // ctor vuoto --> init blackboard vuota
		valid = false;
	}
	public Blackboard(T initial) {  // ctor initial --> init blackboard a initial
		message = initial;
		valid = true;
	}
	
	// Setta mess + valid = true + sveglia tutti thread in wait
	public synchronized void write(T mess) {
		message = mess;
		valid = true;
		notifyAll();
	}
	public synchronized T read() throws InterruptedException {
		while (!valid)   // Se valid = false --> aspetta
			wait();
		return message;  // Altrimenti legge e ritorna
	}
	// Fanno solo questo
	public synchronized void clear() { valid = false; }
	public boolean dataAvailable() { return valid; }
}
```

###### Esempio blackboard

Utile usare una *blackboard* quando si vuole che un messaggio venga scritto e permanga finché non invalidato o sovrascritto; fino a quel punto, i lettori leggeranno il dato come e quando vogliono.

Ci sono anche altre varianti: tipo quella che ha `read` con ***timeout***, quella che esegue <u>lettura non bloccante</u>, quella che aspetta che almeno 1 thread legga prima di sovrascrivere.

#### Broadcast

Un ***broadcast*** permette ad 1 o più mittenti (*sender*) di inviare un messaggio a dei thread se essi sono in attesa. Tale struttura è particolare in quanto: <u>solo i thread in attesa</u> (con *busy waiting*) <u>ricevono il messaggio</u> (<u>poi non più accessibile</u>, i nuovi thread si metteranno in attesa del prossimo messaggio) e il <u>messaggio</u> (seppur il mittente non si blocca mai) <u>si perde</u> se <u>nessuno è in attesa</u> o se <u>c'è un altro messaggio in corso</u> (ancora non letto da tutti i thread in *waiting*).

```java
public class Broadcast<T> {
	private T message;
	private boolean sending = false;  // true se un mess sta ancora venendo letto
	private int waiting = 0;          // n° thread in attesa del mess
	
	// send() solo se --> nessuno sta leggendo un mess + almeno 1 thread in attesa del mess
	public synchronized void send(T message) {
		if (waiting > 0 && !sending) {
			this.message = message;
			sending = true;
			notifyAll();
		}
	}
	public synchronized T receive() throws InterruptedException {
		waiting++;
		try {
			while (!sending)      // wait() finché non arriva un mess
				wait();
		} finally {
			waiting--;
			if (waiting == 0)     // Ultimo receiver indica che finito il broadcast di tale mess
				sending = false;
		}
		return message;
	}
}
```

###### Esempio broadcast

Il *broadcast* si usa in casi come speaker radiofonici (thread) inviano segnali a delle radio (thread), le quali li ascoltano. L'oggetto broadcast è condiviso dai 2 (che sono dei thread) e le radio ascoltano i messaggi nel broadcast quando vogliono, tuttavia c'è il problema dei multipli messaggi, che siano fatti da 1 o più thread, se nessuno è in ascolto o un 2° messaggio viene mandato prima che le radio abbiano ricevuto il 1°, i messaggi dopo il 1° sono persi (questo si risolverebbe con una `queue` di messaggi).

#### Barrier

Una ***barrier*** è un punto di sincronizzazione (non un costrutto di comunicazione, quello va implementato in altri modi) dove i thread che la raggiungono sono <u>bloccati</u> (vanno in *waiting*) finché tutti i thread che la devono raggiungere non ci arrivano. 

Semplicemente, i thread che devono bloccarsi ad una *barrier* chiamano `waitB()` e vanno in *waiting* finché non arriva anche l'ultimo, il quale poi apre la barriera permettendo a tutti i thread in attesa su essa di passare (riprendere).

Se si implementa un meccanismo per contare i cicli, si può usare `waitCycle(int n)` per bloccare dei thread finché la *barrier* non si apre per la `n`-esima volta.

```java
public class Barrier {
    private final int need;             // n° di thread che aspettano (che servono x aprire)
    private int arrived = 0;            // n° di thread arrivati
    private boolean releasing = false;  // flag che indica se barriera aperta/chiusa (init chiusa)
    private int cycle = 0;              // conta i cicli

    public Barrier(int n) {
        need = n;
    }

    public synchronized void waitB() throws InterruptedException {
        // Se barrier ancora aperta --> aspetta che si richiuda
        while (releasing)
            wait();
        arrived++;
        try {
            // Aspetta finché non arrivano tutti
            while (arrived < need && !releasing)  // --> releasing check fa passare tutti (non 1 solo)
                wait();
            // Ultimo thread entrato apre barrier
            if (arrived == need) {
                releasing = true;
                cycle++;
                notifyAll();
            }
        } finally {
            arrived--;
            // Ultimo thread uscito chiude barrier
            if (arrived == 0) {
                releasing = false;
                notifyAll();  // sveglia thread x ciclo successivo
            }
        }
    }
    
    // Blocca un thread fino al ciclo di n° specificato
    public synchronized void waitCycle(int n) throws InterruptedException {
        while (cycle < n)
            wait();
    }
}
```

##### CyclicBarrier

Java mette a disposizione `java.util.concurrent.CyclicBarrier` la cui funzione è la medesima della precedente ma che ha anche un comando `Runnable barrierAction` (opzionale) eseguito subito prima che la *barrier* si apra per far passare tutti i thread (per fare qualcosa appena i thread sono tutti fermi prima di uscire).

Cambiano un paio di cose, tipo: `await()` al posto di `waitB()`, la `barrierAction` in un 2° costruttore, eccezioni diverse (`BrokenBarrierException` , `TimeoutException`) e un metodo `reset()` usato per riavviare la barriera.

---

Prossima lezione: [[]]

