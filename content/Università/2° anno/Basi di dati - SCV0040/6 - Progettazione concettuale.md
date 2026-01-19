# Lezione 6

### Modello ER

Il modello **ER** (*entity-relationship*) serve per modellare schemi concettuali per mezzo di **diagrammi ER**, che sono composti da:

##### Entità

Un'**entità** rappresenta una collezione di oggetti appartenenti al contesto da modellare con certe caratteristiche comuni; gli specifici oggetti modellati da esse si dicono **istanze di entità**. Graficamente:

![](https://i.imgur.com/6hvwTT4.png)

##### Associazioni

Un'associazione è un legame logico tra più entità (spesso identifica un'azione) le cui istanze sono combinazioni di istanze di entità associate. Graficamente:

![](https://i.imgur.com/bpZ95FD.png)

(L'insieme delle istanze di un'associazione è un sottoinsieme del **prodotto cartesiano** degli insiemi di istanze di entità coinvolte; perciò, dato che tale insieme non può contenere duplicati, non tutti i legami logici tra entità possono essere modellati correttamente come associazioni).

> [!info] Nota
> Le stesse entità possono essere coinvolte in più relazioni tra loro:
> ![](https://i.imgur.com/R52OgIA.png)

###### Grado

Le associazioni indicano quante relazioni sono coinvolte in esse attraverso il loro **grado**:

- Associazioni unarie (grado 1), modellano associazioni ricorsive:

  ![](https://i.imgur.com/NTxEYEH.png)

- Associazioni binarie (grado 2), le più comuni:

  ![](https://i.imgur.com/vnvXSYt.png)

- Associazioni *n-arie* (grado > 2), più rare (e da risolvere):

  ![](https://i.imgur.com/yCDCbpU.png)

###### Ruolo

Il **ruolo** delle associazioni indica la funzione che un'entità esercita in un'associazione:

![](https://i.imgur.com/rFyVwvq.png)

<u>Sempre necessario nelle associazioni unarie</u>.

###### Cardinalità delle associazioni

(Leggere prima [[#Cardinalità degli attributi]] siccome il concetto è lo stesso). Oltre agli attributi, anche le associazioni possono avere cardinalità; e tale indica il n° minimo e massimo di istanze dell'associazione a cui un'istanza dell'entità coinvolta può partecipare ("Quante `<entità1>` possono `<associazione>` l'`<entità2>` e viceversa?").

Graficamente ciò si indica ponendo la cardinalità ($c_{min},c_{max}$) sulla linea che congiunge l'entità all'associazione:

![](https://i.imgur.com/g66xZgv.png)

(Nell'esempio, un cliente può noleggiare da 0 a 3 video alla volta mentre un video può essere noleggiato o meno).

Negli ER, se omesse, le cardinalità assumono di default il valore $(0,n)$.

> [!important] Classificazione delle associazioni
> Le **associazioni binarie**, in base alla loro cardinalità, possono essere classificate in 3 gruppi diversi rappresentati dalla seguente tabella:
> ![](https://i.imgur.com/9yyk5jJ.png)

##### Attributi

Gli attributi sono le <u>proprietà di un'entità o associazione</u>, graficamente:

![](https://i.imgur.com/mPPgqFb.png)

> [!info] Attributi composti
> Gli attributi possono essere semplici oppure composti; questi ultimi sono formati da sotto-attributi ognuno con una sua cardinalità e che può essere a sua volta composto. Graficamente:
> ![](https://i.imgur.com/PmqX658.png)

###### Cardinalità degli attributi

In base al n° di valori che possono assumere, gli attributi si dividono in: **mono-valore** e **multi-valore**; inoltre essi possono essere **opzionali** (possono assumere valori `NULL`) o **obbligatori** (non possono assumere valori `NULL`).

Entrambe queste classificazioni possono essere espresse con **vincoli di cardinalità** per attributi, che indicano il <u>n° minimo e massimo di valori che l'attributo può assumere</u>:

- **Cardinalità minima** ($c_{min}$): $0$ per attributi **opzionali** e $1$ (o più) per attributi **obbligatori**,
- **Cardinalità massima**($c_{max}$): $1$ per attributi **mono-valore** e $n$ (o un numero specifico > 1) per quelli **multi-valore**.

> [!example] Nota
> La seguente tabella rappresenta la cardinalità degli attributi:
> ![](https://i.imgur.com/4JXSIbz.png)
> Il valore di default della cardinalità ($c_{min},c_{max}$) è (1,1) se omessa.

###### Domini

Il **dominio** di un'attributo è l'<u>insieme dei valori che esso può assumere</u> e si distinguono in:

- **Domini standard**: tipo `int`, `float`, `date`, `string`...
- **Intervalli**: indicati con la notazione $[x, y]$ (con ${} x$ valore iniziale e $y$ finale),
- **Insiemi di valori**: insiemi di valori per un certo dominio $d$ indicato con `set_of(`$d$`)` (per attributi multi-valore),
- **Enum**: domini di enumerazione definiti dall'utente e indicati con la notazione $\{x_{1}, \ldots x_{n}\}$.
- ***Domini composti***: usati per <u>attributi composti</u> e fatti dal <u>prodotto cartesiano dei domini dei sotto-attributi</u>, indicato con $D = D_{1} \times \ldots \times D_{n}$.

> [!important] Nota
> Comunque, negli ER <u>non si specificano direttamente i domini degli attributi</u> e <u>neanche la loro cardinalità</u>.

#### Vincoli di identificazione

Un **identificatore** (***id***) per un'entità è un'<u>insieme di attributi</u> che <u>identifica univocamente ogni istanza di tale entità</u> (quindi ogni istanza avrà un valore <u>univoco</u> per quell'insieme di attributi). Inoltre, le <u>associazioni</u> (generalmente) <u>non necessitano di id</u> in quanto <u>tutte le loro istanze sono già distinte</u>.

Di questi ***id*** se ne cercano vari (gruppi) nelle entità, ma solo dopo con la <u>progettazione logica</u> si andrà a sceglierne uno ***minimale*** che corrisponderà alla [[2 - Modello relazionale#PK|PK]] (o *primary key*).

> [!important] Minimalità
> Le PK devono essere **minimali**, nel senso che <u>devono comprendere il n° minimo di attributi all'interno della chiave</u> (possibilmente 1 solo). Per questo (in molti casi) è meglio introdurre un attributo PK chiamato `id` invece di cercare la combinazione più minimale degli attributi già esistenti (anche perché poi si rischiano problemi e sprechi di memoria con associazioni e FK).

###### Entità deboli

Un'entità si dice **debole** quando non è identificabile solamente attraverso i suoi attributi ma necessita info da altre entità associate. Per esempio, per modellare più studenti di più università non si può usare la matricola come PK perché potrebbe essere duplicata, perciò si usa una combinazione di matricola e id dell'università per avere un identificatore univoco per ogni studente.

Per queste entità:

- La <u>cardinalità dell'entità debole è sempre (1,1)</u>,
- (Siccome) se $c_{min} = 0$, sarebbero ammesse istanze dell'entità non partecipanti all'associazione e quindi <u>non identificabili</u> (studente che studia in 0 università),
- (Siccome) se $c_{max} > 1$, ci sarebbero istanze dell'entità partecipanti più volte all'associazione e quindi <u>associazioni ambigue</u> (studente che studia in più università).

> [!info] In realtà
> Questa (immagino) sia un caso specifico in progettazione concettuale, in quanto basterebbe usare un campo `id` univoco per studente e un altro per università ed avere una tabella intermedia tra i 2, in modo tale che l'associazione diventi `N-N` senza le suddette restrizioni.

##### Tipi di identificatori

Un'identificatore può essere **semplice** (se contiene un solo attributo) o **composto** (se ne contiene di più); poi può essere **interno** (se formato da 1 o più attributi dell'entità), **esterno** (se costituito da 1 o più attributi di altre entità associate) o **misto** (con attributi dell'entità e di entità associate). Esempi:

![](https://i.imgur.com/83jaVdC.png)

Come si può vedere, l'id o chiave si indica con il pallino pieno.

#### Gerarchie di generalizzazione

Un'entità $E$ è una **generalizzazione** di altre entità $E_{1}, \ldots E_{n}$ se ogni istanza di queste è anche un'istanza di $E$. Questa è la solita **ereditarietà**, quindi $E$ si dice **padre** mentre le altre entità $E_{1}, \ldots E_{n}$ sono delle **specializzazioni** di $E$, si dicono **figli** ed ereditano tutte le proprietà del padre (attributi, id, associazioni...) consentendo l'aggiunta di ulteriori attributi specializzati ma non il cambio di id.

![](https://i.imgur.com/9wZZFOr.png)

> [!important] Vincoli impliciti
> Tra 2 entità 1 padre e l'altra sua figlia ci sono dei vincoli impliciti:
> - Non ci possono essere più istanze nella figlia che nel padre,
> - Ogni attributo del padre deve essere anche attributo della figlia,
> - Ad ogni associazione a cui il padre partecipa deve parteciparvi anche la figlia.

##### Tipi di generalizzazione

Una gerarchia di generalizzazione può essere distinta in base a 2 criteri:

###### Completezza

Indica il n° <u>minimo</u> di istanze dell'entità nell'associazione:

- **Totale**: <u>ogni istanza del padre è istanza anche di almeno 1 figlio</u> (se clienti standard e VIP sono gli unici tipi di clienti),
- **Parziale**: ci sono <u>istanze del padre che non sono istanze di alcun figlio</u> (clienti che non pagano per fidelizzazione né standard né VIP).

###### Disgiunzione

Indica il n° <u>massimo</u> di istanze dell'entità nell'associazione:

- **Esclusiva**: <u>ogni istanza del padre è al massimo 1 e 1 sola istanza di un figlio</u> (cliente è o standard o VIP),
- **Condivisa**: <u>ogni istanza del padre può essere istanza di più figli</u> (un libro può essere sia storico sia romanzo).

###### Particolarità

Da notare la corrispondenza con la [[#Cardinalità degli attributi|cardinalità]]:

![](https://i.imgur.com/XH4sdts.png)

> [!info] Associazione di sottoinsieme
> Vi è un caso particolare di una <u>generalizzazione parziale esclusiva</u> con 1 solo figlio che si dice **associazione di sottoinsieme**:
> ![](https://i.imgur.com/zTEx5rJ.png)
> Essa significa che le istanze dell'entità figlia sono un sottoinsieme di quelle del padre.
> Nota: questa generalizzazione ha senso solo così in quanto, con 1 solo figlio non può essere condivisa, mentre se fosse totale sarebbe come definire una singola entità.

---

Prossima lezione: [[7 - Progettazione logica]]

