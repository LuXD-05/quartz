# Lezione 10

### Use-Case diagrams

L'analisi dei requisiti per lo sviluppo di un sistema viene affiancata dalla rappresentazione di "scenari tipici" per capire tali requisiti (entrambi in maniera informale); è stato poi formalizzato l'uso di tali scenari con gli ***use-case diagrams***, diagrammi che definiscono il comportamento e le funzionalità del sistema descrivendone anche l'ambiente e le sue relazioni con esso.

> [!example] Esempi
> Di seguito 2 esempi il 1° di un sistema di gestione vendite di prodotti aziendali e il 2° di un'università:
> ![](https://i.imgur.com/6XUOggt.png)

#### Use case

Uno ***use case*** rappresenta <u>una funzione</u> ("identificabile" e) <u>attuabile dall'utente</u> e un <u>suo obiettivo atomico specifico</u> e serve per <u>mostrare un'interazione che l'utente compie col sistema</u> (può avere diverse "dimensioni" e diversi livelli di dettaglio). Nei casi più semplici, gli *use cases* sono identificati discutendo col cliente l'uso che vuole fare del sistema.

![](https://i.imgur.com/1UJiuGj.png)

> [!info] Caratteristiche
> Ogni *use case* è:
> - **Etichettato ed identificato con una frase**: per esempio "acquisire dati personali" (più consigliato rispetto ad "acquisizione dati personali"),
> - **Descritto graficamente**: così da evidenziare le relazioni con altri utenti e *use case*,
> - **Descritto testualmente**: integrando testo alla grafica in quanto è estremamente scarna.

###### Documentazione

Per ogni *use case* è possibile specificare: un titolo, autori, una descrizione, requisiti, [[#Attori|attori]], vincoli (pre/post-condizioni o vincoli intermedi), [[#Scenari|scenari]], (inizio, sviluppo e fine)...

##### Attori

Ogni *use case* ha connessioni con 1 o più **attori**: entità esterne al sistema (in generale utenti) che interagiscono col sistema (forniscono input o ricevono output) assumendo un certo ruolo (anche generalizzabile o specializzabile).

![](https://i.imgur.com/pcCqNcI.png)

> [!important] Nota
> - Un <u>attore non è sempre un utente</u>, anzi potrebbe essere un <u>sistema esterno</u> (nonostante l'icona), basta che <u>interagisca col sistema o riceva risultati</u> da esso.
> - <u>Più attori possono avere lo stesso ruolo</u> e <u>1 attore può avere più ruoli</u>,
> - Più <u>attori possono esercitare lo stesso use case</u> e <u>1 attore può esercitare diversi use case</u>.

###### Selezione attori

Spesso è più facile identificare gli eventuali attori piuttosto che gli *use case* direttamente, anche perché avendo gli attori si può pensare quali interazioni facciano col sistema quindi usandoli per trovare gli *use cases* (stessa cosa se l'attore è un evento esterno che suscita una reazione rilevante nel sistema; tale reazione sarà lo *use case*).

(Quando però gli attori sono sistemi esterni non è sempre facile capire quando vadano considerati, perciò tenere da conto interazioni esterne, iniziatori di interazioni...).

##### Relazioni

Esistono 3 tipi di relazione tra gli *use cases*:

###### Generalizzazione

Con questa si ha uno *use case* **figlio** che, oltre a <u>ereditare le caratteristiche del padre</u> ed essere coinvolto in tutte le sue relazioni, può <u>ridefinirne nuovi scenari</u>.

Esempio, un pagamento può essere fatto con carta o con contanti:

![](https://i.imgur.com/Tc8PLbK.png)

Si indicano con una <u>freccia piena</u>.

> [!important] Ereditarietà
> Ogni *use case* può:
> - **Ereditare** da altri $n$ *use cases*,
> - **Essere il padre** di $n$ *use cases*.

###### Inclusione

La relazione di **inclusione** si ha quando uno *use case* è come una "*subroutine*" di un altro, ovvero quando lo *use case* incluso è una **parte di comportamento obbligatorio** (<u>che è sempre fatta</u>) **di quelli in cui è incluso** e/o quando più *use case* ripetono la stessa funzione (usato per <u>scomporre use case o per non ripeterli troppe volte</u>).

Esempio, per trasferire un file o per eseguire un login remoto, i diversi servizi devono entrambi stabilire una connessione TCP/IP:

![](https://i.imgur.com/JswI5Ra.png)

Viene indicata con una <u>freccia tratteggiata</u> verso lo *use case* <u>incluso</u> con *label* "`<<include>>`".

###### Estensione

La relazione di **estensione** è simile a quella di inclusione ma <u>prepone una condizione prima del verificarsi dello use case esteso</u>; la relazione specificherà con 1 o più ***extension points*** anche le <u>condizioni</u> (anch'esse da specificare) che, se verificate, indicano che anche il comportamento opzionale dello *use case* esteso deve essere eseguito.

Esempio, con la creazione di un ordine è possibile includervi il catalogo dei prodotti:

![](https://i.imgur.com/ZgWf4vC.png)

Viene indicata con una <u>freccia tratteggiata</u> verso lo *use case* <u>base</u> con *label*: "`<<extend>>`".

> [!info] Nota
> ***Extension points*** e le *label* in cui sono specificate le condizioni sono obbligatorie (è necessario disegnarle).

###### Include vs extend

![](https://i.imgur.com/1kXXkzQ.png)

##### Scenari

Gli *use case* identificano nello specifico un "**tipo**" di comportamento del sistema; uno **scenario** invece è una singola "storia" (sequenza di azioni con condizioni) di uno *use case*, <u>ovvero descrive uno dei tanti ipotetici comportamenti di uno use case</u>. 

Ogni *use case* è caratterizzato da uno <u>scenario base</u> (sequenza tipica di eventi) e da un numero (imprecisato a priori) di **varianti**; quindi per ogni *use case* si crea un documento in cui ne si raccolgono tutti gli scenari rilevanti (gli **autori** ne effettuano le descrizioni, possibili in linguaggio informale o misto, spesso anche con altri diagrammi).

> [!example] Esempio
> Per esempio, con lo *use case* `PrelievoSoldi`, uno scenario prevede:
> - **Precondizione**: possedere un bancomat,
> - **Svolgimento**: dopo aver inserito la tessera ed inserito il PIN, il sistema riconosce il cliente il quale seleziona "prelievo" di una certa quantità di €; il sistema eroga la quantità desiderata ed infine il cliente ritira la tessera, i soldi e la ricevuta.

###### Tipi di scenari

Ogni scenario può essere di 3 tipi:

- **Normale** (base/primario): indica la <u>sequenza tipica</u> delle azioni,
- **Alternativo**: indica una <u>sequenza alternativa</u> a quella normale (ma comunque possibile),
- **Eccezionale**: casi in cui nello <u>scenario</u> sorgono <u>errori</u>.

> [!example] Esempio
> Scenari alternativi ed eccezionali dello *use case* `PrelievoSoldi` potrebbero essere:
> - **Alternativo**: ... il sistema non riconosce il PIN, invita il cliente a digitarlo di nuovo e al 3° tentativo fallito ritira la tessera.
> - **Eccezionale**: il lettore della tessera non è in grado di leggerla a causa di un malfunzionamento.

###### Istanze

Un'**istanza** di uno *use case* è un'<u>esecuzione concreta delle azioni che lo caratterizzano</u> ed esse (istanze) sono descritte dagli scenari (scenario = descrittivo, istanza = esecuzione).

> [!example] Esempio
> a

###### Composizione

Gli scenari generalmente contengono una **descrizione della sequenza di eventi dell'istanza** (come inizia, i singoli passi e come termina); sia per lo scenario <u>base</u> sia per eventuali scenari <u>alternativi o eccezionali</u>. Inoltre, è opportuno specificare pre-condizioni e post-condizioni (cosa deve essere vero prima e dopo l'esecuzione) per lo scenario.

##### Sviluppo di use-case

Il processo di sviluppo degli *use case* è **iterativo** e parte identificando comportamenti principali per poi descriverne di alternativi e più complessi; è ideale **smettere** quando non c'è più nulla di utile da aggiungere o quando si sta scendendo troppo in dettagli implementativi.

> [!info] Nota
> Gli *use case* sono adatti a specificare requisiti **funzionali** ("cosa fa il sistema", *features*), <u>NON quelli non funzionali</u> ("com'è il sistema", *behaviors*).

###### Granularità

Per gli *use case* è fondamentale la **granularità** in quanto <u>più dettagliati sono, più è chiaro cosa si deve fare</u> (se troppo grossi e poco specifici, la gestione diventa difficile); tuttavia un <u>livello di dettaglio eccessivo</u> può renderne troppo complessa la descrizione e rischia di introdurre dettagli prematuri creando confusione.

![](https://i.imgur.com/o8epEXO.png)

###### Dominio

Non è possibile scrivere degli *use case* efficaci senza aver compreso il dominio del problema (entità, ambito, requisiti, documentazione...); l'analisi del dominio è fondamentale in quanto conduce a classi concettuali, processi e regole che serviranno nei modelli successivi.

###### Altri usi

Altri usi per i diagrammi *use case* prevedono:

- **Convalida del sistema**: ogni *use case* può corrispondere ad un'unità di test che va convalidata,
- **Gestione progetto**: *use case* utili per organizzare il progetto e stimarne la complessità.

---

Prossima lezione: [[11 - Interaction diagrams]]

