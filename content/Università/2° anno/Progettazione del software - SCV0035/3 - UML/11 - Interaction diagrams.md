# Lezione 11

### Interaction diagrams

Descrivono il comportamento dinamico di un gruppo di oggetti e le loro interazioni finalizzate alla risoluzione di un problema; in pratica rappresentano il comportamento di uno specifico *[[10 - Use-Case diagrams#Use case|use case]]* (in termini di oggetti e messaggi scambiati o <u>metodi</u>). 

![](https://i.imgur.com/5ndvm6K.png)

Ce ne sono di 2 tipi:

#### Sequence diagrams

Questi rappresentano le <u>azioni (di interazione tra oggetti) in sequenza temporale</u> per mezzo di una ***timeline*** (senza rappresentare le associazioni tra gli oggetti) e sono usabili in 2 forme diverse: **generica** (mostra tutte le sequenze di azioni possibili) e **d'istanza** (mostra solo una sequenza particolare di azioni).

![](https://i.imgur.com/rsZ4I5V.png)

###### Oggetti

Gli oggetti possono essere qualsiasi cosa che esegue e/o subisce un'azione, quindi anche istanze di attori (in caso il diagramma si riferisce ad uno *use case*) o altro dall'**MVC**:

##### Analisi di robustezza

Le analisi di robustezza si fanno attraverso i ***robustness diagrams***, che (mi sembra di capire) siano semplicemente dei *sequence diagrams* che seguono le regole del pattern MVC (*Model-View-Controller*), ovvero che ogni oggetto può "comunicare" solo con i suoi vicini nella gerarchia (come MVC ma con elementi aggiuntivi).

![](https://i.imgur.com/SZ2agbs.png)

In questo tipo di diagrammi cambia il nome di di utenti, *view*, *controller* e *models* rispettivamente in:

![](https://i.imgur.com/V73EH4I.png)

###### Messaggi

Ci sono diversi tipi di messaggi (metodi): 

- **Completi**: <u>invio di dati con risposta</u> (ricezione risultato),
- ***Self-messages***: messaggi <u>inviati da un oggetto a se stesso</u>,
- **Sync/async**: <u>sincroni</u> (sender si blocca finche non riceve risposta) o <u>asincroni</u> (non bloccanti),
- **Call/signal**: <u>call</u> (messaggio diretto ad altri oggetti) o <u>signal</u> (messaggi inviati da un *publisher* ai *subscriber*, oggetti iscritti all'evento per cui ricevono il *signal*),
- **Lost/found**: <u>lost</u> (non arrivano al destinatario stabilito o non se ne conosce il destinatario) o <u>found</u> (arrivano da un mittente sconosciuto o non nel diagramma).

> [!info] Nota
> Le frecce dei messaggi sincroni e asincroni sono rispettivamente:
> ![](https://i.imgur.com/LrzaJYR.png)
> Mentre le frecce di risposta (e di invio senza risposta?) sono generalmente tratteggiate:
> ![](https://i.imgur.com/DqUoK7A.png)

###### Object lifeline

Gli oggetti possono essere creati o distrutti con frecce particolari che indicano l'azione che si compie sopra esse:

![](https://i.imgur.com/QCYVKQQ.png)

Esempio (la conferma o il rifiuto della richiesta la eliminano): 

![](https://i.imgur.com/9AWFdfc.png)

##### Combined fragments

Negli *interaction diagrams* è possibile utilizzare anche delle strutture dati simili a quelle dei linguaggi di programmazione dette ***combined fragments***:

###### Alternatives

L'operatore `alt` è come un `if` e, in base ad una condizione nella ***guard*** (tra \[]), indica che al max uno dei 2 comportamenti verrà scelto. Per `alt` è necessaria una condizione nella prima *guard*, mentre nella seconda basta specificare `else` (non ho trovato esempi che trattavano `alt` on più di 2 *brackets* come se avesse degli `else-if`):

![](https://i.imgur.com/DFGSTNw.png)

###### Options

L'operatore `opt` è come un `if` con solo la prima condizione (quindi senza `else`), in base alla condizione nella *guard* indica se l'azione al suo interno è fatta o saltata:

![](https://i.imgur.com/k7ChS5J.png)

###### Loop (e break)

L'operatore `loop` indica che le operazioni all'interno del *fragment* saranno ripetute un certo numero di volte o finché è soddisfatta una condizione:

![](https://i.imgur.com/ODnbvMU.png)

In `loop` è anche possibile specificare una condizione di uscita arbitraria con `break`, che è identico al `break` dei linguaggi di programmazione:

![](https://i.imgur.com/HHv9RAf.png)

###### Parallel

L'operatore `par` è usato per indicare che le azioni al suo interno possono essere eseguite parallelamente ed in qualsiasi ordine (con 2 notazioni):

![](https://i.imgur.com/ZZ2Ijls.png)

###### Esempi

![](https://i.imgur.com/iQs3b2o.png)

Nota: quelli che hai visto qui sopra (`opti`) e l'azione "prenota" sotto si dicono `gate`: punti di input o output di dati da/verso l'esterno del sistema (infatti sono esterni ai confini)

![](https://i.imgur.com/ssnOvW0.png)

![](https://i.imgur.com/l3dJ53N.png)

###### Altri operandi

Si possono trovare gli altri operandi [qui](https://www.uml-diagrams.org/sequence-diagrams-combined-fragment.html).

##### Temporizzazione

Gli *interaction diagrams* sono **temporizzabili** in caso sia importante specificare vincoli e durate delle azioni a livello di tempo. I seguenti temporizzano attraverso vincoli (tra {}):

![](https://i.imgur.com/m16PLG6.png)

Mentre i prossimi sono un po' più complessi:

![](https://i.imgur.com/hC80cb8.png)

![](https://i.imgur.com/kvg9kyf.png)

Comunque per la temporizzazione si vedrà tutto meglio con i ***timing diagrams***.

#### Communication diagrams

(O *collaboration diagrams*) sono simili ai precedenti ma sono meno "*constrained*", nel senso che non associano il tempo ad una dimensione precisa e sono un po' più "liberi" (estendibili in qualsiasi direzione delle 2 dimensioni). Le sequenze si indicano con la numerazione (come anche le alternative ma magari con colori diversi) e questi diagrammi sono sostanzialmente più adatti per casi con concorrenza (thread) e chiamate innestate/ricorsive.

Viene mantenuta la maggior parte degli aspetti grafici dei *[[#Sequence diagrams|sequence diagrams]]*.

###### Esempi

![](https://i.imgur.com/NeuvuTf.png)

![](https://i.imgur.com/u48ZQ6G.png)

![](https://i.imgur.com/RSAGWMo.png)

---

Prossima lezione: [[12 - Class diagrams]]

