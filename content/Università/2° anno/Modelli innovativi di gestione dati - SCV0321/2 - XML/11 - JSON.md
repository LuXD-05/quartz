# Lezione 11

### JSON

Un modello dati più recente che ha sostituito XML è **JSON** (*JavaScript Object Notation*), i cui documenti sono dei <u>dizionari chiave-valore</u> (*key-value dictionaries*) chiamati **oggetti** (in JSON, ogni oggetto può contenere altri oggetti come valore).

###### Dizionario

Un **dizionario** è una collezione di coppie di dati in cui uno è detto **chiave** (usata per identificazione e a volte anche per indicizzazione) e l'altro è il **valore** (contiene dati).

I dizionari supportano varie operazioni, tra cui:

- Inserimento,
- Cancellazione,
- Ricerca per chiave (ritorna il valore corrispondente).

> [!info] Nota
> Questa struttura ha tanti nomi (array associativo, *symbol table*, `Map` di Java, `dict` di Python... in javascript ogni oggetto è implementato con un dizionario).

##### Modello dati

Non è ancora standardizzato un *JSON Data Model*, tuttavia una proposta conta 6 tipi di dati:

- **Stringhe**, 
- **Numeri**,
- **Booleani**,
- `null`,
- **Array** (di altri valori),
- **Oggetti** (coppie chiave-valore dove i valori sono dei tipi precedenti).

> [!example] Esempio
> Si consideri il seguente JSON:
> ```json
> {
> 	"name": {
> 		"first": "John",
> 		"last": "Doe"
> 	},
> 	"age": 32,
> 	"hobbies": ["running", "reading"]
> }
> ```
> L'albero corrispondente sarebbe (dove gli oggetti hanno delle *label* per ogni valore mentre gli array hanno indici):
> ![](https://i.imgur.com/cAyvGw3.png)

##### Differenze con XML

La serializzazione JSON è simile a quella di XML ma presenta varie differenze:

- Un oggetto non può avere 2 chiavi con lo stesso nome,
- Con gli array, JSON ne evita la simulazione di XML che avviene duplicando tag all'interno di 1 elemento,
- Gli alberi JSON non sono ordinati (seppur la serializzazione è fatta in ordine, ciò vale in particolare anche per gli indici degli array),
- Il valore di un nodo JSON è l'intero sottoalbero con tale nodo come radice (mentre in XML è solo il valore testuale o il 1° livello di nodi figli del nodo + eventuali attributi),
- In JSON non si possono definire attributi agli elementi.

###### Vantaggi e svantaggi

JSON ha come vantaggi il fatto di essere molto più leggero di XML (serializzazione più veloce per la minor verbosità) e che senza la duplicazione delle chiavi anche l'attraversamento degli alberi è molto più veloce ed efficiente. 

Tuttavia presenta anche uno svantaggio principale: siccome il valore di un nodo è il suo intero sottoalbero, confrontare 2 nodi è molto più dispendioso di XML.

#### JSONPath

***JSONPath*** è un linguaggio di interrogazione per JSON (ispirato ad XPath) e permette di esprimere *path expressions* per JSON.

##### Notazioni e sintassi

Ci sono 2 tipi di notazioni utilizzabili in JSONPath: quella puntata (`$.nodo.array[0]...`) e quella con parentesi (`$['nodo']['array'][0]...`).

Gli operatori fondamentali (che corrispondono più o meno agli assi di XPath) sono:

- `$`: indica il nodo radice (corrisponde a `/` di XPath),
- `@`: indica il nodo corrente (corrisponde a `.` o `self` di XPath),
- `.`: usato per accedere al figlio (corrisponde a `/`, ovvero all'asse `child` di XPath),
- `[]`: usato per accedere agli indici degli array (o per i figli nella notazione con parentesi),
- `*`: indica tutti i nodi figli (***wildcard***),
- `..`: cerca ricorsivamente il sottoalbero (corrisponde a `//`, ovvero all'asse `descendant-or-self` di XPath),
- `?`: usato per filtrare i risultati (usato all'interno di `[]` prima di un'espressione booleana con gli operatori logici),
- `()`: usate per raggruppamenti e precedenze nelle espressioni logiche,
- `&&`, `||`, `!`, `>`, ... `in`: operatori logici.

##### SQL/JSON

Anche JSONPath può essere integrato in SQL con:

- ***JSON publishing***: trasforma dati relazionali in oggetti JSON,
- ***JSON querying***: trasforma oggetti JSON in dati relazionali (con funzioni analoghe a quanto visto per XML: `JSONEXISTS`, `JSONVALUE`, `JSONTABLE`, `JSONQUERY`...).

###### Esempi

Dato il JSON:

```json
{ 
	"negozio": 
	{
	    "libro": [
			{ "titolo": "XPath for Dummies", "prezzo": 10 },
		    { "titolo": "JSONPath Guide", "prezzo": 15 }
	    ],
	    "bici": { "colore": "rosso" }
	}
}
```

Alcuni esempi di espressioni sono:

![](https://i.imgur.com/tIXubjk.png)

Mentre degli esempi di filtri sono:

![](https://i.imgur.com/h4d4Svl.png)

---

Prossima lezione: [[12 - RDF]]

