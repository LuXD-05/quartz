# Lezione 14

### Disposizioni

##### Disposizioni semplici

Una **disposizione semplice** è una **sequenza** (perché l'<u>ordine conta</u>) di $n$ elementi su $k$ posizioni (o di $k$ elementi scelti tra $n$):

- Con $k \leq n$ (non posso disporre, per esempio, 5 elementi su 8 posti),
- <u>Senza ripetizioni</u> (non è possibile riutilizzare elementi già "disposti"). 

In pratica è una *k-upla* di elementi diversi appartenenti ad un insieme di $n$ elementi.

###### Fattoriale

Per calcolare il n° di disposizioni semplici è possibile usare il **fattoriale** (che è una funzione ricorsiva: ${} n! = n \cdot (n-1)! = \ldots {}$ ), utilizzandolo con la seguente formula:

$$d_{n,k} = \dfrac{n!}{(n-k)!}$$

###### Funzioni iniettive tra 2 insiemi

Supponiamo di avere 2 insiemi $A$ e $B$ con: $|A| = k$ (n° di posti) e $|B| = n$ (n° di elementi totali) e sempre con $k \leq n$.

In questo caso ci sono $d_{n,k} = \dfrac{n!}{(n-k)!}$ <u>funzioni iniettive</u> tra $A$ e $B$.

Nel caso in cui $k = n$ (quindi quando $|A| = |B| = n$) tutte le funzioni tra $A$ e $B$ sono **biettive**; per questo (come si vede dopo con le [[15 - Permutazioni#Permutazioni semplici|permutazioni]]) il loro numero è sempre $d_{n,n} = n!$.

###### Esempio disposizioni

$n = 5, k = 3, A = \{a,b,c,d,e\}$

Una disposizione semplice di 5 elementi su 3 posti è una tripla di elementi diversi scelti in A. Quante sono le disposizioni semplici che posso scrivere? 

Qui ci sono 5 * 4 * 3 disposizioni semplici di 5 su 3.

Infatti ${} d_{5,3} = 5 \cdot 4 \cdot 3 = \dfrac{5!}{(5-3)!} = \dfrac{5!}{2!} = \dfrac{5 \cdot 4 \cdot 3 \; \cdot \not{2} \; \cdot \not{1}}{\not{2} \; \cdot \not{1}} {}$

##### Disposizioni con ripetizioni

Le **disposizioni con ripetizioni** sono sempre disposizioni di $n$ elementi su $k$ posti, solo che in queste è possibile <u>ripetere/riutilizzare elementi già "disposti"</u>.

Il numero di disposizioni con ripetizioni è dato da: 

$$d'_{n,k} = n^{k}$$

(Ciò corrisponde al prodotto cartesiano $A \,\times\, ... \,\times\, A$, *k* volte).

Si può vedere come ciò differisca dalle disposizioni semplici considerando il caso di $A = \{a,b,c\}$ (quindi $n = 3$) e $k = 2$:

![](https://i.imgur.com/uSQdFcD.png)

#### Casi d'uso

Per entrambe le disposizioni semplici e con ripetizioni, i casi d'uso più comuni comprendono principalmente il contare i possibili modi in cui è possibile disporre $k$ elementi presi da un'insieme di $n$ elementi.

L'unica cosa è che per le disposizioni con ripetizioni, $k$ può anche essere > di $n$.

# Esercizi

# Soluzioni

---

Prossima lezione: [[15 - Permutazioni]]

