# Lezione 8

### Numeri interi in binario

Con $N$ bit si possono rappresentare tutti i <u>numeri interi senza segno (positivi o nulli) compresi tra</u> 0 e $2^{N}-1$ (per dire, un numero binario a 8 cifre, "pesa" 8 bit e quindi 1 byte).

##### Overflow

Supponiamo di rappresentare interi a 16 bit e che <u>A = 30936, B = 54600, C = 0</u>.

Facendo <u>C = A + B</u>, ci si aspetta che <u>C = 85536</u>, ma in realtà il suo valore è **20000**.

Ciò avviene perché <u>85536 è un numero troppo grande per essere rappresentato come intero a 16 bit</u> proprio perché $2^{16} - 1 = 65535$, ovvero il valore massimo rappresentabile da un intero a 16 bit (sono comunque **65536 numeri**, perché si parte da 0 contandolo).

Quando un registro o una cella di memoria vanno in ***overflow***, il valore che "trabocca" è reinserito nella cella ripartendo da 0; infatti: 85536 - 65536 = 20000.

##### Problemi

Tutto a posto finché si rappresentano numeri interi ***unsigned*** (senza segno, quindi solo positivi o nulli); ma poi sorgono dei <u>problemi</u> quali:

- Come rappresentare numeri ***signed*** (con segno, quindi sia positivi che negativi),
- Come mantenere l'<u>efficienza delle operazioni</u> (siccome sono molto frequenti).

## Tipi di rappresentazione

### Rappresentazione in modulo e segno

Per rappresentare **numeri negativi** semplicemente si dedica l'**MSB** (*Most Significant Bit*) ovvero il bit (la cifra) più significativo (che vale di più) per la rappresentazione del segno $+$ o $-$, i cui valori sono:

- **0** se il numero è **positivo**,
- **1** se il numero è **negativo**.

> [!info] Ricorda
> Il segno è <u>completamente disgiunto</u> dal valore assoluto.

###### Esempio rappresentazione in modulo e segno

Per un intero ad 8 bit, l'**MSB** (7° bit, si parte da 0) è considerato come **segno**, mentre il resto (bit da 0 a 6) sono il **valore assoluto**, quindi:

- +5  =  0|0000101
- -2  =  1|0000010

##### Problemi

La rappresentazione in modulo e segno di interi *signed* presenta 2 <u>problemi</u>:

1) Lo **0** ha <u>2 diverse rappresentazioni</u>:

   - 1 0000000 = -0

   - 0 0000000 = +0

2) Gli algoritmi per eseguire le <u>operazioni coi numeri naturali non funzionano più</u>:   $$9 + (-9)$$   ![](https://i.imgur.com/U6IaXUu.png)

Proprio per questo (e per i conseguenti costi eccessivi di circuiti/algoritmi/tempo) è una notazione poco utilizzata.

### Complemento a 2

Con questa rappresentazione (detta anche ***Cp2***), l'**MSB** di un numero è considerato come **negativo** (ovvero pesa $-2^{N-1}$ invece di $2^{N-1}$), mentre il valore del resto dei bit è sempre positivo.

Il valore di un intero $v$ espresso con tale notazione è dato dalla seguente formula:

$$v = d_{0}B^{0} + d_{1}B^{1} + d_{2}B^{2} + \ldots + d_{n-2}B^{n-2} - d_{n-1}B^{n-1}$$

L'unica pecca è che un <u>intero signed a 8 bit non rappresenta più i valori da 0 a 255, ma da -128 a 127</u>. Esempi:

1|1010101 = -128 + 64 + 16 + 4 + 1 = -43

0|1000111 = 64 + 4 + 2 + 1 = +71

###### Quindi

- La rappresentazione <u>non è più completamente posizionale</u>,
- Già solo dall'<u>MSB</u> si capisce se il <u>numero è positivo o negativo</u>,
- Lo **0** ha un'<u>unica rappresentazione</u>.

##### Rendere un binario puro negativo col Cp2

###### Metodo 1

Per rendere negativi interi in $N$ bit (minori di $2^{N-1}$) usando il complemento a 2 è necessario seguire questi step:

1) Ottenere l'intero $n$ da trasformare,
2) Sottrarre da 128 l'intero $n$,
3) Trasformare il risultato in binario puro,
4) Aggiungere all'inizio (come MSB) un 1 al risultato (vale -128 in Cp2).

###### Metodo 2

Se tale risultato però lo si immagina come binario puro, l'MSB diventa +128, facendo guadagnare 256 al risultato in Cp2. 

Il vero numero in binario puro, quindi corrisponderà al valore del binario negativo in Cp2 + 256.

Proprio per questo è possibile stabilire il 2° metodo per rendere negativo un binario puro, ovvero:

$$256 - n = -n_{Cp2}$$

(Si ricorda che $-n_{Cp2}$ è da convertire in binario).

###### Metodo 3

È possibile anche usare un algoritmo pratico per il calcolo di un intero binario puro negativo in Cp2 (sempre con ${} n < 2^{N-1} {}$), e ciò consiste in:

1) Ottenere $n$ in binario puro,
2) Invertirne tutti i bit,
3) Aggiungere 1.

###### Esempio Cp2

$n$ in binario puro = 74, lo si vuole rendere negativo col Cp2:

Col 1° metodo: $128 - 74 = 54 \;\rightarrow\; 0110110 \;\rightarrow\; -74 = 1|0110110$.

Col 2° metodo: $256 - 74 = 182 \;\rightarrow\; 10110110$.

Col 3° metodo: $74 = 01001010 \;\rightarrow\; -74 = 10110101 + 1 = 10110110$

##### Proprietà

- Il range di valori rappresentabili da un intero in complemento a 2 va da $-2^{k-1}$ a $2^{k-1}-1$ (quindi tipo per 8 bit, il range va da -128 a 127).
- È possibile eseguire operazioni aritmetiche tra binari puri e binari in Cp2 (trascurando l'*overflow*), in particolare $n_{2} + (-n_{Cp2}) = 0$:

  ![](https://i.imgur.com/MQU7JOl.png)

###### Casi limite

![](https://i.imgur.com/NsvyRKe.png)

Quando ci sono operazioni tra valori in $Cp_{2}$, è possibile andare in **[[#Overflow|overflow]]**:

- Con numeri negativi la cui somma è < -128,
- Con numeri positivi la cui somma è > 127.

Infatti quei valori non sono compresi nell'intervallo di rappresentazione \[-128,127\], per questo i risultati invadono il bit di segno.

> [!important] Regole
> Esistono 2 regole per verificare se si ha un *overflow*:
> - Somme tra numeri (nel range) di segno opposto non provocheranno mai overflow (in quanto non escono dal range),
> - Somme tra numeri di segno uguale provocheranno overflow se il risultato non mantiene il loro segno.

### Notazione polarizzata

##### Rappresentazione in codice eccesso B

La **notazione polarizzata** (*in codice eccesso B*) è una notazione non completamente posizionale impiegata nell'aritmetica a virgola mobile.

Semplicemente, questa notazione prevede di sommare al numero da rappresentare in binario una costante $B$ detta **eccesso** o **polarizzazione** prima di codificarlo effettivamente. Per riconvertire il valore binario in intero, basta riconvertirlo e sottrarvi $B$.

###### IEEE 754

Nella rappresentazione a virgola mobile [[9 - Rappresentazione di decimali#Standard IEEE 754|IEEE 754]], $B$ assume valore costante, tipo:

- **127** per rappresentazione su <u>8 bit</u> (singola precisione),
- **1023** per rappresentazioni a <u>11 bit</u> (doppia precisione).

##### Rappresentazione in codice eccesso $2^{N-1}$

Questo caso particolare di notazione polarizzata a $N$ bit permette di riservare:

- Le codifiche da $0$ a $2^{N-1} - 1$ per i numeri **positivi**,
- Le codifiche da $-1$ a $-2^{N-1}$ per i numeri **negativi**.

In pratica si realizza sommando al numero da codificare un eccesso corrispondente a $2^{N-1}$, così da riuscire a rappresentare sia numeri negativi che positivi (similmente al [[#Complemento a 2|Cp2]]).

Dopo che il numero + $2^{N-1}$ è stato convertito in binario, è possibile tornare all'originale riconvertendolo in decimale e sottraendogli $2^{N-1}$.

È più semplice capire visualizzando un esempio sottoforma di tabella (in questo caso con $N = 3$):

![](https://i.imgur.com/AMo0NfL.png)

###### Esempio codice eccesso $2^{N-1}$

Convertire -1, con $N = 3$:

$-1 + 2^{3-1} = 3 = 011$

Al contrario: $011 = 3 \;\rightarrow\; 3 - 2^{3-1} = -1$

# Esercizi

TODO

![](https://i.imgur.com/WEf5KgA.png)

# Soluzioni

---

Prossima lezione: [[9 - Rappresentazione di decimali]]

