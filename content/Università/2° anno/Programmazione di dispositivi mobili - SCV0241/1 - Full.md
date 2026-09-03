# Lezione 1

### KMM

KMM (Kotlin Multiplatform Mobile) = SDK x sviluppo di app cross-platform (codice uguale tra android e iOS).

(get/set autogestiti al contrario di java?)

#### Layering patterns

MVC = obsoleto in quanto le activity diventano sia view sia controller (diventando enormi e difficili da testare).

MVP = legacy, separa bene le logiche ma richiede molto codice *boilerplate* e non è molto compatibile con il lifecycle di android.

MVVM = standard, gestisce perfettamente rotazioni di schermo e dati asincroni.

![381](https://i.imgur.com/Us20Z9E.png)

##### MVC

In MVC, activity/fragment spesso diventavano ***god objects*** contenenti tutto (codici di model, view e controller) ed il problema tipico era che i dati andavano salvati manualmente anche per una rotazione dello schermo:

![476](https://i.imgur.com/yoRfXVx.png)

##### MVVM

MVVM è l'architettura di base x Jetpack con `UIState` (classe contenente lo **stato** della schermata) e `UIEvent` (classe **evento** x gestire le interazioni dell'utente con l'app). 

Questo pattern separa i dati (model) dalle schermate (view) e li interconnette attraverso la logica applicativa (viewmodel)

#### Android studio

Android studio è l'IDE x programmare app android e contiene anche l'android SDK (che include: debugger, librerie, emulatore mobile, ecc...) e degli strumenti come ADB (android debug bridge, che permette di runnare comandi su un android connesso).

##### Gradle

Android studio fa uso di Gradle, un *build automation system*, che permette di automatizzare e gestire la fase di build delle app (compilazione di codice e risorse, packaging in un APK testabile, deploy, signing...); e fa uso di un linguaggio specifico nei suoi files basato su Groovy (linguaggio x OOP x la JVM) invece di XML.

###### Build

Per la fase di build, il progetto è reso un APK, poi il compilatore converte il codice in files DEX, il *packager* combina questi e le risorse nell'APK e poi lo firma:

![296](https://i.imgur.com/jicrilJ.png)

> [!info] Manifest
> Negli APK c'è il file `AndroidManifest.xml` che descrive l'applicazione e indica i componenti che ne fanno parte.

#### Convenzioni

![484](https://i.imgur.com/SyjzRgJ.png)

![487](https://i.imgur.com/LHox0eR.png)

### Kotlin

Kotlin è un linguaggio staticamente tipizzato (variabili devono essere tipizzate in dichiarazione e non ci sono conversioni implicite dinamiche) x android (con altre versioni x la JVM, javascript e piattaforme native).

> [!info] CLI
> Per compilare un file si usa `kotlinc [file].kt` e per eseguirlo si usa `kotlin [file]`.

##### Datatypes

I ***literals*** di kotlin sono i seguenti:

![843](https://i.imgur.com/LB1CiCd.png)

La *type inference* del linguaggio permette l'autodeterminazione dei tipi se viene assegnato un valore alla variabile in dichiarazione; in ogni caso il tipo si dichiara cosi: `val variabile: Tipo`.

(In più i char non possono essere usati come numeri, ma le stringhe possono essere accedute e iterate come se fossero degli array).

##### Variabili

In kotlin <u>ogni tipo è un oggetto</u> (non ci sono tipi primitivi come in Java) e le variabili possono essere dichiarate in 2 modi:

- `val`: indica che la variabile è **immutabile** e non è possibile riassegnarvi un valore con "=" (diverso da `const`, il cui valore è calcolato a *compile-time* e non a *runtime*).
- `var`: indica che la variabile è **mutabile** (usarla meno di `val` e solamente se la variabile <u>deve</u> cambiare x forza).

###### Stringhe

Come in Java, qui possono anche essere usate come array con degli ***iterators***:

![295](https://i.imgur.com/XTlzwlJ.png)

Accedute con l'***indexing operator***: `string[index]` e anche interpolate:

![483](https://i.imgur.com/jbFZyqv.png)

###### Array

Gli array in kotlin non si creano con `[]`, ma con vari altri modi, quali `arrayOf()`, `arrayOfNulls()` e il costruttore `Array()`:

![434](https://i.imgur.com/OEH3jCw.png)

###### Null safety

Per la gestione dei valori `null` e la prevenzione di `NullPointerException` ci sono 4 operatori:

- `?`: dopo un tipo (come `String?`) indica che quel campo accetta valori di quel tipo e anche valori `null`,
- `?.`: accesso ad una proprietà di un oggetto ritorna `null` se non esiste,
- `?:`: (*Elvis operator*) se il valore dell'espressione a sinistra è `null`, usa l'espressione a destra,
- `!!`: (*not null assertion*) tratta la variabile a cui è affisso come `not-null` (se lo è però eccezione).

##### Altri costrutti

###### When

Kotlin al posto di `switch` ha `when`, che è simile e non ha bisogno di `break`:

![377](https://i.imgur.com/xOY2EFK.png)

###### Ranges

Quando si lavora con numeri (e altro) in dei cicli, si possono usare i ***ranges***, tipi che rappresentano una progressione lineare di tipi e si costruiscono o con `rangeTo()`, oppure con il corrispondente operatore `..`.

![318](https://i.imgur.com/iwSqufW.png)

> [!important] `in`
> Dalla foto precedente si nota la keyword `in`, che si può usare sia come `.contains()` sia per ciclare all'interno di un range/lista/mappa...
> ```kotlin
> // contains use
> if (x in list) { /* ... */ }
> // loop use
> for (item in list) { /* ... */ }
> ```

#### Classi

Classi dichiarate uguali a Java solo che i parametri della firma del costruttore (e dei metodi in generale) sono da dichiarare con `var`/`val` (oltre a nome e tipo).

###### Costruttori

Il costruttore **primario**:

![631](https://i.imgur.com/eGSlCZG.png)

Il costruttore **secondario** (e seguenti):

![706](https://i.imgur.com/7p5yMZW.png)

I blocchi `init` sono dei semplici blocchi eseguiti <u>dopo il costruttore primario / inizializzazione proprietà</u> nell'ordine in cui compaiono nella classe:

![247](https://i.imgur.com/Bm8y0hc.png)

##### Classi astratte

Le classi astratte possono avere **stato** (variabili d'istanza), metodi concreti e metodi astratti (questi ultimi vanno x forza implementati nelle sottoclassi):

![320](https://i.imgur.com/54S8e3O.png)

###### Ereditarietà

![570](https://i.imgur.com/Rcw6vw7.png)

##### Interfacce

Le interfacce differiscono dalle classi astratte solo per il fatto che <u>non possono salvare stati</u>, mentre possono contenere dichiarazioni di proprietà/metodi astratti e implementazioni di tali proprietà/metodi (x le proprietà sono getters e setters):

![208](https://i.imgur.com/fFYIlti.png)

### Programmazione funzionale

Kotlin dispone di costrutti di programmazione funzionale (stile dove le funzioni sono trattate come valori).

##### Lambda

Una ***lambda*** è una **funzione senza nome** e si fa con l'operatore `->`, che <u>separa parametri e corpo</u> della funzione nelle `{}` salvabile in variabili o passabile come valore:

![563](https://i.imgur.com/SuYdKIE.png)

Il valore di ritorno in una *lambda* è sempre l'espressione finale di essa (o del branch di essa che viene eseguito), <u>senza</u> `return`:

![297](https://i.imgur.com/XMgLK10.png)

###### Funzioni anonime

Le funzioni anonime differiscono dalle lambda solo per l'uso delle keyword `fun` e `return`, ma del resto sono sostanzialmente identiche:

![335](https://i.imgur.com/vXh1YfB.png)

##### Higher order functions

Queste sono semplicemente funzioni che ne ricevono altre come parametri (delle lambda parametri se ne definiscono solo i tipi come segue):

![425](https://i.imgur.com/R0dIxcW.png)

Nell'immagine sopra viene usata una ***trailing lambda***, ovvero viene <u>definita la funzione parametro subito fuori dalla chiamata del metodo</u>, ma può anche essere chiamata all'interno di essa:

```kotlin
// Identiche
val result = calcola(1,2) {x, y -> x + y}
val result = calcola(1,2, {x, y -> x + y})
```

Se invece è già definito un metodo i cui <u>parametri corrispondono a quelli della funzione parametro</u>, allora è possibile invocarla nella chiamata con l'operatore `::`:

![546](https://i.imgur.com/sUrY3LY.png)

> [!info] Nota
> La *trailing lambda* si usa <u>solo</u> per l'ultima funzione parametro del metodo.
> In caso di <u>+ funzioni parametro</u>, le altre vanno definite <u>dentro</u> le `()` di chiamata del metodo:
> ![](https://i.imgur.com/zECPgKE.png)

##### Operator overloading

Se si vogliono usare degli operatori tipo `+` tra classi complesse, al loro interno è possibile eseguire l'*overload* del comportamento dell'operatore `+` con la keyword `operator`:

![600](https://i.imgur.com/fZQx86H.png)

PAGINA 144 mobile.pdf

---

Prossima lezione: [[]]

