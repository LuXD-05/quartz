# Lezione 39

##### CPU

La CPU (*Control Processing Unit*) è il nucleo centrale del funzionamento dei computer. Essa è composta dalla **ALU** (*Arithmetic Logic Unit*) che esegue le operazioni logico-matematiche e dalla **CU** (*Control Unit*) che gestisce il clock e i segnali di controllo della macchina.

###### Prestazioni

Le prestazioni di una macchina sono determinate da:

- **IS** (*Instruction set*, <u>numero e caratteristiche delle istruzioni</u>),
- **CF** (<u>frequenza di clock</u>,
- **CPI** (<u>cicli di clock per istruzione</u>).

Le ultime 2 sono determinate dalla **CU** e dal design del ***[[35 - Register File#Datapath|datapath]]***.

### Single cycle CPU

Una CPU si dice a ciclo singolo quando $CPI = 1$ (1 istruzione per ciclo di clock).

<u>Vantaggi</u>: semplice da progettare,

<u>Svantaggi</u>: cicli lunghi (durano quanto l'istruzione più lenta).

#### Progettazione

##### 1) Requisiti del datapath dall'IS

Il *[[35 - Register File#Datapath|datapath]]* deve essere in grado di realizzare qualsiasi istruzione, perciò bisognerà adattarlo in base all'**IS**. Prendiamo come esempio un sottoinsieme di un IS reale, il ***MIPS***, che analizzeremo per ottenere la <u>semantica delle istruzioni</u> o **RTL** (*Register Transfer Logic*):

###### MIPS

Il MIPS ha istruzioni tutte a 32 bit e di 3 formati:

- ![](https://i.imgur.com/fHXLSyW.png)
- ![](https://i.imgur.com/pCoegCh.png)
- ![](https://i.imgur.com/dtG1KkV.png)

Queste sono composte da:

- ***op***: codice dell'<u>operazione da eseguire</u>,
- ***rs, rt, rd***: <u>registri degli operandi e del risultato</u>,
- ***shamt*** (*shift amount*): indica di <u>quando shiftare</u> (a dx o sx) il <u>risultato</u>,
- ***funct***: indica <u>varianti</u> di ***op***,
- ***address/immediate***: indirizzo o valore immediato,
- ***target address***: indirizzo di destinazione di un operazione $JMP$.

Quindi:

- Operazioni di tipo $R$: 
- Operazioni di tipo $I$: 
- Operazioni di tipo $J$: saltano direttamente all'indirizzo specificato, ovvero aggiungono direttamente $n$ al PC.

###### RTL

| Istruzione            | Semantica           | Traduzione (alto livello)                                                                                                                            |
| --------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ADD** (R-type)      | `addu rd, rs, rt`   | `rd = rs + rt`                                                                                                                                       |
| **SUB** (R-type)      | `subu rd, rs, rt`   | `rd = rs - rt`                                                                                                                                       |
| **OR** (I-type)       | `ori rt, rs, imm16` | `rt = rs OR imm16`                                                                                                                                   |
| **LOAD** (I-type)     | `lw rt, rs, imm16`  | carica dalla memoria una *word* nell'indirizzo dato da `(rs + imm16)` e la salva in `rt`                                                             |
| **STORE** (I-type)    | `sw rt, rs, imm16`  | salva il valore di `rt` in memoria all'indirizzo dato da `(rs + imm16)`                                                                              |
| **BRANCH** (I/J-type) | `beq rt, rs, imm16` | `if (rs == rt) then PC = PC + 4 + imm16 * 4` (in pratica se `rs` e `rt` sono uguali, fa un $JMP$ alla label calcolata come $PC + 4 + imm16 \cdot 4$) |

> [!info] Fetch
> Nota: prima di eseguire un'istruzione, è necessario leggerla dalla memoria con il comando `fetch`, poi la si **decodifica** e la si **esegue**:
> ![](https://i.imgur.com/PVgZoLn.png)
> Ad ogni `fetch` viene aggiornato il PC con il valore dell'indirizzo della prossima istruzione da eseguire.

##### 2) Componenti e clocking

Dopo aver individuato i requisiti del *datapath*, è necessario sceglierne i componenti (che soddisfano tali requisiti) e la metodologia di temporizzazione.

###### Scelta componenti del datapath

I blocchi che useremo sono:

- 2 ***memory banks*** distinti: uno per le **istruzioni** (*read-only*, single bus) e uno per i **dati** (*read/write*, un bus per direzione) per <u>leggere l'istruzione, calcolare dati e scriverli in memoria in 1 stesso ciclo di clock</u>,

  ![](https://i.imgur.com/gddFw52.png)

- 1 ***register file*** (32x32) per 32 registri da 32 bit con: 2 bus di lettura e 1 di scrittura,

  ![](https://i.imgur.com/SN9DBJv.png)

  Qui ricordiamo che:

  - $o_{1}$ e $o_2$ sono l'input di selezione dei MUX interni al *register file* e selezionano rispettivamente i registri i cui output dovranno uscire nei bus di output 1 e 2,

  - $i_{1}$ semplicemente abilita i registri in cui verranno scritti i dati in input dall'input bus.

- 1 **PC** (*Program Counter*), un registro speciale che memorizza l'indice/indirizzo dell'istruzione corrente (in bytes, = 32 bit) nel *bank* istruzioni ed è usato per leggerla.

  ![](https://i.imgur.com/VWmu8Hl.png)

  La semantica di ogni istruzione specifica cosa succede al PC, di solito incrementato di 4 bytes o sommato di $n$ con `branch` e `jump`; ciò deve essere fatto da un circuito separato dall'ALU (già impegnata a calcolare nello stesso ciclo di clock):

  ![](https://i.imgur.com/mmSkhys.png)

- La **ALU**, per le operazioni logico-matematiche (ipotizziamo con 128 operazioni totali, restituisce anche un bit di esito):

  ![](https://i.imgur.com/BSziPCF.png)

- Altri blocchi funzionali (combinatori), tipo:
  - **EXT**: per le operazioni,
  - **MUX**: per qualsiasi caso di scelta tra più segnali.

###### Scelta del metodo di clocking

In **lettura** tutti i componenti si comportano in maniera <u>combinatoria</u>, ovvero il loro <u>output è permanentemente disponibile</u> (e cambia dopo le scritture).

In **scrittura** invece, tutte le <u>memorie</u> (*register files* 32x32, PC, *memory bank* dei dati) devono essere <u>sincronizzate</u>, perciò si userà lo stesso segnale di clock per tutte. Stabiliamo quindi che sul **fronte di discesa** <u>si memorizza</u> il segnale in input (se la scrittura è abilitata).

##### 3) Progettare il datapath

Adesso bisogna progettare il circuito del datapath coi componenti scelti in modo che tutti i requisiti siano soddisfatti ed il funzionamento della CPU sia assicurato. 

Per fare ciò si usa un'**approccio incrementale** focalizzato sull'IS; quindi si crea un circuito che gestisca l'istruzione $is_{1}$ e lo si aggiorna (aggiungendo anche controlli per la CU da computare) per ogni istruzione successiva finché non si è fatto per tutte.

Partiamo definendo un quadro generale:

![](https://i.imgur.com/47SWeOn.png)

Per i cavi:

- **Rosso**: arriva dalla *instruction memory*,
- **Blu**: arriva dalla CU,
- **Verde**: da/a ALU (read/write),
- **Grigio**: non usato.

> [!info] Fetch
> Bisogna anche progettare il circuito della `fetch`, ovvero uno che in base all'istruzione da eseguire, indica al PC l'indirizzo della prossima:
> ![](https://i.imgur.com/CLokGTH.png)
> Quindi qui:
> - Il *datapath* riceve un'**istruzione** dalla memoria istruzioni (nota imm16 e op) e <u>ritorna un codice alla CU</u>,
> - La CU invia poi un segnale al blocco "***Next address logic***", una serie di componenti che, in base a una certa logica e agli input ricevuti (da CU, imm16 e vecchio PC), <u>restituiscono al PC l'indirizzo della prossima istruzione</u>.

###### Somma e sottrazione

![](https://i.imgur.com/cv5cFwx.png)

Ovvero `addu` e `subu`, per queste:

0) Si ottiene l'istruzione da eseguire dalla memoria istruzioni con `fetch`,
1) ${} op$ e $funct$ vanno nella CU, che ritornerà l'istruzione (e un segnale $RW$ per abilitare la scrittura nei registri); $rd$ invece indica il registro che memorizzerà la *word* in input, mentre $rs$ e $rt$ sono i registri che mostreranno il loro contenuto in output,
2) L'ALU, con l'output dei registri e l'operazione data dalla CU, computerà un risultato e lo metterà in output,
3) Tale output è salvato nuovamente nei registri e il ciclo ricomincia.

###### OR bitwise

![](https://i.imgur.com/iSe8Uh0.png)

Ovvero `ori` (dato che l'OR bitwise è immediato). Qui non è rappresentata la CU, ma da essa escono output in blu, quindi:

0) `fetch` (non rappresentato con CU, ma $ALUctr$ contiene l'operazione, in questo caso OR bitwise),
1) Nei registri entrano `rt` (`rd` non c'è per `imm16`) come registro di input e solo `rs` come registro di output,
2) Infatti, il bus A (output 1 dei registri) è significativo, mentre il 2° input della ALU è sempre `imm16` esteso a 32 bit (perché è un'operazione di tipo $I$, per $ALUsrc$),
3) Output ALU è salvato nei registri e il ciclo ricomincia.

###### Load

![](https://i.imgur.com/gaG3Wln.png)

Ovvero `lw`, anch'essa immediata, dove si accede al *bank* dati per caricare nei registri una *word* letta da lì, la quale si trova all'indirizzo computato dalla ALU:

0) `fetch` ma stavolta non serve `rd`,
1) (Stessa cosa come per *[[#OR bitwise|ori]]*, solo che $ALUctr$ è somma tra output registri a e `imm16` esteso a 32 bit),
2) Si accede al *bank* dati all'indirizzo computato dalla ALU con ${} WR = 0 {}$ (ovvero con $OE = 1$, vedi *[[38 - Memory Bank|memory bank]]*) ovvero in modalità <u>lettura</u> cosicché il *bank* restituisca la *word* a quell'indirizzo (scelta poi dal MUX grazie al flag $MemToReg$),
3) (Salvataggio output nei registri).

###### Store

![](https://i.imgur.com/130sWRq.png)

Ovvero `sw`, sempre immediata, che scrive una *word* in output dall'ALU nel *bank* dati:

0) `fetch` ma neanche stavolta serve `rd`,
1) Qui abbiamo invece `rs` e `rt` abilitati in input, ma $RW = 0$ (scrittura in registri disabilitata), quindi non si salverà niente nei registri ma entrambi i 2 output dei registri sono significativi,
2) Si ottiene l'indirizzo del *bank* dati dove scrivere dall'ALU (output 1 registri + `imm16`), mentre l'output 2 dei registri contiene la *word* da salvare in quell'indirizzo (ciò possibile perché $WR$ del *bank* è a 1, oppure $OE = 0$).

###### Salto condizionato

###### Datapath finale

![](https://i.imgur.com/8Z2jFCF.png)

Schematizzato con:

![](https://i.imgur.com/FvMdNk6.png)

##### 4) Ricerca di controlli di trasferimento tra registri

lezione 34

##### 5) Progettare la CU

# Esercizi

# Soluzioni

---

Prossima lezione: [[]]

