# Lezione 25

### ALU

Una ***Arithmetic Logic Unit*** (**ALU**) è un circuito combinatorio multifunzione capace di eseguire diversi compiti (logico-matematici) condizionalmente (in base a un comando).

**Input**: 

- <u>2+ operandi</u> (di *n* bit ciascuno), 
- <u>1 codice comando</u> di *k* bit (per $2^{k}$ comandi),
- (A volte) <u>1 bit extra</u> usato come $C_{in}$ (riporto di ingresso) nelle somme.

**Output**:

- Il risultato dell'operazione eseguita (sempre in *n* bit),
- Alcuni bit di esito (tipo per [[24 - Shifters#Overflow|overflow]]).

###### Schema

Normale:

![](https://i.imgur.com/aWugd49.png)

Astratto ($F_{n}$ sono le funzioni scelte in base al codice comando):

![](https://i.imgur.com/AF2l8MM.jpeg)

###### Funzioni

![](https://i.imgur.com/AxykP1F.png)

##### 1-bit ALU

![](https://i.imgur.com/E0g5kRr.png)

##### Altro

###### Note

- Le ALU reali (odierne) <u>operano su numeri molto più grandi di bit</u> (<u>8, 16, 32, 64</u>),
- Solitamente, gli <u>operatori</u> hanno lo <u>stesso n° di bit del risultato</u>,
- Alcune ALU possono eseguire anche <u>operazioni complesse</u> (tipo radici, potenze, funzioni trigonometriche...)...

###### Scelte progettuali base

Nella progettazione di circuiti complessi (quali le ALU) ci si chiede: *quante operazioni implementare? e quanto complesse?*. Infatti bisogna tenere da conto che:

- ALU con <u>operazioni complesse</u> (dato che i circuiti sono in parallelo) sono **più lente** (oltre che **più costose**), anche nelle operazioni semplici.
- ALU che supportano <u>operazioni semplici</u>, seppur **più veloci**, necessitano di eseguire **più operazioni semplici per** portare a termine **quelle più complesse**.

# Esercizi

# Soluzioni

---

Prossima lezione: [[26 - Blocchi funzionali sequenziali]]

