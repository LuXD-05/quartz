### Eventi compatibili

> [!important] Compatibilità
> 2 eventi sono **compatibili** quanto il verificarsi di uno <u>non esclude</u> il verificarsi (contemporaneo) dell'altro. In pratica se hanno un'intersezione.
> 2 eventi sono **incompatibili** invece quando il verificarsi di uno <u>esclude</u> il verificarsi dell'altro. In pratica quando la loro intersezione è = $\varnothing$.

--- start-multi-column: ID_50s0
```column-settings
Number of Columns: 2
Largest Column: standard
Alignment: center
Border: off
```

![](https://i.imgur.com/BTrvJju.png)

--- column-break ---

![](https://i.imgur.com/wl3q1xa.png)

--- end-multi-column

##### Somma logica di eventi

Dato che gli eventi sono degli <u>insiemi</u>, è possibile eseguire con essi l'operazione di **somma logica** (corrispondente all'**unione**).

![](https://i.imgur.com/e9o4bnQ.png)

La **somma logica** di 2 eventi si rappresenta con: $\; E_{1} \;\cup\; E_{2} \;$. Quindi:

- Per gli eventi **compatibili**: $\;\;\;\; p(E_{1} \,\cup\, E_{2}) \;=\; p(E_{1}) \;+\; p(E_{2}) \;-\; p(E_{1} \,\cap\, E_{2})$
- Per gli eventi **incompatibili**: $\; p(E_{1} \,\cup\, E_{2}) \;=\; p(E_{1}) \;+\; p(E_{2}) \;-\; 0 \;$ (dato che l'intersezione tra i 2 eventi è = $\varnothing$)

##### Esercizio

###### Problema

Si consideri quindi la seguente situazione: si estrae una carta da un mazzo di 52. Si considerino poi 2 eventi:

- $E_{1}$ = "esce un 4"
- $E_{2}$ = "esce un seme nero"

Quale è la probabilità che gli eventi si verifichino entrambi? 

###### Step

1) Trovare $S$, la $f$ per ogni evento e (eventualmente) la $f$ per ogni intersezione:
2) Calcolare le probabilità di ogni evento e quella delle intersezioni tra questi (2 alla volta):
3) Calcolare l'unione:

###### Risoluzione

$S \;=\; \{\; 1 \;\ldots\; 52 \;\} \;\;\lvert\;\; f_{1} \;=\; \{\; 4_{c}, 4_{q}, 4_{f}, 4_{p} \;\} \;\;\lvert\;\; f_{2} \;=\; \{\; (1 \ldots 10 + J, Q, K)_{p} \;+\; (1 \ldots 10 + J, Q, K)_{f}\;\} \;\;\lvert\;\; E_{1} \;\cap\; E_{2} \;=\; \{\; 4_{f}, 4_{p} \;\}$

$p(E_{1}) \;=\; \dfrac{f_{1}}{N} \;=\; \dfrac{1}{13} \;\;\;\lvert\;\;\; p(E_{2}) \;=\; \dfrac{f_{2}}{N} \;=\; \dfrac{1}{2} \;\;\;\lvert\;\;\; p(E_{1} \;\cap\; E_{2}) \;=\; \dfrac{f}{N} \;=\; \dfrac{\#(E_{1} \;\cap\; E_{2})}{\#S} \;=\; \dfrac{1}{26}$

$p(E_{1} \;\cup\; E_{2}) \;=\; p(E_{1}) \;+\; p(E_{2}) \;-\; p(E_{1} \;\cap\; E_{2}) \;=\; \dfrac{1}{13} \;+\; \dfrac{1}{2} \;-\; \dfrac{1}{26} \;=\; \dfrac{7}{13}$

---

Vedi poi: [[22 Probabilità condizionata e prodotto logico]]

