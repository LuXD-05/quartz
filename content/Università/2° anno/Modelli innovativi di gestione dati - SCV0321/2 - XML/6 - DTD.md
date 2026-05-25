# Lezione 6

### DTD

Un **DTD** (*Document Type Definition*) specifica uno schema XML attraverso delle dichiarazioni di elementi che stabiliscono una struttura valida per i nodi degli alberi XML; e tali dichiarazioni hanno la seguente forma: 

`<!ELEMENT nome modello>`

Dove `nome` è il nome dell'elemento e `modello` ne specifica il contenuto.

##### Tipi di modelli di contenuto

Ci sono 4 tipi di modelli di contenuto:

- `EMPTY`: elemento senza figli (ma può avere attributi),
- `ANY`: modelli senza vincoli specifici sul contenuto, quindi ammettono qualsiasi sequenza di caratteri/elementi (utile per elementi non ancora progettati ma vanno poi comunque dichiarati nello schema),
- `Mixed content`: indica che l'elemento può contenere contenuto misto, ovvero un numero qualsiasi di occorrenze di elementi (sintassi: `(#PCDATA | elemento1 | ...)*`, dove `PCDATA` = *parsed character data*, obbligatorio e seguito da 0 o più elementi),
- `Element content`: elemento che può solamente contenere altri elementi (con eventuale specifica di vincoli su ordine e numero di occorrenze con ***regex***).

##### Regex

Una ***regex*** (espressione regolare) descrive una regola che permette di validare una sequenza di caratteri. Le sequenze (stringhe) valide si dice che <u>corrispondono</u> alla regex. 

Dato un alfabeto $\sum\limits$, le regex definite su esso hanno che:

- Ogni simbolo $\sigma \in \sum\limits$, preso da solo, è una regex.
- Se $\alpha$ e $\beta$ sono regex, allora anche:

  ![](https://i.imgur.com/wlpDGMW.png)

> [!info] Nota
> Tipicamente `?`, `*` e `+` hanno precedenza superiore rispetto alla concatenazione (fatta a volte anche con `,`), la quale ha precedenza superiore rispetto a `|`.
> Per esempio, dato l'alfabeto $\sum\limits = \{a,b,c\}$ e la regex `ab*|c`, l'insieme di stringhe valide è: $\{a,ab,ab...b,c\}$.

###### Esempio

Per esempio, l'elemento XHTML `table` è così definito:

`<!ELEMENT table (caption?, (col* | colgroup*), thead?, tfoot?, (tbody+ | tr+))>`.

Un elemento valido secondo tale DTD è:

![](https://i.imgur.com/BgS5XXH.png)

> [!important] Tipi
> I modelli DTD sono un'approssimazione dei tipi di dati rappresentabili; e in XML un tipo di dato corrisponde più o meno alla struttura di un elemento.
> Infatti il precedente elemento `<table>` è un'istanza del tipo `table` specificato col DTD. 

##### Attributi

Per specificare gli attributi che un elemento può avere si usa una dichiarazione `ATTLIST` così:

`<!ATTLIST elemento definizioni>`

Dove `elemento` è l'elemento di riferimento e `definizioni` è una lista di definizioni di attributi; e ogni definizione è formata da 3 componenti:

- `nome`: il nome dell'attributo,
- `tipo`: specifica i possibili valori dell'attributo (più comuni sono `CDATA` o *character data*, che ammette qualsiasi sequenza di char, altrimenti un `enum` che specifica tutte le stringhe ammesse),
- `default`: determina se l'attributo è obbligatorio o facoltativo con 4 possibilità:
  -  `#REQUIRED`: attributo obbligatorio,
  - `#IMPLIED`: attributo opzionale ma senza valore di default,
  - `"..."`: il testo tra le virgolette è il valore di default dell'attributo,
  - `#FIXED` (seguito da `"..."`): implica che l'attributo è opzionale, ma se presente deve avere per forza il valore tra virgolette.

> [!example] Esempio
> Un esempio lo si ha con l'attributo `align` di `p` in XHTML che ha come tipo un'enumerazione ed è opzionale:
> `<!ATTLIST p align (left|center|right|justify) #IMPLIED>`

##### Alberi e serializzazioni

Dato il seguente albero astratto:

![567](https://i.imgur.com/CokfOZ7.png)

E la seguente serializzazione XML:

![439](https://i.imgur.com/gMgIwOO.png)

Ne corrisponde il seguente DTD:

```DTD
<!ELEMENT collezione (descrizione, ricetta*)>
<!ELEMENT ricetta (titolo, ingrediente+)>
<!ELEMENT titolo (#PCDATA)>
<!ELEMENT ingrediente (#PCDATA)>
<!ATTLIST ingrediente
	nome CDATA #REQUIRED
	quantita CDATA #IMPLIED>
```

##### Limitazioni di DTD

DTD ha molte limitazioni e alcune delle principali sono:

- Non ci sono tipi di dato diversi dalle stringhe,
- Non è possibile imporre alcun vincolo ai dati char,
- Non si possono definire dipendenze (un dato c'è se un altro non c'è...),
- *Namespace* non supportati.

---

Prossima lezione: [[7 - XSchema]]

