# Lezione 12

### Porte logiche

Sono dei piccoli dispositivi dotati di cavi di input e di output. Funzionamento:

1) Viene immesso un segnale binario in <u>input</u>,
2) (Dopo frazioni di nanosecondi) esce un altro segnale in <u>output</u>.

Inoltre:

- Input e output sono codificati allo stesso modo (configurati per operare con una stessa grandezza fisica),
- Finché l'input resta invariato, altrettanto fa l'output.

##### Tipi di porte logiche

Ogni porta logica implementa una <u>funzione logica</u>. Le porte sono classificabili in base a:

- Il loro <u>n° di ingressi</u>: **unarie** (1 input), **binarie** (2 input), **ternarie** (3 input)... (una porta a *n* ingressi implementa una funzione logica a *n* variabili).
- La <u>funzione implementata</u>: **AND**, **OR**, **NOT**...

#### Circuiti digitali

Collegando gli output di 1 porta logica agli input di un'altra si costruiscono dei circuiti logici, i quali possono essere di 2 tipi:

###### Circuiti combinatori

Sono <u>privi di retroazioni</u>:

- Il segnale viaggia da input a output a <u>senso unico</u>,
- C'è una <u>gerarchia</u> (ordinamento parziale) tra le porte,
- <u>Aciclici</u> (nessun ciclo).

###### Circuiti sequenziali

<u>Hanno retroazioni</u>, ovvero, quando un segnale esce da una porta, esso torna indietro (anche se passato da altre porte nel mentre).

![](https://i.imgur.com/3epX4Zw.png)

##### Quali porte logiche usare?

Sarebbe opportuno usare l'insieme di porte logiche più piccolo possibile per realizzare qualunque funzione così da minimizzare i costi. L'insieme più usato (sebbene non il + piccolo) è composto da **AND**, **OR** e **NOT**.

(altra slide mortombo)

### Caratteristiche di porte e circuiti

##### Costo di una porta logica

Il **costo** di una porta logica dipende dal numero di *transistor* necessari per realizzarla, e tale numero dipende dalla tecnologia, funzione e numero di ingressi della porta. Esempi:

- NOT: 1 o 2 transistor,
- AND/OR: 3 o 4 transistor,
- Resto: >= 4 transistor.

###### Criteri di costo di un circuito

Il costo di un circuito digitale si valuta in base a vari criteri di costo:

- Numero totale di porte usate, 
- Altri... (n° di porte universali (NAND, NOR), numero totale di *transistor*...)

##### Velocità di un circuito digitale

> [!important] Tempo di commutazione
> La velocità di un circuito è definita con il tempo che il dispositivo ci mette a generare l'output dopo aver ottenuto un input; il quale è detto **tempo di commutazione**. Il tempo di commutazione può riferirsi a:
> - Un **circuito**: max tempo di commutazione di tutti i percorsi da input a output,
> - Un **percorso**: somma dei tempi di commutazione delle porte attraversate,
> - Una **porta**: dipende da tecnologia, funzione e n° di input della porta (le più veloci sono NAND e NOR).

###### Velocità, latenza e ritardo di un circuito combinatorio

Per calcolare la velocità di una rete combinatoria serve conoscere i ritardi di propagazione delle porte logiche che compongono la rete e poi serve anche analizzare tutti i percorsi input output.

Latenza = 1/tempo di commutazione \[s/ms/us/ns] (quante volte al secondo si può calcolare la funzione logica associata).

La latenza si misura in secondi (meglio in nanosecondo), mentre la frequenza (n° di volte al secondo) si misura in Hz e multipli (Hertz).

# Esercizi

# Soluzioni

---

Prossima lezione: [[13 - Tipi di porte e tavole di verità]]

