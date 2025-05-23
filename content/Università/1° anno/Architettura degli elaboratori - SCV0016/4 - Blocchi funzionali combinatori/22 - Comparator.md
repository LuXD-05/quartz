# Lezione 22

### Comparator

Il ***comparator*** (**COMP**) è un blocco funzionale che **confronta 2 numeri binari** $A$ e $B$ **a *n* bit** presenti sui suoi 2 gruppi di *n* ingressi e **attiva** (pone a 1) l'**uscita corrispondente all'esito della comparazione** (<u>azzerando le altre</u> = a condizioni false).

**Ingressi**: 2 gruppi di *n* ingressi (per rappresentare 2 numeri binari) in base ai bit

**Uscite**: 3 ($A > B$,   $A = B$,   $A < B$)

###### Comparator a 2 bit

![](https://i.imgur.com/hAVbzhj.png)

![](https://i.imgur.com/oaWRlY5.png)

###### K-map caso A < B

![](https://i.imgur.com/LkNxLw5.png)

###### K-map caso A = B

![](https://i.imgur.com/nE8TOfQ.png)

$A=B \,=\, \not\;(A1 \oplus B1)\not\;(A0 \oplus B0)$

###### K-map caso A > B

![](https://i.imgur.com/d5HUJgX.png)

$A>B \,=\, \not\;(A<B)\not\;(A=B)$

###### Possibile implementazione

![](https://i.imgur.com/ityravK.png)

###### Comparator a 4 bit

Realizzandolo con comparator a 2 bit:

![](https://i.imgur.com/sO0xElc.png)

Quindi, è chiaro come è possibile costruire comparator per $2^{n}$ bit con 2 comparator da *n* bit:

- 2 comparator da 2 bit = 1 comparator da 4 bit,
- 2 comparator da 4 bit = 1 comparator da 1 byte,
- 2 comparator da 8 bit = 1 comparator da 2 byte (short),
- 2 comparator da 16 bit = 1 comparator da 4 byte (int).

# Esercizi

###### 1) Realizzazione di un comparator in CP2

Realizzare un comparator tra numeri di 3 bit in CP2.

# Soluzioni

---

Prossima lezione: [[23 - HA e FA]]

