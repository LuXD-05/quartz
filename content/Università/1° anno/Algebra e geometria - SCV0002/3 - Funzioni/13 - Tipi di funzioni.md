# Lezione 13

### Tipi di funzione

##### Funzione identità

Dato $A$ un insieme qualsiasi, si definisce la relazione $id_{A} = \{(x,x) \;|\; x \in A\}$ come la **funzione identità** di $A$ (o *funzione identica*, corrispondente alla relazione diagonale).

$\;id_{A} : A \rightarrow A \;\;\;\;\; \forall x \in A \;\rightarrow\; id_{A}(x) = x$

![](https://i.imgur.com/LKWgz6N.png)

##### Funzione costante

Una funzione costante è una funzione i cui <u>gli elementi del dominio hanno tutti una stessa immagine</u> (in termini grafici, è una funzione orizzontale, quindi con la $y$ sempre uguale).

![](https://i.imgur.com/y5AA3Wm.png)

##### Funzione iniettiva

$f$ si dice **iniettiva** se $x \neq y \;\rightarrow\; f(x) \neq f(y)$

Se parto da 2 elementi diversi del dominio, le 2 frecce non possono indicare lo stesso elemento.

Tutti gli elementi del codominio hanno controimmagine o singleton o $\emptyset$.

![](https://i.imgur.com/f1YHKvX.png)

![](https://i.imgur.com/mq4SJq8.png)

##### Funzione suriettiva

$f$ si dice suriettiva se:

- $\forall y \in B$ esiste $x \in A \;|\; (x) = y$,
- $\forall y \in B \;\rightarrow\; f^{-1}(x) \neq \emptyset$,
- Ogni elemento del codominio è raggiunto da una freccia.

![](https://i.imgur.com/2sg1FT2.png)

##### Funzione biettiva

$f$ si dice ***biettiva*** se è <u>sia iniettiva sia suriettiva</u>.

**Attenzione**: tra 2 insiemi **finiti** <u>non esistono funzioni biettive</u> se $|A| \neq |B|$

> [!info] Permutazioni
> Considerando un insieme $A$ e una relazione binaria $A \times A$, si dicono **permutazioni** tutte le funzioni biettive tra $A$ e $A$.
> In generale, se $n = |A|$:
> - Ci sono $n^{n}$ <u>funzioni</u> di $A$ in $A$,
> - Ci sono ${} n!$ <u>permutazioni</u> di $A$ in $A$.

###### Insiemi equipotenti

2 insiemi $A$ e $B$ (anche infiniti) si dicono **equipotenti** se <u>esiste una funzione biettiva tra di essi</u>. Se sono finiti però, sono equipotenti se e solo se $|A| = |B|$ (perché altrimenti non esisterebbero funzioni biettive tra essi). 

Esempio:   $f : n \in \mathbb{N} \;\rightarrow\; 2n \in 2\mathbb{N}$.   Dominio = $\mathbb{N}$, Codominio = $2\mathbb{N}$

- Iniettiva? Si, dato che se $n \neq m$ allora $2n \neq 2m$ ($f(n) \neq f(m)$, ovvero il doppio di un numero non è mai uguale al doppio di un altro numero diverso).
- Suriettiva? Si, dato che $\forall y \in 2\mathbb{N}$, $y$ è pari, quindi $y = 2x$ (ovvero ogni numero in $2\mathbb{N}$ è il doppio di un altro, quindi tutti hanno la loro metà in $\mathbb{N}$).

Per questo $f$ è <u>biettiva</u> e $\mathbb{N}$ e $2\mathbb{N}$ sono <u>equipotenti</u>.

> [!important] Insieme infinito
> Un insieme è **infinito** se è <u>equipotente ad un suo sottoinsieme "proprio"</u> (cioè un sottoinsieme diverso dall'insieme o da $\emptyset$).
> Esempio: $\mathbb{N}$ e $\mathbb{Q}$ (non con $\mathbb{R}$, è troppo grande come infinito).

###### Funzioni tra 2 insiemi finiti

- Ci sono $|B|^{|A|}$ possibili funzioni tra $A$ e $B$.
- Se $|A| > |B|$, <u>non esistono funzioni iniettive</u> tra $A$ e $B$,
- Se $|A| < |B|$, <u>non esistono funzioni suriettive</u> tra $A$ e $B$,
- Se $|A| = |B|$, <u>ogni funzione</u> tra $A$ e $B$ <u>è biettiva</u>.

##### Funzioni composte

Partiamo con 3 insiemi:

$$A = \{1,2,3\},\;B = \{a,b\},\;C = \{e,g,f\}$$

Legati dalle seguenti relazioni:

![](https://i.imgur.com/QNnIa3x.jpeg)

Se si hanno 2 funzioni ($f$ e $g$) tali che il **codominio** di $f$ è uguale al **dominio** di $g$:

$f : A \;\rightarrow\; B \;\;\;e\;\;\; g : B \;\rightarrow\; C$.

Allora si definisce "$g \circ f$" come una **funzione composta**, tale che:

- $g \circ f : A \;\rightarrow\; C$,
- $\forall x \in A \;\rightarrow\; [g \circ f](x) = f(g(x))$.

###### Esempi funzioni composte

\1) Esempio parole

$f : x \in A^{+} \;\rightarrow\; \#x \in \mathbb{N}$

$g : n \in \mathbb{N} \;\rightarrow\; 2n \in 2\mathbb{N}$

Componendo queste 2 funzioni si ottiene:

${} g \circ f : x \in A^{+} \;\rightarrow\; 2 \cdot \#x \in 2\mathbb{N} {}$

\2) Esempio coppie somma

$f : (n,m) \in \mathbb{N}^{2} \;\rightarrow\; n+m \in \mathbb{N}$

$g : n \in \mathbb{N} \;\rightarrow\; n^{2} \in \mathbb{N}$

Componendo queste 2 funzioni si ottiene:

$g \circ f : (n,m) \in \mathbb{N}^{2} \;\rightarrow\; (n+m)^{2} \in \mathbb{N}$

##### Funzione inversa

Se $f : A \;\rightarrow\; B$ è una [[#Funzione biettiva|funzione biettiva]], allora $\,\forall y \in B \rightarrow f^{-1}(y) =$ elemento di un singleton.

Per questo è possibile definire la funzione $f^{-1} : B \;\rightarrow\; A \;\;|\;\; f^{-1}(y) =$ elemento del singleton. 

Quindi $f^{-1}$ è detta **funzione inversa** di $f$ (Attenzione! <u>non è possibile definire una funzione inversa</u> $f^{-1}$ <u>se</u> $f$ <u>non è biettiva</u> perché altrimenti $f^{-1}$ potrebbe avere nel dominio elementi con <u>nessuna</u> o <u>più di 1 relazione</u> con elementi del codominio).

> [!info] Nota
> Facendo la [[#Funzioni composte|funzione composta]] tra una $f$ e  la sua inversa si ha:
> - $f^{-1} \circ f = id_{A} = A \;\rightarrow\; A$
>   ![](https://i.imgur.com/w5UBGl5.png),
> - $f \circ f^{-1} = id_{B} = B \;\rightarrow\; B$
>   ![](https://i.imgur.com/nYdkwmc.png).

###### Esempio funzioni inverse

Funzione $id_{\mathbb{Z}}$, date:

- $f : n \in \mathbb{Z} \;\rightarrow\; 2n \in 2\mathbb{Z}$
- $g : n \in \mathbb{Z} \;\rightarrow\; n+1 \in \mathbb{Z}$

Si ha che sono entrambe biettive dato che:

- $f$ è iniettiva siccome se e solo se $n \neq m \implies 2n \neq 2m$,
- $f$ è suriettiva dato che $\forall m \in 2\mathbb{Z} \rightarrow \frac{m}{2} = n$ (con $n \in \mathbb{Z}$),
- $g$ è iniettiva siccome se e solo se ${} n \neq m \implies n+1 \neq g+1 {}$,
- $g$ è suriettiva dato che $\forall m \in \mathbb{Z} \rightarrow m-1 = n {}$ (con $n \in \mathbb{Z}$).

Esempio in forma esplicita: $(f \circ g)(n) = f(g(n)) = 2(n+1)$

Determinare le funzioni in forma esplicita (ove possibile) di: $g \circ f^{-1}$, $g^{-1} \circ f$, $g^{-1} \circ f^-1$, $f^{-1} \circ g^{-1}$.

###### Inversione per funzioni non iniettive

Definiamo basandoci su $f : A \;\rightarrow\; B$ la relazione $R_{f} = \{(x,y) \in A^{2} \;|\; f(x) = f(y)\}$. $R_{f}$ è una relazione di equivalenza così rappresentata:

![](https://i.imgur.com/brWdqPg.png)

Si vede ad occhio che ${} R_{f}$ è **solo suriettiva e non iniettiva**, perciò una teorica <u>inversione</u> di $f$ <u>non risulterebbe in una funzione</u> (infrange la regola: ogni elemento del dominio deve essere in relazione con 1 solo elemento del codominio).

La quesitone cambia se si vanno a considerare le classi di equivalenza nell'esempio:

![](https://i.imgur.com/jtCuKac.png)

Dato che ogni classe di equivalenza (se immaginata come se fosse un elemento) si collega effettivamente ad 1 singolo elemento del codominio, rendendo la funzione biettiva e quindi invertibile.

> [!info] In generale
> Se $f : A \;\rightarrow\; B$, ipotizzando una relazione di equivalenza $R_{f} = \{(x,y) \in A^{2} \;|\; f(x) = f(y)\}$, si ha che la funzione ${} \overset{\sim}{f} : A {}$/$R_{f} \;\rightarrow\; B$ è iniettiva.
> (In pratica si fa l'insieme quoziente di una relazione di equivalenza avente le sole classi di equivalenza il che, per la funzione ${} \overset{\sim}{f} : A {}$/$R_{f} \;\rightarrow\; B$, associa agli elementi di $B$ le classi di equivalenza stesse; ciò è fatto per garantire anche l'iniettività per le funzioni solo suriettive).
> Se $f$ è già iniettiva, $R_{f}$ è la relazione diagonale: $R_{f} = \{(x,x) \;|\; x \in A\}$.
> Se $f$ però non è suriettiva, bisogna prima di tutto considerare $\underset{\sim}{f}$, ovvero la differenza tra il codominio e i suoi elementi non relazionati con nessuno del dominio (in pratica si restringe il codominio alle sole immagini degli elementi del dominio).
> Infine si può quindi dire che $\underset{\sim}{\overset{\sim}{f}}$ è **biettiva**.

# Esercizi

###### 1) $P(A)$

$A = \{a,b,c\}$, $P(A)$

$f : X \in P(A) \;\rightarrow\; X \cup \{a\} \in P(A)$

Iniettiva? Suriettiva?

###### 2) $A^{+}$

###### 3) Determinare se iniettiva/suriettiva/biettiva

Dati $A = \{1,2\}$ e $B = \{a,b\}$ dire se la funzione $f : A \times B \rightarrow A \cup B$ tale che:

![](https://i.imgur.com/OIIpw2P.png)

è iniettiva/suriettiva/biettiva.

# Soluzioni

###### 1)

###### 2)

###### 3)

$(1,a) = 1, \; (1,b) = b, \; (2,a) = 2, \; (2,b) = a$

$f$ è iniettiva perché ogni elemento del dominio è relazionato con 1 e 1 solo del codominio.

${} f$ è suriettiva perché nessun elemento del codominio è privo di controimmagine.

Perciò $f$ è biettiva.

---

Prossima lezione: [[14 - Disposizioni]]

