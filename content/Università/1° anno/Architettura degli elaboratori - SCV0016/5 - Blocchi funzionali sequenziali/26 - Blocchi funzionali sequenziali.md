# Lezione 26

### Circuiti sequenziali

Al contrario dei circuiti combinatori, i **circuiti sequenziali** fanno uso (oltre ai valori correnti degli input) anche di valori di input passati; infatti si dice che tali "*memorizzano*" le informazioni (detti quindi anche "*retroazionati*") e ad ogni istante di tempo sono dotati di uno ***stato*** che ne determina il comportamento futuro.

###### Struttura

I circuiti sequenziali sono generalmente formati da:

- **Reti di memorizzazione**: che, come vedremo poi, sono dei ***bistabili*** (di vario tipo) e memorizzano lo **stato** corrente del circuito,
- **Reti combinatorie**: che elaborano le informazioni dello stato corrente passate in input per produrre degli output.

![](https://i.imgur.com/qz7V2sA.png)

#### Descriverne il comportamento

Siccome nei circuiti sequenziali gli output <u>variano</u> (dipendono da input precedenti), le **tavole di verità** non sono più adeguate per descriverne il comportamento. Vediamo quindi alcuni metodi per fare ciò:

##### FSM

Una ***Finite State Machine/Automata*** (**FSM/A**, *macchina/automa a stati finiti*) è un modo per descrivere formalmente il comportamento di una macchina (o *automa*) dotata di **memoria**, la quale interagisce con il mondo esterno. Quindi:

- Interazioni con l'esterno: input e output,
- Stato interno: cosa il dispositivo "si ricorda", ovvero la sua memoria.

###### Rappresentazione

Una FSM è un <u>grafo</u> fatto da:

- **Nodi** (pallini): rappresentano ognuno uno **stato**, ovvero una **configurazione stabile** che il circuito può assumere.

  (Ogni nodo deve avere 1 arco uscente per ogni possibile input "legale").

- **Archi** (frecce): <u>collegano i nodi</u> e rappresentano ognuno una potenziale **transizione** da un nodo all'altro; in più, ad ogni arco sono associati <u>1 o più input</u> del circuito.

  (Un arco può connette un nodo a se stesso e si dice ***cappio***).

- **Output**: lo si può associare ad:
  - <u>Ogni nodo</u>: quindi dipende solo dallo stato (*automa alla Moore*),
  - <u>Ogni arco</u>: dipende dallo stato e dagli ingressi (*automa alla Mealy*).

###### Esempio FSM

![](https://i.imgur.com/3J1SOV8.png)

##### Diagramma temporale

Durante l'uso del circuito il valore logico (0 o 1) di ciascun segnale è una funzione di tempo $y = f(t)$, la quale è rappresentabile con un grafico avente il <u>tempo</u> in ascissa (diviso in intervalli discreti) ed il <u>valore logico del segnale</u> in ordinata (0 o 1 per ciascun segnale).

![](https://i.imgur.com/lKOLNPs.png)

> [!error] Attenzione
> I diagrammi temporali sono di solito disegnati idealmente, senza considerare i ritardi:
> - Caso **ideale**: ![](https://i.imgur.com/ZEt9KCr.png)
> - Caso **reale**: ![](https://i.imgur.com/symgxPS.png)

###### Diagramma di fasci temporali

Si possono rappresentare multipli segnali nella seguente forma, esplicitandone i valori binari (per ogni istante in cui si osservano) e rappresentando un cambio nei valori dei segnali tramite l'incrocio delle 2 linee esterne. Esempio con 4 segnali:

![](https://i.imgur.com/UuPitJt.png)

Servirà di più dalla [[34 - Registro a scorrimento|lezione 33]].

#### Famiglie di circuiti sequenziali

(Qui dopo aver concluso la [[30 - Flip-Flop e sincronizzazione sul fronte|lezione 30]] e le precedenti), esistono 2 famiglie di circuiti sequenziali:

##### Circuiti sequenziali asincroni

I circuiti sequenziali **asincroni** sono detti così perché non fanno uso di ***[[29 - Clock e sincronizzazione sul livello#Clock|clock]]*** ed utilizzano bistabili non sincronizzati (tipo ***[[27 - SR Latch#Latch SR|latch SR]]*** e ***[[28 - Gated D-Latch#Gated D-Latch|gated D-latch]]***, che vedremo poi).

Proprio per questa caratteristica sono <u>impiegati raramente</u> (soprattutto nei circuiti complessi) data la loro difficoltà d'uso e di controllo.

##### Circuiti sequenziali sincroni

Al contrario degli asincroni, i circuiti sequenziali sincroni sono universalmente diffusi e hanno tutti alla loro base il [[30 - Flip-Flop e sincronizzazione sul fronte#Flip-Flop|Flip-Flop]].

![](https://i.imgur.com/9RiXC0q.png)

Ma più in generale:

![](https://i.imgur.com/SPUyPWV.png)

Vedere poi 

# Esercizi

###### 1) FSM

Dalla [[#Esempio FSM|foto]], in che stato arriva il dispositivo se parte dallo stato 1 e riceve in input $A, A, B, A, B, C$?

###### n) Controllo di un cancello motorizzato

(Fare/seguire questo esercizio solo dopo la [[30 - Flip-Flop e sincronizzazione sul fronte|lezione 30]] + le precedenti).

Definire un circuito per il controllo di un cancello motorizzato con 3 input:

- CA: comando di apertura,
- CC: comando di chiusura,
- FC: fine corsa (cancello completamente aperto/chiuso).

E 2 output:

- MO: motore on/off (1 = in movimento, 0 = fermo),
- MA: motore avanti/indietro (1 = apre, 0 = chiude).

Il circuito deve controllare il motore reagendo opportunamente ai comandi. I comandi sono **mutuamente esclusivi**, ovvero in ogni istante di tempo al massimo 1 input può essere a 1.

Definire quindi:

- La FSM del problema (con input/output e poi possibilmente in forma binaria), 
- Uno schema ideale del circuito,
- La dipendenza tra gli stati trovati e le uscite come tavola di verità (4 stati/uscite, 2 bit a testa) e quindi la "formula" delle uscite tramite operatori logici,
- (Tabella del calcolo dello stato prossimo?),
- Mappe di Karnaugh,
- (Eventuale codifica a singolo 1),
- Il circuito finale composto dalle varie porte.

# Soluzioni

###### 1)

a

###### n)

a

---

Prossima lezione: [[27 - SR Latch]]

