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

- Figli: partecipano sempre con cardinalità `1-1` e sono <u>identificate esternamente dal padre</u> (perciò non hanno bisogno di trasferire i suoi attributi),
- Padre: partecipa con cardinalità `0-1`, anche se l'associazione è <u>totale</u> (dato che comunque 1 istanza del padre potrebbe essere associata solo ad alcuni figli).

###### Scelta della regola di traduzione

#### Regole di traduzione

##### Traduzione di entità

##### Traduzione di associazioni

##### Partizionamento e accorpamento

---

