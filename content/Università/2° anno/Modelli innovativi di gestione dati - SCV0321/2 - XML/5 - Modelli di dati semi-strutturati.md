# Lezione 5

### XML

**XML** (*eXtensible Markup Language*) è un <u>linguaggio di markup</u> (non un modello dati), ovvero un linguaggio che permette di annotare testi/dati con delle annotazioni (dette appunto *markups*) sintatticamente distinguibili dai testi/dati annotati (esempi: HTML, LaTeX...).

I markup di XML sono detti ***tag*** e non sono predefiniti, bensì <u>definiti dall'utente</u> (infatti XML può essere usato per definire HTML con **XHTML**); in più XML (e HTML) derivano da [**SGML**](https://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language) (*Standard Generalized Markup Language*).

> [!important] Modello di dati semi-strutturato
> Per definizione, un **modello di dati semi-strutturato** è la formalizzazione della seguente struttura: un documento XML <u>ben formato</u> è una **serializzazione** di un albero ***labellato*** (con *label*, etichette), **con attributi**, **ordinato** e ***unranked*** (ovvero senza un limite sul numero massimo di figli che ciascun nodo può avere).

#### Caratteristiche

##### Schemi e dati

Considerando XML come uno strumento per la descrizione/annotazione di dati, è possibile trattare i <u>tag</u> come lo **schema** e i <u>dati</u> come le **istanze** di tale schema. La differenza fondamentale è che, al contrario dei modelli relazionale e object-oriented, <u>schema e istanza</u> sono contenuti <u>nello stesso documento</u>.

Esistono poi molti linguaggi per definire schemi XML, tra cui **DTD** e **XSchema**.

###### Sintassi

Si spera tutti sappiano cos'è un XML a sto punto; ma per chi vive sotto una roccia, ecco un'esempio:

![468](https://i.imgur.com/KM0tLak.png)

Scrivibile anche come segue (l'indentazione non importa):

![](https://i.imgur.com/eFaqxCB.png)

Le suddette forme testuali però sono solo delle <u>serializzazioni</u> della struttura (ottenuta scrivendo dati e tag sequenzialmente), la quale è ad **albero**:

![](https://i.imgur.com/2VvMsB6.png)

Inoltre, XML è un linguaggio **semi-strutturato** (e non strutturato) siccome non è obbligatorio specificare sempre tutti i tag. Per esempio si potrebbe omettere completamente il tag `director`, mentre nel modello relazionale, tutti i dati di `director` sarebbero dovuti essere impostati a `NULL`.

##### Attributi

Oltre al nome, i tag XML possono anche avere delle coppie chiave-valore dette **attributi**, tipo:

![301](https://i.imgur.com/98qrQEd.png)

> [!info] Nota
> Rappresentare dati sottoforma di tag o attributi è <u>equivalente</u>:
> ![](https://i.imgur.com/dFmoyBq.png)

#### Modelli di dati

Esistono dei modelli di dati semi-strutturati che derivano da XML e i più noti sono:

##### XPath Data Model

***XPath Data Model*** è un modello dati semi-strutturato ed una implementazione di XML che si presenta come una **struttura ad albero** (con tutte le caratteristiche proprie degli alberi *n*-ari) **ordinata** (l'algoritmo usato per visitarne i nodi è il ***preorder*** da sinistra a destra):

![414](https://i.imgur.com/OZD7EYu.png)

In questo modello, i nodi possono essere di vari tipi:

- `Text`: foglie che contengono dati veri e propri (come "Star Wars"...),
- `Element`: nodi con figli (a meno che tali siano vuoti) aventi un nome (in pratica = tag XML, come *movie*, *title*...),
- `Attribute`: sono gli attributi dell'`element` di cui sono figli (come *id*),
- `Processing`: foglie con info relative all'elaborazione con certi strumenti (tipo CSS...).

> [!info] Nota
> XPath Data Model non considera i nodi `attribute` all'interno dell'elenco dei figli di un elemento, quindi non ne considera l'ordine e il *preorder* li skippa.
> Altri tipi di nodi sono: `document`, `namespace` e `comment`.

###### Serializzazione

I componenti più elementari della serializzazione sono i caratteri Unicode, usati per creare: <u>tag di markup</u> (elementi) e <u>character data</u> (dati veri e propri, ovvero nodi `text`). Ogni elemento serializzato è composto da <u>tag di apertura</u> (`<nome>`) e <u>tag di chiusura</u> (`</nome>`). Ci sono poi 2 caratteristiche principali della serializzazione XML:

- XML è ***case sensitive*** (al contrario tipo di HTML),
- In ogni documento vi è sempre il **prologo**, una riga che contiene info di servizio per i *parser* XML (tipo: `<?xml version="1.0" encoding="UTF-8"?>`).

> [!warning] Attenzione
> Non tutti i documenti XML corrispondono a serializzazioni di alberi XPath; infatti, poiché una serializzazione sia ben formata, è necessario che i tag siano scritti nell'ordine di visita dell'albero. Per esempio:
> ![](https://i.imgur.com/NGMErXK.png)
> È una serializzazione ben formata che corrisponde a:
> ![](https://i.imgur.com/amVvR5b.png)
> Mentre la seguente non lo è:
> ![](https://i.imgur.com/m4kcbyl.png)

###### Namespace

XML mette a disposizione il meccanismo dei ***namespace***: degli **URI** (*Uniform Resource Identifiers*) da aggiungere in testa ai documenti, necessari per poter usare i tag di altri documenti XML in un altro senza creare conflitti di nomenclatura. Per esempio:

![](https://i.imgur.com/53rTydI.png)

Qui si sta dando al namespace di XHTML l'alias `xh` e tale viene usato prima dei tag appartenenti a tale documento (separato da ":") per evitare conflitti di nomi.

##### XML InfoSet

**XML InfoSet** è il modello di riferimento (per il W3C) per i dati semi-strutturati serializzati in XML.

Un ***infoset*** può essere usato per rappresentare un documento XML ben formato ed in esso ogni nodo dell'albero corrisponde (più o meno) ad 1 ***information item***.

Per esempio, dato il documento XML precedente (quello di Star Wars), l'*infoset* corrispondente è:

![522](https://i.imgur.com/3F1eYWz.png)

> [!info] Nota
> L'*infoset* (o l'istanza di XPath Data Model) non è un documento XML ma può essere serializzato in uno, come in altre forme.

###### Tipi di information item

Ci sono 11 tipi di *information items*, e i principali sono:

- **Document info item**: è il padre del *root element* del documento (non è un elemento dell'albero), non presente nella serializzazione e contiene cose come versione XML, codifica dei char e il nodo figlio (*root*).
- **Element info item**: è un elemento nella serializzazione (una copia di tag) le cui proprietà sono: nome elemento, namespace, attributi, *info item* figli e padre.
- **Attribute info item**: è un attributo di un elemento (non considerato in relazioni padre-figlio) le cui proprietà sono: nome, valore ed elemento possessore di tale attributo.
- **Character info item**: è un singolo char di una stringa dati in un nodo.
- **Processing info item**: (come nodi processing dell'XPath Data Model).

> [!info] Nota
> Per questi e per la struttura dell'*infoset*, [[#XPath Data Model]] è considerata un'alternativa migliore e più semplice.

#### Schemi e linguaggi

##### Schema

Per scrivere documenti XML ben formati è necessario che il loro **schema**, ovvero un insieme di regole che ne definiscono la corretta struttura, sia valido.

###### Caratteristiche

L'insieme di termini inclusi e regolati dallo schema (detto **linguaggio**) dovrebbe essere:

- **Espressivo**: capace di descrivere strutture complesse con parti semi-strutturate (elementi opzionali presenti in numero variabile...).
- **Efficiente**: uno ***schema processor*** (software che determina se un documento XML è valido rispetto allo schema) deve poter validarlo efficientemente.
- ***User-friendly***: comprensibile dagli utenti.

##### Linguaggi di specifica e di interrogazione di schemi

Nei prossimi documenti verranno spiegati **DTD** e **XML Schema**, 2 linguaggi principali per la specifica di schemi XML; ed in seguito ***XPath*** e ***XQuery***, altri 2 linguaggi che servono per interrogare gli schemi XML.

---

Prossima lezione: [[6 - DTD]]

