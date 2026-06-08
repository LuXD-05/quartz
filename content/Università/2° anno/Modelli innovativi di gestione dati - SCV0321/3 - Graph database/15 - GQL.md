# Lezione 15

### GQL

**GQL** (*Graph Query Language*) è un linguaggio di interrogazione basato su *graph pattern*, che implementa la sintassi di **GPML** (*Graph Pattern Matching Language*).

##### Sintassi

Qui (similmente a SPARQL) si identificano nodi e archi con delle espressioni con la seguente sintassi: `(var :label WHERE ...)`, composta da 3 elementi (tutti opzionali):

- `var`: variabile,
- `:label`: indica che i nodi/archi del pattern potranno corrispondere solo a quelli con tale *label* nel grafo,
- `WHERE ...`: condizioni aggiuntive della clausola `WHERE`.

###### USE e RETURN

I primi 2 comandi sono:

- `RETURN`: identico alla `SELECT` SQL,
- `USE`: identico alla `FROM` SQL (non serve se il database si compone di solo 1 grafo).

###### MATCH

La clausola `MATCH` permette di definire un *graph pattern* attraverso delle espressioni chiamate ***path patterns***, a sua volta composta da:

- ***Node patterns***: parti di *path pattern* che rappresentano un <u>nodo</u>, racchiusi tra <u>parentesi tonde</u> `(...)`,
- ***Edge patterns***: parti di *path pattern* che rappresentano un <u>arco</u>, racchiusi da <u>parentesi quadre</u> in una "<u>freccia</u>" direzionabile `-[...]->`.

> [!example] Esempio
> Dal seguente grafo:
> ![](https://i.imgur.com/FKfy5fp.png)
> Si vogliono sempre trovare le coppie di attori che recitano insieme in film con titolo "*Unforgiven*"; quindi il *graph pattern* è:
> ![](https://i.imgur.com/65R3GFa.png)
> Mentre si traduce in GQL così:
> ```cypher
> MATCH TRAIL (x1 :Person) -[:acts_in]-> (:Movie WHERE title == "Unforgiven") <-[:acts_in]- (x2 :Person)
> RETURN x1, x2
> ```
> Per GQL la semantica non è come Cypher (`no-repeated-edge`) ma è manipolabile con delle keyword dopo `MATCH` dette ***path restrictors***:
> - `WALK`: consente ripetizioni di nodi e archi (omomorfismo, default),
> - `TRAIL`: come `no-repeated-edge`,
> - `ACYCLIC`: come `no-repeated-node`,
> - `SIMPLE`: come `no-repeated-anything` (isomorfismo).

##### Quantificatori

Si possono esprimere vincoli sul numero di elementi di un path con i **quantificatori**, che indicano che il pattern a cui sono associati si può ripetere un certo numero di volte:

- `*`: 0 o più volte,
- `+`: 1 o più volte,
- `{n}`: esattamente $n$ volte,
- `{n,m}`: da $n$ a $m$ volte,
- `{n,}`: minimo $n$ volte,
- `{,m}`: massimo $m$ volte.

###### Quantificazione micro-pattern

Di base i quantificatori sono aggiunti <u>dopo</u> un qualsiasi *node/edge pattern* per (appunto) quantificarli. Esempio:

```cypher
MATCH (a) -[t :transfer]->{1,5} (b)
```

Indica che cerca da 1 a 5 archi `:transfer` consecutivi.

> [!important] Multiple variable matching
> La variabile `t` dell'esempio <u>non corrisponde più ad un solo arco</u>, bensì ad un **array** di archi `[t1, t2, ...]`; perciò essa non può essere usata normalmente, ma bisogna usare delle funzioni di aggregazione (come `count(t)` o `sum(t.amount)`...).
> Per esempio, dato il seguente grafo:
> ![](https://i.imgur.com/DKQbngS.png)
> La seguente query (supponendo che gli archi abbiano label `transfer`):
> ```gql
> MATCH TRAIL (x) ( (y) -[:transfer]-> () ){1,} (x)
> RETURN x AS Source, y AS Chain
> ```
> Produrrebbe il seguente risultato:
> ![](https://i.imgur.com/QGkNF9m.png)
> Mostrando che alla variabile `y` sono legate delle <u>liste di nodi</u>.

###### Quantificazione macro-pattern

Si possono anche quantificare più elementi racchiudendoli in blocchi, utile quando tali devono rispettare ulteriori condizioni. Esempio:

```cypher
MATCH (a) ( (:account) -[:transfer]-> ){2,4} (b)
```

> [!warning] Attenzione
> Avendo sempre 2 elementi così:
> ![](https://i.imgur.com/EWiuETi.png)
> Un pattern come il seguente:
> ```cypher
> MATCH (a :account) -[t :transfer]->* (b :account)
> ```
> Rileverebbe un ciclo che risponde con un numero infinito di archi, perciò si usano i *path restrictors* per questo problema, come `TRAIL` e `ACYCLIC`.

##### Working table

La ***working table*** è una tabella nella quale GQL tiene traccia dei risultati intermedi delle query (come per esempio i *matching* delle variabili della query), mentre il grafo correntemente in uso si dice ***working graph***.

> [!example] Esempio
> Dato il seguente multi-grafo:
> ![](https://i.imgur.com/0Qgm7FC.png)
> Supponiamo di eseguire la seguente query:
> ```gql
> USE Fraud {
> 	MATCH (x) -[z:transfer WHERE z.amount > 100]-> (y WHERE w.Blocked == true)
> 	RETURN x.owner AS Sender, y.owner AS Receiver
> 	THEN
> 	USE Social
> 		MATCH (x1) -[:member]-> (z1:yachtClub),
> 			  (x2) -[:member]-> (z1:yachtClub)
> 		FILTER Sender == x1.name AND Receiver == y1.name
> 		RETURN z1.address AS YachtClub
> }
> ```
> Dopo l'esecuzione di `MATCH` relativa al grafo `Social`, la corrispondente *working table* è:
> ![](https://i.imgur.com/NbYetOk.png)
> Che poi per eseguire `FILTER`, verrà fatta la `JOIN` tra la precedente e la *working table* di `Fraud`, ottenendo:
> ![](https://i.imgur.com/5tpce7W.png)

---

