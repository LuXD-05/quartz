# Lezione 10

### Antisimmetria

Definiamo la <u>relazione di divisibilità</u> (un numero è divisibile per o multiplo di un altro) $R = \{(x,y) \in \mathbb{N}^{2} \;|\; y = kx, k \in \mathbb{N}^{+}\}$

- Riflessiva? Si, $\forall x \,\rightarrow\; xRx (e \; x = x-1)$
- Transitiva? Si, siccome $\forall x,y,z \;\rightarrow\; xRy \land yRz \;\rightarrow\; xRz$
- Simmetrica? No. 

Allora, di base sarebbe $\forall x,y$ se $xRy$ allora $yRx$ (se x multiplo di y, allora y multiplo di x). Però se:

$$\left\{\begin{aligned} 

x &= k_{1}y \\

y &= k_{2}x

\end{aligned}\right.

\;\;\rightarrow\;\;

\left\{\begin{aligned} 

x &= k_{1} * k_{2} * x \\

y &= k_{1} * k_{2} * y

\end{aligned}\right.$$

Solo con $k_{1}$ e $k_{2}$ entrambi = a 1 vale $x = y$; e questa proprietà è detta **antisimmetria**.

> [!important] Antisimmetria
> Una relazione $R$ binaria su $A$ è **antisimmetrica** se:
> $$xRy \land yRx \implies x = y$$
> In pratica, in una relazione antisimmetrica le relazioni (frecce) tra <u>elementi diversi</u> sono **unidirezionali** (ma esistono per esempio tra $a$ e $a$).

###### Esempio antisimmetria

La relazione "maggiore-uguale" $R = \{(x,y) \in A \;|\; x \geq y\}$ è **antisimmetrica** perché le relazioni tra 2 elementi $x,y$ sono unidirezionali eccetto per il caso in cui $x = y$.

###### Relazione asimmetrica

> [!error] Attenzione
> Da non confondere con questa è la relazione **asimmetrica**, che è tale se:
> $$xRy \land yRx \centernot{\implies} x = y$$
> Ovvero, in una relazione asimmetrica <u>tutte</u> le relazioni (frecce) sono **unidirezionali** (non esistono nemmeno, per esempio, tra $a$ e $a$).
> Riprendendo l'[[#Esempio antisimmetria|esempio]], tale relazione non è asimmetrica in quanto, per esserlo, le anche la relazione tra ${} x,y$ nel caso in cui $x = y$ dovrebbe essere unidirezionale.

### Relazione d'ordine

> [!important] Relazione d'ordine
> Una relazione $R$ binaria su $A$ si dice **relazione d'ordine** se è:
> - **Riflessiva**
> - **Antisimmetrica**
> - **Transitiva**
> Se $R$ è una relazione d'ordine e $xRy$, si dice che "*x è minore di y*" rispetto a $R$.

##### Esempi

###### Esempio relazioni d'ordine 1

La relazione "minore-uguale" su $\mathbb{Z}$: $\{(x,y) \in \mathbb{Z}^{2} \;|\; x \leq y\}$

- Riflessiva? Si, ogni numero è $\leq$ a se stesso,
- Antisimmetrica? Si, solo se $n = m \Leftrightarrow n \leq m \land m \leq n$,
- Transitiva? Si, se $x \leq y \land y \leq z \implies x \leq z$.

Infatti questa è una relazione d'ordine.

###### Esempio relazioni d'ordine 2

Relazione di inclusione ${} R = \{(X,Y) \;|\; X \subseteq Y\} {}$

Riflessiva? Si, $\forall X \in P(A) \;\rightarrow\; X \subseteq X$ (ogni insieme è contenuto in se stesso),

Antisimmetrica? Si, perché solo se $X = Y \Leftrightarrow X \subseteq Y \land Y \subseteq X$,

Transitiva? Si, se $X \subseteq Y \land Y \subseteq Z \implies X \in Z$.

Anche questa è una relazione d'ordine.

###### Esempio relazioni d'ordine 3

Relazione di divisibilità (definita [[#Antisimmetria|qui]]), è possibile visualizzarla così:

![](https://i.imgur.com/66IedjI.png)

Il diagramma di Venn da l'idea dell'**ordine**, ovvero dell'andare delle relazioni in una sola direzione. 

Tutto ciò che è in verde è stato disegnato come esempio per la seguente lezione ([[11 - Diagrammi di Hasse, massimi e minimi]]) e per semplificare i diagrammi di Venn per le relazioni d'ordine.

# Esercizi

# Soluzioni

---

Prossima lezione: [[11 - Diagrammi di Hasse, massimi e minimi]]

