# Lezione 3

### Funzioni

Dati ${} X$ e $Y$ due insiemi non $\emptyset$, si definisce $f$ una **funzione** da $X$ in $Y$ che associa ad ogni $x \in X$ un solo elemento $y \in Y$; e si scrive:

$$f : X \rightarrow Y$$

Mentre per applicarla, ovvero dato un input $x$ ottenere il risultato $y$, si scrive: $f(x)$.

##### Definizioni

Vi sono anche dei termini importanti da sapere (+ rappresentazione grafica):

![](https://i.imgur.com/ycYHS4S.png)

- **Dominio**: è l'<u>insieme di partenza</u> $X$,
- **Codominio**: è l'<u>insieme di destinazione</u> $Y$,
- **Immagine**: è l'insieme di tutti i valori del codominio ottenibili applicando $f$ a qualsiasi elemento $x \in X$ (o anche $f(X)$),
- **Controimmagine**: l'insieme di tutte le $x$ per cui ${} f(x) = y$.

> [!info] Il piano cartesiano
> Le funzioni sono rappresentabili nel piano cartesiano, un grafico che ne rende più chiara l'interpretazione:
> ![](https://i.imgur.com/nNmC1r0.png)
> Per convenzione, il **dominio** è sull'asse orizzontale e il **codominio** su quella verticale.

###### Esempi di domini

![](https://i.imgur.com/7vk2L7a.png)

#### Tipi di funzioni

##### Funzioni limitate

Una funzione $f$ è:

- **Limitata superiormente**: se esiste un reale $r$ tale che $f(x) \leq r$,
- **Limitata inferiormente**: se esiste un reale $r$ tale che $f(x) \geq r$,
- **Limitata**: se si verificano entrambe le precedenti.

> [!example] Esempi
> 1\) $f(x) = x^{2}$ è limitata inferiormente nell'intervallo $[0,+\infty)$, infatti l'immagine non è mai negativa (funzione mai sotto 0),
> 2\) $f(x) = \sin x$ è limitata, infatti l'immagine rimane nell'intervallo $[-1,1]$.

###### Massimi e minimi

Si dice **massimo** (<u>assoluto</u>) di $f$ il <u>punto più alto</u> raggiunto ($M$) dalla funzione dato un reale $x_{0} \in X$; ovvero:

$$M = f(x_{0}) \geq f(x) \;|\; \forall x \in X$$

Si dice **minimo** (<u>assoluto</u>) di $f$ il <u>punto più basso</u> raggiunto ($m$) dalla funzione dato un reale $x_{0} \in X$; ovvero:

$$m = f(x_{0}) \leq f(x) \;|\; \forall x \in X$$

> [!example] Esempi
> 1\) $f(x) = \sin x$: il max è 1 ed il min è -1,
> 2\) $f(x) = x^{2}$: il min è 0, mentre il max non esiste.

###### Relazione con immagine

> [!important] Quindi
> Per una qualsiasi funzione $f$:
> - Gli **estremi** (superiore e inferiore) di essa corrispondono a quelli del suo insieme **immagine**,
> - I **massimi** e **minimi** di essa corrispondono a quelli del suo insieme **immagine** (tali come valori sono unici, vedi 1 e -1 nel $\sin x$, ma non i valori $x_{0}$ che li raggiungono, infatti sempre col $\sin x$ sono raggiunti ogni $2k\pi$).

##### Funzioni iniettive, suriettive e biettive

###### Funzione iniettiva

Una funzione $f$ si dice **iniettiva** se $\;\forall x_{1},x_{2} \in X \;\;|\;\; x_{1} \neq x_{2} \;\rightarrow\; f(x_{1}) \neq f(x_{2})$, ovvero quando <u>ogni</u> $y$ è <u>ottenuta da max 1 ed 1 sola</u> $f(x)$.

###### Funzione suriettiva

Una funzione $f$ si dice **suriettiva** se $Im(f) = Y$, ovvero quando <u>ogni elemento del codominio fa parte dell'immagine</u> (raggiunto da 1 o più $f(x)$).

###### Funzione biettiva

Una funzione $f$ è **biettiva** quando è sia [[#Funzione iniettiva|iniettiva]] che [[#Funzione suriettiva|suriettiva]]; quindi quando <u>dominio e immagine hanno lo stesso n° di elementi</u> ed <u>ogni</u> $x$ <u>raggiunge</u> una $y$ <u>diversa</u>.

> [!info] Test grafico per iniettività/suriettività
> Immaginiamo di disegnare tutte le possibili rette parallele all'asse x:
> ![](https://i.imgur.com/XtJHpVq.png)
> Allora, se tali rette intersecano <u>sempre</u> la funzione in:
> - <u>0 o 1 punto</u>: funzione **iniettiva**,
> - <u>1+ punti</u>: funzione **suriettiva**,
> - <u>1 punto</u>: funzione **biettiva**,
> - <u>Altrimenti</u>: funzione **né iniettiva né suriettiva**.

##### Funzioni invertibili

Per ogni <u>funzione iniettiva</u> (dove 1 $x$ = max 1 $y$) si definisce la **funzione inversa** indicata con $f^{-1}$:

$$f : X \rightarrow Im(f) \;\;\;\implies\;\;\; f^{-1} : Im(f) \rightarrow X$$

> [!info] Nota
> $y = x^{3}$ è invertibile perché iniettiva, mentre $y = x^{2}$ no. Tuttavia, se prendiamo una restrizione di $f$ in un intervallo $A$ nel quale essa è iniettiva, allora possiamo trovarne la funzione inversa parziale (per quell'intervallo): $(f|_{A})^{-1}$.
> Nel nostro esempio possiamo considerare l'intervallo $[0,+\infty)$, determinando che ${} f^{-1}(x) = \sqrt{x} {}$, oppure l'intervallo $(-\infty,0]$ che da $f^{-1}(x) = -\sqrt{x}$.

###### Caratteristiche funzioni invertibili

1) Le funzioni <u>iniettive</u> sono <u>invertibili</u> e il **dominio** di $f$ corrisponde all'**immagine** di $f^{-1}$ e viceversa,
2) Come si possono disegnare le coppie $(x,y)$ sul piano di $f$ si possono fare anche le coppie $(y,x)$ sul piano di $f^{-1}$, il che si ottiene <u>ribaltando il grafico di</u> $f$ <u>sull'asse diagonale definita dalla retta</u> $y = x$.

> [!example] Esempio
> Prendiamo ${} y = x^{3}$, per trovare la funzione inversa basta scrivere $f$ in termini di $x$, ovvero: $x = \sqrt[3]{y}$. Quindi il grafico di $f^{-1}(x) = \sqrt[3]{y}$ è:
> ![](https://i.imgur.com/EQwxeCz.png)

###### Funzioni composte

Date $f : X \rightarrow \mathbb{R}$ e $g : Y \rightarrow \mathbb{R}$ dove $Im(f) \cap Y \neq \emptyset$), si dice **funzione composta** $g \circ f$ la funzione:

$$
\left.\begin{aligned}
& g \circ f : X_{0} \rightarrow \mathbb{R} \\
& x \rightarrow g(f(x))
\end{aligned}\right.$$

(dove $X_{0} = \{x \in X : f(x) \in Y\} \subseteq X$). 

In generale $f \circ g \neq g \circ f$ ma vale la proprietà **associativa**: $f \circ (g \circ h) = (f \circ g) \circ h$.

> [!important] Teorema
> Date $f : X \rightarrow \mathbb{R}$ una funzione invertibile e $f^{-1}$ la sua inversa, allora:
> $$f^{-1} \circ f \;|\; x \rightarrow x$$
> $$f \circ f^{-1} \;|\; y \rightarrow y$$
> Infatti: $f^{-1}(f(x)) = x$ mentre $f(f^{-1}(y)) = y$.

##### Funzioni trigonometriche inverse

Le funzioni $\sin(x), \cos(x), \tan(x)$ si ripetono ogni $2k\pi$ quindi di base non sono invertibili, a meno che non le si considera in intervalli specifici in cui lo sono, quali:

- ${} \sin = \left[-\frac{\pi}{2}, \frac{\pi}{2}\right] + k\pi {}$,
- ${} \cos = [0,\pi] + k\pi {}$,
- $\tan = [-\frac{\pi}{2}, \frac{\pi}{2}] + k\pi$.

> [!important] Arcoseno, arcocoseno e arcotangente
> Le funzioni trigonometriche invertite prendono i nomi di **arcoseno**, **arcocoseno** e **arcotangente**, di seguito immagini in cui mostrato intervallo e dominio:
> ![](https://i.imgur.com/3vYSyTT.png)

##### Funzioni monotone

Una funzione $f : X \rightarrow \mathbb{R}$ si dice **monotona** se è <u>crescente o decrescente</u> in $X$ (o un sottoinsieme di esso) e **strettamente monotona** se <u>strettamente crescente/decrescente</u>.

> [!important] Teorema
> Se $f$ è <u>strettamente monotona</u> in $X$ allora è anche **invertibile** in $X$. Questo perché lo "strettamente" implica che l'immagine non ha elementi raggiunti da più di 1 elemento del dominio (non ci sono punti grafico con $y$ uguale), perciò $f^{-1}$ può correttamente avere un dominio nel quale ogni elemento ha 1 e 1 sola immagine.
> Infine, se $f$ è strettamente crescente, anche $f^{-1}$ lo sarà e viceversa con strettamente decrescente.

###### Funzioni crescenti

Una funzione si dice **crescente** quando $\;\forall x_{1}, x_{2} \;\;|\;\; x_{1} < x_{2} \;\rightarrow\; f(x_{1}) \leq f(x_{2})\;$, ovvero quando dato un punto $x_{1}$ < un altro $x_{2}$ (il 1° a sinistra e il 2° a destra nel grafico) l'immagine di entrambi mantiene la relazione in modo che $f(x_{1}) \leq f(x_{2})$.

![](https://i.imgur.com/TU2CYuL.png)

Si dice invece **strettamente crescente** quando le 2 immagini non possono essere uguali (le immagini di 2 $x$ prese sul grafico 1 dopo l'altra non hanno la $y$ uguale).

![](https://i.imgur.com/4kvrr46.png)

###### Funzioni decrescenti

Una funzione si dice **decrescente** quando $\;\forall x_{1}, x_{2} \;\;|\;\; x_{1} > x_{2} \;\rightarrow\; f(x_{1}) \geq f(x_{2})\;$, ovvero quando dato un punto $x_{1}$ > un altro $x_{2}$ (il 1° a sinistra e il 2° a destra nel grafico) l'immagine di entrambi mantiene la relazione in modo che $f(x_{1}) \geq f(x_{2})$.

![](https://i.imgur.com/dCDAwHV.png)

Si dice invece **strettamente decrescente** quando le 2 immagini non possono essere uguali (le immagini di 2 $x$ prese sul grafico 1 dopo l'altra non hanno la $y$ uguale).

![](https://i.imgur.com/wW8VLrk.png)

###### Proprietà funzioni monotone

- La somma di 2 funzioni <u>crescenti</u> è **crescente**,
- La somma di 2 funzioni <u>decrescenti</u> è **decrescente**,
- La somma di 1 funzione <u>crescente</u> e 1 funzione <u>strettamente crescente</u> è **strettamente crescente**,
- La somma di 1 funzione <u>decrescente</u> e 1 funzione <u>strettamente decrescente</u> è **strettamente decrescente**.

###### Altre funzioni

Sia $f : X \rightarrow \mathbb{R}$:

- $f$ si dice **pari** se ${} f(x) = f(-x) {}$,
- $f$ si dice **dispari** se $f(-x) = -f(x)$,
- $f$ si dice **periodica** se $\exists k \;|\; x + k \in X \;\land\; f(x+k) = f(x)$, e $k$ si chiama **periodo** di $f$.

##### Funzione esponenziale

Dato $a \in \mathbb{R}$ la funzione $f(x) = a^{x} \in \mathbb{R}$ si dice **funzione esponenziale** di base $a$.

> [!info] Nota
> La funzione esponenziale segue certe regole:
> - $a > 0$ in quanto $\forall a > 0 \rightarrow a^{x} > 0$ e perché se $0 < x < 1$ sarebbe come fare $\sqrt[x]{a}$ e non va bene se $a$ negativo,
> - $a \neq 1$ siccome $1^{x} = 1$ che è <u>funzione costante e non esponenziale</u>,
> - $a^{0} = 1$ quindi tutte le funzioni esponenziali passano per $(0,1)$.

###### Proprietà funzione esponenziale

- ${} a^{x} \cdot a^{y} = a^{x+y} {}$,
- $(a^{x})^{y} = a^{xy}$,
- Dati $x < y$, se $a > 1 \rightarrow a^{x} < a^{y}$, altrimenti se $a < 1 \rightarrow a^{x} > a^{y}$:

  ![](https://i.imgur.com/YWR7yqC.png)

> [!important] Nota
> La funzione esponenziale è quindi **strettamente monotona** (strettamente crescente per $a > 1$ e strettamente decrescente per $a < 1$), pertanto è anche una funzione invertibile.

##### Funzione logaritmica

Supponendo quindi che $n = a^{x}$ si può definire la **funzione logaritmica** come l'<u>inversa dell'esponenziale</u>, infatti si ha che: $x = \log_{a} n$ (infatti ha come dominio l'immagine dell'esponenziale e come immagine il dominio della stessa).

> [!info] Nota
> Anche la funzione logaritmica, essendo l'inversa dell'esponenziale, è definita solo per valori di $a > 0$ e $a \neq 1$ (sempre per problemi con radici di numeri negativi).
> ![](https://i.imgur.com/sSXLx8k.png)
> ![](https://i.imgur.com/K8lrd24.png)

###### Proprietà funzione logaritmica

Dati $x$ e $y$ reali si ha che:

- $\log_{a} x + \log_{a} y = \log_{a}(x \cdot y)$,
- $\log_{a} x - \log_{a} y = \log_{a}(\frac{x}{y})$,
- $\log_{a}(x^{n}) = n \cdot \log_{a}(x)$,
- $\log_{a}(x) = \frac{\log_{k}(x)}{\log_{k}(a)}$, (solo se $a > 0 \land a \neq 1$).

![](https://i.imgur.com/CcUonEW.png)

###### Logaritmo naturale

![](https://i.imgur.com/lpz761A.png)

# Esercizi

##### 1) Dominio e immagine

![](https://i.imgur.com/p3XNi9i.png)

![](https://i.imgur.com/eFa3ZWU.png)

##### 2) Iniettività e suriettività

###### 2.1) Determinare iniettività o suriettività

Dire se le seguenti funzioni sono iniettive o suriettive:

- $f(x) = \frac{1}{x}$
- $f(x) = -x^{4}$

# Soluzioni

##### 1)

##### 2)

###### 2.1)

![](https://i.imgur.com/PsZ7yGl.png)

---

Prossima lezione: [[]]

