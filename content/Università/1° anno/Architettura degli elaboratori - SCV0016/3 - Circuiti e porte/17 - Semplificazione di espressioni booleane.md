# Lezione 17

### Regole di riscrittura

Esistono varie regole che permettono la semplificazione delle espressioni:

![](https://i.imgur.com/FKwC9RH.png)

> [!info] Considerazioni
> 1) Le regole sono bidirezionali (tipo: se posso rendere $x$ = $x+x$, posso semplificare $x+x$ in $x$).
> 2) Con l'idempotenza, non importa dove nell'espressione e quante volte si sommi (in SoP) o si moltiplichi (in PoS) dei termini, perché il risultato comunque non cambia (NOTA: sembra che sommare/moltiplicare tutti i termini per uno sia una tecnica di semplificazione efficace).
> 3) Con elemento nullo togliere direttamente la parte numerica nota, mentre con l'inverso togliere direttamente le controparti opposte.

##### Ottimizzazione

Per ottimizzare/semplificare espressioni booleane basta semplicemente applicare le regole di riscrittura proposte sopra così da ridurre la lunghezza totale dell'espressione.

###### Esempio

Semplificare: $\lnot{A}BC + A\lnot{B}C + AB\lnot{C} + ABC$

1) <u>Idempotenza</u>: sommare "${} ABC$" ai termini che non lo sommano già: $\lnot{A}BC + ABC + A\lnot{B}C + ABC + AB\lnot{C} + ABC$
2) <u>Distributiva</u>: raccogliere tra le somme i termini comuni: $BC(\lnot{A}+A) + AC(\lnot{B}+B) + AB(\lnot{C}+C)$
3) <u>Inverso</u>: rimuovere gli inversi: $BC + AC + AB$
4) <u>Distributiva</u>: raccogliere: $C(A+B)+AB$

# Esercizi

# Soluzioni

---

Prossima lezione: [[18 - Il metodo di Karnaugh]]

