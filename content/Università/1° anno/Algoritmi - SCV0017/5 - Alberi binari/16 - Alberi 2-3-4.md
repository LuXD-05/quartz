# Lezione 16

### Alberi 2-3-4

Gli **alberi 2-3-4** sono alberi dove gli elementi risiedono in nodi e foglie in maniera ordinata e in cui:

- Ogni nodo ha <u>min 1 valore e al max 3</u>,
- Ogni **nodo interno con *i* valori ha *i* + 1 figli** (regola *i + 1* $\;\rightarrow\;$ 3 valori = max 4 nodi figli),
- Tutte le <u>foglie</u> sono <u>sullo stesso livello</u>,
- Sono <u>ordinati</u> (i + 1 intervalli associati a i + 1 sottoalberi).

##### Proprietà

Avendo $n$ dati in un albero 2-3-4 di altezza $h$ si ha:

$$2^{h + 1} - 1 \;\leq\; n \;\leq\; 4^{h + 1} - 1$$

Perciò:

$$h = \log(n)$$

Anche gli alberi 2-3-4 sono **bilanciati** (altezza = $O(\log(n))$).

##### Operazioni

###### Inserimento

Per inserire elementi negli alberi 2-3-4 si parte dalla radice e (come negli [[15 - Alberi 2-3#Inserimento|alberi 2-3]]) si scende fino ad una foglia in base a confronti; da lì, prima dell'inserimento:

- Se la foglia ha <u>meno di 3 elementi</u>: nessun problema,
- Se la foglia ha <u>3 elementi</u>: bisogna <u>splittarla e ribilanciare l'albero</u>, ovvero: 

  1\) Rendere il valore centrale un fratello del padre (in caso il padre abbia 3 valori questa procedura continua risalendo),
  2\) Inserire l'elemento nella foglia,
  3\) Splittare ed eventualmente rifare i collegamenti tra le foglie ed il padre:
  ![](https://i.imgur.com/jGODIeR.png)

###### Cancellazione

La cancellazione è simile a quella nei [[14 - BST#Cancellazione in BST|BST]] e inizia con la ricerca del nodo/foglia $n$ che contiene il valore $x$ e se trovato:

- $n$ è una <u>foglia con 2 o 3 valori</u>: **cancella** senza problemi,
- $n$ è una <u>foglia con 1 valore</u>: **cancella e ribilancia**,
- $n$ è un <u>nodo interno</u>: **cerca un sostituto** per $x$ (*minmax* o *maxmin*) e nel nodo in cui lo trova si comporta come nei casi precedenti (2/3 = cancella, 1 = cancella e ribilancia):

  ![](https://i.imgur.com/6ZZhuR0.png)

###### Bilanciamento

Il **bilanciamento** è una funzione che si attua quando è necessario ribilanciare un albero 2-3-4 non bilanciato (tipo dopo cancellazione) con nodo vuoto $n$ e agisce secondo 3 casi:

1) $n$ ha un <u>fratello con 2 o 3 valori</u>: si prende il valore max o min (in base a $n$ se fratello maggiore o minore) lo si promuove al padre ed il valore sempre nel padre che prima separava $n$ e il fratello, va in $n$:

   ![](https://i.imgur.com/DFB5gRa.png)

2) Il <u>padre</u> di $n$ ha <u>2 o 3 valori</u>: $n$ viene eliminato ed il valore di separazione tra esso ed un altro suo fratello con 1 valore viene ceduto a tale fratello:

   ![](https://i.imgur.com/Xweh3tt.png)

3) <u>Padre e fratello</u> di $n$ hanno <u>1 valore</u>: i valori di padre e fratello si uniscono nel padre e si ribilancia il resto dell'albero a salire:

   ![](https://i.imgur.com/ihCU5qy.png)

##### Codici di operazioni

###### Insert

```java
public static void Insert(Node n, T x) {

	if (n.children.size() == 3) {                 // Splitta preventivamente in caso di 3 figli
		
		Node parent = Split(n);                   // Prende il valore centrale e assegna ("promuovendolo") al padre
		
		if (x < n.promotedValue)                  // Inserisce in n se < del valore promosso, altrimenti nel padre (poi scenderà)
			Insert(n, x);
		else 
			Insert(parent, x);
		
	}

	if (n.isLeaf())                               // Aggiunge se in una foglia 
		n.add(x);
		
	else if (x < n.first)                         // Se x < 1° valore --> prova a inserire a sinistra del 1°
		Insert(v.first, x);
		
	else if (n.second == null || x < n.second)    // Se c'è 2° val e x < 2° val --> prova a inserire al centro
		Insert(n.second, x);
		
	else                                          // Se no inserisce nel 3°
		Insert(n.third, x);

}
```

La complessità della `insert()` è $\Theta(\log (n))$ in quanto si scorre un'intero percorso (fatto da $\log(n)$ nodi, quindi confronti da fare) dell'albero per posizionare un valore.

###### Delete

???

###### Balance

???

# Esercizi

##### 1) Costruzione alberi 2-3-4

###### 1.1) Costruire albero 2-3-4

##### 2) Inserimento alberi 2-3-4

###### 2.1) Inserimento in albero 2-3-4

##### 3) Cancellazione alberi 2-3-4

###### 3.1) Cancellazione e ribilanciamento in albero 2-3-4

Cancellare la i nodi 50, 38, 27, 33, 95, 47 del seguente albero 2-3-4:

![](https://i.imgur.com/ILg1UQ1.png)

# Soluzioni

##### 1)

###### 1.1)

##### 2)

###### 2.1)

##### 3)

###### 3.1)

Delete(50):

![](https://i.imgur.com/Ot8Cd5j.png)

Delete(38) + Delete(27):

![](https://i.imgur.com/aqgR5mK.png)

Delete(33):

![](https://i.imgur.com/tEAp83E.png)

![](https://i.imgur.com/EuGkGAq.png)

Delete(95):

![](https://i.imgur.com/gm5d8aq.png)

Delete(47):

![](https://i.imgur.com/xTObWYh.png)

---

Prossima lezione: [[17 - Alberi RB]]

