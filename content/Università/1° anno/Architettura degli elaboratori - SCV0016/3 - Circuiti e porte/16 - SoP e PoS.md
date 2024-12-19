# Lezione 16

### Tecniche di sintesi di reti combinatorie

Esistono 2 tecniche universali per il passaggio <u>da tavole di verità alle rispettive reti combinatorie</u>:

#### Sum of Products

La sintesi come ***Sum of Products*** (detta anche *1a forma canonica*) ha in:

- **Input**: la <u>tavola di verità</u> della funzione,
- **Output**: una <u>somma di prodotti</u>, ovvero un'espressione booleana del tipo $XXXX + YYYY + ZZZZ$ (dove ogni addendo è un prodotto con un certo n° di fattori).

> [!important] Quando usarla
> È ideale risolvere con ***SoP*** quando nella colonna di output della tavola di verità sono presenti meno "1" che "0".

##### Procedimento

<u>Per ogni 1 nella colonna output della tavola di verità, costruire un addendo come prodotto di tutti i parametri</u> (tipo con $A = 1$ e $B = 0$, si scriverà ${} A\lnot{B}$ come prodotto che forma l'addendo).

Il passo finale per ottenere l'espressione è l'eventuale semplificazione in base alle regole di riscrittura.

###### Esempio

Data la seguente tavola di verità:

![](https://i.imgur.com/ujVwV1m.png)

Si vede come solo le combinazioni di parametri che danno 1 sono cerchiate, infatti la funzione logica risultante sarà:

$$F(A,B) = \lnot{A}\lnot{B} + \lnot{A}B + AB$$

#### Product of sums

La sintesi come ***Product of Sums*** (detta anche *2a forma canonica*) ha in:

- **Input**: la <u>tavola di verità</u> della funzione,
- **Output**: un <u>prodotto di somme</u>, ovvero un'espressione booleana del tipo $(A+B)(C+D)$ (dove ogni fattore è una somma con un certo n° di addendi).

> [!important] Quando usarla
> È ideale risolvere con ***PoS*** quando nella colonna di output della tavola di verità sono presenti meno "0" che "1".

##### Procedimento

<u>Per ogni 0 nella colonna output della tavola di verità, costruire un fattore come somma di tutti i parametri</u> (tipo con $A = 1$ e $B = 0$, si scriverà $A+\lnot{B}$ come somma che forma il fattore).

### Disegno dello schema di rete

Dopo aver trovato (ed eventualmente semplificato) l'espressione booleana, per risolvere completamente gli esercizi, bisogna implementare l'espressione ottenuta <u>disegnando lo schema logico della rete corrispondente</u>:

##### Per SoP

1) Si disegnano 2 linee orizzontali/verticali per ogni parametro, una normale ed una negata:

   ![](https://i.imgur.com/IcX2M9J.png),

2) Si disegna, per ogni addendo, una porta AND (moltiplicazione) connessa alla rispettiva linea di ogni fattore dell'addendo stesso:

   ![](https://i.imgur.com/RQI0s1P.png),

3) Gli output delle porte AND di tutti i parametri dovranno essere gli input di un'unica grande OR, il cui output sarà il risultato della funzione:

   ![](https://i.imgur.com/5PnToCA.png).

##### Per PoS

# Esercizi

### SoP

##### Funzione maggioranza

Sintetizzare in 1a forma canonica una funzione con 3 ingressi A, B e C ed un output F così definita: "se la maggioranza degli input = 0, l'output = 0, altrimenti se la maggioranza degli input = 1, l'output = 1".

### PoS

# Soluzioni

### SoP

##### Funzione maggioranza

###### 1) Tavola di verità

![](https://i.imgur.com/RgRLvLu.png)

###### 2) Sintesi dell'espressione

![](https://i.imgur.com/DmHrsvE.png)

Il che si traduce nella seguente *SoP*:

$$F(A,B,C) = \lnot{A}BC + A\lnot{B}C + AB\lnot{C} + ABC$$

###### 3) Implementazione dell'espressione in un circuito

![](https://i.imgur.com/5PnToCA.png)

### PoS

##### ?

###### 1) Tavola di verità

###### 2) Sintesi dell'espressione

###### 3) Implementazione dell'espressione in un circuito

---

Prossima lezione: [[17 - Semplificazione di espressioni booleane]]

