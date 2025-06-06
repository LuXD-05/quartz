# Lezione 6

### Random Access Stored Program

Esiste anche il modello **RASP** (*Random Access Stored Program*) che, al contrario del [[5 - Macchina RAM|RAM]]:

- Ha un programma non più fisso ma lo **salva in memoria** (registri),
- Permette la **modifica delle istruzioni a *runtime***.
- Non dispone di indirizzamento indiretto (`*i`),
- Ogni istruzione occupa 2 registri (quindi il PC si auto-incrementa ogni volta di 2)

  ![](https://i.imgur.com/wKCemGt.png)

> [!info] Nota
> I concetti di stato, computazione, CCU e CCL... sono analoghi alle macchine [[5 - Macchina RAM|RAM]] e validi per entrambe.

##### CCU rispetto a RAM

Per ogni algoritmo RAM ne esiste uno RASP con **input** $x$ di **lunghezza** $n$ dove:

- La **funzione** che eseguono è la <u>medesima</u>: $\;f_{RAM}(x) = f_{RASP}(x)$,
- Ma ogni istruzione RAM equivale al max a 6 istruzioni RASP, quindi: $\;T_{RAM} \cdot 6 \geq T_{RASP}$.

> [!example] Programmi e indirizzamento indiretto
> I programmi RASP quindi (dato che ogni istruzione = 2 registri e 1 istruzione RAM = max 6 istruzioni RASP), sono salvati da $R_{2}$ a $R_{r}$ dove $r = 2 \cdot 6 \cdot \#P_{RAM} + 1$ ($R_{0}$ e $R_{1}$ sono rispettivamente l'<u>accumulatore</u> e <u>registro di appoggio</u>).
> Per la <u>mancanza dell'indirizzamento indiretto</u> in RASP, esso va **simulato**:
> 1) Serve avere un registro $R_{x}$ che contiene l'indirizzo di un altro $R_{y}$,
> 2) `LOAD Rx` = Prendo il valore in $R_{x}$,
> 3) `ADD =r` = Gli aggiungo la lunghezza del programma,
> 4) `STORE R?` = Salvo tale valore in `R?` (registro finale che contiene l'indirizzo),
> 5) `[OP] R?` = Eseguo l'operazione (se `R?` contenesse $23$, allora sarebbe come fare `[OP] *23`).

##### CCL rispetto a RAM

Per ogni algoritmo RAM ne esiste uno RASP con **input** $x$ di **lunghezza** $n$ e una **costante** $c > 0$ dove:

- La funzione è la stessa: $\;f_{RAM}(x) = f_{RASP}(x)$,
- Ma in base a $c$ (*penso sia il n° max di istruzioni RASP a cui corrisponde 1 istruzione RAM*): $\;c \cdot T_{RAM}^{l} \geq T_{RASP}^{l}$.

> [!important] Compatibilità con RAM
> Seppur tra RAM e RASP cambiano i criteri di costo per gli algoritmi, la <u>funzione che calcolano è sempre la stessa</u>; perciò è possibile **simulare programmi RASP con macchine RAM**.

#### Calcolabilità

##### Pura

L'equivalenza tra RAM e RASP è a livello ***computazionale*** (di ciò che si può <u>computare</u>) e si estende anche ad altri linguaggi ($\mathcal{F}_{RAM} = \mathcal{F}_{RASP} = \mathcal{F}_{C} \; ...$). Con ciò si va quindi a definire il concetto di ***calcolabilità***:

> [!important] Tesi di Church-Turing
> La **tesi di *Church-Turing*** sancisce che per ogni funzione della classe delle **funzioni calcolabili** (funzioni associate a problemi umanamente risolvibili) esiste una <u>macchina di Turing</u> capace di risolverla (indipendentemente dall'efficienza). Questo <u>vale anche per tutti i modelli di calcolo equivalenti alle macchine di Turing</u>, come in questo caso i **modelli RAM e RASP**.
> Si può quindi stabilire che la classe delle funzioni associate a programmi RAM/RASP (classe della **funzioni ricorsive parziali** $\mathcal{F}$) <u>coincide</u> con quella delle **funzioni calcolabili**.

##### Effettiva

Prendendo le funzioni ricorsive parziali $\mathcal{F}$ se consideriamo i costi in tempo logaritmici:

$$\mathcal{F}(f) = \forall f_{P} \in \mathcal{F} \;\rightarrow\; \{\; \exists{f} \;|\; T_{P}^{l}(n) = O(f(n)) \;\}$$

$\mathcal{F}(f)$ indica quindi le funzioni in $\mathcal{F}$ calcolabili entro tempo $O(f(n))$ e si osserva che, considerando $T_{P}^{l}(n)$, la coincidenza rimane solo tra $\mathcal{F}_{RAM}(f)$ e $\mathcal{F}_{RASP}(f)$, ma non tra questi ed altri, per esempio $\mathcal{F}_{C}(f)$ o $\mathcal{F}_{Python}(f)$ a causa di problemi e de-ottimizzazioni intrinsechi dei linguaggi.

###### Problemi P

Sempre per $\mathcal{F}$ si definisce:

$$\mathcal{P}_{RAM} = \forall f_{P} \in \mathcal{F}_{RAM} \;\rightarrow\; \{\; \exists{k} \;|\; T_{P}^{l}(n) = O(n^{k}) \;\}$$

Ovvero per ogni ${} \mathcal{F} {}$ esiste una variabile $k$ tale che il **costo in tempo logaritmico** $T_{P}^{l}(n)$ del problema (in base alla <u>dimensione dell'input</u> $n$) è = alla *big-O* di $n^{k}$.

Dato che tali problemi sono equivalenti indipendentemente dal linguaggio scelto ($\mathcal{P}_{RAM} = \mathcal{P}_{RASP} = \mathcal{P}_{C} \; ...$) si definisce $\mathcal{P}$ come la classe dei ***problemi risolubili in tempo polinomiale*** o classe dei **problemi P**.

> [!important] Tesi di Church-Turing estesa
> I **problemi P** godono della ***proprietà di invarianza***, la quale, definita dall'estensione della <u>tesi di Church-Turing</u>, sancisce che anche cambiando il linguaggio o il modello di calcolo su cui si esegue un programma, la sua complessità non cambia (al contrario della calcolabilità effettiva, quindi del <u>costo in tempo logaritmico</u> dell'algoritmo).

#### Linguaggio AG

Il linguaggio AG risolve i problemi del modello RAM, ovvero: istruzioni *assembly-like*, poca sintesi e codice poco intuitivo grazie alle sue caratteristiche:

- Uso di **variabili**,
- Usa strutture più ad **alto livello** (condizioni, cicli...),
- Evita <u>dichiarazioni di tipo</u> (se chiaro dal contesto),
- Permette la creazione di **sottoprogrammi** richiamabili (funzioni e procedure),
- Permette di <u>analizzare la complessità senza tradurre in linguaggio RAM</u>.

###### Comandi

![](https://i.imgur.com/caoztrb.png)

(In pratica è un linguaggio pseudocodice).

---

Prossima lezione: [[7 - Strutture dati elementari]]

