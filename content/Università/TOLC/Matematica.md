---
modified_at: 23/09/2024 20:31:14
edited_seconds: 10
---
# Todo
### Aritmetica
- [ ] Numeri primi, 
- [ ] Scomposizione in fattori primi, 
- [ ] MCD e mcm, 
- [ ] Divisione con resto fra interi, 
- [ ] Potenze, 
- [ ] Radici, 
- [ ] Logaritmi, 
- [ ] Decimali, 
- [ ] Frazioni, 
- [ ] Percentuali, 
- [ ] Media (aritmetica).
### Algebra
- [ ] Manipolazione di espressioni, 
- [ ] Concetti di "soluzione"/"insieme delle soluzioni" di equazioni, di disequazioni, di sistemi di equazioni e/o di sistemi di disequazioni,
- [ ] Equazioni e disequazioni di 1° e 2° grado, 
- [ ] Algebra e sistemi lineari.
### Geometria
- [ ] Figure piane e proprietà elementari, 
- [ ] Teorema di Pitagora, 
- [ ] Proprietà dei triangoli simili, 
- [ ] Seno, coseno e tangente di angoli ottenuti come rapporti fra i lati di un triangolo rettangolo,
- [ ] Perimetro e area di figure piane, 
- [ ] Incidenza, parallelismo, perpendicolarità tra rette nel piano,
- [ ] Principali figure nello spazio (rette, piani, parallelepipedi, prismi, piramidi, cilindri, coni, sfere),
- [ ] Area e volume di solidi elementari,
- [ ] Coordinate cartesiane nel piano,
- [ ] Equazione della retta per 2 punti,
- [ ] Equazione della retta passante per un punto,
- [ ] Pendenza e intersezioni con gli assi di una retta,
- [ ] Distanza tra due punti o punto/retta o retta/retta.
### Studio di funzione
- [ ] Linguaggio elementare delle funzioni,
- [ ] Funzioni iniettive, surgettive, bigettive (o corrispondenze biunivoche), composte, invertibili, funzione inversa, pari dispari...
- [ ] Grafico di una funzione. 
- [ ] Funzioni esponenziali, logaritmiche, radici, valori assoluto, con polinomi di 1° e 2° grado, iperbole, seno, coseno e grafici.
- [ ] Semplici equazioni e disequazioni costruite con le suddette.
- [ ] Trasformazioni?.
### Calcolo combinatorio
- [ ] Rappresentazione e conteggio di insiemi finiti.
- [ ] Calcolo della probabilità di un evento in semplici situazioni.
### Logica
- [ ] In una situazione e date certe premesse, stabilire se un’affermazione è vera o falsa (deduzione). 
- [ ] Negare un’affermazione data. 
- [ ] Interpretare le locuzioni “condizione necessaria”, “condizione sufficiente” e “condizione necessaria e sufficiente”.
### Problemi
- [ ] Formulare in termini matematici una situazione o un problema.
- [ ] Comprendere testi che usano linguaggi e rappresentazioni diverse.
- [ ] Rappresentare dati, relazioni e funzioni con formule, tabelle, diagrammi a barre e altre modalità grafiche. 
- [ ] Risolvere un problema, adottando semplici strategie, combinando diverse conoscenze e abilità, facendo deduzioni logiche e semplici calcoli.
# Teoria
### Aritmetica
##### Criteri di divisibilità
Un numero naturale $n$ è divisibile per:
- **2** se l’ultima cifra è pari
- **3** se la somma delle cifre è divisibile per 3
- **4** se le ultime due cifre formano un numero divisibile per 4
- **5** se l’ultima cifra è 0 o 5
- **6** se è divisibile per 2 e per 3
- **7** se il numero ottenuto tralasciando l’ultima cifra sommato a 5 volte l’ultima cifra è divisibile per 7
- **8** se lo è il numero formato dalle sue ultime tre cifre
- **9** se la somma delle sue cifre è divisibile per 9
- **10** se la sua ultima cifra è 0
- **11** se il numero ottenuto tralasciando l’ultima cifra meno l’ultima cifra è divisibile per 11
##### MCD e mcm
###### MCD
Per calcolare l'MCD bisogna scomporre i numeri in fattori primi e di questi moltiplicare i fattori comuni alla potenza più bassa.
###### mcm
Per calcolare l'mcm bisogna scomporre i numeri in fattori primi e di questi moltiplicare i fattori comuni alla potenza più alta.
##### Insiemi
...
###### Intersezione
($A \cap B$) è il sottoinsieme formato dagli elementi comuni tra i 2 insiemi (contenuti sia in A sia in B).
###### Unione
($A \cup B$) è il sottoinsieme formato dagli elementi dei 2 insiemi presi singolarmente (contenuti 1 volta o in A o in B).
###### Complementare
Definendo l'insieme universo $U$ come l'insieme che contiene tutti gli altri insiemi e a cui appartengono tutti glie elementi degli stessi, il complementare di $A$ ($A^{c}$) comprende tutti gli elementi che non appartengono ad $A$ e che servono (insieme a quelli di $A$) a completare l'insieme in cui $A$ è contenuto (e quindi a corrispondere ai suoi elementi).
###### Prodotto cartesiano
Operazione tra insiemi che associa ogni elemento di A con ogni elemento di B, esempio: A = { 1, 2, 3 } : B = { a, b }
$A \;x\; B = \{ 1a, 1b, 2a, 2b, 3a, 3b \}$
### Algebra

### Geometria

### Studio di funzione
##### Definizione e intro
> [!important] Funzione
> Una relazione tra 2 insiemi A e B ($A \;\rightarrow\; B$) in cui 1 elemento di A corrisponde a 1 ed 1 solo di B.

Nell'esempio:
- $A$: è detto **dominio**,
- $B$: è detto **codominio**.
La variabile della funzione scelta all'interno del <u>dominio</u> è detta variabile **indipendente** e si indica con ${} x$.
La variabile della funzione scelta all'interno del <u>codominio</u> è detta variabile **dipendente** e si indica con $y$.
##### Tipi di funzione
###### Iniettiva
> [!important] Funzione iniettiva
> Una funzione è **iniettiva** quando ad elementi distinti del dominio corrispondono elementi distinti del codominio, quindi quando:
> $f(a_{1}) = f(a_{2}) \implies a_{1} = a_{2}$
> ![](https://i.imgur.com/5mMqT9k.png)

Graficamente, una funzione per essere iniettiva necessita che le proiezioni di tutti i suoi punti sull'asse delle y siano univoche per ogni punto (2 punti non possono avere la stessa y).
Una funzione non è iniettiva se presenta **asintoti verticali** <u>nel suo dominio</u>.
###### Suriettiva
> [!important] Funzione suriettiva
> Una funzione è **suriettiva** quando ogni elemento del codominio  è immagine di almeno 1 elemento del dominio, quindi quando:
> $b \in B \implies \exists a \in A : f(a) = b$
> ![](https://i.imgur.com/24ZVFam.png)

Graficamente, una funzione per essere suriettiva <u>non</u> necessita che le proiezioni di tutti i suoi punti sull'asse delle y siano univoche per ogni punto (2 punti possono avere la stessa y).
###### Biiettiva
> [!important] Funzione biiettiva
> Una funzione è **biiettiva** quando è al contempo iniettiva e suriettiva.
###### Invertibile
> [!important] Funzione invertibile
> Una funzione $f$ è **invertibile** se esiste una funzione $g$ che ha come dominio il codominio di $f$ e come codominio il dominio di quest'ultima.

Vale quindi:
![](https://i.imgur.com/iizV63T.png)
Perciò, una funzione è invertibile solo se è anche **biiettiva**.
###### Pari
> [!important] Funzione pari
> Una funzione pari è:
> - simmetrica rispetto all'asse y,
> - se ad $x$ vi sostituisco $-x$ essa rimane invariata,
> - (quindi) $f(x) = f(-x)$
###### Dispari
> [!important] Funzione dispari
> Una funzione dispari è:
> - simmetrica rispetto all'origine del piano cartesiano,
> - se ad $x$ vi sostituisco $-x$ essa assume valore opposto (in y),
> - (quindi) $f(-x) = -f(x)$
###### Crescente
> [!important] Funzione crescente
> Una funzione è crescente quando all'aumentare di $x$, anche $y$ aumenta.
###### Decrescente
> [!important] Funzione decrescente
> Una funzione è decrescente quando all'aumentare di $x$, $y$ diminuisce.
### Calcolo combinatorio
##### Sequenze
###### Senza ripetizioni
Esempio: calcolare quanti sono i numeri di 4 cifre distinte formabili con i numeri da 1 a 6.
Siccome abbiamo 6 cifre da usare ($n$) e 4 "posti" in cui si possono disporre ($k$), la formula da usare è:
$$\dfrac{n!}{(n-k)!} = \dfrac{6!}{(6-4)!} = 360$$
Le sequenze senza ripetizioni in cui $n = k$ sono dette **permutazioni** e per calcolarne il numero la formula è semplicemente $n!$.
###### Con ripetizioni

##### Binominale

##### Anagrammi

### Probabilità

### Logica
##### Proposizioni e negazioni
> [!important] Proposizione
> Affermazione a cui è sempre possibile assegnare un valore di verità oggettivamente.
> Data una proposizione $P$ è possibile formularne la **negazione**, indicata con $\neg{P}$.
##### Connettivi logici
Le proposizioni sono relazionabili in base a connettivi logici, quali "AND" ed "OR" logici, rappresentati rispettivamente con:
- A $\land$ B: per essere vero, nell'AND entrambe A e B devono essere vere purché anch'esso lo sia,
- A $\lor$ B: per essere vero, nell'OR basta che o A o B siano vere per affermare che anche la condizione lo sia.
Sono quindi definite le "tavole di verità" (in questo caso con P e Q):
![](https://i.imgur.com/apivNeP.png)
##### Implicazione
Con "implicazione" si intende il fatto che una proposizione ne implichi un'altra, significando di fatto (per esempio): "se P allora Q".
Rappresentazione: $P \implies Q$
L'unico caso in cui l'implicazione è falsa è quando la premessa "P" è vera mentre la conclusione "Q" è falsa. In tutti gli altri casi l'implicazione è vera (anche quando la premessa è falsa, qualsiasi valore logico la conclusione assuma).
###### Contronominali
Il concetto è identico per le implicazioni (invertite) con negazione (sia in premessa sia in conclusione), dette **contronominali**: $\neg{Q} \implies \neg{P}$. 
Tali sono equivalenti alle loro implicazioni non contronominali e verificare queste significa quindi verificare le altre e viceversa, infatti:
![](https://i.imgur.com/KEjBNab.png)
###### Dimostrazione per assurdo
Se si deduce che da $\neg{P}$, $Q$ è chiaramente falsa, allora (per le tavole di verità) anche $\neg{P}$ sarà falsa, perciò $P$ sarà vera.
##### Condizioni
Data l'implicazione $P \implies Q\;$ vera, di definiscono:
> [!important] Condizione sufficiente
> $P$ è condizione sufficiente per $Q$, ovvero, ci basta sapere che $P$ è vera per dire che anche $Q$ lo sia.

> [!important] Condizione necessaria
> $Q$ è condizione necessaria per $P$, ovvero, è necessario sapere che $Q$ sia vera per dire che anche $P$ lo sia.

Se entrambe le proposizioni implicano l'un l'altra ($P \iff Q$) all'ra questa è detta **condizione necessaria e sufficiente**.