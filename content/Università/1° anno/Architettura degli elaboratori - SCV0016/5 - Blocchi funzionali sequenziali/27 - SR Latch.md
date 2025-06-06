# Lezione 27

### Latch SR

Un **latch** (o bistabile) **SR**, è un blocco funzionale sequenziale capace di memorizzare un bit grazie alla "***retroazione***" (output di un blocco del circuito stesso = input di un altro blocco).

**Ingressi**: 2 ($S$ e $R$, detti canali "***Set***" e "***Reset***")

**Uscite**: 2 ($Q$ e $\overset{\_}{Q}$)

![](https://i.imgur.com/TkMnoaZ.png)

Esso usa 2 porte NOR che ritornano 1 solo quando gli ingressi sono entrambi a 0:

![](https://i.imgur.com/fIDbeSk.png)

> [!error] Attenzione
> Il latch SR non va trattato come un circuito normale (alimentandolo e dandogli certi input di continuo per avere un certo output), bensì basta inserire un 1 in $S$ o $R$ per qualche nanosecondo per far si che il circuito memorizzi un certo valore.

##### Stati

Per la "*retroazione*" un latch SR, quando $S = R = 0$, è caratterizzato da degli "**stati**", durante i quali lo stesso memorizza 0 o 1 (in $Q$, che è l'uscita che rappresenta il bit memorizzato).

##### Funzionamento

Un latch SR, fornito per qualche nanosecondo un 1 in input in $S$ o $R$, cambia il valore che memorizza:

0) Senza mandare segnali ("a riposo", $S = R = 0$) il latch rimane com'è (sia con 0 sia con 1 in memoria),
1) Se si manda un segnale sul canale $S$ (*Set*, con $S = 1$ e $R = 0$), il latch passa a memorizzare $1$ in $Q$ (indipendentemente da ciò che c'era prima) e tale stato permane anche quando il segnale su $S$ cessa,
2) Se si manda un segnale sul canale $R$ (*Reset*, con $S = 0$ e $R = 1$), il latch passa a memorizzare $0$ in $Q$ (indipendentemente da ciò che c'era prima) e tale stato permane anche quando il segnale su $R$ cessa.
3) Mandando un segnale su entrambi i canali, sia $Q$ sia $\overset{-}{Q}$ sono = 0.

> [!error] Attenzione
> Se dopo aver settato $S = R = 1$ si tenta di ritornare a riposo ($S = R = 0$) l'evoluzione successiva è imprevedibile in quanto le uscite ***oscillano***:
> - Se $S$ e $R$ vanno contemporaneamente a 0, le uscite oscillano tra 00 e 11,
> - Se $R$ va a 0 (anche poco) prima di $S$, $Q = 1$ e $\overset{-}{Q} = 0$,
> - Se $S$ va a 0 (anche poco) prima di $R$, $Q = 0$ e $\overset{-}{Q} = 1$.
> Quindi mettere a 1 sia $S$ sia $R$ non è mai utile in un latch SR.

#### Descrivere il comportamento del latch SR

###### Tavola di verità

La **tavola di verità** <u>non è un modo adeguato per rappresentare il comportamento di un circuito sequenziale</u> in quanto per $S = R = 0$ ci sono 2 configurazioni stabili che dipendono dallo <u>stato</u> attuale del circuito (a sua volta dipendente dagli input precedenti).

![](https://i.imgur.com/4xZCf38.png)

###### FSM

Una [[26 - Blocchi funzionali sequenziali#FSM|macchina a stati finiti]] è un modo adeguato per descrivere il comportamento di un latch SR:

![](https://i.imgur.com/y5X2rCF.png)

###### Diagramma temporale

Rappresentiamo ora il diagramma temporale di un latch SR durante l'input di 1 in $R$:

![](https://i.imgur.com/7MJglWT.png)

![](https://i.imgur.com/D1syOCv.png)

##### Latch come adattatore

Un uso più pratico del latch SR prevede di trattarlo come un *adattatore*. Per esempio si ha una periferica che manda un breve segnale (*INTERRUPT*) a una CPU in un certo momento $t$, ma sempre in quel momento la stessa CPU è occupata.

![](https://i.imgur.com/WzodYS1.png)

Si vede come un latch SR viene usato per memorizzare il breve *INTERRUPT* della periferica e lo stabilizza comunicandolo continuamente in output in $Q$ (poi quando la CPU lo riceve rimanda un output al latch SR per azzerare tale valore).

# Esercizi

# Soluzioni

---

Prossima lezione: [[28 - Gated D-Latch]]

