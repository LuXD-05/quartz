# Lezione 7

### Variabili aleatorie continue

Le **variabili aleatorie continue** differiscono da quelle **discrete** sui valori che assumono: 

- Le **discrete** possono assumere solo valori "*discreti*" in un certo insieme di valori reali (<u>numerabili</u>, in quanto <u>ogni valore ha una data probabilità</u> specifica), 
- Le **continue** possono assumere un qualsiasi valore in un certo <u>intervallo infinitesimale</u>, tipo i reali tra 0 e 1 che sono infiniti all'aumentare della precisione decimale.

> [!example] Esempi
> Quindi le discrete vanno bene quando se tra 2 valori non c'è niente, mentre le continue si usano quando tra 2 valori ce ne sono infiniti (e non si sa quale si assume di questi). Per fare un'analogia, le discrete si userebbero per degli <u>scalini</u> (anche infiniti), mentre le continue andrebbero bene per una <u>rampa</u> infinita.

###### PMF e CDF

Dato che i valori delle variabili aleatorie continue sono **infiniti** (infinitesimali), non è possibile calcolare la **PMF** per un certo valore della variabile, perciò (per ogni valore $x$) la <u>PMF di una variabile aleatoria continua sarà sempre 0</u>:

$$P(x) = 0$$

Questo tuttavia non cambia la **CDF**, che anche per le continue è $F(x) = P(X \leq x)$ ed assume valori crescenti da 0 a 1 (l'unica cosa che cambia è che con le discrete la curva della CDF in grafico sarebbe "spezzata" mentre per le continue è "continua").

##### PDF

La **PDF** (*Probability Density Function*) è una funzione che indica la **densità di probabilità**, ovvero <u>dove</u> (nel *range* di valori) <u>è più "densa" la probabilità</u>. Utile nelle continue in quanto (siccome non è possibile determinare la probabilità di un certo valore) essa <u>permette di delineare dei sotto-intervalli più probabili di altri in base a tale "densità"</u>.

(Seppur ci sono delle eccezioni) la PDF ($f(x)$) è semplicemente la <u>derivata della CDF</u>, quindi si indica così:

$$f(x) = F'(x)$$

I valori delineati dalla PDF vanno a costituire una funzione simile a questa (generalmente):

![](https://i.imgur.com/nBG4a4x.png)

Quindi, grazie al teorema fondamentale del calcolo integrale, è possibile usare la differenza di 2 CDF fino a 2 punti $a$ e $b$ per trovare per trovare la densità di probabilità in un certo intervallo ($<$ intercambiabili con $\leq$):

$$\int^{b}_{a} f(x) \;dx = F(b) - F(a) = P(a < X < b)$$

casi particolari

![](https://i.imgur.com/5t62RXP.png)

(perché PMF vale 0)

![](https://i.imgur.com/1QTltV9.png)

##### Valore atteso

Il valore atteso $E[X]$ di una variabile aleatoria continua è uguale ed è definito come una sorta di centro di gravità dell'intera area sotto la curva:

![](https://i.imgur.com/13IuAU9.png)

E la sua formula è:

$$E[X] = \int x \cdot f(x) \;dx$$

##### Varianza

La varianza $\sigma^{2}$ invece rimane la stessa:

$$\sigma^{2} = E(X - E[X]^{2}) = \int (x - E[X])^{2} \cdot f(x) \;dx = \int x^{2} \cdot f(x) \;dx = {\color{yellow}{E[X^{2}] - E[X]^{2}}}$$

---

Prossima lezione: [[8 - Distribuzioni continue note]]

