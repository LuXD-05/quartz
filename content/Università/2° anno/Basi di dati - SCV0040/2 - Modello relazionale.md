# Lezione 2

### Modello relazionale

Il modello relazionale si basa sulla **relazione** (= tabella in db) e si basa sulle regole di certi concetti matematici come la <u>teoria degli insiemi</u> e le <u>operazioni logiche</u>. Rende semplice rappresentare dati per mezzo di **linguaggi dichiarativi** e costruire interrogazioni complesse.

> [!info] Linguaggi dichiarativi
> Sono linguaggi semplici (anche per i poco esperti in informatica) e (grazie al loro alto livello) permettono al DBMS di implementare varie strategie di ottimizzazione proprie.
> Due linguaggi di interrogazione (che hanno quasi lo stesso potere espressivo e che sono la base dello sviluppo del linguaggio **SQL**) sono:
> - **Algebra relazionale**🥱: dove le interrogazioni sono fatte applicando operatori appositi alle relazioni,
> - **Calcolo relazionale**: in cui le interrogazioni sono espresse tramite formule logiche che vanno verificate dalle tuple ottenute come risultato.

###### Dominio

Si definisce **dominio** un insieme (anche infinito) di valori di un certo **tipo**; più comunemente indica l'<u>insieme di valori ammissibili in una certa colonna di tabella e il loro tipo</u>.

(Nota: un dominio indica un insieme di possibili valori = **infinito**, mentre in una relazione i valori sono ristretti e scelti in base a certi vincoli = **finito**).

###### Prodotto cartesiano

Dati dei domini anche non distinti $\;D_{1}, D_{2} \,\ldots\, D_{n} \in D\;$, il **prodotto cartesiano** $\;D_{1} \times D_{2} \times \,\ldots\, D_{n}\;$ è l'<u>insieme di tutte le</u> **tuple** $\;(d_{1}, d_{2} \,\ldots\, d_{n})\;$ <u>tali che</u> $\;d_{1} \in D_{1} \,\ldots\, d_{n} \in D_{n}\;$. Tale prodotto cartesiano ha **grado** $n$ (grado = n° di colonne e quindi di campi della tupla di relazione).

#### Relazione

Dati dei domini ${} \;D_{1}, D_{2} \,\ldots\, D_{n} \in D\;$ una relazione $R$ è un <u>sottoinsieme finito del loro prodotto cartesiano</u> ${} \;D_{1} \times D_{2} \times \,\ldots\, D_{n}\;$.

La relazione è sempre un **insieme**, perciò:

- Non è definito alcun ordinamento fra le tuple,
- Le tuple sono **distinte** tra loro (poi si vedrà, con una PK)

##### Caratteristiche

###### Grado e cardinalità

Il **grado** di una relazione è il <u>numero di domini</u> (o anche **attributi**) del prodotto cartesiano di cui è sottoinsieme (<u>n° di colonne</u>).

La **cardinalità** di una relazione è il <u>numero di tuple</u> appartenenti ad essa (<u>n° di righe</u>).

![](https://i.imgur.com/1CE2r5v.png)

###### Schema e istanza

Lo **schema** di una relazione $R$ avente degli attributi $(a_{1}, a_{2} \,\ldots\, a_{n})$ è così definito: $R(a_{1}, a_{2} \,\ldots\, a_{n})$. Lo **schema del db** è l'<u>insieme degli schemi di tutte le sue relazioni</u>.

![](https://i.imgur.com/jVllWBg.png)

L'**istanza** di una relazione $R$ invece è un insieme delle sue tuple in un certo istante di tempo. L'**istanza del db** è l'<u>insieme di tutte le istanze delle sue relazioni</u> in un certo istante.

###### Notazioni

Per quanto riguarda le tuple, esistono 2 notazioni principali: 

Ci si può riferire ad uno specifico attributo di esse tramite la **notazione posizionale** (un indice permette di ottenere l'attributo della tupla in quella posizione):

![](https://i.imgur.com/XIxlCyj.png)

Stessa cosa si può fare (oltre a descrivere gli attributi di una tupla) anche con la **notazione nominale** (l'indice diventa il nome di colonna per ottenere il valore nella tupla in essa):

![](https://i.imgur.com/vRShB02.png)

##### NULL

Può succedere che in un'istanza o tupla delle informazioni non siano disponibili (almeno per il momento) se un valore è sconosciuto, inesistente o senza informazione. Perciò si introduce un valore speciale detto `NULL` che non fa parte di alcun dominio e simboleggia la mancanza di informazione.

> [!warning] Attenzione
> Non tutti gli attributi dovrebbero/potrebbero essere `NULL`. Data una relazione: `Matricola(id, nome, cognome, telefono)`:
> - L'attributo `telefono` potrebbe essere `NULL` in quanto (generalmente) non è un'informazione essenziale,
> - L'attributo `id` invece <u>non deve</u> essere mai `NULL` in quanto (in quasi tutti i contesti) è fondamentale per identificare univocamente quella tupla dalle altre.

#### Vincoli di integrità

Gli utenti potrebbero inserire dati non corretti, perciò è anche il <u>DBMS</u> ad effettuare dei controlli su inserimenti e modifiche grazie ai **vincoli di integrità**: condizioni da verificare per ogni istanza della relazione con tali vincoli specificati al momento di definizione dello schema (si assegnano tali vincoli alle colonne quando si creano).

##### Vincoli di chiave

Dei vincoli particolari sono quelli di chiave (*key constraints*) e ce ne sono di diversi tipi:

###### PK

Un vincolo ***primary key*** (PK) si impone a <u>1 o più attributi</u> in modo tale che essi <u>distinguano univocamente ogni tupla della relazione</u>. Negli schemi le PK sono <u>sottolineate</u>. Le PK hanno poi 2 proprietà importanti:

1\) **Univocità**: non possono esistere più tuple la cui PK sia identica (ogni tupla deve avere PK univoca),

2\) **Minimalità**: l'insieme degli attributi PK non contiene attributi "inutili", ovvero attributi che non servono per garantire l'univocità.

> [!info] Super-chiave
> Un insieme di attributi PK che è <u>univoco ma non minimale</u> è detto super-chiave.

###### Candidate & alternate key

Una relazione può contenere <u>più attributi sia univoci che minimali</u>, i quali si chiamano tutti **chiavi candidate**. Quando si sceglie la PK tramite certi <u>criteri</u> (< numero di attributi in PK e > frequenza di utilizzo nelle interrogazioni) le altre chiavi candidate che rimangono si dicono **chiavi alternative** (AK) e <u>tali</u>, a differenza delle PK, <u>possono essere NULL</u>.

###### FK

Con i vincoli ***foreign key*** (FK) è possibile collegare 2 relazioni tra loro; questo impone ad una relazione associata $R_{1}$ (detta referente, quella con FK) che i suoi valori del campo FK compaiano come PK di una relazione primaria $R_{2}$ (detta <u>riferita</u>, quella con PK).

![](https://i.imgur.com/lvhvNby.png)

**Nota 1**: il nome della colonna referente non deve necessariamente corrispondere con quello della colonna riferita nell'altra relazione.

**Nota 2**: è possibile avere più FK in una tabella per collegarla con più tabelle diverse.

> [!important] Integrità referenziale
> Il vincolo di integrità referenziale è imposto con la definizione di una FK ed implica che i valori assunti dalla FK della relazione referente devono esistere come valori della PK nella relazione riferita; perciò implica anche che:
> - Non si può impostare come FK un valore non presente come PK della tabella primaria,
> - È possibile immettere NULL nella FK per indicare che le righe non sono correlate,
> - Non si può eliminare una riga la cui PK è presente come FK in altre tabelle (eccetto con `ON DELETE CASCADE` ecc...),
> - Non si può modificare la PK di una riga presente come FK in altre tabelle (eccetto con `ON UPDATE CASCADE` ecc...).

---

Prossima lezione: [[3 - SQL]]

