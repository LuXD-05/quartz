---
modified_at: 21/05/2024 18:50:17
edited_seconds: 640
---
### Teorema di Bayes
Hint: def, formula, es
::
> [!important] Teorema di Bayes
> Il teorema di Bayes permette di trovare la probabilità che, dato un evento $E$, la sua causa sia $E_{i}$. Ciò è espresso dal rapporto tra la [[23 Teorema delle probabilità totali|probabilità totale]] di un evento (dato un altro) e la probabilità dell'evento stesso.
##### Formula
$$p(E_{i}|E) \;=\; \dfrac{p(E_{i}) * p(E|E_{i})}{p(E)}$$
##### Esercizio
###### Problema
Una dispensa ha 2 ceste di mele:
1) 70% mature, resto acerbe,
2) 90% mature, resto acerbe.
Scegliere a caso una cesta e prendere una mela. Probabilità che sia matura?
Sapendo che matura, probabilità che estratta da cesta 1?
###### Step
0) Dati (tutti)
1) (Anche se è probabilità totale: trovare la probabilità totale dell'evento richiesto)
2) Dato l'evento, trovare la probabilità del secondo evento richiesto (Bayes)
###### Risoluzione
$p(C_{1}) \;=\; p(C_{2}) \;=\; \dfrac{1}{2} \;\;\;|\;\;\; p(M|C_{1}) \;=\; \dfrac{7}{10} \;\;\;|\;\;\; p(M|C_{2}) \;=\; \dfrac{9}{10}$
 
$p(M) \;=\; p(C_{1}) * p(M|C_{1}) + p(C_{2}) * p(M|C_{2}) \;=\; 0,7 * 0,5 + 0,9 * 0,5 \;=\; 0,8 \;=\; 80\%$
 
$p(C_{1}|M) \;=\;$

---
Vedi poi: [[25 Prismi e parallelepipedi]]