# Lezione 37

### Tipi di cache

#### Direct mapping cache

Le ***direct mapping cache*** (o *a indirizzamento diretto*) contengono $n$ linee numerate da 0 a $n-1$ dette ***entries*** dove ognuna o è vuota o ospita 1 e 1 solo block di RAM; ed è così raffigurata:

##### Struttura direct mapping

Una cache a indirizzamento diretto si divide in 2 parti principali: ***directory*** e ***data***, le quali contengono:

- ***State***: indica lo <u>stato</u> della *entry* (di solito $1$ = valido e $0$ = invalido; all'accensione, dato che la cache è una SRAM, tutte le posizioni sono messe a $0$),
- ***Tag***: contiene parte dell'<u>indice del blocco di RAM</u> che è stato <u>copiato</u> in quella posizione della cache (*tag* di un blocco in RAM $\rightarrow$ *tag* della *entry* di cache),
- ***Data***: contiene il <u>valore del blocco copiato dalla RAM</u>.

![](https://i.imgur.com/rW8c84N.png)

###### Direct mapping cache con blocchi a 1 word

![](https://i.imgur.com/rgmWJMj.png)

###### Direct mapping cache con blocchi a word multiple

![](https://i.imgur.com/toH55HK.png)

##### Funzionamento direct mapping

Quando è richiesto un dato, si cerca di accedere al suo **indirizzo** di memoria, il che è così suddiviso (per la cache):

![](https://i.imgur.com/PCaIXcN.png)

- ***Tag***: sempre parte dell'indice del blocco di RAM copiato in cache,
- ***Index***: è l'indice che indica a quale *entry* di cache accedere (a quale linea),
- ***Offset***: indica i byte di offset da cui partire a prendere prossimo byte.

Quindi quando viene richiesto un dato ad un certo indirizzo, si controlla prima se il blocco a quell'indirizzo è stato copiato in cache; e ciò avviene in questo modo:

1) Si accede alla cache alla riga di indice *index*, se lo *state* = 0 ***cache miss***,
2) Se *state* = 1, si confronta il *tag* dell'indirizzo richiesto con quello alla riga scelta e se non corrispondono allora ***cache miss***,
3) Se invece i *tag* corrispondono, si prendono i bit del blocco in cache dopo l'*offset* e si ha un ***cache hit***.

###### Sinonimi

Ad ogni blocco di cache, anche se ci sta 1 e 1 solo blocco di RAM, possono corrispondere vari blocchi di RAM. Facciamo un esempio:

Abbiamo una cache da <u>4 blocchi</u> ($n_{C}$) e una RAM da <u>16 blocchi</u> ($n_{R}$) da 1 parola.

![](https://i.imgur.com/Rb90N85.png)

Bit necessari per identificare blocchi in cache: $b_{C} = \log_{2}(n_{C}) = 2$,

Bit necessari per identificare blocchi in RAM: $b_{R} = \log_{2}(n_{R}) = 4$,

![](https://i.imgur.com/PV9lYmR.png)

Si notano chiaramente i potenziali ***sinonimi***, ovvero i <u>blocchi di RAM i cui LSB degli indici corrispondono tutti all'indice di un blocco di cache</u>. Il *tag* infatti permette anche di <u>distinguere i vari sinonimi</u> identificando quello contenente il dato richiesto.

Il n° di bit del *tag* di ogni linea di cache è quindi: $b_{tag} = b_{R} - b_{C} = 2$.

Mentre il n° dei blocchi in RAM per blocco in cache è: $2^{b_{tag}}$.

###### Formule

Dati:

- N° blocchi in cache: $n_{C}$,
- N° blocchi in RAM: $n_{R}$,
- N° di word per block: ${} n_{w} {}$,
- Lunghezza di ogni word: $b_{w}$ (in byte),
- ...

Si ha:

- Bit totali in RAM: $n_{R} \cdot n_{w} \cdot b_{w} \cdot 8$ bit,
- ...

##### Prestazioni direct mapping

Analizziamo 2 casi di prestazioni delle cache *direct mapping*:

###### Direct mapping: caso ottimo

In questo caso c'è un programma che accede ciclicamente alle prime 4 locazioni della RAM:

![](https://i.imgur.com/7xsjDfr.png)

Una volta che le locazioni sono state caricate in cache, non si hanno più *cache miss*, quindi non ce nemmeno più bisogno di accedere alla RAM (vantaggio max).

###### Direct mapping: caso pessimo

In questo caso invece c'è un programma che accede ciclicamente alle prime 8 locazioni della RAM:

![](https://i.imgur.com/tMgN5ME.png)

Andando avanti col ciclo si va a sostituire in continuazione il contenuto di tutti i blocchi in cache (quando ce blocco con *tag* $00$ serve quello con $01$ e viceversa) e le prestazioni sono anche peggiori rispetto a quando non si ha una cache.

Per migliorare le prestazioni o si riduce il *miss rate* o la *miss penalty*.

#### Fully associative cache

Un metodo per ridurre il *miss rate* nelle cache è <u>permettere ai blocchi in RAM di poter essere salvati in qualunque posizione della cache</u>. Le cache che implementano questa strategia si dicono ***fully associative cache*** (o *completamente associative*) e in esse non vi sono relazioni fisse tra indirizzi in RAM e posizione in cache:

![](https://i.imgur.com/12agvYD.png)

##### Struttura fully associative

La struttura interna delle cache *fully associative* è molto simile a quella delle cache *[[#Direct mapping cache|direct mapping]]*, eccetto per alcune cose:

- ***Add***: sostituisce il *tag* nella directory e qui corrisponde all'<u>intero indirizzo della locazione in RAM</u> (invece che solo a parte di esso),
- Sono necessari tanti *[[22 - Comparator#Comparator|comparator]]* quanti i blocchi in cache (vedi [[#Funzionamento fully associative|funzionamento]]).

![](https://i.imgur.com/KXnm89D.png)

##### Funzionamento fully associative

Dato che l'indirizzo non è più suddiviso in ***tag***, ***index*** e ***offset***, cercare un dato in cache richiede il confronto di tutti gli *add* in essa con quello da cercare (processo che, grazie ai *[[22 - Comparator#Comparator|comparator]]* replicati, è molto efficiente e il ***cache hit*** qui è pressoché identico a quello con le *[[#Direct mapping cache|direct mapping cache]]*).

Tuttavia in caso di ***cache miss***, se in cache non vi è un blocco vuoto, bisogna sceglierne uno da sostituire in base a una strategia (tipo la **LRU**, *Least Recently Used*).

#### Set-associative cache

Le ***set-associative cache*** sono una <u>combinazione delle precedenti</u> e sono usate per ridurre il <u>conflitto tra sinonimi</u> delle cache *[[#Direct mapping cache|direct mapping]]* e il <u>costo</u> delle cache *[[#Fully associative cache|fully associative]]*.

In pratica si parte da una cache *[[#Direct mapping cache|direct mapping]]* e la si divide in $n$ ***set*** così (es a <u>2 set</u>):

![](https://i.imgur.com/XBdL3dS.png)

Ogni *set* è come se fosse una cache *[[#Direct mapping cache|direct mapping]]* in sé; mentre le linee della cache originale diventano a $n$ blocchi. I blocchi in RAM ***sinonimi*** possono essere memorizzati in un <u>qualsiasi</u> ***set*** della cache, ma sempre <u>sulla stessa linea</u>.

Una cache set-associativa a $n$ *set* si dice *set-associativa a n-vie* (***n-ways set associative***).

##### Struttura set-associative

La struttura semplicemente mostra delle cache *[[#Direct mapping cache|direct mapping]]* moltiplicate per $n$ e collegate con $n$ *[[22 - Comparator#Comparator|comparator]]* come nelle cache *[[#Fully associative cache|fully associative]]*.

In più nella directory è presente la **politica di rimpiazzo** usata per la rispettiva *entry*.

![](https://i.imgur.com/mvHc8M2.png)

###### Set-associative a 4 vie

![](https://i.imgur.com/rO5lKBF.png)

##### Funzionamento set-associative

Le cache *set-associative* scelgono il *set* come col *[[#Direct mapping cache|direct mapping]]*, mentre scelgono il un blocco di un *set* come col *[[#Fully associative cache|fully associative]]*. Si adattano quindi gli indirizzi di memoria per la distinzione dei *set*:

- (***Tag***: sempre l'indice del blocco di RAM copiato in cache),
- ***Index***: l'LSB deve ora essere diviso in 2 parti:
  - ***Set id***: parte dell'*index* adibita ad identificare un ***set*** nella cache,
  - ***Block id***: parte dell'*index* adibita ad identificare un ***block*** in un *set*,
- (***Offset***: indica i byte di offset da cui partire a prendere prossimo byte).

##### Prestazioni set-associative

Date le seguenti configurazioni di cache:

![](https://i.imgur.com/FgyvBcR.png)

Questi sono i *miss rate* in base all'"associatività":

![](https://i.imgur.com/01N3auA.png)

# Esercizi

###### 1) Direct mapping cache

Dati:

- RAM totale = 16 MB,
- Dimensione *word*: 32 bit,
- Dimensione *block*: 512 word,
- Cache totale (esclusi *tag*): 128 KB.

Determinare:

- Bit di un indirizzo di un byte in RAM?
- Bit di un indirizzo di una *word* in RAM?
- N° blocchi in cache?
- N° Blocchi in RAM?
- Bit di tag della cache?

###### 2) Fully associative cache

###### 3) Set-associative cache

Dati:

- RAM totale = 16 MB,
- Dimensione *word*: 32 bit,
- Dimensione *block*: 512 word,
- Cache totale (esclusi *tag*): 64 KB.

Determinare:

- N° di *set* della cache?
- Come scomporre il seguente indirizzo: $101101001111011110001101$?

###### 4) Domande

Rispondere per ogni tipo di cache:

1) In che posizione sono collocati i blocchi copiati dalla RAM?
2) Come sono identificati i blocchi (e quindi confrontati in base a cosa)?
3) Come si decide che blocco sostituire in caso di *cache miss*?
4) Cosa può succedere durante una scrittura in cache?

# Soluzioni

###### 1)

![](https://i.imgur.com/HP42TQw.png)

![](https://i.imgur.com/3RnhFTc.png)

###### 2) 

###### 3)

![](https://i.imgur.com/wPBE0Xk.png)

($2^{3}$ = *set id*, $2^{2}$ = blocks per set)

###### 4)

1\) Dove si collocano i blocchi:

2\) Come si identificano i blocchi:

3\) Quale blocco sostituire:

4\) Cosa succede in scrittura:

---

Prossima lezione: [[38 - Memory Bank]]

