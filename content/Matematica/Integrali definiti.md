---
public: true
edited_seconds: 3450
modified_at: 29/03/2024 11:55:07
---
### Integrale definito
Abbiamo una funzione generica $f(x)$:

(foto)

Definiamo 2 **estremi di integrazione** $a$ e $b$ sull'asse delle x. Questi delimiteranno a destra e a sinistra l'area sottesa della funzione che vogliamo calcolare.
Suddividere poi l'area sottesa in rettangoli di uguale dimensione, i quali delimiteranno un'area che va dal punto $c_{n}$ (punto medio della base del rettangolo, per ogni rettangolo: $c_{1}, c_{2} \ldots$) al punto $f(c_{n})$ (trovato proiettando ogni $c_{n}$ di ogni rettangolo sulla funzione).

(foto)

A questo punto definiamo:
- $N$ = il n° di rettangoli usati per definire l'area sotto la funzione.
- $\Delta x$ = la lunghezza della base di ogni rettangolo, data da: $\; \Delta x = \dfrac{b - a}{N}$.
Matematicamente, trovare l'area di un n° indefinito di rettangoli $N$ si può rappresentare con:
$$S_{N} = (\Delta x_{1} * f(c_{1})) + (\Delta x_{2} * f(c_{2})) \, \ldots \, (\Delta x_{N} * f(c_{N}))$$
$S_{N}$ è detta **somma di Riemann** e per rappresentarla in modo migliore, si usa questa sommatoria:
$$S_{N} = \sum\limits^{N}_{i \,=\, 1} \, f(c_{i}) * \Delta x$$
L'idea per calcolare l'area della curva è aumentare gradualmente $N$ riducendo di volta in volta la lunghezza della base di ogni rettangolo, prolungando questo processo indefinitamente, così da aumentare sempre di + la precisione con cui i rettangoli corrispondono all'area sotto la funzione. Per questo motivo si usa il limite:
$$\lim_{N \,\to\, +\infty} S_{N} \;\;\;=\;\; \lim_{\Delta x \,\to\, 0} \; \sum\limits^{N}_{i \,=\, 1} \, f(c_{i}) * \Delta x$$
Questo è l'integrale definito e la sua notazione è:
$$\int^{b}_{a} f(x) \; dx$$
Se la funzione $f(x)$ è continua, il limite delle somme di Riemann esiste.
>[!important] Definizione
>L'integrale definito è il limite per $N$ tendente a $+\infty$ delle somme di Riemann, considerandole in una funzione continua

### Proprietà
Gli integrali definiti mantengono le 2 proprietà di [[Integrali indefiniti#Proprietà|linearità]] degli [[Integrali indefiniti|integrali indefiniti]] e ad esse vi aggiungono (le prime 2 sono convenzioni, assiomi):
>[!important] Convenzione 1
>L'integrale compreso nell'intervallo tra un numero $a$ e lo stesso numero $a$ è 0 (siccome l'intervallo è nullo): $\displaystyle \int^{a}_{a} f(x) \; dx = 0$

>[!important] Convenzione 2
>Gli integrali si calcolano da $a$ a $b$ (quindi "da sinistra verso destra" avendo $a < b$) e in questo modo si interpretano come positivi o negativi in base all'area (se si trova sopra o sotto l'asse x).
>Gli integrali calcolati da $b$ ad $a$ (in questo caso "da destra verso sinistra", sempre con $a < b$,) vanno invece interpretati al contrario. 
>Per questo vale l'uguaglianza (sempre se $a < b$): $\displaystyle \int^{b}_{a} f(x) \; dx = - \int^{a}_{b} f(x) \; dx$

>[!important] Additività rispetto all'intervallo d'integrazione
>Se $f(x)$ è continua in un intervallo e quest'ultimo contiene i punti $a$, $b$ e $c$ (possibilmente $a < b < c$), allora:
>$$\int^{c}_{a} f(x) \; dx \;=\; \int^{b}_{a} f(x) \; dx \;+\; \int^{c}_{b} f(x) \; dx$$

>[!important] Monotonia
>Se $f(x)$ e $g(x)$ sono 2 funzioni continue tali che $g(x) \le f(x)$ in ogni punto dell'intervallo \[$a$;$b$\], allora:
>$$\int^{b}_{a} f(x) \; dx \;\le\; \int^{b}_{a} g(x) \; dx$$

>[!important] Positività
>Se una funzione $f(x)$ è sempre $\ge 0$ in ogni punto dell'intervallo \[$a$;$b$\], allora anche il suo integrale lo sarà:
>$$f(x) \ge 0 \;\,\rightarrow\, \int^{b}_{a} f(x) \; dx \ge 0$$

>[!important] Integrale del valore assoluto di una funzione
>(Libro 1298)

>[!important] Integrale di una funzione costante
>(Libro 1298)

### Teorema fondamentale del calcolo integrale
Questo teorema (seppur non enunciato in dettaglio) permette di semplificare il calcolo degli integrali definiti. Se integriamo tra $a$ e $b$ una funzione $f(x)$ continua nell'intervallo, allora:
$$\int^{b}_{a} f(x) \; dx = F(b) - F(a)$$
Con $F$ primitive; quindi si sostituiscono alle $x$ della funzione integranda prima l'argomento di $F(b)$, e poi a questa si sottrae la medesima funzione integranda sostituendovi alle $x$ l'argomento di $F(a)$. 
###### Esempio + notazione
$$\int^{1}_{0} x \; dx \;=\; \biggr{[}\, \frac{x^{2}}{2} \,\biggr{]}^{1}_{0} \;=\; \frac{1^{2}}{2} - \frac{0^{2}}{2} \;=\; \frac{1}{2}$$
### Calcolo dell'area di funzioni pari e dispari
Le funzioni pari e dispari presentano delle particolarità quando vengono prese in un intervallo simmetrico:
##### Funzione pari
Prendiamo come esempio $\cos x$ nell'intervallo di integrazione compreso tra $-\pi$ e $\pi$:
--- start-multi-column: ID_avk9
```column-settings
Number of Columns: 2
Largest Column: standard
```

(foto)

--- column-break ---

$$\int^{\pi}_{-\pi} \cos x \; dx \;=\; 2\int^{\pi}_{0} \cos x \; dx$$

--- end-multi-column
Si nota come nell'intervallo le 2 aree siano identiche, perciò si può considerare una delle 2 e moltiplicarla per 2.
##### Funzione dispari
Prendiamo come esempio $\sin x$ nell'intervallo di integrazione compreso tra $-\pi$ e $\pi$:
--- start-multi-column: ID_avk9
```column-settings
Number of Columns: 2
Largest Column: standard
```

(foto)

--- column-break ---

$$\int^{\pi}_{-\pi} \sin x \; dx \;=\; 0$$

--- end-multi-column
Si nota come nell'intervallo le 2 aree siano identiche ed opposte, perciò si annullano.

---
Vedi poi: [[Calcolo dell'area tra 2 funzioni]]