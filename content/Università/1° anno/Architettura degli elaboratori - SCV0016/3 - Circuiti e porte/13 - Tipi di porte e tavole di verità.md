# Lezione 13

### Porte e tavole di verità

> [!important] Tavole di verità
> Per capire cosa fanno le funzioni logiche, il metodo migliore è ***tabellarle***, quindi per capire cosa fa una funzione logica $f(x_{1}, x_{2}...)$ se ne costruisce la **tavola di verità**, riportandovi, per le variabili in colonna, tutte le combinazioni possibili che esse possono assumere e che risultato dà la funzione logica nella colonna dell'output.

###### Velocità delle porte

> [!info] Tempo di commutazione
> Il **tempo di commutazione** di una porta è il tempo che essa ci mette dato un input a realizzare la sua funzione logica e restituire l'output.

##### Porta NOT

(O invertitore/negatore) ogni valore in ingresso è invertito:

###### Simbolo

![](https://i.imgur.com/YuqOAJU.png)

![](https://i.imgur.com/TPas7PT.png)

###### Tavola di verità

![](https://i.imgur.com/nq5hb3l.png)

##### Porta AND

L'uscita vale 1 se e solo se entrambi gli ingressi sono posti ad 1:

###### Simbolo

![](https://i.imgur.com/d75LQWL.png)

###### Tavola di verità

![](https://i.imgur.com/DmLgnG5.png)

##### Porta OR

L'uscita vale 1 a condizione che 1 dei 2 ingressi abbia valore 1:

###### Simbolo

![](https://i.imgur.com/A0qZVxF.png)

###### Tavola di verità

![](https://i.imgur.com/JUt5se0.png)

##### Porta XOR

(Detto anche OR esclusivo), l'uscita è 1 solo se 1 ingresso è positivo e l'altro è negativo:

###### Simbolo

![](https://i.imgur.com/ijqggkY.png)

###### Tavola di verità

![](https://i.imgur.com/iKdD2WC.png)

##### Porta NAND

###### Simbolo

![](https://i.imgur.com/BX5xjGZ.png)

###### Tavola di verità

![](https://i.imgur.com/SaRnZMa.png)

##### Porta NOR

###### Simbolo

![](https://i.imgur.com/NgLb85x.png)

###### Tavola di verità

![](https://i.imgur.com/LeO7vRe.png)

##### Porta XNOR o NXOR

###### Simbolo

![](https://i.imgur.com/NAUhijr.png)

###### Tavola di verità

![](https://i.imgur.com/W6ipsXd.png)

#### Generalizzare le porte

Alcuni tipi di porte a 2 ingressi si possono generalizzare a 3, 4... AND e OR sono le più usate e si usano a 2, 4 o 8 ingressi (raramente di più).

###### AND a 3 ingressi

![](https://i.imgur.com/QXfu2EZ.png)

![](https://i.imgur.com/cmmrhxx.png)

![](https://i.imgur.com/6wW5atL.png)

###### OR a 3 ingressi

![](https://i.imgur.com/8TGvQqQ.png)

![](https://i.imgur.com/4TzPElv.png)

(La foto che indica la coincidenza in [[#AND a 3 ingressi]] vale anche per l'OR a + ingressi).

### Particolarità di NAND e NOR

(Meglio lasciare questa parte di lezione dopo aver visto le lezioni: 14 e 15)

##### Vantaggi principali

In primis, 2 vantaggi delle porte [[#Porta NAND|NAND]] e [[#Porta NOR|NOR]]:

- Sono le porte più economiche da realizzare,
- Hanno la minore latenza tra tutte le altre porte a 2 ingressi.

##### Equivalenza e costruzione di altre porte

Notare che:

- $A$ NOR $A = \lnot{(A+A)} = \lnot{A}$
- $A$ NAND $A = \lnot{(AA)} = \lnot{A}$

> [!important] Infatti
> 1) **NOR** e **NAND** sono detti **operatori universali**,
> 2) Con sole porte **NOR/NAND** è possibile costruire le altre porte fondamentali dell'algebra booleana classica:

###### NOT

Come suddetto, le seguenti porte sono **equivalenti**:

![](https://i.imgur.com/hv5XFaz.png)

###### AND

Avendo a disposizione **2 NAND**, 1 la si può usare come <u>NOT</u> per <u>negare la NAND iniziale</u>, così da ottenere una **AND**:

![](https://i.imgur.com/4JJDYTP.png)

Infatti: $A$ AND $B = \lnot{}(A$ NAND $B)$

(Si può ottenere un AND anche sostituendo delle NOR alle NAND della rete di esempio in [[#OR]]).

###### OR

Avendo a disposizione **3 NAND**, è possibile costruire una porta **OR** grazie alle leggi di De Morgan:

![](https://i.imgur.com/e0hlqZU.png)

Infatti: $A$ OR ${} B = \lnot{}(\lnot{A}$ AND $\lnot{B}) = (\lnot{A})$ NAND $(\lnot{B)}$

(Si può ottenere un OR anche sostituendo delle NOR alle NAND della rete di esempio in [[#AND]]).

# Esercizi

###### 1) Funzione custom

# Soluzioni

---

Prossima lezione: [[14 - Algebra di Boole]]

