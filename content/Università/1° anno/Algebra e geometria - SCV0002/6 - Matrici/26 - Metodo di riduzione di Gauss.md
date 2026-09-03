# Lezione 26

### Eliminazione gaussiana

Il ***MEG*** (*Metodo di Eliminazione di Gauss*) è un algoritmo che consente di ridurre una qualsiasi matrice in una **[[21 - Matrici#Matrice a scala|matrice a scala]]**; inoltre tale metodo è usato per <u>risolvere sistemi lineari</u> e <u>calcolare rank di matrici</u>.

##### Procedimento

Prima di definire il procedimento definiamo quali sono le mosse possibili da fare, ovvero:

> [!important] Mosse di Gauss
> Le **mosse di Gauss** (o anche *operazioni elementari tra righe*) sono 3:
> - Scambio di 2 righe,
> - Moltiplicazione di una riga per uno scalare $\neq 0$,
> - Combinazione lineare di righe 2 righe, ovvero sommare ad una riga un'altra moltiplicata per uno specifico scalare (vedi dopo).
> C'è anche da considerare la **normalizzazione** di una riga che, anche se non è in sé una mossa di Gauss, è utile per semplificare certi calcoli e consiste nel moltiplicare o dividere la riga in esame per un certo scalare per fare in modo che il suo ***pivot*** sia 1.

###### Esempio MEG

Step 1: si parte con l'individuare una riga che ha il ***[[21 - Matrici#Matrice a scala|pivot]]*** prima di tutte le altre (indice di colonna più piccolo) e nel nostro caso è proprio la prima.

Tenere da conto che: 

- In caso il *pivot* individuato fosse $\neq 1$, sarebbe comodo normalizzarlo a 1,
- La riga scelta, se non lo è già, andrà spostata in prima posizione,
- Eventuali righe nulle dovrebbero essere messe alla fine.

$$\begin{bmatrix} 

  \color{red}{1} & 0 & 4 & 2 \\ 

  2 & 0 & 8 & 8 \\ 
  1 & 2 & 6 & 2 \\ 
  2 & 1 & 9 & 4 
\end{bmatrix}$$

Step 2: ottenuto il *pivot* $p_{ij}$, bisogna fare in modo di rendere tutti i numeri "sotto" di esso (delle righe $> i$ e nella colonna $j$) = 0.

$$\begin{bmatrix} 

  \color{red}{1} & 0 & 4 & 2 \\ 

  \color{orange}{2} & 0 & 8 & 8 \\ 

  \color{orange}{1} & 2 & 6 & 2 \\ 

  \color{orange}{2} & 1 & 9 & 4 

\end{bmatrix}$$

Questo si fa con una [[25 - Vettori linearmente indipendenti#Combinazione lineare|combinazione lineare]], ovvero sommando ad ogni riga $n > i$ la riga prima scelta ($i$) e moltiplicata per l'inverso del 1° numero della riga $n$ (quelli arancioni, cosicché la somma dei 2 vettori abbia come 1° elemento 0):

$$\begin{bmatrix} 

  \color{red}{1} & 0 & 4 & 2 \\ 

  \color{orange}{2} & 0 & 8 & 8 \\ 

  \color{orange}{1} & 2 & 6 & 2 \\ 

  \color{orange}{2} & 1 & 9 & 4 

\end{bmatrix}

\rightarrow

\begin{aligned} 

  & \\ 

  &[ \, + ({\color{orange}{-2}}) \cdot (R_{1}) \, ] \\ 

  &[ \, + ({\color{orange}{-1}}) \cdot (R_{1}) \, ] \\ 

  &[ \, + ({\color{orange}{-2}}) \cdot (R_{1}) \, ]

\end{aligned}

\rightarrow

\begin{bmatrix} 

  1 & 0 & 4 & 2 \\ 
  0 & 0 & 0 & 4 \\ 
  0 & 2 & 2 & 0 \\ 
  0 & 1 & 1 & 0 
\end{bmatrix}$$

Step 3: ripetere gli step precedenti partendo dalla riga $i + 1$ finché non si ottiene una matrice a scala.

Avendo finito con la 1a riga, ora passiamo alle altre. Si nota come le righe col *pivot* all'indice di colonna più piccolo sono la 3 e la 4 e scegliere una o l'altra è pressoché identico.

Sceglieremo la 4 perché il *pivot* è già normalizzato a 1, mentre se avessimo scelto la 3, o si faceva un passo in più dividendo l'intera riga per 2 per normalizzarla, oppure si lasciava cosi e si moltiplicava la riga per $\frac{1}{2}$ (per questo è possibile normalizzare, dato che per la combinazione lineare è necessario moltiplicare la riga scelta per uno scalare, a sto punto si normalizza a 1 per rendere il tutto più semplice).

$$\begin{bmatrix} 

  1 & 0 & 4 & 2 \\ 
  \color{lime}{0} & \color{lime}{0} & \color{lime}{0} & \color{lime}{4} \\ 

  0 & 2 & 2 & 0 \\ 
  \color{lime}{0} & \color{lime}{1} & \color{lime}{1} & \color{lime}{0} 

\end{bmatrix}

\rightarrow\;\,

\begin{aligned} 

  & \\ 

  & \downarrow \\ 

  & \\ 

  & \uparrow 

\end{aligned}

\;\;\rightarrow

\begin{bmatrix} 

  1 & 0 & 4 & 2 \\ 
  0 & \color{red}{1} & 1 & 0 \\ 
  0 & \color{orange}{2} & 2 & 0 \\ 
  0 & \color{orange}{0} & 0 & 4
\end{bmatrix}$$

Ora ripetiamo il 2° step ma solo per la 3a riga in quanto il valore "sotto" il *pivot* nella 4a è già = 0:

$$
\begin{bmatrix} 
  1 & 0 & 4 & 2 \\ 
  0 & \color{red}{1} & 1 & 0 \\ 
  0 & \color{orange}{2} & 2 & 0 \\ 
  0 & \color{orange}{0} & 0 & 4
\end{bmatrix}
\rightarrow
\begin{aligned} 
  & \\ 
  & \\ 
  &[ \, + ({\color{orange}{-2}}) \cdot (R_{1}) \, ] \\ 
  &/ 
\end{aligned}
\rightarrow
\begin{bmatrix} 
  1 & 0 & 4 & 2 \\ 
  0 & 1 & 1 & 0 \\ 
  0 & 0 & 0 & 0 \\
  0 & 0 & 0 & 4
\end{bmatrix}
$$

Infine basta scambiare le ultime 2 righe per ottenere la matrice a scala:

$$\begin{bmatrix} 

  1 & 0 & 4 & 2 \\ 
  0 & 1 & 1 & 0 \\ 
  \color{lime}{0} & \color{lime}{0} & \color{lime}{0} & \color{lime}{0} \\

  \color{lime}{0} & \color{lime}{0} & \color{lime}{0} & \color{lime}{4}

\end{bmatrix}

\rightarrow\;\,

\begin{aligned} 

  & \\ 

  & \\ 

  & \downarrow \\ 

  & \uparrow 

\end{aligned}

\;\;\rightarrow

\begin{bmatrix} 

  \color{aqua}{1} & \color{aqua}{4} & \color{aqua}{2} & \color{aqua}{2} \\ 

  0 & \color{aqua}{1} & \color{aqua}{1} & \color{aqua}{0} \\ 
  0 & 0 & 0 & \color{aqua}{4} \\ 
  0 & 0 & 0 & 0
\end{bmatrix}$$

> [!important] Ricorda
> Il **n° di righe non nulle** delle <u>matrici a scala</u> corrisponde al loro *rank*.
> Se si ottiene una matrice a scala $B$ da una matrice originale ${} A$ tramite il MEG, allora $rank(A) = rank(B)$.

##### Determinante con Gauss

Data una matrice quadrata $A \in M_{n}$, se la si riduce col MEG, si incorre in 1 dei seguenti casi:

- La matrice a scala risultante avrà almeno 1 riga a 0, per cui $det(A) = 0$,
- La matrice a scala risultante sarà una [[21 - Matrici#Matrice triangolare|matrice triangolare]].

###### Matrice triangolare

Con una matrice triangolare, le 3 operazioni elementari cambiano il valore del determinante come segue:

- **Scambio di 2 righe**: $det(A) = -det(A')$,
- **Moltiplicazione di una riga per** $k$: $det(A) = k \cdot det(A')$,
- **Combinazione lineare**: $det(A) = det(A')$.

Perciò, se ci si ricorda quali e quante mosse sono state fatte per arrivare ad $A'$, si avrà che:

$$det(A) = \pm k \cdot det(A')$$

Tuttavia, dato che $A'$ è una matrice triangolare, è semplice calcolarne il determinante siccome basta fare il prodotto degli elementi nella diagonale.

# Esercizi

# Soluzioni

---

Prossima lezione: [[27 - Inversa]]

