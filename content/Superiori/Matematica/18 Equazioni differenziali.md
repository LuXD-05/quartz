---
public: true
edited_seconds: 870
modified_at: 13/05/2024 00:05:51
---
### Definizione
Hint: def, esempio (+ soluzione generale e particolare), ordine (def + esempio)
::
> [!important] Equazione differenziale
> Un'equazione la cui **soluzione** è una $f(x)$ e in cui sono presenti **1 o + derivate di quest'ultima**.
###### Esempio
Partiamo dall'equazione:
$$y' = 2x$$
Questo è il caso più classico, per trovarne la soluzione (ovvero le $f(x)$ che rispettano l'equazione), bisogna integrare entrambe le parti:
$$\int y' \; dx \;=\, \int 2x \; dx$$
Ottenendo così la **soluzione generale**, ovvero la $f(x)$ variabile per il parametro $c$:
$$y = x^{2} + c$$
Si ottiene la **soluzione particolare** invece quando si assegna un certo valore a $c$:
$$P(0, 0) \;\rightarrow\; c = 0 \;\rightarrow\;y = x^{2}$$
##### Ordine
> [!important] Ordine
> Il massimo ordine di derivazione che compare nell'equazione differenziale
<!--SR:!2024-05-29,8,240-->

Per esempio, un'equazione differenziale di **1° ordine** è un'equazione differenziale che contiene al massimo la **derivata 1a** della funzione incognita da trovare (soluzione).
<!--SR:!2024-05-14,2,200-->

### Tipi di equazioni differenziali
#### 1° ordine
##### Elementari

##### A variabili separabili
###### Steps
0) Distinguerla da quelle lineari (quelle a variabili separabili hanno $y' \;=\; \ldots y \;\;* / :\;\; \ldots x$)
1) Isolare $y'$ (portando tutto il resto a destra dell'uguale) e trovare $a(x)$ e $b(y)$
2) Trovare l'eventuale soluzione per $b(y) \;=\; 0$ (impossibile a meno che non ci sia una variabile o sia tipo $1 \;=\; 1$?)
3) Sostituire a: $\dfrac{dy}{dx} \;=\; a(x) * b(y)$ le variabili $a(x)$ e $b(y)$ 
4) Portare tutte le $y$ (e coefficienti) a destra dell'uguale e tutte le $x$ (e coefficienti) a destra
5) Integrare entrambe le parti e risolvere

###### Esercizio
$y * y' \;=\; x^{3} \;\;\rightarrow\;\; y' \;=\; \dfrac{1}{y} * x^{3} \;\;\rightarrow\;\; \{...$

$b(y) \;=\; 0 \;\;\rightarrow\;\; \dfrac{1}{y} \;=\; 0 \;\;\rightarrow\;\; \dfrac{1}{y} \;=\; \dfrac{0}{y} \;\;\rightarrow\;\; 1 \;=\; 0 \;\;\rightarrow\;\; impossibile$

$\dfrac{dy}{dx} \;=\; a(x) * b(y) \;\;\rightarrow\;\; \dfrac{dy}{dx} \;=\; \dfrac{1}{y} * x^{3} \;\;\rightarrow\;\; ydy \;=\; x^{3}dx \;\;\rightarrow\;\; \int y \; dy \;=\; \int x^{3} \; dx \;\;\rightarrow\;\; \dfrac{y}{2} \;=\; \dfrac{x^{4}}{4} + c \;\;\rightarrow$
$\rightarrow\;\; y^{2} \;=\; \dfrac{x^{4}}{2} + 2c \;\;\rightarrow\;\; y \;=\; \pm\sqrt{\dfrac{x^{4}}{2} + 2c} \;\;\rightarrow\;\; [c_{1} \;=\; 2c] \;\;\rightarrow\;\; \pm\sqrt{\dfrac{x^{4}}{2} + c_{1}}$

##### Lineari
###### Steps
0) Distinguerla da quella a variabili separabili (quelle lineari hanno $y' \;=\; \ldots y \;\pm\; \ldots x$)
1) Isolare $y'$ (portando tutto il resto a destra dell'uguale) e trovare $a(x)$ e $b(x)$
2) Calcolare $A(x)$ con: $\displaystyle\int a(x) \; dx$ (senza mantenere il $+ c$)
3) Calcolare $y$ con: $\displaystyle e^{A(x)} * \int e^{-A(x)} * b(x) \; dx$ (mantenendo il $+ c$ dell'integrale)
4) Alla fine, sostituire $c$ e il suo coefficiente con $c_{1}$

CAPIRE COME FARE SISTEMA SU LINEA SINGOLA 
$$\left\{\begin{aligned} 
y &= x^{2} \\
y &= -x^{2} + 2
\end{aligned}\right.$$

###### Esercizio
$y' + 2xy \;=\; -x \;\;\rightarrow\;\; y' \;=\; -2xy - x \;\;\rightarrow\;\; y' \;=\; a(x)y + b(x) \;\;\rightarrow\;\; \{...$

$A(x) \;=\; \int a(x) \; dx \;=\; \int -2x \; dx \;=\; -2\int x \; dx \;=\; -2\dfrac{x^{2}}{2} \;=\; -x^{2}$

$y = e^{A(x)} * \int e^{-A(x)} * b(x) \; dx \;=\; -e^{-x^{2}} * \int e^{x^{2}} * x \; dx \;=\; -e^{-x^{2}} * \dfrac{1}{2}\int e^{x^{2}} * 2x \; dx \;=\; -\dfrac{1}{2}e^{-x^{2}} * (e^{x^{2}} + c) \;=$
$=\; -\dfrac{1}{2}e^{-x^{2}+x^{2}} -\dfrac{1}{2}ce^{-x^{2}} \;=\; -\dfrac{1}{2} -\dfrac{1}{2}ce^{-x^{2}} \;=\; [c_{1} \;=\; -\dfrac{1}{2}c] \;=\; -\dfrac{1}{2} + c_{1}e^{-x^{2}}$
#### ...

---
Vedi: [[19 Calcolo combinatorio]]