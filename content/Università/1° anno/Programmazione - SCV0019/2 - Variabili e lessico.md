# Lezione 2

### Variabili

Le variabili sono come dei contenitori logici che contengono valori. Per <u>definire</u> una variabile in un programma java bisogna "**dichiararla**" (ovvero scriverla definendone il **[[#Tipo|tipo]]**, per esempio: `int variabile;` dove "*int*" è un <u>tipo</u> e "*variabile*" è il <u>nome della variabile</u>).

Per <u>dare un valore</u> a una variabile si usa un'operazione detta di "**assegnamento**". In java l'assegnamento di una variabile si fa con questa notazione: `variabile = valore`; (nota che il valore da assegnare potrebbe anche essere un'<u>espressione da valutare</u>, tipo: `var = x + y`).

Nella realtà però, una **variabile** è un'astrazione del concetto di <u>locazione di memoria</u>, mentre l'**assegnamento** è invece un'astrazione dell'operazione `STORE`.

Si sta invece "**definendo**" una variabile quando la si dichiara e le si assegna un valore allo stesso momento (tipo: `int var = 1;`).

### Tipi

Il **tipo** di una variabile è ciò che ne indica:

- L'insieme dei <u>valori che in essa possono essere memorizzati</u>,
- L'insieme delle <u>operazioni che è possibile effettuare con essa</u>.

In memoria le variabili sono salvate come sequenze di bit, ma sono interpretate in base al loro tipo:

- $01000001$ in '*char*' = '$A$',
- $01000001$ in '*int*' = $65$.

##### Tipi di tipi

Esistono comunque 2 categorie di tipi:

###### Tipi primitivi

Tipi **primitivi**: una variabile di tipo **primitivo** contiene un **valore** "*direttamente*",

  ![](https://i.imgur.com/fSQGeJa.png)

###### Tipi di riferimento

Tipi **di riferimento**: una variabile di tipo **riferimento** contiene il ***riferimento*** con cui si può accedere all'oggetto riferito,

  ![](https://i.imgur.com/p2SrhwZ.png)

> [!info] Null
> `null` è un valore assegnabile a tutte le variabili di **tipo riferimento** e indica che la variabile <u>non fa riferimento ad alcun oggetto</u>.
> Quando si prova ad accedere ad un oggetto `null` di tipo riferimento, viene lanciata una (link) NullReferenceException.

###### Tipi in Java

##### Tipi *boxed*

(Vedere prima classi (link)), in `java.lang` è prevista una classe ***boxed*** per ogni tipo primitivo aventi campi, metodi e costruttori utili agli oggetti di quel tipo:

![](https://i.imgur.com/3aQEm46.png)

###### Integer

| Keyword                        | Categoria   | Tipo      | Accessibilità   | Descrizione                                                                                                                                        |
| ------------------------------ | ----------- | --------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Integer(int x)`               | Costruttore | `Integer` | `public`        | Costruisce classe `Integer` da un `int`                                                                                                            |
| `Integer(String s)`            | Costruttore | `Integer` | `public`        | Costruisce classe `Integer` da una `String` convertibile in `int`                                                                                  |
| `Integer.MIN_VALUE`            | Campo       | `int`     | `static final`  | Minimo valore rappresentabile tramite `int`                                                                                                        |
| `Integer.MAX_VALUE`            | Campo       | `int`     | `static final`  | Massimo valore rappresentabile tramite `int`                                                                                                       |
| `Integer.compareTo(Integer x)` | Metodo      | `int`     | `public`        | Confronta un `Integer` con un altro passato per parametro, ritornando $0$ se i due coincidono, $-1$ se il 1° è < del 2° e $1$ se il 1° è > del 2°. |
| `Integer.intValue()`           | Metodo      | `int`     | `public`        | Ritorna un `int` corrispondente al valore dell'oggetto `Integer`                                                                                   |
| `Integer.longValue()`          | Metodo      | `long`    | `public`        | Ritorna un `long` corrispondente al valore dell'oggetto `Integer`                                                                                  |
| `Integer.parseInt(String s)`   | Metodo      | `int`     | `public static` | Converte una `String` in un `int` (se possibile)                                                                                                   |
| `Integer.valueOf(String s)`    | Metodo      | `Integer` | `public static` | Ritorna un `Integer` corrispondente al valore della `String` passata come parametro                                                                |

###### Character

| Keyword                             | Categoria   | Tipo        | Accessibilità   | Descrizione                                                           |
| ----------------------------------- | ----------- | ----------- | --------------- | --------------------------------------------------------------------- |
| `Character(char c)`                 | Costruttore | `Character` | `public`        | Costruisce classe `Character` da un `char`                            |
| `Character.isDigit(char c)`         | Metodo      | `boolean`   | `public static` | Ritorna `true` se `c` è una cifra, altrimenti `false`                 |
| `Character.isLetter(char c)`        | Metodo      | `boolean`   | `public static` | Ritorna `true` se `c` è una lettera, altrimenti `false`               |
| `Character.isLetterOrDigit(char c)` | Metodo      | `boolean`   | `public static` | Ritorna `true` se `c` è una cifra o una lettera, altrimenti `false`   |
| `Character.isLowerCase(char c)`     | Metodo      | `boolean`   | `public static` | Ritorna `true` se `c` è una lettera minuscola, altrimenti `false`<br> |
| `Character.isUpperCase(char c)`     | Metodo      | `boolean`   | `public static` | Ritorna `true` se `c` è una lettera maiuscola, altrimenti `false`<br> |
| `Character.toLowerCase(char c)`     | Metodo      | `char`      | `public static` | Rende `c` minuscolo                                                   |
| `Character.toUpperCase(char c)`     | Metodo      | `char`      | `public static` | Rende `c` maiuscolo                                                   |

###### Wildcard

Quando si parla di tipi parametrizzati (tipo poi vedremo `List<T>`), per la dichiarazione di questi è possibile usare `?` per indicare che il tipo non è noto al momento (ma lo deve essere alla definizione):

```java
List<?> l;
//...
l = new ArrayList<Integer>();
//...
l = new ArrayList<String>();
```

### Espressioni

Un'**espressione** è una porzione di codice avente:

- Un **tipo**, determinato (in fase di compilazione) dagli <u>operatori</u> e dal tipo degli <u>operandi</u>,
- Un **valore**, determinato (al momento dell'esecuzione) dalla risoluzione dell'operazione.

###### Tipi di espressioni

Le espressioni possono essere di diversi tipi, come letterali, operazioni (matematico-logiche), di variabili (come l'assegnamento fatto con l'operatore "="), coi metodi (link) (invocazioni), con classi e oggetti (istanza: `new`, accesso: `.`)...

> [!error] Effetti collaterali
> Bisogna prestare attenzione anche agli effetti collaterali, ovvero modifiche dei valori delle variabili stesse durante il loro uso in certe espressioni, come:
> ![](https://i.imgur.com/DgzL7Ap.png)

#### Operatori

Ci sono tanti operatori usabili nelle espressioni in java:

![](https://i.imgur.com/7LJ5MGG.png)

![](https://i.imgur.com/CZbkeiy.png)

##### Espressioni matematiche

Per esempio quelle matematiche tra tipi numerici:

![](https://i.imgur.com/jA0Km5T.png)

Si ricorda che per le espressioni matematiche la precedenza è la stessa della matematica.

Se poi 2 variabili `x` e `y` sono di tipo numerico è possibile abbreviare tali operazioni:

![](https://i.imgur.com/htQJapQ.png)

###### Incremento e decremento

Per incrementare o decrementare di 1 una qualsiasi variabile numerica è possibile usare gli operatori `++` e `--` in 2 modi:

- ![](https://i.imgur.com/15NWXX2.png)
- ![](https://i.imgur.com/2Ys8LMC.png)

> [!info] Nota
> Incrementando o decrementando una variabile <u>in un'espressione</u> (di assegnamento, di confronto...), il suo **valore modificato** <u>permane nella variabile stessa</u> invece di essere temporaneo solo per l'espressione corrente.

##### Espressioni booleane

Le espressioni booleane sono di tipo complessivo `boolean` e sono principalmente usate in costrutti [[3 - Costrutti di selezione|condizionali]] e [[4 - Costrutti di iterazione|di iterazione]].

###### Operatori booleani

Gli operatori booleani principali sono `!`, `&&` e `||` (senza contare "\==" o `.equals`). I primi 3 indicano rispettivamente 1) la negazione/inversione del valore di una variabile booleana, 2) la correttezza di entrambe e 3) quella di almeno 1 delle 2.

Tali hanno un'ordine di precedenza: `!` $\rightarrow$ `&&` $\rightarrow$ `||`, infatti:

`!a && b || a && !c` corrisponde a: `((!a) && b) || (a && (!c))`

> [!important] Leggi di De Morgan
> `!(x && y)` = `!x || !y`
> `!(x || y)` = `!x && !y`

###### "=" vs "equals"

Nelle condizioni, per determinare l'uguaglianza di 2 elementi si può usare l'operatore "\==" o `.equals`. Per i tipi di riferimento vi è una differenza fra i 2:

- "\==": ritorna `true` se 2 variabili fanno riferimento allo stesso oggetto in memoria, altrimenti `false`,
- `.equals`: guarda le caratteristiche dell'oggetto referenziato e ritorna `true` sia se le 2 variabili fanno riferimento allo stesso oggetto, sia se i 2 oggetti hanno le stesse caratteristiche (anche se "diversi" in locazione di memoria in cui sono istanziati); ovvio che nell'ultimo caso, se i 2 oggetti hanno anche 1 caratteristica diversa, ritorna `false`.

![](https://i.imgur.com/mBRZIsT.png)

![](https://i.imgur.com/DIoVqJL.png)

###### Lazy evaluation

Gli operatori booleani `&&` e `||` sono detti "***lazy***" siccome seguono le regole della ***lazy evaluation***, che permette di determinare il risultato di un'espressione valutandone solo una parte ed ignorando l'altra.

Ciò funziona solo in certi casi:

- `x && y`: se `x` è `false` abbiamo già determinato il risultato dell'espressione (sempre `false`), indipendentemente da `y`,
- `x || y`: se `x` è `true` abbiamo già determinato il risultato dell'espressione (sempre `true`), indipendentemente da `y`.

#### Conversioni

Quando si opera con tipi diversi spesso è necessario che questi siano **convertiti** a uno stesso tipo per poter fare certe operazioni e questo processo può avvenire in 2 modi:

##### Conversioni implicite

Le **conversioni implicite** (dette anche ***promozioni***) si verificano nelle espressioni quando una variabile di un tipo più "ristretto" (***narrow***) è <u>promossa</u> ad un tipo più "ampio" (***wide***):

![](https://i.imgur.com/gJAsRww.png)

Generalmente, considerando un'espressione `x + y` entrambe dello stesso tipo, la JVM converte implicitamente il risultato dell'espressione a:

- `float`, `double` o `long` se le variabili sono `float`, `double` o `long`,
- `int` se le variabili sono `byte`, `short` o `int`.

###### Esempio conversioni implicite

Per esempio, tra `int` e `long`:

![](https://i.imgur.com/VZ9kDhT.png)

> [!error] Attenzione
> Non è possibile assegnare ad una variabile di tipo più "ristretto" un valore di tipo più "ampio" (anche se il valore stesso può "starci" in un tipo "ristretto").
> Per questo ci vogliono i ***[[#Conversioni esplicite|cast]]***.

##### Conversioni esplicite

Le **conversioni esplicite** (dette anche **forzature** o ***cast***) sono invece fatte dall'utente sempre per convertire un tipo in un altro, ma possibili anche da un tipo più "ampio" ad uno più "ristretto", con il rischio di una possibile <u>perdita di informazione</u>.

> [!error] Perdita di informazione
> Consideriamo un esempio:
> ```java
> int x;
> double y = 1.5;
> x = (int)y;
> ```
> In questo caso `x` risulterebbe = 1, siccome un `int` non può contenere i valori decimali; perciò la parte decimale viene tagliata automaticamente.

# Esercizi

# Soluzioni

---

Prossima lezione: [[3 - Costrutti di selezione]]

