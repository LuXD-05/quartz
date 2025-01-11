# Lezione 37

### Applicazione lineare

Un'**applicazione lineare** è una [[12 - Funzioni#Funzioni|funzione]] tra 2 spazi vettoriali $V$ e $W$:

$$f : V \rightarrow W$$

Che rispetta 2 proprietà:

1) **Additività**: $f(v_{1} + v_{2}) = f(v_{1}) + f(v_{2})$
2) **Omogeneità**: $f(r \cdot v) = r \cdot f(v)$

> [!important] Proprietà
> Se $f : V \rightarrow W$ è un'applicazione lineare, allora:
> $$f(0_{v}) = 0_{W}$$
> Se questa proprietà <u>non è verificata</u> si può già determinare che $f$ <u>non è un'applicazione lineare</u>.

###### Determinare se $f$ è un'applicazione lineare

Per determinare se $f$ è un'applicazione lineare bisogna verificarne le proprietà; prendiamo per esempio $f : \mathbb{R}^{2} \rightarrow \mathbb{R}^{3}$ definita come "$f(x,y) = (x,y,x+y)$".

Sia per additività che per omogeneità bisogna riscrivere le 2 parti dell'uguale in termini della funzione in esame, nel nostro caso $f(x,y)$, così da ottenere da entrambe le parti un risultato "in funzione" della stessa, quindi qui "$(x,y,x+y)$" (vedi [[#1)|qui]]).

##### Kernel

Data un'applicazione lineare $f : V \rightarrow W$, il ***kernel*** di $f$ ($Ker\;f$) è l'insieme:

$$Ker(f) = \{v \in V \;|\; f(v) = 0_{W}\} \subseteq V$$

Il ***kernel*** è quindi un sottospazio di $V$ e <u>l'insieme di tutti i vettori</u> di $V$ che in $W$ <u>corrispondono al vettore nullo</u>.

##### Immagine

Data un'applicazione lineare $f : V \rightarrow W$, l'***immagine*** di $f$ ($Im\;f$) è l'insieme:

$$Im(f) = \{f(v) \;|\; v \in V\} \subseteq W$$

L'***immagine*** è quindi un sottospazio di $W$ e <u>l'insieme di tutti i vettori</u> di $W$ che sono <u>raggiunti da un vettore</u> in $V$ (tutti i vettori $w$ scrivibili come $f(v)$).

##### Riguardo a $Ker$ e $Im$

###### Caratteristiche delle applicazioni lineari

L'applicazione $f : V \rightarrow W$, in base a $Ker$ e $Im$:

- Se $Ker$ contiene solo il <u>vettore nullo</u> (o se $\color{yellow} dim(\,Ker(f)\,) = 0$), $f$ è ***iniettiva***,
- Se $Im$ <u>corrisponde</u> a $W$ (o se $\color{yellow} dim(\,Im(f)\,) = dim(W)$), $f$ è ***suriettiva***,
- Se <u>entrambe</u> le precedenti (${} \color{yellow} dim(V) = Ker(f) + Im(f) = dim(W) + 0 {}$), $f$ è ***biettiva*** (in questo caso si dice ***isomorfismo*** di spazi vettoriali).

###### Teorema di rango-nucleo

> [!important] Teorema della dimensione o di rango-nucleo
> Per una qualsiasi applicazione lineare $f : V \rightarrow W$, si ha:
> $$dim(V) = dim(\,Ker(f)\,) + dim(\,Im(f)\,)$$

###### Determinare il kernel

Per determinare il *kernel*, bisogna (esempio con $f(x,y) = (x,y,x+y)$):

1) Porre $f(x,y) = 0$,
2) Applicare $f$ su $(x,y)$ ottenendo $(x,y,x+y) = 0$,
3) Disporre le incognite in un sistema omogeneo: $\left\{\begin{aligned} & x = 0 \\ & y = 0 \\ & x + y = 0 \end{aligned}\right.$
4) Risolvere il sistema e ottenere i parametri che comporranno i vettori del kernel:

   - In caso $dim(Ker(f)) = 0$: $Ker(f) = \{(0,0)\}$ ($n$ zeri in base a ${} dim(V) {}$),

   - In caso $dim(Ker(f)) > 0$: $Ker(f) = \{(-x,x,-x)\}$ (varia in base a un parametro),

5) Contare i parametri diversi: quella sarà la <u>dimensione del kernel</u> (0 se non ci sono parametri),
6) In caso di parametri, per trovare una <u>base del kernel</u>, porre ogni incognita ad uno scalare qualsiasi.

###### Determinare l'immagine

Per dimensioni e base di un'*immagine*, bisogna (esempio $f(x,y) = (x,y,x+y)$):

1) Per la **dimensione** dell'immagine basta contare le **componenti uniche** (<u>non dipendenti dalle stesse variabili</u>) <u>non costanti</u> del vettore generico $w \in W$ ottenuto <u>applicando</u> $f(v)$.
2) Per la **base**, scegliere $n = dim(V)$ vettori ed applicarvi $f$ (di solito si scelgono quelli della base canonica di $\mathbb{R}^{n}$ siccome semplificano il tutto),
3) Dei vettori risultanti ottenuti mantenere solo un minimo insieme con quelli <u>linearmente indipendenti</u> (calcolabile con il [[31 - Risolvere sistemi con Gauss|MEG]]): quella sarà una **base** dell'immagine,

##### Sottospazi nelle applicazioni

Data un'applicazione lineare $f : V \rightarrow W$, se $S$ è un sottospazio di $V$, allora:

- $f(S)$ è un sottospazio di $W$,
- $dim(f(S)) \leq dim(S)$.

#### Matrici associate alle applicazioni

Ogni applicazione lineare ${} f : V^{n} \rightarrow W^{m} {}$ è associata ad una matrice $A_{m,n}$ tale che:

$$f(v_{1}, \ldots, v_{n}) = [a_{1}, \ldots, a_{n}]^{T} \rightarrow A = \begin{bmatrix} a_{1} \\ \vdots \\ a_{m} \end{bmatrix} = \begin{bmatrix} (r_{1}, \ldots, r_{n})_{1} \\ \vdots \\ (r_{1}, \ldots, r_{n})_{m} \end{bmatrix}$$

Quindi applicare $f$ a dei vettori da dei vettori di coefficienti i quali, se posti come righe di una matrice la quale poi è trasposta, generano $A$, una matrice di coefficienti $m \times n$.

> [!important] Proprietà
> La dimensione dell'immagine di $f$ è = al *rank* di $A$:
> $$dim(Im(f)) = rank(A)$$

##### In generale (rivedere da bmatrix a fine formula)

Ogni matrice associata a $f$ permette di trasformare le coordinare di un vettore di $V$ in quelle del corrispondente in $W$ semplicemente con un [[22 - Operazioni tra matrici#Prodotto|prodotto]]:

$$f(v_{1}, \ldots, v_{n}) = \begin{pmatrix} a_{1} \\ \vdots \\ a_{m} \end{pmatrix} \cdot \begin{pmatrix} x_{1} \\ \vdots \\ x_{n} \end{pmatrix} = \begin{bmatrix} w_{1} \\ \vdots \\ w_{m} \end{bmatrix} = (w_{1}, \ldots, w_{m})$$

Dove:

- ($a_{1}, \ldots, a_{m}$) sono i vettori risultanti dall'applicazione di $f$ (su ogni vettore di una base di $V$) trasposti (quindi colonne della matrice associata),
- (${} x_{1}, \ldots, x_{n} {}$) sono invece le incognite presenti nella "formula" di $f$.

###### Base di $V$ e di $W$

Data un'applicazione lineare $f : V \rightarrow W$ considerare:

- $Bv = \{v_{1}, \ldots, v_{n}\}$, una **base** di $V$ (con dimensione = $n$),
- $Bw = \{w_{1}, \ldots, w_{m}\}$ una **base** di $W$ (con dimensione = $m$),
- $A$ = la **matrice associata** ad $f$.

Sappiamo che facendo ${} f(v) {}$

###### Costruire la matrice associata

Per costruire la matrice associata (di $f : V \rightarrow W$) bisogna:

1) Considerare una <u>base</u> di $V$ (una <u>canonica</u> per semplicità) basta che abbia scalari al posto di incognite,
2) <u>Applicare</u> ad ogni vettore della base la <u>funzione</u> $f$,
3) Riscrivere i vettori $w$ risultanti come <u>righe</u> di una <u>matrice</u> e poi <u>trasporla</u> (o riscriverli direttamente in <u>colonne</u>), questa è la **matrice associata**,
4) Questa, moltiplicata alle variabili di dimensione nello spazio $V$, darà le variabili di dimensione di $W$; inoltre il suo *rank* sarà = a $dim(Im(f))$.

# Esercizi

###### 1) Determinare se $f$ è un'applicazione lineare

La seguente: $f : (x,y) \in \mathbb{R}^{2} \rightarrow (x,y,x+y) \in \mathbb{R}^{3}$ è un'applicazione lineare?

###### 2) Determinare il kernel + base

###### 3) Dimensione immagini

Determina la dimensione delle immagini delle seguenti applicazioni lineari:

- $f(x,y) = (0,0)$,
- $f(x,y,z) = (x+y, y+z)$,
- $f(x,y,z) = (x,x,x)$,
- $f(x,y,z) = (x-y,y-x)$,
- $f(x,y,z) = (x,2,-x)$.

###### 4) Determinare l'immagine + base

###### 5) Determinare iniettività, suriettività o biettività

###### 6) Determinare iniettività, suriettività o biettività

###### 7) Determinare iniettività, suriettività o biettività

###### 8) Considerazioni su sottospazi

(lezione 32 pag 2)

Dati $S = \{(2x,3x) \;|\; x \in \mathbb{R}\} \subseteq \mathbb{R}^{2}$ e $f(x,y) = (y-x,x)$ (sempre in $\mathbb{R}^{2}$), determina se $S$ è un sottospazio di $\mathbb{R}^{2}$ ($V$), la sua dimensione, se $f$ è un'applicazione lineare e se $f(S)$ è ancora un sottospazio di $\mathbb{R}^{2}$ ($W$).

###### 9) Costruire la matrice associata

Data l'applicazione $f : (x,y) \in \mathbb{R}^{2} = (x+y, y, 2x) \in \mathbb{R}^{3}$, costruire la matrice associata ad $f$.

###### 10) Esercizio completo

![](https://i.imgur.com/78lfywA.png)

###### 11) Esercizio completo

![](https://i.imgur.com/O4wk4HI.png)

# Soluzioni

###### 1) 

Abbiamo $f(x,y) = (x,y,x+y)$. 

Verifichiamone l'**additività** con 2 vettori generici $(x_{1}, y_{1})$ e $(x_{2}, y_{2})$ di lunghezza 2 (perché lo spazio di partenza è a 2 dimensioni):

$$f(\,(x_{1}, y_{1}) + (x_{2}, y_{2})\,) = f(x_{1}, y_{1}) + f(x_{2}, y_{2})$$

Riscriviamoli quindi "in termini del codominio" (in una forma congrua, quindi in questo caso passiamo da 2 a 3 dimensioni) <u>"applicando" la funzione</u>:

$$\begin{aligned}
f(x_{1} + x_{2}, y_{1} + y_{2}) &= f(x_{1}, y_{1}) + f(x_{1}, y_{1}) \\
&\;\,\downarrow \\
(x_{1}+x_{2}, y_{1}+y_{2}, x_{1}+x_{2}+y_{1}+y_{2}) &= (x_{1}, y_{1}, x_{1}+y_{1}) + (x_{2}, y_{2}, x_{2}+y_{2}) \\
&\;\,\downarrow \\
\color{lime} (x_{1}+x_{2}, y_{1}+y_{2}, x_{1}+x_{2}+y_{1}+y_{2}) &= \color{lime} (x_{1}+x_{2}, y_{1}+y_{2}, x_{1}+x_{2}+y_{1}+y_{2})
\end{aligned}$$

L'uguaglianza è vera, quindi è <u>verificata l'additività</u>.

Passiamo ora all'**omogeneità** con un vettore generico $(x,y)$ ed uno scalare $r$:

$$f(\,r \cdot (x, y)\,) = r \cdot f(x, y)$$

E facciamo la stessa applicazione della funzione che abbiamo appena fatto:

$$\begin{aligned}
f(\,(rx, ry)\,) &= r \cdot f(x, y) \\
&\;\,\downarrow \\
(rx, ry, rx+ry) &= r(x,y,x+y) \\
&\;\,\downarrow \\
\color{lime} (rx, ry, rx+ry) &= \color{lime} (rx, ry, rx+ry)
\end{aligned}$$

L'uguaglianza è vera, quindi è <u>verificata anche l'omogeneità</u>.

###### 2)

###### 3)

- $f(x,y) = (0,0) \rightarrow dim(Im) = 0$ (costanti non contano come dimensioni),
- $f(x,y,z) = (x+y, y+z, z+x) \rightarrow dim(Im) = 3$ (ogni componente del vettore generico ${} w$ è dipendente da variabili diverse),
- $f(x,y,z) = (x,x,x) \rightarrow dim(Im) = 1$ (3 componenti uguali, 1 unica),
- $f(x,y,z) = (x-y,y-x) \rightarrow dim(Im) = 1$ (2 componenti dipendenti dalle stesse variabili, non importano segni e disposizione),
- $f(x,y,z) = (x,2,-x) \rightarrow dim(Im) = 1$ (2: costanti non contano, $x$ e $-x$: dipendono dalla stessa variabile).

###### 4)

---

Prossima lezione: [[38 - Autovalori]]

