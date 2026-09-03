# Lezione 12

### RDF

I modelli relazionali e semi-strutturati hanno troppi modi diversi per rappresentare informazioni; perciò sono nati i **modelli di dati basati su grafi**, come **RDF** (*Resource Description Framework*): che propone un unico modo per descrivere informazioni.

###### Componenti

RDF presenta vari componenti fondamentali (ognuno identificato da un **URI**):

- **Risorse**: sono le <u>entità</u> (soggetti/oggetti) da rappresentare.
- **Proprietà**: risorse particolari dette anche <u>predicati</u>.
- ***Statements***: <u>espressioni</u> che specificano le proprietà delle risorse.

> [!important] Statements
> Gli ***statements*** sono delle <u>triple</u> formate da `soggetto-predicato-oggetto` (o `oggetto-attributo/proprietà-valore`), ovvero:
> ![](https://i.imgur.com/QlXhcl9.png)
> <u>Soggetto e oggetto degli statement</u> possono anche essere <u>soggetto/oggetto di altri statement</u>, andando quindi a formare la struttura chiamata **grafo RDF**:
> ![](https://i.imgur.com/cWjj1IC.png)

##### RDF/XML

Per usare RDF sono necessarie serializzazioni; e ciò viene con lo standard **RDF/XML** che permette di rappresentare i grafi RDF attraverso documenti XML.

> [!example] Esempio
> Per esempio, lo *statement*: "Mario Rossi è il proprietario di `http://example.org/mrossi`" si serializza in:
> ![](https://i.imgur.com/y1yxUNd.png)
> Dove:
> - `rdf:Description`: è l'intero *statement*,
> - `rdf:about`: è il soggetto,
> - `proprietario`: è il predicato,
> - `http://example.org/mrossi`: è l'oggetto (il contenuto di `proprietario`).

###### Tipi di dati

In RDF/XML il tipo di un dato (se non stringa) deve essere <u>definito con un namespace</u> <u>in un attributo</u> `rdf:datatype`.

> [!example] Esempio
> Per esempio, la serializzazione:
> ![](https://i.imgur.com/BPrBwo0.png)
> Corrisponde allo *statement*: `Mario Rossi ha 27 anni`.

###### Reificazione

La reificazione è una tecnica che permette che l'oggetto di uno *statement* <u>sia a sua volta uno statement</u>; ciò avviene semplicemente considerando uno *statement* come una risorsa singola ed associandogli un URI.

> [!example] Esempio
> Lo *statement*:
> ![](https://i.imgur.com/1ulzAk4.png)
> Può essere reificato come:
> ![](https://i.imgur.com/LXw8MBh.png)

##### Turtle

Siccome RDF/XML è troppo complesso sono nati altri formati di serializzazione, tipo **Turtle** (**TRTL**, *Terse RDF Triple Language*), che rappresenta gli *statement* come triple di URI separate da spazi terminati con `.`.

> [!example] Esempio
> Per esempio lo *statement*:
> ![](https://i.imgur.com/ZSz63lO.png)
> Viene serializzato così: `<[URI]/#spiderman> <[URI]/enemyOf> <[URI]/#green-goblin> .`.

###### Predicate list

Per rappresentare più *statement* con <u>predicati e oggetti diversi</u> ma con <u>soggetto in comune</u>, Turtle permette di indicare 1 sola volta il soggetto seguito da una ***predicate list***: una lista di coppie `predicato-oggetto` separate da `;`.

>[!example] Esempio

>Per esempio, il seguente grafo:

> ![](https://i.imgur.com/MkMQQFD.png)
> Si può rappresentare così:
> ```Turtle
> <[URI]/#spiderman>
> 	<[URI]/enemyOf> <[URI]/#green-goblin> ;
> 	<[URI]/name> "Spiderman" .
> ```

###### Object list

Per rappresentare più statement con stesso soggetto e predicato ma con oggetti diversi, Turtle permette di indicare 1 volta sola la coppia `soggetto-predicato` seguita dai vari oggetti separati da `,`.

>[!example] Esempio

>Per esempio, il seguente grafo:

> ![](https://i.imgur.com/6SslDma.png)
> Si può rappresentare così:
> ```Turtle
> <[URI]/#spiderman> <[URI]/name> 
> 	"Spiderman" ,
> 	"Peter" .
> ```

###### Blank nodes

Per rappresentare risorse che <u>non hanno un URI</u>, si usano i ***blank nodes***, rappresentati con `_`.

>[!example] Esempio

>Per esempio, il seguente grafo:

> ![](https://i.imgur.com/wazXKD7.png)
> Si può rappresentare così:
> ```Turtle
> <[URI]/#pane> <ex:hasIngredient> <_:id1> 
> <_:id1>
> 	<ex:ingredient> <ex:#farina> ;
> 	<ex:amount> "1kg" .
> ```

#### RDFS

Dato che RDF è un modello troppo "generale" (descrive relazioni tra singole entità), è nato ***RDF Schema*** (o **RDFS**): una restrizione di RDF che (oltre a descrivere relazioni tra <u>insiemi</u> di entità), associa alle relazioni dei significati (tipo **appartenenza** ($\in$) e **inclusione** ($\subseteq$)).

> [!example] Esempio
> Un esempio di RDF/RDFS è il seguente grafo:
> ![](https://i.imgur.com/YzSlTii.png)
> In questo:
> - `type`: questo predicato denota una relazione di **appartenenza** ($\in$), per esempio tra `AT` e la <u>classe</u> `professor`.
> - `subClassOf`: questo invece denota una relazione di **inclusione** ($\subseteq$), per esempio tra la <u>sottoclasse</u> `professor` e la classe `academic staff`.

##### Componenti principali

###### Classi

Alcune delle **classi** RDFS principali sono:

- `rdfs:Resource`: classe di ogni risorsa,
- `rdfs:Class`: classe di tutte le classi,
- `rdfs:Literal`: classe dei letterali (stringhe),
- `rdfs:Property`: classe di tutte le proprietà.

###### Proprietà

Alcune delle **proprietà** RDFS principali invece sono:

- `rdfs:type`: indica che un elemento (risorsa) <u>appartiene</u> ad una certa classe ($\in$),
- `rdfs:subClassOf`: indica che una classe <u>eredita</u> da un'altra ($\subseteq$),
- `rdfs:subPropertyOf`: indica che una proprietà <u>eredita</u> da un'altra ($\subseteq$),
- `rdfs:domain`: specifica il <u>dominio</u> di una proprietà (ovvero la classe **soggetto** di un predicato),
- `rdfs:range`: specifica il <u>codominio</u> di una proprietà (ovvero la classe **oggetto** di un predicato).

##### Regole di inferenza

In RDFS ci sono delle **regole** chiamate **di inferenza** che permettono di derivare triple a partire da quelle già presenti, per esempio:

- Se `u subClassOf v` e `v subClassOf w` allora `u subClassOf w`,
- Se `i type v` e `v subClassOf w` allora `i type w`.

> [!info] Confronto con logica
> Tali regole deduttive sono molto simili ai costrutti di **deduzione** della logica di 1° ordine, che si esprimono così:
> $$\dfrac{s_{1}, \ldots s_{n}}{s}$$
> Che si traduce in: "se gli *statement* $s_{1}, \ldots s_{n}$ sono veri, allora anche lo *statement* $s$ lo è".

###### Esempi

Implicazione semplice: "se soggetto `S` è in relazione con oggetto `O` tramite predicato `P`, allora esiste una risorsa `_:n` in relazione con `S` tramite il predicato `P`".

$$\dfrac{S \;\; P \;\; O}{S \;\; P \;\; \_:n}$$

"Se vale lo statement `S P O`, allora `P` è un predicato (proprietà)":

$$\dfrac{S \;\; P \;\; O}{P \;\; \text{rdf:type} \;\; \text{rdf:Property}}$$

"Se `P` è una proprietà, allora è anche una risorsa":

$$\dfrac{\dfrac{S \;\; P \;\; O}{P \;\; \text{rdf:type} \;\; \text{rdf:Property}}}{P \;\; \text{rdf:type} \;\; \text{rdf:Resource}}$$

###### Limiti delle deduzioni

Le deduzioni in RDFS hanno comunque dei limiti:

- Non è possibile esprimere la **negazione** di uno *statement* (seppur è approssimabile così: `Luca rdf:type NonSmoker`).
- Non si possono **derivare inconsistenze dalle triple** (avendo `Luca rdf:type Smoker` e `Luca rdf:type NonSmoker` non è possibile specificare che le classi `Smoker` e `NonSmoker` non hanno elementi comuni).

> [!important] Statement non esprimibili
> Ci sono degli statement non esprimibili in RDFS (risolti poi con [[#OWL]]), tra cui:
> - Ogni progetto ha almeno 1 partecipante,
> - Ogni progetto o è un progetto o è un progetto interno (disgiunzione esclusiva, non può essere entrambi o nessuno dei 2),
> - Il superiore del superiore di un professore è anche superiore di tale professore.

#### OWL

**OWL** (*Web Ontology Language*) è uno standard W3C creato per **bilanciare** il <u>potere espressivo di RDFS</u> con l'<u>efficienza delle regole di deduzione</u> (dato che alcuni concetti logici erano impossibili da esprimere in RDFS); e ne derivano 3 linguaggi che vanno da quello con <u>maggiore potere espressivo</u> a quello <u>più efficiente</u>: **OWL *full***, **OWL DL** e **OWL *lite***.

##### Classi

OWL presenta 3 classi fondamentali:

- `owl:Thing`: classe più generale, ogni cosa appartiene ad essa,
- `owl:Nothing`: classe vuota,
- `owl:Class`: classe che contiene tutte le altre classi definibili.

###### Classi chiuse

OWL *lite* permette di definire **classi chiuse**, ovvero classi le cui istanze sono unicamente quelle che vengono definite al loro interno, che vengono definite con `owl:oneOf`.

> [!example] Esempio
> Nel seguente esempio, si hanno le classi `A` e `B` che sono le uniche che possono appartenere alla classe chiusa `PhD`:
> ```xml
> <owl:class rdf:about="PhD">
> <owl:oneOf rdf:parseType="Collection">
> 	<Person rdf:about="A"/>
> 	<Person rdf:about="B"/>
> </owl:oneOf>
> </owl:class>
> ```

###### Costruttori booleani

Sempre in OWL *lite* è possibile usare dei **costruttori booleani** per calcolare delle <u>classi complesse</u> <u>combinando più classi atomiche</u>:

- `owl:intersectionOf`: intersezione (AND logico),
- `owl:unionOf`: unione (OR logico),
- `owl:complementOf`: complemento (NOT logico).

##### Ruoli

In OWL le proprietà si chiamano anche **ruoli** e si dividono in 2 tipi:

###### Concreti

I **ruoli concreti** mettono in relazione delle <u>risorse con valori letterali o dati puri</u>; e sono specificati con `owl:DatatypeProperty`. Per esempio, data una classe `Person`, si ha:

```xml
<owl:DatatypeProperty rdf:about="#yearsOld">              <!-- DatatypeProperty = ruolo concreto -->
	<rdfs:domain rdf:resource="#Person"/>                 <!-- domain = dominio (soggetto), qui istanze di #Person -->
	<rdfs:range rdf:resource="http://www.w3.org/int"/>    <!-- range = codominio (oggetto), qui indica un integer -->
</owl:DatatypeProperty>
```

###### Astratti

I **ruoli astratti** invece relazionano <u>risorse con altre risorse</u>; e sono specificati con `owl:ObjectProperty`. Per esempio, date classi `Person` e `Book`, si ha:

```xml
<owl:ObjectProperty rdf:about="#reads">      <!-- ObjectProperty = ruolo astratto -->
	<rdfs:domain rdf:resource="#Person"/>    <!-- domain = dominio (soggetto), qui istanze di #Person -->
	<rdfs:range rdf:resource="#Book"/>       <!-- range = codominio (oggetto), qui istanze di #Book -->
</owl:DatatypeProperty>
```

> [!important] Ruoli astratti particolari
> Alcuni ruoli astratti aumentano il potere espressivo di OWL, per esempio:
> - `owl:disjointWith`: indica che 2 classi (soggetto e oggetto) sono <u>mutuamente esclusive</u> (un elemento non può appartenere a entrambe),
> - `owl:equivalentClass`: indica che 2 classi contengono esattamente le stesse istanze,
>   `owl:sameAs`: indica che 2 classi hanno lo stesso significato (come se fossero lo stesso oggetto).

##### Quantificazione

Con i **quantificatori** è possibile applicare delle restrizioni alle classi; e ciò lo si fa con il tag `owl:Restriction` (che crea una <u>classe anonima</u>) in cui vengono descritte regole (<u>che limitano il comportamento di certi ruoli</u> con `owl:onProperty`) da applicare ad altre classi (attraverso `rdfs:subClassOf`).

###### Universale

La **quantificazione universale** avviene con `owl:allValuesFrom` e specifica che <u>tutti gli oggetti di una certa relazione devono essere istanze di una certa classe</u>. Esempio:

```xml
<owl:Class rdf:about="#Exam">
	<rdfs:subClassOf>
		<owl:Restriction>                                     <!-- Restrizione della classe #Exam (in subClassOf) -->    
			<owl:onProperty rdf:resource="#hasExaminer"/>     <!-- Vincolo sul ruolo #hasExaminer --> 
			<owl:allValuesFrom rdf:resource="#Professor"/>    <!-- Tutti gli oggetti di #hasExaminer devono essere #Professor --> 
		</owl:Restriction>
	</rdfs:subClassOf>
</owl:Class>
```

###### Esistenziale

La **quantificazione esistenziale** avviene con `owl:someValuesFrom` e specifica che <u>almeno 1 oggetto di una relazione deve essere istanza di una certa classe</u>. Esempio:

```xml
<owl:Class rdf:about="#Exam">
	<rdfs:subClassOf>
		<owl:Restriction>                                      <!-- Restrizione della classe #Exam (in subClassOf) -->    
			<owl:onProperty rdf:resource="#hasExaminer"/>      <!-- Vincolo sul ruolo #hasExaminer --> 
			<owl:someValuesFrom rdf:resource="#Professor"/>    <!-- Almeno 1 oggetto di #hasExaminer deve essere #Professor --> 
		</owl:Restriction>
	</rdfs:subClassOf>
</owl:Class>
```

##### Deduzioni

Per interrogare una repository di triple OWL, i tipi di deduzioni più usate sono 3:

- **Classificazione dell'ontologia**: calcolo di tutte le gerarchie e sottoclassi dell'ontologia (relazioni `subClassOf` tra classi atomiche),
- **Consistenza dell'ontologia**: validazione delle ontologie e controlli per eventuali contraddizioni,
- ***Instance retrieval***: ricerca di tutte le istanze appartenenti ad una classe complessa.

> [!info] Complessità computazionale OWL
> ![](https://i.imgur.com/ddUCI0P.png)

---

Prossima lezione: [[13 - SPARQL]]

