### Metodi

> [!important] Segnatura (firma)
> La **segnatura** di un metodo è costituita da: \[nome metodo\](\[lista argomenti con relativo tipo\])
> Ovvero: `read(File file)`.

> [!important] Prototipo
> Il prototipo di un metodo è composto da \[tipo metodo\] \[segnatura\]
> Ovvero: `String[] read(File file)`.

> [!important] Overloading
> Possibilità di avere metodi con nome uguale ma firma diversa.

##### Metodi statici

Discriminati dalla *keyword* "***static***" prima del nome del metodo, sono dei "servizi" forniti direttamente dalle classi invece che dagli oggetti (istanze di tali classi). Utili per:

- Costruire oggetti della classe stessa partendo da oggetti/valori dello stesso tipo (convertire un int in stringa),
- Fornire operazioni utili su oggetti o su tipi primitivi (metodi di classe "Math" di java.lang per fare alcune funzioni matematiche),
- Definire proprietà che influenzano il comportamento degli oggetti.

###### Esempio

`String.valueOf(3)`: `valueOf()` è chiamato direttamente dalla classe `String`, senza bisogno di creare una variabile o un oggetto per accedervi.

### I/O

Ci sono diverse classi e metodi adibiti all'I/O (input/output) di dati:

##### Output

##### Input

Prima di utilizzare metodi per l'acquisizione di input in java, è necessario innanzitutto importare la classe `Scanner` con `import java.util.Scanner`. In seguito, per acquisire un input utente si seguono questi passi:

1) Dichiaro uno `Scanner` con parametro `System.in`: `Scanner sc = new Scanner(System.in);`,
2) Ottengo (in questo caso) un intero con `sc.nextInt()`: `int n1 = sc.nextInt();`.

Il metodo di `Scanner`: `next()` (e qualsiasi altro suo simile come `nextInt()`) sono **bloccanti**, ovvero bloccano il flusso di esecuzione del programma fino a quando non è stato inserito un qualsiasi tipo di input in console (e quindi dopo che lo si è "confermato" premendo 'INVIO'); a quel punto il programma riprende.

Quindi, siccome potrebbe non capirsi cosa succede quando si vede solo la console nera, sarebbe meglio stampare un messaggio che segnala che il prossimo input sarà acquisito prima di usare un metodo come `next()`.

(Scanner non in esame ma in esercitazioni)

### Tipi

Java è un linguaggio **fortemente tipizzato**, ciò significa che il tipo delle variabili è già definito nel programma e <u>noto al momento della compilazione</u> e quindi non è possibile (al contrario per esempio di Javascript) usare una variabile `int` per memorizzare un valore `String`.

##### Categorie

###### Tipi primitivi

Contengono direttamente un valore. Comprendono:

- int,
- double,
- char...

###### Tipi di riferimento

Contengono un riferimento ad una cella di memoria (puntatore). Comprendono:

- Classi,
- Interfacce,
- Array...

##### Assegnamenti

###### Copia per valore

###### Copia per riferimento

##### Tipo *null*

Valore assegnabile a qualsiasi variabile di tipo riferimento ed indica che la variabile non fa riferimento ad alcun oggetto. Tentando di accedere ad un oggetto a cui vi è assegnato *null* genererà, in fase di esecuzione, una *NullPointerException*.

