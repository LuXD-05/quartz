# Lezione 8

### Gestione della memoria

Nell'ambito di gestione della memoria l'OS ha 2 obiettivi:

- Allocare più processi in memoria per avere parallelismo e migliori *performance*,
- Proteggere la memoria dei processi impedendo che uno acceda alla memoria di un altro.

#### Traduzione, linking e loading

Per eseguire un programma (da sorgente a binario) si passa tra 3 fasi diverse:

![](https://i.imgur.com/gi2M4Tx.png)

1) **Traduzione**: il ***translator*** (*assembler*/compilatore) riceve in input il programma sorgente (in C, assembly...) e produce un ***object module*** (modulo oggetto), un programma in linguaggio macchina (solitamente non ancora eseguibile siccome può contenere riferimenti ad altri moduli i cui indirizzi non sono ancora noti).
2) ***Linking***: il ***linker*** "risolve i simboli" collegando i vari *object modules* e librerie, producendo l'eseguibile binario (in questa gli indirizzi possono essere **rilocati** al fine di evitare ***overlapping*** con altri indirizzi).
3) ***Loading***: il ***loader*** carica il programma in memoria associandolo ad un processo (nel caso di *overlapping* si effettuano ulteriori rilocazioni).

###### esempio? / rilocazione e linking statici vs dinamici?

---

##### Rilocazione statica e dinamica

La rilocazione può avvenire prima dell’esecuzione (statica) oppure a runtime tramite supporto hardware come il Relocation Register.

- Rilocazione statica: modifica degli indirizzi nel binario
- Rilocazione dinamica: somma RR + indirizzo logico

> [!important]
> Con RR + LBR/UBR la rilocazione dinamica è semplice e sicura.

##### Linking dinamico

Con il linking dinamico i riferimenti a moduli esterni vengono risolti a runtime (es. DLL), riducendo dimensione dei binari e duplicazioni in memoria.

- Risoluzione dei simboli durante l’esecuzione

#### Modello di allocazione della memoria dei programmi

Durante l’esecuzione un programma utilizza diverse aree di memoria con ruoli e dinamiche differenti.

- Area codice, area dati statici, heap, stack

##### Stack e heap

Lo stack gestisce variabili locali e parametri con politica LIFO, mentre l’heap ospita dati dinamici creati a runtime tramite allocator del linguaggio.

- Stack per chiamate annidate, heap per dati PCD

> [!example]
> malloc/calloc/free in C sono interfacce verso l’heap allocator del runtime support.

##### Heap allocator e RTS

La gestione dell’heap è demandata a routine del Runtime Support collegate dal linker; in alcuni linguaggi è presente anche il garbage collector.

- Allocazione/deallocazione automatica o esplicita

##### Layout logico della memoria

Codice e dati statici occupano aree a dimensione fissa, mentre stack e heap condividono uno spazio comune crescendo in direzioni opposte.

- Crescita opposta di stack e heap

#### Gerarchia di memoria

Per bilanciare costo e prestazioni, i sistemi adottano una gerarchia di memoria a più livelli.

- Cache, main memory, disco

##### Ruolo della MMU

La MMU traduce indirizzi logici in indirizzi fisici e gestisce l’accesso alla gerarchia di memoria come se fosse un’unica memoria principale.

- Traduzione logica → fisica

> [!info]
> La gestione della cache è hardware, ma il SO può favorirne l’efficienza (es. thread dello stesso processo).

##### Memoria virtuale nella gerarchia

Con la memoria virtuale, parte dello spazio di indirizzamento risiede su disco e viene trasferita in memoria solo quando necessario.

- Trasferimenti a blocchi (pagine/segmenti)

#### Riuso della memoria

La memoria liberata deve poter essere riutilizzata; ciò avviene tramite strutture che tengono traccia delle aree libere.

- Free list delle aree libere

##### Strategie di allocazione

Quando si richiede un’area di dimensione k, il SO (o RTS) può adottare diverse politiche.

- First fit, best fit, next fit

> [!warning]
> Best fit riduce lo spreco immediato ma peggiora le prestazioni nel lungo periodo.

##### Frammentazione

La presenza di memoria libera non utilizzabile prende il nome di frammentazione.

- Frammentazione esterna

##### Tecniche di contrasto

Esistono tecniche per ridurre o gestire la frammentazione.

- Boundary tags, compaction

> [!important]
> La compattazione richiede rilocazione dei programmi ed è praticabile solo con supporto hardware adeguato.

#### Allocazione contigua e non contigua

Un processo può essere allocato in un’unica area contigua oppure in più aree non adiacenti.

- Allocazione contigua vs non contigua

##### Allocazione contigua

Ogni processo occupa un’unica area continua; protezione e rilocazione sono semplici ma la frammentazione è un problema.

- Uso di RR, LBR, UBR

##### Swapping

I processi possono essere spostati temporaneamente su disco per liberare memoria principale.

- Swapped out / swapped in

##### Allocazione non contigua

Il processo è diviso in componenti allocati in aree diverse; elimina o riduce la frammentazione.

- Componenti logiche del processo

#### Paginazione e segmentazione

Sono le due principali tecniche di allocazione non contigua.

- Paginazione, segmentazione

##### Paginazione

La memoria è divisa in page frame di dimensione fissa e i processi in pagine della stessa dimensione.

- Page table per mappare pagina → frame

> [!important]
> La traduzione avviene per sostituzione di bit, senza somme.

##### Segmentazione

Il processo è diviso in segmenti logici di dimensione variabile.

- Segment table con base e dimensione

> [!warning]
> La segmentazione facilita la condivisione ma non elimina la frammentazione.

##### Segmentazione + paginazione

I segmenti sono divisi in pagine, combinando i vantaggi di entrambe le tecniche.

- Segment table → page table

#### Memoria virtuale

La memoria virtuale crea l’illusione di una memoria più grande di quella fisica disponibile.

- Uso del disco come estensione della RAM

##### Demand paging

Le pagine vengono caricate in memoria solo quando servono.

- Page fault, page-in, page-out

> [!info]
> Il page I/O è trasparente al programma ma degrada le prestazioni.

##### Page table estesa

Ogni entry contiene informazioni utili per traduzione e replacement.

- Validity bit, frame#, prot, ref, mod, disk address

##### TLB

Il Translation Lookaside Buffer accelera la traduzione memorizzando coppie (page#, frame#).

- TLB hit, TLB miss

> [!warning]
> Il TLB va svuotato ad ogni context switch.

##### Protezione della memoria

Accessi fuori dallo spazio logico o non autorizzati generano eccezioni hardware.

- Memory protection exception

#### Principio di località e thrashing

I programmi tendono ad accedere a indirizzi vicini nel tempo; violare questo principio porta al thrashing.

- Località temporale e spaziale

> [!important]
> Troppi page fault ⇒ page I/O elevato ⇒ degrado globale delle prestazioni.

#### Politiche di page replacement

Quando non ci sono frame liberi, il SO deve scegliere quale pagina rimuovere.

- FIFO, LRU

##### Stack property

Una politica ha la stack property se aumentando i frame non aumenta il numero di page fault.

- LRU sì, FIFO no

##### Approssimazioni pratiche

Le politiche ideali sono costose; si usano versioni approssimate.

- Reference bit, second chance

#### Allocazione dei frame ai processi

Il SO decide quanti frame assegnare a ciascun processo.

- Allocazione fissa o variabile, replacement locale o globale

##### Working set

Il working set rappresenta l’insieme delle pagine usate recentemente da un processo.

- WS(P,t,d), WSS(P,t,d)

> [!important]
> Se la somma dei working set supera i frame disponibili, alcuni processi vengono sospesi.

---

