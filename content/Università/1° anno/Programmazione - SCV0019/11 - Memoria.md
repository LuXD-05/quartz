# Lezione 11

### Memoria

La JVM lavora con 2 tipi di memoria:

- **Memoria statica**: utilizzata per classi, metodi e campi `static`, stabilita a priori ed allocata al momento dell'esecuzione,
- **Memoria dinamica**: contiene tutti i dati non statici del programma e si divide in:

##### Stack

Lo ***stack*** contiene i dati dei metodi che vengono man mano eseguiti; quindi ad ogni chiamata di metodo lo *stack* cresce allocandone la memoria per esso e i suoi parametri, mentre decresce <u>automaticamente</u> alla fine dell'esecuzione dei metodi.

Questo prende il nome dallo [[7 - Array e collezioni#Stack|stack]], infatti è una struttura **LIFO** (*Last In First Out*); quindi una pila di <u>record di attivazione</u>, aree di memoria contenenti dati relativi a ciascun metodo allocati.

Esempio con metodi `a` e `b`:

![](https://i.imgur.com/7DgNAME.png)

##### Heap

L'***heap*** invece memorizza tutti gli oggetti creati dinamicamente durante l'esecuzione del programma (espressioni con `new`) e le classi permanenti del **JRE** (*Java Runtime Engine*).

> [!important] Garbage collector
> L'*heap* non si ridimensiona in automatico, bensì, quando un oggetto non è più utilizzato o accessibile, il ***garbage collector*** recupera la memoria occupata dagli oggetti non più referenziati e riorganizza l'*heap* risolvendo eventuali problemi di allocazione (causati dalla frammentazione).

# Esercizi

# Soluzioni

---

Prossima lezione: [[12 - Java specifics]]

