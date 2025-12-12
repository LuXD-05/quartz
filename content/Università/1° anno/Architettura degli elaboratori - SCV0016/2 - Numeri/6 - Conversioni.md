# Lezione 6

### Conversioni

##### Passare da base B a base 10

Per passare da una base $B$ alla base 10, basta semplicemente <u>moltiplicare tutte le cifre del numero in base</u> $B$ <u>per</u> $B$, e si otterrà il numero in base 10:

${} N_{10} = n_{0}B^{0} + n_{1}B^{1} \;...\; n_{k}B^{k} {}$

Esempio:

$351_{6} = 1 * 6^{0} + 5 * 6^{1} + 3 * 6^{2} = 139_{10}$

##### Passare da base 10 a base B

Per passare da un numero in base 10 ad un numero in base $B$ si usa l'**algoritmo delle divisioni successive**, il quale consiste in:

1) Fare la divisione con resto  del numero da convertire per $B$,
2) Trascrivere a fianco il resto,
3) Sotto al numero da convertire, scrivere: (numero - resto) / $B$,
4) Ripetere gli step precedenti finché il numero di cui fare il modulo non diventa 0,
5) Prendere i resti dal basso (MSB) verso l'alto (LSB), quello sarà il risultato.

Esempio: conversione di $11_{10}$ in base 2

![](https://i.imgur.com/HzlMmtU.png)

##### Conversione tra basi una potenza dell'altra 1

###### Colombo version

Consideriamo 2 rappresentazioni in base $P$ e $B$ dello stesso valore $N$:

$N = m_{0}P^{0} + m_{1}P^{1} \;...\; m_{j}P^{j}$

$N = n_{0}B^{0} + n_{1}B^{1} \;...\; n_{k}B^{k}$

Supponiamo ora che $P$ sia una potenza di $B$ ($P = B^{x}$):

$N = m_{0}P^{0} + m_{1}P^{1} \;...\; m_{j}P^{j}$

$N = m_{0}B^{0x} + m_{1}B^{1x} \;...\; m_{j}B^{jx}$

Facendo $\dfrac{N}{B}$, il resto è $e_{0}$

Viceversa la 1a cifra di $N$ in base $P$ è ricavabile osservando le prime $m$ cifre di $N$ in base $B$.

Applicando le divisioni successive otteniamo che l'ennesima cifra di $N$ in base $P$ è ricavabile osservando l'ennesimo gruppo di $m$ cifre di $N$ in base $B$.

##### Conversione tra basi una potenza dell'altra 2

###### Normal version

Ci sono 2 situazioni in cui si applicano le seguenti regole di conversione a 2 numeri $N$ e $M$ (con $N$ = numero da convertire originale ed $M$ = numero convertito incognito):

###### $B_{N}$ è una potenza di $B_{M}$

Quando $B_{N}$ è una potenza di $B_{M}$, si procede così:

1) Si ottiene la potenza ($P$) che, se applicata a $B_{M}$, dà $B_{N}$ facendo $\log_{B_{M}}B_{N}$,
2) Ogni cifra di $N$ bisognerà convertirla nel corrispondente valore in $B_{M}$ usando per ognuna $P$ cifre,
3) Mantenendo MSB e LSB, si otterrà il numero convertito.

Esempio: 

Vogliamo convertire $N_{B} = 5731_{8}$ in base 2: 

1)  $\log_{2}8 = 3$ (cifre in base 2 per cifra in base 8),
2) Si trasforma ogni cifra di $N_{8}$ in 3 cifre di $M_{2}$,
3) ![](https://i.imgur.com/in5hThf.png)

###### $B_{M}$ è una potenza di $B_{N}$

Quando è $B_{M}$ ad essere una potenza di $B_{N}$, si procede così:

1) Si ottiene la potenza ($P$) che, se applicata a $B_{N}$, dà $B_{M}$ facendo $\log_{B_{N}}B_{M}$,
2) Si convertono (partendo dall'LSB) $P$ cifre di $N$ per volta in 1 cifra in base $B_{M}$ (l'ultima, dell'MSB, in caso abbia meno cifre di $P$ si aggiungono degli 0 davanti con significato maggiore),
3) Mantenendo MSB e LSB, si otterrà il numero convertito.

Esempio: 

Vogliamo convertire $N_{B} = 100000010011_{2}$ in base 8: 

1)  $\log_{2}8 = 3$ (cifre in base 2 per cifra in base 8),
2) Dall'LSB, si convertono 3 cifre di $N_{2}$ in 1 cifra di $M_{8}$ per volta,
3) ![](https://i.imgur.com/EyvEHLd.png)

# Esercizi

# Soluzioni

---

Prossima lezione: [[7 - Operazioni aritmetiche]]

