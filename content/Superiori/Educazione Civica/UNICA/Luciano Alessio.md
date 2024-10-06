---
edited_seconds: 5280
modified_at: 25/04/2024 15:10:50
---
# <center>Luciano Alessio</center>
###### <center>Classe 5DI</center>
<center>ISIS J.M. Keynes, Gazzada Schianno (VA)</center>

### Introduzione

##### Cos'è PersonalTrainer?

PersonalTrainer è un'applicazione desktop parte di un progetto scolastico mirato all'approfondimento di *Windows Presentation Foundation* (WPF) e del pattern architetturale *Model-View-ViewModel* (MVVM). 
Il progetto è stato assegnato prima delle vacanze di Natale 2023 e rappresenta un percorso di apprendimento e sviluppo personale.

##### Scopo

L'obiettivo principale di PersonalTrainer è fornire agli utenti un modo semplice ed efficace per tenere traccia delle proprie attività fisiche, le quali sono state inizialmente limitate a camminata, corsa e ciclismo.

##### Funzionalità

Inizialmente pensata come un'applicazione per il tracciamento di dati di base come la data, la distanza, le calorie bruciate e il completamento dell'attività, PersonalTrainer è stata arricchita nel tempo con nuove funzionalità e miglioramenti. 
Alcune caratteristiche chiave che ho implementato comprendono:
- **Interfaccia grafica moderna e dinamica**: l'interfaccia grafica è stata progettata al fine di avere, da una parte, uno stile moderno e *user-friendly*, mentre dall'altra, un'ottima interattività per merito della sua dinamicità.
- **Autenticazione**: è stato progettata ed implementata anche una schermata iniziale che permettesse l'autenticazione e la registrazione degli utenti.
- **Visualizzazione attività**: sono poi state inserite, oltre ad una *home page* con varie informazioni utili, due pagine con due modalità diverse di visualizzazione delle attività, una presentante le attività sottoforma di elenco mentre l'altra contenente un calendario interattivo.
- **Analisi statistica**: è stata poi creata una pagina interamente atta alla rappresentazione statistica dei dati delle attività dell'utente, mediante un grafico.
- **Area personale**: infine è stata aggiunta una discreta area personale al fine di permettere all'utente di gestire i suoi dati ed eventualmente eliminarli.



### Progetto

##### Pianificazione grafica/strutturale

Inizialmente il progetto non era molto complesso e risultava composto da una finestra principale capace di contenere una finestra di registrazione/accesso, delle finestre di creazione e modifica delle informazioni e delle attività e una vista principale (Home) a sua volta in grado di contenere 3 sotto-viste, quella principale, quella per le attività in tabella e l'area personale con i dati del profilo:

![](https://i.imgur.com/UykyPnd.jpeg)

Durante lo sviluppo però, mi sono preso la libertà di effettuare delle modifiche ed ho aggiunto varie funzionalità nuove da implementare; tra cui, oltre ad una nuova organizzazione di finestre, viste e sotto-viste, anche delle viste che permettevano la visualizzazione delle attività in un calendario e delle statistiche filtrabili in base alle attività portate a termine:

![](https://i.imgur.com/ok8ALOT.jpeg)

##### Pianificazione temporale

La pianificazione della struttura grafica dell'applicazione è stata subito seguita dalla pianificazione temporale di ogni macro-componente da realizzare, in particolare:

![](https://i.imgur.com/GEtmQsC.png)

Ovviamente, per le componenti aggiunte durante lo sviluppo dell'applicazione, non è stato possibile stimare i tempi per la loro realizzazione in quanto essa è avvenuta parallelamente allo sviluppo delle altre attività.
### Grafica

##### Login/Register

Le viste di accesso e registrazione sono le prime che accolgono l'utente e prevedono, oltre al cambio tra l'una e l'altra, l'inserimento di username e password:

![](https://i.imgur.com/UPPhh0p.png)

##### Home

All'accesso (o registrazione) si viene portati sulla vista "Home", quella principale. In questa sono elencate delle statistiche in un grafico a barre, i totali, le prossime attività da fare ed in un pannello laterale, qualche informazione biografica e le attività del giorno:

![](https://i.imgur.com/Q5tvs8I.png)

##### Activities

La vista attività invece, presenta le attività in un elenco e ne permette il completamento, la modifica e la cancellazione:

![](https://i.imgur.com/YJoq4ye.png)

##### Calendar

La vista calendario permette, per l'appunto, la visualizzazione di un calendario interattivo e navigabile, che elenca le attività del giorno selezionato:

![](https://i.imgur.com/Soxi8Ez.png)

##### Stats

Poi, la vista statistiche è interamente composta da un grafico interattivo che mostra il proprio progresso graficamente nel tempo. C'è la possibilità di applicare dei filtri per poter vedere attività, distanza calorie o tutte e 3 insieme:

![](https://i.imgur.com/EWfQQFr.png)

##### Profile

Infine, la vista profilo contiene solamente 3 opzioni: una per la modifica delle credenziali, una per la modifica del profilo e un'altra per la cancellazione dei propri dati:

![](https://i.imgur.com/124KGZ6.png)



### Programmazione

##### Struttura

Il progetto si presenta in questo modo:

![](https://i.imgur.com/qiMx0wz.png)

Bisogna sottolineare che ciò è il frutto di un'attenta ottimizzazione della gestione dei vari file al fine di ordinarli il più possibile come in un progetto professionale.
A primo impatto potrebbe essere difficile capire il perché di questa organizzazione o il motivo dietro alla scelta dei nomi; ma le parti seguenti (e più interessanti) mirano a rendere chiaro tutto ciò.

##### Salvataggio dati

Per quanto riguarda il salvataggio dei dati, dato che il professore necessitava verificare le mie competenze nell'uso dei file da C#, ho deciso di non usare un database relazionale per lo *storage* ma salvare tutti i dati su un file XML.
Questo mi è stato possibile grazie alla libreria "*System.Xml.Serialization*", la quale fornisce dei metodi che permettono automaticamente di serializzare un'oggetto in un file XML. Ne ho implementati 3:
- Il primo per aggiungere un utente al file:
  ![](https://i.imgur.com/CZAFHeR.png)
- Il secondo per ottenere tutti gli utenti nel file:
  ![](https://i.imgur.com/YgDLF7U.png)
- Il terzo per aggiornare (e anche cancellare) uno o più utenti dal file:
  ![](https://i.imgur.com/cLnsPV6.png)

##### Gestione statistiche

Una parte interessante che merita di essere presentata è l'implementazione dei grafici nella vista "Home" e in quella delle "Statistiche".
In generale, per implementare un grafico con il pacchetto "*LiveCharts.Wpf*", sono necessarie 2 collezioni: una che è un oggetto "*SeriesCollection*" e contiene un certo numero di serie (insiemi di dati con valori rappresentabili sul grafico) e un'altra semplice lista di stringhe chiamata "*Labels*", che contiene semplicemente le stringhe di testo da rappresentare sull'asse x. Di seguito queste vengono legate programmaticamente al grafico:

![](https://i.imgur.com/fiyYBrB.png)

Per entrambi i grafici in "Home" e "Stats", viene usato un oggetto chiamato "*ChartObject*"; che contiene, oltre alla *SeriesCollection* e alle *Labels*, 2 metodi rispettivamente in grado di costruire il grafico della "Home" e quello delle "Stats".

###### Home chart

Per quanto riguarda il grafico nella "Home", quello ha il compito di presentare, sottoforma di grafico a barre verticali, le attività completate, i chilometri percorsi e le calorie bruciate ogni giorno della settimana corrente.
Il metodo che lo costruisce, prima inizializza le *Labels* e la *SeriesCollection* (questa contenente 3 oggetti *ColumnSeries* rappresentanti le barre verticali di: attività fatte, distanza percorsa e calorie bruciate):

![](https://i.imgur.com/68vMRoV.png)

e poi va a filtrare automaticamente i dati in modo da considerare solo quelli della settimana corrente:

![](https://i.imgur.com/QpyKcFk.png)

Il risultato finale (con attività in verde, distanza in blu e calorie in arancione) si presenta così:

![](https://i.imgur.com/LYYuaOh.png)

###### Stats chart

Il grafico delle "Stats" viene costruito in maniera simile a quello della "Home", però al suo metodo di costruzione sono passate altre 2 variabili oltre all'utente:
- "serie": una stringa che assume i valori di "All", "Activities", "Length" o "Calories" (per indicare quali statistiche si vuole visualizzare in base al filtro selezionato),
- "range": una coppia di date (una di inizio ed una di fine) secondo le quali si vuole filtrare il grafico mostrando solo le statistiche incluse in quel *range* (se posto a null, vengono prese tutte le statistiche).

Rispetto al metodo di costruzione del grafico in "Home" però, questo, prima di tutto, raggruppa le attività completate sempre per giorno (eventualmente filtrandole in base al *range*):

![](https://i.imgur.com/jm03kf9.png)

e solo dopo procede all'inizializzazione delle *Labels* e della *SeriesCollection* (nella quale ora verranno inseriti degli oggetti *LineSeries* rappresentanti le linee del grafico lineare) in base a quelle filtrate:

![](https://i.imgur.com/VkIbG1x.png)

Il risultato finale (sempre con gli stessi colori del grafico in "Home") si presenta così:

![](https://i.imgur.com/f9aJaC0.png)

##### MVVM

La parte di progetto che considero più affascinante è l'implementazione del *design pattern* MVVM e la gestione delle *view* che ne consegue in quanto è stata quella che ha richiesto più tempo ed impegno in assoluto solo per capire ed applicare un concetto.

###### Gestione delle view

Inizia tutto dalla MainWindow, la finestra principale, che è solo un contenitore invisibile per un *ViewModel*, un oggetto legato ad una *View* specifica che viene viene impostato come contesto (*DataContext*) di una finestra WPF. 

![](https://i.imgur.com/LMgI9tv.png)

In questo caso si imposta un *MainViewModel*, ma nella soluzione ho definito più tipi di ViewModel:
- Il ***BaseViewModel***: classe da cui ereditano tutti gli altri *ViewModel* contenente proprietà comuni quali un titolo, un campo di errore e le dimensioni della view,
- Il ***MainViewModel***: il *ViewModel* principale assegnato alla MainWindow; contiene il ViewModel renderizzato e l'utente loggato,
- Gli altri *ViewModel*: uno per *View*, ovvero la "Home", la "Login" e la "Register". 
Nel mio caso, la *View* iniziale è impostata a quella di "Login" ed ogni volta che vi è la necessità di cambiare *View*, si usa un *Command* che permette di ottenere dinamicamente una *View* a partire dal nome del *ViewModel* (poi verrà renderizzata):

![](https://i.imgur.com/09ZhCWK.png)

###### Gestione delle subview

La "Home" *View* a sua volta ha un contenitore che contiene delle *SubView*, che sono le schermate "Home", "Attività", "Calendario", "Statistiche" e "Profilo". Il loro funzionamento è simile a quello di *View* e *ViewModel*, però sono degli *UserControl* che hanno come contesto l'**utente** contenuto in una variabile del *MainViewModel* contesto della finestra in cui sono contenute.
Nell'*HomeViewModel* vi è un metodo che le cambia come le *View* ma qui al click di uno dei bottoni di navigazione a sinistra:

![](https://i.imgur.com/wOqMaX0.png)

Nella *SubView* invece (oltre ad eventualmente inizializzare delle variabili) si imposta il contesto all'utente del MainViewModel contesto della finestra parente:

![](https://i.imgur.com/mL5JeLg.png)



### Conclusione

In conclusione, vorrei aggiungere che sono molto orgoglioso di questo progetto in quanto mi ha aiutato ad approfondire WPF e MVVM e mi ha permesso di comprendere vari concetti che sono sicuro mi saranno utili in futuro.
Sono soddisfatto del risultato che ho ottenuto ma soprattutto della dedizione e perseveranza che io stesso ho presentato nel risolvere ogni problema che mi si è posto davanti.
Questo progetto sarà disponibile su questo [link](https://github.com/LuXD-05/PersonalTrainerWPF) di GitHub.