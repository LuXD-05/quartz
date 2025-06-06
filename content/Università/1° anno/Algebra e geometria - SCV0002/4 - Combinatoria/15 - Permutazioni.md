# Lezione 15

### Permutazioni

##### Permutazioni semplici

Le **permutazioni semplici** sono delle [[#Disposizioni semplici|disposizioni semplici]] nelle quali $n = k$.

> [!error] Attenzione
> $$0! = 1$$
> Ciò rende possibile questo: $d_{n,n} = \dfrac{n!}{(n-n)!} = \dfrac{n!}{0!} = \dfrac{n!}{1} = n!$.
> Infatti il **numero di permutazioni** di $n$ elementi è sempre $n!$.

##### Permutazioni con ripetizioni

Le **permutazioni con ripetizioni** sono identiche alle permutazioni semplici, solo che alcuni elementi che "permutano" si ripetono più volte.

Dal calcolo totale delle permutazioni semplici ($n!$) quindi bisogna rimuovere i casi in cui gli elementi duplicati si invertono di posizione (perché siccome sono lo stesso elemento che si ripete, sarebbe come contare la stessa permutazione più volte).

> [!info] Quindi
> Dati $n$ il numero totale di elementi e $k_{n}$ i numeri di elementi ripetuti, per contare le permutazioni con ripetizioni si usa la seguente formula:
> $$\dfrac{n!}{k_{n}!} = \dfrac{n!}{k_{1}! \cdot k_{2}!\, \cdot \,...\, \cdot \,k_{n}!}$$

#### Casi d'uso

I casi d'uso delle permutazioni sono principalmente il calcolo del totale dei modi in cui è possibile disporre $n$ elementi (in $n$ posti).

Le permutazioni semplici sono usate per contare gli anagrammi di parole senza lettere ripetute.

Le permutazioni con ripetizioni sono invece usate per contare gli anagrammi di parole aventi lettere ripetute.

# Esercizi

##### Es permutazioni semplici

- [ ] 1) Quanti modi ci sono per ridisporre gli elementi di $A = \{a,b,c,d\}$?.

##### Es permutazioni con ripetizioni

- [ ] 2) Contare gli anagrammi della parola CARRO.
- [ ] 3) Contare gli anagrammi della parola MATEMATICA.

# Soluzioni

##### 1)

${} \{a,b,c,d\} = 4! = 4 \cdot 3 \cdot 2( \cdot 1) = 24 {}$

##### 2)

Il numero totale di permutazioni è $5!$.

Tuttavia esistono permutazioni del tipo: $CAR_{1}R_{2}O$ e $CAR_{2}R_{1}O$, perciò le lettere ripetute sono 2.

Il numero di permutazioni corrette sarà quindi: $\dfrac{5!}{2!} = \dfrac{5 \cdot 4 \cdot 3\; \cdot \not{2}\; \cdot \not{1}}{\not{2}\; \cdot \not{1}} = 5 \cdot 4 \cdot 3 = 60$

##### 3)

(151200)

---

Prossima lezione: [[16 - Combinazioni]]

