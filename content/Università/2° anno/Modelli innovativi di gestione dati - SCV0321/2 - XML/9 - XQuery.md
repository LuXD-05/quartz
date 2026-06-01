# Lezione 9

### XQuery

**XQuery** si basa su XPath 2.0 e risolve diversi problemi di quest'ultimo, tra cui:

- L'incapacità di estrarre, confrontare ed elaborare sottoalberi di alberi XML diversi,
- L'incapacità di ristrutturare i risultati, ovvero creare nuovi alberi XML contenenti il risultato di un'interrogazione.

> [!important] Nota
> XQuery introduce una sintassi alternativa per denotare elementi XML che permette di usare **espressioni valutate a *runtime*** (ovvero al momento della lettura del contenuto dell'elemento) e formalizza ciò racchiudendo il contenuto degli elementi tra parentesi graffe; per esempio, i seguenti elementi sono equivalenti:
> ```xml
> <numeri>1 2 3 4 5</numeri>
> <numeri>{ 1 2 3 4 5 }</numeri>
> <numeri>{ 1 to 5 }</numeri>
> ```

##### Type system

XQuery è un linguaggio tipizzato ed il suo *type system* si integra con quello di XML Schema (con anche altri elementi diversi). In generale i tipi XQuery descrivono **sequenze**, ovvero *multi-set* composti da ***items***, i quali possono essere **nodi** o **valori atomici**.

Mentre i tipi di nodi sono i medesimi dell'[[5 - Modelli di dati semi-strutturati#XPath Data Model|XPath Data Model]], i tipi di valori atomici sono 24, di cui: 19 sono i tipi primitivi di XML Schema, mentre gli altri 5 sono tipi usati per descrivere dati non previsti da XML Schema (tipo intervalli temporali).

> [!important] *Type matching*
> Nelle interrogazioni XQuery si può usare il ***type matching*** per determinare il tipo del risultato di un'espressione: `[exp] instance of [type]`, per esempio:
> ![](https://i.imgur.com/55C5hV0.png)

#### Espressioni FLWOR

XQuery aggiunge a XPath 2.0 delle espressioni dette **FLWOR** (*For, Let, Where, Order by, Return*) che agiscono insieme, una dopo l'altra, come in SQL:

- `for`: itera su una sequenza di elementi (facendo sempre uso di un iteratore) ed è analoga all'[[8 - XPath#Espressioni|espressione]] `for` di XPath 2.0,
- `let`: permette di dichiarare altre variabili a *runtime*, eventualmente legandovi valori di altre variabili (come l'iteratore del `for`) anche ricavate da espressioni composte,
- `where`: permette di applicare filtri alle sequenze di variabili generate da `for` e `let` attraverso clausole booleane,
- `order by`: ordina i risultati delle precedenti,
- `return`: calcola e ritorna il risultato valutando, per ogni valore legato alle variabili, un'espressione.

###### Esempio

Dato il seguente albero XML:

![523](https://i.imgur.com/5b6bTjf.png)

Si spiega il seguente codice XQuery:

![438](https://i.imgur.com/vir9dLW.png)

In pratica:

1) `for` itera su ogni elemento `studente` (grazie al `//`) del documento "studenti.xml" assegnando ognuno alla variabile `$s`,
2) `let` definisce `$m` come la lista di elementi `major` di ogni studente,
3) `where` restringe i risultati e mantiene solo gli studenti con un numero di elementi `major` $\ge$ 2,
4) `order by` ordina i risultati in base all'attributo `id` di ogni studente,
5) `return` indica che il valore di ritorno è un elemento `double` contenente il valore dell'elemento `nome` di ogni studente.

> [!info] Nota
> Il risultato di tali interrogazioni è una <u>lista di elementi</u> `double`, tuttavia per renderlo un'albero XML basta racchiudere l'intera sequenza in un'elemento `doubles` così da avere:
> ![](https://i.imgur.com/DTEIriJ.png)

#### Altro

###### `for` vs `let`

Nelle espressioni **FLWOR**, `for` e `let` possono comportarsi in vari modi tra loro:

- Singolo `for`:

  ![](https://i.imgur.com/qfywV0K.png)

- `let` prima di `for`:

  ![](https://i.imgur.com/EssQ8jI.png)

- `for` annidati:

  ![](https://i.imgur.com/mf6vCOK.png)

- `let` doppio:

  ![](https://i.imgur.com/AE3QTjn.png)

> [!info] Nota
> Siccome i valori di `$y` sono indipendenti da quelli di `$x` e viceversa, si ha che:
> ![](https://i.imgur.com/mhNyia8.png)

##### Esempi

###### Query su più documenti

Come XPath 2.0, anche XQuery può esprimere <u>interrogazioni su più alberi XML</u>. Quindi supponendo di avere il precedente albero "ricette.xml" e il seguente "frigorifero.xml":

```xml
<frigorifero>
	<roba>latte</roba>
	<roba>uova</roba>
	<!-- ... -->
</frigorifero>
```

La seguente interrogazione:

![508](https://i.imgur.com/3N2hMMI.png)

Per 1) ogni ricetta `$r` da "ricette.xml", 2) per ogni valore dell'attributo `nome` degli ingredienti `$i` da "ricette.xml" 3) e per ogni roba `$s` da "frigorifero.xml" il cui valore corrisponde ad un'ingrediente di una ricetta, 4) ritorna il valore degli elementi `titolo` distinti (con `fn:distinct-values()`) che hanno almeno 1 roba in frigorifero.

###### Ristrutturazione del risultato

Considerando i documenti XML precedenti, il seguente esempio sottolinea la capacità di ristrutturazione del risultato di XQuery:

![492](https://i.imgur.com/Le762bl.png)

Dove, per ogni ingrediente `$i` distinto in ricette, si ritorna un elemento `ingrediente` con attributo `nome` contenente un elemento `title` (col titolo della ricetta) per ogni ricetta in cui è contenuto; questo tutto all'interno dell'elemento `ingredienti` per ottenere un'albero XML ben formato.

###### Aggregazioni e ordinamento

Sempre dato l'albero XML degli studenti, il seguente codice:

![605](https://i.imgur.com/BAiEmZw.png)

Elenca il nome di ogni studente ordinato in base ai seguenti criteri (in ordine):

1) In ordine decrescente per il numero di voti massimi (30) ricevuti,
2) In ordine decrescente per il numero di *major* (a parità di n° di 30 ricevuti),
3) In ordine crescente di età (a parità di *major*).

> [!info] Nota
> Il contenuto di `age` è testuale ed estratto come testo (`text()`), perciò va convertito in intero (con `xs:integer()`) perché altrimenti andrebbe in ordine lessicografico (facendo risultare, per esempio, 7 come > di 20).

##### Punti deboli

XQuery ha comunque dei punti deboli:

- Complicato,
- Incompleto (almeno per le capacità di *update*, tipo in contesto di database),
- Poco adottati i DBMS che supportano XQuery (e XPath).

---

Prossima lezione: [[10 - XML in SQL]]

