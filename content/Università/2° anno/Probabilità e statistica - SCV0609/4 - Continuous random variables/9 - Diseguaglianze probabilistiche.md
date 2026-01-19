# Lezione 9

### Diseguaglianze probabilistiche

Le diseguaglianze probabilistiche sono strumenti utili che aiutano nel calcolo di variabili aleatorie (sia discrete che continue) in quei casi in cui non si conosce la forma della distribuzione (magari quando mancano certi parametri).

##### Diseguaglianza di Markov

(Spesso) quando si ha la media ($E[X]$) di una distribuzione ma non la si conosce, è possibile usare la **diseguaglianza di Markov** (solo se $X$ è sempre $\geq 0$), la quale indica quanto è probabile che $x \geq a$ (quanti valori $x$ sul totale sono $\geq a$) ed è:

$$P(X \geq a) \leq \dfrac{E[X]}{a}$$

(Per esempio se un lavoro ci mette in media 5 ore, la probabilità che ce ne metta 10 è $P(X \geq 10) \leq \frac{5}{10} = 0.5$; se $10$ è il limite imposto a $x$, $0.5$ è il limite imposto alla probabilità che $x \geq 10$).

> [!info] Quando può servire
> Markov è principalmente usato in problemi che richiedono di calcolare la probabilità massima di un evento (quindi quanto è improbabile che superi un certo limite). Per esso gli esercizi forniscono solo la media e una variabile $X \geq 0$.

##### Diseguaglianza di Čebyšëv

La **diseguaglianza di Čebyšëv** estende Markov rimuovendone il vincolo di positività di $X \geq 0$ e sfrutta media e varianza per definire un limite alla probabilità che $X$ si allontani dalla media di un certo n° di $\sigma$ (deviazione standard usata come unità di spostamento). In pratica indica la probabilità che lo <u>spostamento dal centro</u> di una variabile aleatoria $X$, non può mai superare $\dfrac{1}{\lambda^{2}}$. Si hanno 2 formule identiche:

$$P(|X - \mu| \geq \lambda\sigma) \leq \dfrac{1}{\lambda^{2}} \;\;\;\;\;\lvert\;\;\;\;\; P(|X - \mu| \geq k) \leq \dfrac{\sigma^{2}}{k^{2}}$$

Dove ${} {\color{yellow}{\lambda}}$ è il n° di $\sigma$ di spostamento dalla media, mentre ${\color{yellow}{k }} = \lambda\sigma$ è un numero scelto o fornito che indica la distanza dei limiti dalla media. (Di solito <u>è più comodo usare la 2a formula</u> in quanto è più probabile che venga fornita la **varianza** ($\sigma^{2}$) rispetto al **n° di deviazioni standard** ($\sigma$) di spostamento dalla media).

> [!info] Quando può servire
> Čebyšëv invece è più usato in problemi in cui si vuole calcolare quanto $X$ si discosta dalla media, ovvero quando sono forniti dei limiti superiori e inferiori rispetto alla media. Per esso gli esercizi forniscono media, varianza e dei margini (di solito simmetrici rispetto alla media).

---

