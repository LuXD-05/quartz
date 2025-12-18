# Lezione 38

##### Endorfismi

Si dice ***endorfismo*** un'applicazione lineare il cui dominio è uguale al codominio:

$$f : V \rightarrow V$$

### Autovalori e autovettori

Dato un endorfismo $f : V \rightarrow V$, un ***autovettore*** di $f$ è un vettore ${} v \in V {}$ tale che:

$$f(v) = \lambda \cdot v$$

Dove ${} \lambda {}$ è uno scalare che si dice ***autovalore***. (Si dice che $v$ <u>è un autovettore relativo all'autovalore</u> $\lambda$).

> [!info] Determinare autovettori
> Per determinare se un vettore $v$ è un autovettore di una certa $f$ "ad occhio":
> 1) Porre $f(x,y) = \lambda \cdot (x,y)$,
> 2) Trovare per quali $\lambda$ vale l'uguaglianza.
> Esempio $f(x,y) = \lambda \cdot (x,y) \;\rightarrow\; (y,x) = (\lambda x, \lambda y)$:
> - ${} f(1,1) = \lambda (1,1) \;\rightarrow\; (1,1) = 1 \cdot (1,1) \;\;\; {}$ ($(1,1)$ è un autovettore),
> - ${} f(2,3) = \lambda (2,3) \;\rightarrow\; (3,2) \neq \lambda (2,3) \;\;\;\;\; {}$ ($(2,3)$ <u>non</u> è un autovettore),

##### Autospazi

Dato un autovalore $\lambda$ di $f$, si definisce ***autospazio*** (relativo a $\lambda$) l'insieme:

$$V_{\lambda} = \{v \in V \;|\; f(v) = \lambda \cdot v\}$$

quindi $V_{\lambda}$ contiene i vettori $v$ a cui applicare $f$ corrisponde a moltiplicarli per $\lambda$; ed è un sottospazio di $V$.

###### Determinare autovalori e autospazi

Per determinare un autospazio relativo ad un certo autovalore, bisogna:

1) Considerare $A$, la **[[37 - Applicazioni lineari#Matrici associate alle applicazioni|matrice associata]]** ad $f$ ($n \times n$),
2) Porre $det(A - \lambda \cdot I_{n}) = 0$ (***polinomio caratteristico***),
3) Trovare le soluzioni della suddetta equazione, tali saranno gli autovalori di $f$,
4) Per ogni autovalore $\lambda$ calcolare: $V_{\lambda} = \{v \;|\; f(v) = \lambda v\}$ ponendo, in un sistema, ogni componente di $f(v)$ = a ogni componente di $\lambda v$,
5) Dopo aver portato ogni equazione del sistema = 0, trasformare lo stesso in forma matriciale (non completa, solo con le incognite e tralasciando gli "$= 0$"),
6) Trovare (con [[30 - Teorema di Rouché-Capelli#Teorema di Rouché-Capelli|Rouché-Capelli]]) le soluzioni del sistema e concludere la risoluzione del sistema scrivendo le soluzioni così: $V_{\lambda} = \{(\ldots) \;|\; \ldots \in \mathbb{R}\}$,
7) Infine trovare (eventualmente) una base di tale autospazio prendendo i coefficienti delle incognite nella soluzione.

> [!example] Spiegazione
> Consideriamo la matrice associata di $f(x,y) = (2x+2y, y)$:
> $$A = \begin{bmatrix} 2 & 2 \\ 0 & 1 \end{bmatrix}$$
> Sappiamo che applicare $f$ significa fare $A \cdot v$ oppure $\lambda \cdot v$:
> $$f(x,y) = A \cdot \begin{pmatrix} x \\ y \end{pmatrix} = \lambda \cdot \begin{pmatrix} x \\ y \end{pmatrix} = (2x+2y, y)$$
> Infatti i 2 modi per applicare la funzione sono uguali:
> $$\begin{bmatrix} 2 & 2 \\ 0 & 1 \end{bmatrix} \cdot \begin{pmatrix} x \\ y \end{pmatrix} = \lambda \cdot \begin{pmatrix} x \\ y \end{pmatrix}$$
> Perciò:
> $$\begin{pmatrix} 2x + 2y \\ y \end{pmatrix} = \begin{pmatrix} \lambda x \\ \lambda y \end{pmatrix}$$
> Ora sottraiamo le suddette poste in un sistema omogeneo in forma matriciale:
> $$\begin{pmatrix} 2x + 2y \\ y \end{pmatrix} - \begin{pmatrix} \lambda x \\ \lambda y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} $$ $$ \;\downarrow\; $$ $$ \begin{pmatrix} 2x + 2y - \lambda x \\ y - \lambda y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} $$ $$ \;\downarrow\; $$ $$ \begin{pmatrix} (2-\lambda) x + 2y \\ (1-\lambda) y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} $$ $$ \;\downarrow\; $$ $$ \begin{pmatrix} 2 - \lambda & 2 \\ 0 & 1-\lambda \end{pmatrix}  \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$
> $\lambda$ è un autovalore solo se il suddetto sistema omogeneo ammette soluzioni non nulle, ovvero se $rank(A-\lambda I_{n}) < n$ cioè se $det(A-\lambda I_{n}) = 0$.
> Questo processo è generalizzabile sottraendo ad $A_{n}$ la matrice identità $I_{n}$ moltiplicata per $\lambda$:
> $$A' = A - \lambda I_{n} = \begin{bmatrix} 2 & 2 \\ 0 & 1 \end{bmatrix} - \begin{bmatrix} \lambda & 0 \\ 0 & \lambda \end{bmatrix} = \begin{bmatrix} 2-\lambda & 2 \\ 0 & 1-\lambda \end{bmatrix}$$
> Da qui possiamo trovare gli ***autovalori*** di $f$ ponendo $det(A') = 0$ ($det(A')$ è detto anche ***polinomio caratteristico***, indicato con $\pi_{A}(\lambda)$):
> $$\det(\begin{bmatrix} 2-\lambda & 2 \\ 0 & 1-\lambda \end{bmatrix}) = 0 \;\;\rightarrow\;\; (2-\lambda)(1-\lambda) = 0 \;\;\rightarrow\;\; \begin{aligned} \lambda &= 2 \\ \lambda &= 1 \end{aligned}$$
> A questo punto, per calcolare tutti i $V_{\lambda}$ per ognuno di essi verificare che $f(x,y) = \lambda (x,y)$:
> $$V_{2} = \{(x,y) \;|\; (2x+2y, y) = 2 \cdot (x,y)\}$$
> Traduciamo ciò in un sistema e poi in una matrice (dopo aver posto tutto a 0):
> $$\left\{\begin{aligned} & x+z = 2x \\ & -2z = 2y \\ & -2y = 2z \end{aligned}\right. \;\;\;\rightarrow\;\;\; \left\{\begin{aligned} & -x+z = 0 \\ & -2z -2y = 0 \\ & -2y -2z = 0 \end{aligned}\right. \;\;\;\rightarrow\;\;\; \begin{bmatrix} -1 & 0 & 1 \\ 0 & -2 & -2 \\ 0 & -2 & -2 \end{bmatrix} = A - 2I_{n}$$
> Calcolare poi il n° di soluzioni del sistema con [[30 - Teorema di Rouché-Capelli#Teorema di Rouché-Capelli|Rouché-Capelli]] (NOTA: dato che per trovare gli autovalori abbiamo posto il $det(A') = 0$, allora anche quello di $A'$ con qualunque autovalore sostituito a $\lambda$ sarà ancora 0):
> $$rank(A-2I_{n}) = 2 \implies \infty^{1} \; soluzioni$$
> Poi continuo a risolvere il sistema (eventualmente ignorando equazioni duplicate o già risolte):
> $$\left\{\begin{aligned} & -x = -z \\ & -2y = 2z \end{aligned}\right. \;\;\;\rightarrow\;\;\; \left\{\begin{aligned} & x = z \\ & y = -z \end{aligned}\right.$$
> Trovando infine l'insieme delle soluzioni:
> $$V_{2} = \{(z,-z,z) \;|\; z \in \mathbb{R}\}$$
> Lo si verifica eventualmente applicandovi $f$ o moltiplicandolo per l'autovalore corrente:
> $$f(z,-z,z) = (2z,-2z,2z) = 2(z,-z,z)$$
> Potrebbe magari venir chiesto di calcolare una base di $V_{\lambda}$:
> $$B_{2} = \{(1,-1,1)\}$$
> E poi si continua con il resto degli autovalori...

##### Molteplicità algebrica

La **molteplicità algebrica** ($m_{a}$) di un autovalore $\lambda$ è il (più grande) <u>numero di volte</u> ($m$) che $(\lambda - h)^{m}$ è una <u>soluzione del sistema omogeneo del polinomio caratteristico</u>.

In pratica è l'**esponente** di $(\lambda - h)^{m}$ in considerazione nel polinomio caratteristico. Si calcola appena si trova il polinomio caratteristico (si vede "ad occhio").

##### Molteplicità geometrica

La **molteplicità geometrica** ($m_{g}$) di un autovalore $\lambda$ è invece la <u>dimensione dell'autospazio relativo</u> ad esso:

$$m_{g} = dim(V_{\lambda}) = n - rank(A - \lambda I_{n})$$

Quindi è il numero di parametri per cui varia la soluzione.

##### Proprietà

1) Un'applicazione lineare $f : \mathbb{R}^{n} \rightarrow \mathbb{R}^{n}$ ha al massimo $n$ autovalori,
2) Se un'applicazione lineare $f : \mathbb{R}^{n} \rightarrow \mathbb{R}^{n}$ ha al $n$ autovalori distinti allora esiste una base di $\mathbb{R}^{n}$ formata da autovettori, ovvero:

   $$B = B_{1} \cup \ldots \cup B_{n}$$

3) Esiste una base di $\mathbb{R}^{n}$ formata da **autovettori** di $f$ solo se tutti gli **autovalori** di $f$ sono ***regolari*** (definizione di seguito),
4) Per ogni autovalore vale quanto segue:

   $$1 \leq m_{g} \leq m_{a} \leq n$$

> [!important] Autovalore regolare
> Un'autovalore si dice ***regolare*** se $m_{a} = m_{g}$. 

# Esercizi

###### 1) Determinare autovalori

Data l'applicazione lineare $f(x,y) = (y,x)$, determina a quale autovalore i seguenti autovettori sono relativi (se tali sono autovettori):

- $f(1,1) = (1,1)$,
- $f(2,3) = (3,2)$,
- $f(2,-2) = (-2,2)$.

###### 2) Determinare autospazi

Data l'applicazione lineare $f(x,y) = (y,x)$, determina gli autovettori relativi a $\lambda = 1$ (nell'autospazio $V_{1}$)?

# Soluzioni

###### 1) 

---

Prossima lezione: [[]]

