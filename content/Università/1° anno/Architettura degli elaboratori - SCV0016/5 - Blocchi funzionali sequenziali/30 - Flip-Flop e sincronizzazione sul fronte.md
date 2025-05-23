# Lezione 30

#### Sincronizzazione sul fronte

Con la sincronizzazione sul fronte si risolve il [[29 - Clock e sincronizzazione sul livello#Problema|problema della trasparenza]] dei *synchronized gated D-latch* in quanto:

- Il <u>circuito di memorizzazione</u> è sempre "***frozen***", ovvero non è <u>mai in condizione di trasparenza</u> (eccetto per un <u>breve periodo di commutazione</u> all'inizio di ogni ciclo),
- Come il clock passa da 1 a 0 (o anche da 0 a 1) gli <u>ingressi</u> sono <u>già efficaci</u> (sempre dopo quegli istanti di commutazione del bistabile) e <u>rimangono così</u> per tutto il (resto del) periodo di clock.

### Flip-Flop

Un **Flip-Flop** è semplicemente un bistabile sincronizzato sul fronte.

##### Flip-Flop con generatore di impulsi

Il 1° metodo per realizzare un Flip-Flop è mediante l'uso di un **generatore di impulsi**, ovvero un **clock "*asimmetrico*"** in cui l'<u>intervallo alto è minimo</u>, cioè un segnale il cui <u>fronte di salita coincide quasi col fronte di discesa</u>:

![](https://i.imgur.com/MzZ0uQK.png)

Il generatore a impulsi (collegato ad un clock in input) funziona sfruttando il ritardo della porta [[13 - Tipi di porte e tavole di verità#Porta NOT|NOT]]:

![](https://i.imgur.com/MbbpV5v.png)

###### Blocco funzionale

Il flip-flop a impulsi è realizzato così:

![](https://i.imgur.com/M8lss6E.png)

E si può anche sintetizzare in questo modo:

![](https://i.imgur.com/jJ4Ja7q.png)

(Per invertirlo, ovvero indicare che genera impulsi a 0 invece che a 1, basta inserire una NOT davanti all'ingresso del generatore di impulsi).

###### Problematiche

Seppur semplice ed economica da realizzare, la modalità con generatore di impulsi <u>non è molto robusta</u> (affidabile), dato che il basarsi sul ritardo della NOT non garantisce la **precisa durata dell'impulso**; la quale è fondamentale perché:

- Se <u>troppo corta</u>, non dà abbastanza tempo al gated D-latch per commutare,
- Se <u>troppo lunga</u>, si mantiene il flip-flop in stato di trasparenza troppo a lungo.

##### Flip-Flop *master-slave*

I **Flip-Flop "*master-slave*"** (o *a memoria ausiliaria*) sono i più utilizzati per realizzare il sincronismo sul fronte e si compongono di 2 gated D-latch così disposti:

![](https://i.imgur.com/TciA2j6.png)

Questa disposizione fa sì che il circuito non sia <u>mai in condizione di trasparenza</u>, in quanto lo ***slave*** può assumere $Q1$ in input solo quando $CK$ torna a 0, ovvero dopo che il ***master*** ha memorizzato l'input in modo stabile. Infatti:

- Il ***master*** è bloccato nell'intervallo basso,
- Lo ***slave*** è bloccato nell'intervallo alto,
- L'<u>input</u> del flip-flop <u>non si propaga mai</u> direttamente <u>fino all'output</u>.

> [!important] Nota
> Nei flip-flop il segnale di clock iniziale è generalmente **negato**. Questo riduce il consumo totale dei circuiti e bilancia il circuito per contrastare il [clock skew](https://en.wikipedia.org/wiki/Clock_skew); però è anche utile nei flip-flop *master-slave* dato che:
> - Allinea l'**output** dello *slave* (con $CK = 0$ di default) con l'<u>intervallo alto</u> del clock (> efficienza se si suppone che i blocchi combinatori accettino input nell'intervallo **alto**),
> - Permette al *master* di **memorizzare** (con $CK = 1$ di default) solo quando $CK = 0$ (> l'efficienza se si suppone che l'intervallo in cui i blocchi combinatori inviano l'output alle memorie sia quello **basso**).

###### Diagramma temporale

Di seguito è presentato un esempio di diagramma temporale del Flip-Flop *master-slave*, dove le azioni che avvengono sono:

0) (Clock che manda il segnale temporizzato),
1) Input in $D1$ del ***master*** (quando il clock è a 1) + memorizzazione in $Q1$ e $D2$,
2) Clock passa a 0 + $Q2$ memorizza $D2$,
3) Tentato input breve in $D1$ (quindi in $Q1$ e $D2$) ma non ha effetto (siccome clock è ancora a 1 ed $E2$ conseguentemente a 0),
4) ...

![](https://i.imgur.com/soylTIT.png)

# Esercizi

# Soluzioni

---

Prossima lezione: [[31 - CLR e PR]]

