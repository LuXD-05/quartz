# Lezione 28

##### Latch SR

Il [[27 - SR Latch#Latch SR|latch SR]] ha 2 ingressi $S$ (*Set*) e $R$ (*Reset*) che non solo hanno 2 funzioni:

- Indicano che l'<u>azione da eseguire</u> è la **memorizzazione di un dato**,
- <u>Definiscono quale valore</u> (del dato) <u>memorizzare</u> (**1 o 0**).

### Gated D-Latch

In certi casi potrebbe essere meglio separare le 2 funzioni di "scelta dell'azione" e "definizione del valore"; e il blocco che realizza tale comportamento è il ***gated D-latch***.

Un ***gated D-latch***, è un particolare tipo di blocco funzionale sequenziale che agisce come un [[27 - SR Latch#Latch SR|latch SR]] (infatti lo implementa), solo che i 2 ingressi hanno le 2 funzioni separate.

**Ingressi**: 2 ($D$ e $E$, detti canali "***Data***" e "***Enable***")

- $D$: indica quale valore memorizzare (1 o 0).
- $E$ (detto *gate*): se posto a 1, il valore in $D$ viene memorizzato, altrimenti no.

**Uscite**: 2 ($Q$ e $\overset{\_}{Q}$)

![](https://i.imgur.com/ScEFtzd.png)

Si dice che il D-latch è ***trasparente*** perché l'input $D$ si vede da $Q$.

##### Funzionamento

Come per il [[27 - SR Latch#Latch SR|latch SR]], anche nel gated D-latch si gestiscono 2 input, solo che questi hanno 2 funzioni diverse:

- $D$ è sempre acceso o sempre spento, il che equivale rispettivamente ad inserire un segnale nel $S$ (*Set*) o nel $R$ (*Reset*),
- $E$ invece "abilita" il segnale di $D$ quando posta a 1; infatti:
  - Se $E = 0$ il D-latch è ***congelato***, ovvero il bistabile mantiene il suo stato indipendentemente da $D$,
  - Se $E = 1$ (per qualche nanosecondo) il D-latch assume in output il valore di $D$.

> [!info] Nota
> Questo impedisce che l'input "*illegale*" $S = R = 1$ venga fornito al latch SR interno.

###### Quindi

Quando $E=0$ (***frozen** D-latch*) si legge il valore memorizzato nel D-latch, mentre quando $E=1$ (***transparent** D-latch*) viene scritto nel D-latch il valore di $D$.

# Esercizi

# Soluzioni

---

Prossima lezione: [[29 - Clock e sincronizzazione sul livello]]

