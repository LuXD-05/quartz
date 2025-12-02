# Lezione 3

### SQL

Il **SQL** (*Structured Query Language*) è il linguaggio principale per la gestione dei dati usato dalla maggior parte dei DBMS relazionali. Il SQL è un linguaggio:

- **Dichiarativo**: descrive cosa fare e non come, è più astratto degli altri linguaggi moderni e si basa sull'**algebra relazionale** (almeno per le query),
- ***Set-oriented***: gli operatori operano su relazioni (viste come ***set***, insiemi) e restituiscono sempre una relazione come risultato.

###### Operazioni

![](https://i.imgur.com/sfKi6Yn.png)

##### Tipi di dato

###### Testuali

- **char** --> 1 char fisso da 1 byte,
- **char(N)** --> N char fissi da N byte,
- **varchar(N)** --> stringa lunga max N byte.

###### Numerici

Int, smallint, real, numeric, float/double(n_cifre, precisione).

###### Temporali

- **date** --> solo data, scritta come stringa tra "", formato: "yyyy-MM-dd", 
- **time** --> solo tempo, scritto come stringa tra "", formato: "hh:mm:ss",
- **datetime** --> data e ora, scritti come stringa tra "", formato: "yyyy-MM-dd hh:mm:ss",
- **timestamp** --> timestamp come in PHP, formato: "yyyy-MM-dd hh:mm:ss.xxxxxx".

###### Altri

- **Boolean** (`tinyint(1)` a volte),
- **BLOB** (*binary large object*, per stringe binarie grandi come per foto e testi),
- **enum**: lista che accetta solo certi valori predefiniti.

###### NULL

Abbiamo già discusso del tipo `NULL` nella [[2 - Modello relazionale#NULL|lezione precedente]] e ora vediamo come viene valutato dai DBMS. Per le operazioni logiche i DBMS usano 3 valori di verità: `true` (`T`), `false` (`F`) e `unknown` (`?`, indica che il valore del predicato non è determinabile); le seguenti tavole di verità indicano come funziona la valutazione:

![](https://i.imgur.com/gFalGlX.png)

> [!info] Nota
> `NULL == NULL` $\;\rightarrow\;$ `NULL`, non `true`.
> Tuple i cui valori di verità (di una query) sono `?` non vengono restituite dall'interrogazione.
> Se valutando un vincolo di integrità la condizione restituisce `?`, il vincolo <u>non è violato</u>.
> Per controllare se un valore è `NULL` o meno, si usano `IS NULL` e `IS NOT NULL`.

#### DDL

###### Constraints

I [[2 - Modello relazionale#Vincoli di integrità|vincoli di integrità]] di cui si parlava nella lezione precedente sono detti *constraints* e sono applicabili alle colonne delle tabelle durante le operazioni di creazione e alterazione; tali sono poi verificati per durante ogni operazione di inserimento o modifica dei dati nelle righe e, se un vincolo è violato, l'istruzione SQL eseguita genera un errore.

- `PRIMARY KEY`: indica che il campo è **PK** ed implica `UNIQUE` e `NOT NULL` (e in certi DBMS anche `AUTO_INCREMENT`); una sola specificabile per tabella.
- `AUTO_INCREMENT`: solo per campi numerici interi, questo incrementa in automatico il valore del campo di ogni nuova riga creata (occhio agli errori con delete/update).
- `UNIQUE`: indica che il campo non ammette valori duplicati (eccetto `NULL` eventualmente).
- `NOT NULL`: indica che la colonna non può assumere valori `NULL` (obbligatoria).
- `DEFAULT()`: indica che di default, ogni nuova riga avrà il valore indicato tra parentesi per quella colonna anche se non si specifica il campo all'inserimento (il valore cambia invece se si specifica il campo con un valore diverso all'inserimento).
- `CHECK()`: indica tra parentesi l'<u>espressione logica che deve essere soddisfatta</u> (tipo: `CHECK(age BETWEEN 18 AND 120)`) e tale vincolo può essere applicato ad <u>1 o più campi</u> di 1 relazione (`CHECK startDate < endDate`); alcuni DBMS non vi permettono l'uso di certe funzioni, tipo MySQL `NOW()`).

###### Foreign key

Il *constraint* `FOREIGN KEY` indica che l'attributo `attr1` di una tabella chiamiamola `tab1`, si riferisce ad un altro `attr2` di un'altra tabella `tab2` ed è tipo:

```mysql
-- Generale
FOREIGN KEY <tab1>.<attr1> REFERENCES <tab2>(<tab2>.<attr2>) ON UPDATE <azione> ON DELETE <azione>;
-- Esempio
FOREIGN KEY Studenti.fkClasse REFERENCES Classe(Classe.id) ON UPDATE CASCADE ON DELETE SET NULL;
```

Quindi stiamo dicendo che il campo `fkClasse` della tabella `Studenti` si riferisce al campo `id` di `Classe`.

Inoltre ci sono le clausole `ON UPDATE` e `ON CASCADE`, per le quali va definita un'**azione** da eseguire in caso che un aggiornamento/cancellazione modifichi/cancelli il campo referenziato (quello di `tab2`, il 1° è solo una FK e anche se `NULL` non ci sono problemi), le quali sono:

- `NO ACTION` (o `RESTRICT`): <u>impedisce di modificare/cancellare</u> la riga nella tabella riferita (`tab2`) se la tabella referente (`tab1`) ha righe con FK che si riferiscono a quella.
- `SET DEFAULT`: quando si modifica/cancella la riga nella tabella riferita (`tab2`) il campo FK delle righe di (`tab1`) che si riferivano a quella è impostato al <u>valore di default</u>.
- `SET NULL`: quando si modifica/cancella la riga nella tabella riferita (`tab2`) il campo FK delle righe di (`tab1`) che si riferivano a quella è impostato a `NULL`.
- `CASCADE`: propaga modifiche/cancellazioni delle righe della tabella riferita (`tab2`) alle righe di (`tab1`) che si riferiscono ad esse.

##### CREATE

Comando usato per la creazione di varie cose tra cui:

###### DATABASE

```mysql
CREATE DATABASE <nome_db>;
```

###### TABLE

```mysql
CREATE TABLE <nome_relazione> (
	<nome_colonna> <tipo_dati> <constraints>,
	...
) ENGINE = InnoDB;
```

`ENGINE = InnoDB` è usato in ambienti MySQL tipo in PhpMyAdmin e senza questa riga le tabelle vengono create con motore `MyIsam` che non gestisce FK.

##### DROP

Comando usato per l'eliminazione di un oggetto come `DATABASE` o `TABLE`:

```mysql
DROP TABLE <nome_tabella>;
```

In coda è possibile aggiungere una delle 2 clausole:

- `RESTRICT`: (di default) non rimuove la tabella se vi sono vincoli, view... che ne dipendono.
- `CASCADE`: gli oggetti che dipendono dalla tabella vengono automaticamente cancellati.

##### ALTER

Usato principalmente su `TABLE`, ne modifica la struttura attraverso diverse azioni:

```mysql
ALTER TABLE <nome_tabella> <azione>;
```

###### MODIFY 

Modifica il <u>tipo di una colonna</u> (ma non il nome).

```mysql
ALTER TABLE Studenti MODIFY nome varchar(30) NOT NULL;
```

###### RENAME 

Modifica il <u>nome di una colonna (ma non il tipo)</u>.

```mysql
-- COLUMN
ALTER TABLE Studenti RENAME COLUMN id TO matricola;
-- TABLE
ALTER TABLE Studenti RENAME TO Alunni;
```

###### CHANGE

Può modificare il tipo di una colonna, ma necessita anche di cambiarne il nome.

```mysql
ALTER TABLE Studenti CHANGE id matricola varchar(30) NOT NULL;
```

###### ADD

Aggiungere una colonna alla tabella (e ne definisce eventuali constraint) o un constraint a una colonna.

\- `AFTER`: indica dopo quale colonna aggiungere la nuova,

\- `FIRST`: permette di aggiungerla in prima posizione (altrimenti di default viene aggiunta alla fine).

```mysql
ALTER TABLE Studenti ADD cognome varchar(30) NOT NULL AFTER nome;
```

Si possono anche aggiungere constraints a colonne già esistenti (esempio `CHECK` su data):

```mysql
ALTER TABLE Studenti ADD CONSTRAINT chk_constraint_1 CHECK(nascita > "1900-01-01");
```

###### DROP

Elimina una colonna o un constraint di una colonna dalla tabella.

```mysql
ALTER TABLE Studenti DROP COLUMN cognome;
```

Si possono anche eliminare constraints a colonne già esistenti (esempio `CHECK` su data):

```mysql
ALTER TABLE Studenti DROP CONSTRAINT chk_constraint_1;
```

Anche per questi ci sono le opzioni `RESTRICT` e `CASCADE`.

#### DML

Per la manipolazione dei dati, SQL fornisce 3 comandi fondamentali che permettono l'alterazione dello stato del database, a causa di ciò è necessario controllare i vincoli d'integrità con ognuna di esse (inoltre ogni istruzione può aggiornare il contenuto di una sola tabella).

##### INSERT INTO 

Inserisce dati all'interno di una tabella con la possibilità di specificare <u>quali campi</u> e <u>quante righe</u> inserire (righe multiple solo separate da "," generalmente).

```mysql
-- Insert singolo
INSERT INTO Studenti (nome, dataNascita, fkClasse) VALUES ('mario', '2000-01-01', 1)
-- Insert multiplo
INSERT INTO Studenti (nome, dataNascita, fkClasse) 
VALUES
    ('bulzo', '2001-04-07', 2),
    ('gil', '2002-05-08', 3),
    ('dis', '2003-06-09', 4);
```

> [!info] Note
> - I campi `AUTO_INCREMENT` sono omissibili (dato che si auto-incrementano) sia dalle colonne che dalle righe da inserire,
> - Campi con valori di default o `NULL` assumono il valore di default o `NULL` in caso vengano omessi (sia come colonna sia come valore della tupla insieme),
> - Si possono rimuovere anche tutti i nomi di colonna, ma in quel caso i valori vanno scritti tutti e in ordine.

###### Subquery di inserimento

Come piccolo spoiler, si possono inserire dati appena prelevati da una tabella ad un'altra (basta che i campi selezionati siano almeno quelli indispensabili alla tabella):

```mysql
INSERT INTO StudentiDiMilano
(SELECT id, nome FROM Studenti)
WHERE LuogoNascita = 'Milano';
```

Questa `SELECT` non può contenere `ORDER BY`.

##### UPDATE

Aggiorna gli attributi con i valori specificati si possono aggiornare più campi di un record in una volta sola, ma separati da ",".

```mysql
UPDATE Studenti 
SET 
	nome = 'gil', 
	nascita = '2000-01-01' 
WHERE 1;
```

Nota: non applicare clausole di restrizione provoca l'aggiornamento di <u>tutte le righe della tabella</u>.

##### DELETE FROM 

Elimina record da una tabella in base a dei vincoli (se omessi, tutti i record saranno eliminati).

```mysql
DELETE FROM Studenti WHERE 1;
```

Ovviamente nella `WHERE` ci può essere una qualsiasi clausola logica ([[#WHERE|WHERE]]).

> [!warning] Attenzione
> Usare `DELETE FROM` <u>non resetta indici e valori</u> `AUTO_INCREMENT`, perciò in caso di cancellazione dopo che sono state inserite tipo 3 righe, l'id successivo sarà il 4.

###### TRUNCATE

Comando usato per cancellare tutti i dati in una tabella <u>resettando indici e valori</u> `AUTO_INCREMENT`:

```mysql
TRUNCATE TABLE Studenti;
```

#### Query e funzioni

##### SELECT

Comando usato per ottenere certe righe di 1 o più tabelle in base a certe clausole.

```mysql
SELECT <attr1>, <attr2> FROM <tab1>;
```

Si può scegliere ogni attributo delle relazioni (separati da ",") specificate nel `FROM` e con `*` si indicano tutti gli attributi della relazione.

###### WHERE

Esegue una restrizione sui campi delle tabelle su cui avrà effetto la query.

```mysql
SELECT * FROM Studenti WHERE nome = 'luca';
```

Nella `WHERE` si possono usare tanti **[[#Operatori|operatori]]** per la costruzione di clausole logiche complesse.

> [!info] Nota
> In ordine di valutazione: 1) letta la clausola `FROM`, 2) applicata la clausola `WHERE` sulle tabelle lette, 3) scelti gli attributi della relazione risultante.

###### AS

Definisce l'alias di una tabella o attributo. L'alias verrà riportato come nome di colonna della `SELECT` se selezionato e si riferirà sempre a una sola tabella univocamente.

```mysql
SELECT s.numMat AS NumeroMatricola FROM Studenti AS s;
-- Nota: AS è omissibile in certi casi
SELECT s.numMat AS NumeroMatricola FROM Studenti s;
```

Molto utile in caso un attributo ha un nome poco riconoscibile nello schema e si vuole capire a 1° impatto cos'è, oppure quando si sta lavorando con delle query complesse e non si vuole riscrivere troppe volte il nome di una tabella se complesso.

###### DISTINCT

Permette alla query di selezione di ritornare solo <u>valori distinti</u> dei campi selezionati.

```mysql
SELECT DISTINCT fkClasse FROM Studenti;
```

##### Operatori insiemistici

> [!warning] Compatibilità degli schemi
> Gli output delle 2 query tra cui si fa `UNION`, `INTERSECT` o `EXCEPT` devono avere schemi **compatibili**, ovvero:
> - <u>Stesso numero di colonne</u> (selezionate),
> - <u>Tipi delle colonne compatibili e in ordine corrispondente</u> (tipo `int` $\leftrightarrow$ `int`).

###### UNION

Date 2 query è possibile usare `UNION` per eseguire l'**unione insiemistica** dei 2 risultati:

```mysql
-- Ritorna calciatori E cestisti
-- Rimuove duplicati
SELECT nome FROM Calciatori
UNION
SELECT nome FROM Cestisti
-- Mantiene duplicati
SELECT nome FROM Calciatori
UNION ALL
SELECT nome FROM Cestisti
```

###### INTERSECT

Date 2 query è possibile usare `INTERSECT` per eseguire l'**intersezione insiemistica** dei 2 risultati:

```mysql
-- Ritorna persone sia calciatori sia cestisti
SELECT nome FROM Calciatori
INTERSECT
SELECT nome FROM Cestisti
```

###### EXCEPT

Date 2 query è possibile usare `EXCEPT` o `MINUS` per eseguire la **differenza insiemistica** dei 2 risultati:

```mysql
-- Ritorna calciatori ma non calciatori/cestisti
SELECT nome FROM Calciatori
ECXEPT
SELECT nome FROM Cestisti
```

##### Funzioni di ordinamento

###### ORDER BY

Ordina le tuple risultanti in base all'attributo specificato. L'ordine di default è **crescente** con `ASC`, ma può anche essere **decrescente** con `DESC` (questi <u>alla fine di</u> `ORDER BY`):

```mysql
SELECT s.nome 
FROM Studenti AS s 
ORDER BY s.nome DESC;
```

> [!warning] Nota
> Gli attributi di ordinamento <u>devono</u> comparire nella clausola `SELECT` altrimenti non funziona.

##### Funzioni di aggregazione

Si può anche usare `DISTINCT` all'unterno delle funzioni di aggregazione. Se l'insieme di valori da aggregare è vuoto le funzioni ritornano `NULL` (`COUNT` ritorna 0).

###### COUNT

**Conta** le tuple selezionate tra parentesi:

```mysql
-- Ritorna il numero totale di studenti
SELECT COUNT(*) AS nStudenti FROM Studenti;
```

###### SUM

**Somma** il valore dell'attributo specificato tra parentesi di tutte le tuple selezionate (accetta solo valori numerici):

```mysql
-- Somma le ore di assenza lo studente con la matricola data
SELECT SUM(ore) AS totAssenze FROM Assenze WHERE matricola = "556677";
```

###### MAX/MIN

Ritornano il valore **massimo/minimo** dell'attributo tra parentesi tra i risultati della selezione:

```mysql
-- Ritorna il voto massimo e quello minimo mai presi da chiunque
SELECT MAX(voto) AS votoMax, MIN(voto) AS votoMin FROM Voti;
```

###### AVG

Ritorna la **media** dei valori tra parentesi del risultato della selezione (accetta solo valori numerici):

```mysql
-- Ritorna la media totale dei voti
SELECT AVG(voto) AS media FROM Voti;
```

##### Funzioni di raggruppamento

Le funzioni di aggregazione sono molto usate con quella di raggruppamento `GROUP BY` che permette di aggregare certi valori in base a certi gruppi.

###### GROUP BY

La proiezione può contenere solo colonne che compaiono anche nella clausola `GROUP BY` oppure funzioni di raggruppamento:

```mysql
SELECT nome, AVG(voto) FROM Voti GROUP BY nome;
```

> [!warning] `ONLY_FULL_GROUP_BY`
> In una query con raggruppamento, i valori selezionati dovrebbero essere o aggregati o presenti nella clausola `GROUP BY`; in caso contrario:
> ```mysql
> SELECT nome, data, AVG(voto) FROM Voti GROUP BY nome;
> ```
> Qui `data` non è corretto perché non è né aggregato né raggruppato, quindi il DBMS lancerà un errore. Questo se non si disattiva la modalità SQL `ONLY_FULL_GROUP_BY`; in quel caso SQL sceglierà uno dei valori di data nel gruppo e lo farà apparire lì (ma non ha senso a meno che le date non sono tutte uguali e a quel punto raggruppabili).

###### HAVING

La clausola `HAVING` è fondamentale per definire restrizioni sui gruppi in quanto la `WHERE` non ne è capace e può solo restringere le tuple prima che vengano raggruppate.

```mysql
-- Seleziona studenti con media sufficiente in su
SELECT nome, AVG(voto) AS media
FROM Voti
WHERE anno = 2024     -- filtra le righe singole (solo anno 2024)
GROUP BY nome         -- raggruppa per studente
HAVING media >= 6;    -- filtra il valore aggregato di ogni gruppo
```

#### Operatori

Ci sono tanti operatori oltre ai classici `AND`, `OR` e `NOT` logici:

###### BETWEEN

Verifica se il valore di un attributo è compreso tra 2 valori (`BETWEEN` funziona con numeri e date):

```mysql
WHERE Studenti.eta BETWEEN 15 AND 20;
```

###### LIKE

Verifica se il valore stringa di un attributo rispetta la condizione specificata; tipo una ***regex***:

```mysql
WHERE Studenti.nome LIKE "Mar%*";
```

I caratteri jolly sono:

`*` --> (in alcuni motori anche `_`), sostituisce 1 solo carattere,

`%` --> sostituisce una sequenza di caratteri di lunghezza indefinita.

###### IN

Verifica se il valore di un attributo è contenuto in un certo range/enum di valori:

```mysql
WHERE Studenti.nome IN("Mario", "Maria", "Gilberto");
```

##### Funzioni temporali

- `CURRENT_DATE()` = ritorna la data corrente.
- `CURRENT_TIME()` = ritorna l'ora, minuto e secondo corrente.
- `DATE(datetime)` = ritorna la parte di data dal datetime.
- `TIME(datetime)` = ritorna la parte di tempo dal datetime.
- `DAY(datetime)` = ritorna il giorno del datetime.
- `DAYOFMONTH(datetime)` = ritorna il giorno del mese del datetime.
- `HOUR(datetime)` = ritorna l'ora del datetime.
- `YEAR(datetime)` = ritorna l'anno del datetime.

> [!warning] Nota
> Alcuni motori non consentono l'utilizzo di funzioni temporali o stored procedures all'interno delle clausole dei constraint `CHECK`.

#### Eventi e trigger

Gli **eventi** sono delle operazioni che avvengono sul database che possono scatenare certe azioni. Generalmente questi eventi sono scaturiti da operazioni di `INSERT`, `UPDATE`, `DELETE`, `CREATE/ALTER/DROP TABLE` e altri comandi. 

I ***trigger*** sono delle procedure automatiche (specifiche per una tabella o vista) che reagiscono a tali eventi e che eseguono un certo blocco di codice quando l'evento di cui sono in ascolto si verifica.

```mysql
DELIMITER //
CREATE TRIGGER trg_check_date
BEFORE INSERT ON courses
FOR EACH ROW
BEGIN
  IF NEW.startDate > NEW.endDate THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Course cannot start after it ends';
  END IF;
END;
//
DELIMITER ;
```

###### Timing

Ci sono 2 tipi di ***timing*** che si possono dare ai trigger:

- `BEFORE`: trigger eseguito prima che l'operazione sia finalizzata (utile per modifica o convalida preventive di valori),
- `AFTER`: trigger eseguito dopo che l'operazione è eseguita con successo (utile per log di azioni che dipendono dall'operazione).

###### Granularità

La **granularità** invece indica lo "*scope*" del trigger:

- `FOR EACH ROW`: indica che il trigger è eseguito 1 volta per ogni riga interessata (può usare `NEW` e `OLD` e modificare la riga se usato `BEFORE`),
- `FOR EACH STATEMENT`: indica che il trigger è eseguito 1 volta per l'intera istruzione.

##### Asserzioni

Le asserzioni invece definiscono vincoli globali che coinvolgono più relazioni e devono essere sempre vere. Purtroppo sono un concetto del SQL standard e non sono supportate in tanti DBMS, però sono simulabili attraverso *trigger*.

```mysql
-- Massimo studenti in scuola è 1000
CREATE ASSERTION asrt_max_studenti
CHECK (
   (SELECT COUNT(id) FROM Studenti) < 1000
);
```

#### View

Una ***view*** è una "relazione virtuale" il cui contenuto è definito da una query fatta sul database; sono quindi delle query **ricalcolate ogni volta** (<u>non memorizzate nel database</u>) e utilizzabili come se fossero delle tabelle. Gli usi principali sono:

- <u>Semplificare l'accesso ai dati</u> (si fa una query su una view già filtrata invece di scrivere tutte le condizioni in una volta),
- Fornire <u>indipendenza logica</u> e <u>proteggere i dati</u> (rendo disponibile una view agli utenti e non tutta la tabella).

```mysql
CREATE VIEW <nome_view> [(<colonne>)]
AS <interrogazione>
[WITH [{LOCAL|CASCADED}] CHECK OPTION]
```

##### Uso

Oltre a mostrare certi dati definiti da un'interrogazione, è possibile usare comandi per le tabelle normali anche per le view (`INSERT`, `UPDATE`...), stessa cosa per le loro query di definizione (in esse si possono usare `JOIN`, funzioni di ordinamento/aggregazione/raggruppamento...) e si possono creare view basate su altre view.

> [!warning] Aggiornabilità delle view
> Non su tutte le view si possono fare operazioni di `INSERT`, `UPDATE` o `DELETE` in quanto tali vanno propagate sulle tabelle originali. Infatti, si possono aggiornare solo le view in cui <u>ogni riga corrisponde tale e quale alla stessa nella tabella di base</u>. 
> Non sono aggiornabili le view che, nel blocco più esterno dell'interrogazione che la definisce:
> - Non contengono la PK della tabella di base,
> - Contengono `JOIN`,
> - Contengono funzioni di aggregazione nella `SELECT`,
> - Contengono espressioni nella `SELECT`,
> - Contengono `DISTINCT`.

###### WITH CHECK OPTION

Le view (aggiornabili) possono avere delle clausole `WHERE` nelle loro query di definizione, perciò esiste anche la clausola opzionale `WITH CHECK OPTION`, che impone che i dati modificati continuino a soddisfare le condizioni nella `WHERE` della query di definizione della view:

- (Senza: le tuple aggiornate potrebbero scomparire dalla view).
- `LOCAL`: controlla <u>solo i vincoli della view corrente</u>.
- `CASCADED` (default): controlla i <u>vincoli di tutte le view da cui quella corrente deriva</u>.

##### Comandi

###### CREATE

Per creare una view, bisogna darle un nome e il suo contenuto con una query di `SELECT`:

```mysql
CREATE VIEW vista AS
SELECT s.nome, s.cognome
FROM Studenti s;
```

Si possono omettere le colonne da visualizzare se la query di definizione della view le contiene già.

###### REPLACE

Si può poi sostituire il contenuto di una view lasciandone il nome invariato:

```mysql
REPLACE VIEW vista AS
SELECT s.cognome, s.nome
FROM Studenti s;
```

###### DROP

Per eliminare una view invece:

```mysql
DROP VIEW vista;
```

#### Join

Siccome le tabelle sono relazionate tra loro è possibile che certe interrogazioni richiedano dati presenti in più tabelle; supponiamo di avere le tabelle "studenti" e "voti" separate in relazione `1 - N`, ci sono 2 modi per estrarre i voti di uno studente:

```mysql
-- 1) Prodotto cartesiano
SELECT * FROM Studenti s, Voti v WHERE s.id = v.idStudente AND s.id = "556677";
-- Oppure: ... FROM Studenti CROSS JOIN Voti ...

-- 2) Join
SELECT * FROM Studenti s
JOIN Voti v ON s.id = v.idStudente
WHERE s.id = "556677";
```

Nel 1° caso si usa il **prodotto cartesiano** delle 2 tabelle (<u>ogni riga di "studenti" è associata 1 volta con ogni riga di "voti"</u>) per poi applicarvi il filtro sugli `id` nella `WHERE` (filtrare tutte quelle righe diventa sempre più <u>complesso</u> e richiede sempre più <u>tempo</u> man mano che si aggiungono tabelle al prodotto cartesiano).

Nel 2° caso invece si usa il comando di `JOIN` per unire la 2a tabella cosicché <u>non si vada ad applicare la clausola di join</u> (quella dopo `ON`, che indica quale è il campo che lega le 2 tabelle) <u>su tutte le righe derivate dal prodotto cartesiano</u> (ma ritorna solo quelle che soddisfano la clausola), velocizzando enormemente le query.

![](https://i.imgur.com/1IwI8f2.png)

##### Inner join

###### Equi join

La *join* più classica, collega 2 tabelle basandosi sulla clausola:

```mysql
SELECT s.nome, c.nome 
FROM Studenti s 
JOIN Classi c ON s.fkClasse = c.id
-- Oppure: ... INNER JOIN Classi ON ...
```

Come la *equi-join*, ma le PK e FK associate <u>hanno lo stesso nome</u> (nell'esempio supponiamo `"idClasse"`):

```mysql
-- Sintassi normale (poco usata dato che usa TUTTE le colonne con nome uguale nella join)
SELECT s.nome, c.nome
FROM Studenti s NATURAL JOIN Classi c;
-- Sintassi con USING (più usata)
SELECT s.nome, c.nome
FROM Studenti s JOIN Classi c USING(idClasse);
```

###### Theta join

La ***theta join*** è una inner join particolare in quanto non si basa sulla corrispondenza di 2 campi PK/FK ma usa operatori relazionali tra valori confrontabili:

```mysql
SELECT s.nome, c.nome
FROM Studenti s
JOIN Classi c ON s.media > c.mediaTotale
```

###### Self join

Seppur non precisamente una inner join, la ***self join*** è fatta tra una tabella ed una copia di se stessa per estrarre informazioni; per esempio vogliamo trovare gli studenti con la stessa media (senza fissare una media specifica):

```mysql
SELECT s1.nome, s2.nome FROM Studenti s1
JOIN Studenti s2 ON s1.media = s2.media AND s1.id != s2.id;
```

> [!important] Nota
> 1\) È fondamentale che la tabella oggetto della self join sia rinominata con 2 nomi diversi altrimenti il DBMS non capisce quale è e da errore.
> 2\) Si usa `s1.id != s2.id` per prevenire la duplicazione delle tuple con valori invertiti (studenti $A$ e $B$: $A$ ha la stessa media di $B$ ma anche viceversa = 2 tuple).

##### Outer join

###### Left join

Restituisce le righe della 1a tabella con congiunti gli attributi della 2a. Per le righe della 1a tabella <u>non relazionate ad alcuna della 2a</u> si pongono le righe congiunte di quest'ultima a `NULL` (quindi per gli studenti non assegnati ad una classe ritornerà `NULL` come nome di classe):

```mysql
SELECT s.nome, c.nome
FROM Studenti s LEFT JOIN Classi c ON s.fkClasse = c.id;
```

###### Right join

Restituisce le righe della 2a tabella concatenandogli le righe della 1a. Le righe della 2a che non sono relazionate con alcuna riga della 1a conterranno `NULL` al posto dei valori congiunti di quest'ultima (quindi qui potrebbero venire mostrate classi senza studenti):

```mysql
SELECT s.nome, c.nome
FROM Studenti s RIGHT JOIN Classi c ON s.fkClasse = c.id;
```

###### Full join

Restituisce il risultato della *left join* unito a quello della *right join* (senza duplicati indipendentemente dall'ordinamento delle colonne di 1 o dell'altra) che è diverso da una *inner join* in quanto questo ritorna anche le righe della 1a tabella non relazionate ad alcuna della 2a e viceversa:

```mysql
SELECT s.nome, c.nome
FROM Studenti s LEFT JOIN Classi c ON s.fkClasse = c.id
UNION
SELECT s.nome, c.nome
FROM Studenti s RIGHT JOIN Classi c ON s.fkClasse = c.id;
```

#### Subquery

Le *subquery* sono semplicemente query `SELECT` innestate in altre query (nello specifico all'interno di clausole: `WHERE`, `HAVING` e `FROM`).

> [!info] Tipi di subquery
> Ci sono 3 tipi di subquery:
> - **Subquery scalari**: (o *single-row subquery*) restituiscono un solo valore scalare alla query principale e usano operatori relazionali per confronti di valori,
> - **Subquery di colonna**: (*multiple-row* subquery) restituiscono più righe (sempre di 1 campo) e usano comandi specifici per i confronti.
> - **Subquery di tabella**: (*table* subquery) restituiscono una tabella (più righe e più colonne) e necessitano di costruttore di tupla.

###### Usi

Le subquery si possono avere nelle clausole `WHERE`, `HAVING` e `FROM`.

> [!important] Tabelle derivate
> Nello specifico, le subquery nella clausola `FROM` servono per determinare **tabelle derivate** che sono <u>riferibili come tabelle normali dall'esterno</u> (a livello di attributi) e permettono di interrogare il database con più livelli di aggregazione (vedi [[#Altri esempi|esempio]] di seguito).

##### Operatori

Per le *single-row* subquery non servono nuove funzioni in quanto al massimo si usano quelle di aggregazione; mentre per le *multiple-row* e *table* subquery sono usate in interrogazioni più complesse nelle quali spesso sono necessari predicati particolari che vediamo di seguito:

###### ANY

Il predicato `ANY` è vero se almeno 1 valore restituito dalla subquery soddisfa la condizione di confronto e falso in caso contrario (o se la subquery non ritorna tuple).

```mysql
-- Trovare gli studenti che hanno almeno 1 voto in matematica (DISTINCT per evitare duplicati a causa di + voti)
SELECT DISTINCT s.* FROM Studenti s
WHERE s.id = ANY (
	SELECT studentId FROM Voti
	WHERE materia = 'matematica'
);
```

> [!important] `IN`
> Quando si usa `ANY`, <u>se l'operatore di confronto tra l'attributo e il risultato della subquery è "="</u>, allora si può anche usare l'operatore `IN` che ha la stessa funzione; lo stesso è anche negabile usando `NOT IN`.

###### ALL

Il predicato `ALL` è vero se tutti i valori restituiti dalla subquery soddisfano la condizione di confronto (o se non ritorna tuple) e falso in caso contrario.

```mysql
-- Trovare gli studenti che hanno solo voti in informatica (+ mostrare per ognuno di essi la media)
SELECT s.*, AVG(v.voto) AS media FROM Studenti s    -- (DISTINCT non serve perché c'è già GROUP BY)
JOIN Voti v ON s.id = v.studentId
WHERE s.id != ALL (
	SELECT studentId FROM Voti
	WHERE materia != 'informatica'
)
GROUP BY s.id;    -- Questo senza ONLY_FULL_GROUP_BY, altrimenti dovevo raggruppare tutto di Studenti 
```

###### EXISTS

Il predicato `EXISTS` ritorna vero se la subquery restituisce almeno una tupla, altrimenti falso (se negato con `NOT EXISTS` è viceversa); infatti di solito si usa `SELECT 1` (per convenzione) per indicare la selezione della 1a tupla restituita dall'interrogazione in quanto leggerne altre sarebbe inutile (il risultato è lo stesso). Riscriviamo le query precedenti:

```mysql
-- Studenti con almeno 1 voto in mate
SELECT s.* FROM Studenti s
WHERE EXISTS (
    SELECT 1 FROM Voti v
    WHERE v.studentId = s.id AND v.materia = 'matematica';
);

-- Studenti con solo voti in info (senza media)
SELECT s.* FROM Studenti s
WHERE NOT EXISTS (
    SELECT 1 FROM Voti v
    WHERE v.studentId = s.id AND v.materia != 'informatica'
);
```

> [!important] Subquery correlate
> `EXISTS` è principalmente usato con **subquery correlate**, ovvero delle subquery che fanno uso di dati dalla main query esterna (sopra vedi come fa `v.studentId = s.id`). Queste sono particolari in quanto la subquery non viene fatta una volta ma <u>viene eseguita ripetutamente per ogni tupla da valutare nella query esterna</u> (in questo caso ogni volta che si considera uno studente dalla main query, quello (id) è passato nella subquery per essere valutato).
> Le interrogazioni correlate sono possibili grazie agli [[#AS|alias]] definiti nelle query esterne (non ci si può invece riferire dall'esterno ad alias creati in una subquery interna, eccetto per i casi in cui si usano [[#Usi|tabelle derivate]]).

##### Altri esempi

```mysql
-- 1) Selezionare studenti la cui media è > di quella totale
SELECT DISTINCT s.* FROM Studenti s             -- DISTINCT se no se uno studente ha + voti > media lo si vede + volte
JOIN Voti v ON s.id = v.studentId
WHERE v.voto > ( SELECT AVG(voto) FROM Voti );

-- 2) Selezionare classi la cui media è > di quella totale
SELECT c.nome, AVG(v.voto) AS media FROM Classi c
JOIN Studendi s ON c.id = s.classId
JOIN Voti v ON s.id = v.studentId
GROUP BY c.nome                                 -- Tutti i campi non aggregati in GROUP BY
HAVING AVG(v.voto) > ( SELECT AVG(voto) FROM Voti );

-- 3) ANY / IN


-- 4) ALL


-- 5) EXISTS


-- 6) Costruttore di tupla


-- 7) Tabella derivata --> Trovare lo studente con la media massima
SELECT AnnoIscrizione, MAX(Media)
FROM Studenti s, (
	SELECT v.studentId, AVG(v.voto) AS Media
	FROM Voti v
	GROUP BY v.studentId
) AS Medie m
WHERE s.Matricola = m.Matricola
GROUP BY AnnoIscrizione;
-- non mi piace, rifare
```

---

Prossima lezione: [[4 - Database nelle app]]

