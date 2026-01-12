# Lezione 3

### Sequenze

Quando si fanno certi esperimenti, spesso gli esiti sono delle **sequenze**, le quali:

- Possono essere **con o senza ripetizioni** (contengono più volte gli stessi simboli o meno),
- Il loro **ordine può contare o meno** (può importare l'ordinamento della sequenza o no).

> [!info] Nota
> Nel seguito verrà fatto uso di 2 variabili: "$k$" che indica il <u>n° di elementi presi in considerazione</u> ed "${} n$" che indica il <u>n° di posti in cui è possibile disporre gli elementi</u>.

#### Disposizioni

Le **disposizioni** identificano tutti i casi delle sequenze in cui l'<u>ordine conta</u> e possono essere <u>con o senza ripetizioni</u>. L'obiettivo di queste è di trovare tutti i modi di disporre una certa sequenza di lunghezza $n$ dati $k$ elementi.

###### Disposizioni semplici

Le disposizioni semplici <u>non ammettono ripetizioni</u> e la formula per calcolarle è:

$$D_{n,k} = \dfrac{n!}{(n-k)!}$$

> [!example] Quando si usa
> Questa si usa quando si ha una sequenza in cui i $k$ elementi sono "unici", nel senso che non possono occupare più di un posto e una volta disposti non è più possibile ridisporli; per esempio, trovare tutti i modi in cui 3 persone possono sedersi in 5 posti, che sono 60 (quando il 1° si siede, il 2° avrà 4 scelte disponibili e così via).

###### Disposizioni con ripetizioni

Queste invece <u>ammettono ripetizioni</u> e la formula per calcolarle è:

$$D^{r}_{n,k} = n^{k}$$

> [!example] Quando si usa
> Questa si usa in quei casi in cui un elemento può essere ripetuto più volte all'interno della sequenza; per esempio, se si volesse calcolare la probabilità di indovinare al 1° tentativo una password di 8 caratteri composta da 10 cifre, 26 lettere minuscole e 26 maiuscole, tale sarebbe $\frac{1}{62^{8}}$.

##### Permutazioni

Le **permutazioni** sono un caso particolare delle disposizioni in cui $n = k$ e si distinguono in:

###### Permutazioni semplici

Le permutazioni semplici <u>non ammettono ripetizioni</u> e la formula è:

$$D_{n} = n!$$

> [!example] Quando si usa
> Questa si usa quando (oltre ad avere lo stesso n° di elementi e posti) <u>tutti gli elementi della sequenza sono diversi</u>; per esempio, se dovessi contare i modi in cui disporre le lettere A, B e C otterrei $3! = 8$.

###### Permutazioni con ripetizioni

Queste invece <u>ammettono ripetizioni</u> e la formula per calcolarle è:

$$D_{n}^{r} = \dfrac{n!}{n_{1}! \,\cdot\, n_{2}! \;\ldots\; n_{k}!}$$

(${} k$ = n° di gruppi | ${} n$ = n° totale di elementi)

> [!example] Quando si usa
> Questa si usa quando (oltre ad avere lo stesso n° di elementi e posti) gli elementi della sequenza sono <u>indistinguibili</u> (eventualmente a gruppi); per esempio, se dovessi assumere 6 dipendenti, in quanti modi questi sono composti da 2 ingegneri, 2 architetti e 2 programmatori? La risposta è 90.

#### Combinazioni

Le **combinazioni** sono delle "*selezioni*" di $k$ elementi presi da un insieme di $n$ elementi in cui l'<u>ordine non conta</u> (quindi 2 combinazioni con gli stessi elementi in ordine diverso sono considerate uguali).

###### Combinazioni semplici

Le combinazioni semplici <u>non ammettono ripetizioni</u> e la formula fa uso del **coefficiente binomiale**:

$$C_{n,k} = \binom{n}{k} = \dfrac{D_{n,k}}{k!} = \dfrac{n!}{k! \cdot (n-k)!}$$

Nota: come concetto è possibile interpretarlo come la probabilità che $n$ elementi sono messi in $k$ posti.

> [!example] Quando si usa
> Questa si usa quando è specificato che non è importante l'ordine della sequenza (selezioni con stessi elementi sono considerate uguali); per esempio, se di 10 cartelle l'antivirus ne segnala 3 come infette, allora le possibili combinazioni di cartelle infette saranno 120.

###### Combinazioni con ripetizioni

Queste invece ammettono ripetizioni e la formula cambia un po':

$$C_{n,k}^{r} = \binom{n+k-1}{k} = \binom{k + n-1}{n-1} = \dfrac{(k + n - 1)!}{k! \cdot (n-1)!}$$

($n$ = n° di gruppi | $k$ = n° totale di elementi)

Il metodo di risoluzione è detto "*asterischi e barre*" (siccome avremo degli elementi <u>indistinguibili</u> possibilmente a gruppi) e consiste nel disegnare $x$ asterischi per il 1° gruppo di elementi, seguiti poi da una barra e così via fin quando non si sono rappresentati tutti i gruppi separati (2 barre indicano che quel gruppo ha 0 elementi). Avendo $n-1$ barre e $k$ asterischi basta solo sostituire questi dati nella formula e basta.

> [!example] Quando si usa
> Questa si usa quando (oltre a specificare che non è importante l'ordine della sequenza) si hanno <u>più gruppi di elementi indistinguibili</u>; per esempio, voglio scegliere 5 forme tra cerchi, quadrati e triangoli, quindi (con 2 barre e 5 asterischi) si ha: $\binom{3 + 5 - 1}{5} = \binom{7}{5} = 21$.

---

Prossima lezione: [[4 - Probabilità condizionata]]

