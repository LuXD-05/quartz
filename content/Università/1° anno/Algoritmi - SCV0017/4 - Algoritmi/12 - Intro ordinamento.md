# Lezione 12

### Ordinamento: introduzione

Gli <u>algoritmi di ordinamento</u> mirano a disporre elementi di una sequenza in un certo modo in base a un certo criterio. Questi si dividono in:

- **Elementari**: i quali ordinano sequenze mediante operazioni di **confronto** e **assegnamento/scambio**,
- **Digitali**: che si basano sui **bit** (singoli o gruppi) di ogni elemento per l'ordinamento della sequenza.

> [!info] Caratteristiche
> Un algoritmo di ordinamento può essere:
> - **Stabile**: se mantiene l'ordine degli elementi di ugual valore (ovvero non scambia valori uguali),
> - **Adattivo**: non effettua operazioni di scambio/confronto inutili (meno complessità quanto più parzialmente è ordinato l'input),
> - **Ottimale**: (se la sua complessità è la migliore possibile per la sua categoria di problemi ???)

###### Inversioni

In una sequenza, un'**inversione** è uno <u>scambio di 2 elementi</u> in base ad un criterio ai fini di ordinamento. In una qualsiasi sequenza $S$, il numero di inversioni $N_{i}(S)$:

$$0 \leq N_{i}(S) \leq \dfrac{n \cdot (n-1)}{2}$$

Dove:

- $N_{inv}(S) = 0 \;\rightarrow\;$ implica che $S$ è <u>ordinata</u>,
- ${} N_{inv}(S) = \frac{n \,\cdot\, (n-1)}{2} \;\rightarrow\; {}$ implica che $S$ è <u>ordinata al contrario</u>.

> [!important] Calcolare le inversioni
> Ci sono 2 modi per calcolare il n° di inversioni in una qualsiasi sequenza $S$:
> - Per ogni elemento $x$ in $S$ contare il n° di elementi minori di $x$ e alla sua destra ${} d_{x} {}$ (che vengono dopo di lui): $N_{i}(S) = \sum\limits_{x \in S} d_{x}$.
> - Per ogni elemento $x$ in $S$ contare il n° di elementi minori di $x$ e alla sua sinistra $s_{x}$ (prima di lui): $N_{i}(S) = \sum\limits_{x \in S} s_{x}$.
> ![](https://i.imgur.com/CZSI9Cj.png)

###### Albero di decisione

Per qualsiasi sequenza esiste un albero binario detto **albero di decisione** che, grazie a confronti binari nei nodi, permette di ottenere tutti i possibili ordinamenti della sequenza (nelle foglie). Vediamo l'esempio di una sequenza $A$ con 3 elementi:

###### Numero minimo di confronti

Dato che un albero di altezza $h$ ha massimo $2^{h}$ foglie si determina che il **n° minimo di confronti** (<u>nodi di un percorso</u> verso una foglia) sarà $\log_{2}(k)$ dove $k$ è il n° di **foglie** (o di <u>possibili ordinamenti della sequenza</u>) dell'albero. 

![](https://i.imgur.com/hmitjQD.png)

Quindi:

- $h$ = altezza dell'albero,
- $2^{h}-1$ = n° massimo di nodi,
- $2^{h}$ = n° massimo di foglie (permutazioni),
- $\log_{2}(k)$ = n° minimo di confronti (o di nodi di un percorso) per arrivare ad una foglia (con $k$ = n° di foglie o di possibili ordinamenti della sequenza). Vale sempre:$$h \geq \log_{2}(k)$$

> [!example] Permutazioni
> I <u>possibili ordinamenti (foglie)</u> sono anche detti **permutazioni** della sequenza e dati $n$ elementi in essa, le permutazioni sono $n!$
> Infatti prendiamo come esempio 3 numeri $A$, $B$ e $C$, le possibili permutazioni di questi sono: $ABC, ACB, BAC, BCA, CAB, CBA$, ovvero $3! = 6$ (l'esempio si riferisce alla 1a immagine dell'albero e non a quella subito qui sopra).
> Facendo $\log_{2}(6) = 2.58$, il che indica che nel caso peggiore ci vogliono almeno 3 confronti per ordinare la sequenza in un certo modo.

###### Lower bound

Avendo $n!$ permutazioni è possibile costruire un albero decisionale i cui nodi (confronti) permettono di discernere ogni percorso che porta ad una foglia (possibile ordinamento):

![](https://i.imgur.com/o8yDU0a.png)

L'**altezza** di tale albero nel caso peggiore corrisponde al <u>n° di confronti necessari ad ordinare la sequenza</u>; ed è $\log_{2}(n!)$. Grazie all'[approssimazione di Stirling](https://it.wikipedia.org/wiki/Approssimazione_di_Stirling) si riesce a definire un ***lower bound*** (limite inferiore) per il <u>n° minimo di confronti</u> di qualsiasi algoritmo di ordinamento elementare nel caso peggiore; il che è:

$$\Omega(\log_{2}(n!)) \approx \Omega(n \log_{2}n)$$

##### Classe algoritmi java

```java
// "Algoritmo" sarà il nome della classe per ogni specifico algoritmo
public class Algoritmo {

	// "sort()" sarà il metodo principale con la logica di ordinamento dell'algoritmo
	public static void sort(Comparable[] arr) {
		//...
	}

	// Ritorna true se x < y
	public static void less(Comparable x, Comparable y) {
		return x.compareTo(y) < 0;
	}

	// Scambia i valori agli indici i e j in arr
	public static void exchange(Comparable[] arr, int i, int j) {
		Comparable _ = arr[i];
		arr[i] = arr[j];
		arr[j] = _;
	}
	
}
```

---

Prossima lezione: [[13 - Algoritmi di ordinamento]]

