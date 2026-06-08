# Lezione 7

### Progettazione logica

La **progettazione logica** ha l'obiettivo di <u>tradurre lo schema ER</u> (della progettazione concettuale) in uno <u>schema logico equivalente</u> per il DBMS scelto. Oltre allo schema logico si hanno in output vincoli di dominio, `CHECK`, trigger, comandi `GRANT` e documentazione. 

La progettazione logica si divide poi in 2 fasi:

##### Fase di ristrutturazione

Questa crea un **ER ristrutturato** equivalente all'originale al fine di semplificarne la successiva traduzione:

- Si <u>eliminano i costrutti non rappresentabili</u> nel modello logico del DBMS (tipo attributi composti, multi-valore e gerarchie di generalizzazione),
- Si fanno <u>altre ristrutturazioni relative alle prestazioni</u>...

##### Fase di traduzione

In questa l'ER ristrutturato viene <u>tradotto nello schema logico equivalente</u> applicando certe **regole di trasformazione** per i vari costrutti del modello ER. Come la [[#Fase di ristrutturazione|precedente]], queste fasi <u>non sono univoche</u> in quanto dipendono dal carico di lavoro e dal DBMS scelto.

#### Regole di ristrutturazione

##### Eliminazione di attributi composti

Ci sono 2 modi per eliminare un attributo composto $A$ da un'entità $E$ (comunque, i <u>vincoli di cardinalità</u> dell'attributo composto sono riportati su quelli nuovi anche ricorsivamente in caso di sotto-attributi composti):

![](https://i.imgur.com/bcdxLUg.png)

###### "Collasso" in 1

Questo prevede che tutti gli attributi "collassino" in uno solo semplice. Scelta adatta se basta conoscere l'informazione complessiva, tuttavia i vincoli dei sotto-attributi "collassati" devono essere garantiti dall'applicazione.

![](https://i.imgur.com/XJC8GEQ.png)

###### "Esplosione"

Con questa invece i sotto-attributi vengono "esplosi" diventando direttamente attributi semplici di $E$. Scelta adatta se è necessario accedere ad ogni sotto-attributo, tuttavia si perde il collegamento logico tra i sotto-attributi (comunque si cerca di suggerirlo con i nomi degli stessi).

![](https://i.imgur.com/WHV7V31.png)

##### Eliminazione di attributi multi-valore

Per eliminare gli attributi multi-valore, si definisce una nuova entità (col nome dell'attributo) dotata di un attributo semplice che <u>la identifica</u> (**PK**) e che <u>contiene i valori dell'attributo multi-valore originale</u>:

![](https://i.imgur.com/DpXJkUn.png)

Nella nuova associazione che si crea, circa le cardinalità delle entità che vi partecipano:

- **Entità originale**: <u>mantiene la cardinalità dell'attributo multi-valore</u>,
- **Entità generata**: la cardinalità <u>dipende dal dominio</u> (nell'esempio `1-N` siccome suppone che ogni numero può essere condiviso tra più clienti).

##### Eliminazione di gerarchie di generalizzazione

Le gerarchie di generalizzazione vengono sostituite da entità e associazioni ed esistono varie opzioni per tale ristrutturazione (in base al tipo di gerarchia):

> [!important] Generalizzazioni a più livelli
> In caso ci siano più livelli di generalizzazione nella gerarchia si applicano le seguenti regole partendo dalle foglie (ultime entità figlie).

###### Eliminazione di entità figlie

Di una gerarchia possono esserne eliminate le entità **figlie** e ciò comporta che i loro <u>attributi</u> vengano <u>trasferiti al padre diventando opzionali</u>:

![](https://i.imgur.com/dQ10Oes.png)

Stessa cosa per le associazioni sulle entità figlie, la cui partecipazione diventa <u>opzionale</u>, rendendo tale associazione <u>parziale</u>:

![](https://i.imgur.com/oVu4D5e.png)

Inoltre (se necessario) viene aggiunto al padre un **attributo discriminante** (solitamente chiamato "`type`") che permette di determinare <u>di che tipo</u> (figlio) <u>è ogni istanza dell'entità padre</u> mantenuta; tuttavia tale attributo deve rispettare certi vincoli per i vari tipi di generalizzazioni:

- **Totali**: `type` è <u>obbligatorio</u> (`NOT NULL`),
- **Parziali**: `type` è <u>opzionale</u> (`NULL`),
- **Esclusive**: `type` è <u>mono-valore</u>,
- **Condivise**: `type` è <u>multi-valore</u>.

> [!info] Vincoli di integrità aggiuntivi
> In seguito è necessario definire altri vincoli di integrità (in documentazione) per imporre che i valori degli attributi aggiunti al padre rispettino l'attributo `type` (per esempio cliente VIP con attributo "bonus" e cliente Standard con attributo "punti", in base a `type` uno dei 2 attributi deve essere `NULL` e l'altro valorizzato):
> ![](https://i.imgur.com/SfeNacs.png)
> Perciò se la generalizzazione è:
> - **Totale**: gli <u>attributi di almeno 1 figlio devono assumere valori non nulli</u>,
> - **Esclusiva**: gli <u>attributi di al massimo 1 figlio possono assumere valori non nulli</u>.  

###### Eliminazione dell'entità padre

Con questa soluzione gli <u>attributi del padre sono inseriti in ogni figlio</u> (applicabile <u>solo</u> per le generalizzazioni **totali** in quanto eliminando il padre non si possono rappresentare istanze che non sono anche istanze di 1 figlio):

![](https://i.imgur.com/liwCdX9.png)

Se la generalizzazione è **condivisa**, un'entità che è istanza di più figli viene rappresentata con istanze separate di ogni figlio ma con <u>identificatori uguali</u>.

Se la generalizzazione è **esclusiva**, si aggiunge un **vincolo di integrità** per indicare che <u>non possono esistere più istanze con gli stessi identificatori</u>.

Delle associazioni a cui partecipava il padre, ad ognuna vi deve partecipare ogni figlio e:

- I **figli** <u>mantengono le cardinalità del padre</u>,
- Per le **entità dall'altro** lato delle associazioni, la loro <u>partecipazione</u> (se non specificata la possibilità del contrario) <u>diventa opzionale</u> (**parziali**, in quanto un'istanza non può essere anche istanza di più entità figlie).

###### Sostituzione con associazioni

Con questo metodo le entità rimangono inalterate mentre la gerarchia viene sostituita con ${} n$ associazioni `1-1` ognuna che lega il padre a 1 figlia:

![](https://i.imgur.com/mHKTpVR.png)

Se la generalizzazione è **totale**, <u>ogni istanza del padre deve partecipare ad almeno 1 associazione con le figlie</u> (posto come <u>vincolo di integrità</u>).

Se la generalizzazione è **esclusiva**, <u>1 istanza del padre può partecipare al massimo 1 associazione con le figlie</u> (posto come <u>vincolo di integrità</u>).

Per ognuna di queste:

- **Figli**: partecipano sempre con cardinalità `1-1` e sono <u>identificate esternamente dal padre</u> (perciò non hanno bisogno di trasferire i suoi attributi),
- **Padre**: partecipa con cardinalità `0-1`, anche se l'associazione è <u>totale</u> (dato che comunque 1 istanza del padre potrebbe essere associata solo ad alcuni figli).

###### Scelta della regola di traduzione

Si può scegliere una regola di traduzione in base al contesto in valutazione (seppur sono concesse anche soluzioni ibride) e per ciò ci sono certe cose da considerare:

- **[[#Eliminazione di entità figlie|Eliminazione figli]]**: utile quando i <u>figli hanno pochi attributi</u> o quando alla <u>> parte delle operazioni non serve distinguere tra padre e figli</u>,
- **[[#Eliminazione dell'entità padre|Eliminazione padre]]**: utile con generalizzazioni **totali** in cui la <u>> parte delle operazioni distinguono spesso tra padre e figli</u> (risparmia memoria rispetto alla precedente).
- **[[#Sostituzione con associazioni|Sostituzione con associazioni]]**: è la soluzione più generale ed è utile in caso <u>le altre non vadano bene</u> (risparmia comunque memoria rispetto a eliminare i figli).

> [!info] Svantaggi
> Nota che ogni soluzione comporta anche degli svantaggi:
> - **Eliminazione figli**: comporta <u>sprechi di memoria</u> a causa della presenza di valori `NULL`,
> - **Eliminazione padre**: applicabile <u>solo per generalizzazioni totali</u> e le <u>operazioni generali</u> (tipiche del padre) vanno <u>replicate su ogni figlio</u>, 
> - **Sostituzione con associazioni**: può essere <u>dispendioso ricostruire l'informazione originale completa</u> (soprattutto in database relazionali dove servono tante `JOIN`).

#### Regole di traduzione

##### Traduzione di entità

Le **entità** possono venire tradotte direttamente <u>se non possiedono identificatori esterni o misti</u> (in caso contrario la loro traduzione è legata a quella delle <u>associazioni</u>).

![](https://i.imgur.com/EXNlOHi.png)

(Dove: $D_{i}$ sono i domini degli attributi e vanno anche definiti vincoli di obbligatorietà per attributi non opzionali e vincoli di chiavi candidate).

Perciò una tale entità viene così tradotta:

- **Nome**: uguale a quello dell'entità,
- **Attributi**: sono gli stessi dell'entità e con lo stesso dominio (con opportuni vincoli di obbligatorietà per quelli non opzionali),
- **Identificatori**: diventano <u>chiavi candidate</u> della relazione tra cui deve essere scelta una **PK**, che comporta che le altre diventino attributi opzionali (nota: è ideale che la PK sia scelta tenendo da conto le regole di minimalità e da quante operazioni è usata, in quanto il DBMS ne crea un *index* rendendo le operazioni più efficienti).

> [!important] Niente PK?
> Se nessuna delle chiavi candidate soddisfa i suddetti requisiti si può aggiungere alla relazione un <u>attributo univoco</u> (generalmente `id`) che assume valori appropriati ai fini dell'identificazione.

##### Traduzione di associazioni

###### N-N (unarie/binarie)

Ogni associazione `N-N` (binaria e unaria) corrisponde a una relazione:

![](https://i.imgur.com/wwzKZVk.png)

In cui:

- **PK**: formata dalla <u>coppia degli identificatori delle 2 entità collegate</u> (che fungono anche da FK) così da non avere legami duplicati tra le stesse istanze,
- **Attributi**: gli identificatori (nelle associazioni unarie `N-N`) devono essere <u>rinominati</u> con `alias` (così da non averceli presenti 2 volte nella singola entità coinvolta), mentre in generale possono essere aggiunti attributi propri dell'associazione.

###### 1-N (binarie)

Per tradurre relazioni binarie `1-N`, normalmente si aggiungono alla relazione dal lato `1` (con cardinalità max = 1) una **FK** (che riferisce la PK dell'altra relazione) e gli eventuali attributi propri della relazione (opzionali o obbligatori in base all'opzionalità/obbligatorietà della relazione dal lato `1`):

![](https://i.imgur.com/fjPWxG7.png)

Se l'associazione esiste <u>solo per poche istanze</u>, si avrebbero tanti valori `NULL`; in tal caso si può adottare un'altra soluzione che (come per le `N-N`) consiste nel <u>creare una nuova relazione</u> contenente gli identificatori delle 2 entità partecipanti (che fungono da FK mentre la PK è composta solo dall'attributo che riferisce la relazione dal lato `1`) e gli attributi propri dell'associazione:

![](https://i.imgur.com/FERXeeb.png)

###### 1-1 (binarie)

Ci sono 3 modi per tradurre associazioni binarie `1-1` (in base alla <u>cardinalità minima</u>):

1\) Se solo <u>1 delle 2 entità ha partecipazione obbligatoria</u>, si aggiungono alla sua relazione la FK che referenzia l'altra entità e gli attributi dell'associazione:

![](https://i.imgur.com/zLR3rWs.png)

2\) Se entrambe sono **obbligatorie** è (quasi) indifferente in quale relazione aggiungere FK e attributi dell'associazione:

![](https://i.imgur.com/kveFQKo.png)

3\) Se entrambe sono **opzionali** anche qui è (quasi) indifferente in quale relazione si aggiungono attributi (opzionali stavolta) e FK:

![](https://i.imgur.com/dWf9Gsq.png)

> [!info] Per eliminare i valori `NULL`
> Altrimenti è possibile tradurre l'associazione in una sola nuova relazione contenente tutti gli attributi dell'associazione e 1 PK a scelta tra gli identificatori delle 2 entità.

###### 1-1 e 1-N (unarie)

Anche le associazioni `1-1` e `1-N` si traducono come quelle binarie (ma considerando, al posto delle entità associate, i ruoli):

![](https://i.imgur.com/XI4lb20.png)

###### (n-arie)

Anche le n-arie si traducono come quelle binarie, solo che servono più FK (spesso sono `N-N` e si traducono creando una nuova relazione):

![](https://i.imgur.com/yu6bavP.png)

##### Traduzione relazioni con identificatore esterno/misto

![](https://i.imgur.com/Jrw36wV.png)

Partizionamento e accorpamento?

---

