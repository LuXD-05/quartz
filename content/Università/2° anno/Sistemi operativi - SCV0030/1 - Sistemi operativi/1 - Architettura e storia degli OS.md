# Lezione 1

### Sistemi operativi

#### Architettura

Un **sistema operativo** (***OS***) è un programma opportunamente strutturato che:

- Controlla l'esecuzione dei programmi utente <u>garantendo</u> loro l'<u>accesso a risorse</u> **fisiche** (CPU, memoria...) e **logiche** (file...),
- Fornisce a tali programmi un'<u>interfaccia verso l'hardware</u> (***hw***) così da permettergli di interagirvi senza conoscerne i dettagli architetturali.

> [!example] Unix V - 1986
> Vediamo un esempio di OS (shell, senza GUI) che contiene tutti gli argomenti che verranno trattati in seguito (tra cui: *hardware control*, *system calls*, PCS, *memory management*...):
> ![](https://i.imgur.com/P1oXJC0.png)

##### Modalità operative hw

L'hw ha 2 modalità operative: la ***user mode*** e la ***kernel mode***, discriminate da un <u>bit</u> nel <u>registro</u> **PSW** (*Program Status Word*) della CPU. Il passaggio tra le 2 avviene continuamente, ogni volta che le applicazioni interagiscono con l'OS.

###### User mode

In ***user mode*** eseguono tutti i <u>programmi applicativi</u> non-utente, quindi la **GUI** (*Graphical User Interface*) e i programmi aperti tramite essa.

###### Kernel mode

L'unico programma che esegue in ***kernel mode*** è l'<u>OS stesso</u> e solo in questa modalità è possibile eseguire certe istruzioni ***privilegiate*** del linguaggio macchina.

#### Storia

##### Tubi a vuoto

Dal 1945 al 1955 i calcolatori venivano usati per calcoli scientifici e non avevano OS. Si accedeva direttamente all'hw, non serviva una macchina virtuale (VM) intermedia e si runnava 1 programma per volta.

##### Transistor

Dal 1955 al 1965 coi *transistor* i pc venivano prodotti in serie e venduti a gruppi i cui utenti finali erano i programmatori. Per questi sono stati introdotti *assembly* e *Fortran* e per I/O e memoria si usavano prima schede perforate e poi nastri magnetici.

###### Sistemi batch

In seguito sono anche stati introdotti i **sistemi batch**, capaci di caricare gruppi di programmi su schede perforate (***batch***) in 1 volta ed eseguirli automaticamente 1 dopo l'altro (***jobs***). Qui sono stati usati i primi OS, incaricati di *scheduling*, gestione memoria, protezione e interazione utente.

##### Circuiti integrati

Dal 1965 al 1980 macchine usate ancora per calcoli scientifici ma anche per elaborazioni commerciali; si vede l'introduzione di HDD e terminali (postazioni con tastiera + video). In più vi è il passaggio a linguaggi di alto livello (C, shell...) favorito dagli editor.

###### Multiprogrammazione

cos'è

CPU scheduling

Gestione memoria (LBR e UBR)

Gestione dispositivi (I/O, partitioning e pooling)

requisiti hw (DMA e interrupt)

###### Throughput

CPU e I/O bounds

ottimizzazione

###### Spooling

cos'è

###### Time sharing

cos'è

###### Context switch e overhead

##### LSI/VLSI e PC

Dal 1980 ad oggi si diffondono i **PC** (*Personal Computers*), accessibili alle masse e dotati di GUI per facilitarne l'uso; seguiti dai sistemi *real time* e poi dagli OS distribuiti.

---

Prossima lezione: [[2 - Hardware]]

