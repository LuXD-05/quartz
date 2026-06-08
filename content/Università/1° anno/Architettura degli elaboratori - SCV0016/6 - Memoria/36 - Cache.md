# Lezione 36

### Cache

La ***cache*** è un buffer di memoria statica che in prestazioni e grandezza (dimensioni da KB a MB) si colloca tra i registri e la RAM. Essa è integrata nelle CPU cosicché non vi scambi dati attraverso il bus esterno, per una maggiore efficienza.

Con essa vi è anche il ***gestore della cache***, circuiti di controllo che ne gestiscono il funzionamento.

###### Scopo

Il suo scopo principale è recuperare e fornire velocemente dati e programmi che si prevede debbano essere utilizzati nel breve termine. La previsione di questi è fatta secondo i **principi di località**.

> [!important] Principi di località
> I **principi di località** sono degli assiomi che definiscono la probabilità che un certo dato venga richiesto nel breve termine per eseguire certi calcoli; e sono 2:
> - **Località temporale**: se un dato viene letto o scritto in un certo istante è probabile che nel breve termine <u>verrà richiesto altre volte</u>.
> - **Località spaziale**: se un dato viene letto o scritto in un certo istante è probabile che entro breve <u>vengano richiesti anche i dati nelle celle di memoria vicine</u>.

##### Funzionamento

Quando la CPU richiede l'accesso in lettura ad un dato, la sua ricerca inizia in cache e vi sono quindi 2 casi possibili:

- "***Cache hit***": ovvero in caso di <u>successo della ricerca</u> (del dato in cache), il <u>dato è fornito alla CPU</u> immediatamente,
- "***Cache miss***": ovvero in caso di <u>fallimento della ricerca</u> in cache, essa <u>prosegue nel livello inferiore</u>.

  Il dato ottenuto è <u>copiato in cache</u> anche eventualmente scartandone altri in base ad una certa strategia (*località temporale*); inoltre spesso vengono anche <u>copiati dati in celle vicine</u> a quella del dato richiesto (*località spaziale*).

###### Read miss strategies

Quando si cerca di leggere un dato in cache ed esso non vi è presente, si va a ricercare il blocco corrispondente in RAM, lo si copia in cache e lo si rilegge (comunque intanto la CPU è in stallo per quel tempo). Questo procedimento si fa secondo 2 strategie:

- ***Read back***: prima si carica il blocco interamente in cache, poi lo si legge da lì,
- ***Load through***: il blocco viene restituito alla CPU e in contemporanea copiato in cache (***early restart*** invece dà la priorità a mandare il blocco alla CPU, poi copia).

###### Write hit strategies

I blocchi in cache possono anche essere modificati (se sono presenti, non se ne può creare uno da 0 perché la cache contiene blocchi di RAM). Quando si scrive un blocco in cache si fa secondo 2 strategie:

- ***Write-through***: scrittura del dato <u>sia in cache che in RAM in contemporanea</u> (semplice da implementare ma poco efficiente con aggiornamenti ripetitivi),
- ***Write-back***: scrittura del dato <u>solo in cache</u>, in RAM sarà fatta quando quel blocco deve essere sostituito con uno ad un indirizzo diverso ("***flush***") (evita aggiornamenti ripetuti ma complesso da implementare e non efficiente ricopiando blocchi con parole "***dirty***" e non),

> [!important] Dirty
> Con la ***write-back*** si mantiene un bit "***dirty***" per ogni blocco che:
> - è a $0$ se il blocco è una copia esatta e "***pulita***" della RAM,
> - è a $1$ se il blocco è stato "***sporcato***" da una scrittura.
> Così si gestisce tale strategia, infatti il blocco *dirty* avrà sempre il valore *sporco* a disposizione finché non verrà rimpiazzato, quindi lì verrà copiato dalla cache alla RAM nella posizione da cui è stato preso originariamente.

###### Organizzazione

Le cache sono organizzate in una struttura a ***[[32 - Memoria e gerarchie#Blocks|blocks]]*** (*blocchi*, insiemi di *word* contigue) dove, con la ricerca, si verifica se una certa *word* appartiene ad un block (grazie a particolari meccanismi e strategie); quindi in caso di:

- ***Cache hit***: la *word* richiesta <u>è in un</u> certo <u>block</u>, quindi <u>la si legge da lì</u>,
- ***Cache miss***: la *word* richiesta <u>non è in nessun block</u>, quindi <u>la si cerca in RAM</u> e si <u>carica il blocco in cui è stata trovata in cache</u>.

![](https://i.imgur.com/rfCrlLf.png)

Considerando i blocks però, bisogna capire come verificare se sono in cache, se lo sono, come accedervi e se non lo sono in quale block copiare quello copiato dalla RAM.

##### Metriche

Ci sono varie metriche da misurare nelle cache:

- ***Hit rate***: è il n° di hit rispetto al totale degli accessi (`n° hit / n° totale accessi`)
- ***Hit time***: è il tempo necessario per ottenere il dato dalla cache (ovvero `tempo di accesso alla cache + tempo per determinare hit/miss`)
- ***Miss rate***: (`1 - hit rate`),
- ***Miss penalty***: tempo per sostituire un blocco in cache + tempo per dare il dato alla CPU (meglio: `hit time (di ogni cache fin qui) + tempo accesso a RAM`).

###### Prestazioni

A quanto risulta dal profiling (simulazione del comportamento della cache su un benchmark di programmi di natura molto diversa per valutarne costi e benefici), il ***miss rate*** diminuisce aumentando la dimensione dei blocchi (fino a un certo punto), mentre aumenta all'aumentare delle dimensioni della cache:

![](https://i.imgur.com/mEHe8q8.png)

##### Livelli

Le cache sono distinte in livelli:

- **Cache L1**: la più piccola, veloce e "vicina" alla CPU,
- **Cache L2**: più grande, lenta e "lontana" dalla CPU di una cache L1, ma sempre più veloce della RAM centrale,
- **Cache L3**: ancora più grande, lenta e "lontana" dalla CPU di una L2, sempre più veloce della RAM ma piuttosto rara, solitamente in CPU potenti o di server,
- (Cache L4: molto poco comune, quasi mai vista, esterna al core).

![](https://i.imgur.com/HRQL8mT.png)

###### Scopo dei livelli

Il <u>tempo medio di accesso alla memoria</u> si calcola con:

$$access\;time = hit\;rate \,\times\, hit\;time \,+\, miss\;rate \,\times\, miss\;penalty$$

La *miss penalty* è il parametro che maggiormente grava sul tempo di accesso, quindi per ridurla si divide la cache in più livelli. Vi è anche la possibilità di dividere un livello di cache in 2 sottolivelli di dati e istruzioni:

![](https://i.imgur.com/L7Wbfqh.png)

Combinando più cache si ottiene una formula leggermente diversa per il calcolo della *miss penalty*:

$$miss\;penalty\;L1 = hr_{2} \times (ht_{1} + ht_{2}) + mr_{2} \times mp_{2}$$

Quindi, per il calcolo del tempo di accesso medio alla memoria (a 2 livelli):

$$t = hr_{1} \times ht_{1} + mr_{1} \times (hr_{2} \times (ht_{1} + ht_{2}) + mr_{2} \times mp_{2})$$

E a 3 livelli:

$$t = hr_{1} \times ht_{1} + mr_{1} \times (hr_{2} \times (ht_{1} + ht_{2}) + mr_{2} \times (hr_{3} \times (ht_{1} + ht_{2} + ht_{3}) + mr_{3} \times mp_{3}))$$

# Esercizi

###### 1) Calcolo tempo medio di accesso

In un sistema con 2 livelli di cache si calcoli il tempo medio di accesso alla memoria dati:

- $hr_{1} = 90\%$
- $hr_{2} = 80\%$
- $ht_{1} = 1$ ns
- $ht_{2} = 5$ ns
- Tempo di accesso a RAM: 100 ns

# Soluzioni

###### 1)

---

Prossima lezione: [[37 - Tipi di cache]]

