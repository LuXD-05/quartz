# Lezione 2

### Modello object-oriented

Nato per rappresentare realtà gerarchiche, di modelli *object-oriented* ne esistono diversi, ma le caratteristiche comuni di essi sono:

- I dati sono <u>istanze di classi</u> (**oggetti**) ovvero <u>non</u> sono contenuti nelle <u>relazioni</u> ed hanno un **OID** (*Object Identifier*) uno **stato** (dati) e un **comportamento** (metodi).
- **Persistenza**: meccanismi che garantiscono l'esistenza dei dati indipendentemente dalle app che li usano (nei DBMS object-oriented serve che la persistenza sia specificata con apposite *keyword*).

#### ODL

Per la gestione della struttura dei dati (*type system*) si usa la **ODL** (*Object Definition Language*) analoga alla DDL di un DBMS relazionale.

##### Tipi

Oltre ai soliti attributi di base letterali (tipo numerici, stringhe, temporali...), la ODL permette la definizione di **tipi costruttore** (che possono contenere <u>costruttori di tipo</u>), come:

- **Tuple**: simili a record o struct,
- **Collezioni**: tipo liste, insiemi...

> [!example] Esempio
> Un esempio di definizione di tipo è:
> ```sql
> define type Department(
> 	tuple(
> 		name: string;
> 		number: int;
> 		head: tuple(manager: Employee; date: Date;)
> 		locations: set(string);
> 	);
> )
> ```

##### Classi

Definire un tipo (come fatto sopra) specifica solo lo **stato** delle sue istanze, mentre una **classe** comprende:

- **Stato**: <u>il tipo definito</u> (come sopra),
- **Comportamento**: le <u>firme dei metodi</u> da implementare (non implementati ancora, come se fossero astratti).

> [!example] Esempio
> ```sql
> define class Department(
> 	type tuple(
> 		name: string;
> 		number: int;
> 		head: tuple(...)
> 		locations: set(string);
> 	);
> 	operations:
> 		addDepartment(d: Department): bool;
> 		removeDepartment(d: Department): bool;
> )
> ```
> Le implementazioni delle varie `operations` saranno scritte nel linguaggio ad oggetti host (tipo Java); inoltre, avendo `d` istanza di `Department`, si potranno invocare le sue operazioni con `d.operation()`.
> (Non si capisce bene la sintassi e non si sa se posso avere più `type` in una classe).

##### Persistenza

Per salvare dati in memoria bisogna rendere gli oggetti **persistenti** (<u>non transienti</u>, ovvero che permangono attraverso le esecuzioni); e i DB *object-relational* usano 3 meccanismi:

- ***Naming***: questo implica assegnare un <u>nome univoco</u> ad un oggetto, cosicché sia indirizzabile attraverso esso (sul disco) rendendolo un **PNO** (*persistent named object*).
- ***Reachability***: questa implica che tutti i <u>sotto-oggetti</u> di un PNO sono <u>raggiungibili attraverso esso</u>; e perciò, sono anch'essi <u>persistenti</u>.
- ***Extent***: un *extent* invece indica l'<u>insieme dei PNO</u> di un certo <u>tipo definito</u> (e dei suoi <u>sottotipi</u>).

> [!example] Esempio
> ```sql
> define class DepartmentSet(
> 	type:
> 		set(d: Department);
> 		...
> 	operations:
> 		...
> 	extent:
> 		Departments: DepartmentSet;
> )
> ```
> Dove nell'*extent*, `Departments` è il nome che rende dei PNO tutti gli oggetti di tipo `Department` (all'interno di `DepartmentSet`).

#### OQL

La **OQL** (*Object Query Language*) è il linguaggio di interrogazione standard che cerca di rifarsi al modello dichiarativo di SQL: **SFW** (`SELECT FROM WHERE`); solo che questo deve consentire anche la navigazione di strutture complesse e gerarchiche di dati e lo fa con le ***path expressions*** (`object.attr` in *dot notation*) tipica della OOP.

> [!example] Esempio
> Nota: è necessario che nella clausola `FROM` vi sia un PNO che fa da *entry point* al DB:
> ```sql
> SELECT d.name
> FROM d in Departments;
> ```

###### Risultati delle query

Mentre in SQL le query sulle tabelle restituiscono altre tabelle, negli OODB il tipo restituito di default è un ***multi-set***: un <u>insieme non ordinato di valori che possono ripetersi</u> (ma è possibile specificare tipi di output diversi, tipo se si sceglie un *set* verranno rimossi i duplicati dall'insieme).

Sebbene sia più complesso riutilizzare i risultati per altre query rispetto a SQL, qui è più semplice la <u>ristrutturazione delle risposte</u> (costruire un output particolare con una struttura arbitraria).

###### Data reachability

Bisogna prestare particolare attenzione alla ***reachability*** in quanto è <u>monodirezionale</u>; questo mette a rischio le prestazioni del database e la correttezza delle query, rendendo più complessa la fase di progettazione.

Dato uno schema con 2 classi `A` e `B` legate da una associazione dove le istanze di `A` sono persistenti mentre quelle di `B` sono raggiungibili da quelle di `A` (calcolate a runtime), allora:

- Una query che "parte" da `A` e accede alle istanze di `B` associate funziona correttamente,
- Una che invece "parte" dalle istanze di `B` non ancora materializzate, non funziona. 

##### Vantaggi e svantaggi

Il principale vantaggio di questo modello è la rappresentazione naturale dei dati senza necessità di appiattirli o semplificarli; in compenso tale presenta vari svantaggi (causa della sua scarsa adozione):

![](https://i.imgur.com/8btD3lO.png)

---

Prossima lezione: [[3 - Modello object-relational]]

