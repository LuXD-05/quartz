# Lezione 6

### Software design "in piccolo"

Il software design "in piccolo" si concentra sul definire le parti di un software sempre in termini astratti ma pronti per essere implementati, garantendo alta qualità, basso effort e poco tempo. 

##### Problemi

Esempio: vogliamo creare una classe `IntegerSet` (insieme di numeri interi) che contiene interi:

```java
public class IntegerSet {
    public final static int SIZE = 10;
    public int n;
    public int list[] = new int[SIZE];
    
    public int search(int x) {
        for (int i = 0; i < n; i++) {
            if (list[i] == x) return i;
        }
        return -1;
    }
}
```

E tali interi sono gestiti diversamente tra pari e dispari con delle classi di supporto:

```java
// NUMERI PARI
public class EvenManager {
    public IntegerSet set = new IntegerSet();

    public void add(int x) {
		if (x % 2 == 0 && set.n < IntegerSet.SIZE) {    // Cambia solo sto check
            set.list[set.n] = x;
            set.n++;
        }
    }
}
// NUMERI DISPARI
public class OddManager {
    public IntegerSet set = new IntegerSet();

    public void add(int x) {
        if (x % 2 == 1 && set.n < IntegerSet.SIZE) {    // Cambia solo sto check
            set.list[set.n] = x;
            set.n++;
        }
    }
}
```

Ci sono però 3 caratteristiche da garantire per un buon design che questo codice non ha:

###### Modificabilità del software

Supponiamo di voler avere più di 10 numeri: bisogna cambiare da `int[]` a una lista. A quel punto dovrei fare un casino con tutte le altre classi in quanto va trasformata tutta la gestione da array a lista (e solo quella), quindi si spreca tempo, effort e si rischiano altri difetti.

###### Integrità dei dati

Se diverse funzioni possono accedere liberamente ai dati di una classe, c'è il rischio che vi siano problemi quando tali <u>usano o cambiano</u> tali dati. Per garantire l'**integrità dei dati** è necessario controllare che essi siano validi dopo essere stati cambiati e prima di venire usati; per esempio potremmo inserire un controllo per evitare l'inserimento di duplicati.

###### Riusabilità dei componenti

Un componente è **riutilizzabile** quando è possibile <u>usarlo in contesti diversi senza doverlo riscrivere da 0</u>. Per rendere la classe riutilizzabile, bisogna quindi centralizzare le operazioni cosicché non debbano essere ridefinite in ogni nuovo client (che usa `IntegerSet`), avere metodi che abbiano lo stesso comportamento indipendentemente dalli dati...

###### Soluzione

Per garantire tutto questo, si propone come soluzione l'uso di **moduli**. Quindi alla fine avremmo:

```java
// Classe per elementi di lista concatenata (ognuno punta al prossimo)
public class IntegerListNode {
    public int item;
    public IntegerListNode next;

    public IntegerListNode(int item) {
        this.item = item;
        this.next = null;
    }
}
// Nuovo IntegerSet
public class IntegerSet {
    public IntegerListNode firstNode;

	public void add(int value) {
		// Evita duplicati
		if (search(value) == null) {
	        IntegerListNode newNode = new IntegerListNode(value);
			newNode.next = firstNode;
			firstNode = newNode;
		}
    }

    public IntegerListNode search(int value) {
        IntegerListNode ref = firstNode;
        while (ref != null && ref.item != value) {
            ref = ref.next;
        }
        return ref;
    }
}
// NUMERI PARI
public class EvenManager {
    public IntegerSet set = new IntegerSet();
    public void add(int x) {
		if (x % 2 == 0) set.add(x);
    }
}
// NUMERI DISPARI
public class OddManager {
    public IntegerSet set = new IntegerSet();
    public void add(int x) {
		if (x % 2 == 1) set.add(x);
    }
}
```

#### Moduli

Un **modulo** è una parte di un sistema che offre certi servizi ad altri moduli (i **servizi** sono elementi di computazione che altri moduli potrebbero usare).

L'**interfaccia** di un modulo è l'insieme di servizi che fornisce (esportati ad altri moduli) ed è l'unica parte del modulo che permette l'interazione (moduli fatti da corpo e interfaccia).

##### Tipi di moduli

###### Operazione astratta

In pratica un semplice **metodo** o funzione (seppur sempre da dichiarare in una classe), dove la <u>firma è l'interfaccia</u> e il <u>contenuto</u> del metodo è il <u>corpo</u> del modulo.

![](https://i.imgur.com/BehurSz.png)

###### Oggetto astratto

Un **oggetto astratto** è un <u>modulo che incapsula una struttura dati ed esporta delle operazioni</u> di cui non sono permesse istanze multiple, e ciò si ottiene tramite implementazione con classi anonime:

![](https://i.imgur.com/Xd9ugNQ.png)

###### Tipo astratto

Un **tipo astratto** permette invece istanze multiple ma non ereditarietà, quindi in java si dichiara con la *keyword* `final`:

![](https://i.imgur.com/cSQOg6v.png)

###### Classe

Un **tipo di dato astratto** che <u>permette ereditarietà</u>, contenente metodi e proprietà chiamati **membri**, i quali possono essere di istanza (personali di ogni oggetto) o di classe (statici).

##### Visibilità

I membri di un modulo hanno diversi livelli di visibilità:

- ***Public***: membri accessibili dall'esterno, generalmente solo metodi in quanto non è consigliato avere dati pubblici nei moduli (si usa l'***encapsulation*** per nascondere dati e metodi pubblici per permettere l'accesso a certe funzionalità specifiche del modulo),
- ***Protected***: membri accessibili dalla classe e istanze, da altre classi nello stesso *package* e da sottoclassi,
- ***Package-protected***: è la visibilità di default (senza *keyword*) ed è come *protected* ma senza l'accesso da sottoclassi,
- ***Private***: membri non accessibili dall'esterno (dati dovrebbero essere *private*, ma anche metodi possono esserlo).

> [!info] ***Friend*** visibility
> La visibilità *friend* è particolare in quanto permette ad un certo metodo o classe di accedere ai membri non pubblici di un'altra classe (non simmetrica, transitiva o ereditaria):
> - *Friend function*: una funzione *non-member* di una classe ma che ha accesso ai suoi membri *private* e *protected*,
> - *Friend class*: una classe di cui tutti i metodi diventano *friend* di un'altra classe (quindi permesso l'accesso a membri *private* e *protected*).

##### Altri modificatori

- ***Static***: classi e membri statici sono inizializzati a *runtime*; le classi possono usare solo i membri statici mentre i membri sono unici per tale classe e tutti i suoi oggetti.
- ***Final***: classi con attributo `final` non possono avere figli che ereditano da esse, mentre membri `final` non possono essere ridefiniti nelle sottoclassi.
- ***Abstract***: classi `abstract` invece devono necessariamente essere estese per ereditarietà, come i metodi `abstract` vanno ridefiniti nelle sottoclassi (classi non istanziabili e metodi non richiamabili).

##### Interfacce

Le interfacce sono strutture denominate dalla *keyword* `interface` e definiscono una sorta di "scheletro" in cui tutti i metodi sono `public abstract` (necessariamente da ridefinire) e tutti i dati sono `public final static`.

![](https://i.imgur.com/YVGfpFf.png)

##### Costruttori

Parlando di classi ognuna ha almeno 1 costruttore, un metodo che ne inizializza le proprietà quando un oggetto di quella classe è istanziato. Di 3 tipi:

- *Default*: costruttore senza parametri,
- *With params*: costruttore con parametri personalizzabili,
- *Copy*: costruttore che accetta un oggetto della stessa classe per copiarne le proprietà all'interno di quello che si istanzia.

##### Generics

Si possono definire classi e metodi anche non sapendo il tipo di parametro che gli si sta passando, basta usare il tipo generico `<T>`, tuttavia bisogna fare attenzione alla gestione dei parametri in quanto il metodo non deve crashare se incontra un tipo di dato inaspettato:

![](https://i.imgur.com/AmoIWUL.png)

#### Metodi

Tutte le caratteristiche dei metodi sono descritte dalla ***signature*** (firma):

![](https://i.imgur.com/IP3daJx.png)

La firma dei metodi deve essere più chiara possibile, al fine di evitare commenti per spiegare ogni metodo cosicché si possa capire cosa fa solo dalla firma (per quanto possibile).

##### Overloading e overriding

**Overloading**: più metodi con nome uguale ma firma diversa.

**Overriding**: metodo di una sottoclasse che ridefinisce il comportamento di uno con lo stesso nome della classe base.

![](https://i.imgur.com/otBJe5L.png)

##### Parametri

I parametri di un metodo possono essere passate ad esso in 3 modi diversi (preceduti dalle seguenti keyword):

- `in`: al metodo viene passato solo il **valore** del parametro, in <u>caso di modifiche a tale valore all'inderno del metodo</u>, la <u>variabile passata rimane invariata</u>.
- `out`: al metodo si passa una **variabile** da inizializzare, quindi il parametro potrebbe non avere ancora un valore ma è necessario che alla fine del metodo il parametro abbia assegnato un valore (tale <u>permarrà all'infuori del metodo nella variabile passata</u>).
- `inout`: si passa solo il valore al metodo ma potrebbe comunque cambiare (misto dei 2 precedenti).

##### Categorie

Nelle classi ci sono 3 tipi di metodi:

- ***Utility***: metodi privati necessari al funzionamento interno della classe,
- ***Getters***: metodi non privati la cui funzione è di accedere ai dati privati della classe rendendoli disponibili all'esterno,
- ***Setters***: metodi non privati il cui compito è di permettere la modifica dei dati privati della classe dall'esterno.

#### Design by contract

Quest'ultima parte dice solo minchiate, il mio amico [ChatGPT](https://chatgpt.com) vi darà una mano riassumendo al posto mio che mi sono anche rotto il cazzo 🥀:

![](https://i.imgur.com/9bh0C57.png)

---

Prossima lezione: [[7 - Design in grande]]

