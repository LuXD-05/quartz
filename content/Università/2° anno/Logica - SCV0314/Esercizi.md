# Esercizio 1

### Albero di parsing

Data una formula $P$ rappresentarne l'**albero di parsing**, formato così:

\- $P$ è la radice dell'albero,

\- Se il connettivo principale di un nodo è **binario** ($\land$, $\lor$, $\rightarrow$) $\;\;\;\rightarrow\;\;\;$ aggiungere al nodo <u>2 figli</u>: <u>sx</u> = la parte sx del connettivo e <u>dx</u> = quella dx (splittare il nodo sul connettivo),

\- Se il connettivo principale di un nodo è **unario** ($\lnot$) $\;\;\;\rightarrow\;\;\;$ aggiungere al nodo 1 figlio contenente la stessa formula negata (negare il nodo: $\lnot Y \rightarrow Y$),

\- I nodi con variabili proposizionali pure senza connettivi sono le **foglie**.

![181](https://i.imgur.com/CFOZIMj.png)

![314](https://i.imgur.com/AD0CpF0.png)

![367](https://i.imgur.com/Vlj2K08.png)

![309](https://i.imgur.com/JlH6DMW.png)

### Induzione strutturale

##### Sottoformule

Data una formula $P$, definirne l'unsieme delle sottoformule $Sub(P)$, fatto così:

\- Se $\;\;P = P_{1} \land P_{2}\;$ | $\;P = P_{1} \lor P_{2}\;$ | $\;P = P_{1} \rightarrow P_{2} \;\;\;\rightarrow\;\;\; Sub(P) = Sub(P_{1}) \cup Sub(P_{2}) \cup \{P\}$,

\- Se $\;\;P = \lnot P_{1} \;\;\;\rightarrow\;\;\; Sub(P) = Sub(P_{1}) \cup \{P\}$,

\- Se $\;P\;$ è una variabile proposizionale (pura, senza connettivi) $\;\;\;\rightarrow\;\;\;$ $Sub(P) = \{P\}$.

![443](https://i.imgur.com/FmVMG3C.png)

![455](https://i.imgur.com/0p7s9bC.png)

##### Lunghezza $|P|$

Data una formula $P$, la sua **lunghezza** $|P|$ è il <u>n° di connettivi</u> che compaiono in $P$, così definita:

\- Se $\;\;P = P_{1} \land P_{2}\;$ | $\;P = P_{1} \lor P_{2}\;$ | ${} \;P = P_{1} \rightarrow P_{2} \;\;\;\rightarrow\;\;\; |P| = |P_{1}| + |P_{2}| + 1 {}$,

\- Se $\;\;P = \lnot P_{1} \;\;\;\rightarrow\;\;\; |P| = |P_{1}| + 1$,

\- Se $\;P\;$ è una variabile proposizionale (pura, senza connettivi) $\;\;\;\rightarrow\;\;\;$ $|P| = 0$.

![321](https://i.imgur.com/sLNY2Pl.png)

![391](https://i.imgur.com/1HQOpJa.png)

![311](https://i.imgur.com/xxGXPcn.png)

### Tavole di verità

Fare una valutazione di una certa formula $P$ con le tavole di verità, coi seguenti step:

\- Porre ogni variabile singola della formula in testa ad una tavola di verità,

\- Riempire le colonne (con 0 e 1 alternati) in modo da formare tutte le combinazioni logiche,

\- Scomporre $P$ riempiendo una colonna della tavola di verità per ogni sottoformula; questo in ordine "dall'interno" (singoli $\lnot$, formule in parentesi interne, eccetera),

\- Continuare fino ad arrivare ai valori di verità dell'intera formula.

![308](https://i.imgur.com/8jCsqWs.png)

![222](https://i.imgur.com/0CjLSTr.png)

![253](https://i.imgur.com/JEAqqKK.png)

##### Soddisfacibilità

Determinare se una formula è:

\- **Soddisfacibile** (si scrive $v \models P$): se esiste <u>1 riga</u> della sua <u>tavola di verità ad 1</u> (se esiste una valutazione delle sue variabili $v$ tale che $v(P) = 1$),

\- **Tautologia** (si scrive $\models P$): se <u>tutte le righe</u> della sua <u>tavola di verità</u> sono <u>ad 1</u> (se tutte le valutazioni delle sue variabili $v$ sono tali che $v(P) = 1$),

\- **Contraddizione**: se <u>tutte le righe</u> della sua <u>tavola di verità</u> sono <u>a 0</u> (se tutte le valutazioni delle sue variabili $v$ sono tali che $v(P) = 0$).

(esercizi precedenti)

![364](https://i.imgur.com/oJPgH0P.png)

![302](https://i.imgur.com/bgsAEqn.png)

###### Insieme soddisfacibile

Un insieme di formule $\Delta$ (tipo $\{A \lor B, \lnot B \land C\}$) si dice <u>soddisfacibile</u> se esiste almeno 1 riga nella tavola di verità composta in cui entrambe le celle sotto le formule sono 1.

Nelle conseguenze logiche si chiamano **premesse**.

##### Conseguenza logica

Determinare se un'insieme di (1 o più) formule (<u>premesse</u>, a sinistra di $\models$) ne <u>implica logicamente</u> un'altra $P$, così:

\- Si fa la tavola di verità sempre con le variabili singole riempite,

\- Si calcola 1 colonna per premessa per capire se è un'insieme soddisfacibile ($\Delta$) + la colonna di $P$,

\- Se <u>nessuna riga è soddisfacibile</u> (per $\Delta$) oppure se <u>per tutte le righe soddisfacibili</u> anche $P$ ha <u>valore 1</u> (in tale riga) $\;\implies\;$ conseguenza **VERA**

\- Se <u>anche solo 1 riga soddisfacibile</u> (per $\Delta$) ha che $P$ ha <u>valore 0</u> in tale riga $\;\implies\;$ conseguenza **FALSA**

![440](https://i.imgur.com/zqLzHzu.png)

![442](https://i.imgur.com/qQTADaZ.png)

##### Equivalenza logica

Determinare se 2 formule sono <u>logicamente equivalenti</u> ($\equiv$), così:

\- Si fa sempre la tavola di verità fino a trovare i valori per le formule dell'equivalenza,

\- Se i valori di verità delle 2 formule sono uguali, l'equivalenza è VERA, altrimenti FALSA.

![458](https://i.imgur.com/MskYMKp.png)

![437](https://i.imgur.com/XSlx08F.png)

# Esercizio 2

### DNF/CNF

Trasformare una formula in **forma normale** (DNF o CNF), e si fa così:

\- Eliminare tutte le implicazioni ($\rightarrow$) con la seguente <u>equivalenza logica</u>: $X \rightarrow Y \equiv \lnot X \lor Y$ (x ogni implicazione sostituirla con $\lor$ e negare la 1a variabile),

\- Risolvere le parentesi negate con <u>De Morgan</u> (ovvero: $\lnot(\ldots)$) portando il $\lnot$ sulle variabili singole,

\- Trasformare in **DNF** (OR di AND) o **CNF** (AND di OR) usando la distributività (e in base a cosa richiesto).

![474](https://i.imgur.com/bx4pbem.png)

![339](https://i.imgur.com/ZOjfjML.png)

##### Con le tavole di verità

Data una tavola di verità, trovare la rispettiva formula in forma normale (DNF o CNF) così:

\- **DNF**: per ogni riga dove $P$ (risultato) è 1 $\;\rightarrow\;$ fare un $\land$ delle variabili, che saranno $\;\rightarrow\;$ $X$ se nella riga c'è 1 e $\lnot X$ se nella riga c'è 0 e $\;\rightarrow\;$ infine concatenare con $\lor$ tali $(\land)$.

\- **CNF**: per ogni riga dove $P$ (risultato) è 0 $\;\rightarrow\;$ fare un $\lor$ delle variabili, che saranno $\;\rightarrow\;$ $X$ se nella riga c'è 0 e $\lnot X$ se nella riga c'è 1 e $\;\rightarrow\;$ infine concatenare con $\land$ tali $(\lor)$.

![294](https://i.imgur.com/s4aVH6E.png)

###### Alfa e beta formule

In base al loro simbolo logico principale, le formule possono essere le seguenti (tali in quanto scomponendo le $\alpha$-formule si hanno $\land$ principali e $\lor$ per le $\beta$-formule):

![478](https://i.imgur.com/eSqW1De.png)

Di queste i **ridotti** sono gli elementi che si hanno riducendo la formula col metodo dei tableaux, ma ci sono altre regole:

- Per le $\alpha$-formule: ridurre significa aggiungere un nodo figlio con i ridotti separati da ",".
- Per le $\beta$-formule: ridurre significa aggiungere 2 nodi figli con 1) uno la <u>parte a sx</u> del $\lor$ + <u>resto dei ridotti</u> e 2) l'altro la <u>parte a dx</u> del $\lor$ + <u>resto dei ridotti</u> (duplicati nei nodi).

### Tableaux proposizionale

Controllare se una formula $P$ è soddisfacibile con il metodo dei tableaux:

\- Scrivere la formula per intero come radice di un albero,

\- Partire dal connettivo principale e ridurre (se possibile ridurre sempre prima le $\alpha$-formule),

\- Arrivando alle foglie, quelle contenenti <u>coppie di variabili complementari</u> (tipo: $X, \ldots \lnot X$) si dice che il suo ramo è **chiuso**, altrimenti è **aperto**,

\- $P$ è **soddisfacibile** (risolvibile) se <u>almeno 1</u> dei suoi <u>rami</u> è <u>aperto</u>, **insoddisfacibile** se <u>tutti</u> i suoi <u>rami</u> sono <u>chiusi</u> e **tautologia** se $\lnot P$ ha <u>tutti i rami chiusi</u>.

![382](https://i.imgur.com/cAu78PS.png)

![404](https://i.imgur.com/RuzifSL.png)

##### Conseguenza logica con tableaux

Controllare se una conseguenza logica è vera o no con il metodo dei tableaux (trovare se le premesse soddisfano la conclusione negata: $\Gamma \models \lnot P$):

\- Scrivere la conseguenza logica come nodo radice di un albero,

\- Risolvere (ridurre) $\models$ sostituendolo con $,$ e <u>negando</u> la parte <u>destra</u> della conseguenza logica,

\- Derivare tutti i rami ($\alpha$-formule e $\beta$-formule) come per i tableaux,

\- Se anche 1 ramo è aperto, la conseguenza logica è <u>falsa</u> (non risolvibile), altrimenti se tutti chiusi è <u>vera</u> (si sta cercando se esiste o no un controesempio)

![369](https://i.imgur.com/AO29bly.png)

###### Da tableaux a DNF

Rispetto alla DNF:

\- Ogni ramo <u>aperto</u> corrisponde a una clausola congiuntiva (AND) della DNF ($\;X, \lnot Y \;\rightarrow\; (X \land \lnot Y)\;$),

\- La DNF si ottiene unendo tutte le clausole derivate da rami aperti con OR ($\lor$).

Rispetto alla CNF:

\- Fare il tableau di $\lnot P$ invece che di $P$,

\- Fare la DNF coi rami aperti di tale albero,

\- La CNF di $P$ si ottiene negando tutto con De Morgan.

![357](https://i.imgur.com/OrvPwDv.png)

# Esercizio 3

###### Clausole

Una **clausola** è una <u>disgiunzione di letterali</u> (variabili connesse da $\lor$) visibili come letterali separati da $,$ come in <u>notazione insiemistica</u> (tipo: $\;(X \lor Y) \lor \lnot Z = \{X, Y, \lnot Z\}\;$).

Un'**insieme di clausole** è semplicemente una CNF di tali insiemi (tipo: $\;\{\; \{X, \lnot Y\}, \{Z, \lnot X, Y\} \;\}\;$); dove le $,$ che separano gli insiemi sono derivate dagli $\land$ della CNF.

Il simbolo $\square$ indica una <u>clausola vuota</u> ($\{\}$), mentre $\varnothing$ rappresenta un'<u>insieme vuoto di clausole</u>.

> [!info] Soddisfacibilità
> Una clausola $C$ è <u>insoddisfacibile</u> se è $\square$, <u>soddisfacibile</u> se contiene almeno 1 letterale e <u>tautologia</u> se contiene 2 letterali complementari $L$ e $\lnot L$ (queste si <u>cancellano sempre</u> perché danno sempre 1 e negli insiemi fare $C \land 1 = C$).
> Un insieme di clausole è <u>soddisfacibile</u> se c'è una combinazione di valutazioni che rende tutte le clausole vere (anche se tutte le clausole sono complementari, il che da $\varnothing$, che *sarebbe* tautologia ma rientra in "soddisfacibile" qui), se no <u>insoddisfacibile</u>.

###### Valutazioni

Una valutazione $v$ è una <u>riga di tavola di verità</u>, ovvero una funzione che attribuisce ad ogni variabile di una clausola un valore di verità 0 o 1, e ci sono 3 regole:

1\) Un **letterale** $X$ è <u>vero</u> se la sua valutazione $v(X) = 1$, e <u>falso</u> se $v(X) = 0$ (mentre $\lnot X$ è <u>vero</u> se $v(\lnot X) = 0$, e <u>falso</u> se $v(\lnot X) = 1$),

2\) Una **clausola** $C$ è <u>vera</u> se <u>almeno 1 dei suoi letterali è vero</u> (siccome le clausole sono letterali separati da $\lor$),

3\) Un'**insieme di clausole** $S$ è <u>vero</u> se <u>tutte le sue clausole sono vere</u> (siccome gli insiemi di clausole sono clausole separate da $\land$).

> [!example] Casi particolari
> \- La clausola vuota $\square$ è sempre <u>insoddisfacibile/falsa</u> (clausola = ${} \lor$, che tra 0 valori corrisponde al suo <u>elemento neutro</u> che è 0).
> \- Ogni insieme di clausole che contiene $\square$ è <u>insoddisfacibile/falso</u> (per la regola 3).
> \- L'insieme vuoto di clausole $\varnothing$ è sempre <u>soddisfacibile/vero</u> (insieme = $\land$, che tra 0 valori corrisponde al suo <u>elemento neutro</u> che è 1).

###### Risolvente

Date 2 clausole $C_{1}$ e $C_{2}$, se tali hanno un letterale $L$ tale che $L \in C_{1}$ e $\lnot L \in C_{2}$, allora il **risolvente** $R$ di $C_{1}$ e $C_{2}$ (rispetto a $L$) è $(C_{1} \setminus \{L\}) \cup (C_{2} \setminus \{\lnot L\})$, ovvero una clausola composta da tutti i letterali <u>distinti</u> in $C_{1}$ e $C_{2}$ <u>eccetto</u> $L$ e $\lnot L$.

Esempio: dati $\{X, A\}$ e $\{\lnot X, B\}$ il risolvente è $R = \{A, B\}$.

> [!important] Correttezza della risoluzione
> Il risolvente $R$ è <u>conseguenza logica</u> delle clausole $\{ C_{1}, C_{2} \}$ (ovvero: $\{ C_{1}, C_{2} \} \models R$).
> Quindi $\{ C_{1}, C_{2} \} \equiv \{ C_{1}, C_{2}, R \}$. Ciò è come aggiungere una colonna $R$ in $\land$ al resto della tavola di verità, implicando che le valutazioni <u>non cambiano</u>.

###### Derivazione per risoluzione

Determinare se $P$ è soddisfacibile tramite <u>derivazione per risoluzione</u>:

\- Trasformare $P$ in un insieme di clausole,

\- Selezionare 2 clausole contenenti letterali complementari, eliminare tali letterali (1 coppia x volta), unire i letterali rimanenti in un risolvente e aggiungerlo all'insieme,

\- Bisogna continuare così con qualsiasi possibile combinazione di letterali finché non si ha una **refutazione** ($\square$), se <u>non la si trova</u> vuol dire che $P$ è <u>soddisfacibile</u>.

> [!info] Refutazione
> La **refutazione** è una derivazione particolare che produce $\square$ (fatta con 2 clausole aventi una un letterale $L$ e l'altra il suo opposto $\lnot L$).
> Se $R$ contiene $\square$ allora $P$ è <u>insoddisfacibile/falsa</u> (per la **correttezza della risoluzione**).

###### Sussunzione

Date 2 clausole $C \neq G$, se $C \subseteq G \;\rightarrow\;$ si dice che $C$ <u>sussume</u> $G$ ("sussume" = "è contenuto in").

**Regola**: si possono <u>eliminare</u> da un insieme (di clausole) <u>tutte le clausole sussunte da altre</u> (se $S = \{G, C\}$ e $G = \{C, \,\ldots\}$, allora $\{G,C\} \equiv \{C\}$).

### Davis-Putnam

Verificare se l'insieme di clausole $S$ è soddisfacibile con Davis-Putnam, così:

\- Eliminare tutte le clausole che sono <u>tautologie</u> ($\{L, \lnot L, \ldots\}$, eliminare tutta la clausola, non solo i letterali opposti),

\- Eliminare tutte le clausole <u>sussunte</u>,

\- Scegliere un ***pivot***, ovvero variabile $L$ che appare nella clausola più corta (con più clausole di pari cortezza, andare in ordine alfabetico),

\- Spostare da $S$ ad un nuovo insieme $S_{1}$ tutte le clausole $L$-esonerate (che non contengono $L$ o $\lnot L$),

\- Aggiungere ad $S_{1}$ (in una singola clausola?) tutti i <u>risolventi</u> (rispetto a $L$) di $S$ (senza le clausole $L$-esonerate appena spostate in $S_{1}$),

\- Ripartire dall'inizio con $S_{1}$ (dopo aver rifatto i primi 2 step si avrà eliminato $L$ dall'insieme originale).

\- Alla fine, se le clausole sono <u>tutte tautologie</u>, si ottiene $\square$ (caso $S$ = <u>insoddisfacibile</u>) oppure se rimangono <u>letterali senza l'opposto</u> si ottiene $\varnothing$ (caso $S$ = <u>soddisfacibile</u>).

###### Trovare una valutazione

Se $S$ è soddisfacibile dopo Davis-Putnam, può venir chiesto di trovare una **valutazione** (trovare dei valori da dare alle clausole per fare in modo che siano <u>tutte vere</u> in CNF):

\- Dare a tutte le variabili rimaste al penultimo step di Davis-Putnam (eccetto l'ultimo pivot scelto) un valore di verità arbitrario (1 o 0),

\- Risalire 1 alla volta gli insiemi di clausole precedenti sostituendo i valori assegnati alle variabili del punto precedente,

\- Risolvere 1 alla volta tali insiemi di clausole sostituiti facendo in modo che ogni clausola sia vera (almeno un letterale/valore sia = 1) finché non si fa con tutte.

Potrebbe anche venir data una valutazione e chiedere se essa è valida per $S$, caso in cui bisogna solo sostituire i valori alle variabili date (se tutto 1 valida se no invalida).

> [!info] Casi di risoluzione (in *backtracking*)
> Quando si risolvono le clausole a cui alcuni letterali sono sostituiti da valori, ci sono diversi casi (siccome l'insieme è una CNF dove le clausole in $\land$ hanno i letterali in $\lor$):
> \- **C'è già un 1** ($\{0, 1, A\}$): per queste <u>non importa</u> che <u>valore</u> assumono i <u>letterali</u> (tipo $A$), siccome la clausola è già <u>vera</u>,
> \- **Solo letterali con eventuali 0** ($\{0, A, B\}$): per queste il valore di <u>almeno un letterale deve per forza essere 1</u> (per fare in modo che la clausola sia <u>vera</u>),
> \- **Solo 0**: è stato <u>sbagliato un passo precedente</u>, altrimenti la formula è <u>insoddisfacibile</u> (e se Davis-Putnam da soddisfacibile, allora è sbagliato Davis-Putnam).

##### In DIMACS

**DIMACS** è il formato di testo standard usato dai computer per interpretare formule in CNF; e i programmi che leggono tale formato sono i ***SAT solvers*** il cui unico scopo è prendere una formula DIMACS in input e ritornare `SAT` (soddisfacibile) o `UNSAT` (insoddisfacibile). Esempio:

![526](https://i.imgur.com/pBWvtwy.png)

In pratica ogni codice DIMACS inizia con la *problem line* (con variabili e clausole), le righe di clausole poi hanno dei numeri (da 1) corrispondenti a letterali distinti (positivi di base, altrimenti negativi col $-$ davanti) e terminano con 0 (per semplicità $1 = A, 2 = B \ldots$).

Per gli esercizi basta ricostruire l'insieme di clausole sostituendo un letterale per numero alle clausole DIMACS.

# Esercizio 4

###### Intro predicati

Nella logica dei predicati, invece di variabili $X$ e $Y$ che possono valere 0 o 1, ci sono:

\- **Termini**: (di una formula) che possono essere <u>costanti</u> ($a, b, c$... minuscole), <u>variabili</u> ($x, y, z$... minuscole) o <u>funzioni</u> ($f(x)$ che prendono 1 termine e ne ritornano un altro).

\- **Predicati**: (tipo $A, B, C$... maiuscole) che rappresentano <u>proprietà</u> (tipo: $A(x)$ = "$x$ ha proprietà $A$" o $B(x,y)$ = "$x$ e $y$ sono legati dalla proprietà $B$").

\- **Quantificatori**: che sono $\forall x$ ("per ogni $x$") o $\exists x$ ("esiste almeno un $x$").

$\phi$/$\psi$ = formule

$\forall x \psi$, $\psi$ = <u>campo d'azione</u> del quantificatore ($x$ è <u>vincolata</u> se appare nel campo d'azione del quantificatore, se no <u>libera</u>)

Formula senza variabili libere si dice <u>chiusa</u>.

$\forall x A(x) \equiv \lnot \exists x \lnot A(x)$

${} \exists x A(x) \equiv \lnot \forall x \lnot A(x) {}$

($FV(\phi)$) ?

Strutture:

![530](https://i.imgur.com/bZhAL5e.png)

![493](https://i.imgur.com/PzKsU0I.png)

Valutazioni e soddisfacibilità?

###### Forma normale prenessa

Una formula è in **FNP** (*Forma Normale Prenessa*) se i suoi **quantificatori** sono tutti <u>all'inizio</u> di essa e si può trasformare in FNP qualsiasi formula con equivalenze logiche

Di una formula in FNP ($\mathcal{Q}_{1}x_{n} \,\ldots\, \mathcal{Q}_{n}x_{n}\psi$) si ha che $\mathcal{Q}_{i}$ = $\forall$ o $\exists$, mentre $\psi$ contiene il resto della formula e si chiama **matrice**. Trasformare in FNP:

\- Trasformare le implicazioni ($\rightarrow$) così: $A \rightarrow B \;\equiv\; \lnot A \lor B$,

\- Spostare i $\lnot$ <u>dai quantificatori alla matrice</u> (nessun $\lnot$ su $\mathcal{Q}$),

\- Rinominare le variabili seguite da ogni quantificatore in modo che ognuno di essi ne abbia una diversa,

\- Spostare i quantificatori davanti a tutto (mantenendone l'ordine da sinistra a destra della formula).

![413](https://i.imgur.com/q8qMesT.png)

Importante lo scope dei quantificatori (parentesi a cui sono davanti), infatti una cosa così è permessa: $\forall x (\lnot B(x) \lor \exists y C(x,y))$

###### Forma di Skolem

Una formula $\phi$ è in **forma di Skolem** ($\phi^{S}$) se <u>è in FNP</u> e <u>non contiene quantificatori</u> $\exists$. Data $\phi$, la *skolemizza* così:

\- Caso $\exists$ all'inizio: sostituire ogni occorrenza della variabile di $\exists_{1}$ (supponiamo $x_{1}$) con una costante di Skolem $c$ e cancellare ${} \exists_{1} {}$.

\- Caso $\exists$ dopo un $\forall$: sostituire ogni occorrenza della variabile di $\exists_{i}$ (supponiamo $x_{i}$) con una funzione di Skolem $f(x_{1} \,\ldots\, x_{i-1})$ e cancellare $\exists_{i}$.

> [!important] Equisoddisfabicilità
> $\phi$ è soddisfacibile solo se $\phi^{S}$ è soddisfacibile.

###### Universo di Herbrand

Data una formula chiusa $\phi$ in forma di Skolem, l'**universo di Herbrand** $H(\phi)$ di $\phi$ è l'insieme di <u>termini ground</u> (senza variabili) costruibili usando <u>costanti e funzioni</u> di $\phi$:

\- Se $\phi$ ha <u>costanti</u>, scrivere quelle in $H(\phi)$, altrimenti inventarsene 1 (letteralmente): $H(\phi) = \{ b, c \}$,

\- Se $\phi$ <u>non ha funzioni</u> è finita lì ($H(\phi) = \{b,c\}$), altrimenti $H(\phi)$ si espande all'infinito riapplicando ogni funzioni ripetutamente ($\{b,c,f(b),g(b),f(c),g(c),f(f(b))\ldots\}$).

###### Struttura di Herbrand

Una struttura $\mathcal{A} = (D,I)$ dove $D$ è il <u>dominio</u> (elementi presi in considerazione) e $I$ è la <u>funzione di interpretazione</u> (mappa i simboli della formula sul dominio) si dice **struttura di Herbrand** per $\phi$ se:

\- Il dominio è l'universo di Herbrand di $\phi$ ($D = H(\phi)$, ovvero le stringhe: "b", "c", "f(c)"... in $\{b,c,f(b),g(b),f(c),g(c),f(f(b))\ldots\}$),

\- Costanti e funzioni sono mappate su se stesse ($I(c) = c$, $I(f(\ldots)) = f(\ldots)$),

\- La funzione di interpretazione di ogni proprietà contiene solo costanti/funzioni appartenenti ad $H(\phi)$ ($I(P) \subseteq H(\phi)$)

\+ Variabili e costanti di una proprietà $P$ in $I(P)$ si dice che sono <u>vere</u>, altrimenti <u>false</u>.

> [!important] Teorema di Herbrand
> Una formula $\phi$ <u>chiusa</u> in <u>forma di Skolem</u> è soddisfacibile solo se ha un **modello di Herbrand** (una struttura di Herbrand che la soddisfa, ovvero i cui insiemi $I$ di ogni proprietà contengono una giusta combinazione di costanti per fare in modo che il risultato logico finale della funzione sia <u>vero</u>).
> Esempio:
> ![](https://i.imgur.com/uUjAmHV.png)

### Modelli di Herbrand

Costruire un modello di Herbrand per la formula ${} \phi$ (+ eventuali altre condizioni):

\- Portare la formula in <u>forma di Skolem</u>,

\- Trovare l'universo di Herbrand $H(\phi)$ per la formula,

\- Definire la <u>funzione di interpretazione</u> <u>per ogni predicato</u> facendo in modo che rispetti le eventuali condizioni imposte,

\- Verificare (sostituendo ai predicati i valori nei loro insiemi $I$) se $\phi$ è <u>vera</u> per tutte le combinazioni di elementi sostituite ai suoi predicati.

(Tip: guardare i connettivi della formula, tipo un $\rightarrow$ principale indica che, affinché la roba a sinistra sia 0, la roba a destra può anche essere $\varnothing$, ovvero non importa cosa sia).

![524](https://i.imgur.com/jmbaOIu.png)

![526](https://i.imgur.com/ZppLIva.png)

![522](https://i.imgur.com/SSNB13Y.png)

![523](https://i.imgur.com/9O1R5JA.png)

###### Espansione di Herbrand

L'**espansione di Herbrand** $E(\phi)$ di una formula è l'insieme di tutte le <u>istanze concrete di essa</u>, e ciò si fa così:

\- Si tolgono tutti i $\forall$,

\- Creare tante <u>istanze concrete della formula</u> **sostituendo** alle <u>variabili all'interno di proprietà</u> le costanti/funzioni nell'insieme $I$ di tali rispettive proprietà.

![](https://i.imgur.com/k0p0dmN.png)

> [!important] Teorema di Herbrand 2
> Una formula $\phi$ è <u>soddisfacibile</u> solo se <u>tutte le formule</u> in $E(\phi)$ sono vere (soddisfacibili).

![616](https://i.imgur.com/w1Vqd37.png)

# Esercizio 5

###### Gamma e delta formule

Oltre alle $\alpha$/$\beta$-formule, per i tableaux nella logica dei predicati ci sono anche le $\gamma$-formule ($\forall$ o $\lnot\exists$) e le $\delta$-formule ($\exists$ o $\lnot\forall$); i cui ridotti:

\- Per le $\delta$-formule: aggiungere 1 nodo figlio con i ridotti <u>senza il quantificatore</u> e sostituire ad ogni variabile del quantificatore (nel suo scope) una costante <u>nuova</u> (non già presente in formula) <u>unica per variabile</u>,

\- Per le $\gamma$-formule: aggiungere 1 nodo figlio con i ridotti <u>senza il quantificatore</u> e sostituire ad ogni variabile del quantificatore (nel suo scope) una costante <u>già presente in formula</u> (qualsiasi, dovunque sia, solo se non presente ne si inventa una tipo $a$).

![](https://i.imgur.com/PUbjIQ4.png)

$\psi$ è semplicemente il resto della formula dopo il quantificatore, mentre \[$a$/$x$] indica che si sostituisce $a$ a tutte le occorrenze di $x$ nella formula (ad ogni variabile diversa di un quantificatore si assegna una costante unica diversa, tipo $x$ e $y$ diventano $a$ e $b$).

Ordine e precedenza: seguire le parentesi (tipo prima quantificatori davanti a tutto e poi resto, da esterno all'interno) e poi $\alpha$, $\delta$, $\beta$, $\gamma$.

> [!important] Soddisfacibilità
> (più o meno come per i tableaux proposizionali (conseguenza logica), rami <u>chiusi = falsi</u> e rami <u>aperti = veri</u>).
> Per dimostrare che una formula $\phi$ è valida, bisogna dimostrare che $\lnot\phi$ sia insoddisfacibile (verificare se ha tutti i rami chiusi/falsi).

###### Modelli

Alcuni esercizi chiedono se una formula $\phi$ è <u>invalida</u> e di trovare un "***modello** per la sua negazione*". Tale modello ${} \mathcal{M} {}$ è molto simile a uno di Herbrand $\mathcal{A} = (D, I)$, solo che:

\- Per ogni <u>ramo aperto distinto</u> della formula bisogna creare un modello $\mathcal{M}_{n}$ con un certo dominio e una certa funzione di interpretazione,

\- Il **dominio** di un ramo è composto dalle <u>costanti della formula in esso</u>,

\- La **funzione di interpretazione** si fa sempre <u>per ogni proprietà</u> del ramo al fine di trovare una combinazione che lo renda <u>vero</u> o <u>falso</u> (in base alla richiesta).

> [!info] Note
> Se è chiesto un modello per la formula $\phi$, allora essa:
> 1\) Non va negata all'inizio (poi si fa tableaux normalmente),
> 2\) Se tutta chiusa non ci sono modelli che ne confermano la validità,
> 3\) Se anche 1 ramo aperto, la $I$ del modello che si cerca per quel ramo deve avere valori tali che il ramo risulti <u>vero</u>.
> Ci sono varie variazioni di sti esercizi dove non si nega (gli altri si negano, dipende sempre se devi dimostrare validità o il contrario):
> ![](https://i.imgur.com/zvX9XuN.png)
> Alcuni rami <u>aperti</u> possono avere termini infiniti:
> ![](https://i.imgur.com/b2zJJDF.png)

### Tableaux predicativi

Determinare se una formula $\phi$ è valida/invalida con il metodo dei tableaux:

\- Se chiede di dimostrare che è <u>valida</u> si procede, se invece chiede se è <u>invalida</u> è meglio avere $\lnot\phi$ come radice (per dimostrare che il contrario di $\phi$ è tutto valido, se anche 1 ramo aperto in $\lnot\phi \;\rightarrow\; \lnot\phi$ è <u>valida</u> $\;\rightarrow\; \phi$ <u>invalida</u>).

\- Ridurre la formula in ordine di come è scritta tra tutte le $\alpha, \delta, \beta, \gamma$ formule,

![466](https://i.imgur.com/GXCWSnM.png)

![473](https://i.imgur.com/0TwtEMm.png)

###### Trovare modelli

(Gli esercizi potrebbero anche chiedere di) trovare un modello che determina la validità/invalidità della formula, seguendo questi [[#Modelli|step]].

##### Conseguenza logica con tableaux

Controllare se una conseguenza logica è vera o no con il metodo dei tableaux (trovare se le premesse soddisfano la conclusione negata: $\Gamma \models \lnot\phi$):

\- Scrivere la conseguenza logica come nodo radice di un albero,

\- Risolvere (ridurre) $\models$ sostituendolo con $,$ e <u>negando</u> la parte <u>destra</u> della conseguenza logica,

\- Derivare tutti i rami usando l'ordine di priorità delle formule $\alpha, \delta, \beta, \gamma$ (come per esercizi normali dei tableaux)

\- Se anche <u>1 ramo è aperto</u>, la conseguenza logica è <u>falsa</u> (+ quel ramo fornisce il modello che la rende falsa), altrimenti se <u>tutti chiusi</u> è <u>vera</u> (non esistono controesempi).

![](https://i.imgur.com/EXxdsCy.png)

# Esercizio 6

###### Sostituzioni

Per fare delle risoluzioni tra clausole si trova il <u>risolvente</u> per una variabile al loro interno che in una è positiva e nell'altra è negata (tipo: $\{\{A, B\},\{\lnot A\}\} = \{B\}$). In logica dei predicati i letterali hanno variabili e costanti per cui possono differire, quindi al fine di fare risoluzioni bisogna effettuare <u>sostituzioni</u> (tipo: $\sigma = \{c/x\}$, dove le $x$ diventano $c$).

###### Unificatori e MGU

Un **unificatore** (per un'insieme di clausole $E$) è 1 o più sostituzioni $\sigma$ che, se applicate ad $E$, $E\sigma$ ha 1 solo elemento (ovvero se rende uguali tutti gli elementi di $E$).

![](https://i.imgur.com/TP8UOrs.png)

L'**MGU** (*Most General Unifier*) è l'<u>insieme più generale</u> (non introduce vincoli inutili) <u>di sostituzioni</u> che bisogna fare per rendere un <u>letterale uguale a un altro</u>.

###### Algoritmo di Robinson

L'**algoritmo di Robinson** permette di trovare l'**MGU**, così:

\- Identificare il ***disagreement set***: scannerizzare <u>tutte le clausole</u> di un insieme $E$ (al contempo) e inserire in $D(E)$ i primi termini (dei letterali) da sx a dx che vi differiscono,

\- Sostituire ad un termine di $D(E)$ (a scelta) un altro nella formula iniziale (in base a certe <u>regole</u>) e se il controllo passa si aggiunge la sostituzione (tipo $\{t/x\}$) a ${} \sigma$,

\- Ripetere il punto precedente (sempre da sx a dx) finché non ci sono più "*disagreements*".

(Ricordarsi di mantenere l'insieme delle sostituzioni $\sigma$ che in caso passa va restituito o usato per le risoluzioni).

> [!important] Regole di sostituzione
> Ci sono certi casi in cui il controllo x la sostituzione non passa:
> \- **Termini uguali**: se in $D(E)$ ci sono 2 costanti diverse o 2 funzioni diverse (fallimento),
> \- ***Occur check***: se in $D(E)$ c'è una variabile $x$ e una funzione che la ha come parametro $f(x)$ (fallimento $\rightarrow$ sostituzione infinita).
> Si può benissimo sostituire una <u>variabile con una costante/variabile/funzione diversa</u>.

##### Risoluzioni predicative

Calcolare (se possibile) le risoluzioni di 2 clausole $C_{1}$ e $C_{2}$:

\- Individuare i letterali opposti tra le clausole (se non ce ne sono non risolvibile),

\- Se le variabili/costanti nei letterali sono diverse, applicare l'algoritmo di Robinson tra le 2 (finché non si hanno uguali che differiscono solo per il $\lnot$ iniziale),

\- Se si riesce a sostituire tutto e a rendere le 2 clausole uguali (differenti solo per $\lnot$) allora è risolvibile (e si procede) altrimenti fallimento per una regola di sostituzione,

\- Avendo $\sigma$ da Robinson, applicare le sostituzioni a tutti gli altri letterali nelle clausole,

\- Cancellare i letterali opposti (su cui si è fatto Robinson),

\- Unire i letterali rimasti in un insieme, quello è il risolvente.

(così se si vuole solo fare la risoluzione, se è parte di SLD, allora tale risolvente diventa la nuova CC)

###### Clausole di Horn

Una **clausola di Horn** è una clausola che contiene <u>al max 1 letterale positivo</u> (eventuali altri sono <u>negativi</u>).

> [!important] Traduzione in PROLOG
> Ci sono 3 casi di clausole di Horn (ah in PROLOG `X` maiuscola è una <u>variabile</u> mentre `c` minuscola è una <u>costante</u>):
> \- **Fatti**: contengono <u>solamente il letterale positivo</u> tipo $A(c)$ che in PROLOG = `A(c)`,
> \- **Regole**: contengono <u>il letterale positivo e 1 o più negativi</u> tipo $A(x) \lor \lnot B(y) \lor \lnot C(z,d)$ che in PROLOG = `A(X) :- B(Y), C(Z,d)`,
> \- **Clausole *goal***: contengono <u>solamente letterali negativi</u> tipo $\lnot A(c)$ che in PROLOG = `:- A(c)` o `?- A(c)`.
> Un **programma** è un'insieme di clausole di Horn <u>definite</u> (ovvero fatti e regole) e serve per la verifica delle clausole goal (?).

### PROLOG

Dimostrare che da un programma PROLOG è possibile dedurre una certa clausola (goal), così:

\- Tradurre il programma PROLOG (insieme di clausole di Horn) in insieme di letterali,

\- Scrivere il ***goal*** (clausole goal) da dimostrare, che diventano la "clausola corrente" **CC** (ciò in CC è implicitamente negato, poi si cerca solo su letterali positivi infatti),

***SLD***:

\- Prendere il 1° letterale della CC (considerandolo <u>invertito</u> rispetto a come dato nel goal, tipo ${} \lnot A {}$)

\- Cercare nel <u>programma</u> un fatto/regola che abbia un letterale positivo che combaci col precedente (quindi $A$, stesso predicato) a scelta,

\- Trovare l'<u>MGU</u> tra il letterale goal e quello positivo che vi combacia con l'<u>algoritmo di Robinson</u>,

\- Applicare l'MGU sia alla CC, sia a tutta la clausola scelta (effettuare le sostituzioni),

\- Eliminare dalla clausola scelta il fatto/regola scelto e aggiungere ciò che rimane in coda/testa alla CC,

\- Ripetere gli step finché la CC non diventa la <u>clausola vuota</u> ($\square$) e se non lo diventa (e non si ha sbagliato) il goal non è deducibile (PROLOG da `false`).

(sembra che in albero di derivazione o backtracking, se ci sono path diversi, meglio scegliere quello che porta a $\square$)

![](https://i.imgur.com/wmmyrfn.png)

![587](https://i.imgur.com/cmCEaHD.png)

![586](https://i.imgur.com/zapDbjV.png)

![588](https://i.imgur.com/iZFYMCc.png)

