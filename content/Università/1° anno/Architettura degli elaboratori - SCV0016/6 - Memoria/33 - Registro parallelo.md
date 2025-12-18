# Lezione 33

### Registro parallelo

Il **registro parallelo** è un **vettore** di $n \geq 1$ **[[30 - Flip-Flop e sincronizzazione sul fronte#Flip-Flop|flip-flop D]]** (sincronizzati sul fronte) che, ad ogni ciclo di clock, legge e memorizza nel suo stato una ***word*** di $n$ bit in input e la presenta sulle $n$ uscite del ciclo successivo.

**Ingressi**: $n$ ($I_{1}, \ldots I_{n}$) + $CK$ (clock)

**Uscite**: $n$ ($U_{1}, \ldots U_{n}$)

> [!error] Attenzione
> Se si usassero dei bistabili sincronizzati **[[29 - Clock e sincronizzazione sul livello#Sincronizzazione sul livello|sul livello]]**, si rischia **trasparenza** e di conseguenza il malfunzionamento del circuito (non si comporterebbe come un registro <u>ma farebbe passare subito i segnali</u>).

##### Struttura

La seguente è la struttura di un registro parallelo a **4 bit**, infatti è composto da 4 [[30 - Flip-Flop e sincronizzazione sul fronte#Flip-Flop|flip-flop D]],

![](https://i.imgur.com/wV99BAr.png)

###### Diagramma temporale

Nel caso $n = 4$ (input/output) e si carichino in ordine $0000$, $0101$, $0011$ e così via:

![](https://i.imgur.com/tXxKzpB.png)

#### Comando Load

Un registro parallelo può avere anche un ulteriore input $L$ (*Load*), rappresentante un **comando di caricamento**, che:

- Quando $L = 1$, la ***word* in input viene memorizzata** (funzionamento normale),
- Quando $L = 0$, il **registro mantiene la *word* corrente** in memoria (per quel ciclo di clock).

##### Struttura con Load

Per implementare il comando $L$, si antepone quindi un [[21 - Multiplexer#Multiplexer|MUX]] ad ogni input $D$ dei gated D-latch cosicché se $L = 0$ si sceglie il 1° valore (input $I_{n}$), altrimenti il 2° (output già memorizzato $U_{n}$).

![](https://i.imgur.com/i32mwVP.png)

###### Diagramma temporale con Load

![](https://i.imgur.com/ZHAP5dG.png)

#### Varianti

Dei registri paralleli esistono anche altre varianti:

- Registri paralleli con comando **[[31 - CLR e PR#Comandi CLR e PR|CLR]]**, permettono l'<u>azzeramento</u> in modo asincrono del proprio contenuto quando $CLR = 1$,
- Registri paralleli con comando **[[31 - CLR e PR#Comandi CLR e PR|PR]]**, permettono di <u>settare a</u> (tutti) <u>1</u> il proprio contenuto in modo asincrono quando $PR = 1$,
- **Registri paralleli universali**, i quali semplicemente implementano tutte le funzioni $L$, ${} CLR$ e $PR$.

# Esercizi

# Soluzioni

---

Prossima lezione: [[34 - Registro a scorrimento]]

