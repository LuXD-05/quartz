# Lezione 2

### CPU

La CPU ha un "ciclo" di esecuzione che si compone di 3 operazioni fondamentali: ***fetch*** (prelievo dell'istruzione dalla memoria), ***decode*** (decodifica l'istruzione) ed ***execute*** (esecuzione dell'istruzione), per poi proseguire con la prossima istruzione ricominciando il ciclo.

##### Registri

La CPU fa uso di certi **registri**, suddivisi in:

- **Generali** (*general purpose registers*): il 1° livello della gerarchia di memoria e contengono dati e risultati temporanei che servono alla CPU,
- **Di controllo** (*control registers*): controllano gli stati della CPU stessa.

###### Registri di controllo

Ci sono diversi registri di controllo:

- **PC** (*Program Counter*): contiene l'<u>indirizzo della prossima istruzione</u> da prelevare,
- **SP** (*Stack Pointer*): <u>puntatore al top dello stack</u> dove sono contenuti i *frame* (record di attivazione) delle procedure in esecuzione, 
- **PSW** (*Program Status Word*):
  - **PM** (*Privileged Mode*): bit che indica la <u>modalità dell'OS</u> (user o kernel),
  - **CC** (*Condition Code*): codici di condizione impostati dall'ALU in base a certe operazioni,
  - **IM** (*Interrupt Mask*) e **IC** (*Interrupt Code*): usati per la gestione di ***interrupt***,
  - **MPI** (*Memory Protection Information*): info sulla porzione di memoria accessibile (tipo **LBR** e **UBR**).

##### Interrupt

Gli ***interrupt*** sono un meccanismo per segnalare alla CPU un evento da gestire che avviene nel sistema; gli obiettivi di questi sono:

- Interrompere il normale ciclo di esecuzione della CPU (per poi riprenderlo una volta gestito l'*interrupt*),
- Richiedere l'intervento dell'OS (ovvero eseguire del codice che ne fa parte).

> [!info] Quando avvengono?
> Un'*interrupt* avviene quando la CPU riceve un segnale hardware (***interrupt request***) su un'apposita linea del bus di sistema; e questo può essere causato dal <u>clock</u> o da un <u>controller di un dispositivo</u> (*[[#Hardware interrupt|hardware interrupt]]*) oppure dal <u>programma in esecuzione</u> (*[[#Program interrupt|program interrupt]]*).

#### Hardware interrupt

Questi sono **eventi asincroni** rispetto al programma in esecuzione, quindi non si ha modo di prevedere se e quando si verificano; si dividono ulteriormente in:

- ***Timer interrupt***: usati dal <u>clock per notificare un tick</u> (passaggio di un certo quanto di tempo), in tal caso l'OS controlla se il *tick* ha esaurito il *time slice* del programma in esecuzione per eventualmente eseguire un *context switch*.
- ***I/O interrupt***: usati da <u>dispositivi I/O per notificare eventi</u> che devono essere <u>gestiti dall'OS</u> (tipo movimento del mouse), dopodiché esso riprenderà l'esecuzione (e la schedulazione) del programma precedentemente attivo.

##### Fasi dell'hardware interrupt

Un hardware interrupt, visualizzato è:

![](https://i.imgur.com/x3BVtEM.png)

Mentre, semplificando, esso prevede 5 fasi:

1) Mentre esegue l'istruzione $i$ di un programma $P$, la CPU riceve un'*interrupt request*,
2) Eseguita $i$, la CPU sospende l'esecuzione di $P$ e salta all'***interrupt handler*** (procedura di gestione dell'interrupt, parte dell'OS quindi ***kernel mode***),
3) L'*interrupt handler* gestisce l'interrupt,
4) L'*interrupt handler* restituisce il controllo a $P$ (o ad un altro $P'$ in base allo *scheduling* e al *time sharing*),
5) $P$ riprende la propria esecuzione dall'istruzione $i+1$ (o riparte $P'$).

> [!info] Nota
> Le fasi 2 e 4 sono complesse in quanto il <u>valore dei registri</u> (e in particolare del **PC**) <u>va salvato</u> prima di passare all'*interrupt handler*, tuttavia il **programma** <u>non sa quando salvarlo</u> (non sa quando arriva un interrupt) e l'***handler*** <u>non può</u> (quando ha il controllo il valore è già cambiato); perciò è la **CPU** che lo salva in registri speciali per poi ripristinarlo quando termina la gestione dell'interrupt.

###### Interrupt a cascata

Può capitare che durante la gestione di un interrupt arrivino altre *interrupt request*; la gestione normale prevede di: 1) sospendere l'handler corrente, 2) eseguire un nuovo handler per l'altro interrupt e, al termine di questo, 3) riprendere l'handler precedente.

![](https://i.imgur.com/yOeLmKe.png)

Tale metodo però <u>non è efficiente per gestire un n° eccessivo di interrupt a cascata</u> in quanto lo spazio di <u>memoria per salvare lo stato dei programmi interrotti è limitato</u>. Perciò si organizzano gli interrupt in **classi di priorità**, secondo le quali (durante la gestione di un'interrupt) le *interrupt request* di priorità <u>minore o uguale a quella corrente</u> rimangono **pendenti** (*pending*) e vengono <u>trattate in seguito</u> (così il n° max di interrupt a cascata = n° di classi di priorità). Esempio di gerarchia (da priorità max a min):

![](https://i.imgur.com/DDd6OGI.png)

(*Exception* e *Trap* sono le 2 categorie di [[#Program interrupt|program interrupt]] che vediamo in seguito).

> [!important] Ignorare le interrupt request
> Per mezzo dei bit di **IM** (*Interrupt Mask*) nel registro **PSW** è possibile determinare quali classi di interrupt sono abilitate (***enabled***) e quali no (***masked off***), ciò (tranne in *user mode* dove tutte le classi sono abilitate, altrimenti si potrebbe impedire all'OS di interrompere i programmi) è possibile con 2 implementazioni:
> - **IM** contiene 1 bit per ogni classe di interrupt,
> - **IM** contiene un valore $m$ per abilitare tutti gli interrupt di priorità $\geq m$.

###### Fase 2

(Nella *user area* della RAM) per ogni classe di interrupt vi è una **SRIA** (*Saved Register Information Area*), nella quale vengono salvati PC, SP e PSW prima di passare all'*handler*.

(Nella *kernel area* della RAM) per ogni classe di interrupt vi è un ***interrupt vector*** che contiene:

- L'<u>indirizzo della prima istruzione dell'handler</u> da assegnare al **PC** per effettuare il salto,
- Il <u>valore da assegnare alla</u> **PSW** coi valori di **PM** (per mettere la CPU in *kernel mode*) e di **IM** (per disabilitare gli interrupt di priorità non superiore).

> [!info] Note
> Gli interrupt vector sono inizializzati in memoria durante il *boot*. 
> Quando arriva un interrupt abilitato, le fasi sono: 1) l'hw imposta l'**IC** per dire all'OS che tipo di interrupt è, 2) **PC**, **SP** e **PSW** sono salvati nell'apposita **SRIA** e 3) **PC** e **PSW** sono impostati in base ai valori nell'interrupt vector apposito; perciò l'handler può partire.

###### Fase 3

L'*interrupt handler*, una volta avviato:

1) <u>Salva i registri generali</u> della CPU (oltre a PC, SP e PSW, già salvati nella SRIA),
2) <u>Esegue il codice</u> apposito <u>per</u> gestire l'<u>interrupt</u> (in base alle info nell'**IC**),
3) <u>Salta al codice dello scheduler</u>, il quale sceglie il programma da eseguire (ovvero la prossima istruzione a cui saltare).

###### Fase 4

In seguito, lo ***scheduler***:

1) <u>Ripristina</u> i valori dei **registri generali** salvati prima,
2) <u>Ripristina</u> i valori dei **registri di controllo** (quindi anche **PC** riprendendo l'esecuzione precedentemente interrotta) spesso con l'istruzione **IRET** (*Interrupt Return*).

> [!important] Nota
> La SRIA contiene i <u>valori dei registri per tutti i programmi interrotti</u>, è per questo che lo scheduler può far riprendere uno qualsiasi di questi.

##### Considerazioni

- L'**IC** contiene <u>info particolari in base all'interrupt</u> (per esempio, con un *disk interrupt*, l'IC conterrà info che permettono di identificare quale disco ha fatto la request).
- Gli OS assumono che l'<u>hardware supporti gli interrupt</u>.
- Salvare il PC e impostarne il valore in base al *vector* sono operazioni fatte necessariamente dall'<u>hardware</u> (in quanto è l'unico modo per interrompere il programma attivo); gli altri potrebbero essere salvati via <u>software</u> (meno complesso ma più lento), quindi per il <u>salvataggio</u> dei registri: <u>hw per quelli di controllo e sw per quelli generali</u>. 
- Dato che il n° max di interrupt gestibili è dettato dal n° di classi di priorità, è sufficiente che ogni programma abbia <u>1 SRIA per classe</u>.

###### Interrupt su CPU avanzate

Le CPU moderne non seguono il tradizionale ciclo *fetch-decode-execute*, bensì alcuni esempi con cicli diversi sono:

- ***Pipeline***: si effettuano contemporaneamente la *fetch* dell'istruzione $i$, la *decode* di $i+1$ e la *execute* di $i+2$.
- CPU **superscalare**: hanno più unità di *fetch*, *decode* ed *execute* che lavorano in contemporanea.

> [!info] Nota
> Queste CPU hanno prestazioni nettamente migliori rispetto a quelle tradizionali, ma introducono ulteriori <u>complessità</u> nella gestione degli interrupt, per esempio: quando si hanno <u>istruzioni già prelevate ma non ancora eseguite</u> oppure con le CPU superscalari dove possono esserci <u>istruzioni eseguite parzialmente</u>; tuttavia i principi base degli interrupt rimangono gli stessi, si complica solo l'implementazione.

#### Program interrupt

Questi invece possono essere di 2 tipi (direttamente sotto gli altri 5 hardware interrupt nella [[#Interrupt a cascata|gerarchia]]): **eccezioni** e ***traps***. 

> [!info] Nota
> Questi, al contrario degli [[#Hardware interrupt|hardware interrupt]], non sono eventi <u>asincroni</u> rispetto all'esecuzione del programma, bensì sono interni ad esso e <u>richiedono l'intervento dell'OS</u>.

##### Exceptions

Le **eccezioni** (o interrupt interni) sono involontarie e causate da situazioni anomale interne ai programmi stessi; e si suddividono in:

- **Eccezioni aritmetiche**: tipo divisione per zero, overflow...
- **Eccezioni di *paging*** (*page fault*): ovvero errori durante l'indirizzamento (<u>non anomali</u> ma fondamentali per mantenere programmi un po' in RAM e un po' su disco),
- ***Memory violations*** (*violation fault*): violazione delle protezioni di memoria.

##### Traps

Le ***traps*** (o *software interrupt*) sono il meccanismo che <u>permette ai programmi utente di usufruire dei servizi offerti dall'OS</u> (tipo I/O...) in quanto una semplice chiamata di procedura non può passare da *user mode* a *kernel mode* ed accedere alla *kernel area* della RAM dove sono situati i programmi privilegiati dell'OS.

Queste sono quindi causate dall'istruzione `TRAP` (detta ***Software Interrupt Instruction***), prevista nel linguaggio macchina e dotata di un **parametro** per indicare il <u>tipo di intervento</u> richiesto (in base all'*instruction set*, questo è <u>passabile come operando</u> della `TRAP` o <u>ponendolo sullo stack</u>) che viene poi assegnato ai bit **IC** della PSW che l'handler legge per determinare cosa fare.

> [!example] Esempio di funzionamento
> ![](https://i.imgur.com/es0tY0F.png)
> Quando un programma esegue l'istruzione `TRAP`:
> 1) Registri di controllo salvati nella **SRIA**,
> 2) Registri di controllo impostati ai valori specificati nell'***interrupt vector***,
> 3) L'***interrupt handler***:
>    - Salva il contenuto dei registri generali,
>    - Controlla l'IC per ottenere il parametro della `TRAP`,
>    - Esegue le sue funzioni (in base al parametro),
>    - Invoca lo ***scheduler***.
> 4) Se seleziona il programma interrotto, lo scheduler:
>    - Ripristina i registri generali,
>    - Ripristina i registri di controllo coi valori nella SRIA (istruzione `IRET`) facendo quindi ripartire il programma.
> 5) Il programma legge il valore di ritorno della `TRAP` (aspettato in `R0` dei registri generali, però se l'handler lo scrivesse subito, il valore verrebbe sovrascritto, perciò l'handler lo sovrascrive direttamente nella parte di memoria in cui sono salvati i registri generali, così che `R0` avrà già il valore corretto al ripristino).

###### System call

Con le ***traps*** è quindi possibile realizzare le varie ***system call***, richieste all'OS da parte di un programma che:

- Costituiscono l'interfaccia che permette ai programmi di comunicare con l'OS,
- Si distinguono in base al parametro della `TRAP` (e ad altri parametri propri di *system call*), quindi se l'IC ha $n$ bit, si hanno $2^{n}$ *system call* diverse (di solito $n \geq 8$),
- Sono disponibili in varie librerie di funzioni associate alle *system call* (per esempio in C sono in assembly ed invocabili da programmi in C).

###### Altro

![](https://i.imgur.com/2coc5W4.png)

In UNIX/Linux ci sono circa 100 *system call*, fra cui:

![](https://i.imgur.com/GLkAcot.png)

---

Prossima lezione: [[3 - Dispositivi e controller]]

