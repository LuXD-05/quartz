# Lezione 13

### Package diagrams

I ***packages*** sono dei "contenitori" (generalmente) di classi UML (raggruppano *class diagrams* spesso) e definiscono un *namespace* all'interno di essi all'interno del quale i nomi devono essere diversi e ci sono interfacce precise per accedere dall'esterno al package.

![](https://i.imgur.com/eN1CnhQ.png)

Questi esistono per modellare in modo migliore sistemi complessi e gerarchici grazie ad alta coesione interna ed interfacce precise.

##### Relazioni

Tra package possono esistere delle relazioni che "riassumono" altre relazioni *dello stesso tipo* tra gli elementi all'interno di 2 package (in pratica 1 freccia di un certo tipo tra 2 package generalizza indicando che dipendenza c'è tra il package $A$ e il package $B$ in base alle relazioni che hanno); alcuni esempi:

- **Generalizzazione**: se c'è almeno 1 generalizzazione tra $A$ e $B$ (se almeno 1 classe in $A$ ne estende 1 in $B$ e viceversa),
- **Dipendenza**: se c'è almeno 1 relazione di dipendenza tra gli elementi di $A$ e di $B$ (se almeno 1 classe di $A$ dipende da una di $B$ e viceversa),
- **Aggregazioni**: se un package contiene un altro package,
- ***Merge***: simile alla generalizzazione (?), si ha quando si vogliono combinare 2 package in 1 (tipo il `merge` di git) ed eventuali conflitti (*delta*) per nomi uguali tra i 2 package vanno risolti.

##### Dipendenze

Le dipendenze tra package devono essere tutte esplicite in quanto non è detto che se il package $B$ ha elementi pubblici allora il package $A$ può accedervi, in più le relazioni non sono transitive, ovvero se $A$ può accedere a $B$ e $B$ può accedere a $C$, non è detto che $A$ possa accedere a $C$. 

Per queste, UML definisce 2 stereotipi, `<<access>>` e `<<import>>`:

![](https://i.imgur.com/7mvl9a3.png)

A livello di linguaggio si vede la differenza che `String` è sempre disponibile di base, mentre `Time` generalmente va importato.

###### Access

Lo stereotipo `<<access>>` indica che il package da cui parte la freccia può accedere agli elementi del package target, tuttavia serve usare il nome del package target (perciò `<<access>>` non modifica il namespace del client e non crea riferimenti).

###### Import

Lo stereotipo `<<import>>` invece aggiunge al namespace del package client gli elementi del package target, quindi il client può usarli come se fossero suoi, tuttavia c'è la necessità che non ci siano conflitti tra i nomi delle classi. `<<import>>` permette inoltre di importare elementi rinominandoli con alias:

![](https://i.imgur.com/r3PXZeP.png)

---

Prossima lezione: [[14 - State diagrams]]

