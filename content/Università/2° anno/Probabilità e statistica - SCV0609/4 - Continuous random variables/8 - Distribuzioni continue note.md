# Lezione 8

### Distribuzioni continua note

##### Distribuzione uniforme

La **distribuzione uniforme** premette che tutti i valori tra $a$ e $b$ siano <u>equiprobabili</u>, infatti la sua funzione di densità è costante:

![](https://i.imgur.com/SBC942q.png)

CDF:

$$F(x) = \dfrac{X - a}{b-a}$$

PDF ($a < x < b$)

$$f(x) = \dfrac{1}{b-a}$$

$$E[X] = \dfrac{a + b}{2}$$

$$\sigma^{2} = \dfrac{(b-a)^{2}}{12}$$

Uniforme standard: $a = 0$ e $b = 1$ ($E[X] = \frac{1}{2}$ e $\sigma^{2} = \frac{1}{12}$).

##### Distribuzione esponenziale

Una variabile aleatoria esponenziale indica il tempo tra 2 eventi di Poisson.

Qui abbiamo $\lambda$ (una frequenza, misurata in $\text{min}^{-1}$, quindi inversa rispetto a $E[X]$): n° medio di eventi che si verificano per unità di tempo (in un certo intervallo): $\dfrac{1}{E[X]}$.

CDF (solo quando $\geq 0$, altrimenti CDF = 0):

$$F(x) = 1 - e^{-\lambda \cdot x}$$

PDF (solo quando $\geq 0$, altrimenti PDF = 0):

$$f(x) = \lambda \cdot e^{-\lambda \cdot x}$$

$$E[X] = \frac{1}{\lambda}$$

$$\sigma^{2} = \frac{1}{\lambda^{2}}$$

###### Proprietà esponenziale

**Assenza di memoria**: questa proprietà indica che, dato un certo evento già accaduto $T$ quantificato da una variabile $t$ (valore aggiuntivo già passato), l'avvenire dell'evento principale $x$ (evento corrente post-$t$) non è influenzato da $t$:

$$P(X > x + t \;|\; X > x) = P(X > t)$$

(Per esempio, se chiesto: qual è la probabilità che dopo che sono passati 10 min ad aspettare, un pullman passi tra 5 min? La probabilità è la stessa di aspettare 5 min).

###### Funzione di sopravvivenza

##### Distribuzione normale

La **distribuzione normale** (o *gaussiana*) è usata nei problemi che involvono misurazioni (di solito misurazioni medie o tassi casuali). In questa la densità segue la curva di una *campana* (di Gauss) <u>simmetrica e centrata in</u> $E[X]$ (variare il valore atteso sposta la campana a destra o sinistra) con <u>dispersione indicata da</u> $\sigma$ (variare la deviazione standard la concentra o appiattisce).

CDF

$$F(x) = \Phi(\dfrac{x - \mu}{\sigma})$$

PDF

$$f(x) = \dfrac{1}{\sigma \cdot \sqrt{2\pi}} \cdot e^{-\dfrac{(x-E[X])^{2}}{2\sigma^{2}}}$$

$$E[X] = \mu$$

$$Var[X] = \sigma^{2}$$

###### Distribuzione normale standard

La **normale standard** è una distribuzione normale i cui parametri sono: $\mu = 0$ e $\sigma = 1$. Il suo uso principale è quello di sfruttare le caratteristiche dei suoi parametri per "standardizzare" i valori delle distribuzioni normali e a tale scopo si definisce una variabile aleatoria $Z$:

$$Z = \dfrac{X - \mu}{\sigma}$$

Da cui si può ricavare la formula inversa (per problemi di <u>destandardizzazione</u>, che danno già $\Phi(z)$ e chiedono di trovare $x$):

$$x = \mu + \sigma \cdot \Phi^{-1}$$

Con ciò si ridimensionano le curve a campana delle normali rendendole standard (centrate e concentrate/appiattite) in modo da ottenere un valore $z$ che indica quanto $x$ <u>è lontano dalla media in termini di</u> $\sigma$ (tipo se $Z = -2(\sigma)$, allora il valore è molto sotto la media).

> [!important] Tabella normale
> La standardizzazione è utile anche per evitare di calcolare integrali complicati per ogni misurazione grazie alla **tabella normale**, che contiene dei valori così indicizzati:
> \- **Verticalmente** (a sinistra): i valori sono disposti in base alla <u>prima cifra intera e alla prima decimale di</u> $z$,
> \- **Orizzontalmente** (in alto): i valori sono disposti in base alla <u>seconda cifra decimale di</u> $z$.
> Questo processo di <u>individuazione del valore nella tabella normale</u> è indicato con:
> $$\Phi(z)$$
> Questa permette di sfruttare la simmetria della PDF standard anche in caso ci siano <u>valori e/o formule inverse</u> da calcolare (con $-\infty < z < \infty$):
> $$\Phi(-z) = 1 - \Phi(z)$$

---

Prossima lezione: [[9 - Diseguaglianze probabilistiche]]

