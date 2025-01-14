# Lezione 9

### Numeri binari frazionari

I numeri non interi in basi diverse dalla 10 si rappresentano sempre allo stesso modo: separando la parte intera da quella decimale con un punto. Inoltre:

- I valori **prima** del punto verranno moltiplicati per la base elevata ad una <u>potenza</u> della base = alla posizione della cifra dal punto,
- I valori decimali **dopo** il punto, verranno moltiplicati per la base elevata ad una <u>potenza negativa</u> della base = alla posizione della cifra dal punto.

##### Calcolare la parte decimale di una base

###### Metodo 1

Prendiamo il numero 101.1001

- Calcolare l'intero è semplice: 101 = 5
- Per la parte decimale bisognerebbe fare: $1 * 2^{-1} + 0 * 2^{-2} + 0 * 2^{-3} + 1 * 2^{-4}$

###### Metodo 2

Per renderlo più semplice, è necessario fare così:

1) Considerare la parte decimale come se fosse intera e convertirla alla base di destinazione,
2) Dividere il numero ottenuto per la base iniziale elevata al n° di cifre che compongono la parte decimale.

In questo caso si avrebbe: 1001 = 9 --> 9 / 2^4, il che è = 0,5625.

##### Numero binario tra 0 e 1

Un numero binario tra 0 e 1 si esprime esattamente come un numero binario normale, solo che l'MSB pesa 2^-1, il seguente 2^-2 e cosi via.

###### Conversione da decimale a binario di numeri frazionari

Per convertire un numero frazionario da decimale a binario si usa l'**algoritmo delle moltiplicazioni successive**:

1) Si raddoppia la parte frazionaria del numero (quella tra 0 e 1) preceduta da "$0,$",
2) Ci si segna la parte intera ottenuta (tranne la 1a, corrispondente al 1° valore intero) e si riprende a raddoppiare sempre solo le parti decimali,
3) Si continua a raddoppiare finché o si arriva a 0,00 oppure fin quando  è necessario per l'approssimazione.

Esempio:

![](https://i.imgur.com/dyI3Bsz.png)

> [!info] Attenzione
> Come esistono numeri periodici in base 10, anche in base 2 alcuni numeri (non necessariamente periodici in base 10) sono **periodici**, come si vede nel suddetto esempio.

### Approssimazione

Ci sono 2 tecniche scrivere dei numeri frazionari con infinite cifre decimali come se fossero (per cosi dire) "finiti":

- **Troncamento**: si ignorano tutte le cifre dopo una specifica (*k*),
- **Arrotondamento**: come prima ma la cifra scelta (*k*?) è arrotondata per eccesso o per difetto per minimizzare l'errore. Questo:
  - Dipende solo dalla 1a cifra scartata (la (k+1)-esima), (base 10: 0-4 = difetto / 5-9 = eccesso | base 2: 0 = difetto | 1 = eccesso)

##### Numeri frazionari in virgola fissa

Per rappresentare un numero frazionario con *k+h* bit (k = bit interi, h = bit decimali):

- Convertirlo in base 2,
- Arrotondare ad *h* le cifre della parte decimale,
- Memorizzare la parte intera in *k* bit e la parte dopo la virgola in *h* bit (cosicché il totale dei bit usati sia *k+h*)

Comunque, essi vengono trattati e rappresentati come interi; l'unica differenza è nella loro interpretazione e dipende dalla posizione della virgola.

###### Proprietà

Limiti: 

- Max numero esprimibile: $2^{k}-1\;+$ quasi 1 = quasi $2^{k}$,
- Min numero esprimibile > 0:  $2^{-h}$ (numeri <  sono arrotondati a 0).

###### Esempio 1

Vogliamo rappresentare 6,125 in 8 bit, con k = 4 e h = 4 (4 bit per parte intera e 4 per parte decimale)

/,125 (0 intero)

0,25

0,5

1,0

0110|0010 --> ci sta --> 110.001

###### Esempio 2

Vogliamo rappresentare 6,225 in 8 bit, con k = 4 e h = 4 (4 bit per parte intera e 4 per parte decimale)

/,225 (0 intero)

0,450

0,9

1,8

1,6

1,2

0,4

...

0110|001110... --> NON ci sta, quindi

- O si tronca: 0110.0011
- O si arrotonda (in questo caso x eccesso): 0110.0100

Per trovare quale tra i 2 metodi è il migliore, semplicemente confrontare il valore approssimato con quello da rappresentare (> parte delle volte vince arrotondamento).

### Numeri reali

I reali sono nell'intervallo ($+\infty ... -\infty$) le grandezze usate sono molto grandi/piccole, nell'ordine di circa $10^{30} - 10^{-30}$.

Siccome non c'è bisogno di tanta precisione per numeri di così alto ordine, si usa la notazione scientifica:$$v = n,d \times 10^{e}$$Dove: 

- v = valore,
- n = parte intera,
- d = parte decimale,
- n,d = mantissa,
- e = esponente.

##### Notazione scientifica in forma normalizzata

La **forma normalizzata** prevede che la mantissa sia: $0 < mantissa < 10$ (0 e 10 esclusi), cosicché la parte intera della mantissa sia <u>una cifra sola</u> (non 0), mentre l'esponente è detto "*ordine di grandezza*". Questo è fondamentale per rendere semplice il confronto tra numeri reali in forma scientifica.

###### Limiti di rappresentazione

Dato che l'insieme $\mathbb{R}$ è **denso**, esistono numeri aventi cifre decimali infinite i quali non sono interamente rappresentabili con valori limitati di mantissa ed esponente; è per questo che si ricorre all'**approssimazione**.

#### Forma normalizzata binaria

I reali possono essere anche rappresentati anche in <u>notazione scientifica in base 2</u>: $N = x * 2^{E}$.

Sia mantissa ($x$) che esponente ($E$) hanno un <u>segno</u> e:

- La **mantissa** è espressa in <u>modulo e segno</u>,
- L'**esponente** è espresso in generale in <u>notazione polarizzata</u>.

La rappresentazione nei pc è a **virgola mobile**, per cui <u>spostarla a destra o a sinistra</u> corrisponde (rispettivamente) a <u>decrementare o incrementare l'esponente</u> (in notazione scientifica).

![](https://i.imgur.com/lFM3B9A.png)

Proprio come nella forma normalizzata decimale la mantissa è <u>tra 0 e 10 esclusi</u> (eccetto per rappresentare lo 0 stesso), qui la **mantissa** è <u>tra 0 e 2 esclusi</u>, perciò vale sempre 1:

![](https://i.imgur.com/GbhxtZj.png)

##### Standard IEEE 754

Lo **standard IEEE 754** è universalmente adottato per la rappresentazione dei numeri *floating point*, e definisce 2 formati:

- Numeri a **singola precisione** (32 bit), detti ***float*** (esponente 8 bit $\rightarrow$ <u>bias = 127</u> $\rightarrow$ range polarizzazione da -126...127 | -127 perché il 1° bit frazionario è il <u>segno</u> dell'esponente):

  ![](https://i.imgur.com/5CvLmXI.png)

- Numeri a **doppia precisione** (64 bit), detti ***double*** (esponente 11 bit $\rightarrow$ <u>bias = 1023</u> $\rightarrow$ range polarizzazione da -1022...1023 | -1022 perché il 1° bit frazionario è il <u>segno</u> dell'esponente):

  ![](https://i.imgur.com/JyN8gHB.png)

Per entrambi, il **bit di segno** è <u>0 per i positivi</u> e <u>1 per i negativi</u>.

Lo standard, oltre alla rappresentazione normalizzata, prevede altre 4 rappresentazioni:

![](https://i.imgur.com/1ClQicz.png)

> [!important] Attenzione
> Dato che la **parte intera** della mantissa è sempre <u>1</u>, di solito **si omette** e <u>si rappresenta solo la parte frazionaria</u>.

###### Da decimale a IEEE 754

###### Da IEEE 754 a decimale

###### Esempi standard IEEE 754

\1) -30,25 in formato virgola mobile IEEE 754

Segno (-) significa: MSB = 1

30 = 11110

0,25 = 01 (algoritmo delle moltiplicazioni successive)

Quindi: 11110,01

In forma normalizzata: 1,111001 \* 2^4 --> 1110010...0 \* 2^4 (dato che nn si rappresenta l'1 iniziale, la seq di zeri dopo la mantissa sono fatti per riempire la mantissa).

(deriviamo l'esponente???) 4 + 127 = 131 = 10000011

P754 = 1 10000011 11001000000000000000000

\2) dato P754 = 0 10001100 10001100000000000000000

0 = segno +

E = 2^2 + 2^3 + 2^7 = 128 + 8 + 4 - 127 = 13

M = (da sx a dx) 2^-1 + 2^-5 + 2^-6 + 2^0 (????????) = 1 + 0,5 + 1/32 + 1/64 = 1,546875 \* 2^13

\3) -5.828125 in IEEE 754

Segno - = MSB = 1

int: 5 = 101

dec: 0,828125 = 0,110101

Quindi: 101,110101 = 1,01110101... \* 2^2

E = 2 + 127 = 129 = 10000001

Quindi: 1 10000001 01110101000000000000000

###### Limiti IEEE 754

In ***float***, il numero normalizzato più piccolo ha mantissa = 1 ed esponente = -126, quindi = $2^{-126}$.

Quando un calcolo dà un risultato inferiore ad esso, prima c'erano 2 possibilità:

- Azzerare il risultato (numero talmente piccolo da essere approssimabile a 0),
- Generare un'eccezione di ***underflow*** (numero talmente piccolo da non essere rappresentabile).

Dato che entrambe queste soluzioni non erano soddisfacenti, lo standard IEEE 754 ha introdotto i **numeri denormalizzati**.

##### Numeri denormalizzati

Numeri binari in forma normalizzata che hanno:

- Sempre uno 0 a sinistra della virgola,
- L'esponente denotato da una sequenza di 0 (che per convenzione corrisponde a -126).

Il numero denormalizzato più grande ha esponente 0 e tutti 1 in mantissa e vale circa $0,999999 * 2^{-126}$ (quasi come il più piccolo normalizzato; inoltre 0,99999 è dato dalla mantissa, mentre $2^{-126}$ è convenzionale).

Il più piccolo denormalizzato ha la mantissa composta da 0 e l'LSB a  1, e il suo valore è $2^{-149}$ ($2^{-23}$ da mantissa e $2^{-126}$ convenzionale).

In pratica questi permettono una transizione morbida verso lo 0 e i valori che causano l'underflow.

Inoltre:

- Lo 0 è dato da un'apposita configurazione,
- Si può rappresentare $\infty$ con la possibilità di eseguire operazioni con esso,
- (Operazioni tipo $\infty$/$\infty$ danno ${} NaN$ (*Not a Number*)).

###### Operazioni in virgola mobile

Per somma e sottrazione:

- Si uguagliano gli esponenti,
- Si sommano le mantisse,
- Si rinormalizza la mantissa (aggiustando l'esponente per la notazione scientifica).

Per moltiplicazione e divisione:

- Si moltiplicano/dividono le mantisse,
- Si sommano/sottraggono gli esponenti,
- Si rinormalizza il risultato.

Sono più complesse delle operazioni sugli interi, ma spesso sono più ottimizzate e più comuni e utili nelle elaborazioni (eseguite di frequente). Per questo motivo, le operazioni in virgola mobile sono state utilizzate per esprimere la potenza di calcolo matematica dei calcolatori; con l'unità di misura dei FLOPS (***FLoating point OPerations per Second***), in diverse unità:

# Esercizi

###### 1) Esercizio IEEE 754

Derivare il valore decimale di $N$ rappresentato con la seguente codifica floating point IEEE 754 in singola precisione: 

$$N = 1\;10000101\;11110000000000000000000$$

###### 2) Esercizio IEEE 754

Derivare il valore decimale di $N$ rappresentato con la seguente codifica floating point IEEE 754 in singola precisione: 

$$N = 1\;10000111\;10110101110000000000000$$

###### 3) Esercizio IEEE 754

Derivare la codifica floating point IEEE 754 in singola precisione di:

$$N_{10} = -721.5625$$

# Soluzioni

###### 1) Esercizio IEEE 754

###### 2) Esercizio IEEE 754

###### 3) Esercizio IEEE 754

---

Prossima lezione: [[10 - Char]]

