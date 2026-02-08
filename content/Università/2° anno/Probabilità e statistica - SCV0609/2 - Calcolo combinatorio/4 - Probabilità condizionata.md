# Lezione 4

### Probabilità condizionata

La probabilità condizionata di un evento $A$ dato un altro $B$ è la probabilità che $A$ si verifichi quando si sa che anche $B$ si è verificato ($A$ dipende da $B$):

$${} P(A|B) = \dfrac{P(A \cap B)}{P(B)} {}$$

###### Teorema delle probabilità totali

Quando si vuole trovare la probabilità di un evento $A$ in base ad altri eventi, si usa il **teorema delle probabilità totali**:

$${\color{yellow}{P(A)}} = P(A|B) \cdot P(B) + P(A|B^{c}) \cdot P(B^{c})$$

(Con il complementare si intende l'evento contrario).

> [!important] Quando si usa
> Il teorema delle probabilità totali si usa quando ci sono vari eventi (cause) e si vuole trovare la probabilità di un certo evento (effetto) basato su essi (su una sorta di "intersezione" fra loro); in pratica quando è richiesto di calcolare la probabilità di un evento che dipende da altri in un certo modo.

##### Teorema di Bayes

Quando si ha la probabilità di un evento scaturito da altri (a posteriori) e si vuole trovare la probabilità dell'evento che lo ha generato (anteriore), si usa il **teorema di Bayes**: 

$$P(B|A) = \dfrac{P(A|B) \cdot P(B)}{{\color{yellow}{P(A)}}}$$

In caso il denominatore non sia noto, è possibile ricavarlo col [[#Teorema delle probabilità totali|teorema delle probabilità totali]].

> [!important] Quando si usa
> Il teorema di Bayes si usa quando, dato un certo evento (effetto), si vuole risalire a quale causa (evento o intersezione di eventi) lo ha scaturito; quindi di solito quando si ha un evento-effetto e si vuole verificare la probabilità che sia scaturito da un certo evento-causa.

---

Prossima lezione: [[5 - Random variables]]

