# Lezione 35

### Sottospazi

Un sottospazio $U$ di uno spazio vettoriale $V$ è un sottoinsieme ***stabile*** di $V$, ovvero tale che siano rispettate le ***condizioni di stabilità*** per esso:

- $\forall u_{1}, u_{2} \in U \implies u_{1} + u_{2} \in U$
- $\forall u \in U, r \in \mathbb{R} \implies r \cdot u \in U$

> [!important] Nota
> Ogni sottospazio vettoriale è a sua volta uno **spazio vettoriale**.
> Un sottospazio vettoriale deve contenere sempre il **vettore nullo**.

###### Verificare sottospazi

Similmente agli spazi vettoriali, per verificare se uno spazio è un sottospazio bisogna:

1) <u>Definire l'insieme</u> $U$, l'<u>operazione di somma</u> ($+$) e quella di <u>prodotto per uno scalare</u> ($\,\cdot\,$),
2) Verificare la validità delle *condizioni di stabilità*.

##### Proprietà

Se $U$ è un sottospazio vettoriale di $\mathbb{R}^{2}$, allora $U$ può essere:

- L'**origine**, ovvero $U$ è formato solo dal **vettore nullo**: $U = \{(0,0)\}$,
- Una **retta** che <u>passa per l'origine</u>,
- $\mathbb{R}^{2}$.

Andando ad aumentare le dimensioni (tipo $\mathbb{R}^{3}$), $U$ può essere:

- $\{0,0,0\}$,
- Una retta che passa per l'origine,
- Un ***piano*** che passa per l'origine,
- $\mathbb{R}^{3}$.

###### Combinazioni lineari

> [!important] Nota
> Per far sì che $U$ sia un sottospazio, le componenti dei vettori devono essere combinazioni lineari:
> - Di variabili: $u_{1} = r \cdot u_{2}$,
> - L'una dell'altra: $u_{1} = r_{2} \cdot u_{2} + r_{3} \cdot u_{3} \ldots$.

# Esercizi

###### 1) Verificare un sottospazio

$V = \mathbb{R}^{2}$, $\;\;\; U = \{(x,0) \;|\; x \in \mathbb{R} \}$ è un sottospazio?

###### 2) Verificare un sottospazio

$V = \mathbb{R}^{2}$, $\;\;\;U = \{(1,x) \;|\; x \in \mathbb{R}\}$ è un sottospazio?

###### 3) Provare che $X$ è un sottospazio (soluzioni di un sistema)

![](https://i.imgur.com/zbNtgLR.png)

###### 4) Provare che $U$ è un sottospazio (matrici)

![](https://i.imgur.com/24ygRBY.png)

# Soluzioni

###### 1) 

Per quanto riguarda la somma, se $u_{1}, u_{2} \in U \;\;\rightarrow\;\; u_{1} + u_{2} = (x_{1}, 0) + (x_{2}, 0) = (x_{1} + x_{2}, 0) \in U \;\;\rightarrow\;\;$ Si.

Per quanto riguarda il prodotto scalare, se $u \in U, r \in \mathbb{R} \;\;\rightarrow\;\; r \cdot u = r(x_{1}, 0) = (r \cdot x_{1}, 0) \in U \;\;\rightarrow\;\;$ Si.

Quindi $U = \{(x,0) \;|\; x \in \mathbb{R} \}$ è un sottospazio (di $V = \mathbb{R}^{2}$).

###### 2) 

Per quanto riguarda la somma, se $u_{1}, u_{2} \in U \;\;\rightarrow\;\; u_{1} + u_{2} = (1, x_{1}) + (1, x_{2}) = (2, x_{1} + x_{2}) \in U \;\;\rightarrow\;\;$ No, $(2,x) \not\in \{(1,x)\}$.

Basta questo per constatare che $U = \{(1,x) \;|\; x \in \mathbb{R} \}$ <u>non</u> è un sottospazio (di $V = \mathbb{R}^{2}$).

---

Prossima lezione: [[36 - Basi di spazi vettoriali]]

