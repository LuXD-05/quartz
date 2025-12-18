# Lezione 17

### Design patterns

Un ***design pattern*** è uno schema riutilizzabile per risolvere problemi; in particolare descrive oggetti e classi comunicanti adattabili per risolvere problemi di progettazione (perciò sono relativamente astratti, non complessi o *domain-specific*, cosicché possano essere utilizzati in app diverse).

![](https://i.imgur.com/StVfZMz.png)

##### Caratteristiche

Un *design pattern* identifica in particolare:

- Classi (e istanze) del problema,
- Associazioni e ruoli,
- Modalità di comunicazione/collaborazione tra le classi,
- Distribuzione delle responsabilità.

###### Vantaggi

Coi *design pattern* diventa più semplice sviluppare applicazioni in quanto forniscono soluzioni consolidate e già testate per vari problemi (si sa già cosa si deve fare).

###### Svantaggi

L'unica pecca è che con essi la struttura del progetto o il codice potrebbero diventare più complessi del necessario; per questo ogni volta va deciso se ne vale la pena o se utilizzare una soluzione ad hoc.

> [!info] Quando usare un design pattern
> Per scegliere se usare un *design pattern* si possono ricordare 2 detti:
> - "*when to doubt, leave it out*": se si è in dubbio nell'uso di un pattern o meno, non usarlo.
> - "*keep it simple*": cercare di non complicare troppo il progetto.

#### Factory

Il ***factory*** pattern ridefinisce la modalità di creazione degli oggetti <u>disaccoppiando il metodo che li crea dal costruttore della loro classe</u>; in pratica, in una classe "*creator*" c'è un metodo "*factory*" che <u>istanzia gli oggetti di 1 o più classi</u> (solo se hanno lo stesso tipo, quindi ereditano tutte da una classe) al posto del loro costruttore

![](https://i.imgur.com/YkuOl3Q.png)

Nell'esempio la `ShapeFactory` è il *creator* che, in base a certi parametri, determina la `Shape` da creare e la sceglie tra quelle che ereditano da `Shape`, così da dover importare solo la *factory* nei moduli e non tutte le `Shape` ogni volta.

#### Singleton

Una classe ***singleton*** è usata in quei casi in cui si vuole avere una sola istanza di un oggetto e ciò si realizza tramite un'istanza statica dello stesso all'interno della sua classe:

![](https://i.imgur.com/9nJGd4k.png)

###### Esempio singleton

```java
public class Singleton { 
	// Istanza statica
	private static Singleton instance; 
	// ctor
	private Singleton() {
		// ...
	} 
	// Metodo che ottiene l'istanza se c'è, altrimenti la crea
	public static Singleton getInstance() { 
		if (instance == null) { 
			instance = new Singleton(); 
		} 
		return instance; 
	}
}
```

#### Flyweight

In una situazione in cui si hanno <u>tanti oggetti identici e immutabili usati contemporaneamente</u> si hanno grandi sprechi di memoria; per risolvere ciò si usa il ***flyweight*** pattern, che fa uso di una `FlyweightFactory` che gestisce tali oggetti già istanziati in una struttura come una tabella o una `HashMap` e permette, dato un identificatore posizionale, di ritornare l'oggetto in quella posizione della struttura (se in tale posizione l'oggetto non c'è, lo crea).

![](https://i.imgur.com/5lo1FLc.png)

Con questo pattern è possibile (se c'è un alto grado di condivisione degli oggetti):

- Risparmiare memoria,
- Risparmiare tempo non inizializzando gli oggetti duplicati,
- Usare "=\=" invece che `equals` per i confronti.

###### Esempio flyweight

Supponiamo di star creando un videogioco e vogliamo gestire migliaia di oggetti `Tree`, ognuno dei quali ha dati **intrinseci** (invarianti, custom per ogni <u>categoria di albero</u>) ed **estrinseci** (custom per ogni <u>singola istanza di albero</u>):

```java
public class Tree {
	// dati intrinseci --> determinano la categoria di albero
    private final String tipo;
    private final String foglia;

    public Tree(String tipo, String foglia) {
        this.tipo = tipo;
        this.foglia = foglia;
    }

    public void draw(int x, int y, String colore, int altezza) { // dati estrinseci --> custom per ogni albero (passati come parametri)
        System.out.println(/* ... */);
    }
}
```

La nostra `FlyweightFactory` conterrà la `HashMap` con gli alberi del videogioco ed un metodo per ottenerne uno specifico:

```java
public class TreeFactory {
	// Tabella con alberi indicizzati in base a tipo + foglia
    private static final HashMap<String, Tree> trees = new HashMap<>();
    
	// Metodo per ottenere tipo di albero
    public static Tree getTree(String tipo, String foglia) {
        String key = tipo + '|' + foglia;
        // Crea se non esiste
        if (!trees.containsKey(key)) {
            trees.put(key, new Tree(tipo, foglia));
        }
        // Ritorna il tipo di albero
        return tree.get(key);
    }
}
```

In questo modo, istanziati in memoria si hanno solo i tipi di albero diversi, mentre le caratteristiche estrinseche di ogni albero sono definite a runtime:

```java
public static void main(String[] args) {
	// Tipo istanziato
	Tree quercia = TreeFactory.getTree("Quercia", "foglia_verde");
	// Alberi non istanziati
    quercia.draw(10, 20, "verde scuro", 12);
    quercia.draw(15, 30, "verde chiaro", 15);
}
```

L'unico problema è che non si ha la "tracciabilità" degli alberi in quanto non sono salvati in memoria (quindi non si può avere un riferimento ad ognuno di essi). Per avere ciò bisognerebbe definire una classe `TreeType` (con tipo e foglia) e metterla all'interno di `Tree`, ma a quel punto `TreeType` non è altro che un `enum`.

#### State

Quando si hanno degli oggetti mutabili con variabilità molto alta, ovvero che hanno molti stati che cambiano e dei metodi con comportamento dipendente da tali stati (quindi metodi con dentro `if/else/switch` per gestire i casi in base allo stato), è ideale usare lo ***state*** pattern, il quale interpone tra la classe e l'esterno un'interfaccia per la gestione dei suoi stati.

###### Esempio state

Supponiamo di star gestendo gli ordini di un e-commerce che possono essere: "creati", "pagati", "spediti" e "annullati". Creiamo l'interfaccia di stato:

```java
public interface StatoOrdine {
	// Operazioni che variano in base allo stato
    void annulla(Ordine ordine);
    void spedisci(Ordine ordine);
}
```

Ed implementiamola per ogni stato utile per cui i metodi cambiano comportamento:

```java
public class OrdineCreato implements StatoOrdine {
    public void annulla(Ordine o) {
        o.setStato(new OrdineAnnullato());
    }
    public void spedisci(Ordine o) {
        throw new IllegalStateException("Prima paga");
    }
}
public class OrdinePagato implements StatoOrdine {
    public void annulla(Ordine o) {
        o.rimborsa();
        o.setStato(new OrdineAnnullato());
    }
    public void spedisci(Ordine o) {
        o.setStato(new OrdineSpedito());
    }
}
public class OrdineSpedito implements StatoOrdine {
    public void annulla(Ordine o) {
        throw new IllegalStateException("Già spedito");
    }
    public void spedisci(Ordine o) {
        throw new IllegalStateException("Già spedito");
    }
}
```

Facendo così non si hanno più troppe condizioni in ogni metodo ma si gestisce tutto con `StatoOrdine`:

```java
public class Ordine {
    private StatoOrdine stato = new OrdineCreato();
    void setStato(StatoOrdine s) {
        stato = s;
    }
    public void annulla() { stato.annulla(this); }
    public void spedisci() { stato.spedisci(this); }
    public void rimborsa() { System.out.println("Rimborso effettuato"); }
}
```

#### Strategy

Lo ***strategy** pattern* è utile in quei casi in cui si vuole trattare un algoritmo come un oggetto e passarlo ad un metodo per modificare il suo comportamento in base all'algoritmo stesso. Il caso più famoso è con `java.util.Comparator`, che definisce l'algoritmo di confronto tra oggetti dello stesso tipo:

```java
public class AlphabeticComparator implements Comparator<String> { 
	public int compare(String s1, String s2) { 
		return s1.toLowerCase().compareTo(s2.toLowerCase()); 
	}
} 
public static void main(String[] args) { 
	String[] s = new String[30]; 
	// ...
	Arrays.sort(s, new AlphabeticComparator());
}
```

#### Proxy

Un ***proxy*** è un oggetto che si interpone tra un altro e i suoi client presentando la medesima interfaccia dell'oggetto iniziale ma permettendo di controllare gli accessi a quest'ultimo. In pratica tutte le chiamate e interazioni che vengono dai client sono dirette al *proxy* che le gestisce con una logica propria prima di evaderle. 

![](https://i.imgur.com/RcDvZiB.png)

Con questo si può:

- Aggiungere un **ACL** (*Access Control Layer*), strategie di caching... ad un'oggetto,
- Postporre l'istanziazione di oggetti finché non è necessaria (o possibile tipo `Queue`),
- Rendere trasparente la comunicazione con un oggetto remoto...

#### Adapter

Quando si usano delle interfacce (generalmente esterne) diverse o mutabili per fare una certa cosa, spesso la firma dei metodi cambia. Per non suddividere il codice per ogni tipo di interfaccia usata (anche perché magari vengono cambiate) è possibile usare degli ***adapter***: interfacce che ridefiniscono la firma dei metodi usati per adattarla ai propri scopi.

###### Esempio adapter

Supponiamo di voler implementare le strategie di pagamento `PayPal`, `Stripe` e `CreditCard` nella nostra applicazione; le loro interfacce sono, però, tutte diverse:

```java
public class StripeAPI {
    public void charge(double amount) { }
}
public class PayPalAPI {
    public void sendPayment(double amount) { }
}
public class CreditCardAPI {
    public void process(double amount) { }
}
```

Invece di definire un singolo flusso di pagamento con degli `if` per ogni metodo, si crea per ognuno un adapter:

```java
// Interfaccia con metodo che serve
public interface PaymentMethod {
    void pay(double amount);
}
// Adapters (implementano tale interfaccia)
public class StripeAdapter implements PaymentMethod {
    public void pay(double amount) {
        new StripeAPI().charge(amount);
    }
}
public class PayPalAdapter implements PaymentMethod {
    public void pay(double amount) {
        new PayPalAPI().sendPayment(amount);
    }
}
public class CardAdapter implements PaymentMethod {
    public void pay(double amount) {
        new CreditCardAPI().process(amount);
    }
}
```

Ciò ci permette di avere un solo metodo per qualsiasi pagamento:

```java
public class Checkout {
    public void pay(PaymentMethod method, double amount) {
        method.pay(amount);
    }
}
// ...
public static void main(String[] args) {
	Checkout c = new Checkout();
	c.pay(new StripeAdapter(), 10);
	c.pay(new PayPalAdapter(), 10);
	c.pay(new CardAdapter(), 10);
}
```

#### Decorator

Quando si ha una classe più o meno completa con già un'interfaccia stabile ma si vogliono aggiungere delle funzionalità, invece di creare tante sottoclassi è possibile usare dei ***decorator***, classi *wrapper* che contengono la classe iniziale e vi aggiungono delle funzionalità.

###### Esempio decorator

Riprendiamo l'esempio precedente del pagamento (senza *adapter*):

```java
public interface PaymentService {
    void pay(double amount);
}
public class BasicPayment implements PaymentService {
    public void pay(double amount) { }
}
```

Possiamo ora creare un <u>decorator astratto</u> (template per gli altri eventuali *decorators* di `BasicPayment`) ed una sua implementazione concreta (per esempio di logging):

```java
// Decorator astratto
public abstract class PaymentDecorator implements PaymentService {
	// Classe (che implementa da interfaccia) wrappata
    protected final PaymentService wrapped;
    // ctor
    protected PaymentDecorator(PaymentService wrapped) {
        this.wrapped = wrapped;
    }
}
// Decorator contreto
public class LoggingPayment extends PaymentDecorator {
    public LoggingPayment(PaymentService wrapped) {
        super(wrapped);
    }
    public void pay(double amount) {
        System.out.println("LOG: pagamento in corso");
        wrapped.pay(amount);
    }
}
```

Perciò istanziando questi si avrà qualcosa tipo:

```java
// LoggingPayment wrappa BasicPayment
PaymentService service = new LoggingPayment( new BasicPayment() );
service.pay(100);
```

#### Composite

#### Abstract factory

(mettere nel factory?)

#### Façade

#### Observer

#### Altri pattern

##### MVC

---

