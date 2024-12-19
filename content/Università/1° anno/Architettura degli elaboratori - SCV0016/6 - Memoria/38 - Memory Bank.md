# Lezione 38

### Memory bank

Un ***memory bank*** (o *banco di memoria*) è un blocco funzionale capace di memorizzare un certo numero $m$ di parole in un certo numero $n$ di bit ciascuna ($n \times m$). 

Ogni *bank* è composto da 1 o più ***memory chip***, singole unità di memoria di cui si specificano:

- **Capacità**: ovvero le dimensioni in bit, ottenuta dal prodotto tra il n° di *word* memorizzabili ed il n° di bit per *word*,
- **Funzioni**: *read/write* o *read-only*,
- **Numero di porte di accesso**.

###### Bus dati bidirezionale

Di solito i *memory bank* usano 1 solo **bus dati bidirezionale** *read/write*. Serve quindi che il *bank* impedisca l'interferenza fra entrate e uscite del bus; e ciò si fa con il ***tri-state buffer*** (impedisce anche l'interferenza tra uscite dei vari chip).

##### Tri-state buffer

Il **tri-state buffer** è un dispositivo che funziona come un'interruttore:

- Quando $E = 1$, il valore dell'uscita $U$ corrisponde a quello dell'ingresso $I$,
- Quando $E = 0$, il segnale non passa e si dice che il dispositivo è in stato di alta impedenza ($Z$), che isola elettricamente l'uscita.

**Ingressi**: $I$ (ingresso segnale), $E$ (*Enable*, a 1 passa segnale, a 0 isola).

**Uscite**: $U$ (uscita segnale).

![](https://i.imgur.com/IRSjEVi.png)

![](https://i.imgur.com/Vo5OkVw.png)

###### MUX

Si può usare un [[20 - Decoder#Decoder|DEC]] in combinazione a $n$ *tri-state buffer* per implementare un [[21 - Multiplexer#Multiplexer|MUX]]:

![](https://i.imgur.com/v7MPKJx.png)

Tuttavia, non è una soluzione necessariamente veloce.

#### Memory chip

Il seguente è lo schema funzionale di un *memory chip*:

![](https://i.imgur.com/PXBZPAj.png)

**Ingressi**:

- $n$ per i bit di indirizzo,
- $m$ per i bit dei dati,
- ***RD*** (*Read*): indica se si legge o se si scrive in un chip,
  - RD = 1: si vuole <u>leggere</u> nel chip,
  - RD = 0: si vuole <u>scrivere</u> nel chip.
- ***CS*** (*Chip Select*): seleziona il chip della *bank* che deve essere in "ascolto":
  - CS = 1: il chip è <u>selezionato</u> (solo <u>1 chip per volta può avere CS = 1</u>),
  - CS = 0: il chip è <u>inattivo</u> (<u>isolato elettricamente dal bus</u>, come se non ci fosse).
- ***OE*** (*Output Enable*): abilita (o meno) l'invio di output di un chip sul bus (<u>se CS = 0, allora anche OE = 0</u>),
  - OE = 1: il chip <u>riversa il suo output</u> sul bus,
  - OE = 0: il chip <u>non emette output</u> sul bus.

**Uscite**: $m$, congiunte con le uscite dati ma selezionate in modo mutuamente esclusivo.

> [!info] Interfaccia alternativa
> Si potrebbe avere un chip di memoria con un'interfaccia leggermente diversa:
> ![](https://i.imgur.com/7xZD7Mh.png)
> Qui oltre all'input di clock per la sincronizzazione, al posto di RD, CS e OE ci sono solo **RD** (*Read*) e **WR** (*Write*) che funzionano cosi:
> - $RD = 1 + WR = 0$: lettura sul chip,
> - $RD = 0 + WR = 1$: scrittura sul chip,
> - $RD = 0 + WR = 0$: chip inattivo,
> - $RD = 1 + WR = 1$: non consentito.

##### Struttura

La seguente è la struttura di un *memory bank* da 32x64 bit a 1 chip:

![](https://i.imgur.com/VQLh5kQ.png)

Quindi se **CS** = 0 il chip è del tutto isolato, mentre se è = 1 si stabilisce se si scrive nel chip o se si legge da esso (il chip manda i dati nel bus) in base ad **OE**.

###### Struttura alternativa

In più, grazie a questo:

![](https://i.imgur.com/cd5eHZD.png)

Si può implementare una soluzione alternativa:

![](https://i.imgur.com/pSplCRW.png)

##### Memory bank con più chip

Si possono usare chip multipli per ottenere *memory bank* di dimensioni maggiori:

- Con ***word* più lunghe**: usare $n$ componenti 32x64 in un *bank* da 32x(64$\times n$),
- Con **più *word***: usare $n$ componenti 32x64 in un *bank* da (32$\times n$)x64,

###### Memory bank con *word* più lunghe

La seguente è la struttura di un *bank* da 32x128 bit con *word* più lunghe implementato con 2 chip da 32x64 bit:

![](https://i.imgur.com/2RXCmMU.png)

Indirizzi: 5 bit di indirizzi per 32 blocchi da 64 bit l'uno,

Dati: ora 128 in quando il chip HIGH contiene la 1a parte dei dati di una *word*, mentre il chip LOW ne contiene la 2a (in 2 fanno sempre una *word*, solo più lunga).

###### Memory bank con più *word*

La seguente è la struttura di un *bank* da 128x64 bit con più *word* implementato con 4 chip da 32x64 bit:

![](https://i.imgur.com/znYcCPB.png)

Indirizzi: 7 bit adesso, 5 sempre per l'indirizzo del blocco, gli altri 2 per la scelta del chip (2 bit perché ci sono 4 chip).

Dati: *word* sempre da 64 bit, solo che CS e OE sono moltiplicati per il n° di chip (ogni chip è considerato come <u>blocco</u>, quindi in questo caso ogni blocco ha 4 *words*).

# Esercizi

# Soluzioni

---

Prossima lezione: [[]]

