---
modified_at: 02/10/2024 11:58:03
edited_seconds: 6630
public: true
---
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
###### Differenze

###### Moltiplicazioni

###### Divisioni

### Rappresentazione di interi
Con N bit si possono rappresentare tutti i numeri interi senza segno (positivi o nulli) compresi tra 0 e $2^{N}-1$.
8 bit (numero binario con 8 cifre) = 1 byte
##### Overflow
Supponiamo di rappresentare interi a 16 bit e che $A = 30936,\;B = 54600,\;C = 0$
Facendo $C = A + B$, ci si aspetta che $C = 85536$, ma in realtà il suo valore è 20000.
Ciò avviene perché 85536 è un numero troppo grande per essere rappresentato come intero a 16 bit proprio perché $2^{16} - 1 = 65535$, ovvero il valore massimo rappresentabile da un intero a 16 bit (sono comunque 65536 cifre, perché si parte da 0 contandolo).
Quando un registro o una cella di memoria vanno in overflow, il valore che "trabocca" è reinserito nella cella, infatti, facendo $85536 - 65536 = 20000$.
##### Rappresentazione in modulo e segno
Il modo più semplice per rappresentare numeri negativi consiste nel trattarli normalmente, con un simbolo per il segno ed altri per il valore assoluto.
Per rappresentare esplicitamente il segno, si usa un bit (detto **MSB**, *Most Significant Bit* o la cifra più significativa, quella che vale di più), che assume:
- Valore 0 se il numero è positivo,
- Valore 1 se il numero è negativo.
###### Esempio
Per un intero ad 8 bit, l'MSB (bit 7) è considerato come **segno**, mentre il resto (bit da 0 a 6) sono il **valore assoluto**.
Il segno è <u>completamente disgiunto</u> dal valore assoluto.
###### Problemi
La rappresentazione di interi *signed* presenta 2 problemi:
1) Lo 0 ha 2 diverse rappresentazioni:
   - 1 0000000 = -0
   - 0 0000000 = +0
2) Gli algoritmi per eseguire le operazioni coi numeri naturali non funzionano più, vedi "$9 + (-9)$":
   $$0\;\;0001001 +$$
   $$1\;\;0001001 =$$
   $$------$$
   $$1\;\;0010010 =$$
   Il che fa $-18$, quando dovrebbe essere invece $0$.

### Complemento a 2
Con questa rappresentazione, l'MSB di un numero ha peso $-2^{N-1}$ (invece che $2^{N-1}$), mentre il valore del resto dei bit è normale.
Il valore di un intero v espresso con tale notazione è dato dalla formula: (formula)
L'unica pecca è che un intero *signed* a 8 bit non rappresenta più i valori da 0 a 255, ma da -128 a 127. Esempi:
11010101 = -128 + 64 + 16 + 4 + 1 = -43
01000111 = 64 + 4 + 2 + 1 = +71
###### Quindi
La rappresentazione non è più completamente posizionale; ma solo dal MSB si capisce se il numero è positivo o negativo.
Inoltre si risolve il problema della doppia rappresentazione dello 0.
##### Rappresentare in complemento a 2 un numero negativo
Dato un numero N, si vuole rappresentare -N in complemento a 2 mediante 8 bit.
N = 128 + X
-N = -128 + X
S in compl. a 2 = -128 + X = -N --> X = 128-N
...
###### Esempio
-N = -74
-128 + X = -74
...

> [!important] Formula
> $Cp_{2} \; (-N) = 2^{k}, \; per \; N > 0$
> (Generalizzando alla rappresentazione per *k* bit)

Con k = 8, la rappresentazione di $1$ in complemento a 2 è:
$Cp_{2} \; (-1) = 2^{8} - 1 = 256 - 1 = 255 = 11111111$
(Poi -1 in generale è sempre una sequenza di tutti "1" come anche 0 è sempre una sequenza di "0")
##### Proprietà
Il range di valori rappresentabili da un intero in complemento a 2 va da ${} -2^{k-1} {}$ a $2^{k-1}-1$.
C'è il -128 perché lo 0 è considerato come parte dei positivi, rendendo i numeri rappresentabili come 128 negativi e 128 positivi.
Inoltre è verificata la proprietà $x + (-X) = 0$ (trascurando il riporto siccome va in overflow).
###### Problema
La rappresentazione in complemento a 0 permette però di usare algoritmi usati anche per numeri naturali per eseguire operazioni aritmetiche.
In particolare è verificata la proprietà X - X = 0 ...

...
###### Esempio
$Cp_{2}(47) = 256 - 47 = 209 = 11010001$
$47 + (-47) = 0$
Come:
$00101111 + 11010001 = (1) 00000000 = 0$
(1 qui è il riporto che diventa $2^{9}$ e quindi 0 siccome non rappresentabile in interi a 8 bit).

##### Calcolare un inverso in complemento a 2
La definizione formale del complemento a 2 è poco pratica per determinarne la rappresentazione di un numero, quindi:
Dalla definizione $Cp_{2} (-X) = 2^{n} - X$
Aggiungendo e sottraendo 1 il risultato non cambia: $Cp_{2} (-X) = (2^{n} - 1) (- X + 1)$
Sappiamo però che $2^{n}-1 = -1$, siccome risulta in un numero binario in complemento a 2 composto da soli "1".
Poi, la differenza tra gli $n$ "1" ed  il numero binario $X$ corrisponde ad invertire  tutti i bit di $X$
Infine basta solo aggiungere 1 per riottenere $2^{n} - X$
###### Esempio
Vogliamo trovare -25 partendo da 25 (su 8 bit):
0) 25 = 00011001
1) Invertire i bit: 11100110
2) Aggiungere 1: 11100111 = -128 + 64 + 32 + 4 + 2 + 1 = **-25**
Questo funziona anche coi numeri negativi, da -25 si riotterrebbe 25.
###### Casi limite
In decimale: $-73 -73 = -146$
Ma in binario: $10110111 - 10110111 = (1)01101110 = +110$ (in 8 bit)
(vale anche per $73 + 73$, che poi da in binario $10010010 = -110$)
Quando ci sono operazioni tra valori in $Cp_{2}$, è possibile andare in ***overflow***:
- Con numeri negativi > 128,
- Con numeri positivi > 127.
Infatti quei valori non sono compresi nell'intervallo di rappresentazione \[-128,127\], per questo i risultati invadono il bit di segno.
> [!important] Regole
> Esistono 2 regole per verificare se si ha un *overflow*:
> - Somme tra numeri (nel range) di segno opposto non provocheranno mai overflow (in quanto non escono dal range),
> - Somme tra numeri di segno uguale provocheranno overflow se il risultato non mantiene il loro segno.

### Notazione polarizzata
##### Rappresentazione in codice eccesso B
La notazione polarizzata (*in codice eccesso B*) è una notazione non completamente posizionale impiegata nell'aritmetica a virgola mobile.
Il valore denotato da una rappresentazione su *k* bit $d_{k-1}, d_{k-2}, ... d_{1}, d_{0}$ corrisponde a $2^{k-1} * d_{k-1} + 2^{k-2} *d_{k-1}$.
$B$ corrisponde ad un bias prefissato riferito come **eccesso** o **polarizzazione**.
Nella rappresentazione a virgola mobile IEEE 754, $B$ assume valore costante:
- 127 per rappresentazione su 8 bit (singola precisione),
- 1023 per rappresentazioni a 11 bit (doppia precisione).
In questa rappresentazione il numero N da rappresentare viene prima sommato a B e poi codificato come intero *unsigned*.
Esempio: K = 8 e B = 127, consideriamo la codifica 10000000 denota  il valore 1 (ovvero $1 * 2^{7} - 127 = 128 - 127 = 1$)

Quindi il valore in polarizzata è N sommato all'eccesso (B) e rappresentato in binario puro. Per riconvertirlo in decimale basta ritrasformarlo in decimale e togliere l'eccesso (B).

##### Rappresentazione in codice eccesso 2^k-1
Il numero da rappresentare $N$ è sommato a $2^{k-1}$ e codificato come intero *unsigned*.
Esempio: k = 3 e N = -1, N in codice eccesso $2^{3-1} = (-1 + 2^{3-1} = 3) = 011$ 
Per definizione, il valore v della formula è ... (formula)
Formula + figa : $v = N + 2^{k-1} = -1 + 2^{3-1} = 3 = 011$
Come prima per fare al contrario, riconvertire $v$ in decimale e poi sottrarre $2^{k-1}$
###### Numeri negativi in codice eccesso 2^k-1

(QUESTI SONO POSITIVI PERCHE LE SLIDE DI COLOMBO FANNO CAGARE)

I numeri positivi in codice eccesso $2^{k-1}$ hanno MSB = 1.
Se $d_{k-1} = 1$, la formula $v = -2^{k-1} - 2^{k-1} * d_{k-1} + ... + 2^{0}*d_{0}$ si riduce a:
$v = ... + 2^{0}*d_{0}$
Esempio:
Con k = 4 bit, 1101 denota il valore di N: 4 + 1 = 5; poiché il bit 3 che ha peso 8 viene compensato dalla sottrazione di $2^{4-1} = 8$.
(dualmente: se N = 5 gli sommo 2^4-1 = 13, allora 13 in base 2 = 1101)

(QUESTI SONO POSITIVI PERCHE LE SLIDE DI COLOMBO FANNO CAGARE)

Ora partono i negativi
I negativi in codice eccesso ... hanno con MSB = 0
Se $d_{k-1} = 0$, la formula $v = -2^{k-1} - 2^{k-1} * d_{k-1} + ... + 2^{0}*d_{0}$ si riduce a:
$v = -2^{k-1} + ... + 2^{0}*d_{0}$
Esempio:
Con k = 4 bit, 0101 denota -8 + 4 + 1 = -3

###### Proprietà
Intervallo:
- MSB = 1 --> k-1 bit usabili come in binario puro (intervallo da 0 a $2^{k-1}-1$),
- MSB = 0 --> stesso intervallo traslato di $-2^{k-1}$ --> (intervallo da $-2^{k-1}$ a -1).
Complessivamente l'intervallo è ...
Esempio:
4 bit = 16 combinazioni = intervallo da -8 a 7, come col Cp2 con metà valori psitivi e meta negativi.