### Cosa sono

Gli integrali impropri sono degli integrali particolari che hanno in 1 o in entrambi gli estremi di integrazione un valore in cui la funzione da integrare non è definita / ha un asintoto / tende a $\pm\infty$.

##### Convergenza e divergenza

- Integrale **convergente** in un intervallo: è un'integrale il cui **limite** su 1 o entrambi gli **estremi di integrazione** risulta **finito** (quindi un numero); questo tipo di integrale ha come **estremi 2 numeri finiti** dei quali **almeno 1 è un'asintoto** della funzione da integrare. 
- Integrale **divergente** in un intervallo: è un'integrale il cui **limite** su 1 o entrambi gli **estremi di integrazione** risulta **infinito** o **inesistente**; questo tipo di integrale ha come **estremi** (raramente 2 infiniti, di solito) **un numero finito e un infinito** (positivo o negativo).

### Casi e risoluzione

##### Integrale improprio convergente

###### Risoluzione

1) Trovare il dominio della funzione da integrare.
2) Calcolare il limite (tenendo conto dell'intervallo definito dagli estremi di integrazione) della funzione con x tendente al valore infinitesimale + o - (in base alla funzione e a dove si trova / al suo dominio) del dominio.
3) Se il limite nel punto calcolato è $+\infty\,$ o $\,-\infty$, antecedere all'integrale iniziale lo stesso limite però con t tendente al valore infinitesimale di prima e sostituire all'estremo di integrazione in cui vi è l'asintoto questa t.
4) Risolvere infine l'integrale e applicare il limite.

###### Esempio

$\displaystyle\int^{1}_{0} \dfrac{\ln^{2}{x}}{x} \; dx \; \Biggr| \; D: x > 0$

$\;\;\;\;\;\displaystyle \lim_{x \to 0^{+}} \dfrac{\ln^{2}{x}}{x} \;=\; \dfrac{\ln^{2}{0}}{0^{+}} \;=\; \dfrac{+\infty}{0^{+}} \;=\; +\infty$

$\displaystyle \lim_{t \to 0^{+}} \int^{1}_{t} \dfrac{\ln^{2}{x}}{x} \; dx \;=\; \lim_{t \to 0^{+}} \int^{1}_{t} \ln^{2}{x}*\dfrac{1}{x} \; dx \;=\; \lim_{t \to 0^{+}} \left[\dfrac{\ln^{3}{x}}{3}\right]^{1}_{t} \;=\; \lim_{t \to 0^{+}} \left[0 - \dfrac{\ln^{3}{t}}{3}\right] \;=\; +\infty$

##### Integrale improprio divergente

###### Risoluzione

1) Anteporre all'integrale un limite con t tendente all'estremo di integrazione infinito, andando a sostituire quest'ultimo con t nell'integrale stesso.
2) Risolvere l'integrale e applicare il limite.

###### Esempio

$\displaystyle\int^{0}_{-\infty} \dfrac{e^{x}}{1 + e^{x}} \; dx \;$

$\displaystyle \lim_{t \to -\infty} \int^{0}_{t} \dfrac{e^{x}}{1 + e^{x}} \; dx \;=\; \lim_{t \to -\infty} \biggr{[} \ln{|1 + e^{x}|} \biggr{]}^{0}_{t} \;=\; \lim_{t \to -\infty} \biggr{[} \ln{(1 + e^{x})} \biggr{]}^{0}_{t} \;=\; \lim_{t \to -\infty} \biggr{(} \ln{2} - \ln{(1 + e^{t})} \biggr{)} \;=\; \ln{2} - \ln{1} \;=\; \ln{2}$

---

Vedi poi: [[17 Teorema del confronto]]

