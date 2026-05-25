# Lezione 23

### Half adder

L'*half adder* (**HA** o **semisommatore**) permette il calcolo della somma con riporto di 2 bit (2 numeri binari a 1 bit):

**Ingressi**: 2

**Uscite**: 1 (somma) + 1 (*carry*, ovvero il riporto)

![](https://i.imgur.com/HJg5DZ9.png)

![](https://i.imgur.com/w0kCUjY.png)

### Full adder

Il *full adder* (**FA** o **sommatore**) è un blocco funzionale composto da 2 **HA** che esegue la somma tra i 2 bit + il loro (eventuale) riporto:

**Ingressi**: 3 ($A$, $B$ e $C_{in}$ o *carry in*, il riporto da sommare al risultato)

**Uscite**: 1 (somma) + 1 ($C_{out}$ o *carry out*, il riporto finale)

![](https://i.imgur.com/QqeB4c0.png)

![](https://i.imgur.com/V53c0Yt.png)

![](https://i.imgur.com/1B7cw3p.png)

$S = A \oplus B \oplus C_{in}$

$C_{out} = AB + C_{in}(A \oplus B)$

##### FA a n bit

Per creare dei sommatori a *n* bit è necessario che:

- Ogni gruppo di input ($A$ e $B$) abbia *n* ingressi (di cui 1 rispettivamente per ogni FA a 1 bit),
- Il $C_{in}$ del 1° FA sia 0,
- Il $C_{out}$ del 1° FA diventi il $C_{in}$ del secondo e così via.

Il $C_{out}$ dell'ultimo FA a 1 bit sarà il $C_{out}$ effettivo (il riporto finale), mentre gli output di somma di ogni sommatore corrisponderanno al risultato (in binario):

![](https://i.imgur.com/oddQQrd.png)

###### Overflow

C'è il rischio che sommare 2 numeri porti ad **overflow**, come in questo caso:

![](https://i.imgur.com/PkRmF7y.png)

Si può notare come l'output in $C_{out}$, se posto a 1, indica che c'è stato un overflow.

###### CP2

Seppur il funzionamento del blocco funzionale rimane immutato, la situazione può cambiare se si usano degli interi in CP2:

![](https://i.imgur.com/QJaEEuT.png)

Infatti, mentre l'operazione viene eseguita normalmente:

- L'output in $C_{out}$ è qui ignorabile,
- Vi è overflow solo se: $A_{n-1} = B_{n-1} \neq S_{n-1}$ (dove $X_{n-1}$ è l'MSB di $A$, $B$ e $S$).

##### Esempio

Progettare un circuito digitale combinatorio con:

- **Input**: 2 numeri binari naturali $A$ e $B$ da *n* bit e un segnale di comando $C$ da 1 bit,
- **Output**: 1 numero binario naturale $Z$ da *n* bit tale che:
  - Se $C = 0 \;\rightarrow\; Z = A + B$,
  - Se $C = 1 \;\rightarrow\; Z = A - B$.
- Si trascurino inoltre i **riporti**.

###### Ipotesi 1

Consideriamo un paio di cose:

- L'obiettivo è fare una somma, quindi il blocco finale sarà un sommatore,
- Dato che $A$ rimane sempre positivo, non ha bisogno di trasformazioni, quindi viene immesso come input diretto del sommatore finale,
- Per quanto riguarda $B$, in base al segnale di controllo $C$, bisogna scegliere se il suo valore sarà positivo o negativo; perciò bisognerà usare un MUX:

![](https://i.imgur.com/oGVVeIe.png)

###### Ipotesi 2

Il problema principale è il blocco che cambia di segno $B$ per rendere il suo valore in CP2. Se ci ricordiamo che per fare il **CP2** di un binario basta <u>invertirne i bit ed aggiungere 1</u>, allora si può ipotizzare una soluzione del genere:

![](https://i.imgur.com/QrQvhYv.png)

###### Ipotesi 3

Siccome non ci sono regole scritte che permettono notare sprechi e inefficienze nei circuiti, bisogna accorgersene da soli; infatti (aldilà della porta NOT usata per invertire B) stiamo sprecando in sommatore solo per aggiungere un 1.

Quindi ragionando: dobbiamo aggiungere 1 (per l'inversione e fare il CP2) solo se $C = 1$; inoltre abbiamo già un sommatore il cui $C_{in}$ è 0.

Quindi il circuito più ottimizzato risultante è:

![](https://i.imgur.com/leNUpLz.png)

# Esercizi

###### Circuito che ritorna 1 in caso di overflow in CP2

# Soluzioni

---

Prossima lezione: [[24 - Shifters]]

