# Lezione 6

### Metodi

I metodi contengono blocchi di codice che vengono eseguiti con una chiamata al nome del metodo e usano parametri passati allo stesso. Definizioni:

- La **firma** (o ***signature***) di un metodo è costituita da: \[nome metodo\](\[lista argomenti con relativo tipo\]), tipo: `println(String s)`.
- Il **prototipo** di un metodo è composto da \[tipo metodo\] \[firma\], tipo: `void println(String s)` (tipo del metodo `void` indica che non restituisce niente).

###### Parti di un metodo

- **Modificatori**: forniscono info relative all'accessibilità del metodo da parte di altri metodi, classi o *scope*. Tipo: `public`, `private`...
- **Tipo restituito**: il tipo di ciò che è restituito dal metodo (con `return`), tipo: `int`, `Class`, `void` (non ritorna niente), ...
- **Nome**: il nome del metodo,
- **Parametri**: lista di parametri tra "()" separati da virgola, divisi in:
- **Eccezioni**: definite con `throws`.

###### Passaggio di parametri

I parametri al metodo possono essere passati per:

- **Valore**: tutti i parametri (di tipo <u>primitivo</u>) sono normalmente passati per valore, ovvero una **copia** del loro valore è data al metodo per lavorare con essa in locale.
- **Riferimento**: i parametri di tipo <u>riferimento</u> invece, quando passati ad un metodo, se modificati all'interno di esso manterranno le modifiche anche finita la sua esecuzione.

##### Metodi statici

Discriminati dalla *keyword* "***static***" prima del nome del metodo, sono forniti direttamente dalle classi.

Esempio: `String.valueOf(3)`; il metodo `valueOf()` è chiamato direttamente dalla <u>classe</u> `String`, senza bisogno di creare un oggetto per accedervi.

##### Metodi ricorsivi

Un metodo ricorsivo è un metodo che richiama se stesso al suo interno, per esempio:

```java
public static int fattoriale(int n) {
	if (n <= 1)
		return 1;
	else
		return n * fattoriale(n - 1);
}
```

# Esercizi

# Soluzioni

---

Prossima lezione: [[7 - Array e collezioni]]

