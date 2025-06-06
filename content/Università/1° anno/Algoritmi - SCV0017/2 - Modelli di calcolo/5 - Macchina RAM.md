# Lezione 5

### Random Access Machine

Operazioni e complessità degli algoritmi dipendono dalla struttura/modello sulla quale tali vengono eseguiti. Un modello di riferimento <u>teorico</u> è il modello **RAM** (*Random Access Machine*).

![](https://i.imgur.com/cwnSS7L.png)

##### Caratteristiche

La RAM ha:

- Un **programma** <u>fisso</u> composto da <u>istruzioni</u> elementari (fatte da `opcode` e `address`, tipo `READ 1`) con: I/O, operazioni logico-aritmetiche, lettura/scrittura su registri e salti (condizionati e non):

  ![](https://i.imgur.com/CubPIJA.png),

- Un **PC** (*Program Counter*) che contiene l'indirizzo (o *label*) dell'istruzione corrente,
- **Registri** infiniti ad accesso casuale ($R_{1}, R_{2} \; ...$) capaci di contenere un intero qualsiasi e ognuno identificato da un indirizzo intero $k$ (Nota: per <u>operazioni aritmetiche si usa solo</u> $R_{0}$),
- Un <u>nastro di input</u> infinito dal quale si leggono interi,
- Un <u>nastro di output</u> infinito sul quale si scrivono interi.

> [!info] Indirizzamento
> Vi sono 3 modi di usare la parte `address` (che è un intero) delle istruzioni:
> - =`n` indica il numero naturale $n$ come **valore** o costante,
> - `n` indica un indirizzo di un registro ed è usato quando se ne deve prendere il contenuto come **valore** (***indirizzamento diretto***),
> - `*n` è sempre un indirizzo ma il contenuto del registro corrispondente è la ***label*** (***indirizzamento indiretto***) di un <u>altro registro</u> da cui prendere il <u>contenuto come valore</u>.

###### Stato

Lo **stato** della RAM è una funzione che associa ad ogni registro (PC compreso) il suo contenuto e ai puntatori ai nastri di I/O la loro posizione, tipo:

- $S(r)$ = posizione puntatore sul nastro di input,
- $S(w)$ = posizione puntatore sul nastro di output,
- $S(PC)$ = *label* in PC,
- $S(k)$ = contenuto di $R_{k}$ (per ogni $k$).

> [!example] Stato iniziale
> Lo stato iniziale $S_{0}$ prevede:
> - $S_{0}(r) = S_{0}(w) = S_{0}(PC) = 1$,
> - $S_{0}(k) = 0$ (per ogni $k$).

###### Esecuzione di programmi

Si illustra in pseudocodice il ciclo di esecuzione delle istruzioni di un programma:

```java
setInitialState();
while(Prog[PC] != 'HALT') {
	fetch(PC);       // Individua l'istruzione da eseguire per mezzo di PC
	decode(istr);    // Decodifica il comando con l'opcode
	execute(istr);   // Esegue l'istruzione e aggiorna lo stato della macchina
}
```

Inoltre, dopo ogni istruzione (eccetto i salti), **PC** è <u>incrementato di 1</u>.

###### Computazione

Una ***computazione*** è una sequenza di stati ($S_{0}, S_{1} \; ... \; S_{i}$) nella quale:

- $S_{0}$ è lo <u>stato iniziale</u>,
- $S_{i+1}$ (stato successivo) si ottiene eseguendo l'istruzione di indice $PC$ nello stato $S_{i}$.

La computazione può essere infinita (*loop*), ma se <u>termina</u> è perché è stata eseguita l'istruzione `HALT` o una non eseguibile.

###### Semantica

La semantica del linguaggio RAM è definita dalla seguente funzione parziale:

$$f_{p} : \bigcup_{n=0}^{\infty} \mathbb{Z}^n \longrightarrow \bigcup_{n=0}^{\infty} \mathbb{Z}^n \cup \{\perp\}$$

E:

- $\displaystyle\bigcup_{n=0}^{\infty} \mathbb{Z}^{n}$ è uno spazio che contiene **vettori** (*array*) di <u>qualsiasi lunghezza</u> i cui <u>elementi</u> sono <u>numeri interi qualsiasi</u>,
- $\{\perp\}$ è un insieme che contiene tutti gli <u>output non idonei o non conclusivi</u> (tipo quando il programma va in *loop*).

Quindi quando la computazione si ferma, $f_{p}(x)$ è un vettore di interi in output, altrimenti è = $\perp$.

###### Esempi

1\) ![](https://i.imgur.com/tsJnsrs.png)

2\) ![](https://i.imgur.com/mFgIy56.png)

3\) ![](https://i.imgur.com/KWh4iDh.png)

### Complessità computazionale

La **complessità computazionale** di un algoritmo è la <u>quantità di risorse</u> che esso usa durante la computazione (inversamente proporzionale all'***efficienza*** dello stesso, che è maggiore quanto più piccola la complessità computazionale); e le risorse sono definite come <u>costi</u> in termini di ***tempo*** e ***spazio***.

Per calcolare la complessità computazionale di un algoritmo esistono 2 <u>criteri di costo</u>: **[[#CCU|uniforme]]** e **[[#CCL|logaritmico]]**.

##### CCU

Il ***CCU*** (*Criterio di Costo Uniforme*) assume che il costo dell'algoritmo sia:

- **Tempo** ($T_{p}$) = <u>n° totale di istruzioni</u> (ogni istruzione "costa" 1 unità in termini di tempo),
- **Spazio** ($S_{p}$) = <u>n° totale di registri utilizzati</u> (ogni registro <u>distinto</u> usato "costa" 1 unità in termini di spazio).

> [!important] Convenzione
> - Se la computazione **non termina** (*loop*) $\;\rightarrow\; t = \infty$,
> - Se si usa un **n° illimitato di registri** $\;\rightarrow\; s = \infty$.

###### Limiti CCU

In certi casi il CCU è <u>poco significativo</u> dato che non tiene conto della **dimensioni degli input** e degli **interi in essi**; perciò tale metodo è realistico e impiegabile solo per quegli algoritmi in cui la <u>dimensione degli input è trascurabile e/o non aumenta troppo</u> (ordinamento con confronti, ricerca...).

##### CCL

Il ***CCL*** (*Criterio di Costo Logaritmico*) è più preciso e realistico del precedente siccome qui il **costo** di un'istruzione dipende dal **n° di bit** (<u>dimensione</u>) **dell'operando** ($n$) e si calcola così:

$$l(n) = \log_{2}(|n|)+1$$

Dove $l$ è la funzione che indica il costo dell'operando $n$.

> [!important] Formule
> Il costo logaritmico in termini di **tempo** ($T_{p}^{l}(x)$) è la somma dei costi ($l$) delle istruzioni del programma in base all'input ($x$).
> Il costo logaritmico in termini di **spazio** ($S_{p}^{l}(x)$) è il massimo valore che raggiunge lo spazio utilizzato durante la computazione.

###### Esempi CCL

1\) Calcolo del massimo tra $n$ valori (interi compresi tra 1 e $k$):

```java
int[] input = [1, 5, 2, 9];       //// (in linguaggio RAM l'input non è salvato in registri)
int cont = 0;                     //// (in linguaggio RAM cont non è salvato in registri)
int max = 0;                      // Per max si usa 1 registro
while (cont < input.length()) {   // Ciclo fatto n volte --> T = n (tempo totale sarà già * n)
	if (input[cont] > max)            // JGTZ --> costa l(max) = log(max) in tempo
		max = input[cont];            // STORE --> costa log(max) + log(input[cont]) in tempo
	cont++;                           //// (in linguaggio RAM cont non è salvato in registri)
}
return max;                       // (supponendo max = k) --> l(max) = log(k)
```

Quindi avremo che:

- $T_{p}^{l}(x)$ = ${} \color{yellow}{n} {}$ (cicla $n$ volte, 1 per ogni elemento in input) $\color{yellow}{\cdot \; 12\log(max)}$ (nel caso peggiore in cui in ogni ciclo fa sia `JGTZ` e `STORE`, con input crescente),
- ${} S_{p}^{l}(x)$ = $\color{yellow}{\log(max) = \log(k)}$ (dato che usa 1 registro `max` il che contiene il numero massimo della sequenza prima stabilito come $k$).

In [[4 - Notazioni asintotiche#Big-O notation $O$|big-O notation]], riducendo al minimo e senza costanti si ha che:

- ${} T_{p}^{l}(x) = n \log(k) {}$,
- $S_{p}^{l}(x) = \log(k)$.

# Esercizi

CCU ogni operazione costa O(1)

Per il CCL, si guardano gli stati

---

Prossima lezione: [[6 - Macchina RASP]]

