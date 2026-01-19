# Esami

### Modalità d'esame

Prova articolata in 3 parti:

1) Domande a risposta aperta su carta (no appunti), valgono tipo il 30% della prova.
2) Esercizio di verifica e convalida di un software su carta (no appunti).
3) Esercizi UML su carta (appunti consultabili), questa e la precedente valgono il restante 70% della prova.

# Esercizi

### 1 - Domande teoria

#####

### 2 - Esercizio

##### Annulment-Def-Use

L'esercizio di **annullamento-definizione-uso** prevede di indicare sequenzialmente le azioni di annullamento/definizione/uso di certe variabili di un codice mostrato.

> [!info] Errori
> Errori di precedenza di a / d / u

###### Annulment

L'***annulment*** si indica con la lettera `a` e si ha quando si **dichiara** una variabile (non contando l'assegnamento di un valore ad essa):

```java
int a; // a - annullment
```

###### Def

La ***def*** si indica con la lettera `d` e si ha quando si assegna un valore ad una variabile (sia <u>durante la dichiarazione</u> che come <u>parametri di funzione</u> che negli altri casi):

```java
// Def sia di arr che di n
public int func(int arr[], int n) {  // arr/n --> d

	// def di a (senza annulment)
	int a = 5;                       // a --> d (non "ad")
	
	// "read(variabile)" è def
	read(x);                         // x --> d
}
```

> [!info] Nota
> Essere parametri di funzione comporta la *def* degli stessi.
> Quando si ha dichiarazione con assegnamento al prof va bene che si scriva solo `d` e non `ad`.

###### Use

Lo ***Use*** invece si indica con la `u` e si ha quando si accede ad una variabile per usarne il valore (quando è usata banalmente):

```java
// Letto il valore di x per assegnarlo ad a
a = x;       // x --> u

// Nel for:
for (int i = 0; i <= n; i++) { ... }
// i --> du(...udu)*   (ovvero:)   "i=0" = d, "i<=n" = u, ("..." = roba in for, "i++" = "i=i+1" = ud, "i<=n" = u), "*" = non rientra?
// n --> uu*           (ovvero:)   "i<=n" = u, "u*" = se u precedente era true allora rifà u, altrimenti no (esce dal for)

// return (legge il valore di f per ritornarlo)
return f;    // f --> u
```

###### Altre notazioni

Ci sono ulteriori simboli e notazioni:

- `()`: racchiudono gli *statement* all'interno di un ciclo o di una condizione (anche le condizioni del ciclo che si ripetono prima di uscirci),
- `*`: indica che l'azione o l'insieme di azioni (`()`) precedenti potrebbero non avvenire in caso la condizione del ciclo sia `false` (indica che forse si esce dal ciclo),
- `+`: usato solo per indicare i 2 rami di un `if` e usato sempre con (`()`); esempio: `(...+...)` dove i primi `...` sono le azioni del ramo `true` e gli altri del ramo `false`,
- $\varepsilon$: usata quando si indica che di una variabile non viene fatta alcuna azione in un blocco (`()`), (usato solo negli `if` e non nei cicli: `(...+`$\varepsilon$`)`è un `if` senza `else`); se di una variabile non sono fatte azioni in nessuno dei blocchi di una condizione, non c'è bisogno di scrivere `(`$\varepsilon$`+`$\varepsilon$`)` ma si salta.

###### Casi particolari

1\) `return` prima della fine della funzione: quando si ha un `return` (di solito in un `if`) prima dell'ultimo `return` della funzione, per variabili usate o definite dopo è necessario separare i *branch*: quello che entra nell'`if` e quello che lo salta con condizione `false`; perciò ci si può ritrovare con qualcosa del tipo `(`$\varepsilon$`+...)`.

```java
public int func(int x) {
	int y = 0;
	if (x >= y) 
		return y;
	int z = x/2;
	return z;
}
```

\- `x = du(`$\varepsilon$`+u)` -  $\varepsilon$ nel caso in cui ritorna `y` (e si ferma lì), altrimenti c'è l'uso in `z = x/2`. 

\- `y = du(u+`$\varepsilon$`)` -   qui se entra nell'`if` fa un uso altrimenti $\varepsilon$.

\- `z = (`$\varepsilon$`+du)` -   stessa cosa della `x`, $\varepsilon$ nel caso che entra nell'`if` e `z` non è neanche definita.

##### White box

Per questa parte è necessario generare degli input di test per fare in modo che coprano rispettivamente:

- Tutti gli *statement* ma non tutti i *branch*,
- Tutti i *branch* ma non tutte le *conditions*,
- Tutti *statement*, *branch* e *conditions*.

###### Statements

Per coprire tutti gli *statement* sono necessari 1 o più input che riescano a coprire ogni singola riga del codice senza seguire tutti i possibili percorsi in esso (*branch*); l'esempio principale è quando si ha un `if` senza `else`, in quel caso si possono avere degli input che passano per tutte le righe senza entrare nell'`else` implicito di quell'`if`.

###### Branches

Per coprire tutti i *branch* invece servono 1 o più input che coprano tutti i percorsi che il codice può seguire (anche condizioni `else` implicite) ma senza coprire tutte le condizioni; per esempio per un `if` all'interno di un ciclo, con 1 solo input ben studiato, è possibile fare in modo che ci entri in un'iterazione ed entri nell'else implicito nell'altra.

Quindi in caso di `if/else` **con 1 sola condizione**, <u>non è possibile coprire tutti i branch senza coprire tutte le conditions</u> (se `true` entra in `if` e se `false` entra in `else`).

###### Conditions

Infine, per coprire tutte le *condition* serve fare in modo che gli input rendano una volta `true` e una volta `false` ogni condizione; se però in un codice non ci sono `if` con più condizioni allora coprire solo i *branch* è impossibile, nel caso contrario invece bisognerà fare in modo che gli input coprano $2^{n}$ casi (con $n =$ numero delle condizioni consecutive).

> [!important] Attenzione
> Quando si vanno a valutare le *conditions*, bisogna valutarle <u>tutte</u>, non solo quelle importanti come quando si valuta per *modified conditions* (tipo con `&&` tra 2 condizioni basta valutare i casi di entrambe vere, 1a vera e 2a falsa e viceversa evitando entrambi falsi), con 2 condizioni si avranno da rispettare $2^{2} = 4$ casi sempre; per esempio:
> ![](https://i.imgur.com/VavxILz.png)
> In questo caso 

#### Domande Morasca

1\) es 4

![](https://i.imgur.com/exVP7rd.png)

![](https://i.imgur.com/MJBZsW0.png)

Non si capisce la spiegazione del set di input n° 1 (dice che non si può fare `i++` senza entrare nell'`else` implicito dell'`if` dentro al `for` ma cosa centra con gli *statement*? meglio dire che non si può fare tutto perché o ti fa `return false` dentro o ti fa `return true` fuori e mai tutti e 2).

Perché gli input sono A = {1} e B = {1,5,3}? Nel senso perché proprio questa configurazione? Cosa risolve a livello delle 3 richieste?

Avendo input A = {1} e B = {5,1}, se è possibile combinarli insieme per darli come soluzione come fatto nel punto 3, allora con essi è possibile il punto 1 perché faccio tutti gli statement senza entrare nel branch `else` implicito dell'`if`.

2\) es 13

![](https://i.imgur.com/VbdFMUO.png)

array = du(e+(uu)\*)

index = du(e+u(u)\*)

i = (e+du(uuudu)\*)

ret = d(u+((ud+e))\*u)

A = { array = \[ 1 ], index = 2 }

B = { array = \[ 2 ], index = 0 }

C = { array = \[ 1, 2 ], index = 1 }

D = { array = \[ -2, -1 ], index = 1 }

- statement ma no branch: { A, B }
- branch ma no condition: { A, C } 
- tutti statement, branch e condition: { A, C, D }

array = duu(uuu(uuudud+e)uu)\*

count = d((ud+e))\*u   ||   d((ud))\*u

i = duu(uu(uuuu+e)uduu)\*

temp = ((du))*

A = { array = \[ 1,-1 ] }

B = { array = \[ 1,1,0,-1 ] }

C = { array = \[ 0,1 ] }

D = { array = \[ 1 ] }

- statement ma no branch: { A }
- branch ma no condition: { B } 
- tutti statement, branch e condition: { B, C, D }

if (cond1 && cond2) 

<u>VV</u> / VF / FV / <u>FF</u>

### 3 - UML

#### Metodo

##### Use-Case

1\) Identificare attori

2\) Identificare use-case

3\) Fare diagramma

#### Esercizi

##### Es 1

Esercizio sistema studenti università:

1\) Attori: studenti, docenti, Consiglio, coordinatore Erasmus, segreteria

2\) Use cases

Studente: 

