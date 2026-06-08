# Lezione 3

### Modello object-relational

Il modello ***object-relational*** nasce da una fusione del precedente *object-oriented* e il modello relazionale (integrazione poco elegante a causa di alcune incoerenze ma comunque standardizzato da SQL3/SQL:99 ed implementato in tutti i DBMS relazionali moderni).

##### Caratteristiche

Le principali caratteristiche di tale modello sono:

- **UDT** (*User-Defined Types*): possibilità di definire dei tipi complessi con strutture nidificate, costruttori e metodi (oltre ai tipi base predefiniti).
- ***Typed tables***: tabelle che sono istanze di UDT con comportamento implementato (che come per il resto dei tipi possono essere organizzate in gerarchie con specializzazione ed ereditarietà).

> [!info] Vantaggi
> Il modello *object-relational* preserva il principale [[2 - Modello object-oriented#Vantaggi e svantaggi|vantaggio del modello object-oriented]] però garantendo la possibilità di operare sul DB utilizzando il DDL di SQL imparando solo poca sintassi aggiuntiva e spesso mantenendo l'efficienza tipica dei DBMS relazionali.

#### Tipi

##### Row

I tipi con costruttori principali includono multiset, array (sequenza di elementi di tipo <u>omogeneo</u>) e ***row*** (sequenza di elementi di tipo <u>eterogeneo</u>, in pratica tuple/struct che formano le righe di una tabella). Per la creazione di una *row* si ha:

```sql
CREATE TYPE Name AS (
	firstname VARCHAR(20),
	lastname VARCHAR(20)
) FINAL;    -- FINAL indica che il tipo non ammette sottotipi (di default li ammette come se fosse "NOT FINAL")
```

###### Row type anonimi

All'interno degli *statement* `CREATE TABLE` è possibile definire direttamente dei *row type* (detti anonimi):

```sql
CREATE TABLE Person( 
	name ROW(
		first_name VARCHAR(20),
		last_name VARCHAR(20)
	), 
	address ROW( 
		street VARCHAR(50),
		city VARCHAR(30),
		zip_code NUMERIC 
	), 
	birth DATE
);
```

##### Table

Il principale uso che si ha dei [[#Row|row type]] è nelle ***table***, dove è possibile assegnarli ad un attributo di esse (come i tipi di base), tipo:

```sql
CREATE TABLE Person(
	name Name,
	address Address,
	birth DATE
);
```

Si va quindi a definire una struttura nidificata delle tabelle (attributi che hanno sotto-attributi); per cui il modello relazionale diventa <u>modello relazionale nidificato</u>, rendendo non più necessaria l'eliminazione degli attributi composti nella fase di progettazione logica.

###### Typed table

C'è anche un altro modo di creare tabelle; e ciò è fatto con le ***typed tables***, che prevedono:

```sql
-- 1) Creazione di un row type con dentro tutti gli attributi della tabella
CREATE TYPE PersonType(
	name Name, 
	address Address,
	birth DATE
);
-- 2) Creazione di una table in cui le righe sono istanze di tale row type (keyword "OF")
CREATE TABLE Person OF PersonType;
```

#### Metodi

Per i tipi è quindi anche possibile definire dei metodi e ciò si fa in 2 passaggi: innanzitutto si specifica la firma del metodo nel comando di creazione del tipo, per poi implementarlo con il comando `CRATE INSTANCE METHOD`:

```sql
CREATE TYPE PersonType(
	name Name, 
	address Address,
	birth DATE
) METHOD age_on_date(on_date DATE) RETURNS INTERVAL YEAR;

CREATE INSTANCE METHOD age_on_date(on_date DATE)
	RETURNS INTERVAL YEAR
	FOR PersonType                 -- Keyword "FOR": necessaria per definire il tipo a cui il metodo è associato
	RETUTN on_date - SELF.birth    -- Keyword "SELF": usata x riferirsi all'istanza del tipo a cui il metodo...
```

Un esempio di invocazione di tale metodo è:

```sql
SELECT name.lastname, age_on_date(CURRENT_DATE) FROM Person;
```

### Ereditarietà

In questo modello l'ereditarietà riguarda sia tipi che tabelle:

##### Di tipi

Per quanto riguarda i tipi, è possibile definire un sottotipo con la keyword `UNDER`:

```sql
CREATE TYPE Student UNDER Person AS (
	id NUMERIC,
	degree VARCHAR(50)
) FINAL;
```

In questo modo le istanze di `Student` avranno tutti gli attributi di `Person` più `id` e `degree`.

> [!warning] Attenzione
> Al contrario di Java, un tipo SQL può avere <u>al massimo 1 solo supertipo</u>, ovvero <u>non</u> è supportata l'**ereditarietà multipla**.

###### Istanziabilità

Oltre alla keyword `FINAL` (usata per indicare se un tipo può avere sottotipi o meno), esiste anche la keyword `INSTANTIABLE` (di default) che indica se il tipo/classe è istanziabile o meno (un tipo `NOT INSTANTIABLE` e `FINAL` non è utilizzabile, siccome sarebbe <u>astratto</u> e <u>non raffinabile</u> al contempo).

##### Di tabelle

Seppur non è necessario che per ogni tipo vi sia una relativa tabella, data una gerarchia di tipi è possibile creare una corrispondente gerarchia di *typed tables* (purché <u>non venga saltato alcun livello della gerarchia</u>):

![526](https://i.imgur.com/UQY7SSm.png)

#### In pratica

##### Sintassi

Per indicare che la tabella `DVDs` eredita da `Movies` si fa:

```sql
CREATE TABLE Movies OF Movie (
	REF IS movie_id SYSTEM GENERATED
);
CREATE TABLE DVDs OF DVD UNDER Movies; 
```

Qui si usa `REF` per definire un attributo aggiuntivo alla tabella `Movies` (la tabella "*root*", quella da cui tutte le altre ereditano) per fungere da <u>identificatore univoco delle tuple</u>.

Si possono anche imporre dei vincoli alle *typed tables* create con la keyword `WITH OPTIONS` (i vincoli saranno poi ereditati dalle relative sottotabelle):

```sql
-- NOTA: duration e price erano già attributi di Movie
CREATE TABLE ShortMovies OF Movie (
	REF IS movie_id SYSTEM GENERATED,
	duration WITH OPTIONS CHECK (duration < 90)    -- Override duration con constraint < 90 min
);
CREATE TABLE ShortDVDs OF DVD UNDER ShortMovies (
	price WITH OPTIONS CHECK (price < 1.99)        -- Override price con constraint < 1.99€
);
-- NOTA: ShortDVDs eredita i vincoli di ShortMovies (quindi anche duration < 90 min)
```

##### Query

Quando si esegue una query su una supertabella, la si sta eseguendo anche su tutte le sue sottotabelle, per esempio:

```sql
SELECT title, duration FROM ShortMovies WHERE duration < 60;
```

Tale query considera tutte le tuple di `ShortMovies` e anche quelle di `ShortDVSs` in quanto ogni istanza di `DVD` è anche istanza di `Movie` (come nella OOP).

Per ottenere invece solo le tuple della tabella specificata nella `FROM` bisogna usare `ONLY`:

```sql
SELECT title, duration FROM ONLY(ShortMovies) WHERE duration < 60;
```

Questa ritornerà il risultato valutando solamente le tuple istanze di `ShortMovies` che <u>non sono istanze anche di</u> `ShortDVDs` (si vede visualmente nel prossimo paragrafo).

#### Gerarchie: tipi vs tabelle

Dal POV dei tipi (quindi *object-oriented*), creando un'istanza di `DDS` si va a creare anche un'istanza di `DVD` e quindi anche una di `Movie`; e ciò è visualizzabile così:

![278](https://i.imgur.com/bEkYeoa.png)

Dal POV delle tabelle (quindi relazionale) invece, esistono dei <u>modelli di consistenza dei dati</u> che definiscono le interazioni tra i ***data model*** *object-oriented* e *relational*.

##### Duplicate row model

Questo modello prevede la <u>duplicazione delle righe fra tabella e supertabella</u>, nel senso:

- Ad ogni <u>riga della supertabella</u> ne corrispondono **1 o 0** della <u>sottotabella</u> (una tupla può essere solo `Movie` o `DVD`, che è anche `Movie`),
- Per ogni <u>riga della sottotabella</u> ne corrisponde **esattamente 1** nella <u>supertabella</u> (una tupla `DVD` è sempre anche `Movie`).

> [!info] Note
> Questo permette di eseguire facilmente le query; tuttavia, oltre alla **ridondanza dei dati**, certe operazioni sono "**pesanti**" a causa delle propagazioni tra tabelle, tipo:
> - `INSERT` in sottotabella: è necessario aggiungere la tupla (con attributi eventualmente ristretti) anche nella supertabella,
> - `DELETE` in supertabella: è necessario propagare a cascata la cancellazione della tupla alle sottotabelle,
> - `UPDATE`: bisogna aggiornare tutti gli eventuali riferimenti in supertabelle e sottotabelle.

##### Single table model

Questo modello fa uso di una <u>singola tabella</u> per contenere l'<u>intera gerarchia di tipi più 1 attributo</u> `hierarchy` che indica a che <u>tipo della gerarchia</u> corrisponde quella tupla. Siccome la tabella contiene tutti gli attributi di tutti i sottotipi, quelli che non appartengono all'istanza della singola tupla sono posti a `NULL`.

> [!info] Note
> Qui sono semplici sia query che aggiornamenti, tuttavia di solito si ha notevole spreco di spazio a causa dei tanti valori `NULL`.

##### Union model

Questo modello invece <u>separa le istanze dei vari tipi nelle rispettive tabelle</u> (`Movies` contiene solo istanze `Movie` mentre `DVDs` contiene solo istanze `DVD`). L'unico problema è che le query su una tabella devono restituire risultati valutandone anche tutti i sottotipi (senza `ONLY`), perciò una query del genere:

```sql
SELECT title, duration FROM Movies WHERE duration < 60;
```

Viene reinterpretata così dal DBMS:

```sql
SELECT title, duration FROM Movies WHERE duration < 60 
UNION 
SELECT title, duration FROM DVDs WHERE duration < 60;
```

> [!info] Note
> Questo è il modello concettualmente più "pulito" in quanto evita ridondanze, complessità operazionale e valori `NULL`; l'unica pecca è che rende necessaria la riscrittura delle query, le quali risultano quindi meno efficienti.

---

Prossima lezione: [[4 - OLAP]]

