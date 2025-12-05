# Lezione 4

### Big-O notation $O$

La ***Big-O notation*** descrive il <u>n° di operazioni compiute da un algoritmo</u> basandosi sulla dimensione dell'input, permettendo di determinarne la complessità indipendentemente dal tempo di esecuzione (influenzato da altri fattori). Si denota quindi una gerarchia:

![](https://i.imgur.com/xhfQyRS.png)

##### Definizione

Una funzione $f(n)$ è la *big-O* di un'altra $g(n)$ (entrambe nell'ordine dei reali) se: 

$$f(n) \leq c \cdot g(n) \;\rightarrow\; f(n) = O(g(n))$$

![](https://i.imgur.com/ZBI67VL.png)

Questo significa che la funzione $f$ è nell'ordine di $g$, ovvero la sua crescita (dopo un certo punto $n_{0}$) non supererà mai quella di $g$ ($\cdot \; c$).

> [!example] Esempio
> Supponiamo di avere la seguente funzione: $f(n) = 3n^{2} + 5n + 4$.
> Si nota che il termine più "dominante" è ${} 3n^{2}$, perciò la complessità con la *big-O notation* sarà così determinata da esso: ${} O(g(n)) = O(n^{2}) {}$. 
> ![](https://i.imgur.com/jGBD3H3.png)
> Con ciò stabiliamo che esiste una costante $c$ che, moltiplicata a ${} g(n) {}$, renderà la crescita della stessa <u>sempre</u> maggiore di quella di $f(n)$ (eventualmente dopo un certo punto $n_{0}$ nel grafico); e in questo caso la costante potrebbe essere $4$:
> ![](https://i.imgur.com/WzWAfUc.png)

###### O(1)

Il n° di operazioni è **costante** ed è indipendente dalla dimensione dell'input, come quando si accede direttamente ad un'elemento di un'array tramite indice:

![](https://i.imgur.com/krWTPmd.png)

###### O(log n)

Qui il n° di operazioni aumenta **logaritmicamente** (ogni volta è < di prima), come per la binary search:

![](https://i.imgur.com/rI7eu9i.png)

###### O(n)

Qui le operazioni aumentano linearmente rispetto alla dimensione dell'input (ricerca in un array di 6 elementi = 6 operazioni nel caso peggiore):

![](https://i.imgur.com/MCqYtvp.png)

###### O(n log n)

Algoritmi di questa complessità combinano caratteristiche di quelli lineari e logaritmici (crescita *linearitmica*), come algoritmi di *sorting* efficienti (*merge sort*, *quick sort* o *heap sort*):

![](https://i.imgur.com/hvNhXWD.png)

###### O($n^{2}$)

Di algoritmi con crescita **quadratica**, da semplici cicli innestati ad algoritmi di *sorting* semplici (*bubble sort*, *selection sort* e *insertion sort*):

![](https://i.imgur.com/PuBSqTq.png)

Simili sono quelli con crescita **cubica**:

![](https://i.imgur.com/C6vklUh.png)

###### O($2^{n}$)

Questi algoritmi <u>raddoppiano in complessità</u> per ogni unità aggiunta alla dimensione dell'input:

![](https://i.imgur.com/VphNpcG.png)

###### O(n!)

Algoritmi con crescita **fattoriale**, per esempio le <u>permutazioni</u>.

### Omega notation $\Omega$

La notazione $\Omega$ grande è il contrario della [[#Big-O notation $O$|Big-O notation]] in quanto stabilisce un <u>limite</u> **inferiore** <u>di complessità degli algoritmi</u> invece che uno superiore.

##### Definizione

Una funzione $f(n)$ è la *big-*$\Omega$ di un'altra $g(n)$ se: 

$$f(n) \geq c \cdot g(n) \;\rightarrow\; f(n) = \Omega(g(n))$$

![](https://i.imgur.com/1Owo8vX.png)

Questo significa che la funzione $g$ è nell'ordine di $f$, ovvero la sua crescita (dopo un certo punto $n_{0}$) non supererà mai quella di ${} f$ ($\cdot \; c$).

### Theta notation $\Theta$

La notazione $\Theta$ grande invece è un misto delle 2 precedenti, siccome stabilisce <u>2 limiti</u> di complessità per gli algoritmi, uno superiore e uno inferiore.

##### Definizione

Una funzione $f(n)$ è la *big-*${} \Theta {}$ di un'altra $g(n)$ se:

$$c_{1} \cdot g(n) \leq f(n) \leq c_{2} \cdot g(n) \;\rightarrow\; f(n) = \Theta(g(n))$$

![](https://i.imgur.com/tZ3uwXt.png)

Questo significa che le funzioni $f$ e $g$ hanno lo <u>stesso ordine di grandezza</u>, e la crescita di $f$ (dopo un certo punto $n_{0}$) sarà sempre <u>compresa</u> tra quella di $c_{1} \cdot g(n)$ e $c_{2} \cdot g(n)$.

> [!important] Proprietà
> $f(n) = \Theta(g(n))$ solo se $f(n) = O(g(n)) = \Omega(g(n))$

### Altre notazioni

##### ~

##### Little-o

---

Prossima lezione: [[5 - Macchina RAM]]

