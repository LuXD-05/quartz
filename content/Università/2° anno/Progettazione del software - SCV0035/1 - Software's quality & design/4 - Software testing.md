# Lezione 4

## Testing

È necessario verificare la correttezza dei software ed essa non è mai determinabile a prescindere, perciò si fanno 2 cose:

- ***Analysis*** (statica): si analizza il codice senza eseguirlo (**pessimistico** siccome è meglio segnalare qualsiasi cosa assumendo che sia un difetto),
- ***Testing*** (dinamico): si prova il software con degli input di test (**ottimistico** in quanto, se i test passano, si assume che il software è corretto).

> [!info] Perché si fanno?
> La combinazione di *analysis* e *testing* è fondamentale per ridurre il rischio di errori e scovare bug sia prima che dopo l'esecuzione, ciò denota la loro complementarità.

###### Termini

- ***Test data*** (input): generalmente semplice da generare, anche in automatico.
- ***Test case*** (input + output): più complesso da ottenere (come predire l'output finale del software).

###### Stakeholder, impatti e proprietà

![](https://i.imgur.com/2Dqjf8Z.png)

> [!important] TDD
> Alla fine il testing viene interpretato non come un atto finale (dato che non produce risultati concretissimi), bensì come una disciplina da applicare durante lo sviluppo. Così si arriva al **TDD** (*Test Driven Development*), una pratica di sviluppo nella quale si scrivono prima i test e poi si scrive il codice (> qualità e < errori).

##### Principi

Esistono anche dei principi per un testing efficace:

- ***Sensitivity***: la <u>sensibilità</u> (o meglio <u>coerenza</u>) significa che un test è efficace <u>se segnala sempre un errore, non solo qualche volta</u> (esempio: un test del codice `double n = 1/input;` non è affidabile in quanto darà sempre corretto tranne quando l'input è 0; oppure un test che segnala errore su una macchina e non su un'altra...).
- ***Redundancy***: essere <u>ridondanti</u> durante l'analisi aiuta a scovare errori prima e meglio (usare tipi statici e non dinamici, verificare i requisiti prima del software finale...).
- ***Partitioning***: il codice da testare viene <u>partizionato</u> così da suddividere gli input per gestirli meglio (più semplice creare input per 1 procedura che per l'intero software).
- ***Restriction***: si possono gestire problemi complessi <u>restringendoli</u> grazie a dei vincoli (tipo dinamico da errore a runtime, con tipo statico da errore più specifico).
- ***Feedback***: l'<u>esperienza</u> costruita negli anni è fondamentale, siccome serve per fare delle *checklist* di problemi comuni già riscontrati in precedenza per scrivere test migliori.

##### POV aziendale

Qualche cosa da prendere in considerazione a livello di organizzazioni:

- I <u>software sono diversi</u>; per qualcuno è necessaria più affidabilità e sicurezza, mentre per altri la priorità è il *time-to-market* e il numero di *features*,
- Bisogna <u>premiare chi trova bug</u> con incentivi (altrimenti i dev tendono a <u>nascondere i problemi</u>) e <u>staccare</u> la figura del <u>tester da</u> quella del <u>dev</u> per evitare che non siano indipendenti (non troppo però, altrimenti si rischia il *throw over the wall*: dev che consegnano il lavoro ai tester e se ne sbattono di ulteriori problemi),
- È difficile avere **visibilità anticipata** così da <u>capire prima se si sta andando nella giusta direzione</u>, perciò si usano dei **KPI** (*Key Process Indicators*) come <u>testabilità</u> e <u>n° di errori</u> o bug per monitorare preventivamente il progetto.

#### Types of testing

![](https://i.imgur.com/j8dxHHF.png)

Esistono diversi tipi di testing, divisi in 2 macrocategorie:

- **Di verifica**: confermano che l'oggetto del test soddisfa tutti i suoi requisiti (logica interna corretta),
- **Di validazione**: confermano che il prodotto sia adatto al compito che deve svolgere (output corretti).

###### Unit testing

I **test di unità** vengono fatti su singoli componenti del software (unità più piccole testabili, tipo classi o metodi) e sono tutti indipendenti (generalmente fatti dai programmatori con anche il debugger).

###### Integration testing

I **test di integrazione**, per l'appunto, verificano il corretto funzionamento di tutte le interazioni tra i vari moduli/unità e la loro corretta integrazione (fatti dopo *unit testing*). Generalmente verificano dati/oggetti gestiti male o improprie chiamate o sequenze di ritorno (fatti da programmatori e tester).

###### System testing

I **test di sistema** verificano che il sistema (tutte le parti integrate insieme) funzioni correttamente (generalmente include anche test di performance, sicurezza... ed è un po più *requirement-oriented*).

###### Acceptance testing

I **test di accettazione** sono fatti specificatamente per determinare se un sistema soddisfa tutti i requisiti imposti in un ambiente simile a quello di produzione (viene fatto insieme al cliente per avere un feedback e capire se va tutto bene o se ci sono modifiche da fare).

###### Beta testing

Un software è in ***beta test*** quando è usato dal cliente in produzione per trovare ulteriori difetti da sistemare (una sorta di *acceptance testing* esterno per avere feedback).

###### Regression testing

I **test regressivi** invece sono usati per controllare il comportamento di nuove versioni del software (si usano i vecchi test sulle nuove versioni per, in caso, aggiornarli).

#### Test structure

I test sono strutturati secondo un modello detto ***given-when-then*** (ovvero <u>dati</u> dei dati, <u>quando</u> avviene una certa cosa, <u>allora/poi</u> cosa esce fuori):

![](https://i.imgur.com/N37vWMH.png)

Definiamo il modello:

- ***Given***: in questa fase un *constructor* inizializza un **SUT** (*Software Under Testing*, non necessariamente un programma intero, anche una parte di esso) al quale vengono impostati (*set property*) dei dati di mock,
- ***When***: ora viene semplicemente chiamato il metodo da testare (*call*), chiamando magari anche altri componenti dipendenti mockati (*mocked dependency*, il cui comportamento è emulato per restituire al metodo dei dati specifici),
- ***Then***: infine il metodo ha ritornato un valore (*return value*), quindi si vanno ad asserire (*assert*, verificare che combacino con gli output aspettati) il valore di ritorno, eventuali *property* dell'oggetto che sono cambiate e se le altre *dependency* sono state chiamate o no.

#### Testing process

Il processo di testing è composto da diverse attività:

![](https://i.imgur.com/t6KrzZG.png)

###### Test planning

La **pianificazione** dei test serve per identificarne l'ambito, definirne gli obiettivi e strutturare i test in modo che soddisfino i requisiti. In più con essa si determina l'approccio (tecniche, procedure, team...), le risorse necessarie, i risultati da aspettarsi e si schedulano tutte le altre fasi.

###### Test control

Il **monitoraggio** del testing è una fase continuativa che si fa per tutta la durata del testing e mira ad identificare preventivamente anomalie scaturite dai test e ad effettuare eventuali misure correttive.

###### Test analysis & design

Con **analisi** e **design** si analizza quanto pianificato fin qui e si progettano dei test tangibili basandosi su obiettivi e requisiti che essi devono soddisfare.

###### Test implementation & execution

Con l'**implementazione** si iniziano a trasformare le condizioni in *test cases* (di vario [[#Types of testing|tipo]]), per i quali vengono create *test suites* e *test data* (input), per poi verificare che l'ambiente sia stato setuppato correttamente. In seguito si passa all'**esecuzione** dei test (manualmente o con strumenti di test) per scovare incongruenze coi risultati aspettati.

###### Result evaluation

Si vanno poi a **valutare** i log dei test e i criteri d'uscita specificati nel [[#Test planning|planning]] e si decide se servono altri test o se considerare il sistema testato.

###### Test closure

Con la **chiusura** si va ad archiviare tutto il materiale di testing utilizzato per uso futuro e si analizza quanto imparato per il futuro.

### Problemi

Ci sono dei problemi fondamentali con il testing di software:

##### Scaffolding

Per l'esecuzione di test è necessario un ambiente simile a quello reale, tuttavia è complesso da setuppare (con strumenti tipo *docker* o *JUnit*).

##### Oracles

Come capire se un test è passato o fallito? A questo ci pensano gli ***oracles***, meccanismi che controllano i risultati dei test. Il problema è che è complesso progettare un *oracle*, lo è ancora di più automatizzarli per software grandi e per creare ognuno si usano tecniche diverse.

##### Test case generation

La generazione di *test case* è altamente complessa, dal trovare le specifiche al generare i dati di input:

![](https://i.imgur.com/GRqjgGH.png)

Per fare ciò si dividono i programmi in **classi di equivalenza** da testare (insiemi di codice con caratteristiche simili) e lo si fa secondo certi criteri:

###### Criterio black box

Il criterio ***black box*** (*functional*) si basa interamente sulle <u>specifiche</u>, ovvero si divide in classi in base alla <u>funzione generale di un modulo</u> (esempio: moduli di interazione col db, moduli che eseguono richieste API, moduli di interazione col front-end...). Questo metodo è adatto per <u>test funzionali</u> (di cui non è necessario sapere cosa fa il codice ma interessano solo gli output), però non permette di notare eventuali difetti all'interno del codice.

![](https://i.imgur.com/4SRWmOk.png)

###### Criterio white box

Il criterio ***white box*** (*structural*) al contrario, <u>analizza il codice direttamente</u> e permette di dividere in classi basandosi sulla <u>funzione specifica di metodi e classi</u> (esempio: metodo che legge un file, metodo che processa i dati ottenuti dal file...). Questo criterio è più adatto per <u>test di unità</u>, ma non è ottimo per testare la correttezza delle funzionalità del sistema in quanto non scala molto bene in sistemi grandi.

![](https://i.imgur.com/DeWOQV1.png)

###### Criteri random e fault-based

Criterio ***random*** divide in classi casuali o a scelta dei tester, mentre il ***fault-based*** raggruppa le classi in base a <u>bug comuni possibili</u> nel codice (divisione per 0, overflow, index out of bounds...) e mira a <u>far emergere tali bug</u>.

##### Termination

(Problema principle per i manager) quando fermare il testing? C'è qualche strategia:

- Quando finiscono le risorse disponibili (tempo e budget): non si hanno informazioni sull'efficacia del test ma almeno i *constraint* sono rispettati,
- Quando si ha raggiunto un certo punto: non è assicurata la qualità del software ma è un criterio ragionevole.

###### Misure

- **Troppo testing**: si sprecano risorse, aumentano i costi e anche *deadlines* e *time-to-market*,
- **Poco testing**: rischio di permanenza di difetti, insoddisfazione del cliente, alti costi di riparazione e supporto *post-deploy*.

### Altro

##### Faults & improvement

Costruendo software si incorrerà <u>sempre</u> in errori e *fault*, perciò è buona cosa creare un sistema che permetta di analizzarli, scoprirne le cause ed usarli per migliorare i processi cosicché tali errori vengano prevenuti o scovati subito.

Per ogni *fault* è fondamentale <u>categorizzarlo in base al tipo</u>, capire <u>a che fase dello sviluppo emerge</u> più spesso, capire <u>perché occorre</u> e infine <u>come prevenirlo</u>. Da ciò possono essere create delle misure di prevenzione, tipo: starci attenti prima, modificare parte del codice soggetto a tale *fault* o riscrivere quella parte interamente (tra queste si sceglie con in mente la ***cost-effectiveness*** e non la perfezione).

##### Fatti

- Un test che ha successo è uno che causa un *failure* (o trova un errore),
- Testers e devs devono lavorare insieme per trovare e fixare (rispettivamente) più difetti possibili,
- (Generalmente) non è fattibile <u>testare tutto</u> e uno dovrebbe basare i test su: obiettivi, priorità, costi e rischi,
- Il *testing* <u>mostra che ci sono dei difetti</u> (non può mostrare che non ce ne sono),
- Il *testing* non prova che un software è corretto ma ne aumenta l'affidabilità (< rischio di difetti),
- Fare test il prima possibile (in quanto più tardi il costo sale esponenzialmente),
- Pochi moduli hanno tanti difetti e la > parte del *downtime* è causata da una piccola parte di tutti i difetti,
- Un software potrebbe fare cose non richieste (***fault of commission***) ma potrebbe anche non fare cose richieste (***fault of omission***) e i test sono fondamentali per determinare evitare questi *faults*.

##### Indipendenza

Ci sono diversi livelli di indipendenza in chi testa il software (crescente):

- *Dev testing*: chi scrive il codice lo testa,
- *Pair testing*: il codice è testato anche da un altro membro del team,
- *Test team*: un team apposito per il testing testa il codice,
- *External testing*: il testing è fatto da un gruppo esterno all'organizzazione (***outsourcing***).

###### I dev dovrebbero testare il loro codice?

![](https://i.imgur.com/fKWt8sy.png)

### Unit testing

Lo *unit testing* è attuabile con varie tecniche, 2 delle quali sono:

##### Specification-based testing

Questo tipo di *unit testing* <u>si basa</u> interamente <u>sulle specifiche del software fornite</u>, le quali possono essere:

- **Formali**: si possono automatizzare i test (tipo: automi a stati finiti, logiche o algebra),
- **Semi-formali**: test parzialmente automatizzabili ma è semplice derivare le partizioni di input o classi di equivalenza (esempi: UML, flow-chart...),
- **Informali**: test non automatizzabili, è richiesta una struttura o linee guida per agire così da coprire bene i casi (specifiche dette a parole).

###### Criteri di copertura

Con ***copertura*** si intende la percentuale di codice effettivamente testata; ed essa è calcolabile secondo diversi criteri:

- ***Statement coverage***: con dei dati in input fissati <u>si esegue ogni istruzione almeno 1 volta</u> (non puoi trovare un *fault* se non esegui l'istruzione), però con 1 solo gruppo di input non si riuscirebbe a gestire ogni caso.
- ***Basic block coverage***: si testano interi blocchi di codice.
- ***Branch coverage***: (*decision*) un ***branch*** è un <u>possibile percorso di esecuzione determinato in base a una decisione nel codice</u>, quindi si esegue ogni *branch* almeno 1 volta (non puoi trovare un *fault* se la decisione che lo provoca non è scelta); uno svantaggio però è la ***short-circuit evaluation*** che potrebbe non far coprire certe cose (esempio: `if(cond1 && (cond2 || func()))`, `func()` potrebbe non essere mai eseguita),
- ***Condition coverage***: simile alla precedente ma implica che ogni condizione deve essere eseguita (sia `false` che `true`) almeno una volta; il problema è che è molto tedioso e costoso come criterio in quanto si hanno max $2^{n}$ casi di test con $n$ condizioni:

  ![](https://i.imgur.com/TQ37r91.png)

- ***Modified condition/decision coverage***: 
- ***Path coverage***: un ***path*** è un insieme di *branch* e questo criterio richiede che ogni *path* abbia almeno 1 *test case*; il problema diventano i cicli (*paths* e *test cases* indefiniti), quindi in quel caso o si skippa il loop, o se ne fanno 1 o tutte le iterazioni; poi anche le condizioni `if/else` complicano tutto perché ognuna determina un path diverso.
- ***Data flow coverage***: (o *def-use*) testa solo i paths determinati dalla definizione all'uso di ogni variabile (si basa sugli effetti di essa e non fa tutti i cicli).
- ***Method coverage***: qui ogni unità è una classe, della quale se ne testano i metodi.

> [!error] Problemi pratici
> - ***Budget coverage criterion***: i test finiscono quando finiscono soldi o tempo (avere il 100% di *coverage* è troppo costoso, quindi di solito ci si accontenta dell'80%).
> - ***Inflessibilità***: non tutti i *data flow* o *paths* sono eseguibili e quindi testabili, perciò o si giustificano omissioni o si splittano le percentuali (95% *statement coverage* e 80% *data flow coverage*).

##### Fault-based testing

Il *fault-based testing* invece <u>identifica</u> certe <u>porzioni di codice</u> nelle quali c'è <u>rischio di un certo</u> *fault* e ve <u>ne inserisce uno </u>**finto**<u> al fine di generare dei </u>*test cases* adeguati <u>per quel fault basandosi su quello finto</u> impiantato dai tester stessi.

Il metodo è molto efficace per il testing a livello di **hardware** (ci sono tanti modelli di *fault* ed errori noti) rispetto che a livello di software (dove più errori sono derivati da design e disattenzioni dei dev); tuttavia è <u>inutile</u> per *fault* al design interno dei componenti (esempio: [Pentium bug](https://it.wikipedia.org/wiki/Pentium_FDIV_bug)).

###### Mutation testing

Un esempio di *fault-based testing* si basa sulla ***mutation***, ovvero vengono creati programmi alternativi (***mutants***) generati modificando sintatticamente il software originale così da venir anch'essi testati. La qualità di un software testato con *mutation testing* è asserita dal numero di *mutants* all'interno del *test set*.

Esempi di *mutation* possono essere: cambiare numeri (uno 0 diventa 1), cambiare `true` in `false`, rendere condizioni sempre vere o sempre false (ci si aspetta che la *suite* di test uccida i *mutants*, altrimenti non è buona).

#### Infrastruttura

Alla fine, è importante setuppare l'infrastruttura e l'ambiente per l'esecuzione del test:

![](https://i.imgur.com/wqde4GF.png)

Essa può essere specifica per 1 o più test ma anche generica per qualsiasi test. Oltre all'*oracle*, in essa ci sono:

- ***Driver***: è il chiamante di un metodo da testare (volendo testare il metodo `paga()`, bisogna creare un driver che la chiama ed esegue il test, tipo `main()`),
- ***Stub***: simula <u>semplicemente</u> un componente richiamato all'interno del test (`paga()` usa una funzione per lo sconto, che come *stub* è: `calcolaSconto() { return 0; }`),
- ***Mock***: è uno *stub* sofisticato con dati generati (avendo `paga(mock.carta)`, si ha un oggetto `carta` da una classe `mock` che ne inizializza delle proprietà finte, tipo template).

###### Problemi

![](https://i.imgur.com/3WWJ6QA.png)

---

Prossima lezione: [[5 - Software analysis]]

