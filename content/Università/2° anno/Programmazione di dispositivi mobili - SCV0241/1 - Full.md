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

![](https://i.imgur.com/5XpHgor.png)

> [!info] Manifest
> Negli APK c'è il file `AndroidManifest.xml` che contiene: il nome del package java, i componenti che ne fanno parte (activities, services...), permessi...

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

#### Programmazione funzionale

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

### Android

Le app android cono composte dalla UI (activities, views, intents...) e da logica e dati (services, content providers, broadcast receivers); quelle moderne fanno uso di `ViewModel` (invece di activities), `WorkManager` (invece di services) e `Room` (al posto di SQLiteDatabase) per semplificazione e ottimizzazione.

###### ART

ART (*Android RunTime*) è come il java runtime ma runna i file `.dex` degli apk sui dispositivi android eseguendoli più velocemente (però richiede + tempo di installazione e storage):

![473](https://i.imgur.com/HIr953a.png)

#### Componenti

##### Activity

Una ***activity*** è una singola schermata della UI e gestisce il *lifecycle* dell'app. Queste vengono distrutte e ricreate (<u>perdendo il proprio stato</u>) da android in certe situazioni: 1) ruotando lo schermo, 2) cambiando lingua/configurazione del dispositivo e 3) premendo i tasti `back` o `home`.

> [!info] ViewModel
> Un ***ViewModel*** è un componente proprio del pattern MVVM e permette di conservare i dati della UI separandoli dalla activity, facendo in modo che sopravvivano attraverso le distruzioni e le ricostruzioni della UI performate da android:
> ![](https://i.imgur.com/HzJ4WKG.png)

###### Fragment

I ***fragment*** sono <u>porzioni</u> di UI in un'*activity* ma sono gestiti in modo diverso e sono fondamentali per la gestione dell'interfaccia, modularizzandola e permettendo un miglior controllo della navigazione oltre che al supporto di layout complessi dispositivi di dimensioni diverse (per esempio, UI diverse tra telefoni e tablet):

![632](https://i.imgur.com/T61ZCoJ.png)

L'ART rileva le dimensioni dello schermo (pixel) e permette l'aggiunta di altre view per supportare diversi layout:

![282](https://i.imgur.com/DVdoHlP.png)

##### Service

Un ***service*** è un processo che viene eseguito in background senza una UI usato per eseguire compiti particolari o lunghi che potrebbero dare problemi alla UI (tipo per query su database, ascoltare musica, operazioni I/O, che se fatte sul *main thread* potrebbero bloccare l'app).

###### WorkManager

Ora invece dei *services* Google raccomanda l'uso di ***WorkManager***, che permette di eseguire operazioni in background che vanno completate in modo <u>affidabile</u> (quindi anche se l'app viene chiusa, il dispositivo viene riavviato o il sistema decide di posticiparne l'esecuzione per motivi di batteria o rete):

![315](https://i.imgur.com/7JzIAfX.png)

##### Content provider

Un ***content provider*** è un componente che gestisce l'accesso a un set condiviso di dati, mettendo a disposizione delle operazioni CRUD (`query()`, `insert()`, `update()`, `delete()`) per permettere a varie app di interagirvi:

![](https://i.imgur.com/oMN22LX.png)

Un esempio è la **rubrica**, un *content provider* di sistema attraverso la quale le app possono gestire i <u>contatti</u>.

##### Broadcast receiver

Un ***broadcast receiver*** è un componente che permette ad un'app di ascoltare <u>eventi di sistema</u> (lanciati in broadcast a tutti i *receivers*). Esempio:

```kotlin
class BatteryReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        if (intent.action == Intent.ACTION_POWER_CONNECTED)
            println("Il telefono è in carica!")
    }
}
```

#### Stacks

##### Backstack

Il ***backstack*** è una <u>pila</u> navigabile in cui sono salvate le activities di una app. Quando si apre una nuova activity essa viene aggiunta al backstack e rimossa quando si esce da tale schermata.

##### Task stack

Una ***task*** è una **sequenza di activities** (anche di app diverse) aperte cronologicamente per fare qualcosa. Ogni task contiene quindi un backstack di activities di una (o più) app e sono salvate nel ***task stack*** (accessibile dal quadratino della bottom bar o con swipe verso l'alto).

### Activities

Una app android richiede almeno 1 *activity*, un file di *layout* e un *manifest*. Le *activities* possono essere lanciate in 2 modi:

\- All'avvio dell'app: se una activity è contrassegnata come `launchable` nel manifest,

\- `Intent`: da un'*activity* si crea un ***intent*** che permette il passaggio ad un'altra *activity*.

```xml
<!-- Launchable (nel manifest) -->
<application ...>
    <activity 
        android:name=".MainActivity"
        android:exported="true">
        <intent-filter>
	        <!-- Indica che è l'entry point -->
            <action android:name="android.intent.action.MAIN" />
            <!-- Indica di creare l'icona dell'app nella home -->
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>
```

```kotlin
// Intent
fun newIntent() {
	// Crea l'intent
	val intent = Intent(this, ExampleActivity::class.java)
	// Avvia l'activity
	startActivity(intent)
}
```

#### Intents

Gli ***intent*** sono degli "oggetti" che android usa per far comunicare i [[#Componenti|componenti]] di 1 (o più) app fra loro; e contengono l'azione richiesta + eventuali dati. Ne esistono di 2 tipi:

###### Espliciti

Gli intent espliciti indicano al sistema il nome esatto del componente da aprire e sono usati principalmente per navigare tra le activity:

```kotlin
val intent = Intent(this, ExampleActivity::class.java)
intent.putExtra("id", 1) // aggiunta di dati extra da passare all'intent
startActivity(intent)
```

###### Impliciti

Gli intent impliciti invece specificano la propria azione e il target di tale intent:

```kotlin
// Esempio mostra pagina web
val intent = Intent(Intent.ACTION_VIEW, Uri.parse("http://www.sito.it"))
startActivity(intent)
```

---

Prossima lezione: [[]]

