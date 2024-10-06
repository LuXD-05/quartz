---
public: true
edited_seconds: 6820
modified_at: 21/06/2024 09:22:34
---
### Normalizzazione
::
> [!important] Normalizzazione
> La **normalizzazione** è un processo che parte da un db <u>non normalizzato</u> e definisce delle regole (modificandone lo schema logico) al fine di evitare **inconsistenze** dei dati ed **anomalie** nelle operazioni.
 
Questa è un'ottimizzazione **progressiva** che permette di riportare le relazioni nelle cosiddette **forme normali**. Il fatto di essere <u>progressiva</u> implica che non è possibile normalizzare un db direttamente a una certa forma normale senza prima normalizzarla a quelle precedenti. Ovviamente sui db NoSQL la normalizzazione ha scarso (se non nessun) effetto.

### Anomalie
::
###### Ridondanza
Questa è il + grande difetto dei db. Perché:
1) Occupa spazio inutile,
2) Intralcia le SELECT,
3) Rende i dati duplicati e inconsistenti, che non portano informazione.
##### Anomalie d'inserimento
Se nell'<u>inserire un nuovo record</u> si è costretti a <u>inserire info già presenti nel db</u>. Conseguenza: **ridondanza**.
###### Esempio 1
In una [[#Esempio 5|tabella ordini mista a clienti]] (non normalizzata), non è pensabile far inserire al client ogni volta l'indirizzo a cui spedire il pacco perché magari lo scrive ogni volta in modo diverso. Quindi l'indirizzo deve essere presente in una tabella a parte e la selezione deve essere possibile mediante una ComboBox.
##### Anomalie di cancellazione
Se nel <u>cancellare un record</u> si è costretti a <u>cancellare info</u> che possono <u>ancora essere utili nel db</u>. Conseguenza: **inconsistenze**.
###### Esempio 2
In una [[#Esempio 5|tabella ordini mista a clienti]] (non normalizzata), cancellando una riga si cancella anche il cliente.
##### Anomalie di aggiornamento
Se dovendo <u>aggiornare un record</u> si è costretti ad <u>aggiornarne altri</u>. Conseguenza: **performance basse**.
###### Esempio 3
In una [[#Esempio 5|tabella ordini mista a clienti]] (non normalizzata), se l'indirizzo di un cliente cambia allora bisogna cambiarlo in tutte le altre tuple.

### Forme normali
::
> [!important] Forma normale
> Una **forma normale** (FN) è una proprietà di uno schema relazionale che ne garantisce l'assenza di anomalie.
 
Ci si ferma solitamente alla **3FN** (o alla *Boyce-Codd*) in quanto il costo in termini di tempo per realizzarle sarebbe > dell'effettivo guadagno.

#### 1FN
::
##### Cos'è
Una relazione è in **1FN** (detta anche *forma atomica*) se:
- Ha una **PK** (tutte le <u>tuple devono essere diverse</u>),
- **Ogni attributo** è definito su un **dominio** di attributi **atomici** (<u>no attributi composti o multivalore</u>).
##### Step
1) Ogni **attributo composto** viene sostituito da tanti **attributi** quanti sono i **valori** atomici **che contiene**,
2) Ogni **attributo multivalore** viene riportato in una **nuova tabella** con una **nuova PK**, mentre la PK della tabella primaria diventa **FK**. Questo si fa <u>invece di duplicare la tupla della tabella primaria</u> per ogni valore dell'attributo in quanto ciò creerebbe anomalie e ridondanza.
###### Esempio 4
La relazione:
**Ordini**(<u>idOrd</u>, <u>idCli</u>, <u>idProd</u>, nome, cognome, prodotti, qta, prezzo, indirizzo)
Diventa (solo in <u>1FN</u>):
**Ordini**(<u>idOrd</u>, <u>idCli</u>, nome, cognome, via, citta, numcivico)
**OrdiniProdotti**(<u>id</u>, idOrd\*, idProd\*, qta)
**Prodotti**(<u>idProd</u>, prezzo)

#### 2FN
Hint: dipendenze funzionali, cos'è
::
##### Dipendenze funzionali
Per poter normalizzare in **2FN**, bisogna identificare all'interno della relazione, le **dipendenze funzionali**.
>[!important] Dipendenza funzionale
>In una relazione $R$ con almeno 2 attributi $x$ e $y$: se $y$ (valore) varia al variare di $x$ (valore), $y$ ha una **dipendenza funzionale** da $x$. Si indica con: $x \rightarrow y$ ($x$ determina $y$).
 
(Questo vale, oltre che per i singoli attributi, anche per **insiemi di attributi**).
Inoltre ne consegue che: **per ogni insieme di tuple** (**righe**) possibili **in $R$**, <u>non ne possono esistere 2 che hanno lo stesso valore di</u> $x$ <u>e valori diversi di</u> $y$.
###### In generale
Data una relazione R ed un'insieme di attributi:
$x = \{x_{1}, x_{2}, \,\ldots\, x_{n}\} \;di\; R$
Si dice che un attributo $y$ di $R$ dipende da $x$ (e si scrive:)
$x_{1}, x_{2}, \,\ldots\, x \rightarrow y$
se e solo se i valori degli attributi di $x$ hanno un valore in $y$ univoco per ogni istanza di $R$.
La PK è quindi determinante per ogni attributo della relazione.
##### Cos'è
Una relazione è in **2FN** se:
- La relazione è in **1FN**,
- Tutti i suoi <u>attributi non PK</u> **dipendono dalla PK** (**intera**), quindi gli attributi non devono dipendere da <u>solo parte della PK</u>.
##### Step
Si **scompone** la relazione di partenza in **nuove relazioni**, ognuna avente gli **attributi** e la **parte di PK** da cui dipendono.
Se una relazione ha una **PK** semplice (**singola**), essa è <u>già in 2FN</u> dato che gli attributi dipendono tutti solo da essa.
###### In generale
Data una relazione <u>non in 2FN</u>: 
$R(A_{1}, A_{2}, \,\ldots\, A_{5})$
Con:
$A_{1}, A_{2} \rightarrow A_{3}$
$A_{1} \rightarrow A_{4}$
$A_{2} \rightarrow A_{5}$
Si vanno a creare:
$R1(A_{1}, A_{2}, A_{3})$
$R2(A_{1}, A_{4})$
$R3(A_{2}, A_{5})$
Includendo eventualmente le relative **FK**.
###### Esempio 5
La relazione:
**Ordini**(<u>idOrd</u>, <u>idCli</u>, nome, cognome, via, citta, numcivico)
Diventa (solo in 2FN):
**Ordini**(<u>idOrd</u>, idCli\*, via, citta, numcivico)
**Clienti**(<u>idCli</u>, nome, cognome)

#### 3FN
Hint: cosa serve per la 3FN? (dipendenze transitive + def)
::
##### Dipendenze transitive
Per poter normalizzare in **3FN**, bisogna identificare all'interno della relazione, le **dipendenze transitive**.
> [!important] Dipendenza transitiva
> In una relazione $R$ con 3 attributi $x$, $y$ e $z$ con $x$ PK,
 
Quando un attributo non chiave, dipende da un altro attributo non chiave (che a sua volta dipende dalla PK in quanto è già in 2FN).
Al variare di un attributo non chiave, varia anche l'altro attributo.

Quando sono in 2FN, per evitare ridondanze, partendo dalla PK, si vedono le dipendenze transitive. Queste si capiscono facendo una tabella e buttandoci dentro un paio di dati.
###### Esempio
 Veicolo(<u>id</u>, tipo, prezzo, potenza):
  
| ID  | Tipo | Prezzo | Potenza |
|:---:|:----:|:------:|:-------:|
| 1   | Bike | 100    | 1kw     |
| 2   | Car  | 1000   | 10kw    |
| 3   | Bike | 100    | 1kw     |
 
In questo caso <u>tutti gli attributi dipendono dall'id</u>, però **prezzo** e **potenza** <u>dipendono dal tipo del veicolo</u>. Questa è una dipendenza transitiva.

##### Cos'è
Una relazione è in **3FN** se:
- è in **2FN**,
- **Non ha dipendenze transitive** (<u>tutti gli attributi non-chiave dipendono direttamente dalla PK</u>).

Un database è in 3FN se tutte le relazioni sono in 3FN.
##### Step
Si ottiene scomponendo la relazione di partenza in nuove relazioni, nelle quali tutti gli attributi dipendono dalla PK.

##### Formalizzando
Data la relazione R(<u>A1</u>, A2, A3, A4) in 2FN, con le seguenti dipendenze funzionali:
- A1 $\rightarrow$ A2
- A2 $\rightarrow$ A4
Si ha quindi una **dipendenza transitiva**: A1 $\rightarrow$ A2 $\rightarrow$ A4
Si può normalizzarla andando a <u>rimuovere questa</u> e creando una nuova relazione per la dipendenza: A2 $\rightarrow$ A4
Ottenendo infine:
- R1(<u>A1</u>, A2, A3)
- R2(<u>A2</u>, A4)