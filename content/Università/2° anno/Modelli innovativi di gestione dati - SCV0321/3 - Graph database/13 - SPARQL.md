# Lezione 13

### SPARQL

RDF/RDFS serializzano in XML, tuttavia per interrogarli non vanno bene linguaggi come XQuery e XPath in quanto non sfruttano le definizioni (sintassi e significato) dei termini RDF/RDFS, perciò e stato definito **SPARQL** (*Sparql Protocol And RDF Query Language*), un linguaggio con sintassi *SQL-like* per interrogare dei grafi specifici.

###### Edge-labelled graphs

SPARQL è usata sul modello dati di RDF, ovvero su ***edge-labelled multigraphs***: dei grafi particolari in cui 1) sia <u>nodi</u> che <u>archi hanno delle</u> ***label*** (<u>etichette</u>) ed 2) è permessa la presenza di <u>archi multipli tra 2 nodi</u>. Per esempio:

![](https://i.imgur.com/wzMzboc.png)

Il motore di interrogazione quindi si basa sul concetto di ***graph pattern matching***.

> [!important] Graph pattern matching
> Un ***graph pattern*** è un'espressione che identifica certi *edge-labelled graphs* facendo uso di **variabili** per le etichette. 
> Un esempio che identifica delle triple (***basic graph pattern***) è: `x insegna MIGD`; da qui il processo di ***matching*** <u>controlla tutte le triple esistenti</u> e <u>seleziona</u> tutte <u>quelle che combaciano</u> con le risorse del *pattern*.

##### Property paths

Con SPARQL 1.1 è possibile scrivere delle **RPQ** (*regular path query*) grazie ai ***property paths***, elementi che permettono di estrarre nodi basandosi su delle *regex*.

Tali elementi sono i seguenti (e indicano che):

- `*`: il predicato si può ripetere <u>0 o più volte</u> nella query,
- `+`: il predicato si può ripetere <u>1 o più volte</u> nella query,
- `?`: il predicato si può ripetere <u>0 o 1 volta</u> nella query,
- `|`: <u>OR logico</u> tra l'elemento prima e quello dopo di questo,
- `/`: <u>concatenazione</u> di 2 elementi (il 1° seguito dal 2°),
- `^`/`!`: (NOT) <u>inverso dell'elemento</u> a cui è associato.

> [!important] Nota
> Si possono sempre usare le `()` per definire precedenze nelle regole.

#### Esempi

I seguenti esempi contengono la solita sintassi SQL con `SELECT`, `FROM` (omissibile, considera il grafo corrente in caso) e `WHERE` (seguito da `{}`), più elementi RDFS e variabili:

###### Query normale

2 query normali sono:

```sparql
# Ritorna tutti i soggetti che appartengono ad una classe
SELECT ?c
WHERE {
	?c rdf:type rdfs:Class .
}
# Ritorna i soggetti istanze della classe "course" di "uni"
SELECT ?x 
WHERE { 
	?x rdf:type uni:course . 
}
```

Nota: se l'engine SPARQL supporta anche RDFS, allora (nelle precedenti query) verranno restituite anche le sottoclassi (per le regole di inferenza RDFS).

###### JOIN implicite

Le seguenti eseguono una `JOIN` implicita tra le triple per ritornare i `lecturer` e i loro `number`:

```sparql
# Ritorna tutti i "lecturer" di "uni" e i loro numeri di telefono
SELECT ?lecturer ?number 
WHERE { 
	?lecturer rdf:type uni:lecturer .  # prende le istanze di uni:lecturer + le lega a ?lecturer
	?lecturer uni:phone ?number .      # dei ?lecturer tiene quelli con predicato uni:phone + ne lega il n° di telefono a ?number
}
# Se Turtle è supportato, si può anche abbreviare così:
SELECT ?lecturer ?number 
WHERE { 
	?lecturer rdf:type uni:lecturer ;
	          uni:phone ?number . 
}
```

###### FILTER

Dal grafo:

![](https://i.imgur.com/5MZlb4T.png)

La clausola `FILTER` si può usare per esprimere `JOIN` esplicite:

```sparql
SELECT ?name
WHERE { 
	?x rdf:type uni:course ;    # ?x = risorse di tipo course 
	   uni:isTaughtBy :12345 .  #    = insegnate dall'elemento denotato con :12345 (sarebbe un prof e 12345 è l'id? boh)
	?c uni:name ?name .         # ?name = risorse (?c) che hanno predicato "uni:name" (?c = "corsi" in teoria)
	FILTER (?c = ?x)            # Filtra e ritorna solo i risultati le cui risorse ci ?c ed ?x corrispondono
}

# Versione con JOIN implicita:
SELECT ?name
WHERE { 
	?x rdf:type uni:course ; 
	   uni:isTaughtBy :12345 ; 
	   uni:name ?name . 
}
```

###### Property paths

Schema:

![](https://i.imgur.com/ziggCAM.png)

Esempi:

```sparql
# /
?x :conosce / :lavoraPer :EvilCorp .
# |
:Alice (:conosce | :odia) ?target .
# ^
:EvilCorp ^:lavoraPer ?dipendente .
# +
:Alice :conosce+ ?conoscenti .
# *
:Alice :conosce* ?persone .
# ?
:Alice :haManager? ?manager .
```

---

Prossima lezione: [[14 - Property graphs]]

