---
public: true
edited_seconds: 2920
modified_at: 12/04/2024 16:55:55
---
### Ridondanza
Questa è il + grande difetto dei db. Perché:
1) Occupa spazio inutile,
2) Intralcia le SELECT,
3) Rende i dati duplicati e inconsistenti, che non portano informazione.
### Normalizzazione
> [!important] Normalizzazione
> La **normalizzazione** è un processo che parte da un db <u>non normalizzato</u> e definisce delle regole (modificandone lo schema logico) al fine di evitare **inconsistenze** dei dati ed **anomalie** nelle operazioni.

Questa è un'ottimizzazione progressiva che permette di riportare le relazioni nelle cosiddette **forme normali**. Il fatto di essere <u>progressiva</u> implica che non è possibile normalizzare un db direttamente a una certa forma normale senza prima normalizzarla a quelle precedenti.
Ovviamente sui db NoSQL la normalizzazione ha scarso (se non nessun) effetto.
##### Steps
1) Analisi della realtà d'interesse,
2) [[Progettazione concettuale]],
3) [[Progettazione logica]],
4) [[Normalizzazione]],
5) Schema fisico.
### Anomalie
##### Anomalie d'inserimento
Se nell'inserire un nuovo record si è costretti a inserire info già presenti nel db. Conseguenza: **ridondanza**.
###### Esempio
In una tabella ordini mista a clienti (non normalizzata), non è pensabile far inserire al client ogni volta l'indirizzo a cui spedire il pacco perché magari lo scrive ogni volta in modo diverso. Quindi l'indirizzo deve essere presente in una tabella a parte e la selezione deve essere possibile mediante una ComboBox.
##### Anomalie di cancellazione
Se nel cancellare un record si è costretti a cancellare info che possono ancora essere utili nel db. Conseguenza: **inconsistenze**.
###### Esempio
In una tabella ordini mista a clienti (non normalizzata), cancellando una riga si cancella anche il cliente.
##### Anomalie di aggiornamento
Se dovendo aggiornare un record si è costretti ad aggiornarne altri. Conseguenza: **performance basse**.
###### Esempio
In una tabella ordini mista a clienti (non normalizzata), se l'indirizzo di un cliente cambia allora bisogna cambiarlo in tutte le altre tuple.
### Forme normali
> [!important] Forma normale
> Una **forma normale** (FN) è una proprietà di uno schema relazionale che ne garantisce l'assenza di anomalie.

Ci si ferma solitamente alla **3FN** (o alla *Boyce-Codd*) in quanto il costo in termini di tempo per realizzarle sarebbe > dell'effettivo guadagno.
##### 1FN
Una relazione è in **1FN** (detta anche *forma atomica*) se:
- Ha una **PK** (tutte le <u>tuple devono essere diverse</u>),
- **Ogni attributo** è definito su un **dominio** di attributi **atomici** (<u>no attributi composti o multivalore</u>).
###### Step
1) Ogni **attributo composto** viene sostituito da tanti **attributi** quanti sono i **valori** atomici **che contiene**,
2) Ogni **attributo multivalore** viene riportato in una **nuova tabella** con una **nuova PK**, mentre la PK della tabella primaria diventa **FK**. Questo si fa <u>invece di duplicare la tupla della tabella primaria</u> per ogni valore dell'attributo in quanto ciò creerebbe anomalie e ridondanza.
##### 2FN
###### Dipendenze funzionali
Per poter normalizzare in **2FN**, bisogna identificare all'interno della relazione, le **dipendenze funzionali**.
>[!important] Dipendenza funzionale
>In una relazione $R$ con almeno 2 attributi $x$ e $y$: se $y$ (valore) varia al variare di $x$ (valore), $y$ ha una **dipendenza funzionale** da $x$. Si indica con: $x \rightarrow y$ ($x$ determina $y$).

(Questo vale, oltre che per i singoli attributi, anche per **insiemi di attributi**).
Inoltre ne consegue che: **per ogni insieme di tuple** (**righe**) possibili **in $R$**, <u>non ne possono esistere 2 che hanno lo stesso valore di</u> $x$ <u>e valori diversi di</u> $y$.
Data una relazione R ed un'insieme di attributi:
$x = \{x_{1}, x_{2}, \,\ldots\, x_{n}\} \;di\; R$
Si dice che un attributo $y$ di $R$ dipende da $x$ (e si scrive:)
$x_{1}, x_{2}, \,\ldots\, x \rightarrow y$
se e solo se i valori degli attributi di $x$ hanno un valore in $y$ univoco per ogni istanza di $R$.
La PK è quindi determinante per ogni attributo della relazione.
###### Definizione
Una relazione è in **2FN** se: