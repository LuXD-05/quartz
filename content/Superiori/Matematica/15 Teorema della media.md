### Teorema della media

> [!important] Teorema della media
> Se una funzione è <u>continua</u> nell'intervallo tra gli estremi di integrazione \[a; b\], esiste almeno un punto $z$ dell'intervallo, tale che:
> $$\int^{b}_{a}f(x) \; dx \;=\; (b - a) * f(z) \;\;\; con \;\;\; z \in [a; b]$$

##### Approfondimento

Prendiamo come esempio questa funzione:

![](https://i.imgur.com/9VfZN9O.png)

Siccome la $f(x)$ è continua in \[a; b], allora nell'intervallo assumerà 2 valori: uno minimo ($m$) e uno massimo ($M$), tali per cui:

$$m \;\le\; f(x) \;\le\; M$$

Secondo il [[17 Teorema del confronto]] (perché???) vale anche la diseguaglianza:

$$\int^{b}_{a} m \;dx \;\le\; \int^{b}_{a} f(x) \;dx \;\le\; \int^{b}_{a} M \;dx$$

Applicando la proprietà dell'[[12 Integrali definiti#Proprietà|integrale di una funzione costante]] (nonostante si stia calcolando l'integrale su un punto, questo è sempre costante), vale:

$$m(b - a) \;\le\; \int^{b}_{a} f(x) \;dx \;\le\; M(b - a)$$

E dividendo tutto per $(b - a)$ si ottiene:

$$m \;\le\; \dfrac{\displaystyle\int^{b}_{a} f(x) \;dx}{b - a} \;\le\; M$$

Secondo il teorema della media ($f(x)$ deve assumere almeno 1 volta tutti i valori compresi tra $m$ e $M$, quindi) deve esistere un punto $z$ in \[a; b] per cui:

$$f(z) \;=\; \dfrac{\displaystyle\int^{b}_{a} f(x) \;dx}{b - a}$$

##### Il valore medio

Questo teorema esprime l'equivalenza (per una $f(x)$ positiva e continua tra a e b) fra l'area contrassegnata da $\int^{b}_{a}f(x) \; dx$ e un rettangolo di base $(b - a)$ e altezza $f(z)$. $z$ è un punto compreso tra $a$ e $b$, e $f(z)$ invece è un punto sulla funzione ottenuto dalla proiezione di z sulla stessa.

![](https://i.imgur.com/KoiDm2w.png)

$f(z)$ è detto **valore medio** di $f(x)$ in \[a;b\] e trova applicazione in vari problemi nei quali è usata la formula (derivata dalla precedente):

$$f(z) = \dfrac{1}{b - a} \,* \int^{b}_{a}f(x) \; dx$$

###### Esempio

Il prezzo di un bene in 5 anni (dal 2009 al 2013) è espresso con: $p(t) = 20 + 0,3t + 3e^{2-0,1t}$. Calcola il prezzo medio del bene nei primi 2 anni.

$\displaystyle f(z) = \dfrac{1}{24} \,* \int^{24}_{0} (20 + 0,3t + 3e^{2-0,1t}) \; dt$

...

---

Vedi poi: [[16 Integrali impropri]]

