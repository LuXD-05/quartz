---
modified_at: 04/10/2024 17:17:21
edited_seconds: 10
public: true
---
### Numeri binari frazionari
I numeri non interi in basi diverse dalla 10 si rappresentano sempre allo stesso modo: separando la parte intera da quella decimale con un punto. I valori a sinistra del punto verranno moltiplicati per la base elevata ad una potenza = alla posizione della cifra dal punto; esattamente come i valori decimali a destra della virgola, solo che questi verranno moltiplicati per la base elevata ad una potenza = alla posizione della cifra dal punto in negativo.
##### Calcolare la parte decimale di una base
Prendiamo il numero 101.1001
- Calcolare l'intero è semplice: 101 = 5
- Per la parte decimale bisognerebbe fare: $1 * 2^{-1} + 0 * 2^{-2} + 0 * 2^{-3} + 1 * 2^{-4}$
Per renderlo più semplice, è necessario fare così:
1) Considerare la parte decimale come se fosse intera e convertirla alla base di destinazione,
2) Dividere il numero ottenuto per la base iniziale elevata al n° di cifre che compongono la parte decimale.
In questo caso si avrebbe: 1001 = 9 --> 9 / 2^4, il che è = 0,5625.
##### Numero binario tra 0 e 1
Un numero binario tra 0 e 1 si esprime esattamente come un numero binario normale, solo che il MSB pesa 2^-1, il seguente 2^-2 e cosi via.
Formula: $v = 2^{-1}d_{k-1} + 2^{-2}d_{k-2} + ... + 2^{-k}d_{0}$
###### Conversione da decimale a binario di numeri frazionari
Raccogliendo 2^-1 si ottiene $v = 2^{-1} * (...)$
Quindi se si moltiplica v per 2, la parte intera del risultato $d_{k-1}$ corrisponderà alla 1a cifra frazionaria della rappresentazione binaria di v:
$$2v = d_{k-1} + 2^{-1}*d_{k-2} + ... + ...$$
Se 2v < 1 allora  d_k-1 = 0 (e viceversa).
Una volta noto d_k-1, il problema diventa codificare la parte frazionaria di 2v, ovvero 2v - d_k-1
si moltiplica la parte frazionaria di 2v per 2 e si vede se è < 1, reiteranddo finché non si ottiene una parte frazionaria nulla o un numero sufficiente di cifre.
###### Algoritmo delle moltiplicazioni successive
In pratica si moltiplica il numero (quello tra 0 e 1, quindi per forza 0,qualcosa) per 2 fino a quando ??? e poi si prendono le parti intere che eccedono: La 1a (del numero tra 0 e 1 originale) è lo zero, mentre le altre compongono il numero decimale. Esempio:
0,15 
0,30
0,60
1,20
0,40
0,80
1,60
1,20
0,40

(una slide)

(una slide)

##### Note matematiche
Tutti e soli i numeri razionali (frazioni) hanno sempre sviluppi che sono o **finiti** o **periodici**.ì, al contrrario degli irrazionali che hanno sviluppi infiniti e non periodici
...

### Arrotondamento
Ci sono 2 tecniche scrivere dei numeri frazionari con infinite cifre decimali come se fossero (per cosi dire) "finiti":
- **Troncamento**: si ignorano tutte le cifre dopo una specifica (*k*),
- **Arrotondamento**: come prima ma la cifra scelta (*k*?) è arrotondata per eccesso o per difetto per minimizzare l'errore. Questo:
  - Dipende solo dalla 1a cifra scartata (la (k+1)-esima), (base 10: 0-4 = difetto / 5-9 = eccesso | base 2: 0 = difetto | 1 = eccesso)
##### Numeri frazionari in virgola fissa
Per rappresentare un numero frazionario con *k+h* bit:
- Convertirlo in base 2,
- Arrotondare ad *h* le cifre della parte decimale,
- Memorizzare la parte intera in *k* bit e la parte dopo la virgola in *h* bit (cosicché il totale dei bit usati sia *k+h*)
Comunque, essi vengono trattati e rappresentati come interi; l'unica differenza è nella loro interpretazione e dipende dalla posizione della virgola.
###### Proprietà
Limiti: 
- Max numero esprimibile: $2^{k}-1 +$ quasi 1 = quasi $2^{k}$,
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
Siccome non c'è bisogno di tanta precisione per numeri di così alto ordine, si usa la notazione scientifica:
$$v = n,d \times 10^{e}$$, dove: 
- v = valore,
- n = parte intera,
- d = parte decimale,
- n,d = mantissa,
- e = esponente.
##### Notazione scientifica in forma normalizzata
La forma normalizzata prevede che la mantissa sia: $0 < mantissa < 10$ (0 e 10 esclusi), cosicché la parte intera della mantissa sia una cifra sola (non 0), mentre l'esponente è detto "ordine di grandezza". Questo è fondamentale per rendere semplice il confronto tra numeri reali in forma scientifica.
