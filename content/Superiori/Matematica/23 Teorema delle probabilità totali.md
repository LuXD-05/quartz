---
modified_at: 13/05/2024 22:23:15
edited_seconds: 1070
---
### Teorema delle probabilità totali
Hint: def, formula, es (spiegaz)
::
> [!important] Teorema delle probabilità totali
> Il teorema delle probabilità totali definisce la <u>probabilità che 2 eventi si verifichino congiuntamente</u> (ovvero la probabilità che si realizzi l'<u>intersezione</u> tra essi).
##### Formula
$$p(E) \;=\; p(E|E_{i}) * p(E_{i}) \; \ldots$$
##### Esercizio
###### Problema
Si hanno 2 monete, 1 è truccata in modo che la probabilità che un suo lancio faccia testa è $\frac{1}{3}$. Si lancia una delle 2 monete scegliendola a caso. Quale è la probabilità che esca testa?
###### Step
0) Dati,
1) Calcolare la probabilità che si verifichino i casi da prendere in considerazione,
2) Calcolare la probabilità dell'evento per ogni caso,
3) Calcolare la probabilità totale con la formula: $p(E) \;=\; p(E|E_{i}) * p(E_{i}) \; \ldots$
###### Risoluzione
$p(T) \;=\; ? \;\;\; | \;\;\; (m_{1} \;=\; moneta \; normale) \;\;\; | \;\;\; (m_{2} \;=\; moneta \; truccata)$
Si trovano le probabilità che i casi si verifichino:
$p(m_{1}) \;=\; \dfrac{1}{2} \;\;\;|\;\;\; p(m_{2}) \;=\; \dfrac{1}{2}$
Si calcola la probabilità dell'evento per ogni caso:
$p(T|m_{1}) \;=\; \dfrac{f}{N} \;=\; \dfrac{1}{2} \;\;\;|\;\;\; p(T|m_{2}) \;=\; \dfrac{f}{N} \;=\; \dfrac{1}{3}$
Si calcola la probabilità totale:
$p(T) \;=\; p(T|m_{1}) * p(m_{1}) + p(T|m_{2}) * p(m_{2}) \;=\; \dfrac{1}{2} * \dfrac{1}{2} + \dfrac{1}{3} * \dfrac{1}{2} \;=\; \dfrac{5}{12}$

---
Vedi poi: [[24 Teorema di Bayes]]