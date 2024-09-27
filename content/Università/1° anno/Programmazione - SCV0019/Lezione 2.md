### Java

> [!important] Programma java
> Costituito da un insieme di oggetti che cooperano per realizzare un obiettivo.

File con estensioni .java

Si compila con comando `javac file.java`, il che genera il file `file.class`, ovvero il file col bytecode.

Per eseguire il bytecode fare `java file` con solo il nome della <u>classe</u> da eseguire. Se essa e il file si chiamano in modo diverso e si prova a eseguire `java file` (mentre la classe magari si chiama Class), non funzionerà. Nominare sempre file java con lo stesso nome della classe che contiene.

### Paradigmi

OOP è uno dei paradigmi di programmazione:

- Imperativo,
- Funzionale,
- Logico.

> [!important] Protocollo
> a

Fondamentale è la scomposizione e riutilizzo del codice, infatti la creazione di componenti riutilizzabili è uno degli obiettivi della OOP.

### Classi e oggetti

##### Classe

Modello che specifica lo stato e il comportamento di tutte le sue istanze ([[#Oggetto|oggetti]]).

###### Costruttore

A meno che la classe non sia **statica** è necessario "costruirla" per creare l'oggetto ed usare i suoi metodi.

La sintassi comprende: `new Class(...)`, dove:

- `new` è una *keyword* necessaria ad istanziare l'oggetto,
- `Class` è il nome del costruttore che coincide con quello della classe (indipendentemente da quale sia, una classe può avere + costruttori),
- `...` sono gli argomenti del costruttore.

##### Oggetto

Ogni oggetto è quindi un'istanza di una classe. I metodi degli oggetti dipendono dalla classe di cui sono istanze.

Quando si istanzia un oggetto è necessario memorizzarlo in qualche modo. Siccome l'operazione di creazione/istanziazione alloca lo spazio per l'oggetto in memoria, per "puntare" all'indirizzo di memoria di un oggetto è necessario usare una variabile in questo modo: `Class c = new Class()`, dove:

Per semplicità trattare `c` come l'oggetto vero e proprio, da cui si potrà accedere ai metodi della sua classe.

###### Overloading

Quando 2 metodi/classi hanno lo stesso nome ma parametri diversi (per tipologia o numero).

> [!important] Espressioni
> Sequenze di operatori ed operandi costruite secondo le regole sintattiche del linguaggio.
> Le espressioni hanno un tipo complessivo, determinato (in fase di compilazione) dagli operatori e dal tipo degli operandi. In fase di esecuzione, originano un valore.

(new ...() = espressione di creazione):

- Tipo: la classe dell'oggetto costruito,
- Valore: riferimento all'oggetto della classe specificata.

Garbage collector

Oggetti e memoria non utilizzati sono automaticamente eliminati

##### Import

...

### Classe String

La classe `String` modella stringhe, ovvero sequenze di char (caratteri)

