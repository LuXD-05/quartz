# Lezione 4

### OLAP

Mentre prima i DBMS implementavano l'**OLTP** (*On-Line Transaction Processing*), ovvero le "normali" operazioni di lettura, scrittura, aggiornamento ed eliminazione di dati; con SQL:2003 è stato introdotto l'**OLAP** (*On-Line Analytical Processing*), che fa riferimento a tutte quelle interrogazioni effettuate per "analizzare" dati (quindi operazioni complesse, tipo per calcolare valori aggregati...) che prima venivano fatte da applicativi e strumenti esterni.

###### Collection types

Le operazioni OLAP si effettuano principalmente sui ***collection types***, che oltre alle ***row*** ne includono altri, tra cui:

- ***Array***: <u>lista ordinata</u> (numerata) di valori con <u>lunghezza massima prefissata</u>,
- ***Multiset***: <u>lista non ordinata</u> di valori che <u>ammette duplicati</u> e <u>senza limiti di dimensione</u>.

#### Operazioni

Delle seguenti, molte si basano su `GROUP BY`; ripassarne il funzionamento con anche `HAVING`, `EVERY` ed `ANY/SOME`.

##### Definizione e INSERT

Supponendo di avere definito i seguenti:

```sql
CREATE TYPE Publisher AS ( 
	name VARCHAR(20), 
	branch VARCHAR(20) 
); 
CREATE TYPE Book AS ( 
	title VARCHAR(20), 
	author_array VARCHAR(20) ARRAY[10],  -- array con 10 elementi di tipo VARCHAR(20)
	publication_date DATE, 
	publisher Publisher, 
	keyword_set VARCHAR(20) MULTISET     -- multiset di elementi di tipo VARCHAR(20)
);
CREATE TABLE Books OF Book;
```

Per inserire un'istanza di tipo `Book` nella tabella `Books` bisogna eseguire un `INSERT` particolare a causa dei *collection types*:

```sql
INSERT INTO Books VALUES (
	'libro',
	ARRAY['autore1','autore2'],
	'2020-01-12',
	NEW Publisher('nome', 'branch'),
	MULTISET['k1', 'k2', 'k3']
);
```

##### UNNEST

Per interrogare una tabella con tipi come array e multiset si usa il costrutto `UNNEST` (direttamente su tali *collection types*), che crea una tabella temporanea contenente i valori della collezione e che permette di eseguire una subquery in essa.

Per esempio, se per ogni libro si volesse ottenere il titolo e gli autori (in tuple tipo `[titolo, autore]`) si farebbe:

```sql
-- Sintassi: UNNEST(<collection>) AS <table_alias>(<field_alias1>,...)
SELECT b.title, a.author
FROM Books AS b, UNNEST(b.author_array) AS a(author);
```

Ottenendo tipo:

![](https://i.imgur.com/zumdByQ.png)

> [!info] Nota
> Facendo l'`UNNEST` di un array si perde l'informazione sulla posizione dei suoi elementi; perciò se la si vuole mantenere, bisogna usare la clausola `WITH ORDINALITY`:
> ```sql
> SELECT b.title, a.author, a.position
> FROM Books AS b, UNNEST(b.author_array) WITH ORDINALITY AS a(author, position);
> ```
> Ottenendo tipo:
> ![](https://i.imgur.com/4Bo0io2.png)

###### Array access

Per accedere agli elementi degli array non è necessario sempre `UNNEST`, infatti si può utilizzare la notazione posizionale tipica dei linguaggi di programmazione:

```sql
-- Selezionare i primi 2 autori per il libro di titolo 'Compilers':
SELECT author_array[1], author_array[2]
FROM Books
WHERE title = 'Compilers';
```

> [!warning] Attenzione
> Lo standard specifica che gli indici partono da 1 e non da 0.

##### COLLECT

L'operazione inversa ad `UNNEST` è `COLLECT`, la quale si basa su `GROUP BY` ma (invece di eseguire una funzione di raggruppamento sui campi non raggruppati) raccoglie in un multiset i campi non raggruppati dalla query; questa è usata insieme ai costruttori di *row type* per ricreare tabelle con tipi complessi.

Per esempio se si volesse passare dalla seguente tabella `flat_books`:

![627](https://i.imgur.com/rh2EDEC.png)

Ad una complessa `Books`, bisognerebbe fare:

```sql
SELECT 
	title, 
	COLLECT(author) AS author_set, 
	Publisher(publisher_name, publisher_branch) AS publisher, 
	COLLECT(keyword) AS keyword_set 
FROM flat_books 
GROUP BY title, publisher_name, publisher_branch;
-- Nella GROUP BY sembra ci vadano i campi da raggruppare e i campi dei row types
```

Ottenendo così la seguente:

![585](https://i.imgur.com/7kUxyh2.png)

##### ROLLUP e CUBE

Questi operatori estendono `GROUP BY` permettendo di aggregare dati su più attributi all'interno di un'unica query; e per questi si userà il seguente modello di dati:

```sql
CREATE TABLE movie_titles ( 
	title VARCHAR(30), 
	year_released DATE, 
	movie_type VARCHAR(10), 
	dvds_in_stock INTEGER, 
	total_dvd_units_sold INTEGER
	-- ... 
);
```

###### ROLLUP

L'operatore `ROLLUP` aggrega a più livelli in maniera "gerarchica", vediamolo con un esempio: si vuole trovare il "numero di DVD per ogni tipo di film, per ogni anno e per tutti gli anni" (da tradurre per capirla bene); mentre la query è così:

```sql
SELECT movie_type, year_released, SUM(dvds_in_stock) AS sum_of_dvds 
FROM movie_titles 
GROUP BY ROLLUP(movie_type, year_released);
-- Si potrebbe anche aggiungere una "HAVING ..." dopo la "GROUP BY ROLLUP(...)"
```

Ed il risultato che si ottiene è:

![358](https://i.imgur.com/BCitOsk.png)

Da questa tabella si può capire il funzionamento "gerarchico" di `ROLLUP`:

1) Raggruppa `movie_type, year_released`: per ogni coppia `[tipo,anno]` univoca (dove né tipo né anno = `NULL`) sono raggruppati i DVD <u>di quel tipo</u> e <u>di quell'anno</u>.
2) Raggruppa solo `movie_type`: alla fine del dettaglio di un `tipo` per ogni `anno` fa il **subtotale** (con anno = `NULL`) dei DVD <u>di quel tipo</u> <u>per tutti gli anni</u>.
3) Raggruppa tutto `()`: alla fine di tutti i dettagli e subtotali vi è una unica riga (tipo e anno = `NULL`) dove viene fatto il **totale** <u>per tutti i tipi</u> e <u>per tutti gli anni</u>.

###### CUBE

La precedente query di esempio per `ROLLUP` aggregava i risultati per coppia `[tipo,anno]`, per tutti gli anni di ogni `[tipo]` e per tutti i tipi per tutti gli anni; tuttavia mancherebbe il subtotale inverso, ovvero l'aggregazione per tutti i tipi di ogni `[anno]`, perciò la query:

```sql
SELECT movie_type, year_released, SUM(dvds_in_stock) AS sum_of_dvds 
FROM movie_titles 
GROUP BY CUBE(movie_type, year_released);
```

Produce:

![359](https://i.imgur.com/7gam1S2.png)

> [!info] Nota
> Con `CUBE` l'ordine non conta (tanto raggruppa per ogni gruppo possibile); al contrario di `ROLLUP(A, B, C)`, che nell'esempio specifico:
> 1) Raggrupperebbe per `[A,B,C]` univoci,
> 2) Raggrupperebbe per `[A,B]` univoci (`C` = `NULL`),
> 3) Raggrupperebbe per `[A]` univoci (`B` e `C` = `NULL`),
> 4) Raggrupperebbe per `[]` (tutto, con `A`, `B` e `C` = `NULL`).

---

Prossima lezione: [[5 - Modelli di dati semi-strutturati]]

