# Lezione 24

#### Estensioni numeriche

Si può estendere la rappresentazione di un numero da *n* bit a *m* bit usando un circuito detto **EXT**.

##### Estensione con 0

È possibile estendere un numero intero aggiungendo zeri a sinistra dello stesso, infatti:

$11011_{2} = 27$

$00011011_{2} = 27$

![](https://i.imgur.com/HawloHo.png)

![](https://i.imgur.com/BnT5TYz.png)

##### Estensione in segno

La questione cambia per i numeri in **CP2** coi quali, per estendere il numero:

- Se l'MSB è **0**, aggiungere "0" a sinistra del numero ($0101 = 0000101 = +5$),
- Se l'MSB è **1**, aggiungere "1" a sinistra del numero ($1101 = 111101 = -3$).

![](https://i.imgur.com/x4TK7It.png)

![](https://i.imgur.com/VsJNJnQ.png)

###### Estensione a scelta

Con un semplice ingresso di selezione aggiuntivo (gestito da un [[21 - Multiplexer|MUX]]) è possibile scegliere se estendere con 0 o in segno.

![](https://i.imgur.com/bzxoBSm.png)

![](https://i.imgur.com/l4suIEi.png)

### Shifters

##### Left shifter

Il ***left shifter*** ($<<$) è un blocco funzionale che permette di **spostare a sinistra** (<u>di un certo numero di cifre</u>) **un numero binario**.

(foto <<)

Lo *shift* a sinistra di *n* cifre, comporta sempre la **moltiplicazione del numero shiftato** per $2^{n}$; e ciò vale:

- Sia per <u>binari puri</u>:

  ![](https://i.imgur.com/kEOw7pU.jpeg)

- Sia per <u>binari in CP2</u>:

  ![](https://i.imgur.com/5Q3q62l.jpeg)

###### Overflow

Moltiplicare un numero per una potenza di 2 potrebbe comunque generare overflow, perciò per rilevarlo si realizza un blocco funzionale con un output "overflow" posto a 1 se c'è overflow:

...

Inoltre:

- **Sommando** 2 numeri a *n* cifre, si ottiene al max un numero a ${} n+1$ cifre:

  ![](https://i.imgur.com/gsqdRzN.png)

- **Moltiplicando** 2 numeri a *n* cifre, si ottiene al max un numero a $2n$ cifre:

  ![](https://i.imgur.com/O2QPURU.png)

###### Parametrizzazione

Il $<<$ è parametrizzabile, ovvero è possibile usare un [[25 - ALU|MUX]] con *k* ingressi di selezione (in questo caso 2) per scegliere di quante cifre "*shiftare*" (da 0 a $2^{k} - 1$) il numero binario in input:

![](https://i.imgur.com/a7NrAve.png)

##### Right shifter

Il ***right shifter*** ($>>$) è un blocco funzionale che permette di **spostare a destra** (<u>di un certo numero di cifre</u>) **un numero binario**.

(foto $>>$)

Lo *shift* a destra di *n* cifre, comporta sempre la **divisione del numero shiftato** per $2^{n}$ (con approssimazione per difetto per numeri dispari) e, come per gli estensori, aggiunta a sinistra di "0" se l'MSB = 0 e di "1" se l'MSB = 1; e ciò vale:

- Sia per i <u>binari puri</u>:

  ![](https://i.imgur.com/JotkmuV.jpeg)

- Sia per i <u>binari in CP2</u>:

  ![](https://i.imgur.com/l7EIa25.jpeg)

#### Moltiplicazione

Shiftando a sinistra per 0 bit si ha un **MUL** che moltiplica un numero per 0 o 1 (quindi che ritorna o 0 o il numero stesso):

![](https://i.imgur.com/92Yw79V.png)

##### MUL a *n* bit

Per eseguire moltiplicazioni a *n* bit (per esempio 5), come:

![](https://i.imgur.com/0BzqbwY.png)

Si combinano *n* MUL a 1 bit, seguiti da [[#Estensioni numeriche|EXT]], poi da [[#Left shifter|<<]] da 0 a $n-1$ e infine da dei [[23 - HA e FA#Full adder|FA]].

![](https://i.imgur.com/38HcuHS.png)

###### MUL in pratica

Per il possibile [[#Overflow|overflow]] della moltiplicazione di 2 numeri a *n* bit, data la poca praticità di rappresentare il risultato con più di *n* bit, generalmente si usano <u>2 variabili</u> per memorizzare il risultato:

- **HIGH**: gli *n* bit <u>più significativi</u>,
- **LOW**: gli *n* bit <u>meno significativi</u>.

![](https://i.imgur.com/52FgNCX.png)

![](https://i.imgur.com/SyDUKzx.png)

# Esercizi

# Soluzioni

---

Prossima lezione: [[25 - ALU]]

