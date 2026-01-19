# Lezione 5

### Variabili aleatorie discrete

Una variabile aleatoria discreta $X$ è una<u> funzione che in base a un esito</u> $\omega$ <u>ne determina un numero reale</u> (appartenente ad un insieme $D$, sottoinsieme di $\mathbb{R}$), ha dominio $\Omega$ e codominio $D$ e si indica con:

$$X = f(\omega)$$

Questo significa che ad ogni esito $\omega$ vi è associato un numero reale di $D$ attraverso la variabile aleatoria $X$, quini descrivibile anche con:

$$X(\omega)$$
(Non è la probabilità di $\omega$, bensì semplicemente un numero associato ad esso e ad ogni altro esito).
###### Random variables associate ad eventi
Si possono avere variabili aleatorie discrete <u>associate a più esiti</u> (considerabili quindi come <u>associate ad un evento</u>), per esempio, lanciando 3 monete e contando il n° di teste in sequenza avremmo che:
$$X = \{0, 1, 2, 3\}$$

Questo si può indicare con: $X(\omega_{i}) = x$ o $X = x$ dove $\omega_{i}$ è il gruppo di esiti e $x$ è un valore della variabile aleatoria uguale e associato a tutti gli esiti del gruppo.

$P(X = 0) = P(CCC) = \frac{1}{2} \cdot \frac{1}{2} \cdot \frac{1}{2} = \frac{1}{8}$

##### PMF

La **PMF** (*Probability Mass Function*) è una funzione che calcola la <u>probabilità dell'intero gruppo di esiti</u> delineato da un **valore** ($x$) di una <u>variabile aleatoria discreta</u> $X$, e si indica con:

$$P(X = x_{i})$$

Esempio (prima finire):

$$
p_X(k) =
\begin{cases}
\dfrac{1}{8} & k = 0 \\
\dfrac{3}{8} & k = 1 \\
\dfrac{3}{8} & k = 2 \\
\dfrac{1}{8} & k = 3 \\
0 & \text{altrimenti}
\end{cases}
$$

> [!info] Proprietà
> 1) $p \leq P(X = x) \leq 1$ per ogni $x$,
> 2) $\sum\limits_{x} P(X = x) = 1$

###### CDF

La **CDF** (*Cumulative Distribution Function*) è invece una funzione che calcola la probabilità combinata di tutti i valori minori o uguali a una certa $x$, e si indica con:

$$F(x) = P(X \leq x) = \sum\limits_{y \leq x} P(y)$$

L'insieme dei valori possibili di $X$ si dice **supporto** della distribuzione $F$.

![](https://i.imgur.com/rPBB9qa.png)

![](https://i.imgur.com/b2jAmOC.png)

![](https://i.imgur.com/hfh5N0w.png)

#### Valore atteso

Basando la variabile aleatoria $X$ su un evento, ognuno dei suoi valori possibili $x$ è associato a degli esiti $\omega$ in base a cui (n° di esiti per valore di $X$) è possibile calcolare la probabilità che dall'esperimento "esca" uno di essi (con [[#PMF|PMF]]).

Il **valore atteso** ($\mu$) di una variabile aleatoria è la <u>somma dei "tipi di esiti"</u> ($x$) <u>moltiplicata per la loro probabilità di "uscire"</u> (la PMF: $P(X = x)$); ciò si può vedere anche come:

$$\mathbb{E}[X] = \mu = \sum\limits_{x} x \cdot P(x)$$

Si può considerare $\mu$ come una <u>media ponderata</u> dei vari valori di $X$ in base alle loro probabilità $P(x)$.

###### Valore atteso di funzione

Nel caso si abbia una variabile cumulativa detta $Y$ che raggruppa altre $X$ in base ad una certa formula, si può definire $Y = f(X)$ e sostituire nella formula del valore atteso:

$$\mathbb{E}[f(X)] = \sum\limits_{x} f(x) \cdot P(x)$$

> [!important] LOTUS
> La LOTUS (o *legge dello statistico inconscio*) è ...
> ![](https://i.imgur.com/o7uJJ22.png)

##### Proprietà

Date 2 variabili aleatorie $X$ e $Y$ e 2 numeri $a$ e $b$ vale:

$$E[aX + bY] = aE[X] + bE[Y]$$

Questo grazie ad altre proprietà:

$$E[a] = a \;\;\;\;\;|\;\;\;\;\; E[X + a] = E[X] + a \;\;\;\;\;|\;\;\;\;\; E[aX] = a \cdot E[X]$$

Per il valore atteso di <u>somme di variabili aleatorie</u>:

$$E\left[\sum\limits_{i=1}^{n} X_{i}\right] \;=\; \sum\limits_{i=1}^{n} E[X_{i}]$$

Per variabili aleatorie <u>solo indipendenti</u> moltiplicate (vale anche per alcune dipendenti):

$$E[XY] = E[X] \cdot E[Y]$$

#### Varianza

La **varianza** di una variabile aleatoria è definita come il <u>valore atteso</u> ($E$) <u>dello scarto dalla media</u> ($X - \mu$) <u>al quadrato</u>. Questa è fondamentale per capire quanto variano le variabili aleatorie dal loro valore medio; e si definisce così:

$$\sigma^{2} = Var(X) \;\;=\;\; E[(X - \mu)^{2}] \;\;=\;\; E[X^{2}] - E[X]^{2} \;\;=\;\; {\color{yellow}{\sum\limits_{x} (x - E[X])^{2} \cdot P(x)}}$$

La varianza è uguale a 0 solo se $x = \mu$ per ogni $x$ (ovvero $X$ ha sempre la stessa probabilità).

> [!info] Elevazione al quadrato
> Se non venisse fatta l'elevazione al quadrato, si otterrebbe che:
> $$Var(X) = E[X - E[X]] = E[X] - E[X] = 0$$
> E questo non avrebbe senso in quanto non da informazioni sulla distribuzione di $X$, mentre con l'elevazione sarebbe:
> $$\sigma^{2} = E[(X - E[X])^{2}] = E[X^{2}] - E[X]^{2}$$

###### Deviazione standard

La **deviazione standard** è semplicemente la radice quadrata della varianza:

$$\sigma = Std(X) = \sqrt{Var(X)}$$

Comunque è molto importante in quanto "traduce" le unità di misura al quadrato della varianza in unità sensate.

##### Proprietà

Anche la varianza ha delle proprietà fondamentali:

- **Non-negatività**: $\;\;\;\sigma^{2} \geq 0$
- **Varianza di costante**: $\;\;\;Var(a) = 0$
- **Somma con costante**: $\;\;\;Var(X + a) = Var(X)$
- **Moltiplicazione per costante**: $\;\;\;Var(aX) = a^{2} \cdot Var(X)$
- **Somme di variabili aleatorie** (<u>solo se indipendenti</u>): $\;\;\;Var(X + Y) = Var(X) + Var(Y)$

---

Prossima lezione: [[6 - Distribuzioni discrete note]]

