# java.util

### String

La classe `String` modella stringhe, ovvero sequenze di char (caratteri).

`String` mette a disposizione un costruttore avente come argomento una sequenza ti caratteri tra "". Tuttavia questo non viene mai chiamato ma si inizializzano stringhe nel seguente modo: `String s = "stringa";`

##### Metodi

La classe `String` mette a disposizione vari metodi:

- `toLowerCase(String s);`,
- `toUpperCase(String s);`,
- `concat(String s)`: concatena 2 stringhe (corrisponde a fare `"stringa1" + "stringa2"`),
- `length()`: restituisce la lunghezza (n° di caratteri) di una stringa (si, a quanto pare per le classi esiste length come metodo, mentre per altro tipo array è una proprietà, quindi usata senza parentesi).
- `substring(int start, int? end)`: restituisce una porzione della stringa originale partendo dalla posizione `start`. Il parametro `end` si può anche non specificare, ma se è specificato verrà restituita una la porzione di stringa da `start` a `end`; altrimenti restituirà la stringa da `start` alla fine.
  - Se `end` è maggiore di `s.length()`, allora il metodo genererà l'eccezione `java.lang.`[[#Eccezioni|StringIndexOutOfBoundExceprtion]].
- `charAt(int index)`: ritorna il char alla posizione `index` della stringa.

##### Eccezioni

- `StringIndexOutOfBoundsException`: eccezione generata quando un intero passato ad un metodo di un oggetto `String` è maggiore della lunghezza della stringa.

### Math

##### Metodi

- `pow(base, esp)`: ritorna il risultato di `base` elevato a `esp`,

# Statici

### Integer

##### Metodi

- `parseInt(string s)`: converte una stringa in int (se possibile), altrimenti genera una `java.lang.NumberFormatException`.
- 
