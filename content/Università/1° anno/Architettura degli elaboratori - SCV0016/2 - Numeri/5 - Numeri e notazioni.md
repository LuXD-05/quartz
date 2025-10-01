# Lezione 5

### Livello logico

##### Numeri

Esistono diversi tipi di rappresentazione degli <u>interi non negativi</u>:

- **Notazioni additive**: tipo per i <u>numeri romani</u>, dove ogni simbolo ha valore fisso e i loro valori si sommano a meno ché il valore di uno non preceda un simbolo con valore maggiore (in quel caso si sottrae),
- **Notazioni posizionali**: dove il valore di un simbolo è determinato in base alla sua posizione, con formula: 

  $$n_{0}*B^{0} \;+\; n_{1}*B^{1} \;...\; n_{k}*B^{k}$$

  In questa le cifre ($n$, che assumono valori da $0$ a $B-1$) acquistano **significatività** da destra a sinistra per ogni **posizione** (in formula: $n_{?}$ = numero, $B^{?}$ = base elevata a una potenza in base alla sua posizione).

##### Notazioni

Di seguito sono riportate alcune tra le notazioni più importanti ed usate:

###### Decimale

> [!important] Notazione decimale
> La **notazione decimale** è una notazione posizionale avente base 10, pertanto la formula precedente diventa:

$n_{0}10^{0} + n_{1}10^{1} \;...\; n_{k}10^{k}$

I valori che $n$ può assumere sono (dato $n = \{0 \;...\; B-1\}$) $\;\rightarrow\;$ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

###### Binaria

> [!important] Notazione binaria
> La notazione binaria invece ha base 2, quindi si ha:
> $n_{0}2^{0} + n_{1}2^{1} \;...\; n_{k}2^{k}$
> I valori che $n$ può assumere sono (dato $n = \{0 \;...\; B-1\}$) $\;\rightarrow\;$ 0, 1

###### Esadecimale

> [!important] Notazione esadecimale
> La notazione esadecimale invece ha base 16, quindi si ha:
> $n_{0}2^{0} + n_{1}2^{1} \;...\; n_{k}2^{k}$
> I valori che $n$ può assumere sono (dato $n = \{0 \;...\; B-1\}$) $\;\rightarrow\;$ 0, 1
> **ATTENZIONE**: per non confondersi (dato che la notazione esadecimale per rappresentare i numeri da 10 a 15 usa le lettere dalla A alla F) solitamente i numeri esadecimali sono preceduti dalla sequenza di caratteri "**0x**".

---

Prossima lezione: [[6 - Conversioni]]

