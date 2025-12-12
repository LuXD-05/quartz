# Lezione 7

### Collezioni

Le collezioni sono semplicemente insiemi di variabili o oggetti rappresentati in un certo modo. Ce ne sono di diversi tipi:

#### Array

Gli ***array*** sono degli oggetti che rappresentano insiemi ordinati di variabili dello <u>stesso tipo</u> (quindi anche oggetti con la stessa base) ognuna delle quali è accessibile tramite la sua **posizione** nell'array stesso. Di questi ricordare:

- <u>Dichiarazione</u>: `String[] array;` in questo caso di stringhe,
- <u>Definizione</u>: `String[] arr = new String[4]` per gli array è **obbligatorio** definirne la **dimensione**, infatti in `arr` potranno essere contenute massimo 4 stringhe.
- <u>Inizializzazione</u>: alla definizione, ogni elemento di array è posto a `null`, a meno che non si faccia: `String[] arr = { "a", "b", "c", "d" }` dandogli un valore ed una dimensione definite a priori.
- <u>Accesso ad elementi</u>: `String s = arr[0]`, qui si sta accedendo all'array per prendere la stringa all'indice $0$ (le posizioni negli array vanno da 0 alla loro dimensione - 1); $0$ può anche essere una variabile basta che sia `int`.

> [!error] IndexOutOfBouds
> Nel caso si provi ad accedere ad un array con un indice >= alla sua **dimensione** (perché gli indici vanno da 0 a dimensione - 1), verrà lanciata un'eccezione (link) in fase di esecuzione, la `ArrayIndexOutOfBoundsException`.

###### Cicli

Solitamente degli array, come per le altre collezioni, si itera attraverso ognuno dei suoi elementi per fare qualcosa e più comunemente si usa il ***for*** invece che il ***foreach*** in quanto col 2° non è possibile accedere agli indici dell'array e fare confronti tra essi e quello corrente.

###### Array di tipi primitivi vs di tipi di riferimento

Esempio di array con tipi primitivi (`char`) vs array con tipi di riferimento (`string`):

![](https://i.imgur.com/PUv9ACB.png)

##### Matrici

Se gli array classici sono *monodimensionali*, le **matrici** sono invece array *bidimensionali*; in parole povere, array di array (ogni elemento di un array è un array). Quindi:

- <u>Dichiarazione</u>: `String[][] matrix;` sempre di stringhe (tutta la matrice è di stringhe),
- <u>Definizione</u>: `String[][] mat = new String[3][12]` per le matrici bisogna invece **necessariamente** definire sia la dimensione delle righe sia quella delle colonne:

  ![](https://i.imgur.com/0AV7jO9.png)

- <u>Inizializzazione</u>: stessa cosa degli array ma così: `String[][] mat = { {1,2,3}, {4,5,6}, {7,8,9} }`.
- <u>Accesso ad elementi</u>: `String s = mat[0][0]`, qui si sta accedendo alla matrice per prendere la stringa all'indice di riga $0$ e a quello di colonna $0$.

#### ArrayList

Un `ArrayList<T>` è un'oggetto che implementa l'interfaccia `List<T>` e, in parole semplici, è un'[[#Array|array]] dinamico, quindi di dimensione variabile. Le cose importanti quindi sono:

- <u>Funzionamento</u>: è il medesimo degli array ma senza limiti di dimensione o `ArrayIndexOutOfBoundException` + sintassi diversa (Nota: `T` è il *parameter type*, ovvero il <u>tipo delle variabili nella lista</u>).
- <u>Definizione</u>: `List<String> list = new ArrayList<String>()`.
- <u>Inizializzazione</u>: praticamente stessa cosa degli array.
- <u>Accesso ad elementi</u>: ...

#### LinkedList

Le `LinkedList<T>` sono praticamente la stessa cosa delle `ArrayList<T>`, ma cambiano piccole cose a livello di struttura, efficienza e memoria:

...

#### Stack

Lo `Stack<T>` è una collection **LIFO** (*Last In First Out*) coi seguenti metodi:

###### Metodi

- `public void push(T obj)`: inserisce un elemento in cima allo `Stack<T>`,
- `public T pop()`: rimuove l'elemento in cima allo `Stack<T>` e lo restituisce,
- `public boolean empty()`: ritorna `true` se lo `Stack<T>` è vuoto.

###### Eccezioni

- `EmptyStackException`: se si prova a fare `pop()` quando lo stack è vuoto.

#### Queue

La `Queue<T>` è una collection **FIFO** (*First In First Out*) coi seguenti metodi:

###### Metodi

- `public void add(T obj)`: inserisce un elemento nella `Queue<T>`,
- `public T remove()`: rimuove il 1° elemento dalla `Queue<T>` e lo ritorna,
- `public boolean element()`: ritorna un riferimento al 1° elemento della `Queue<T>`.

###### Eccezioni

- `EmptyQueueException`: se si prova a fare `remove()` quando la queue è vuota.

# Esercizi

# Soluzioni

---

Prossima lezione: [[8 - Eccezioni]]

