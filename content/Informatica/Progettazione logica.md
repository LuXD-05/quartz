# La progettazione logica

### Descrizione

Descrive la situazione di un db attraverso un modello **logico**. È specifica per ogni tipo di db (SQL o noSQL).

È stata inventata da **James Codd** e si basa sul concetto matematico di “**relazione**”, rappresentabile per mezzo di **tabelle**.

### Prodotto cartesiano

Dati degli insiemi $(D_{1}, D_{2} \;\ldots\; D_n)$ anche non distinti, il **prodotto cartesiano** $(D_{1} * D_{2} \;\ldots\; * D_n)$ è **l’insieme di tutte le n-uple ordinate** $(d_{1}, d_{2} \;\ldots\; d_n)$ **tali che**: $d1 \in D1,\; d2 \in D2 \;\ldots\; e \;dn \in Dn$.

(tab)

### Relazione

(Dati una sequenza di insiemi $D_{1}, D_{2} \;\ldots\; D_n$) una **relazione** R è un **sottoinsieme del prodotto cartesiano** di $D_{1} * D_{2} \;\ldots\; * D_n$.

(Quindi un insieme di n-uple ordinate $d_{1}, d_{2} \;\ldots\; d_n$ con $d_i$ appartenente a $D_i$). Mentre una **relazione modella un’entità**, ogni **tupla è un’istanza dell’entità stessa**.

(tab)

In una relazione quindi: 

- **Non** è **definito** alcun **ordinamento** tra le **n-uple**,
- Le **n-uple** sono **distinte** tra loro (con la **PK**).

##### Domini

Sono **l’insieme di tutti i possibili valori che un attributo** può assumere (tutti i valori delle celle di una colonna db). Ciascuno di essi:

- Si rifà ad un **tipo di dato** elementare (int, char…),
- Ha un **nome**, detto **attributo** che lo distingue dagli altri nella relazione (nome di colonna).

In tabella quindi: **colonne** (nomi) = **attributi** e **righe** = **tuple**. <u>Dominio</u> = <u>Attributo ER</u>

(foto)

##### Caratteristiche

###### Grado

Il **grado** di una relazione è il **n° di attributi che compongono quella relazione** (<u>n° di colonne</u>).

###### Cardinalità

La **cardinalità** di una relazione è il **n° di tuple** (<u>n° di righe</u>).

###### Schema

Lo **schema** (o **intensione**) di una relazione **R** (A1, A2… An) è costituito dal **nome R** e dagli **attributi Ai**, si indica come: 

\<NomeRelazione\>(\<A1\>, …, \<An\>) - \[Es: Giocatore (Nome, Cognome, Squadra)\]

Lo schema è **statico**, non cambia nel tempo (NomeRelazione e i suoi attributi non cambiano).

Lo **schema** del **db** è l’insieme di tutti gli schemi di relazione all’interno di esso.

###### Istanza

Una **istanza** (o **estensione**) di una relazione **R** (A1, A2… An) dello schema di R (A1… An) è un **insieme di tuple** **r(R) = { t1, … tn }** **in un certo istante di tempo** (l’insieme di tutte le tuple/righe di una relazione in un certo istante).

L’istanza è **dinamica**, cambia nel tempo (i valori delle colonne possono cambiare nel tempo).

Un’**occorrenza** di **db** invece è l’insieme di tutte le istanze di tutti gli schemi di relazione (tutte le tabelle).

### Rappresentazione di una relazione

Una relazione può essere rappresentata in diversi modi, tramite: **insiemi**, **elenchi** (tipo json) o **tabelle**.

Quindi una **tabella** di db è la **rappresentazione di una relazione** e <u>non</u> la relazione stessa.

##### Tabelle

Nelle tabelle:

- **Colonne** = **attributi**, sono unici e identificano un dominio (il loro ordine è ininfluente),
- **Righe** = specifiche **tuple/record** diversi fra loro (il loro ordine è ininfluente),.

Una **tabella** **rappresenta** una **relazione** **se**:

- I **valori** di ogni **colonna** sono **omogenei** fra loro (stesso dominio),
- Le **righe** sono diverse tra loro (**univoche** considerandone tutti i valori),
- Le **intestazioni** delle colonne (**attributi**) sono **diversi** tra loro.

### Struttura basata su valori

I db relazionali sono **basati sui valori**, ovvero sul **contenuto delle singole celle**, (senza puntatori).

##### Valori NULL

Nei db relazionali c’è il valore **NULL**, indicante che il **dato** in quella cella **manca**, **non c’è** (questo non include “” o 0), per vari motivi:

- Valore **sconosciuto**, quando **esiste un valore nel dominio ma non è noto** (ES: "Film preferito? Non lo so"),
- Valore **inesistente**, **non esiste un valore nel dominio** (Es: "Film preferito? Non ne ho uno"),
- Valore **senza informazione**, **non si sa se esiste un valore o meno** ("Film preferito? (se chiesto a un neonato, non sa cos'è un film)").

I vari **DBMS non distinguono il tipo NULL** (implicitamente è lo stesso valore per tutti).

# Chiavi e vincoli

### Primary Key

La **PK** è un **attributo** (**o** un **insieme** di essi) che **identifica in modo univoco una tupla** della relazione (NOT NULL).

I valori NULL (nei campi PK) impediscono di identificare le tuple e di realizzare i riferimenti ad altre relazioni.

### Foreign Key

La **FK** è un **attributo** (**o** un **insieme** di essi) che **non è la PK della relazione in cui compare**, ma **di un’altra**, alla quale è legata tramite una **associazione**.

### Vincoli di integrità

Un DBMS deve prevenire l’immissione di info non corrette. Ad uno **schema di db** si possono associare dei **vincoli d’integrità** e un’**istanza di db** che **soddisfa tutti** i **vincoli di** **integrità** è detta **legale**.

##### Definizione

Insieme di **regole** che devono essere **rispettate** affinché il **db non contenga info inconsistenti** durante le **manipolazioni** (inserimenti, modifiche, cancellazioni…).

### Vincoli

I vincoli possono essere:

##### Espliciti

Quelli che impongono **restrizioni sui valori** assumibili **dagli attributi** (V1: \[Entità.Attributo\] \[espressione\])

##### Impliciti

Sono definiti **all’interno delle strutture dati** (schema logico), e sono:

- Vincoli **PK** --> **in** un’**entità** **ogni** **istanza** (riga) deve essere **univoca**, quindi i **campi** **PK** devono essere **tutti** **diversi**,
- Vincoli **referenziali** --> date 2 entità **A** e **B** aventi un’**associazione**, **non esiste** (o non è inseribile) un **elemento** in **A** che **non** sia **associato** ad un altro **elemento** in **B** (rappresentato disegnando la relazione nell’ER / associazioni totali).

### Tipi

I vincoli possono essere di 2 tipi:

##### Intrarelazionali (o interni)

Sono definiti all’interno di una **singola relazione**. Si suddividono a loro volta in:

###### Vincoli su una singola tupla 

Coinvolgono **1 sola riga**. (Forma: Vn° (relazione) …) e sono:

- Su **valori** / di **dominio**: coinvolgono **1 solo attributo** (vincolo su valori che può assumere: V1(E) voto < 10…),
- Su **+ attributi** (ES: V1(E): data_start < data_end)

###### Vincoli su + tuple (sono in pratica la **PK** che impedisce tuple uguali)

##### Interrelazionali (o esterni)

Sono **vincoli** definiti **tra + relazioni**. (Forma: Vn° (\[relazione1} … \[relazioneN\]): \[espressione\]).

ES: V1(Azienda, Dipendente): SE D.livello < 7 ALLORA D.stipendio < A.MediaStipendio;

### Integrità referenziale

È un insieme di **regole** che garantisce **l’integrità dei dati nelle relazioni associate tramite** una **FK**.

Quindi **ogni** valore (_not null_) della **FK** deve avere un valore di **PK** **corrispondente** nella tabella associata.

È il vincolo più importante tra i vincoli **interrelazionali**.

Quindi:

Un **vincolo d’integrità referenziale** (**FK**) tra un attributo **A1** di una relazione **R1** (**associata**) e un’altra relazione **R2** (**primaria**) impone ai valori di **A1** in **R1** di comparire come valori **PK** in **R2**.

Quindi:

1) **Non si può mettere** un valore nella **FK** della tabella associata **se non è** una (esiste tra i valori della) **PK** della **tabella** **primaria**,
2) **È possibile** immettere **NULL** nella **FK** per dire che le **righe** **non** sono **correlate** (**associazione parziale**),
3) **Non si può eliminare** una **tupla** dalla tabella **primaria** se ha righe **legate** ad essa con la **FK** nella tabella **associata**,
4) **Non si può modificare** la **PK** nella tabella **primaria** se ad essa **corrispondono** **righe** nella tabella **associata**.

# Dall'ER allo schema logico

#### Recap

Per farlo bisogna:

1) Calcolare il n° di relazioni con: n° relazioni = n° entità – n° associazioni 1:1 + n° associazioni N:N.
2) Applicare le regole di derivazione ad ogni entità (Ovvero: mappare ogni entità a relazione sottolineando le PK e tradurre ogni associazione in base a molteplicità/cardinalità).
3) Per ogni relazione indicare le FK:
4) Mappare eventuali vincoli espliciti con sintassi: V1 : (\[nomerelazione\]) \[espressione\].
5) Controllare che il numero di relazioni scritte coincida col n° trovato col punto 1.

### Regole di derivazione

- **Entità** = **Relazione**,
- **Attributo** (entità) = **Attributo** (relazione),
- **PK** (entità) = **PK** (relazione),
- **Associazioni** (tra entità) = si mappano in base a **cardinalità**/**molteplicità**.

### Mapping delle associazioni

Le associazioni, per passare dall’ER al modello logico, devono essere **mappate**.

##### Associazione 1:1 totale

Si derivano le **2 relazioni** in **una unica** che contiene gli **attributi della 1° + quelli della 2°**. Viene poi **scelta 1** delle 2 **PK**.

##### Associazione 1:1 parziale

Nell’**entità** con **parte** dell’**associazione totale** è messa la **PK** dell’**altra entità** che **diventa FK**.

##### Associazione 1:N

Vengono aggiunti all’**entità** con **parte** della **relazione** **N** la **FK** dell’**entità** con parte **a 1**.

##### Associazione N:N

Si crea una **nuova relazione** fatta dalle **PK delle 2 entità** **+** eventuali **attributi** dell’associazione.

