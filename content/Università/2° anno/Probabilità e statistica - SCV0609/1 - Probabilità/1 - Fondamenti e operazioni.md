# Lezione 1

### Esperimenti aleatori

Un esperimento aleatorio può avere diversi esiti ma può concludersi con 1 solo di essi. Alcune definizioni:

###### Spazio campionario

Lo **spazio campionario** di un esperimento è l'insieme di tutti i suoi possibili <u>esiti</u> (non necessariamente finiti) e si indica così:

$$\Omega = \{\omega_{1}, \;\ldots\; \omega_{n}\}$$

(Gli $\omega$ singoli invece indicano i singoli **esiti** dell'esperimento).

Esempio: l'esperimento di lancio della moneta ha 2 esiti: testa o croce (senza considerare altri casi particolari).

###### Evento

Un **evento** è un <u>insieme di esiti</u> che è anche un <u>sottoinsieme</u> di $\Omega$ e del quale se ne può calcolare la probabilità:

$$E = \{\omega_{1},\;\omega_{2},\;\omega_{3}\}$$

Ogni evento non contiene necessariamente più esiti, anche 1 solo. Nota: uno spazio campione con $n$ esiti genera $2^{n}$ eventi possibili (compreso $\emptyset$ e 1 evento con ogni esito).

Dato un evento $E$ esiste anche il suo evento contrario indicato con $\overline{E}$.

Esempio: del lancio della moneta, un evento potrebbe essere che "viene lanciata la moneta ed esce testa" (e la sua probabilità sul suo $\Omega$ è $\frac{1}{2}$).

##### Probabilità

La **probabilità** $P$ di un evento $E$ è indicata dal <u>rapporto tra il n° di esiti di un evento</u> (detti <u>casi favorevoli</u> $\#\omega$) e il <u>n° totale di esiti dello spazio campionario</u> ${} \Omega$ (detti <u>casi totali</u>, che indichiamo con $N$).

$$P(E) = \dfrac{\#\omega}{N}$$

Nel caso in cui $N$ tende a $\infty$ la probabilità si avvicina sempre di più a 0.

$$P(E) = \lim_{N \rightarrow \infty} \dfrac{\#\omega}{N}$$

La probabilità di un evento contrario $\overline{E}$ invece corrisponde a:

$$P(\overline{E}) = 1 -  \dfrac{\#\omega}{N}$$

---

Prossima lezione: [[2 - Operazioni insiemistiche su eventi]]

