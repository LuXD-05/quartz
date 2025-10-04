# Lezione 16

### Combinazioni

##### Combinazioni semplici

Una **combinazione semplice** di $n$ elementi su $k$ posti è un **insieme** (non una sequenza, perché l'<u>ordine non conta</u>) di $k$ elementi scelti in un insieme di $n$ elementi (ovvero un sottoinsieme di $k$ elementi di un insieme di $n$ elementi).

###### Coefficiente binomiale

Per contare le combinazioni semplici si usa il **coefficiente binomiale**, ovvero:

$$C_{n,k} = \dbinom{n}{k} = \dfrac{n!}{k!*(n-k)!} = \dfrac{d_{n,k}}{k!}$$

> [!important] Proprietà
> Il coefficiente binomiale ha varie proprietà, ma qui le più semplici:
> 1) Formula di Newton: $\sum\limits^{n}_{k=0}\dbinom{n}{k} = 2^{n}$ = n° di sottoinsiemi di un insieme con $n$ elementi.
> 2) Legge delle classi complementari: $\dbinom{n}{k} = \dbinom{n}{n-k}$

###### Triangolo di tartaglia

Dalla 2a proprietà si deduce come tra $n$ coefficienti binomiali ordinati (secondo $k$), il <u>coefficiente in posizione</u> $k$ <u>corrisponde a quello in posizione</u> ${} n-k$.

Visualizzando questa legge per i vari valori di $n$ (da 0 a $\infty$) si ottiene un triangolo detto il **triangolo di tartaglia**:

![](https://i.imgur.com/yrErXPR.png)

Con ciò è possibile innanzitutto semplificare vari calcoli di coefficienti binomiali:

$k = 0 \;\rightarrow\; \dbinom{n}{0} = \dfrac{n!}{n!} = 1$

$k = n \;\rightarrow\; \dbinom{n}{n} = \dfrac{n!}{k!} = 1$

$k = 1 \;\rightarrow\; \dbinom{n}{1} = \dfrac{n!}{(n-1)!} = n$

$k = n-1 \;\rightarrow\; \dbinom{n}{n-1} = \dfrac{n!}{(n-1)!} = n$

Poi è anche possibile fare altri ragionamenti riguardanti la formula di Newton considerando i numeri di riga (in questo esempio indicati con $n$):

1) La somma dei numeri di ogni riga corrisponde a $2^{n}$:

   ![](https://i.imgur.com/hcqcDHE.png)

   Considerazione: vedi [[3 - Contenimento e insieme delle parti#Esempio insieme delle parti|powerset]] e guarda la riga del triangolo dove $n = 3$.

2) I numeri di ogni riga corrispondono ai relativi coefficienti di $(a+b)^{n}$:

   ![](https://i.imgur.com/FjSOiUp.png)

##### Combinazioni con ripetizioni

Per le combinazioni con ripetizioni, la formula è:

$$c'_{n,k} = \dbinom{n+k-1}{k}$$

#### Casi d'uso

a

# Esercizi

\1)

$A = \{a,b,c,d\}, n = 4, k = 2$

Le combinazioni sono 6: $\{a,b\},\{a,c\},\{a,d\},\{b,c\},\{b,d\},\{c,d\}$

Infatti: $\dbinom{n}{k} = \dfrac{4!}{2!\cdot(4-2)!} = \dfrac{24}{2 \cdot 2} = 6$

\2) Una gelateria ha 10 gusti di gelato, quanti coni con 3 gusti diversi è possibile fare?

(combinazioni semplici, non interessa ordine)

$n$ = 10 oggetti, $k$ = 3 posti

${} \dbinom{10}{3} = \dfrac{10!}{3!\cdot(10-3)!} = \dfrac{10!}{3! \cdot 7!} = \dfrac{10 \cdot 9 \cdot 8}{3 \cdot 2} = {}$ (questo perché 10! = 10 \* 9 \* 8 \* 7!) ${} = 5 \cdot 3 \cdot 8 = 120 {}$

\3) 4 frutti (mela, pera, banana, kiwi) quanti modi posso prendere 2 frutti anche uguali tra loro?

$n$ = 4, $k$ = 2

${} c'_{4,2} = \dbinom{4+2-1}{2} = \dbinom{5}{2} = \dfrac{5!}{2! \cdot 3!} = 10 {}$

# Soluzioni

---

Prossima lezione: [[17 - Principio di induzione]]

