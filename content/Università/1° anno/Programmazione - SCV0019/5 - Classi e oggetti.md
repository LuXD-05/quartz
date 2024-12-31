# Lezione 5

### Classi e oggetti

##### Classe

Una **classe** è un modello che specifica lo <u>stato</u> e il <u>comportamento</u> delle sue istanze, che si dicono [[#Oggetto|oggetti]]. Quindi, per "istanziare" oggetti di una classe si usa il:

###### Costruttore

(A meno che non sia **statica**), è necessario "costruire" una classe per istanziarne un oggetto ed usare i suoi metodi. La sintassi comprende: `new Class(...)`, dove:

- `new` è una *keyword* necessaria ad istanziare l'oggetto,
- `Class` è il nome della classe,
- `(...)` indica che si sta chiamando il metodo costruttore della classe (una classe può avere più costruttori, quindi si decide quale usare in base ai parametri `...`).

##### Oggetto

Ogni oggetto è quindi un'<u>istanza di una classe</u>. I loro metodi dipendono dalla classe di cui sono istanze.

Istanziare un oggetto significa allocare lo spazio per esso in memoria; infatti ogni oggetto ha come tipo la sua classe, che è di [[2 - Variabili e lessico#Tipi di riferimento|tipo riferimento]] siccome "punta" all'indirizzo di memoria dello stesso. Un esempio è: `Class c = new Class()`, dove `c` è l'oggetto da cui si potrà accedere ai [[6 - Metodi#Metodi|metodi]] della sua classe.

###### Overloading

(Vedi prima [[6 - Metodi#Metodi|metodi]]) quando 2 metodi/classi hanno lo stesso nome ma parametri diversi (per tipologia o numero). Questo funziona in quanto il compilatore capisce automaticamente dai parametri quale metodo chiamare

###### Overriding

(Vedi prima [[#Ereditarietà|ereditarietà]]) quando un metodo di una classe base è <u>ridefinito</u> in una classe derivata. Questo permette di adattare il comportamento di uno stesso metodo ad una certa classe in base al tipo della stessa (fa una cosa se è la base e un'altra se è una derivata).

> [!info] Fasi
> L'*overriding* è risolto in fase di esecuzione in quando:
> - <u>Compilazione</u>: ***early binding***, ovvero il compilatore <u>individua le firme candidate a soddisfare la chiamata</u> in base a n° e tipo dei parametri compatibili e accessibilità al codice chiamante (se non ce ne sono segnala errore); poi si <u>sceglie quella più specifica</u> (che richiede il minor n° di promozioni di parametri),
> - <u>Esecuzione</u>: ***late binding***, viene scelto il metodo con la firma scelta in base al tipo dell'oggetto chiamante.

#### Ereditarietà

L'ereditarietà è un meccanismo che permette ad una **classe derivata** (da un'altra, detta anche *sottoclasse*) di <u>ereditare attributi e metodi</u> da una **classe base** (o *superclasse*).

Non tutto della base è necessariamente ereditato dalla classe derivata e ciò si vede anche con una rappresentazione grafica (UML):

![](https://i.imgur.com/pzjYMM6.png)

Qui la classe `Rettangolo` ha certi metodi, ma solo quelli conformi anche alla classe derivata `Quadrato` sono ereditati da essa (eventualmente vengono ridefiniti in `Quadrato` se è necessario un comportamento diverso).

> [!important] Ereditarietà classi
> In codice, per dire che una classe eredita da un'altra si usa `extends` e poi la classe base:
> ```java
> class Sub extends Super {
> 	//...
> }
> ```

##### Relazione "is-a"

Tra classi base e sottoclassi esiste una relazione "***is-a***", ovvero "*è un*" secondo la quale una sottoclasse "*è una*" classe base (ma non il contrario). Tradotto in codice questo significa che è possibile istanziare una sottoclasse avente come tipo una classe base:

```java
// Supponendo di avere una classe base Rettangolo e una sottoclasse Quadrato:
Rettangolo r = new Quadrato(5); // Quadrato di lato 5 --> Rettangolo con base = altezza = 5
```

Per verificare se un oggetto è un'istanza di una certa classe si usa la keyword `instanceof`:

```java
if (r instanceof Quadrato)
	out.print("Quadrato");
else
	out.print("Rettangolo");
```

###### Cast di classi

Supponiamo si debba accedere ad un metodo di una classe `Quadrato` specifico per essa e non presente in `Rettangolo`, ma si ha preso un oggetto di tipo `Rettangolo` e non si sa se sia veramente un `Rettangolo` o un `Quadrato`.

Per questo prima si verifica con `instanceof` se è un `Quadrato`. Se lo è allora si può fare un cast del tipo: `Quadrato q = (Quadrato)r;` per poi accedere al metodo di `q`.

#### Astrazione

Esistono delle classi **astratte**, discriminate dal modificatore `abstract` che non possono essere istanziate ma possono avere delle sottoclassi che ereditano da esse.

Tali implementano metodi anch'essi **astratti**, i quali devono essere necessariamente ridefiniti all'interno delle sottoclassi **concrete** che ereditano dalla classe base astratta.

Nel seguente esempio tutte le classi che estendono `Figura` dovranno implementarne i metodi:

```java
public abstract class Figura {
	public abstract double getArea();
	public abstract double getPerimetro();
}
public class Rettangolo extends Figura {
	public double getArea() {
		// base * altezza
	}
	public double getPerimetro() {
		// 2 * (base + altezza
	}
}
```

Quindi:

```java
Figura f = new Rettangolo(); // valido
Figura f = new Figura();     // invalido
```

### Enum

Gli `enum` sono delle strutture che contengono valori fissi numerati in base all'ordine in cui i valori sono definiti. In fase di esecuzione, la JVM crea un oggetto per ogni valore dell'`enum` e ne memorizza il riferimento nella costante corrispondente. Esempio:

```java
public enum Mese {
	GENNAIO, FEBBRAIO, MARZO, APRILE, MAGGIO, GIUGNO, LUGLIO, AGOSTO, SETTEMBRE, OTTOBRE, NOVEMBRE, DICEMBRE;
}
```

La classe generica `enum` implementa l'interfaccia [[#Comparable|Comparable]] e quindi il metodo `compareTo(T obj)` (solo che è `final` in `enum`).

###### Metodi enum

- `public String name()`: ?
- `public int ordinal()`: ?
- `public int compareTo(T obj)`
- `public static T[] values()`: restituisce l'array delle costanti di tipo `T` nell'`enum`.

##### Campi

Per ogni `enum` è possibile definire costruttori, attributi e metodi. Questi sono usati dalla JVM per costruire le istanze corrispondenti alle costanti. Esempio:

```java
public enum Mese {
	// Costanti
	GENNAIO("Gennaio", 31), FEBBRAIO("Febbraio", 28)...
	// Campi
	private String nome;
	private int nGiorni;
	// Costruttori
	private Mese(String nome, int nGiorni) {
		this.nome = nome;
		this.nGiorni = nGiorni;
	}
}
```

### Interfacce

Le **interfacce** sono simili alle classi astratte in quanto specificano il prototipo di certi metodi senza fornirne alcuna implementazione.

Una classe che implementa un'interfaccia deve implementarne tutti i metodi; a meno che tale classe non sia <u>astratta</u>.

> [!important] Implementazione interfacce
> In codice, per dire che una classe implementa un'interfaccia si usa `implements` così:
> ```java
> class Class implements Interface {
> 	//...
> }
> ```

###### Definizione

Le interfacce si definiscono con la keyword `interface`:

```java
public interface Interface {
	void method();
}
```

Nota che, come le classi, delle interfacce possono estendere anche altre interfacce.

###### Uso interfacce

Le interfacce sono anche usate come tipi di riferimento (*supertipi* per tutte le classi che le implementano), infatti è possibile una cosa del genere:

```java
Comparable<Integer> i = 10;                // esempio 1
Comparable<Frazione> f = new Frazione(1,2) // esempio 2
```

##### Comparable

L'interfaccia `Comparable<T>` specifica un unico metodo il cui scopo è definire un ordine sugli oggetti che la implementano. Essa specifica il metodo `public int compareTo(T obj)`, che confronta l'oggetto che chiamante con quello passato, ritornando:

- $-1$: se l'<u>oggetto chiamante</u> è **minore** del <u>parametro</u>,
- $0$: se l'<u>oggetto chiamante</u> è **uguale** al <u>parametro</u>,
- $1$: se l'<u>oggetto chiamante</u> è **maggiore** del <u>parametro</u>,

##### Iterable

L'interfaccia `Iterable<T>` rappresenta una [[7 - Array e collezioni#Collezioni|collezione]] "iterabile", ovvero scandibile 1 elemento per volta tramite un oggetto detto ***iteratore***. Ha 1 solo metodo: `public Iterator<T> iterator()` che ritorna l'iteratore degli oggetti di tipo `T` della collezione che esegue il metodo. 

###### Iterator

Un `Iterator<T>` ha 2 metodi:

- `public T next()`: ritorna il prossimo elemento a cui punta l'iteratore eliminandolo dallo stesso (non dalla collezione per la quale l'iteratore è stato creato); lancia eccezione se non ha un prossimo elemento.
- `public boolean hasNext()`: ritorna `true` se l'iteratore ha un elemento successivo, altrimenti `false`.

Quindi:

```java
List<String> l = new ArrayList<String>();
Iterator<String> iterator = l.iterator();
while (iterator.hasNext()) {
	out.println(iterator.next())
}
```

# Esercizi

# Soluzioni

---

Prossima lezione: [[6 - Metodi]]

