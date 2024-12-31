# Lezione 13

### Classi

##### ConsoleOutputManager

`ConsoleOutputManager` è una classe di `prog.io` le cui istanze permettono di stampare in output (a video su una CLI) qualcosa.

Ha i metodi `print(...)`, che stampa il testo passato, e `println(...)` che fa la stessa cosa ma va anche a capo.

###### Uso ConsoleOutputManager

```java
import prog.io.ConsoleOutputManager;

class Program {
	public static void main(String[] args) {
		ConsoleOutputManager output = new ConsoleOutputManager();
		output.println("Hello World");
	}
}
```

##### ConsoleInputManager

`ConsoleInputManager` è una classe di `prog.io` le cui istanze permettono di registrare input di tastiera dell'utente rendendoli disponibili al programma.

Ha i metodi `readLine()` che legge l'intera riga scritta dall'utente + `read*()` dove `*` sta per un qualsiasi tipo di dato (1a lettera maiuscola), tipo `readInt()` che legge e converte in int.

###### Uso ConsoleInputManager

```java
import prog.io.ConsoleInputManager;

class Program {
	public static void main(String[] args) {
		ConsoleInputManager input = new ConsoleInputManager();
		String messaggio = input.readLine();
	}
}
```

##### Frazione 🤮

Classe le cui istanze modellano frazioni.

###### Costruttori frazione

- `public Frazione(int x)`: crea una frazione con numeratore `x` e denominatore 1.
- `public Frazione(int x, int y)`: frazione con numeratore `x` e denominatore `y`.

###### Metodi e proprietà frazione

- `public Frazione piu(Frazione f)`: ritorna (il riferimento a) un nuovo oggetto Frazione ottenuto sommando ad una frazione il parametro `f`.
- `public Frazione meno(Frazione f)`: ... sottraendo `f` ad una frazione.
- `public Frazione per(Frazione f)`: ... moltiplicando una frazione per `f`.
- `public Frazione diviso(Frazione f)`: ... dividendo una frazione per `f`.
- (bool) `equals(Frazione f)`: ritorna `true` se il <u>valore</u> delle 2 frazioni è uguale.
- (bool) `isMinore(Frazione f)`: `true` se frazione è minore di `f`.
- (bool) `isMaggiore(Frazione f)`: `true` se frazione è maggiore di `f`.
- (int) `getNumeratore()`: ritorna il numeratore della frazione.
- (int) `getDenominatore()`: ritorna il denominatore della frazione.
- (string) `toString()`: ritorna una stringa che rappresenta la frazione che chiama il metodo.

##### Figura 🤮

![](https://i.imgur.com/qLqTGY0.png)

![](https://i.imgur.com/rNIuIiI.png)

##### Rettangolo 🤮

![](https://i.imgur.com/zMiW98W.png)

##### Quadrato 🤮

![](https://i.imgur.com/48xXAxg.png)

##### Cerchio 🤮

![](https://i.imgur.com/D8s7YNc.png)

##### Sequenza 🤮

La classe `Sequenza<T>` è la stessa identica cosa di una `ArrayList<T>` ma con metodi custom Insubria.

###### Proprietà sequenza

- `public int size()`: ritorna il numero di elementi della sequenza.

###### Metodi sequenza

- `public boolean add(T obj)`: aggiunge alla fine della sequenza l'oggetto `obj` e ritorna `true` (se `obj` è `null`, non fa niente e ritorna `false`).
- `public boolean remove(T obj)`: elimina il 1° elemento della sequenza che trova che corrisponde a `obj` e ritorna `true`; se `obj` non c'è lascia la sequenza immutata e ritorna `false`.
- `public boolean isEmpty()`: ritorna `true` se la sequenza è vuota.
- `public boolean contains(T obj)`: ritorna `true` se la sequenza contiene on oggetto le cui proprietà corrispondono ad `obj`, altrimenti `false`.
- `public T find(T obj)`: ritorna il riferimento al 1° oggetto che trova avente le stesse caratteristiche di `obj`, altrimenti ritorna `null`.

##### SequenzaOrdinata

La classe `SequenzaOrdinata<T>` è identica a `Sequenza<T>`, solo che i suoi oggetti sono ordinati con un certo criterio in base a `T`. Questo ne limita gli usi in quanto `T` deve essere necessariamente un tipo ordinabile.

##### Coppia 🤮

La classe `Coppia<T1, T2>` è semplicemente una `Map` custom Insubria.

###### Metodi

![](https://i.imgur.com/HzQryKd.png)

##### Orario

Classe per tempo.

###### Metodi

![](https://i.imgur.com/V9SCmon.png)

![](https://i.imgur.com/tUhy1Fq.png)

![](https://i.imgur.com/QD6D5Bm.png)

![](https://i.imgur.com/VSKhrAg.png)

# Esercizi

# Soluzioni

---

