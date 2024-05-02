# Angoloidi

> [!important] Angoloide
> Dato un poligono convesso e un punto V non appartenente al suo piano, si chiama angoloide di vertice V la figura formata da tutte le semirette di origine V che passano per i punti del poligono dato, inclusi quelli appartenenti al suo contorno.

Le semirette che passano per il punto V e per i vertici del poligono si chiamano spigoli dell'angoloide. 

In particolare, un angoloide con tre spigoli si chiama triedro. 

Gli angoli che hanno come vertice V e come lati due spigoli consecutivi si dicono facce dell'angoloide.

![](https://i.imgur.com/fqkJlpS.png)

### Piramidi

> [!important] Piramide
> Si chiama piramide la parte di un angoloide compresa tra il vertice dell'angoloide e un piano che interseca tutti gli spigoli dell'angoloide.

![](https://i.imgur.com/8NxIyUq.png)

> [!important] Piramide retta
> Una piramide si dice retta se la base è un poligono circoscrivibile a una circonferenza e il centro di tale circonferenza coincide con il piede dell'altezza della piramide.

![](https://i.imgur.com/ML44FxO.png)

> [!important] Piramide regolare
> Una piramide si dice regolare se è retta e la base è un poligono regolare (equilatero ed equiangolo).

![](https://i.imgur.com/jJWiE0M.png)

Una piramide si dice triangolare, quadrangolare, pentagonale... a seconda che la sua base sia un triangolo, un quadrilatero, un pentagono... 

In particolare, una piramide a base triangolare si chiama tetraedro.

##### Apotema di una piramide retta

In una piramide retta, ciascuna altezza delle facce laterali (relativa al proprio spigolo di base) è detta **apotema** della piramide.

![](https://i.imgur.com/IMk1Eg6.png)

### Calcolo dell'area

##### Area di una piramide retta

Si parte calcolando l'area laterale $A_{l}$ e questa si fa sommando l'area di ogni faccia (con $l$ = base faccia e $a$ = apotema):

$A_{l} \;=\; \dfrac{1}{2}l_{n} * a$

Però, $\dfrac{1}{2}l_{n}$ corrisponde al semiperimetro (sarebbe $\dfrac{1}{2}(l_{1} + l_{2} + \;\ldots\; l_{n})$), quindi:

$A_{l} \;=\; \dfrac{p}{2} * a$

Per calcolare poi la superficie totale basta aggiungere ad $A_{l}$ l'area della base:

$A \;=\; \dfrac{p}{2} * a + A_{b}$

$h_{max} \;=\; \sqrt{3}$

$b^{2}_{max} \;=\; 36 - 4h^{2} \;\;\rightarrow\;\; b^{2}_{max} \;=\; 36 - 4(\sqrt{3})^{2} \;\;\rightarrow\;\; b^{2}_{max} \;=\; 24 \;\;\rightarrow\;\; b_{max} \;=\; \pm\sqrt{24} < 2\sqrt{6} acc   -2\sqrt{6} non acc$

Sistemare richiesta e richiedere le <u>dimensioni</u> della piramide con vol max...

Trovare il modo di fare il < grande come se fosse il risultato della x di un'equazione di 2° grado

### Calcolo del volume

##### Volume di una piramide retta

Una piramide retta equivale a 1/3 del prisma avente la sua stessa base e la sua stessa altezza, quindi:

$V \;=\; \dfrac{1}{3}V_{prism} \;=\; \dfrac{1}{3}A_{b} * h$

###### Step

0) Scrivere i dati (+ $h_{min/max}$ e $b_{min/max}$ in quanto il $V_{min/max}$ si calcola con esse).
1) Fare il disegno
2) Trovare la base della piramide tramite il teorema di Pitagora applicato su:

   $a$ = ipotenusa

   $h$ = cateto lungo

   $\frac{b}{2}$ = cateto corto

   La base sarà da calcolare in base al n° di lati.

3) Calcolare il volume
4) Calcolare la derivata del volume
5) Studiare il segno della suddetta e trovare il max o il min in base a cosa è richiesto
6) Calcolare il $V_{max/min}$ dai dati ottenuti

###### Esercizio

Fra tutte le piramidi regolari a base quadrata di apotema 3, quale ha il volume maggiore?

Dati: $a \,=\, 3 \;\;\lvert\;\; h_{max} \;=\; ?  \;\;\lvert\;\; b_{max} \;=\; ?$

Formula dal teorema di Pitagora:

$h^{2} + (\dfrac{b}{2})^{2} \;=\; a^{2}$

Sostituisco il termine noto (in questo caso l'apotema):

$h^{2} + (\dfrac{b}{2})^{2} \;=\; 9$

Quindi:

$h^{2} + \dfrac{b^{2}}{4} \,=\, 9 \;\;\rightarrow\;\; \dfrac{4h^{2} + b^{2}}{4} \,=\, 9 \;\;\rightarrow\;\; b^{2} \,=\, (9 * 4) - 4h^{2} \;\;\rightarrow\;\; b^{2} \,=\, 36 - 4h^{2}$

$V \;=\; \dfrac{1}{3}A_{b} * h \;=\; \dfrac{1}{3}b^{2} * h \;=\; \dfrac{1}{3} * (36 - 4h^{2}) * h \;=\; 12h - \dfrac{4}{3}h^{3}$

$V' \;=\; (12h - \dfrac{4}{3}h^{3})' \;=\; 12 - \dfrac{4}{3} * 3h^{2} \;=\; 12 - 4h^{2}$

$V' > 0 \;\;\rightarrow\;\; 12 - 4h^{2} > 0 \;\;\rightarrow\;\; 3 - h^{2} > 0 \;\;\rightarrow\;\; h^{2} < 3 \;\;\rightarrow\;\; h < \pm\sqrt{3} \;\;\rightarrow\;\; (graf) \;=\; -\sqrt{3} < h < \sqrt{3}$

(dis)

$h_{max} \;=\; ...$

---

Vedi poi: [[25 Solidi di rotazione]]

