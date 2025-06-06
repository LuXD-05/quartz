# Lezione 9

#### Algebra eterogenea

Con "algebra eterogenea" si denota una struttura composta da vari insiemi di con tipi di dati diversi ed un'insieme di operazioni che agiscono su questi. Prendiamo ad esempio un insieme $A$; per rappresentare esso e le sue parti ($P(A)$) abbiamo bisogno di 3 operazioni: `member(x, A)` che dice se $x \in A$, `insert(x, A)` che inserisce $x$ in $A$ e `delete(x, A)` che rimuove $x$ da $A$.

Continuando si introduce $P(A)_{O}$, ovvero l'insieme delle parti di $A$ ordinato, il quale dispone di altre operazioni quali `min()`, `max()`... Per implementare algebre eterogenee come l'insieme $P(A)$ si possono usare:

- ***Linked lists***: semplici, ma in media le operazioni costano $O(n)$,
- ***Hash tables***: in media le operazioni costano $O(1)$ (se non si sbaglia ad impostare certi parametri, in quel caso $O(n)$).

### Tabelle hash

Una ***hash table*** è una struttura dati fatta da un array lungo $n$ (dove in ogni posizione c'è una lista di elementi che hashano ad essa) + un intero che indica il n° di elementi in esso ($\leq n$). La dimensione della tabella hash può essere fissa (**hash statico**) o variabile (**hash dinamico**). Inoltre, in base a dove sono memorizzati i dati ci sono 2 metodi di gestione:

- **Concatenazioni separate**: i dati stanno in <u>liste concatenate</u> e la <u>tabella hash contiene i riferimenti</u>,
- **Indirizzamento aperto**: i dati stanno <u>direttamente nella tabella hash</u>.

###### Caratteristiche

- Ogni dato è distinto da una *key* che determina una posizione in tabella,
- Il n° di *key* possibili è molto elevato: $\Theta(2^{|c|})$, dove $c$ è la lunghezza in bit della chiave ($n << k$),
- Ogni posizione della tabella lunga $n$ è identificata da un **indirizzo** $i$ compreso tra $0$ e $n-1$,
- Una **funzione di hash** <u>trasforma le key in indirizzi</u>.

##### Funzioni di Hash

Trasformando *key* in indirizzo, la funzione di hash è usata per trovare la posizione di un dato nella tabella e deve rispettare certe caratteristiche:

- **Efficienza**: essere <u>facile/veloce da calcolare</u> (costo $O(|c|)$),
- **Distribuzione uniforme**: delle chiavi su $n$ indirizzi (hashando una chiave, <u>ogni indirizzo deve avere la stessa probabilità</u> $\tfrac{1}{n}$ <u>di essere scelto</u>),
- **Determinismo**: l'indirizzo calcolato deve dipendere da tutti i bit di $c$, perciò la <u>stessa chiave da sempre lo stesso risultato</u>.

> [!example] Esempi
> La **funzione identità** $H(c) = c$ non va bene dato che $n << k$ (quindi con una *key* molto grande rischio di trovare un indice fuori dai limiti della tabella).
> La **funzione costante** $H(c) = r$ (dove $r$ è un reale qualsiasi) non va bene perché avendo tutte le chiavi che danno lo stesso risultato si hanno collisioni (diventa *linked list*).
> Una **funzione modulo** $H(c) = c_{n}$ potrebbe funzionare scegliendo bene $n$, però multipli di $c$ e $n$ hanno collisioni facendo $c \% n$.
> Perciò di solito per la stessa $H(c) = c_{n}$ si usano **numeri primi** così da non avere problemi coi multipli.

###### Hash di stringhe

...

###### Esempi di funzioni hash

```java
public static int Hash(String s) {

	int m = 0;
	char c;
	
	for (int i = 1; i <= s.length; i++) {    // Per ogni char in stringa
		c = v.charAt(i);                     // Prende char
		m = (ALPHA * m + (int)c) % TAB;      // ALPHA = ??? | TAB = ??? | m = ??? | c = valore int ASCII del char
	}

	return m;

}
```

##### Collisioni

Una funzione di hash è necessariamente "N a 1" (nel senso che applicandola a *key* diverse si può ottenere lo stesso indice); perciò bisogna gestire le collisioni, che ci sono quando:

$$x \neq y \;\land\; H(x) = H(y)$$

###### Hash statico con concatenazioni separate

Si utilizza una tabella $T$ di dimensione fissa $n$ e una lista concatenata $L$. $L$ contiene dati sottoforma di coppie chiave-valore e ogni elemento di $T$ ha un riferimento al 1° nodo di $L$ la cui chiave $c$ permetta: $H(c) = i$ (quindi all'indice $i$ di $T$ ci sarà un puntatore all'elemento $j$ di $L$ la cui chiave hashata da $i$). Metodi: 

- `member(x)` scorre la lista in $T[i]$ (dove $i = H(x.key)$) fino a trovare $x$,
- `insert(x)` inserisce all'inizio della lista in $T[H(x.key)]$,
- `delete(x)` come `member()` ma quando trova $x$ lo cancella.

> [!info] Nota
> Se la funzione hash rispetta tutte le 3 caratteristiche e $T$ ha dimensione $n$ e contiene $m$ dati, la lunghezza media di ogni lista in $T[i]$ sarà $\dfrac{m}{n}$.
> Per l'uso di liste, ogni operazione costa come farla su lista normale; se poi si ha una stima del n° di dati attesi, si ha in media un costo di $O(1)$ scegliendo $n \approx m$.
> \[TEOREMA]...

###### Hash statico con indirizzamento aperto

Con i dati inseriti direttamente in $T$ (array di $n$ elementi), essa deve avere $n \geq m$ (dimensione $\geq$ dati attesi). Siccome in ogni $T[i]$ c'è un dato e non una lista, sorge il problema delle collisioni quando:

- `insert(x)`: ma $T[H(x.key)] \neq$ `null` (ovvero quando in $T[H(x.key)]$ c'è già un elemento),
- `member(x)` e `delete(x)`: quando $T[H(x.key)] = y$ e non $x$ (ovvero quando cerco/elimino $x$ accedendo a $T$ tramite l'hash della sua *key* ma mi ritorna $y$ e non $x$).

> [!important] Come si fa?
> ###### Sondaggi
> In caso di collisione quindi vengono effettuati sondaggi in $T$, ovvero vengono cercate altre posizioni libere ($h_{i}(c)$) nella tabella in base ad una strategia $F$ usata nella formula:
> $$h_{i}(c) = (Hash(c) + F(i)) \; \% \; m$$
> Alcune strategie di sondaggio sono:
> - **Scansione lineare**: dove $F(i) = i \; \rightarrow$ ovvero se $T[1]$ è occupato, si cercherà in $T[1 + i]$ e così via,
> - **Scansione quadratica**: dove $F(i) = i^{2} \; \rightarrow$ ovvero se $T[1]$ è occupato, si cercherà in $T[1 + i^{2}]$ e così via,
> - **Hash doppio**: dove $F(i) = i \cdot H_{2}(c) \; \rightarrow$ ovvero se $T[1]$ è occupato, si cercherà in $T[1 + i \cdot H(c)]$ e così via.
> ###### Fattore di carico e prestazioni
> Il costo delle operazioni `member(x)`, `insert(x)` e `delete(x)` dipende da: 1) il **fattore di carico** $\alpha = \frac{m}{n}$, 2) la **dimensione dei *cluster*** (gruppi contigui di celle occupate) e 3) dalla **strategia** $F$ di **gestione delle collisioni**.
> ![](https://i.imgur.com/rHQSlLo.png)
> ![](https://i.imgur.com/RV0rZwK.png)
> ![](https://i.imgur.com/QhTbUzM.png)

###### Hash dinamico

Con queste, l'idea è che appena $\alpha = 1$ ($T$ piena) se ne crea una nuova grande $2n$ (eliminando la 1a) e reinserendone i dati nella 2a (o quando piena per $\frac{1}{4}$ si fa lo stesso con $\frac{n}{2}$).

> [!info] Costo ammortizzato
> Data una tabella $T$ di dimensione $n$, solo all'inserimento dell'$n$-esimo elemento bisogna creare una $T$ grande $2n$ e riallocare i dati. Perciò si finisce quando:
> $$n \cdot 2^{k-1} < m \leq n \cdot 2^{k}$$
> Ovvero dopo che si ha raddoppiato la tabella $k$ volte ed aver superato i dati $m$. Il costo di ogni inserimento è $O(1)$ tranne quando l'inserimento scatena il raddoppio della tabella, in quel caso è $O(n \cdot k)$ (con $k$ che aumenta in base al n° di raddoppi).
> Siccome si fanno tanti inserimenti normali $O(1)$ e pochi raddoppi, se ne deriva che il **costo ammortizzato** di un qualsiasi elemento in generale è $O(1)$.

---

Prossima lezione: [[11 - Attraversamento degli alberi]]

