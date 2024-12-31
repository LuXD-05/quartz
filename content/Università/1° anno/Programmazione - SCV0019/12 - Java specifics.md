# Lezione 12

### Main

Il `main` è un metodo statico `void` (non ritorna niente) e avente come parametro un array di stringhe: `public static void main(String[] args)`.

Esso è fondamentale in ogni file che si esegue in quanto la JVM cerca specificatamente nel *bytecode* della classe principale un metodo statico col suddetto prototipo e, se lo trova, lo invoca (`args` è valorizzato solo se sono passati parametri da linea di comando all'esecuzione del file, altrimenti è una collezione vuota).

### I/O

Ci sono diverse classi standard e metodi adibiti all'I/O:

##### Output

##### Input

Prima di utilizzare metodi per l'acquisizione di input in java, è necessario innanzitutto importare la classe `Scanner` con `import java.util.Scanner`. In seguito, per acquisire un input utente si seguono questi passi:

1) Dichiaro uno `Scanner` con parametro `System.in`: `Scanner sc = new Scanner(System.in);`,
2) Ottengo (in questo caso) un intero con `sc.nextInt()`: `int n1 = sc.nextInt();`.

Il metodo di `Scanner`: `next()` (e qualsiasi altro suo simile come `nextInt()`) sono **bloccanti**, ovvero bloccano il flusso di esecuzione del programma fino a quando non è stato inserito un qualsiasi tipo di input in console (e quindi dopo che lo si è "confermato" premendo 'INVIO'); a quel punto il programma riprende.

Quindi, siccome potrebbe non capirsi cosa succede quando si vede solo la console nera, sarebbe meglio stampare un messaggio che segnala che il prossimo input sarà acquisito prima di usare un metodo come `next()`.

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

Parte di `java.lang`, `Math` è una libreria standard di Java usata per varie operazioni matematiche anche complesse.

##### Metodi

- `pow(base, esp)`: ritorna il risultato di `base` elevato a `esp`,
- `log10(double n)`: ritorna il logaritmo in base 10 di `n`,

### Integer

##### Metodi

- `parseInt(string s)`: converte una stringa in int (se possibile), altrimenti genera una `java.lang.NumberFormatException`.
- 

# Esercizi

# Soluzioni

---

Prossima lezione: [[13 - Insubria specifics]]

