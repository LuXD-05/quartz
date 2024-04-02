---
public: true
edited_seconds: 860
modified_at: 29/03/2024 11:55:49
---
### Cos'è?
Se una funzione è continua nell'intervallo tra gli estremi di integrazione \[a; b\], esiste almeno un punto $z$ dell'intervallo, tale che:
$$\int^{b}_{a}f(x) \; dx \;=\; (b - a) * f(z) \;\;\; con \;\;\; z \in [a; b]$$
##### Il valore medio
Questo teorema esprime l'equivalenza (per una $f(x)$ positiva e continua tra a e b) fra l'area contrassegnata da $\int^{b}_{a}f(x) \; dx$ e un rettangolo di base $(b - a)$ e altezza $f(z)$. $z$ è un punto compreso tra $a$ e $b$, e $f(z)$ invece è un punto sulla funzione ottenuto dalla proiezione di z sulla stessa.
$f(z)$ è detto **valore medio** di $f(x)$ in \[a;b\] e trova applicazione in vari problemi nei quali è usata la formula (derivata dalla precedente):
$$f(z) = \dfrac{1}{b - a} \,* \int^{b}_{a}f(x) \; dx$$
###### Esempio
Il prezzo di un bene in 5 anni (dal 2009 al 2013) è espresso con: $p(t) = 20 + 0,3t + 3e^{2-0,1t}$. Calcola il prezzo medio del bene nei primi 2 anni.
$\displaystyle f(z) = \dfrac{1}{24} \,* \int^{24}_{0} (20 + 0,3t + 3e^{2-0,1t}) \; dt$
...

---
Vedi poi: [[Integrali impropri]]