# Lezione 12

## Class diagrams

I ***class diagrams*** definiscono una visione statica del sistema descrivendone le **classi** e le **relazioni** tra esse.

##### Classe

Negli **UML** una classe è composta da 3 parti: un <u>nome</u>, gli <u>attributi</u> (lo stato) e i <u>metodi</u> (il comportamento):

![](https://i.imgur.com/k3PQxdU.png)

###### Rappresentazione

Negli UML le classi si rappresentano attraverso dei rettangoli con 3 spazi separati per nome, attributi e metodi (col nome si indica anche la molteplicità). Gli <u>attributi</u> sono scritti con il formato `[modif.] nome: tipo [= ?]` (modificatore e valore di default eventuali), mentre i <u>metodi</u> solamente `[modif.] nome([args])` (tra classi diverse si usano gli stessi `nome` e `args` solo tra metodi che fanno logicamente la stessa cosa, altrimenti è meglio non riutilizzare gli stessi nomi per operazioni di natura diversa).

I tipi utilizzabili sono gli stessi di SQL e i modificatori disponibili sono generalmente quelli del linguaggio nel quale si andrà a codificare la soluzione:

![](https://i.imgur.com/xvzyU8J.png)

> [!important] Attributi
> Gli attributi delle classi devono essere precisi e coerenti (per una classe `Studente` vanno bene `nome, cognome`, ma non ha tanto senso `corsiScelti`); e in più non devono avere **identità**, dato che nei *class diagrams* non è necessario aggiungere tali attributi in quanto gli oggetti stessi hanno una loro identità (quindi no attributi `id`).
> In caso servano, è possibile indicare **attributi calcolati** (<u>non memorizzati</u>) nella classe (per esempio `età` che sarebbe `{oggi - dataNascita}` in anni) così:
> ![](https://i.imgur.com/9PZAzPG.png)

###### Implementazione

Ovviamente c'è una corrispondenza tra l'UML di una classe e l'implementazione con un linguaggio:

![](https://i.imgur.com/yw780aF.png)

### Associazioni

Un'associazione (<u>binaria</u>) definisce una connessione logica tra 2 classi e le sue istanze si dicono ***link*** (associazione connette classi, *link* connette oggetti). Ogni associazione necessita di un <u>verso di lettura</u> ed (eventualmente) di un'<u>etichetta</u> che la definisce (solitamente un verbo):

![](https://i.imgur.com/lMyRliU.png)

> [!info] Associazioni n-arie
> Generalmente non si definiscono relazioni *n-arie* (tra più di 2 classi) in quanto andrebbero trasformate ulteriormente quando si traduce in codice ed anche perché la maggior parte degli strumenti non le supporta; perciò si introduce una classe che rappresenta la relazione (non so perché non vada bene l'altro esempio nella foto):
> ![](https://i.imgur.com/eK6S5MC.png)

###### Ruolo

Le classi possono partecipare ad un'associazione anche indicandone un **ruolo** specifico, che è raccomandato (e a volte obbligatorio) in associazioni multiple tra 2 classi e auto-associazioni: 

![](https://i.imgur.com/EQOW5Kl.png)

###### Altri tipi di associazione

![](https://i.imgur.com/iA5mrb5.png)

##### Molteplicità

La **molteplicità** viene usata per definire il <u>numero minimo e massimo di oggetti relazionabili ad un'altro</u> e di conseguenza <u>indicare se l'associazione è obbligatoria o meno</u> (può non essere specificata in 1 o entrambi gli estremi):

![](https://i.imgur.com/VrmMQEZ.png)

(In questo esempio specifico significa che ogni studente può seguire da 0 a $\infty$ corsi, mentre ogni corso può essere seguito da minimo 3 e max 10 studenti). Altri esempi:

![](https://i.imgur.com/8SYEPqI.png)

La molteplicità (e altre caratteristiche delle classi) sono anche rappresentabili testualmente nel grafico (vedi `unique` e `ordered` nel seguente):

![](https://i.imgur.com/j3d7saE.png)

###### Navigabilità

Il seguente diagramma indica che 1 persona può possedere un qualsiasi n° di auto, tuttavia non fornisce informazioni sul n° di proprietari di una singola auto:

![](https://i.imgur.com/vykyFAj.png)

Perciò si introduce la **navigabilità** di un'associazione, che indica quale delle classi associate può "navigare" all'altra, ovvero <u>da quale è accessibile l'altra</u>:

![](https://i.imgur.com/GXJnQtl.png)

Implementando ciò in codice, si avrebbe che nella classe di persona ci sarebbe una lista di auto; perciò il discorso è simile a:

![](https://i.imgur.com/dUicY5r.png)

##### Attributi di associazione

A volte anche le associazioni (sia binarie che *n*-arie) possono contenere attributi, e ciò si indica con un'ulteriore classe collegata con linea tratteggiata all'associazione:

![](https://i.imgur.com/KkjD7nD.png)

In associazioni `1-N` o `N-N` tali attributi si possono <u>implementare come attributi di classe</u> (di quella a "`N`"), ma questo è preferibile a livello di codice e non nel diagramma.

##### Vincoli

Come per gli attributi derivati, è possibile imporre dei **vincoli** (su attributi e associazioni) scrivendoli sempre tra parentesi graffe (a margine della classe o dell'associazione):

![](https://i.imgur.com/Xmp8hup.png)

Per le associazioni **singole**, i vincoli permettono anche di fissare l'ordinamento dal lato "`N`" di un'associazione: 

![](https://i.imgur.com/f0lWKdj.png)

Mentre per quelle **multiple**, si può condizionare un'associazione rispetto ad un'altra:

![](https://i.imgur.com/42cEvfa.png)

###### Vincoli relativi

Alcuni vincoli "implementativi" possono essere espressi come commenti:

![](https://i.imgur.com/LKHkKpk.png)

#### Modalità di associazione

Ci sono varie modalità di associazione tra classi:

##### Aggregazione

Un'aggregazione indica che una classe "aggrega" un certo numero (definito dalla molteplicità) di istanze di un'altra classe, delineabile con un *rombo vuoto* (che si legge come: "è un insieme di") o anche testualmente scrivendo "aggrega":

![](https://i.imgur.com/KTZbAwr.png)

> [!important] Proprietà
> **Transitiva**: se una classe `PC` contiene una `UnitaBase` e questa contiene `CPU`, allora `PC` contiene `CPU`.
> **Asimmetria**: se una classe `PC` contiene una `UnitaBase`, ciò non implica che una `UnitaBase` contenga il `PC`.

###### Composizione

Una composizione è un tipo di aggregazione "forte" nel senso che le <u>classi componenti esistono solo all'interno di quella contenitore</u> (e non da sole); e ciò si indica con un *rombo pieno*:

![](https://i.imgur.com/4CD64RU.png)

Questa è particolare in quanto da parte del contenitore la molteplicità non può essere > 1, mentre può essere qualsiasi per i componenti.

> [!important] Propagazione degli effetti
> La composizione inoltre implica che <u>gli effetti sul contenitore si propagano ai componenti</u>, per esempio: se copio un `Documento` che contiene vari `Capitolo`, devo copiare anche tutte le classi `Capitolo`, mentre se distruggo un `Documento`, dovrò distruggere anche tutti le sue classi `Capitolo`.

###### Aggregazione vs composizione

Dal seguente esempio, un'istanza di `Ruota` non può essere la stessa di `Auto` e `Moto`, e se si cancella un'auto se ne cancellano tutte le ruote; mentre un'istanza di `Stile` può essere condivisa tra le 2 e non viene eliminato alla cancellazione di un'`Auto` o di una `Moto`.

![](https://i.imgur.com/oZPqbre.png)

![](https://i.imgur.com/AUEBBQ1.png)

###### Associazione riflessiva

Un'associazione è **riflessiva** (detta anche ***auto-associazione***) se mette in relazione oggetti multipli della stessa classe:

![](https://i.imgur.com/2uKWRvN.png)

##### Ereditarietà

Un'associazione di ereditarietà è praticamente identica alla **generalizzazione** tra classi nei linguaggi di programmazione, dove le <u>sottoclassi ereditano le caratteristiche della classe base con la possibilità di aggiungere nuove proprietà o ridefinirne i comportamenti</u> (stessa cosa si ha con classi astratte come basi).

![](https://i.imgur.com/sIleA5a.png)

> [!warning] Delegation
> Supponiamo di voler definire la classe `Stack` e di voler utilizzare `Sequence` come base, qui l'ereditarietà non va bene in quanto poi `Stack` potrebbe inserire elementi dovunque nella lista, quindi ha più senso fare una **delega**, ovvero usare `Sequence` all'interno della parte privata di `Stack` come se fosse in [[#Composizione|composizione]]:
> ![](https://i.imgur.com/FRiIjs0.png)

###### Ereditarietà multipla

In linguaggi come Java è possibile far ereditare una classe da più classi, tuttavia ciò porta a vari problemi:

- **Ridondanza**: sprechi di memoria causati da campi o legami duplicati,
- **Contraddizione**: si rischia di avere varianti diverse di stesse operazioni/attributi/associazioni.
- Altro tra cui *multiple inheritance* accidentale...

> [!info] Soluzioni
> Oltre che non usare ereditarietà multipla (difficile implementazione in linguaggi che non la supportano), ci sono alcune soluzioni:
> - Semplificare il modello,
> - Usare classificazione nidificata (?),
> - Limitare l'ereditarietà di certi attributi o metodi,
> - Usare la delega invece di ereditarietà.

#### Interfacce

Un'interfaccia è simile a una classe ma con restrizioni: tutte le <u>operazioni sono pubbliche e astratte</u> (non hanno *default*) e <u>tutti i dati sono costanti</u>; però una classe <u>può sempre implementare più interfacce</u>. Può indicare l'insieme minimo di "servizi" offerti o richiesti e ce ne sono di 2 tipi:

- **Fornita**: una classe espone l'interfaccia (con le proprie operazioni) per farla usare ad altre,
- **Richiesta**: una classe richiede l'interfaccia per usufruire delle operazioni che dichiara per svolgere certi compiti.

###### Interfacce nei *class diagrams*

Per esempio una classe `ProximitySensor` fornisce un'interfaccia `ISensor` che è poi richiesta dalla classe `TheftAlarm`:

![](https://i.imgur.com/ZeS4Jzh.png)

#### Altro

##### Classi parametriche

Una **classe parametrica** (o ***template***) fa uso di parametri di tipo generico per definire una "famiglia di classi" che si ottengono istanziando tali parametri. Le classi istanziate si dicono ***bound class*** e sono legate alla classe parametrica tramite una relazione di *binding* indicata con `<<bind>>`:

![](https://i.imgur.com/tPCTYZf.png)

Si possono anche creare ***anonymous bound classes*** indicando i parametri direttamente nella classe e a quel punto la relazione di binding è implicita:

![](https://i.imgur.com/gAyYc3I.png)

##### Altre entità

###### Classi utility

Le **classi *utility*** sono delle semplici classi che hanno <u>tutti i metodi statici e sono usate senza istanziarle</u> per varie operazioni "di servizio", per esempio la libreria `Math`.

###### Enum

Gli enum definiscono semplicemente un elenco di valori.

###### Stereotipi

Gli stereotipi sono usati per estendere la notazione UML per consentire all'utente di inserire nomi o relazioni personalizzate e si indicano con `<<stereotipo>>`; come esempio vediamo i seguenti (apparsi anche prima):

- `<<entity>>`: classe <u>passiva</u> (da essa non nascono mai interazioni) usato solo per <u>rappresentare i dati</u> (*model*)

  ![](https://i.imgur.com/0YxPj2w.png),

- `<<boundary>>`: classi di interfaccia verso l'esterno del sistema (*view*)

  ![](https://i.imgur.com/4AuSyh5.png),

- `<<control>>`: classe che controlla le interazioni tra `entity` e `boundary` (*controller*)

  ![](https://i.imgur.com/AQWBIQD.png).

> [!important] Dipendenza
> UML con certi stereotipi permette anche di assegnare relazioni di dipendenza tra classi, per cui modifiche sugli elementi indipendenti hanno effetto anche su quelli che da loro dipendono; alcuni esempi sono: `<<instantiates>>`, `<<calls>>`, `<<friend>>` e `<<usage>>`.
> Un altro esempio è l'annidamento che si rappresenta così:
> ![](https://i.imgur.com/tV55xiW.png)

#### Object diagram

Un object diagram descrive gli oggetti (istanze) al posto delle classi e i link al posto delle associazioni; adatto per esempi o situazioni specifiche siccome permette di fare una sorta di "snapshot" delle istanze esistenti in un certo istante di tempo.

##### Componenti

Gli oggetti sono caratterizzati da: nome, classe di cui è istanza e valore degli attributi:

![](https://i.imgur.com/blKLEqg.png)

I link invece sono rappresentati tanti collegamenti tra 2 oggetti quanti ne indica la molteplicità (specificando il tipo di link):

![](https://i.imgur.com/BHCZDeS.png)

---

Prossima lezione: [[13 - Package diagrams]]

