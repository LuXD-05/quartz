# Lezione 11

### Serializzazione

La **serializzazione** è la conversione di un oggetto (o grafo di oggetti) in una sequenza di byte per salvarlo o trasferirlo (tipo con socket); ed il suo contrario è la **deserializzazione**. In Java si usa `ObjectOutputStream` per scrivere e `ObjectInputStream` per leggere.

##### Regole

Per serializzare un oggetto ci sono delle regole:

- La sua classe deve implementare l'interfaccia `Serializable`,
- L'interfaccia richiede di definire `private static final long serialVersionUID = 1L;` (se no `InvalidClassException`).
- I campi con keyword `static` non vengono serializzati (sono della classe, non dell'istanza).
- I campi con keyword `transient` non vengono serializzati (si usano per oggetti non serializzabili, tipo `Thread`).
- Se una classe serializzabile <u>deriva</u> da una classe non serializzabile, quest'ultima deve avere un costruttore vuoto (se no `InvalidClassException`).
- Se un campo (non `transient`) di un oggetto serializzabile referenzia una classe non serializzabile, viene lanciata `NotSerializableException`.

#### Object stream su socket

Invece di usare `BufferedReader`/`PrintWriter` (che inviano testo), si "montano" sugli stream del socket gli stream di oggetti per inviare dati binari:

```java
public class Server {
	try (ServerSocket server = new ServerSocket(PORT);
	     Socket socket = server.accept();
	     ObjectOutputStream out = new ObjectOutputStream(socket.getOutputStream())) 
	{
	    out.writeObject(new Person("nome"));  // serializza l'oggetto sul socket
	}
}
public class Client {	
	try (Socket socket = new Socket(SERVER_IP, PORT);
	     ObjectInputStream in = new ObjectInputStream(socket.getInputStream())) 
	{
	    Person p = (Person) in.readObject();  // legge l'oggetto dal socket + cast
	}
}
```

> [!warning] ClassNotFoundException
> Quando si deserializza, la JVM riceve solo byte. Se il programma che legge non ha il file `.class` dell'oggetto che sta deserializzando (o non è nei suoi import), il programma non sa come ricostruire l'oggetto e lancia `ClassNotFoundException`.

##### Serializzazione custom

Non gestendo oggetti `transient` o `static`, per essi (on in generale) si vorrebbe  magari effettuare un certo comportamento alla serializzazione/deserializzazione; e ciò si fa con 2 metodi di `Serializable`: 

\- `private void writeObject(ObjectOutputStream out)`: ridefinisce le azioni da fare alla serializzazione,

\- `private void readObject(ObjectInputStream in)`: ridefinisce le azioni da fare alla deserializzazione.

Ci sono poi 2 metodi di base per le ridefinizioni di `readObject()` e `writeObject()`:

\- `in.defaultReadObject()`: converte lo stream di bytes in lettura permettendo di assegnare i valori dell'oggetto streammato all'istanza corrente,

\- `out.defaultWriteObject()`: converte l'oggetto da serializzare in bytes da inviare sullo stream.

Questi di base si mettono <u>sempre</u> quando si ridefiniscono `readObject()` e `writeObject()` (a meno che non si vuole leggere dato per dato).

In più specificando in tali metodi delle funzioni tipo `in.readInt()` o `out.writeInt()` è possibile ricevere ed inviare i valori dei campi statici tra le classi.

Esempio:

```java
// Classe thread che si auto-starta (con init()) --> vogliamo farlo ripartire alla deserializzazione)
public class PersistentClock implements Serializable, Runnable {
    private static final long serialVersionUID = 1;
    private transient Thread t;
    private static int x = 1;
    private int i;

    public PersistentClock(int i) {
	    this.i = i;
        init();      // Non chiamato in deserializzazione
    }

    private void init() {
        t = new Thread(this);
        t.start();
    }
    public void run() {
	    //...
    }

    // Perciò si ridefinisce la deserializzazione con questo
    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
        in.defaultReadObject();
        x = in.readInt();  // Legge dallo stream il valore del campo statico "x" e glielo assegna
        init();            // Chiama init() (quando deserializzato)
    }
    // (non serve in sto caso)
    private void writeObject(ObjectOutputStream out) throws IOException, ClassNotFoundException {
        out.defaultWriteObject();
        out.writeInt(x);  // Passa alla classe di destinazione il campo statico "x"
        //...
    }
}
```

---

Prossima lezione: [[]]

