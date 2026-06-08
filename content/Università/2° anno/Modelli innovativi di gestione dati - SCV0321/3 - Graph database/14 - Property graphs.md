# Lezione 14

### Property graphs

I linguaggi di interrogazione per modelli basati su grafi si basano su 2 concetti che, per RDF, si applicano agli ***edge-labelled multigraphs*: ***path expressions*** (tipo "trovare i path più corti tra 2 attori") e ***graph patterns*** (tipo "trovare tutte le coppie di attori che hanno recitato insieme in un certo intervallo temporale").

Per aggiungere dati agli *edge-labelled multigraphs* bisogna per forza espanderli (inefficiente); perciò sono nati i ***property graphs***: grafi i cui nodi e archi, oltre ad essere identificati univocamente da una label, hanno associato un insieme di coppie chiave-valore (coppie dette **attributi *property-value***).

Tale approccio permette di annotare il grafo senza modificarne la struttura; ed un esempio è:

![](https://i.imgur.com/hfVYk0o.png)

> [!info] Nota
> I *property graphs* hanno 2 caratteristiche base: 1) ogni nodo e ogni arco hanno una sola label e 2) ogni proprietà ha un solo valore. Rimuovendo tali vincoli si ha invece un ***knowledge graph*** (non definito formalmente).

##### Matching e patterns

Come visto per gli *[[13 - SPARQL#Edge-labelled graphs|edge-labelled multigraphs]]*, è possibile eseguire il ***matching*** di un *graph pattern* anche su un ***property graph*** al fine di interrogarlo. Si distinguono poi 2 tipi di *graph pattern* utilizzabili:

- ***Basic graph pattern*** (*BGP*): pattern di grafi nei quali al posto delle <u>label</u> (o delle <u>proprietà</u> per *property graphs*) possono comparire **variabili**,
- ***Complex graph pattern*** (*CGP*): pattern costruiti a partire da altri *BGP* mediante operazioni come proiezioni, unioni, join...

#### BGP

##### BGP matching

Un ***match*** tra un grafo (*edge-labelled* o *property*) $G = (N,E)$ ed un *BGP* ${} Q = (N', E') {}$ (dove $N'$ ed $E'$ possono contenere variabili invece di costanti) è un mapping:

$$f \,:\, \text{Consts} \,\cup\, \text{Vars} \,\rightarrow\, \text{Consts}$$

Tale che:

1) <u>Ogni costante è mappata a se stessa</u> ($\;\forall a \in \text{Consts} \rightarrow f(a) = a\;$),
2) Per l'arco (<u>arco + nodi</u> che collega) del *BGP* $(x, e, y) \in E'$ si ha che l'<u>arco mappato</u> $(f(x), f(e), f(y)) \in E$ <u>appartiene al grafo</u> $G$:

   ![](https://i.imgur.com/57PgNNs.png).

> [!important] Implicazioni
> Per il 2° punto, ogni arco di $Q$ è mappato in un arco di $G$. Di conseguenza, mappando $Q$ con le costanti e variabili di $G$, il risultato è un sottografo di $G$.
> Per i *property graph*, oltre alle <u>label di nodi e archi</u>, **costanti e variabili** possono essere: gli <u>identificatori di nodi e archi</u> o anche <u>le proprietà coi loro valori</u>.
> ![](https://i.imgur.com/JDRlyvq.png)

###### Omomorfismi e isomorfismi

Un *mapping* che soddisfa entrambi i precedenti [[#BGP matching|punti]], si dice **omomorfismo**; mentre un **isomorfismo** è il medesimo ma col vincolo di dover mappare variabili diverse di $Q$ su nodi/archi diversi di $G$. **SPARQL** si basa su omomorfismi, mentre i linguaggi basati su isomorfismi si distinguono in 3 **semantiche** diverse:

- `no-repeated-anything`: <u>variabili diverse</u> di $Q$ vanno <u>mappate su nodi/archi diversi</u> di $G$,
- `no-repeated-node`: ogni <u>variabile "nodo"</u> di $Q$ va <u>mappata su un nodo</u> di $G$ (mentre più <u>variabili "arco"</u> di $Q$ possono essere <u>legate allo stesso arco</u> di $G$),
- `no-repeated-edge`: ogni <u>variabile "arco"</u> di $Q$ va <u>mappata su un arco</u> di $G$ (mentre più <u>variabili "nodo"</u> di $Q$ possono essere <u>legate allo stesso nodo</u> di $G$).

##### Esempi

###### Esempio edge-labelled multigraph

Dato $G$ il seguente *edge-labelled multigraph*:

![](https://i.imgur.com/3rDUI3v.png)

Si vogliono "trovare tutte le coppie di attori che recitano nello stesso film"; e il *BGP* $Q$ che corrisponde a tale query è:

![](https://i.imgur.com/lmtQQu0.png)

Quindi il risultato $Q(G)$ sarà:

![](https://i.imgur.com/T58axd4.png)

> [!info] Nota
> Le ultime 2 righe della tabella sono identificate quando si cerca di mappare lo stesso attore in $x_{1}$ e $x_{2}$; ed in certi sistemi ciò è permesso (anche per il fatto che la query prevedeva di trovare coppie della stessa entità). Proprio perché tali sono permesse, questo è un'**[[#Omomorfismi e isomorfismi|omomorfismo]]**.

###### Esempio property graph

Dato $G$ il seguente *property graph*:

![567](https://i.imgur.com/Ga7yCPe.png)

Si vogliono "trovare tutti i post che piacciono a coppie di amici (ed estrarre varie info dai risultati)"; e il *BGP* $Q$ che corrisponde a tale query è:

![419](https://i.imgur.com/VcPTyKd.png)

Quindi il risultato ${} Q(G)$ sarà:

![](https://i.imgur.com/wVaJtnn.png)

(Vengono inclusi nella risposta solo match corrispondenti a sottografi presenti in $G$).

#### CGP

I ***CGP*** (*Complex Graph Pattern*) sono pattern costruiti a partire da dei *BGP* attraverso vari operatori, fra cui:

- Proiezione: come la `SELECT` di SQL,
- Unione: come `UNION` di SQL (?),
- *Filter*: come la `WHERE` di SQL (filtra i risultati con predicati di selezione e connettivi come congiunzione, disgiunzione, negazione...),
- *Join*: simile a una `JOIN` SQL ma meno immediata su grafi, il seguente esempio illustra una `JOIN` con condizione `z = w` in modo chiaro:

  ![](https://i.imgur.com/Kis5zGJ.png)

##### Esempio

Dato il seguente *edge-labelled graph*:

![](https://i.imgur.com/o8uhkNx.png)

Si vogliono trovare tutte le coppie di attori che recitano nei film con titolo "*Unforgiven*"; perciò il *BGP* corrispondente è:

![](https://i.imgur.com/uC56qsE.png)

E tradotto in query SPARQL diventa:

```sparql
SELECT ?x1 ?x2 
WHERE {
	?x1 :acts_in ?x3 ;         # x1 = risorsa di tipo Person con predicato "acts_in" verso x3
	:type :Person .
	?x2 :acts_in ?x3 ;         # x2 = risorsa di tipo Person con predicato "acts_in" verso x3
	:type :Person .
	?x3 :title "Unforgiven" ;  # x3 = risorsa di tipo Movie con title = "Unforgiven"
	:type :Movie .
}
```

> [!info] Nota
> Dato che SPARQL si basa su **omomorfismi**, verranno restituite anche le coppie in cui è presente lo stesso attore 2 volte; perciò, se si vogliono escludere, bisogna farlo esplicitamente con la clausola `FILTER`:
> ```sparql
> SELECT ?x1 ?x2 
> WHERE {
> 	?x1 :acts_in ?x3 ;
> 	:type :Person .
> 	?x2 :acts_in ?x3 ;
> 	:type :Person .
> 	?x3 :title "Unforgiven" ;
> 	:type :Movie .
> 	FILTER (?x1 != ?x2)
> }
> ```

---

Prossima lezione: [[15 - GQL]]

