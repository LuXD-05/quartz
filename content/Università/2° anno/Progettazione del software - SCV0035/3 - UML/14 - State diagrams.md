# Lezione 14

### State diagrams

Gli ***state diagrams*** sono diagrammi dinamici che permettono di descrivere automi a stati finiti attraverso i seguenti elementi:

![](https://i.imgur.com/fSRvgXF.png)

Stati iniziale e finale sono anche detti ***entry point*** ed ***exit point***.

#### Diagrammi semplici

##### Stati

Uno **stato** è una <u>situazione durante la quale una condizione è verificata</u> (solitamente implicita ma intuibile dal nome dello stato); tale condizione può corrispondere a una situazione statica, l'attesa di un evento esterno...

![](https://i.imgur.com/GmMs2rX.png)

Lo stato di ogni oggetto è l'insieme dei valori dei suoi attributi e link in un certo istante di tempo; tuttavia tale è **astratto**, in quanto potrebbe eventualmente corrispondere a diverse (anche infinite) combinazioni di attributi/link. Ciò non significa che gli stati sono **fissi**, anzi potrebbero anche indicare lo <u>svolgimento di un'attività</u> da parte dell'oggetto.

La cosa certa è che gli stati però **permangono nel tempo** <u>finché un evento non fa cambiare stato all'oggetto</u>.

> [!info] Comportamento
> Lo stato di un'oggetto ne influenza il **comportamento**: <u>una stessa operazione può avere effetti diversi in base allo stato dell'oggetto</u> (esempio: inserire in uno stack vuoto inserisce l'oggetto, mentre farlo in uno stack pieno da errore).

###### Eventi

Un **evento** (o *trigger*) è uno stimolo esterno "**individuabile**" (identificabile in una certa classe di eventi) che può causare nell'oggetto che lo riceve una **transizione** (un <u>cambio di valore/stato</u>) o la produzione di altri eventi (la <u>risposta</u> a tali dipende sempre e comunque dallo <u>stato corrente</u> dell'oggetto).

> [!tip] Caratteristiche
> Gli eventi possono avere degli attributi, [[#Condizioni|guardie]] o effetti, ed il loro destinatario può essere unico o un set di oggetti:
> ![](https://i.imgur.com/KvFaK4C.png)
> Inoltre possono essere generati da **[[#Operazioni|azioni]]**.

###### Scenari

Uno **scenario** è una <u>sequenza di eventi</u> che accadono durante una specifica **esecuzione** del sistema.

###### Condizioni

Sulle <u>transizioni</u> è possibile specificare delle **condizioni booleane** (*guard*) che devono essere rispettate, altrimenti non avviene la transizione di stato seppur l'evento che la dovrebbe scaturire si è verificato. In queste è possibile anche usare <u>variabili di altri oggetti</u> del diagramma ma sono <u>valide solo per l'intervallo di tempo in cui si verifica l'evento</u>.

![](https://i.imgur.com/e51tpuu.png)

###### Operazioni

Durante la loro vita, gli oggetti eseguono delle **operazioni** che si dividono in **azioni** (operazioni <u>istantanee</u> (tipo producono eventi o cambiano valori) e associate a <u>eventi e transizioni</u>) e **attività** (operazioni <u>continue o sequenziali</u> associate agli <u>stati</u> e <u>durano finché permane lo stato</u> a cui sono associate):

![](https://i.imgur.com/o91vmKi.png)

Qui abbiamo:

- `do`: specifica l'<u>attività associata allo stato</u>,
- `entry`/`exit`: specificano rispettivamente le azioni che si svolgono <u>all'entrata e all'uscita dallo stato</u>,
- Azioni che vengono fatte in base a certi eventi (qui 1 e 2),
- Transizioni che avvengono in base a certi eventi (qui 3 e 4) con eventuali condizioni o automatiche...

> [!important] Transizioni automatiche
> La freccia che va in basso nell'esempio è una **transizione automatica**, ovvero che si verifica automaticamente alla fine dell'attività in `do` (o dalle $n$ attività scaturite da essa).

###### Identificazione degli stati

Per costruire uno *state diagram* occorre <u>identificare ogni singolo stato in cui esso si può trovare</u>. Per fare ciò al meglio è consigliato:

- **Trascurare attributi ininfluenti** che non incidono in alcun modo sui cambiamenti di stato dell'oggetto,
- **Definire un corretto livello di astrazione** (per uno stack è meglio avere stati tipo "vuoto", "pieno"... e non stati come "0 elementi", "1 elemento"...).

#### Diagrammi strutturati

Gli *state diagrams* **semplici** (piatti) diventano "ingarbugliati" al crescere di stati e transizioni; ciò si risolve con gli *state diagrams* **strutturati**, che fanno uso di sottostati e sotto-macchine per descrivere il tutto in maniera più gerarchica e comprensibile.

###### Stati compositi e regioni

Oltre agli stati semplici, adesso vengono introdotti gli **stati compositi**, che contengono delle sotto-macchine (insiemi di stati e transizioni) nelle proprie **regioni**:

- **Stati compositi semplici**: contengono <u>1 sola regione</u> ([[#Decomposizione OR]]),
- **Stati compositi ortogonali**: contengono <u>più regioni</u> ([[#Decomposizione AND]]).

> [!important] Regione
> Una **regione** è uno <u>spazio ortogonale di uno stato composito che contiene stati e transizioni</u> (analoghe a <u>diagrammi innestati all'interno di altri diagrammi</u>).

##### Decomposizioni

Le decomposizioni descrivono le regioni astratte all'interno degli stati compositi in base a 2 modelli:

###### Decomposizione OR

La **decomposizione OR** <u>suddivide uno stato composito in più sottostati</u> e si chiama così perché quando ci si trova in quello composito, significa che ci si trova in solo 1 dei suoi sottostati. Esempio di un cambio automatico:

![](https://i.imgur.com/cPGml1U.png)

> [!info] Nota
> I sottostati ereditano le transizioni dello stato composito che li contiene:
> - Una transizione che entra in uno stato composito porta (solitamente) allo <u>stato iniziale del sotto-diagramma</u>,
> - Quando si esce da uno stato composito <u>si esce anche da qualsiasi sia il suo sottostato</u>.

###### Decomposizione AND

La **decomposizione AND** invece uno stato composito è suddiviso in più regioni che si evolvono **in parallelo**: quando si è sullo stato composito, ogni regione di esso avrà uno stato attivo (tanti stati attivi quante le regioni). 

![](https://i.imgur.com/JvFJqdK.png)

Questa può essere usata per rappresentare:

- **Oggetti composti**: come l'accendino, che come oggetto aggrega il serbatoio e il fornello e di conseguenza i loro diagrammi,
- **Flussi di esecuzione paralleli**: flussi che si dividono (*fork*) per fare operazioni parallele e che poi si uniscono (*join*) risincronizzandosi (l'<u>esecuzione non termina finché non terminano tutti i sottoflussi paralleli</u>).

##### History

La ***history*** può essere associata a stati compositi ed è come una sorta di "memoria" che si ricorda l'ultimo sottostato in cui si era prima di uscire dal macro-stato; ciò permette di definire transizioni che ritornino direttamente allo stato salvato in history (invece di ripartire dal sottostato iniziale).

Esistono 2 tipi di *history* (identificate con 2 simboli):

###### Shallow history

La ***shallow history*** considera <u>1 solo livello</u> di decomposizione e riporta all'ultimo stato del macro-stato per cui è definita (porta solo allo stato al 1° livello di profondità del macro-stato per cui è definita).

![](https://i.imgur.com/jXS23UJ.png)

###### Deep history

La ***deep history*** invece considera <u>tutti</u> i livelli di decomposizione del macro-stato per cui è definita e riporta all'ultimo stato attivo a qualsiasi livello di decomposizione.

![](https://i.imgur.com/MQUN1KQ.png)

###### Esempio history

Supponendo che si è usciti da `A` quando era attivo `A2.2`:

![](https://i.imgur.com/0VC0Num.png)

- Se si verifica `E2` si tornerà all'ultimo evento ad 1 livello di decomposizione di `A`, ovvero `A2` (e si prosegue dal suo *entry point*),
- Se si verifica `E3` invece, si tornerà direttamente ad `A2.2`.

##### Altro

###### Entry/exit point

Si possono avere diversi *entry points* (nel 2° diagramma in `PerformingActivity` è astratto):

![](https://i.imgur.com/J3lS9fD.png)

Come anche diversi *exit points*:

![](https://i.imgur.com/StsA5Lt.png)

Mentre il simbolo di terminazione indica la fine della *lifeline* della macchina a stati:

![](https://i.imgur.com/FO5lpXi.png)

###### Fork e join

![](https://i.imgur.com/9HwfCcW.png)

###### Selezione

Si può rappresentare un `if` con condizioni in questo modo:

![](https://i.imgur.com/mLERhu5.png)

Usando delle ***junctions*** (giunzioni) si possono rappresentare multiple condizioni anche con più stati come parametri:

![](https://i.imgur.com/WumHxys.png)

###### Conflitti

Si possono anche verificare dei conflitti tra le transizioni (tipo quando hanno guardie non mutuamente esclusive):

![](https://i.imgur.com/qqFMwfg.png)

Qui, nel caso in cui `Y` sia compresa tra 10 e 20, lo stato successivo potrebbe essere indifferentemente `B` o `C`.

###### Priorità

In situazioni di conflitto, la scelta si basa generalmente su priorità implicite (che risolvono i conflitti), le quali si basano sulla posizione relativa nella gerarchia degli stati (<u>una transizione che ha origine da un sottostato ha > priorità rispetto a una che ha origine nello stato composito</u>).

---

Prossima lezione: [[15 - Activity diagrams]]

