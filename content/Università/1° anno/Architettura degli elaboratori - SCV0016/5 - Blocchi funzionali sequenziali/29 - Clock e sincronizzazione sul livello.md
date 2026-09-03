# Lezione 29

##### Sincronizzazione

In certi casi potrebbe essere necessario <u>impedire che lo stato di un latch possa cambiare durante certi intervalli di tempo</u>. Per ottenere questo comportamento è necessario:

- Disporre di un **segnale di clock** che scandisca gli intervalli nei quali i cambi di stato possano avvenire,
- Sincronizzare il latch con tale segnale di clock.

### Clock

Un **clock** è un dispositivo che produce un <u>segnale binario con andamento periodico nel tempo</u> (e tale viene propagato all'intero processore/circuito).

Essendo **periodico**, il segnale di clock è composto da ***cicli*** durante i quali si ripete la stessa porzione di segnale.

![](https://i.imgur.com/P3wuw6m.png)

> [!important] Periodo, frequenza e definizioni
> Ogni periodo dura un tempo $t$, detto **periodo di clock**, durante il quale si susseguono: un intervallo basso (segnale a 0), un fronte di salita (passaggio da 0 a 1), un intervallo alto (segnale a 1) e un fronte di discesa (torna a 0).
> La ***frequenza*** è l'inverso del **periodo**, si calcola con $\tfrac{1}{t}$ e conta il n° di cicli eseguiti al secondo (si misura in **Hz**, *Hertz*).

###### Convenzioni

Ci sono varie convenzioni riguardanti i segnali di clock che si utilizzano:

- Il **fronte di discesa** è sempre il <u>1° ed ultimo atto di ogni ciclo</u>,
- Il **fronte di salita** avviene sempre a <u>metà di un ciclo</u>,
- L'**intervallo basso** corrisponde sempre alla <u>1a metà di un ciclo</u>,
- L'**intervallo alto** corrisponde sempre alla <u>2a metà di un ciclo</u>,
- (Un **ciclo** = intervallo basso + intervallo alto).

###### Frequenze tipiche

![](https://i.imgur.com/MEY0HQu.png)

#### Sincronizzazione sul livello

Collegando l'input $E$ di un [[28 - Gated D-Latch#Gated D-Latch|gated D-latch]] ad un [[#Clock|clock]] (ciò si dice "*sincronizzazione **sul livello***") si ottiene un *synchronized gated D-latch*, il quale:

- Nell'<u>intervallo basso</u> del clock (0), è ***frozen*** (input $D$ è ignorato),
- Nell'<u>intervallo alto</u> del clock (1), è ***attivo*** (input $D$ è memorizzato) ma anche ***transparent*** (input $D$ è visibile in $Q$).

![](https://i.imgur.com/3F7k7nX.png)

Così si fa in modo che $Q$ cambi al valore di $D$ sempre e solo quando il clock passa a 1:

![](https://i.imgur.com/QkyqZXF.png)

> [!error] Questione della trasparenza
> Durante l'intervallo alto del clock, l'input $E$ del gated D-latch è a 1, il che significa che l'output $Q$ assume il valore dell'input $D$.
> Questo però non "dura" un istante (quanto necessario per $Q$ per assumere il valore di $D$), infatti se $D$ cambiasse di nuovo nel mentre che il clock è a 1, $Q$ ne assumerebbe lo stesso i valori.
> ![](https://i.imgur.com/ZBPVKAr.png)

###### Problema

Supponiamo di avere un circuito elaboratore costituito da una parte di <u>memorizzazione</u> (gated D-latch) e una di <u>elaborazione</u> (circuito combinatorio) dove, ad ogni ciclo di clock:

1) Il circuito combinatorio di elaborazione calcola il nuovo stato,
2) Il circuito di memorizzazione memorizza il nuovo stato calcolato.

![](https://i.imgur.com/0Uv5Zjp.png)

Così, quando il clock va ad 1, gli output del circuito combinatorio sono (quasi) immediatamente memorizzati. 

Ciò è un grave problema in quanto, se solo alcuni output sono già stati calcolati (e quindi anche memorizzati), il circuito combinatorio (presupposto che il clock sia ancora ad 1) potrebbe ritrovarsi ad usare dei valori appena sovrascritti per calcolare gli output rimanenti, andando ad invalidare i risultati finali.

![](https://i.imgur.com/fv76nOK.png)

Se si bloccasse l'acquisizione di $Q$ da parte del circuito combinatorio durante l'intervallo alto del clock, tutto il circuito <u>si ferma</u> per quella metà di ciclo, restando <u>inutilizzato</u>.

# Esercizi

# Soluzioni

---

Prossima lezione: [[30 - Flip-Flop e sincronizzazione sul fronte]]

