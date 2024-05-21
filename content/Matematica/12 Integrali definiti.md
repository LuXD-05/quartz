### Integrale definito

Per una funzione generica $f(x)$, si definiscono 2 **estremi di integrazione** $a$ e $b$ sull'asse delle x. Questi delimiteranno a destra e a sinistra l'area sottesa della funzione che vogliamo calcolare.

Questa va poi suddivisa in **rettangoli** di <u>uguale dimensione</u>, i quali delimiteranno un'**area** che va dal punto $c_{n}$ (il punto medio alla base di ogni rettangolo) al punto $f(c_{n})$ (trovato proiettando ogni $c_{n}$ per la funzione su y).

![](https://i.imgur.com/ylnlGiA.png)

A questo punto definiamo:

- $N$ = il **n° di rettangoli** usati per definire l'area sotto la funzione.
- $\Delta x$ = la lunghezza della **base di ogni rettangolo**, data da: $\; \Delta x = \dfrac{b - a}{N}$.

Matematicamente, trovare l'<u>area di un n° indefinito di rettangoli</u> $N$ si può rappresentare con:

$$S_{N} = (\Delta x_{1} * f(c_{1})) + (\Delta x_{2} * f(c_{2})) \, \ldots \, (\Delta x_{N} * f(c_{N}))$$

$S_{N}$ è detta **somma di Riemann** e per rappresentarla in modo migliore, si usa questa sommatoria:

$$S_{N} = \sum\limits^{N}_{i \,=\, 1} \, f(c_{i}) * \Delta x$$

L'idea per calcolare l'area della curva è <u>aumentare gradualmente</u> $N$ <u>riducendo di volta in volta la lunghezza della base di ogni rettangolo</u>, prolungando questo processo <u>indefinitamente</u>, così da <u>aumentare</u> sempre di + la <u>precisione con cui i rettangoli corrispondono all'area</u> sotto la funzione.

![](https://i.imgur.com/AaW4teJ.png)

Per questo motivo si usa il limite:

$$\lim_{N \,\to\, +\infty} S_{N} \;\;\;=\;\; \lim_{\Delta x \,\to\, 0} \; \sum\limits^{N}_{i \,=\, 1} \, f(c_{i}) * \Delta x$$

Questo è l'integrale definito e la sua notazione è:

$$\int^{b}_{a} f(x) \; dx$$

Se la funzione $f(x)$ è **continua**, il limite delle somme di Riemann (integrale definito) **esiste**.

> [!important] Definizione
> L'integrale definito è il limite per $N$ tendente a $+\infty$ delle somme di Riemann, considerandole in una funzione continua

### Proprietà

Gli integrali definiti mantengono le 2 proprietà di [[11 Integrali indefiniti#Proprietà|linearità]] degli [[11 Integrali indefiniti|integrali indefiniti]] e ad esse vi aggiungono (le prime 2 sono convenzioni, assiomi):

> [!important] Convenzione 1
> L'integrale compreso nell'intervallo tra un numero $a$ e lo stesso numero $a$ è 0 (siccome l'intervallo è nullo): $\displaystyle \int^{a}_{a} f(x) \; dx = 0$

> [!important] Convenzione 2
> Gli integrali si calcolano da $a$ a $b$ (quindi "da sinistra verso destra" avendo $a < b$) e in questo modo si interpretano come positivi o negativi in base all'area (se si trova sopra o sotto l'asse x).
> Gli integrali calcolati da $b$ ad $a$ (in questo caso "da destra verso sinistra", sempre con $a < b$,) vanno invece interpretati al contrario.
> Per questo vale l'uguaglianza (sempre se $a < b$): $\displaystyle \int^{b}_{a} f(x) \; dx = - \int^{a}_{b} f(x) \; dx$

> [!important] Additività rispetto all'intervallo d'integrazione
> Se $f(x)$ è continua in un intervallo e quest'ultimo contiene i punti $a$, $b$ e $c$ (possibilmente $a < b < c$), allora:
> $$\int^{c}_{a} f(x) \; dx \;=\; \int^{b}_{a} f(x) \; dx \;+\; \int^{c}_{b} f(x) \; dx$$

> [!important] Monotonia
> Se $f(x)$ e $g(x)$ sono 2 funzioni continue tali che $g(x) \le f(x)$ in ogni punto dell'intervallo \[$a$;$b$\], allora:
> $$\int^{b}_{a} f(x) \; dx \;\le\; \int^{b}_{a} g(x) \; dx$$

> [!important] Positività
> Se una funzione $f(x)$ è sempre $\ge 0$ in ogni punto dell'intervallo \[$a$;$b$\], allora anche il suo integrale lo sarà:
> $$f(x) \ge 0 \;\,\rightarrow\, \int^{b}_{a} f(x) \; dx \ge 0$$

> [!important] Integrale del valore assoluto di una funzione
> (Libro 1298)

> [!important] Integrale di una funzione costante
> (Libro 1298)

### 1° teorema fondamentale del calcolo integrale

Questo teorema (seppur non enunciato in dettaglio) permette di semplificare il calcolo degli integrali definiti. Se integriamo tra $a$ e $b$ una funzione $f(x)$ <u>continua</u> nell'intervallo, allora:

$$\int^{b}_{a} f(x) \; dx = F(b) - F(a)$$

$F$ sono **primitive**; quindi si va a sostituire alle $x$ della funzione integranda, prima l'argomento di $F(b)$, e poi a questa si sottrae la medesima funzione integranda sostituendovi alle $x$ l'argomento di $F(a)$.

###### Esempio + notazione

$$\int^{1}_{0} x \; dx \;=\; \biggr{[}\, \frac{x^{2}}{2} \,\biggr{]}^{1}_{0} \;=\; \frac{1^{2}}{2} - \frac{0^{2}}{2} \;=\; \frac{1}{2}$$

### 2° teorema fondamentale del calcolo integrale

###### Funzione integrale

> [!important] Funzione integrale
> Funzione (continua e positiva) che associa ad ogni $x$ l'area sottesa compresa tra $a$ e $x$ (quindi al variare di $x$ varia anche l'area sottesa).
> $$F(x) \;=\; \int^{x}_{a} f(t)\,dt$$

##### Teorema

Derivando la funzione integrale ($F(x)$), si ottiene la funzione integranda:

$$F(x)' \;=\; f(x) \;\; per \; ogni \; x \; \in [A, B)$$

### Calcolo dell'area di funzioni pari e dispari

Hint:

Le funzioni **pari** e **dispari** presentano delle particolarità quando vengono prese in un **intervallo simmetrico**:

##### Funzione pari

Prendiamo come esempio $\cos x$ nell'intervallo di integrazione compreso tra $-\pi$ e $\pi$:

--- start-multi-column: ID_avk9
```column-settings
Number of Columns: 2
Largest Column: standard
Border: off
Alignment: center
```

(foto)

--- column-break ---

$$\int^{\pi}_{-\pi} \cos x \; dx \;=\; 2\int^{\pi}_{0} \cos x \; dx$$

--- end-multi-column

Si nota come nell'intervallo le <u>2 aree siano identiche</u>, perciò si può considerare <u>una delle 2 e moltiplicarla per 2</u>.

##### Funzione dispari

Prendiamo come esempio $\sin x$ nell'intervallo di integrazione compreso tra $-\pi$ e $\pi$:

--- start-multi-column: ID_avk9
```column-settings
Number of Columns: 2
Largest Column: standard
Border: off
Alignment: center
```

(foto)

--- column-break ---

$$\int^{\pi}_{-\pi} \sin x \; dx \;=\; 0$$

--- end-multi-column

Si nota come nell'intervallo le <u>2 aree siano identiche ed opposte</u>, perciò si <u>annullano</u>.

---

Vedi poi: [[13 Calcolo dell'area tra 2 funzioni]]

