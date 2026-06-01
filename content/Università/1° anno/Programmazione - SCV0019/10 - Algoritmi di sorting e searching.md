# Lezione 10

### Algoritmi

C'è una scienza dietro gli algoritmi di ordinamento (***sorting algorithms***) e di ricerca (***searching algorithms***) per studiarne e migliorarne sempre di più l'efficienza.

##### Sorting

###### Bubble sort

Il bubble sort consiste nell'ordinare un'array nella maniera più classica: confrontare coppie di elementi adiacenti e scambiarle se non sono nell'ordine giusto:

![](https://i.imgur.com/QOyq8Zk.png)

Questo si ripete per più iterazioni finché l'array non è completamente ordinato.

```java
public static <T extends Comparable<? super T>>	void sort(T[] a) {
	T temp;
	boolean scambiato;
	do {
		scambiato = false;
		for (int i = 1; i < a.length; i++) {
			if (a[i - 1].compareTo(a[i]) > 0) {
				temp = a[i - 1];
				a[i - 1] = a[i];
				a[i] = temp;
				scambiato = true;
			}
		}
	} while (scambiato);
}
```

##### Searching

# Esercizi

# Soluzioni

---

Prossima lezione: [[11 - Memoria]]

