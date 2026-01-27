# Lezione 5

### Processi

Un processo è un (istanza di) "esecuzione" di un programma.

> [!info] Osservazioni
> - Un **programma** è un'<u>entità passiva</u>, che non esegue nessuna azione di per sé (il processo ne concretizza le azioni),
> - Le entità schedulate dall'OS sono processi, non programmi,
> - In un OS con <u>multiprogrammazione</u>, più processi coesistono ed eseguono "contemporaneamente",
> - Si possono avere più processi relativi al medesimo programma (i quali non devono interferire tra di loro ed accedere solo alle proprie aree di memoria designate).

###### Componenti

Un processo (non programma) si compone di:

- Le sue risorse logiche (tipo file...) e fisiche (tipo dispositivi...),
- Le sue aree di testo, dati e stack,
- Lo stato della CPU, ovvero il contenuto dei registri (generali e di controllo).

> [!info] Nota
> Se si esegue un programma più volte, tutti i processi risultanti hanno la medesima area di testo (in quanto tale non è modificabile durante l'esecuzione).

##### Parallelismo e concorrenza

Nei sistemi con CPU singola l'OS la assegna "a turno" ai vari processi (ciò è detto ***interleaving***), quindi il loro parallelismo è <u>simulato</u> (con un DMA controller si possono avere processi e operazioni di I/O parallele, ma tale non è un parallelismo che riguarda l'evoluzione dei processi). 

Il parallelismo (quello vero dei processi) si ha quando <u>più processi sono eseguiti</u> (*evolvono*) <u>nello stesso momento</u> (si può avere solo con [[#Sistemi multi-core|CPU multi-core]]); mentre la **concorrenza** è l'<u>"illusione" del parallelismo</u>, ovvero quando sembra che più processi si evolvono in parallelo ma in realtà <u>ognuno concorre alle risorse</u> che gli servono.

![](https://i.imgur.com/NrBfN25.png)

Nell'esempio, l'*overhead* si ha quando l'OS sottrae la CPU a un processo per darla ad un altro (rosa) o quando si ha un interrupt che chiama l'handler e lo scheduler riassegna la CPU al processo precedentemente messo "in pausa" (verde).

###### Velocità di evoluzione

La **velocità di evoluzione** di un processo (quella con cui vengono eseguite le sue istruzioni) **non è uniforme** nel tempo in quanto in certi momenti dispone della CPU mentre in altri no. Inoltre essa **non è riproducibile**:

- Né la <u>velocità dello stesso</u> (in quanto tale è ***CPU-bound*** e ***I/O-bound***, quindi diverse esecuzioni identiche possono richiedere tempi diversi),
- Né la <u>velocità relativa agli altri</u> (ovvero come avanza rispetto ad altri processi per il motivo suddetto).

###### Sistemi multi-core

Se sono disponibili <u>più CPU</u> (o <u>core</u>) il parallelismo è invece **reale** (per processi in esecuzione su più CPU/core diversi); e si distingue tra 2 casi:

- ***Multiprocessing***: più processi eseguono su una macchina con più CPU/core,
- ***Distributive processing***: più processi eseguono su più macchine distribuite e indipendenti.

> [!info] Nota
> Tali casi sono comunque <u>limitati dal n° di CPU/core</u>, in quanto se ci sono <u>più processi che CPU/core</u>, si ha comunque **concorrenza**.

#### Stati di un processo

Di base, un processo si può trovare almeno in 1 di 3 stati:

- ***Running***: il processo <u>è in esecuzione sulla CPU</u> (con singola CPU si ha 1 processo *running* per volta o nessuno; comunque per convenzione un processo è sempre *running* anche quando è interrotto da un *interrupt* e si sta eseguendo il codice dell'*handler*).
- ***Ready***: il processo non è in esecuzione ma <u>è pronto per avere la CPU ed iniziare ad evolversi</u> (ha tutte le altre risorse che gli servono).
- ***Waiting***: il processo non è in esecuzione e non sarebbe in grado di evolversi anche se ottenesse la CPU in quanto <u>sta aspettando un evento</u> (tipo che si liberi una risorsa occupata...); questo è detto anche *blocked* o *sleeping*.

##### Transizioni

Ci sono 4 possibili **transizioni** da stato a stato (dei precedenti):

![](https://i.imgur.com/6RI2xU0.png)

- ***Ready*** $\rightarrow$ ***running***: lo *scheduler* <u>seleziona il processo da eseguire e gli assegna la CPU</u> (in caso di più processi *ready*, la scelta è effettuata in base alla **politica di *scheduling*** o alla loro **priorità**; tale è l'unica modalità di schedulazione, infatti i processi non possono forzare/manipolare lo scheduler).
- ***Running*** $\rightarrow$ ***ready***: quando la <u>CPU è sottratta ad un processo per essere data ad un altro</u> (seppur il 1° può continuare ad evolversi); e ciò avviene in 2 casi:
  - ***Preemption***: quando è diventato *ready* un processo con priorità maggiore,
  - ***Time slice expiration***: quando scade la *time slice* del processo.
- ***Running*** $\rightarrow$ ***waiting***: il <u>processo è impossibilitato ad evolversi a causa di un evento bloccante</u> ed attende un evento *sbloccante* (tipo con operazioni di I/O),
- ***Waiting*** $\rightarrow$ ***ready***: <u>si verifica l'evento</u> *sbloccante* <u>che sblocca il processo</u> (tale può poi passare direttamente da *ready* a *running* o meno in base allo *scheduling*).

##### Caso UNIX system V

Nel sistema **UNIX system V** sono definiti 8 stati in cui i processi si possono trovare:

![](https://i.imgur.com/m6qETGU.png)

> [!important] Swap
> Introduciamo il concetto della **memoria virtuale** (o ***swap area***): essa è una <u>parte di memoria del disco fisso nella quale vengono salvati dei processi inattivi</u>. 
> Questo permette a <u>più processi di quanti ce ne stiano in RAM di esistere senza bloccarla</u> (concorrenza anche per la RAM) e le operazioni di *swapping* sono:
> - ***Swap out***: quando serve liberare RAM, l'OS sposta certi processi da essa alla *swap area* del disco designato (l'OS preferisce quelli *waiting*, poi quelli *ready*),
> - ***Swap in***: quando si spostano dei processi dal disco alla RAM a certi intervalli di tempo (solo per i processi ready e in base a quanta RAM è libera).

###### Ready e waiting

Gli stati *ready* e *waiting* sono suddivisi in 2 sottostati: ***in memory*** e ***swapped*** per la gestione della memoria virtuale. Tali processi possono avere le aree di testo, dati e stack <u>interamente in RAM</u>, <u>interamente su disco</u> o <u>in parte su uno ed in parte sull'altro</u>.

Nota: le operazioni di spostamento da RAM a disco e viceversa sono **lente** a causa dell'<u>elevato tempo di accesso al disco</u>.

###### Running

Lo stato *running* si divide in ***user running*** e ***kernel running***. Un processo è ***user running*** quando la CPU sta eseguendo il suo codice, mentre è ***kernel running*** quando:

- <u>Sta venendo schedulato</u>: quindi quando l'OS deve preparare i registri per eseguirlo (temporaneamente, poi ripassa ad *user running*),
- <u>Si ha un interrupt</u>: quindi avviene una transizione *user running* $\rightarrow$ *kernel running* e rimane in tale stato finché l'handler non ha finito di eseguire, poi può tornare *user running*/*waiting*/*ready* in base allo scheduler.

> [!info] Interrupt a cascata
> In caso di **interrupt a cascata**, per evidenziare il fatto che sono eseguiti *handler* diversi, si dice che c'è una transizione *kernel running* $\rightarrow$ *kernel running*.

###### Altri

Infine, un processo può anche essere:

- ***Created***: quando l'OS sta "costruendo" il processo dal programma per poi farlo diventare *ready in memory* se c'è spazio in RAM, altrimenti *swapped* (un processo *created* non può andare in *waiting* dato che è sicuramente pronto ad eseguire la sua prima istruzione).
- ***Zombie***: quando un processo termina diventa *zombie*, uno stato in cui vengono raccolte delle sue statistiche prima di cancellarlo completamente.

> [!info] Nota
> L'unica transizione per diventare ***zombie*** è *kernel running* $\rightarrow$ *zombie* in quanto:
> - Quando il processo finisce i suoi compiti, l'ultima istruzione che esegue (in UNIX) è la *system call* [[#Exit|exit]] che chiede all'OS di terminare il programma,
> - Se il processo si arresta a causa di una situazione anomala, è comunque l'OS (un [[#Interrupt|interrupt handler]]) che lo termina.

#### PCB

L'OS tiene traccia dei processi nel sistema mantenendo una struttura dati chiamata ***process table*** che contiene, per ogni processo, un **PCB** (*Process Control Block*). 

![](https://i.imgur.com/6Lr7LNK.png)

I dati in esso variano per OS, tuttavia quelli necessari sono:

- Il **PID** (*Process Identifier*): l'identificatore univoco per ogni processo esistente,
- Lo **stato del processo**, 
- Lo **stato della CPU**: i valori dei registri (generali e di controllo) salvati quando il processo perde la CPU (ripristinabili quando il processo torna *running*),
- La **priorità** (e altri parametri di *scheduling*),
- **Puntatori** a varie zone di memoria per accedere alle aree di testo, dati e stack, ai file aperti ed ai dispositivi disponibili (dato che i PCB hanno dimensione fissa),
- 1 o più ***PCB pointers***: puntatori ad altri PCB al fine di realizzare strutture dati (tipo liste...) per gestire scheduling...

###### Ready queue scheduling

Un esempio di uso dei *PCB pointers* è l'implementazione di una ***queue*** (coda) per lo *scheduling* dei processi ***ready***: grazie a 2 soli puntatori aggiuntivi (per indicare inizio e fine della coda) si realizza una struttura dati semplice ed efficiente per il <u>basso overhead</u> (inserimento e rimozione dalla coda hanno complessità costante):

![](https://i.imgur.com/QG262gT.png)

##### Paging

Nei sistemi moderni i processi possono essere allocati in RAM in modo **non contiguo**: ciò è gestito con un meccanismo di ***paging***, ovvero "paginando" la RAM in più ***page frame*** della stessa dimensione. 

Per esempio, una memoria da $2^{32}$ byte (4GB) potrebbe essere divisa in *frame* da $2^{10}$ byte (1kB) l'uno, perciò ogni indirizzo di memoria sarebbe così:

![](https://i.imgur.com/j5CYqFo.png)

Con il *page frame* identificato dai 22 bit più significativi mentre il resto indica l'*offset* (a quali byte del *frame* corrisponde l'indirizzo). Analogamente, anche le aree di testo, dati e stack dei processi possono venir divise in **pagine** della stessa dimensione dei frame ($2^{10}$ byte); ed ognuna può essere caricata in qualsiasi *frame* (comunque l'OS deve tenere traccia di quali *frame* sono occupati da ogni processo).

> [!info] Pagine virtuali e fisiche
> La **MMU**, siccome traduce indirizzi virtuali in fisici, <u>traduce anche pagine virtuali in fisiche</u>, salvando le corrispondenze nella ***page table***. 
> - Le **pagine fisiche** sono dei *page frame* che possono contenere le aree di testo, dati e stack dei processi (non contigui, come vi si riferiscono i processi?),
> - Le **pagine virtuali** invece sono blocchi di memoria astratti (riferite con indirizzi virtuali) che fanno apparire le varie pagine fisiche come una unica grande area di memoria (logicamente) indirizzabile e isolata ai singoli processi.

###### Page faults

Dato che non è detto che tutte le pagine virtuali risiedano in RAM (potrebbero essere ***swapped out*** per liberare memoria), si rischia di accedere ad una pagina nello *swap device* (disco). Questo comporta un'eccezione chiamata ***page fault*** e quindi un *interrupt* che richiede all'OS di caricarla in RAM (se non è nella cache del disco, è richiesta un'operazione I/O che manda il processo in *waiting* per un po').

![](https://i.imgur.com/Z1f9Ayl.png)

Per ogni pagina virtuale (area testo e dati, quella di stack non ha ), l'OS mantiene una voce nella ***page table*** con (almeno) le seguenti informazioni:

- <u>N° del frame</u> in cui è caricata (`NULL` qui indica che la pagina non è in RAM),
- <u>Indirizzo di pagina nello swap device</u> (`NULL` indica che la pagina non è mai stata nello *swap device*, nemmeno come copia),
- <u>Indirizzo del file di backing nel disco</u> (indirizzo dell'eseguibile originale).

#### Context e operazioni

Il **contesto** (o <u>ambiente</u>) di un processo (***process context***) è costituito da:

- ***Register context***: il contenuto dei registri della CPU,
- ***User-level context***: le aree di testo, dati e stack in RAM a cui il processo può accedere,
- ***System-level context***: le informazioni relative al processo gestite dall'OS (tipo PCB, i puntatori di questo ed il ***kernel stack*** un *call stack* degli *interrupt handler*).

###### Operazioni sui processi

L'OS esegue 3 operazioni fondamentali per garantire l'esecuzione dei processi:

- ***Context save***: quando un processo *running* perde la CPU, l'OS ne salva il *context* all'interno del suo PCB,
- *Scheduling*: quando, in base ad una certa <u>politica</u>, l'OS sceglie un processo da eseguire tra quelli *ready*,
- ***Dispatching***: quando l'OS ripristina il *context* di un processo schedulato sfruttando i dati salvati nel suo PCB col *context save*.

##### Context switch

Si ha un ***context switch*** quando l'OS: 1) esegue il ***context save*** di un processo $P$, 2) **schedula** un altro processo $P'$ e 3) effettua il ***dispatching*** per $P'$.

Seppur fondamentale, il *context switch* può causare: 

- ***Overhead* significativo**: se l'algoritmo di scheduling è complesso,
- **Rallentamenti dell'OS**: in quanto le varie cache contengono dati utili a $P$, quindi finché non si ripopolano, $P'$ evolverà più lentamente del normale.

###### Esempio 1

Ch. 4: pages 58-63 / Azzolini context switch

###### Esempio 2

Ch. 4: pages 64-69 / Azzolini context switch

###### Esempio 3

Ch. 4: pages 70-77 / Azzolini context switch

#### Creazione e terminazione di processi

Gli OS permettono la creazione di processi da parte di altri processi. Ciò è possibile anche in UNIX/Linux con la system call `fork`, la quale rende il processo creatore un <u>padre</u> ed il processo creato un <u>figlio</u> del precedente (quindi si crea una gerarchia in cui ogni processo può avere 1 solo padre ma più figli).

##### Creazione

###### Fork

La `fork` di per sé <u>clona il processo padre in un processo figlio quasi identico</u>, che vi differisce solo per il PCB (con PID diversi) e il valore di registri ed aree di testo, dati e stack per la variabile in cui è salvato il valore della `fork` (vedi poi `x`). Un esempio:

```c
int main(void) { 
	int p = getpid();    // ritorna il PID del processo corrente
	int x = fork();      // ritorna 0 al figlio e il PID del figlio al padre
	// if su fork
	if (x == 0) {
		printf("Figlio = %d\n", getpid());                   // eseguito solo da figlio
	} else {
		printf("Padre = %d, Figlio = %d\n", getpid(), x);    // eseguito solo dal padre
	} 
}
/* POSSIBILE ESECUZIONE (dove è schedulato prima il padre):
Padre = 2085, Figlio = 2086
Figlio = 2086
*/
```

Quindi in sequenza si ha:

1) Con `getpid()` si richiede l'intervento dell'OS per ottenere il PID del processo corrente, che è salvato nel suo PCB (quindi nella *kernel area* della RAM).
2) Il processo si clona con `fork()` con i valori in `x` specificati dal commento per padre e figlio,
3) Padre e figlio eseguono i rispettivi rami dell'`if` in base alla condizione su `x` (in caso di istruzioni comuni prima dell'`if`, entrambi le avrebbero eseguite).

##### Gestione

###### Exec

Dopo la clonazione di un processo con `fork`, per <u>eseguire un nuovo processo differente</u> si usa la *system call* `exec`, la quale <u>sostituisce il codice</u> (eventualmente) <u>del processo creato con quello del programma che si vuole eseguire</u>. Un esempio:

```c
int main(void) { 
	int p = getpid(), x = fork(); 
	if (x == 0) { 
		execl("b.out", "b.out", NULL);    // Sostituisce il codice del processo con quello nel file "b.out"
	} else { 
		int s;
		wait(&s);                         // Passo un puntatore ad s alla wait così che ottenga il suo stato di terminazione
		printf("Padre: mio figlio %d ha terminato ed ha stato %d\n", x, s); 
	} 
}
/* POSSIBILE ESECUZIONE:
Eseguito "b.out" (non si vede, è un printf all'interno di "b.out")
Padre: mio figlio 2086 ha terminato ed ha stato 0
*/
```

Qui `execl` è una funzione che corrisponde alla system call `exec` i cui effetti principali sono:

- Sostituzione delle aree di testo, dati e stack con quelle di "b.out",
- PSW, PC e SP assumono i valori necessari per eseguire "b.out",
- I registri generali sono "azzerati",
- Vengono chiusi eventuali file aperti e rilasciati eventuali dispositivi I/O in uso.

###### Wait

Con la *system call* `wait` un <u>padre chiede all'OS di essere messo in waiting finché non termina uno qualsiasi dei suoi figli</u> (quando il figlio chiama `exit`, l'interrupt handler rileva che la terminazione è attesa dal padre e lo imposta a *ready*).

Passando un puntatore ad una variabile alla `wait` il padre può ottenere in quella variabile il valore del parametro di `exit` del figlio terminato.

##### Terminazione

Quando un processo termina: <u>rilascia</u> tutte le <u>risorse</u>, i suoi <u>figli</u> possono essere <u>terminati o meno</u> (in UNIX diventano figli del processo "init") e (finché non è terminato dal padre) il <u>PCB rimane in stato zombie</u> per poi essere distrutto.

Abbiamo già detto che la terminazione di un processo è sempre fatta dall'OS, ma può avvenire per diversi motivi:

###### (Interrupt)

Un processo può terminare forzatamente dall'*interrupt handler* delle **eccezioni** (tipo in seguito ad una violazione di memoria).

###### Exit

La *system call* `exit` è usata per <u>terminare il processo che la chiama</u> ed ha un **parametro**: un numero intero che indica lo <u>stato di terminazione</u> (generalmente 0 indica una terminazione regolare senza errori, ma comunque si possono definire degli *exit codes* personalizzati per gestire vari casi di terminazione).

###### Kill

Esiste il comando `kill`, col quale un processo può richiedere la terminazione di un altro, tuttavia tale operazione va a buon fine solo se il "killer" ha il diritto di eseguire tale operazione (per esempio in UNIX un padre può sempre uccidere un figlio).

#### Tipi di processi

In UNIX esistono 3 tipi di processi:

##### User process

Uno ***user process*** è un processo <u>associato ad un utente</u> (non solo che esegue in *user mode*) e che ha bisogno di usare le *system call* per richiedere i servizi dell'OS (questi sono la maggior parte dei processi, compresa la ***shell***).

###### Shell

La ***shell*** è uno *user process* normalmente in *waiting* che attende gli input dell'utente e che, quando riceve un comando, avvia il programma specificato. Supponendo di avere un programma "a.out", la *shell* può eseguirlo in 2 modi:

- Esecuzione **classica** (comando `a.out`): 1) la shell fa una `fork`, 2) il figlio fa `exec` su "a.out" mentre il padre fa la `wait` e 3) quando il figlio termina, il padre si rimette in attesa di un altro comando da parte dell'utente.
- Esecuzione **in background** (comando `a.out&`): `fork` ed `exec` sono uguali alla precedente ma poi il padre (shell) non fa la `wait` e si mette subito in attesa di altri comandi.

##### Daemon process

Un ***daemon process*** è un processo che esegue in *user mode* che però <u>non è associato ad alcun utente</u>. Questi generalmente: <u>non terminano</u>, passano gran parte della loro vita in *waiting* e svolgono <u>operazioni di routine</u> (spesso importanti per l'OS).

Un esempio è `getty`, che gestisce il login degli utenti al terminale e avvia la shell (con `fork`, in caso di login con successo) ed attende che termini (con `wait`).

##### Kernel process

Un ***kernel process*** sono dei *daemon* che eseguono in *kernel mode* che non hanno bisogno di system call e possono controllare i propri parametri di scheduling... Esempi sono lo ***swapper process*** (che gestisce lo swapping) e lo ***stealer process*** (che fa lo *swap out* delle pagine che non hanno avuto accessi di recente).

---

Prossima lezione: [[6 - Thread]]

