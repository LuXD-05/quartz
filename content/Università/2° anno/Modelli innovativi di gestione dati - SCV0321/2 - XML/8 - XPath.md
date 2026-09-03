# Lezione 8

### XPath

**XPath** definisce una notazione per <u>identificare e navigare percorsi e sottoalberi di un albero XML</u>. Le espressioni XPath sono costituite da ***[[#Location paths|location paths]]*** (percorsi di locazione), sequenze di nodi detti ***[[#Location steps|location steps]]*** (passi di locazione), ed ogni *location path* viene <u>valutato</u> in base al nodo di partenza che viene chiamato ***context node*** (nodo contesto).

##### Location steps

Ogni *location step* è composto da una struttura del genere `asse::test_di_nodo[predicato_1]...[predicato_n]` con:

- **Asse**: indica in che "*direzione*" andare nell'albero (se considerare i discendenti, i figli, gli attributi... del *context node*),
- **Test di nodo**: indica quali nodi considerare nell'asse specificata,
- **Predicati** (da $0$ a $n$): regole/proprietà che restringono l'insieme dei nodi da considerare.

> [!example] Esempi
> Considerando il seguente albero (con *context node* `collezione`):
> ![](https://i.imgur.com/CeDHyiX.png)
> Alcuni esempi di passi di locazione (da soli potrebbero avere poco senso, vedi poi il percorso) sono:
> - `child::ricetta[attribute::id='117']`: indica tra i figli (del *context node*) chiamati `ricetta` quello con attributo `id` che ha valore `117`.
> - `child::ingrediente`: indica tutti i figli (del *context node*) chiamati `ingrediente`,
> - `attribute::quantità`: indica l'attributo `quantità`.

##### Location paths

Per formare i ***location paths*** si concatenano in un certo ordine dei *location steps* separandoli dal carattere `/` (questo esegue un <u>cambio di contesto</u>, ovvero fa diventare *context node* i nodi che corrispondono allo *step* precedente).

Considerando l'esempio precedente, concatenando i passi in questo modo: `child::ricetta[attribute::id='117'] / child::ingrediente / attribute::quantità` si andrebbe ad ottenere il valore dell'attributo `quantità` dell'`ingrediente` della `ricetta` con `id='177'` (il *path* è risolto <u>in ordine</u>, dal 1° all'ultimo *step*).

> [!important] Nota
> Il risultato delle interrogazioni XPath <u>non</u> è un albero XML, ma un <u>insieme di elementi/attributi/valori</u>, quindi non si possono comporre/concatenare più interrogazioni XPath.

###### Tipi di assi

XPath 1.0 prevede 12 tipi di assi, che (con il *context node* in rosso pieno nelle foto) corrispondono rispettivamente a:

- `child`: figli del *context node* (nota: `child::nome` corrisponde a scrivere solamente `nome` nello step),
- `descendant`: discendenti del *context node*,
- `parent`: padre del *context node* (che è o 1 solo o nessuno se il *context node* è la *root*),
- `ancestor`: antenati del *context node* (padre, padre del padre... fino alla *root*),
- `following`: nodi "dopo" il *context node* in base al ***preorder***,
- `preceding`: nodi "prima" il *context node* in base al ***preorder***, 
- `following-sibling`: nodi fratelli "a destra" del *context node*,
- `preceding-sibling`: nodi fratelli "a sinistra" del *context node*,
- `attribute`: attributi del *context node* (nota: `attribute::nome` = `@nome` nello step),
- `self`: il *context node* stesso,
- `descendant-or-self`: `descendant` + `self` (nota: scrivibile anche con `//`),
- `ancestor-or-self`: `ancestor` + `self`.

> [!info] Graficamente
> Alcuni esempi graficamente sono:
> ![](https://i.imgur.com/zqnJvFz.png)
> Mentre in generale si ha:
> ![](https://i.imgur.com/ZheFSHY.png)
> Diventa chiaro come, mediante gli <u>assi</u>, sia possibile <u>raggiungere qualsiasi nodo di un albero</u> partendo da un *context node* arbitrario.

###### Tipi di test di nodi

I test di nodi filtrano i nodi inclusi nell'asse specificato; e tali filtri includono:

- `[nome]`: include i nodi che si chiamano `nome` (può specificare anche un namespace al posto di `nome`),
- `*`: include tutti i nodi della categoria dell'asse specificato (tutti gli attributi per `attribute`...),
- `text()`: include tutti i nodi contenenti dati testuali.

###### Predicati

Solo una nota: i predicati possono contenere a loro volta altri *location paths*, per esempio:

![687](https://i.imgur.com/yTsgddn.png)

#### XPath 2.0

La versione 2.0 di XPath aggiunge **elementi** ed **espressioni**, permettendo di eseguire <u>computazioni</u> sulle sequenze.

##### Elementi

Gli elementi delle sequenze possono essere:

- **Valori atomici**: numeri, booleani, stringhe e altri tipi di dato definiti nello schema XML,
- **Nodi**: nodi degli alberi XML

> [!tip] Atomizzazione
> L'**atomizzazione** consiste nella conversione da un nodo ad un valore atomico, che ritorna una stringa formata dai valori contenuti nel nodo e nei suoi eventuali sottoelementi.

##### Espressioni

XPath 2.0 prevede vari tipi di **espressioni**:

- **Letterali**: denotano valori atomici,
- **Variabili**: indicate con <u>prefisso</u> `$` (tipo `$var`) che possono riverirsi a diversi valori (non solo atomici),
- **Espressioni aritmetiche**: (tipo `$var + 67`),
- **Espressioni di confronto**: come nei linguaggi di programmazione (tipo `$var > 67`),
- **Espressioni di sequenza**: denotano sequenze costruite concatenando i valori di più espressioni (tipo `exp_1, exp_2 ... exp_n`); in più:
  - `()`:  indica una <u>sequenza vuota</u>,
  - `exp1 to exp2`: indica la sequenza di interi compresi tra quelli risultanti dalle valutazioni di `exp1` ed `exp2`,
- ***Path expressions***: indicano dei *location paths* (importanti anche per altri modelli, tipo quelli basati su grafi),
- **Espressioni filtro**: come i <u>predicati</u> di XPath 1.0 (tipo `exp1[exp2]`) dove `exp1` denota una sequenza ed `exp2` filtra gli elementi della precedente,
- **Espressioni** `if`: selezionano un'espressione in base ad un'altra (tipo: `if (exp1) then exp2 else exp3`),
- **Espressioni** `for`: ciclano gli elementi di un'espressione (usando una variabile come iteratore) per restituire dei risultati (vedi poi l'esempio),
- **Espressioni quantificate**: determinano se alcuni/tutti gli elementi di una sequenza soddisfano una condizione (riscrivibili anche con `for` e `if`); ce ne sono di 2 tipi:
  - `some`: ritorna `true` se <u>almeno 1</u> degli elementi di una sequenza soddisfa un'espressione (tipo: `some $var in exp1 satisfies exp2`),
  - `every`: ritorna `true` se <u>tutti</u> degli elementi di una sequenza soddisfano un'espressione (tipo: `every $var in exp1 satisfies exp2`).

> [!example] Esempio `for`
> L'espressione `for` (riferita all'esempio dell'albero XML precedente): 
> ```
> for $r in //rcp:ricetta
> 	return fn:count($r//rcp:ingrediente[fn:not(rcp:ingrediente)])
> ```
> Interpretata è: "restituisce (per ogni `ricetta` chiamata `$r`) il numero di ingredienti che non hanno sottoingredienti".
> Tale espressione fa uso di 2 **funzioni**:
> - `fn:count()`: che conta il numero di elementi della sequenza passata come argomento,
> - `fn:not()`: uguale all'operazione logica `not`, nell'esempio ritorna `true` se non ci sono ingredienti all'interno degli elementi `ingrediente` della 1a espressione.

---

Prossima lezione: [[9 - XQuery]]

