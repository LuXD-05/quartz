# Lezione 19

###### Simmetrizzabilità in $(\mathbb{Z}_{n},\cdot)$

Considerando il precedente [[18 - Strutture algebriche#7)|esempio]], si nota una correlazione tra le varie classi di resto ed $n$:

> [!important] Numeri coprimi
>  Due numeri $m$ ed $n$ si dicono **coprimi** se il loro $MCD = 1$.
>  Inoltre, se e solo se $MCD(m,n) = 1$, allora in $\mathbb{Z}_{n}$ è verificato che $[m]_{n}$ è [[18 - Strutture algebriche#Simmetrizzabilità|simmetrizzabile]].
>  Perciò, se $n$ è un <u>numero primo</u>, tutte le classi $[m]_{n}$ sono <u>simmetrizzabili</u> eccetto per $[0]_{n}$; questo rende $(\mathbb{Z}^{+},\cdot) = (\mathbb{Z}_{n} - \{[0]_{n}\},\cdot)$ un **gruppo**.

### Funzione di Eulero

La **funzione di Eulero**, definita con la lettera greca $\varphi$ (*phi*), <u>conta quanti sono i coprimi</u> $< n$ (e di $n$) nell'insieme $\mathbb{N}^{+}$. In generale:

$$\forall n \in \mathbb{N} \;\rightarrow\; \varphi(n) = \lvert\,\{\; m \in \mathbb{N}^{+} \;|\; MCD(m,n) = 1 \;\land\; 0 < m < n \;\}\,\lvert$$

###### Procedimento

In caso esca una domanda del tipo: "Calcolare i coprimi di $x$", il procedimento è:

1) Riscrivo $x$ come il prodotto dei suoi fattori primi,
2) Verificare che l'MCD tra i suddetti fattori = 1,
3) Fare $\varphi(x)$ riscrivendo $x$ come prodotto dei suoi fattori primi e applicare le proprietà (eventualmente).

###### Alternativa

Una formula alternativa per il calcolo di $\varphi$ è:

$$\varphi(n)=n\cdot\prod\limits^{k}_{i=1}(1 - \dfrac{1}{p_{i}})$$

##### Proprietà

- Se $x$ è numero primo $\;\rightarrow\; \varphi(x) = x-1$
- Se $MCD(x,y) = 1 \;\rightarrow\; \varphi(x \cdot y) = \varphi(x) \cdot \varphi(y)$
- $\varphi(x^{n}) = x^{n} - x^{n-1}$

# Esercizi

###### 1) $\varphi$

Calcola il n° di coprimi di 12.

###### 2) Funzioni di $A \rightarrow A$

# Soluzioni

###### 1)

1) ${} 12 = 2^{2} \cdot 3 {}$
2) $MCD(2^{2},3) = 1$
3) $\varphi(12) = \varphi(2^{2} \cdot 3) = \varphi(2^{2}) \cdot \varphi(3) = (2^{2} - 2^{1}) \cdot 2 = 4$

---

Prossima lezione: [[20 - Sottostrutture algebriche]]

