# Lezione 36

##### Generatori

Si definisce ***generatore*** un vettore di uno spazio $V$ che, usato insieme ad altri generatori dello stesso, permette di "costruire" tutti i vettori di $V$ attraverso **combinazioni lineari**.

Per esempio in $\mathbb{R}^{2}$, $(1,0)$ e $(0,1)$ sono generatori perché, attraverso combinazioni lineari, permettono di ottenere ogni altro vettore di $\mathbb{R}^{2}$.

###### Sistemi di generatori

Un sistema di generatori $S$ di uno spazio vettoriale $V$ è un <u>qualsiasi</u> insieme di vettori $\{v_{1}, v_{2}, \ldots v_{n}\}$ generatori di $V$, i quali permettono quindi di ottenere ogni vettore di $V$ tramite combinazioni lineari.

Si scrive $V = <S>$, infatti:

$$S = \{(0,1), (1,0)\} \subseteq \mathbb{R}^{2} \;\;\rightarrow\;\; <S> \, = \{a \cdot (0,1) + b \cdot (1,0) \;|\; a,b \in \mathbb{R}^{2}\}$$

> [!important] Nota
> Al contrario delle [[#Base|basi]], per i sistemi di generatori:
> - <u>Non è necessario che i loro vettori siano linearmente indipendenti</u> tra di loro,
> - Sono comunque <u>ammesse "ridondanze"</u>, ovvero <u>vettori che sono combinazioni lineari di altri</u> (tipo per $\mathbb{R}^{2}$, in $\{(1,0), (0,1), (1,1)\},\,$ $(1,1)$ è ridondante in quanto bastano gli altri 2 per generare tutti i vettori di $\mathbb{R}^{2}$).

### Base

Una ***base*** $B$ di uno spazio vettoriale è un **[[#Sistemi di generatori|sistema di generatori]] *minimo***, ovvero un insieme di vettori generatori che soddisfa 2 condizioni:

- **Indipendenza lineare**: non sono ammesse "ridondanze", nel senso che nessun vettore della base può essere una combinazione lineare di altri,
- **Completezza**: ogni vettore dello spazio deve poter essere scritto come combinazione lineare dei vettori della base (ogni vettore di $V$ è una combinazione lineare ***unica*** dei vettori di $B$).

> [!error] Attenzione
> Le [[#Base|basi]], come quindi anche i [[#Sistemi di generatori|sistemi di generatori]], non possono ammettere il **vettore nullo**.

##### Dimensione

Uno spazio vettoriale $V$ può avere <u>infinite basi</u>; ma queste hanno tutte la **stessa cardinalità**, ovvero lo stesso <u>numero di vettori</u> al loro interno. 

Si dice quindi "***dimensione***" di uno spazio $V$ ($dim(V)$) il <u>numero di vettori</u> di una base $B$ di $V$ (oppure il massimo numero di vettori linearmente indipendenti di $V$).

###### Considerazioni sulla dimensione (TODO)

Rispetto a quanto abbiamo visto finora ci sono delle considerazioni da fare:

- Il rank di una matrice corrisponde alla dimensione ...
- si possono trovare le ... linearmente indipendenti rendendo la matrice a scala con Gauss (differenza tra x righe e per colonne CHATSSS)
- Se $det(A) \neq 0$ (con $A \in M_{n}$), $rank(A) = n = dim(V)$; (Nota: in $\mathbb{R}^{n}$, un insieme di $n$ vettori linearmente indipendenti è sempre una sua base).

##### Base canonica

Una base di uno spazio $V$ di dimensione $n$ si dice ***canonica*** quando:

- È composta esattamente da $n$ vettori,
- Ogni vettore (rispettivamente) ha una diversa componente a 1 e le altre a 0.

Per esempio, in $\mathbb{R}^{n}$, la base canonica $B = \{v_{1}, v_{2}, \ldots v_{n}\}$ è formata da:

$$\left.\begin{aligned} & v_{1} = [1,0, \ldots 0] \\ & v_{2} = [0,1, \ldots 0] \\ & \ldots \\ & v_{n} = [0,0, \ldots 1] \end{aligned}\right.$$

(Nota che non è necessario che il componente a 1 di ogni vettore $v_{i}$ sia esattamente alla posizione $i$, basta che ogni posizione diversa tra tutti abbia un 1).

# Esercizi

###### 1) Capire se $B$ è base di $V$

$B = \{ (0,1), (1,1) \}$ è una base di $\mathbb{R}^{2}$?

###### 2) Capire se $B$ è base di $V$

###### 3) Trovare la combinazione lineare di $B$ per un vettore di $V$

Data la base $B = \{ (2,-1), (3,1) \}$ di $\mathbb{R}^{2}$, per quali scalari la combinazione lineare tra i vettori della base restituisce $(5,3)$?

# Soluzioni

###### 1) 

Per capire se un sistema di generatori è una base di $V$ ($\mathbb{R}^{2}$), scriviamolo sottoforma di matrice e troviamone il rango:

$$B \in M_{2} = \begin{bmatrix} 0 & 1 \\ 1 & 1 \end{bmatrix} \;\;\rightarrow\;\; det(B) \neq 0 \;\;\rightarrow\;\; rank(B) = 2$$

Ciò significa che le 2 righe di $B$ sono linearmente indipendenti; quindi che $B$ è una base di $V$.

###### 2)

###### 3)

Avendo $B = \{ (2,-1), (3,1) \}$, per capire quale combinazione lineare dei suoi vettori corrisponde a $(5,3)$, bisogna trovare gli scalari che moltiplicano tali vettori e che diano $(5,3)$; perciò iniziamo col sostituirli con delle incognite:

$$(5,3) = a(2,-1) + b(3,1) = (2a+3b,b-a)$$

Rendiamo il tutto un sistema e proviamo a trovare il valore delle incognite:

$$\left\{\begin{aligned} & 2a+3b = 5 \\ & b-a = 3 \end{aligned}\right. \;\;\rightarrow\;\; \left\{\begin{aligned} & 5a + 9 = 5 \\ & b = 3+a \end{aligned}\right. \;\;\rightarrow\;\; \left\{\begin{aligned} & a = -\frac{4}{5} \\ & b = 3-\tfrac{4}{5} = \frac{11}{5} \end{aligned}\right.$$

Per una verifica più completa, sostituire ad $a$ e $b$ della formula precedente i valori trovati.

---

Prossima lezione: [[]]

