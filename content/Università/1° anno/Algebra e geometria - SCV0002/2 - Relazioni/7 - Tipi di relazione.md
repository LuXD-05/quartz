# Lezione 7

### Tipi di relazione

##### Relazione inversa

Se $R$ è una relazione tra $A$ e $B$, è detta **relazione inversa** $R^{-1}$ la relazione tra $B$ e $A$ così definita:

$$R^{-1} = \{(b,a) \;|\; (a,b) \in R\}$$

$R^{-1} \subseteq B \times A$, mentre $R \subseteq A \times B$

##### Relazione diagonale

Una relazione tra $A$ e $B$ è **diagonale** (o detta anche *identità*) quando ogni elemento di $A$ è in relazione <u>solo</u> con il "corrispondente" di $B$, ovvero:

$$R = \{(x,y) \in A \times B \;|\; x = y\}$$

Anche una relazione **[[#Relazione binaria|binaria]]** può essere **diagonale** (riprendendo $A = \{1,2,3\}$ di prima):

$$R = \{(1,1),(2,2),(3,3)\}$$

Diventa più semplice visualizzarla in una **matrice di adiacenza** (sempre riferita all'esempio di prima):

![](https://i.imgur.com/34JjJXl.png)

> [!info] Attenzione
> Una relazione (**[[#Relazione binaria|binaria]]**) **diagonale** è sempre anche **[[#Relazione binaria riflessiva|riflessiva]]**.

##### Relazione binaria

Una **relazione binaria** (su $A$) è un sottoinsieme di $A \times A$, così descritta:

$$R \subseteq A \times A$$

Un esempio potrebbe essere una relazione "*minore o uguale*" su $\mathbb{N}$ (considerata in $A = \{1,2,3\}$):

$R = \{(1,1),(2,2),(3,3),(1,2),(2,3)\}$:

![](https://i.imgur.com/SZ1EZfN.png)

###### Relazione binaria riflessiva

Una relazione $R$ **[[#Relazione binaria|binaria]]** su $A$ è **riflessiva** se ogni elemento di $A$ è in relazione (anche/almeno) con se stesso (quindi se contiene la **[[#Relazione diagonale (identità)|relazione diagonale]]**):

$$\forall a \in A \;\rightarrow\; aRa$$

$R$ non è riflessiva se esiste almeno 1 elemento $(a,a) \not{\in}\;\; R$.

Per quanto riguarda la rappresentazione con **diagramma di Venn**, <u>tutti gli elementi devono avere una freccia che li collega con se stessi</u>:

![](https://i.imgur.com/VEwWtsv.png)

Per quanto riguarda la rappresentazione con **matrice di adiacenza**, deve essere presente una $\times$ in <u>tutte le celle facenti parte della diagonale</u>:

![](https://i.imgur.com/Oj2pCzr.png)

> [!info] Proprietà
> Se $R$ è **riflessiva** allora $|R| \geq |A|$
> Infatti, basta che gli elementi di $A$ si colleghino tutti a se stessi per far sì che $|R| = |A|$, poi avere altre relazioni tra elementi diversi non invalida il fatto che la relazione sia riflessiva. 

###### Relazione binaria simmetrica

Una relazione $R$ **[[#Relazione binaria|binaria]]** è **simmetrica** se le relazioni vanno "in 2 direzioni", ovvero esistono (per ogni $x$ e $y$) entrambe le coppie $(x,y)$ e $(y,x)$; quindi se:

$$\forall x,y \in A \;\rightarrow\; xRy \land yRx$$

Per quanto riguarda la rappresentazione con **diagramma di Venn**, <u>per ogni elemento con una freccia che lo collega ad un altro, da quest'ultimo deve partire una freccia che lo ricollega al 1°</u>:

![](https://i.imgur.com/YFD5Yqy.png)

Per quanto riguarda la rappresentazione con **matrice di adiacenza**, le celle contenenti una $\times$ devono essere <u>simmetriche rispetto alla diagonale</u> (da in alto a sinistra a in basso a destra):

![](https://i.imgur.com/4IKgXPE.png)

(Avere elementi in relazione con se stessi non invalida il fatto che $R$ sia simmetrica).

###### Relazione binaria transitiva

Una relazione $R$ su $A$ si dice **transitiva** se ogni elemento ($x$) in relazione con un altro ($y$) lo raggiunge attraverso una relazione fatta con 1 tra tutti gli altri elementi ($z$) con cui $y$ è collegato), ovvero se:

$$\forall x,y,z \in A \;\rightarrow\; xRy \,\land\, yRz \,\land\, xRz$$

Ciò vale anche per gli <u>elementi relazionati solo con se stessi</u> in quanto:

$$aRa \land aRa \;\rightarrow\; aRa$$

(Quindi anche le [[#Relazione diagonale|relazioni diagonali]] sono **transitive**).

Per quanto riguarda la rappresentazione coi **diagrammi di Venn**, <u>se tra 2 elementi esiste un percorso fatto da 2 frecce, ce ne deve essere uno fatto da 1 freccia</u>.

![](https://i.imgur.com/BM2dYXk.png)

> [!info] Esempi
> Esempio 1:
> $R = \{ (x,y) \in \mathbb{N} \;|\; x \leq y \}$
> Riflessiva? Si perché ogni elemento è = a se stesso,
> Simmetrica? No, perché 1 < 2 ma 2 > 1,
> Transitiva? Si, perché ogni elemento è relazionato con tutti i successivi e con se stesso.
> Esempio 2:
> $R = \{ (x,y) \in \mathbb{Z} \;|\; x - y \;\%\; 4 = 0\}$
> Riflessiva? Si, $\forall x \in Z \;\rightarrow\; x-x = 0$ che è multiplo di 4.
> Simmetrica? Si, $\forall x,y \in Z$ se $x-y \;\%\; 4 = 0$ allora anche $-(y-x) \;\%\; 4 = 0$
> Transitiva? Si, $\forall x,y,z \in Z$ se $x-y \;\%\; 4 = 0$ e $y-z \;\%\; 4 = 0$, per ${} x$ e $z$, essendo entrambi multipli di 4, varrà $x-z \;\%\; 4 = 0$

##### Relazione di equivalenza

Una relazione si dice "**di equivalenza**" quando è sia **[[#Relazione binaria riflessiva|riflessiva]], [[#Relazione binaria simmetrica|simmetrica]]** e **[[#Relazione binaria transitiva|transitiva]]** (detta anche relazione **totale** (?) e l'esempio più semplice di essa è la <u>relazione di uguaglianza</u>, ovvero quella data da tutte le coppie di $A \times B$).

###### Esempi relazioni di equivalenza

\1) Relazione sottoinsieme (definita su prodotto cartesiano di 2 $P(A)$):

$A = \{a,b,c\}$ e $R \subseteq P(A) \times P(A)$

$R = \{(x,y) \in P(A) \times P(A) \;|\; x \subseteq y\}$

Riflessiva? Si perché ogni insieme contiene anche se stesso.

Simmetrica? No perché se $\{a,b,c\} \subseteq \{a\} \;\rightarrow\; \{a\} \not{\subseteq}\; \{a,b,c\}$. 

Transitiva? Si dato che se $x \subseteq y$ e $y \subseteq z$ allora $x \subseteq z$.

Di equivalenza? No.

\2) Relazione multipli di 4:

$R_{4}= \{(x,y) \in \mathbb{Z} \times \mathbb{Z} \;|\; x - y \;\%\; 4 = 0\}$

Riflessiva? Si, $\forall x \in Z \;\rightarrow\; x-x = 0$ che è multiplo di 4.

Simmetrica? Si, $\forall x,y \in Z$ se $x-y \;\%\; 4 = 0$ allora anche $-(y-x) \;\%\; 4 = 0$

Transitiva? Si, $\forall x,y,z \in Z$ se $x-y \;\%\; 4 = 0$ e $y-z \;\%\; 4 = 0$, per ${} x$ e $z$, essendo entrambi multipli di 4, varrà $x-z \;\%\; 4 = 0$

Quindi è una relazione di equivalenza.

# Esercizi

# Soluzioni

---

Prossima lezione: [[8 - Classi di equivalenza e insieme quoziente]]

