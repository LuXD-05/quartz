# Lezione 6

### Distribuzioni note

##### Distribuzione di Bernoulli

Una variabile aleatoria si dice di **Bernoulli** se la sua **distribuzione** è di Bernoulli, ovvero segue certe regole:

Presupponiamo di avere un esperimento binario (tipo testa o croce) dove i 2 esiti sono: "successi" (1) e "insuccessi" (0); le loro probabilità sono:

$$P(1) = p \;\;\;\;\;|\;\;\;\;\;P(0) = (1-p) = q$$

Calcolandone valore atteso e varianza si ha:

$$E[X] = \sum\limits_{x} x \cdot P(x) = 0q + 1p = p$$

$$\sigma^{2} = \sum\limits_{x} ({\color{aqua}{x}} - p)^{2} \cdot {\color{lightgreen}{P(x)}} = ({\color{aqua}{0-p}})^{2} \cdot {\color{lightgreen}{(1-p)}} + ({\color{aqua}{1-p}})^{2} \cdot {\color{lightgreen}{p}} = \ldots = {\color{yellow}{p(1-p)}}$$

Tutto ciò solo per dimostrare quanto abbiamo stabilito all'inizio:

$$P(x) = \begin{cases} x=0 \implies {\color{yellow}{1-p}} \\ x=1 \implies {\color{yellow}{p}} \end{cases}$$

Ed in più:

$$E[X] = p \;\;\;\;\;|\;\;\;\;\; \sigma^{2} = p(1-p) = pq$$

##### Distribuzione binomiale

La **distribuzione binomiale** fa uso delle <u>variabili di Bernoulli</u> applicandole però su una <u>sequenza di esperimenti</u>, la quale ha 2 parametri: $n$ che è il <u>n° di prove</u> e $p$ che è la <u>probabilità di successo</u>. La sua PMF è:

$$P(x) = \binom{n}{x} \cdot p^{x} \cdot q^{n-x}$$

Il valore atteso è:

$$E[X] = n \cdot p$$

Mentre la varianza è:

$$\sigma^{2} = n \cdot p \cdot q$$

###### Particolarità binomiale

La somma delle probabilità per tutti i possibili valori di $x$ è 1 (infatti (*fill after binom in counting*)):

$$\sum\limits_{x=0}^{n} \binom{n}{x} p^{x} q^{n-x} = 1$$

Mentre i casi estremi sono (tutti successi e tutti insuccessi rispettivamente):

$$P(X = n) \rightarrow p^{n} \;\;\;\;\;|\;\;\;\;\; P(X = 0) \rightarrow (1-p)^{n}$$

##### Distribuzione di Poisson

La **distribuzione di Poisson** è usata specificatamente per modellare **eventi rari** (o *poissoniani*) che avvengono (per l'appunto) raramente <u>durante un certo lasso di tempo o spazio</u>.

Questa fa uso di un solo parametro: $\lambda$ (***lambda***), che rappresenta <u>il tasso medio di occorrenza degli eventi</u> (nota: la Poisson può essere derivata dalla binomiale quando $n$ è molto grande e $p$ è molto piccola con ${} np$ costante al crescere di $n$).

Comunque PMF, valore atteso e varianza sono:

$$P(x) = \dfrac{\lambda^{x}}{x!} \cdot e^{-\lambda}$$

$$E[X] = \lambda$$

$$\sigma^{2} = \lambda$$

Negli esercizi verrà chiesto generalmente quant'è la probabilità che un evento si verifichi più di un certo n° di volte in un certo lasso di tempo; quindi, dato che le volte possono essere da 0 a $\infty$ (e non si può calcolare la probabilità su $\infty$) bisognerà calcolare la probabilità dell'evento contrario e sottrarla con $1 - p$ per avere la probabilità dell'evento.

(riformulare)

> [!important] Quando usare Poisson
> 1) La Poisson va usata quando si verificano eventi (rari) **durante un intervallo di tempo** ($n$ grande e $p$ molto piccola),
> 2) Quando tali eventi sono <u>potenzialmente infiniti</u> calcolare $q$ (1 - probabilità evento contrario), altrimenti $p$ normalmente (se si ha un n° max di eventi nel tempo),
> 3) La Poisson <u>non si usa con eventi dipendenti</u>.

###### Ricavo Poisson da binomiale

(3.3.5 dove spiega i passaggi)

---

Prossima lezione: [[7 - Continuous random variables]]

