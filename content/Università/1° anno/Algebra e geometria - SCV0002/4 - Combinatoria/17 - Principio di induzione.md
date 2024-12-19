# Lezione 17

### Principio di induzione

Il principio di induzione è una tecnica di dimostrazione di tesi matematiche che consente di dimostrarne la validità dalla verifica di 2 condizioni; tuttavia, vale solo per gli enunciati formulati in funzione di $\mathbb{N}$.

> [!important] Condizioni
> Poniamo come assioma che in $\mathbb{N}$ tutti i numeri naturali > 0 sono successori di altri. Per dimostrare che una proprietà ${} P(n) {}$ è vera su tutti i numeri di $\mathbb{N}$ è necessario verificare la validità di queste condizioni:
> - **Base / *passo zero***: dimostrare che $P(n)$ è vera quando $n = 0$ (o il valore iniziale del *range* preso in considerazione),
> - **Passo / *passo induttivo***: dimostrare che $P(n) \implies P(n+1)$ (se $P(n)$ è vera, $P$ deve essere vera anche per tutti i successori $n+1$).

##### Dimostrazione

In generale, data una proprietà $P$:

1) Si dimostra la **base** di induzione <u>sostituendo il valore iniziale del range</u> considerato alla $n$ <u>della formula</u> di $P$ e verificando che il risultato di $P$ sia coerente (con $P$ stessa o la sua formula),
2) Per il **passo** di induzione invece: 

   1) Sostituire $(n+1)$ ad $n$ nella formula di $P$ (così da avere $P(n+1)$),
   2) Riscrivere $P(n+1)$ in termini di $P(n)$, tipo: "$P(n+1) = P(n) + (n+1)$" (in caso l'operatore sia "+"),
   3) Sostituire a $P(n)$ il valore della sua formula originale; se, aggregandoci $(n+1)$, la formula ottenuta coincide con quella del (sub)step 1 $P(n+1)$, allora il **passo** è verificato (quindi come anche $P$ stessa per ipotesi di induzione).
Vedi l'esempio concreto in questo [[#1) Dimostrare sommatoria per induzione|esercizio sommatoria]] e nella relativa [[#1)|soluzione]].

### Sommatoria

Invece di scrivere $1 + \ldots + n$, si scrive $\displaystyle\sum\limits^{n}_{k=1} k$. Si può vedere (analogia con programmazione) come un ciclo *for*:

```java
int result = 0;
for(int k = 1; k <= n; k++) {
	result += k;
}
return result;
```

In generale quindi, con $k$ detta "***variabile muta***":

$$\sum\limits^{n}_{k=1} a_{k} = a_{1} + a_{2} + \ldots + a_{n}$$

### Produttoria

Simile alla [[#Sommatoria|sommatoria]] però <u>moltiplica</u> invece di sommare (nel ciclo *for* sarebbe `*=` invece di `+=`):

$$\displaystyle\prod^{n}_{k=1} a_{k} = a_{1} \cdot a_{2} \cdot \ldots \cdot a_{n}$$

# Esercizi

##### 1) Dimostrare sommatoria per induzione

Si vuole dimostrare per induzione che la somma dei primi numeri naturali $\geq 1$ fino ad $n$ corrisponda alla seguente proprietà: $P(n) = \dfrac{n(n+1)}{2}$.

![](https://i.imgur.com/al4QD80.png)

##### 2) Dimostrare produttoria per induzione

Si vuole dimostrare per induzione la seguente proprietà per i numeri naturali $\geq 2$ fino ad $n$: $\displaystyle\prod^{n}_{k=1} \left(1 - \dfrac{1}{k}\right) = \dfrac{1}{n}$

##### 3) Dimostrare che $(7^{n}-1)\,\%\,6=0 {}$ per induzione

Si vuole dimostrare per induzione che $\forall n \in \mathbb{N} \geq 1$ corrisponda alla seguente proprietà: $P(n) = 7^{n} - 1 \;\%\; 6 = 0$ (ovvero che $7^{n} - 1$ sia sempre multiplo di 6).

# Soluzioni

##### 1)

Dimostriamo che $\forall n \in \mathbb{N} \geq 1$, $P(n)$ è valida; ovvero che vale quanto segue:

$$(1 + 2 + \ldots + n) = (\sum\limits^{n}_{i=1} i) = \dfrac{n(n+1)}{2}$$

###### Base di induzione

Il valore iniziale del *range* da considerare è 1, quindi:

$$P(1) = \dfrac{1 \cdot (1+1)}{2} = \dfrac{2}{2} = 1$$

La base è **valida**, ovvero la somma dei primi naturali da 1 a *n* (quindi da 1 a 1 = 1 e basta), coincide con $P(1)$.

###### Passo di induzione

\1) Ottenere $P(n+1)$:

$$P(n+1) = \dfrac{(n+1)((n+1)+1)}{2} = \dfrac{(n+1)(n+2)}{2} = \dfrac{n^{2} + 3n + 2}{2}$$

\2) Scrivere $P(n+1)$ in funzione di $P(n)$:

$$P(n+1) = P(n) + (n+1)$$

\3) Sostituire $P(n)$ con la sua formula:

$$P(n+1) = \dfrac{n(n+1)}{2} + (n+1) = \dfrac{n(n+1)+2(n+1)}{2} = \dfrac{n^{2}+3n+2}{2}$$

Il passo è **valido** in quanto il <u>risultato</u> di $P(n+1)$ <u>del (sub)step 3 corrisponde al valore</u> di $P(n+1)$ <u>del (sub)step 1</u>.

Ciò rende **verificata** $P$ per ogni $n \in \mathbb{N} \geq 1$ per **induzione**.

##### 2) 

Dimostriamo che $\forall n \in \mathbb{N} \geq 2$, $P(n)$ è valida; ovvero che vale quanto segue:

$$\displaystyle\prod^{n}_{k=2} \left(1 - \dfrac{1}{k}\right) = \dfrac{1}{n}$$

###### Base di induzione

Il valore iniziale del *range* da considerare è 2, quindi:

$$P(2) = \displaystyle\prod^{2}_{k=2} \left(1 - \dfrac{1}{k}\right) = 1 - \dfrac{1}{2} = \dfrac{1}{2}$$

La base è **valida** in quanto il risultato di $P(2)$ coincide con quello di $P(n)$ con $n=2$.

###### Passo di induzione

\1) Ottenere $P(n+1)$:

$$P(n+1) = \displaystyle\prod^{n+1}_{k=2} \left(1 - \dfrac{1}{k}\right) = \dfrac{1}{n+1}$$

\2) Scrivere $P(n+1)$ in funzione di $P(n)$:

$$P(n+1) = P(n) \cdot \left(1 - \dfrac{1}{n+1}\right)$$

\3) Sostituire $P(n)$ con la sua formula:

$$P(n+1) = \displaystyle\prod^{n}_{k=2} \left(1 - \dfrac{1}{k}\right) \cdot \left(1 - \dfrac{1}{n+1}\right) = \dfrac{1}{n} \cdot \left(1 - \dfrac{1}{n+1}\right) = \dfrac{1}{n} - \dfrac{1}{n(n+1)} = \dfrac{n+1-1}{n(n+1)} = \dfrac{1}{n+1}$$

Il passo è **valido** in quanto il risultato di $P(n+1)$ del (sub)step 3 corrisponde al valore di $P(n+1)$ del (sub)step 1.

Ciò rende **verificata** $P$ per ogni $n \in \mathbb{N} \geq 2$ per **induzione**.

##### 3) 

...

###### Base di induzione

...

###### Passo di induzione

...

---

Prossima lezione: [[18 - Strutture algebriche]]

