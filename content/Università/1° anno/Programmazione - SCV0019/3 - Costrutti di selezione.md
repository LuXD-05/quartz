# Lezione 3

### Costrutti di selezione

In Java ci sono diversi costrutti coi quali è possibile scegliere un certo blocco di istruzioni in base a una condizione di tipo `boolean`. Abbiamo:

```java
if () {
	//...
}

if () {
	//...
} else {
	//...
}

if () {
	//...
} else if () {
	//...
} else {
	//...
}

switch () {
	case '':
		//...
		break;
	default:
		//...
		break;
}

String _ = s != null ? s : null;
```

Di questi:

- I primi 3 sono 3 modi per scrivere il costrutto di base: l'`if`, il quale può comprendere la condizione `else` (se la condizione nell'if è `false`) ed eventualmente anche `else if` (per lo stesso motivo),
- Quando ci sono troppi `if-else-elseif` per una singola variabile è meglio usare uno `switch` un costrutto molto efficiente che ci porta alla label col valore della variabile ed esegue solo il codice al suo interno (se label per un valore non è definita, va in `default`).
- L'ultimo caso invece è una condizione in una linea per un'assegnamento in cui: "se `s` non è `null` assegna a `_` il valore di `s`, altrimenti `null`".

# Esercizi

# Soluzioni

---

Prossima lezione: [[4 - Costrutti di iterazione]]

