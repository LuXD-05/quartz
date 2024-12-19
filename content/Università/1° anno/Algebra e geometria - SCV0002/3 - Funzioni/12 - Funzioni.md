# Lezione 12

### Funzioni

> [!important] Funzione
> Una funzione (o applicazione) tra $A$ e $B$ è una relazione $f \subseteq A \times B$ tale che ${} \forall x \in A$ esiste un unico $y \in B$, tale che $(x,y) \in f$.
> Dati $(x,y) \in f$ si scrive $f(x) = y$.

###### Notazione

> [!info] Notazione
> Se $f$ è una funzione tra $A$ e $B$, si scrive $f : A \rightarrow B$ (con $A$ = dominio e $B$ = codominio).

###### Esempi funzioni

La seguente **è** una funzione in quanto ogni elemento di $A$ è in relazione con un unico elemento di $B$ (non partono + frecce da 1 solo elemento di $A$).

![](https://i.imgur.com/JMJq1ah.png)

$f(1) = 4, f(2) = 4, f(3) = 5$

La seguente invece **NON è** una funzione, dato che:

- 1 elemento di $A$ è in relazione con + elementi di $B$,
- $f(2)$ non è definito.

![](https://i.imgur.com/DZiJ24i.png)

##### Dominio e codominio

> [!important] Dominio e codominio
> Se $f$ è una funzione tra $A$ e $B$:
> - $A$ è detto **dominio** (input),
> - $B$ è detto **codominio** (output).

##### Immagine e controimmagine

> [!important] Immagine e controimmagine
> ###### Immagine
> Se $f : A \rightarrow B$, ${} \;\;\forall x \in A$, ${} \;\;f(x) {}$ è detta **immagine** di $x$.
> (Ovvero), l'**immagine** di un elemento (del dominio) è l'<u>elemento del codominio con cui esso è relazionato</u>.
> Trovare l'immagine $y$ di $x$ significa fare ${} f(x) = y {}$
> ###### Controimmagine
> Se $f : A \rightarrow B$, ${} \;\;\forall y \in B {}$, ${} \;\;f^{-1}(y) = \{x \in A \;|\; f(x) = y\}\; {}$; quindi ${} f^{-1}(y) {}$ è la **controimmagine** di $y$.
> (Ovvero), la **controimmagine** di un elemento (del codominio) è <u>un sottoinsieme del dominio con gli elementi che hanno come immagine tale elemento</u> (del codominio).
> Trovare la controimmagine di $y$ significa fare $f^{-1}(y) = x$

##### Altri esempi di funzioni

###### 1) Funzione "raddoppio"

Questa: $\{(n, 2n) \;|\; n \in \mathbb{N} \} \subseteq \mathbb{N} \times \mathbb{N}$ è una funzione?

![](https://i.imgur.com/ZKIMTHi.png)

Qui si vede che da ogni $n$ parte una sola freccia che lo collega con $2n$, perciò è una funzione e si indica con: $f(n) = 2n$; (in questo caso dominio = codominio = $\mathbb{N}$).

###### 2) Funzione "lunghezza"

Con $A = \{a,b,c\}$ e $A^{+}$ come l'insieme delle parole su $A$, consideriamo:

$f: u \in A^{+} \;\rightarrow\; \#u \in \mathbb{N}$.

Ad ogni parola associo la sua lunghezza; ma è una funzione? Si, perché ogni parola ha un'unica lunghezza (da ogni elemento del dominio parte 1 sola freccia):

![](https://i.imgur.com/EI38w15.png)

###### 3) Funzione "cardinalità di powerset"

Data $f: x \in P(A) \;\rightarrow\; ...$

![](https://i.imgur.com/vmKSaOe.png)

###### 4) Funzione ?

$f: x \in P(A) \;\rightarrow\; x \cup \{a\} \in P(A)$

# Esercizi

# Soluzioni

---

Prossima lezione: [[13 - Tipi di funzioni]]

