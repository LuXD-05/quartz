# Lezione 4

### Costrutti di iterazione

I costrutti iterazionali in Java permettono di eseguire uno stesso blocco di righe di codice per un certo numero di volte o finché non si verifica una certa condizione. Abbiamo:

```java
while () {
	//...
}

do {
	//...
} while ()

for (init; cond; incr) {
	//...
}

for (type var : collection) {
	//...
}
```

Di questi:

- `while` è il ciclo più semplice: in base a una qualsiasi condizione esegue il suo corpo diverse volte. Può ripeterlo anche 0 volte se la condizione è già `false`.
- `do-while` è come il precedente, solo che esegue il suo corpo almeno 1 volta (anche se la condizione è già `false`).
- Il 1° `for` è il suo uso più "normale", che nella condizione comprende 3 espressioni: 1 di inizializzazione (tipo `int i = 0;`), 1 condizione che fin quando rispettata il ciclo continua (tipo `i < n;`), e un'espressione di incremento (tipo `i++`).
- Il 2° `for` è quello che più comunemente è detto `foreach`, ovvero che per ogni elemento di una *collection* (tipo un [[7 - Array e collezioni#Array|array]]), prende l'oggetto corrente nella variabile *var* ed esegue delle istruzioni per essa.

###### Break

Il `break` è usato nei cicli per interromperli prima che la condizione che ne scandisce le iterazioni non sia più rispettata. Per esempio:

```java
int i = 3;
while (i > 0) {
	if (i % 2 == 0)
		break;
	i--;
}
```

In questo caso il ciclo si fa 1 volta con `i = 3`, poi la 2a volta, quando `i = 2`, si entra nella condizione ed il ciclo termina per il `break`.

###### Continue

Il `continue` è usato nei cicli per saltare 1 singolo ciclo e passare al successivo. Per esempio:

```java
int i = 3, sum = 0;
while (i > 0) {
	if (i % 2 == 0) {
		i--;
		continue;
	}
	sum += i;
}
```

Qui la somma finale sarà ${} 4$ dato che si eseguono solo i cicli quando `i = 3` e `i = 1`, mentre quello in cui `i = 2` si salta.

# Esercizi

# Soluzioni

---

Prossima lezione: [[5 - Classi e oggetti]]

