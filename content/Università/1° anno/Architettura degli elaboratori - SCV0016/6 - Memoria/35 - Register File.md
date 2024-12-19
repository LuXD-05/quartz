# Lezione 35

### Register File

Un ***register file*** (o *banco di registri*) è una struttura a vettore in cui sono organizzati $m$ registri paralleli tutti aventi la <u>stessa dimensione</u> ($n$ bit) e le <u>stesse funzioni</u> più vari <u>circuiti di controllo per</u> accedervi in <u>lettura e scrittura</u>.

I *register files* sono blocchi funzionali essenziali per le CPU in quanto ne costituiscono i <u>registri interni</u>, i quali contengono <u>operandi e risultati della ALU</u>.

**Ingressi**:

- $i$ da $n$ bit (*word* da memorizzare),
- $x_{i}$ da $k$ bit (indici dei registri di input),
- $x_{o}$ da $k$ bit (indici dei registri di output),
- 1 di $\overset{---}{CK}$.

**Uscite**: $o$ da $n$ bit (output),

##### Struttura

La seguente è la struttura di un *register file* a 1 input a $n$ bit e 2 output, che contiene $m \, (2^{k})$ registri da $n$ bit (<u>indicizzati</u> da $0$ a $2^{k}-1$):

![](https://i.imgur.com/sMrWu1s.png)

Tale viene quindi usata nelle CPU per garantire alle ALU l'accesso a delle memorie veloci per le proprie operazioni:

![](https://imgur.com/vSBG6HM.png)

> [!info] Esempio
> Supponiamo di avere un codice del genere:
> ```java
> int a, b, c;
> //...
> s = a + b; 
> ```
> Tradotto in assembly (supponendo che ad `a`, `b` e `c` corrispondano i registri $4$, ${} 12$ e $9$), tale diventa:
> ```assembly
> ADD R9, R4, R12
> ```
> Tradotto in linguaggio macchina, il codice assembly potrebbe essere:
> ![](https://i.imgur.com/9w5HYXh.png)
> Perciò ciò che avviene è:
> ![](https://i.imgur.com/FzfasMp.png)

###### Implementazione

Il seguente è un esempio di implementazione di un *register file* a 32 registri ognuno a 64 bit, con 1 bus di input (salvataggio risultato) e 2 di output (estrazione operandi):

![](https://i.imgur.com/r1zlNLG.png)

(La struttura non ha 2 MUX con $32 \cdot 64 = 2048$ input, ma per ogni MUX ce ne sono $n = 64$ **MUX** ciascuno con **32 input** 1 per registro. Ogni MUX seleziona **1 bit** tra i 64 di ognuno dei 32 registri con $o_{0}$ e $o_{1}$, 5 input di selezione (per 2 $o$) per scegliere tra $2^{5}$ input/registri condivisi negli input di selezione dei 64 MUX; si hanno infine **64 bit** paralleli in output).

##### Funzionamento

(Riferendoci all'immagine precedente) il *register file*:

1) ($CK = 0$) Prende in input una *word* da $n$ bit (in questo caso 64),
2) ($CK = 0$) Legge il valore decodificato (tramite **[[20 - Decoder#Decoder|DEC]]**) di $i_{0}$ e lo usa come indice per scegliere il registro (alla posizione $i_{0}$) nel quale andrà memorizzata la word corrente,
3) ($CK = 0$) Col comando [[33 - Registro parallelo#Comando Load|Load]] ($L = 1$ nel registro all'indice $i_{0}$) si carica la *word* nel registro scelto, mentre gli altri continuano a memorizzare il valore precedente (ricordiamo che i flip-flop master-slave, per il ${} CK$ negato, memorizzano quando è a $0$ e restituiscono output quando è a $1$),
4) ($CK = 1$) I registri iniziano a restituire l'output dato che il clock ha cambiato valore,
5) ($CK = 1$) Gli $m$ **[[21 - Multiplexer#Multiplexer|MUX]]** (in questo caso $m = 2$) restituiscono in output le $m$ *word* che i registri agli indici $o_{1}$ e $o_{2}$ stanno restituendo in output (ricordiamo che i [[21 - Multiplexer#Multiplexer|MUX]] implementano un [[20 - Decoder#Decoder|DEC]], per questo non ce n'è bisogno per decodificare $o_{1}$ e $o_{2}$).

Quindi:

- Nell'**intervallo alto** dei cicli ($CK = 1$) il *register file* <u>manda gli operandi alla ALU</u>, la quale <u>computa il risultato</u> e lo <u>rimanda</u> al *register file* <u>in input</u>,
- Nell'**intervallo basso** dei cicli ($CK = 0$) il *register file* <u>memorizza i dati</u> inviatigli dalla ALU.

Tale suddivisione permette l'esecuzione di operazioni quali: `R1 = R1 + R2`, infatti `R1` viene sovrascritto solo quando $CK = 0$ e finché $CK = 1$ la ALU può vedere il valore di `R1` immutato.

Tuttavia il ciclo di clock deve essere sufficientemente lungo da permettere al segnale di propagarsi dall'output del *register file* al suo input, imponendo indirettamente un limite alla frequenza di clock.

#### Altre considerazioni

##### Varianti

Ci sono altri *flag* di comando che possono essere aggiunte:

- $WR$ (*write*): se $WR = 0$ la <u>memorizzazione</u> in qualsiasi registro <u>è disabilitata</u>,
- $CLR$ (*clear*): <u>per azzerare 1 o tutti i registri contemporaneamente</u> (asincrono).

##### Costi

Per $m$ registri a $n$ bit ci vogliono:

- $k = log_{2}(m)$ bit di input per gli indici,
- $x_{o} \cdot n$ MUX a $m$ ingressi,
- $m$ registri paralleli con comando *Load* (ovvero $m \times n$ flip-flop),
- Un DEC da $k$ a $m$ bit,
- $3 \cdot k$ bit nelle istruzioni in $ML$ binario solo per i 3 indici dei registri.

Questo è un prezzo <u>molto caro</u>, soprattutto per $m$; infatti $m$ è <u>piccola</u> in quasi tutte le architetture reali (da 8 a 64) siccome $m$ piccolo = **istruzioni corte** + ***register file* piccolo e veloce**. Invece $n$ (dimensione della *word* dell'architettura) è a 32 o 64 bit.

##### Scalabilità

Seppur i registri sono il tipo di memoria migliore per le ALU grazie alla loro velocità, essi non sono **scalabili** a causa del loro costo elevato.

Per memorizzare e lavorare con milioni, miliardi (e oltre) di *word* dei programmi e dei dati servono altri tipi di memoria.

# Esercizi

# Soluzioni

---

Prossima lezione: [[36 - Cache]]

