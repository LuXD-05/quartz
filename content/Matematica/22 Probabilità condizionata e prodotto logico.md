### Probabilità condizionata

> [!important] Dipendenza
> 2 eventi sono **dipendenti** quando il verificarsi di uno <u>influisce</u> sul verificarsi dell'altro.
> 2 eventi sono **indipendenti** quando il verificarsi di uno <u>non influisce</u> sul verificarsi dell'altro.

Inoltre:

> [!important] Probabilità condizionata
> (Dati 2 eventi $E_{1}$ ed $E_{2}$) la probabilità condizionata di $E_{2}$ rispetto a $E_{1}$ corrisponde alla probabilità che $E_{2}$ si verifichi sapendo che si è già verificato $E_{1}$.
> La probabilità condizionata di $E_{2}$ rispetto ad $E_{1}$ si rappresenta con: $p(E_{2}|E_{1})$.

##### Prodotto logico di eventi

Dato che gli eventi sono degli <u>insiemi</u>, è possibile eseguire con essi l'operazione di **prodotto logico** (corrispondente all'**intersezione**).

![](https://i.imgur.com/e9o4bnQ.png)

Il **prodotto logico** di 2 eventi si rappresenta con: $\; E_{1} \;\cap\; E_{2} \;$. Quindi:

- Per gli eventi **dipendenti**: $\;\;\;\; E_{1} \;\cap\; E_{2} \;=\; p(E_{1}) \;*\; p(E_{2}|E_{1})$
- Per gli eventi **indipendenti**: $\; E_{1} \;\cap\; E_{2} \;=\; p(E_{1}) \;*\; p(E_{2})$

##### Esercizio probabilità condizionata

###### Esercizio

Calcola la probabilità che, estraendo una carta da un mazzo da 40 (7 numeri e 3 figure per seme), essa sia pari sapendo che è uscito picche.

- $E_{1}$ = che la carta sia picche
- $E_{2}$ = che la carta (si picche) sia pari

$\#S \;=\; 40 \;\;\lvert\;\; \#E_{1} \;=\; 10 \;$ (non si scrive la cardinalità di $E_{2}$ in quanto dipende da $E_{1}$ e si fa dopo con $\cap$)

$p(E_{1}) \;=\; \dfrac{f}{N} \;=\; \dfrac{\#E_{1}}{\#S} \;=\; \dfrac{1}{4}$

$\#E_{2} \;\cap\; \#E_{1} \;=\; 3 \;\;\rightarrow\;\; p(E_{2} \;\cap\; E_{1}) \;=\; \dfrac{f}{N} \;=\; \dfrac{\#E_{2} \;\cap\; \#E_{1}}{\#S} \;=\; \dfrac{3}{40}$

$p(E_{2} \lvert E_{1}) \;=\; \dfrac{p(E_{2} \;\cap\; E_{1})}{p(E_{1})} \;=\; \dfrac{\frac{3}{40}}{\frac{1}{4}} \;=\; \dfrac{3}{40} * \dfrac{4}{1} \;=\; \dfrac{3}{10}$

##### Esercizio prodotto logico

###### Step

0) Capire se gli eventi sono dipendenti o indipendenti:
1) Calcolare la probabilità del 1° evento (per $S$ e $f \;/\; E_{1}$ fare pure solo la $\#$ se si può):
2) Calcolare la probabilità condizionata del 2° evento rispetto al 1° (calcolandone prima la cardinalità e lo spazio campionario dopo il 1° evento):
3) Calcolare la probabilità totale (intersezione tra i 2 eventi):

###### Esercizio

Si consideri quindi la seguente situazione: un'urna contiene 3 palline nere e 3 palline rosse. Ne viene estratta una e non viene reimmessa. Ne viene estratta una 2a. Probabilità che le palline siano entrambe nere? 

Cambia lo spazio campionario dopo il verificarsi del 1° evento? Si: dipendenti | No: indipendenti.

$\#S_{0} \;=\; 6 \;\;\lvert\;\; \#E_{1} \;=\; 3$

$p(E_{1}) \;=\; \dfrac{f}{N} \;=\; \dfrac{\#E_{1}}{\#S_{0}} \;=\; \dfrac{3}{6}$

$\#S_{1} \;=\; 6 \;-\; 1 \;=\; 5 \;\;\lvert\;\; \#E_{2}|E_{1} \;=\; 3 - 1 \;=\; 2$

$p(E_{2}|E_{1}) \;=\; \dfrac{f}{N} \;=\; \dfrac{\#E_{2}|E_{1}}{\#S_{1}} \;=\; \dfrac{2}{5}$

$p(E_{1} \;\cap\; E_{2}) \;=\; p(E_{1}) \;*\; p(E_{2}|E_{1}) \;=\; \dfrac{5}{21} \;*\; \dfrac{4}{20} \;=\; \dfrac{1}{21}$

---

Vedi poi: [[23 Prismi e parallelepipedi]]

