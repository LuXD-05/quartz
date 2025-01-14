# Lezione 3

### Tradurre da L1 a L0

Esistono 2 possibilità per tradurre le istruzioni in $L_{1}$ in istruzioni in $L_{0}$:

##### Compilazione

(Detta anche *traduzione*), in questa un apposito programma (il **compilatore**) traduce il programma $P_{L_{1}}$ scritto in $L_{1}$ in un programma $P_{L_{0}}$ scritto in $L_{0}$, il quale verrà eseguito dalla macchina $L_{0}$.

(I 2 programmi fanno la stessa cosa ma sono scritti in linguaggi diversi).

![](https://i.imgur.com/1fgS2XY.png)

###### Processo di compilazione

Il compilatore:

- Riceve in **input** un programma $P_{L_{1}}$,
- Restituisce in **output** un corrispondente $P_{L_{0}}$,
- Ha il <u>controllo solo nella 1a fase</u> (di traduzione da $P_{L_{1}}$ a $P_{L_{0}}$).

Esso **traduce in 1 volta tutte le istruzioni** del programma in $L_{1}$ in quelle di un corrispondente programma in $L_{0}$ e, una volta fatta la traduzione, non serve più (se tutto va bene).

Si può fare un compilatore da $L_{1}$ a $L_{0}$ oppure uno che fa da $L_{1}$ a $L_{x}$ (quest'ultimo è meglio solo se si ha già un compilatore da $L_{x}$ a $L_{0}$).

###### Caratteristiche della compilazione

Vantaggi:

- **Buone prestazioni**: si esegue $P_{L_{0}}$ direttamente in $L_{0}$.
- **Ottimizzazione**: durante la traduzione si può ottimizzare il codice.

Svantaggi:

- In caso di <u>modifica del codice</u> (tipo per *debugging*) è necessario **ricompilare** il programma modificato.

##### Interpretazione

Qui un apposito programma (detto **interprete**) esamina $P_{L_{1}}$ scritto in L1 e, <u>istruzione per istruzione</u>, lo traduce in $L_{0}$ e lo esegue (solitamente gli interpreti sono scritti in $L_{0}$ e parti integranti di $M_{1}$).

![](https://i.imgur.com/UHCzjYU.png)

###### Processo di interpretazione

L'interprete:

- Riceve in **input** un programma $P_{L_{1}}$,
- <u>Non</u> restituisce in **output** un programma ma <u>esegue direttamente ogni istruzione che traduce (1 per volta)</u>,
- Il controllo è <u>sempre nelle sue mani</u>.

###### Caratteristiche dell'interpretazione

Vantaggi:

- Identificando immediatamente gli errori, è possibile correggerli prima di aver tradotto tutto il programma.

Svantaggi: 

- **Prestazioni ridotte**: ogni istruzione va tradotta ogni volta che viene eseguita.

### VM

##### VM M1

Siccome scrivere una macchina "reale" che comprenda direttamente L1 è troppo complesso e costoso, si usano la compilazione e l'interpretazione per tradurre L1 e farlo comprendere a M0, permettendo quindi la creazione di una **VM M1**.

###### Problema

- **Distanza tra i livelli**: per rendere efficiente la traduzione tra L1 e L0, la <u>distanza tra i 2 linguaggi non può essere troppo grande</u> (altrimenti i programmi sarebbero poco efficienti),
- <u>Non è detto che M1 sia la soluzione desiderata</u> (potrebbe ancora essere troppo distante da un livello comprensibile da un umano).

##### VM M2

Per questo è possibile adottare lo stesso procedimento di astrazione/virtualizzazione usato per passare da M0 a M1 anche per passare da M1 a M2 capace di comprendere un linguaggio L2.

###### Traduzione di L2

Per tradurre un linguaggio L2:

- O lo si traduce in **L1** per eseguire il programma su M1,
- O lo si traduce in **L0** per eseguire il programma direttamente su M0 (+ oneroso > i livelli).

Ovviamente l'iterazione dell'astrazione delle VM tende all'"infinito", o almeno finché non è comprensibile dall'uomo.

![](https://i.imgur.com/7V1qQpI.png)

Per scrivere i programmi per il livello *n* <u>non è necessario conoscere come le istruzioni vengono tradotte</u>. Solo chi vuole capire come funziona un calcolatore o come si progetta una macchina virtuale ha necessità di conoscere come funzionano i livelli intermedi/inferiori.

# Esercizi

# Soluzioni

---

Prossima lezione: [[4 - Livelli dei calcolatori]]

