### Livello logico

A livello di circuiti logici, i calcolatori memorizzano e rappresentano valori basati su bit

...

##### Numeri

Esistono diversi tipi di rappresentazione degli interi non negativi:

- **Notazioni additive**: tipo per i numeri romani, dove ogni simbolo ha valore fisso e i loro valori si sommano a meno ché il valore di uno non preceda un simbolo con valore maggiore (in quel caso si sottrae),
- **Notazioni posizionali**: dove il valore di un simbolo è determinato in base alla sua posizione (formula: $n_{0}B^{0} + n_{1}B^{1} \;...\; n_{k}B^{k}$). In questa le cifre ($n$, che assumono valori da $0$ a $B-1$) acquistano significatività da destra a sinistra per ogni posizione (in formula: $n_{?}$ = numero, $B^{?}$ = base elevata a una potenza in base alla sua posizione).

###### Notazioni

> [!important] Notazione decimale
> La **notazione decimale** è una notazione posizionale avente base 10, pertanto la formula precedente diventa:

$n_{0}10^{0} + n_{1}10^{1} \;...\; n_{k}10^{k}$

I valori che $n$ può assumere sono (dato $n = \{0 \;...\; B-1\}$) $\;\rightarrow\;$ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

> [!important] Notazione binaria
> La notazione binaria invece ha base 2, quindi si ha:
> $n_{0}2^{0} + n_{1}2^{1} \;...\; n_{k}2^{k}$
> I valori che $n$ può assumere sono (dato $n = \{0 \;...\; B-1\}$) $\;\rightarrow\;$ 0, 1

> [!important] Notazione esadecimale
> La notazione esadecimale invece ha base 16, quindi si ha:
> $n_{0}2^{0} + n_{1}2^{1} \;...\; n_{k}2^{k}$
> I valori che $n$ può assumere sono (dato $n = \{0 \;...\; B-1\}$) $\;\rightarrow\;$ 0, 1
> ATTENZIONE: per non confondersi (dato che la notazione esadecimale per rappresentare i numeri da 10 a 15 usa le lettere dalla A alla F) solitamente i numeri esadecimali sono preceduti dalla sequenza di caratteri "0x".

###### Passare da base B a base 10

Per passare da una base $B$ alla base 10, basta semplicemente moltiplicare tutte le cifre del numero in base $B$ per $B$, e si otterrà il numero in base 10:

$n_{B} = n_{0}B^{0} + n_{1}B^{1} \;...\; n_{k}B^{k}$

Esempio:

$351_{6} = 1 * 6^{0} + 5 * 6^{1} + 3 * 6^{2} = 139_{10}$

###### Passare da base 10 a base B

(Spiegazione Colombo: $n_{10} = d_{0} * B(d_{1} * B(d_{2} * B(...)))$ ... poi me la rivedo va)

Per passare da un numero in base 10 ad un numero in base $B$, basta semplicemente fare la divisione con resto di un numero per la sua base finché non si arriva a 0, i resti in ordine (dall'ultimo al 1°) daranno il numero in base $B$:

(foto)

###### Conversione tra basi una potenza dell'altra (sistemare)

Consideriamo 2 rappresentazioni in base $P$ e $B$ dello stesso valore $N$:

$N = m_{0}P^{0} + m_{1}P^{1} \;...\; m_{j}P^{j}$

$N = n_{0}B^{0} + n_{1}B^{1} \;...\; n_{k}B^{k}$

Supponiamo ora che $P$ sia una potenza di $B$ ($P = B^{x}$):

$N = m_{0}P^{0} + m_{1}P^{1} \;...\; m_{j}P^{j}$

$N = m_{0}B^{0x} + m_{1}B^{1x} \;...\; m_{j}B^{jx}$

Facendo $\dfrac{N}{B}$, il resto è $e_{0}$

Viceversa la 1a cifra di $N$ in base $P$ è ricavabile osservando le prime $m$ cifre di $N$ in base $B$.

Applicando le divisioni successive otteniamo che l'ennesima cifra di $N$ in base $P$ è ricavabile osservando l'ennesimo gruppo di $m$ cifre di $N$ in base $B$.

Esempio: vogliamo convertire in base 2: $N = 5731_{8}$ 

Siccome la base di $N$ è una potenza della base 2, si può determinare che per ogni cifra del numero in base (in questo caso) 8, ci saranno $log_{2}8$ (3) cifre in base 2.

dato che ogni cifra in base 8 = 3 cifre in base 2, è possibile trasformare singolarmente ogni cifra di $N_{8}$ in 3 cifre di ${} N_{2} {}$

$N = 5731_{8} \;\;\rightarrow\;\; 101 111 011 001$

Esempio: vogliamo convertire in base 2: $N = 5731_{16}$ 

Siccome la base di $N$ è una potenza della base 2, si può determinare che per ogni cifra del numero in base (in questo caso) 8, ci saranno $log_{2}16$ (4) cifre in base 2.

dato che ogni cifra in base 8 = 4 cifre in base 2, è possibile trasformare singolarmente ogni cifra di $N_{8}$ in 4 cifre di $N_{2}$

$N = 5731_{16} \;\;\rightarrow\;\; 0101 0110 0011 0001$

##### Operazioni aritmetiche

Tutte le notazioni posizionali utilizzano le stesse regole (indipendentemente dalla base) come per le operazioni normali in base 10.

###### Somme

In binario:

$0 + 0 = 0$

$0 + 1 = 1$

$1 + 1 = 10$ (oppure $0$ con riporto di $1$)

In esadecimale:

