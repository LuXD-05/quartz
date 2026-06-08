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

- **Indipendenza lineare**: non sono ammesse "*ridondanze*", nel senso che <u>nessun vettore della base può essere una combinazione lineare di altri nella stessa</u>,
- **Completezza**: ogni vettore dello spazio deve poter essere scritto come <u>combinazione lineare dei vettori della base</u> (ogni vettore di $V$ è una combinazione lineare ***unica*** dei vettori di $B$).

> [!error] Attenzione
> Le [[#Base|basi]], come quindi anche i [[#Sistemi di generatori|sistemi di generatori]], non possono ammettere il **vettore nullo** (il quale è una combinazione lineare di qualsiasi vettore moltiplicato per lo scalare $0$).

##### Dimensione

Uno spazio vettoriale $V$ può avere <u>infinite basi</u>; ma queste hanno tutte la **stessa cardinalità**, ovvero lo stesso <u>numero di vettori</u> al loro interno. 

Si dice quindi "***dimensione***" di uno spazio $V$ ($dim(V)$) il <u>numero di vettori</u> di una base $B$ di $V$ (oppure il massimo numero di vettori linearmente indipendenti di $V$).

###### Considerazioni

Rispetto a quanto abbiamo visto finora ci sono delle considerazioni da fare:

- $n$ vettori di $\mathbb{R}^{n}$, se **linearmente indipendenti**, sono sempre una base di $\mathbb{R}^{n}$,
- Se il ***rank*** di una matrice le cui <u>righe</u> sono gli $n$ vettori è $n$, allora tali vettori sono **linearmente indipendenti** (quindi sono una base dello spazio di <u>dimensione</u> $n$).
- 

##### Base canonica

Una base di uno spazio $V$ di dimensione $n$ si dice ***canonica*** quando:

- È composta esattamente da $n$ vettori,
- Ogni vettore (rispettivamente) ha una diversa componente a 1 e le altre a 0.

Per esempio, in $\mathbb{R}^{n}$, la base canonica $B = \{v_{1}, v_{2}, \ldots v_{n}\}$ è formata da:

$$\left.\begin{aligned} & v_{1} = [1,0, \ldots 0] \\ & v_{2} = [0,1, \ldots 0] \\ & \ldots \\ & v_{n} = [0,0, \ldots 1] \end{aligned}\right.$$

(Nota che non è necessario che il componente a 1 di ogni vettore $v_{i}$ sia esattamente alla posizione $i$, basta che ogni posizione diversa tra tutti abbia un 1).

#### Per gli esercizi

###### Capire se un sistema è una base

Per capire se un sistema di generatori è una base, bisogna:

1) Scriverlo come matrice (1 vettore per riga),
2) Trovare il rank della suddetta, ovvero il suo n° di righe linearmente indipendenti,
3) Se il rank = n° di vettori del sistema, esso è una base dello spazio di riferimento.

###### Trovare gli scalari che in combinazione lineare con una base danno un certo vettore

Per trovare quali scalari che, posti in combinazione lineare con i vettori di un sistema, danno un certo vettore appartenente allo spazio di riferimento, bisogna:

1) Scrivere il sistema come combinazione lineare dei suoi vettori con **incognite** <u>al posto degli scalari</u> (da trovare),
2) <u>Risolvere</u> i prodotti scalari e risolvere le somme e sottrazioni tra i polinomi,
3) Adesso, verificare se il vettore effettivamente generato dal sistema in esame ponendolo = ad esso; se il sistema è risolvibile allora si otterranno i valori degli scalari che generano quel vettore.

# Esercizi

###### 1) Capire se $B$ è base di $V$

$B = \{ (0,1), (1,1) \}$ è una base di $\mathbb{R}^{2}$?

###### 2) Capire se un sistema è base di $V$

Dato il sistema:

$$\{ x + y + z = 0$$

Trovare la dimensione, lo spazio delle soluzioni e una base di $\mathbb{R}^{3}$.

###### 3) Trovare la combinazione lineare di $B$ per un vettore di $V$

Data la base $B = \{ (2,-1), (3,1) \}$ di $\mathbb{R}^{2}$, per quali scalari la 

combinazione lineare tra i vettori della base restituisce $(5,3)$?

# Soluzioni

###### 1) 

Per capire se un sistema di generatori è una base di $V$ ($\mathbb{R}^{2}$), scriviamolo sottoforma di matrice e troviamone il rango:

$$B \in M_{2} = \begin{bmatrix} 0 & 1 \\ 1 & 1 \end{bmatrix} \;\;\rightarrow\;\; det(B) \neq 0 \;\;\rightarrow\;\; rank(B) = 2$$

Ciò significa che le 2 righe di $B$ sono linearmente indipendenti; quindi che $B$ è una base di $V$.

###### 2)

Riscriviamo in forma matriciale:

$$A = \begin{bmatrix} 1 & 1 & 1 \end{bmatrix}$$

Poi: ${} rank(A) = 1 {}$, quindi per il teorema di Rouché-Capelli, il sistema ha $\infty^{3-1} = \infty^{2}$ soluzioni; quindi la dimensione della base è 2.

Prendendo poi $y$ e ${} z$ come parametri si ha:

$$x = -y-z$$

E lo spazio delle soluzioni è:

$$V = \{(-y-z,y,z) \;|\; y,z \in \mathbb{R}\} \subseteq \mathbb{R}^{3}$$

Ci resta solo da trovare una base per lo spazio trovato, per cui basta sostituire ai parametri nella formula dello spazio degli scalari (diversi per avere $n = 2$ vettori diversi nella base):

- Con $y = 1$ e $z = 0$ si ha $(-1,1,0)$,
- Con $y = 0$ e $z = 1$ si ha $(-1,0,1)$.

Quindi la base trovata sarà:

$$B = \{(-1,1,0),(-1,0,1)\}$$

###### 3)

Avendo $B = \{ (2,-1), (3,1) \}$, per capire quale combinazione lineare dei suoi vettori corrisponde a $(5,3)$, bisogna trovare gli scalari che moltiplicano tali vettori e che diano $(5,3)$; perciò iniziamo col sostituirli con delle incognite:

$$(5,3) = a(2,-1) + b(3,1) = (2a+3b,b-a)$$

Rendiamo il tutto un sistema e proviamo a trovare il valore delle incognite:

$$\left\{\begin{aligned} & 2a+3b = 5 \\ & b-a = 3 \end{aligned}\right. \;\;\rightarrow\;\; \left\{\begin{aligned} & 5a + 9 = 5 \\ & b = 3+a \end{aligned}\right. \;\;\rightarrow\;\; \left\{\begin{aligned} & a = -\frac{4}{5} \\ & b = 3-\tfrac{4}{5} = \frac{11}{5} \end{aligned}\right.$$

Per una verifica più completa, sostituire ad $a$ e $b$ della formula precedente i valori trovati.

---

Prossima lezione: [[37 - Applicazioni lineari]]

