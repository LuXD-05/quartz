# Lezione 17

### Alberi Red-Black

Gli alberi RB sono degli alberi in cui:

- Ogni nodo contiene <u>1 valore</u> e <u>1 colore</u> (rosso o nero, questo può essere considerato colore del valore o del collegamento del nodo al padre a favore) e la <u>root è sempre nera</u>,
- <u>Non possono esistere 2 nodi rossi consecutivi</u> (uno padre dell'altro) e/o <u>ogni percorso nodo-nipote ha almeno 1 nodo/lato nero</u> (stessa cosa),
- <u>Ogni percorso</u> dalla radice ad una foglia deve avere lo <u>stesso n° di nodi/lati neri</u>.

##### Proprietà

Dato un albero 2-3-4 di altezza $h$, per attraversare ogni suo nodo ci servono max 2 nodi RB, quindi ogni albero RB equivalente ad esso ha altezza massima: 

$$2h$$
Per le considerazioni riportare [[#Corrispondenza con alberi 2-3-4|qui di seguito]], si stabilisce che un albero RB con $n$ valori ha altezza $O(\log n)$, perciò gli alberi RB sono **bilanciati**.
##### Operazioni
###### Inserimento
Per l'inserimento è necessario seguire le seguenti regole:
1) <u>Tutti i nodi si inseriscono come foglie rosse</u> (quindi sempre alla fine del percorso calcolato dopo circa $\log(n)$ confronti),
2) Se il nodo inserito ha <u>padre rosso</u>, bisogna **invertire i colori di quel percorso**/sottoalbero per fare in modo di avere lo stesso n° di nodi neri in ogni percorso,
3) Se poi il nodo è inserito quando il <u>livello del padre non è saturo</u>, allora bisogna **ribilanciare l'albero**:
   ![](https://i.imgur.com/lL3AYSg.png)
###### Cancellazione

#### Corrispondenza con alberi 2-3-4
Ad ogni [[16 - Alberi 2-3-4|albero 2-3-4]] corrisponde almeno 1 albero RB. Di seguito una mappa generale per le conversioni di nodi 2-3-4 con 2, 3 e 4 figli:
![](https://i.imgur.com/61uHY8l.png)
> [!question] Quanti alberi RB sono traducibili in un certo 2-3-4?
> Dall'immagine suddetta, la corrispondenza per nodi con 2 e 4 valori è biunivoca (1 sia per RB che per 2-3-4), mentre per nodi con 3 valori (**3-nodi**) ci sono 2 possibilità. 
> Per questo il n° di alberi RB traducibili in un certo 2-3-4 corrisponde a:
> $$2^{\#3nodi}$$

# Esercizi

##### 1) Costruzione alberi RB

###### 1.1) Costruire l'abero RB

Costruisci l'albero RB data la sequenza: 4, 8, 1, 10, 3, 2, 5, 6, 7, 9

##### 2) Cancellazione alberi RB

###### 2.1) Cancella valori dall'albero RB

##### 3) Trasformazione in 2-3-4 e viceversa

###### 3.1) Da RB a 2-3-4

Trasforma l'albero dell'esercizio [[#1.1) Costruire l'abero RB]] in un albero 2-3-4.

# Soluzioni

##### 1)

###### 1.1)

![](https://i.imgur.com/t093GKF.png)

##### 2)

###### 2.1)

##### 3)

###### 3.1)

![](https://i.imgur.com/CFTIBAe.png)

Domanda:

**Tra quali estremi è compresa l'altezza `H` di un albero RB con `n` nodi? Perché?**

###### 🔴 Step 1 – Collegamento con albero 2-3-4

Gli **alberi Red-Black (RB)** simulano il comportamento di **alberi 2-3-4**.  

Ogni **nodo 2-3-4** può contenere 1, 2 o 3 chiavi → quindi possono rappresentare da 2 a 4 figli.

> [!info] Idea chiave 
> Ogni **nodo 2-3-4** può corrispondere a **1, 2 o 3 nodi** RB disposti lungo un cammino.
> Quindi:
> Se un albero 2-3-4 ha altezza `h`, l'albero RB corrispondente ha altezza al massimo `2h`.

###### 🧮 Step 2 – Quanti nodi può avere un albero 2-3-4?

Un albero 2-3-4 **perfettamente bilanciato** con altezza `h` può avere:

- **Minimo**: se tutti i nodi sono 2-nodi (con 1 chiave → 2 figli) $n \geq 2^h+1 - 1$,
- **Massimo**: se tutti sono 4-nodi (con 3 chiavi → 4 figli) $n \leq 4^h+1 - 1$.

Quindi: `2^(h+1) - 1 ≤ n ≤ 4^(h+1) - 1`

###### ➗ Step 3 – Isolare `h`

Invertiamo le disuguaglianze:

1) Partiamo da: $2^(h+1) - 1 \leq n \rightarrow 2^{(h+1)} \leq n + 1 \rightarrow h + 1 \leq log_{2}(n + 1) \rightarrow h \leq log_{2}(n + 1) - 1$
2) E: $n \leq 4^(h+1) - 1 \rightarrow n + 1 \leq 4^(h+1) \rightarrow h + 1 \geq log₄(n + 1) \rightarrow h \geq log₄(n + 1) - 1$,
3) $log_{4}(n + 1) - 1 \leq h \leq log_{2}(n + 1) - 1$

###### 🔴 Step 4 – Torniamo all'albero RB

Ricorda che l'albero RB può avere **altezza doppia** rispetto al 2-3-4 ($h \in [h, 2h]$).

Sostituiamo gli estremi trovati per `h`:

- Estremo inferiore: $h \geq log_{2}(n + 1) - 1$
- Estremo superiore: $h \leq 2 * (log_{2}(n + 1) - 1) = 2log_{2}(n + 1) - 2$

###### Risultato finale

L'altezza $h$ di un albero RB con $n$ nodi è compresa tra:

$$log_{4}(n + 1) - 1 \;\leq\; h \;\leq\;  2log_2(n + 1) - 2$$

---

Prossima lezione: [[]]

