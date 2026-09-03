# Lezione 10

### XML in SQL

Alla fine XML, invece di essere adottato come modello dati per i database, ha finito per essere integrato in SQL con lo standard **SQL/XML**, di cui la versione del 2003 ha aggiunto un <u>tipo di dato</u> `XML`, mentre quella del 2006 ha esteso il supporto ad <u>XQuery</u> (e a <u>XPath 2.0</u>). 

> [!info] Nota
> Ad oggi i DBMS commerciali supportano la possibilità di: 
> - Includere alberi XML come valori delle tabelle,
> - Scrivere query SQL contenenti delle espressioni XQuery (come subquery).

##### Caratteristiche SQL/XML

Lo standard SQL/XML è definito coi seguenti obiettivi:

- ***Shredding* trasparente**: <u>salvare elementi/alberi XML</u> direttamente <u>come valori atomici</u> del *type system* di <u>SQL</u> (invece di usare il tipo `XML`),
- ***XML Publishing***: possibilità di <u>interrogare i database relazionali e ottenere come risultati elementi/alberi XML</u>,
- Fornire un <u>mapping tra i tipi di dato</u> del modello <u>object-relational</u> e quelli di <u>XQuery</u>,
- <u>Interrogare alberi XML</u> (presenti come valori nelle tabelle) e <u>salvare i risultati delle query in</u> altre <u>tabelle</u>.

###### XML Shredding

Prima di SQL/XML, per salvare un albero XML all'interno di un database, era necessario eseguire una trasformazione detta ***XML Shredding***, che ne prevede la "scomposizione" in un'insieme di tabelle, in cui:

- Gli elementi con lo <u>stesso nome</u> sono salvati in una medesima <u>tabella</u> che contiene `NULL` in corrispondenza di <u>nodi mancanti</u> nell'albero (dato che XML è semi-strutturato).
- Ogni <u>legame tra un elemento ed i suoi sottoelementi</u> è rappresentato con un **vincolo FK**.

> [!example] Esempio
> Si considera il seguente albero XML:
> ![](https://i.imgur.com/B5S94kG.png)
> Le tabelle che lo rappresentano sarebbero:
> ```
> movies(movie_id);
> movie(movie_id, title, runtime, year_released, durector_id);
> director(director_id, name, surname);
> ```

#### XML Publishing

##### Funzioni SQL-to-XML

Basandosi sull'albero XML precedente `movies`, sono presentate 4 funzioni principali per estrarre dati da tabelle SQL con risultati in formato XML:

###### XMLELEMENT

Questa funzione, per ogni tupla del risultato della query, restituisce un'<u>elemento XML</u>; ciò con la sintassi: `XMLELEMENT(NAME name, element)`, dove `name` è il nome dell'elemento tra `<>` (il nome del *tag*) ed `element` ne rappresenta il contenuto (simile a `!ELEMENT` di [[6 - DTD#DTD|DTD]]).

> [!example] Esempio
> Per ottenere il titolo di ciascun `movie` si fa:
> ```SQL
> SELECT XMLELEMENT(NAME "title", title) AS "Movie Titles" 
> FROM movie;
> ```
> Ottenendo una tabella con una singola colonna così:
> ![](https://i.imgur.com/N5XnC43.png)

###### XMLATTRIBUTES

Questa funzione serve per definire gli <u>attributi</u> degli elementi ritornati da una `SELECT` con [[#XMLELEMENT]] (solo con esso); e come parametri ha una lista di campi separata da `,`:

> [!example] Esempio
> Per ottenere il titolo di ciascun `movie` avente però durata e il cognome del regista come attributi, si fa:
> ![](https://i.imgur.com/Mgq3Rop.png)
> Ottenendo una tabella del genere:
> ![](https://i.imgur.com/3sESda7.png)

###### XMLEXISTS

Questa funzione è usata nella `WHERE` per filtrare le tuple in base al <u>contenuto di una colonna XML</u> (le query con `XMLEXISTS` ritornano le tuple per cui la XQuery nella funzione ritorna `true`); ed ha come argomenti sempre un'espressione XQuery con parametri.

> [!example] Esempio
> Per ottenere i `movie` la cui durata è > 120, si fa:
> ```sql
> SELECT * FROM movie 
> WHERE XMLEXISTS(
> 	'//runtime[text() > 120]' 
> 	PASSING movie_xml
> );
> ```
> In questa, `PASSING` serve per passare dei parametri da considerare come contesto per la XQuery (in questo caso il campo `movie_xml` della tabella che contiene valori XML).
> Facendo così vengono filtrate le tuple della query includendo solo quelle che nel campo `movie_xml` contengono `runtime > 120`.

###### XMLAGG

Questa funzione aggrega gli `XMLELEMENT` al suo interno in una lista, la quale può essere inserita all'interno di altri `XMLELEMENT`.

> [!example] Esempio
> La stessa query dell'esempio di [[#XMLELEMENT]] ma le cui tuple sono aggregate in una sola tupla in un'elemento `<all-titles>`:
> ![](https://i.imgur.com/79AiuqZ.png)
> Ed il risultato ottenuto è:
> ![](https://i.imgur.com/JCapfHQ.png)

###### XMLFOREST

Questa funzione permette di definire multipli `XMLELEMENT` all'interno di un altro (padre) con una lista di `XMLELEMENT` separati da `,` come parametro.

> [!example] Esempio
> Si vuole ottenere un elemento `movie-details` contenente titolo e anno (ecc...) di ogni film e ci sono 2 modi per fare ciò:
> ![](https://i.imgur.com/1CcdmVS.png)
> La differenza è che:
> - Con `XMLFOREST`, <u>non</u> sarà possibile usare `XMLATTRIBUTES` sugli elementi, però quelli contenenti valore `NULL` verranno <u>omessi</u>.
> - Con più `XMLELEMENT` invece, si potranno <u>specificare attributi per gli elementi</u> ma quelli contenenti valore `NULL` saranno comunque <u>creati vuoti</u>.

##### Funzioni XML-to-SQL

Basandosi sulla seguente tabella (con 2 alberi XML):

![](https://i.imgur.com/zyQpm2v.png)

Vengono presentate 3 funzioni per l'estrazione di dati XML da tabelle per ottenerli in strutture diverse, per esempio come valori di una colonna di una tabella SQL.

###### XMLQUERY

Questa è una funzione usata di solito con `SELECT` che permette di specificare espressioni XQuery/XPath per estrarre nodi "semplici" da alberi XML "complessi" ritornando il risultato in una tabella con singola colonna. Nel seguente esempio se ne vede l'utilizzo con diversi parametri:

- L'espressione XQuery scritta come stringa,
- `PASSING [col] AS "[var]"`: lega alla variabile XQuery `[var]` tra virgolette la colonna `[col]` (nell'esempio sarà usata per iterare i valori della colonna),
- `RETURNING CONTENT`: indica che il valore di ogni tupla restituita è il `CONTENT` del risultato, ovvero (in questo caso) il nodo serializzato in stringa,
- `NULL ON EMPTY`: indica che per gli elementi vuoti, nella tupla risultante sarà inserito `NULL` (altrimenti `EMPTY ON EMPTY` per far avere campi vuoti).

> [!example] Esempio
> Per ottenere i titoli dei film all'interno di elementi `title`, si fa:
> ![](https://i.imgur.com/rBwM9Nf.png)
> Ottenendo quindi:
> ![](https://i.imgur.com/PeJUMr8.png)

###### XMLCAST

Sebbene non usata per estrarre dati, questa funzione è usata per eseguire dei ***cast***, ovvero trasformare un tipo di dato in un altro (è seguita da `AS [type]`).

> [!example] Esempio
> Per calcolare la media delle durate dei film, bisognerà fare un `XMLCAST` sul risultato di una `XMLQUERY`:
> ![](https://i.imgur.com/9R0hfZC.png)
> La query è simile all'esempio di [[#XMLQUERY]], però in questo caso i risultati, prima di essere passati alla funzione `AVG`, vengono *castati* a `DECIMAL(8,1)`, tipo di dati che permette il calcolo della media su di essi, altrimenti la query avrebbe fallito (tentando di fare la media di $n$ nodi XML sottoforma di stringa); infatti si ottiene:
> ![](https://i.imgur.com/V51H3EP.png)

###### XMLTABLE

Questa funzione permette di estrarre dati in forma relazionale da alberi XML, definendo una tabella con più colonne con dati provenienti da alberi XML. La sintassi è molto simile a quella di [[#XMLQUERY]] e gli argomenti sono divisibili in 2 gruppi:

- Il ***row pattern***: l'espressione XQuery (+ `PASSING` e altri eventuali parametri) usata per generare le righe della relazione risultante,
- Il ***column pattern***: che fa uso della *keyword* `COLUMNS` dopo la quale si specifica una colonna per riga con la sintassi: `"[col]" [type] PATH '[exp]',` (`col` e `type` sono autoesplicativi dall'esempio, mentre `PATH` indica che l'espressione XQuery `exp` che determina il valore di ogni riga nella colonna).

> [!example] Esempio
> Per ottenere una tabella "piatta" le cui colonne sono titolo, durata e anno di ogni film, si fa:
> ![](https://i.imgur.com/iS1m3dR.png)
> Ottenendo:
> ![](https://i.imgur.com/qCioew7.png)

##### Aspetti non considerati da SQL/XML

Uno degli aspetti principali non considerati dallo standard è la definizione di un metodo di progettazione che "guidi" il mapping tra la rappresentazione tabellare e ad albero XML dei dati (e viceversa). Per esempio, la seguente tabella `T`:

![155](https://i.imgur.com/KsoFAgH.png)

Può corrispondere a 2 alberi diversi:

![472](https://i.imgur.com/RttdyTH.png)

Sebbene in generale ci siano numerosi metodi di progettazione, nessuno è standard; perciò tale aspetto è lasciato alla decisione del progettista.

---

Prossima lezione: [[11 - JSON]]

