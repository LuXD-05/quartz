# Lezione 7

### Sincronizzazione

Oltre ai vari vantaggi, ci sono diverse problematiche legate all'interazione tra processi/thread da gestire quando si usa la programmazione concorrente. Per semplicità, supponiamo quindi (per i punti che seguono) che più processi <u>condividano una zona di memoria</u> (come nell'[[6 - Thread#Esempio thread|esempio coi thread]]).

###### Tipi di interazioni

Esistono 4 tipi di interazioni tra processi:

- ***Data sharing***: i processi condividono dati situati in memoria/file condivisi,
- ***Control synchronization***: un'azione $a$ di un processo $P$ è abilitata solo dopo che un altro processo $P'$ ha svolto un'azione $a'$,
- ***Message passing***: un processo $P$ invia un messaggio ad un processo $P'$ che lo riceve,
- ***Signals***: un processo $P$ invia un <u>segnale</u> (messaggio vuoto) ad un processo $P'$ per segnalargli una situazione particolare.

##### Processi interagenti e indipendenti

Dato un processo $P$ (o anche un thread), l'insieme di <u>dati letti da esso</u> si dice `read_set` (o $R$), mentre l'insieme di <u>dati scritti da esso</u> si dice `write_set` (o $W$) (ciò vale anche se $P$ legge/scrive un dato solo in alcune circostanze o in base a certe condizioni, perché c'è comunque la possibilità di lettura/scrittura del dato).

Quindi, 2 processi (o thread) $P_{1}$ e $P_{2}$ si dicono **interagenti** (contrario di **indipendenti**) se:

- $R_{1}$ e $W_{2}$ hanno <u>intersezione non vuota</u> ($R_{1} \cap W_{2} \neq \emptyset$),
- $R_{2}$ e $W_{1}$ hanno <u>intersezione non vuota</u> ($R_{2} \cap W_{1} \neq \emptyset$).

###### Comportamento di processi

Sia processi interagenti che indipendenti <u>competono per le risorse rallentandosi a vicenda</u>, tuttavia c'è una differenza fondamentale:

- **Processi indipendenti**: i loro comportamenti sono <u>riproducibili</u> in quanto non dipendono dalla loro velocità relativa,
- **Processi interagenti**: i loro comportamenti <u>non</u> sono <u>riproducibili</u> in quanto dipendono dalla loro velocità relativa (questo significa che in base a chi è schedulato per 1°, i risultati delle esecuzioni di entrambi i processi potrebbero, seppur con gli stessi input, dare <u>risultati diversi</u>).

> [!info] Nota
> Il fatto che i comportamenti dei processi <u>non siano riproducibili</u> è **inevitabile**, **accettabile** e a volte **desiderabile** (va bene che tra 2 processi che competono per una risorsa se la aggiudichi solo 1 dei 2), anche se esistono meccanismi per forzare l'ordine di esecuzione di determinate azioni.

###### Esempio di non riproducibilità

Vediamo un esempio di comportamento non riproducibile con 2 processi $P_{1}$ e $P_{2}$ (simile agli esercizi sulle *race condition* dell'esame):

```c
// Variabile condivisa
int x = 100;

void *f1() {        // Funzione eseguita da P1
	x = 10;         // Modifica di x
	pthread_exit(NULL); 
} 

void *f2() {        // Funzione eseguita da P2
	int y = x + 5;  // Lettura di x
	printf("y = %d\n", y); 
	pthread_exit(NULL); 
} 

int main(void) { 
	pthread_t t1, t2; 
	pthread_create(&t1, NULL, f1, NULL); 
	pthread_create(&t2, NULL, f2, NULL); 
}
```

$P_{1}$ e $P_{2}$ sono processi **interagenti** in quanto $R_{1} \cap W_{2} = \{x\} \neq \emptyset$; infatti il risultato dipende dall'<u>ordine di esecuzione</u> dei 2 processi (e da scheduling, priorità...), quindi si può dire che il comportamento di $P_{2}$ <u>non è riproducibile</u>, in quanto:

- A volte $P_{2}$ stampa "$105$" (`f1(f2()) = ...`, `f2()` stampa "${} 100 + 5 {}$") ,
- A volte $P_{2}$ stampa "$15$" (`f2(f1()) = f2(10)`, `f2()` stampa "$10 + 5$").

#### Race condition

Dati 2 <u>processi/thread</u> $P_{1}$ e $P_{2}$, un <u>dato condiviso</u> $d$ con <u>valore</u> $v$, 2 <u>operazioni</u> $o_{1}$ ed $o_{2}$ (eseguite rispettivamente da $P_{1}$ e $P_{2}$) e 2 <u>funzioni</u> $f_{1}$ ed $f_{2}$ (che eseguono rispettivamente $o_{1}$ ed $o_{2}$ su $d$) che modificano $v$:

Le operazioni $o_{1}$ ed $o_{2}$ danno luogo ad una ***race condition*** (corsa critica) sul dato condiviso $d$ se, dopo aver eseguito entrambe, $v$ è <u>diverso dal valore che potrebbe assumere eseguendo le funzioni negli ordini possibili</u>: `f1(f2(v))` o `f2(f1(v))`.

###### Conseguenze

Le *race condition* hanno sempre 3 effetti:

- Il <u>comportamento di processi/thread non è corretto</u>,
- I <u>dati</u> sui quali ha luogo la *race condition* diventano ***inconsistenti*** (<u>assumono stati non previsti</u>),
- I comportamenti non previsti non sono riproducibili, quindi diventa <u>più difficile il debugging</u> dei programmi.

###### Esempio race condition

Riprendiamo l'esempio precedente con qualche modifica e l'aggiunta di `pthread_join()`, che permette di <u>aspettare la fine del thread specificato</u> (manda in *waiting* il processo principale sincronizzando la fine di `t1` e di `t2`, cosicché la `x` sarà stampata <u>solo dopo che entrambi i processi terminano</u>):

```c
int x = 100;             // d
void *f1() {
	x = x + 10;          // o1
	pthread_exit(NULL); 
} 
void *f2() {
	x = x + 5;           // o2
	pthread_exit(NULL); 
} 
int main(void) { 
	pthread_t t1, t2; 
	pthread_create(&t1, NULL, f1, NULL); 
	pthread_create(&t2, NULL, f2, NULL);
	pthread_join(t1, NULL);
	pthread_join(t2, NULL);
	printf("%d", x); 
}
```

I risultati che ci si aspetterebbe sono `f1(f2(100)) = f2(f1(100)) = 115`, tuttavia questa aspettativa è errata in quanto le operazioni $o_{1}$ = `x = x + 10` e $o_{2}$ = `x = x + 5` non sono **atomiche**, ovvero sono composte da altre <u>sotto-operazioni che non eseguono in ordine</u>, quindi danno origine a una ***race condition***.

Infatti i risultati da aspettarsi da un'esecuzione del suddetto codice sarebbero: 115, 110 e 105.

> [!warning] Attenzione
> Le sotto-operazioni che compongono un'operazione di riassegnamento di `x` sono: 1) <u>leggi</u> `x`, 2) <u>esegui</u> `x + n`, 3) <u>salva</u> `x + n` in `x`; e seppur sia stata fatta una `join` sui thread, non si sa <u>in che ordine tali operazioni vengano eseguite</u>, ma si possono delineare 3 casi con 3 risultati diversi:
> - `x` = $\color{lime}{115}$: quando tutte le sotto-operazioni di $o_{1}$ o $o_{2}$ sono eseguite per poi far eseguire le altre (per esempio $o_{1}$ legge, somma e salva il risultato in `x` e solo dopo ciò $o_{2}$ fa lo stesso e viceversa).
> - `x` = $\color{red}{110}$: quando $o_{1}$ legge `x` (100) e salva `x + 10` in `x` dopo che $o_{2}$ ha già salvato `x + 5` in essa (anche se $o_{2}$ salva 105 in `x`, $o_{1}$ somma 10 al valore iniziale di `x` perché lo ha letto prima che $o_{2}$ lo modificasse, quindi "vince" perché è ultimo).
> - `x` = $\color{red}{105}$: quando $o_{2}$ legge `x` (100) e salva `x + 5` in `x` dopo che $o_{1}$ ha già salvato `x + 10` in essa (anche se $o_{1}$ salva 110 in `x`, $o_{2}$ somma 5 al valore iniziale di `x` perché lo ha letto prima che $o_{1}$ lo modificasse, quindi "vince" perché è ultimo).

#### Sezioni critiche

Una **sezione critica** (*critical section*) per un dato condiviso $d$ è una <u>porzione di codice</u> che viene <u>eseguita non concorrentemente</u> (con se stessa o altre per $d$), in quanto tra di loro sono **mutuamente esclusive**: quando un processo/thread accede ad una di esse, impedisce a tutti gli altri di accedere a qualsiasi altra sezione critica di $d$.

Con esse e con la mutua esclusione, è possibile eliminare le *race condition* per un certo dato $d$ (1 processo/thread per volta modifica $d$), tuttavia rimane la difficoltà di come implementarle.

##### Implementazioni errate

Le implementazioni di sezioni critiche devono soddisfare alcune proprietà:

- **Correttezza**: deve essere garantita la mutua esclusione (le sezioni critiche per un dato $d$ non possono essere eseguite concorrentemente),
- **Progresso**: se nessun processo/thread sta eseguendo una sezione critica per $d$ e alcuni vogliono farlo, 1 di essi deve poter eseguire tale sezione critica per $d$,
- **Attesa limitata** (*bounded wait*): quando un processo/thread $P$ vuole eseguire una sezione critica, gli altri processi (che ci stanno accedendo o vogliono accedervi) possono accedervi solo un certo n° ($k$) di volte, dopo le quali "tocca" necessariamente a $P$.

> [!important] Starvation
> Le proprietà di **progresso** e ***bounded wait*** servono a prevenire la ***starvation***, ovvero l'<u>attesa infinita da parte di un processo per eseguire una sezione critica</u>.

###### Disabilitare interrupt

Questa implementazione prevede di <u>disabilitare gli interrupt prima della sezione critica</u> e <u>riabilitarli al termine</u> di quest’ultima:

```c
//...
disable_interrupt();
// { critical section }
enable_interrupt();
//...
```

> [!error] Implementazione errata
> Seppur funzionante su sistemi monoprocessore, essa necessita che sia possibile disabilitare gli interrupt da un programma utente (in *user mode*), creando il rischio che il programma possa monopolizzare la CPU.

###### Variabili lock condivise

Data una variabile condivisa `lock = 0` si ha:

```c
//...
while (lock != 0) {}
lock = 1;
// { critical section }
lock = 0;
//...
```

Con questo, ad ogni processo che vuole entrare in una sezione critica è imposto di controllarne il valore e:

- Se `lock = 0` ("aperta"): lo imposta a $1$, esegue la sezione critica e lo reimposta a $0$,
- Se `lock = 1` ("chiusa"): la sezione critica è occupata, quindi il processo aspetta finché `lock != 0`.

> [!error] Implementazione errata
> Questa soluzione prevede l'uso di un dato condiviso per evitare *race condition* su altri dati condivisi quando essa stessa è soggetta a *race condition* (se 2 processi leggono `lock = 0` prima che 1 dei 2 esegua `lock = 1` allora entrambi entrano concorrentemente nella sezione critica).

###### Variabili di turno condivise 1

Con questa soluzione ogni processo da il turno ad un altro quando ha finito di eseguire la sezione critica (esempio con $P_{1}$ e $P_{2}$):

```c
// Codice P1
while (true) {
	//...
	while (turn != 0) {}
	// { critical section }
	turn = 1;
	//...
}
// Codice P2
while (true) {
	//...
	while (turn != 1) {}
	// { critical section }
	turn = 0;
	//...
}
```

Questa si applica a 2 processi ma può anche essere generalizzata per un n° superiore di essi (diventando progressivamente più complicata).

> [!error] Implementazione errata
> Nonostante garantisca <u>correttezza</u> (mutua esclusione in ogni momento) e <u>bounded wait</u> (dato che i processi si alternano per eseguire le sezioni critiche), questa soluzione <u>non soddisfa il progresso</u> (se il processo di turno non esegue la propria sezione critica e fa altro, non passa il turno all'altro processo, essendo l'unico che può modificare la variabile di turno, mandandolo inevitabilmente in *starvation*).

###### Variabili di turno condivise 2

Qui, invece di `turn`, usiamo 2 variabili booleane `c1` e `c2` che se vere, indicano rispettivamente che $P_{1}$ o $P_{2}$ sono nella sezione critica (possibile entrambe false):

```c
// Codice P1
while (true) {
	//...
	while (c2) {}
	c1 = true;
	// { critical section }
	c1 = false;
	//...
}
// Codice P2
while (true) {
	//...
	while (c1) {}
	c2 = true;
	// { critical section }
	c2 = false;
	//...
}
```

> [!error] Implementazione errata
> Rispetto alla precedente, questa soluzione garantisce il <u>progresso</u> (ogni processo rimane in *busy waiting* finché la variabile che indica che l'altro è dentro è `true`), tuttavia è comunque errata in quanto non garantisce la <u>correttezza</u> (se $P_{1}$ cambia `c1` in `false` passa per il `while(c2)` prima che $P_{2}$ imposti `c2 = false`, oppure viceversa, entrambi i processi eseguono la sezione critica concorrentemente).

###### Variabili di turno condivise 3

Qui si sposta l'assegnamento a `true` di `c1` e `c2` prima della *busy waiting* del processo:

```c
// Codice P1
while (true) {
	//...
	c1 = true;
	while (c2) {}
	// { critical section }
	c1 = false;
	//...
}
// Codice P2
while (true) {
	//...
	c2 = true;
	while (c1) {}
	// { critical section }
	c2 = false;
	//...
}
```

Rispetto alla precedente, questa garantisce la <u>mutua esclusione</u> in quanto garantisce che le variabili booleane siano una vera e una falsa in ogni momento.

> [!error] Implementazione errata
> Nonostante ciò, l'implementazione è comunque errata in quanto può succedere che entrambe le variabili `c1` e `c2` siano impostate a `true` prima che vengano eseguiti i controlli, in tal caso si ha un ***deadlock*** (o stallo): una situazione in cui 2 o più processi si bloccano a vicenda indefinitamente in attesa di una risorsa (quindi violato il <u>progresso</u>).

###### Variabili di turno condivise 4

Qui viene continuamente reso falso il valore della variabile di un processo finché quella dell'altro è vera (per impedire che diventino entrambe vere):

```c
// Codice P1
while (true) {
	//...
a:  c1 = true;
	while (c2) {
		c1 = false;
		goto a;
	}
	// { critical section }
	c1 = false;
	//...
}
// Codice P2
while (true) {
	//...
b:  c2 = true;
	while (c1) {
		c2 = false;
		goto b;
	}
	// { critical section }
	c2 = false;
	//...
}
```

Questa soluzione elimina il deadlock e garantisce la mutua esclusione.

> [!error] Implementazione errata
> Tuttavia anche questa implementazione non è corretta in quanto si può verificare il ***livelock***: una situazione in cui 2 processi continuano a modificare i propri stati in risposta agli altri senza effettivamente compiere progressi nel proprio *task*, ostacolandosi a vicenda (non rispetta il <u>progresso</u>).

##### Implementazioni corrette

Da qui in poi (nei seguenti paragrafi) vediamo delle implementazioni corrette di sezioni critiche; ma per proseguire è necessaria una definizione:

###### Operazione indivisibile

Un'**operazione indivisibile** (o **atomica**) su un dato condiviso $d$ è un'operazione che è certamente eseguita in modo non concorrente su $d$ (quindi non può dar luogo a *race condition* si $d$).

###### Istruzione TS

Il 1° caso di implementazione corretta delle sezioni critiche si ha a basso livello con l'**istruzione TS** (*test and set*) che fa 2 cose su locazione di memoria: 1) controlla se tale locazione ha valore 0 (ponendo il risultato nel bit CC della PSW) e 2) imposta la locazione a una sequenza di 1 indipendentemente dall'esito. In pratica:

```c
// Pseucocodice (simil-C)
//...
while(TS(lock) == 1) {/* busy waiting */}
// { Critical section }
lock = 0;
//...
```

Quindi data `lock` la locazione di memoria, `TS(lock)` ritorna 0 la prima volta e pone `lock` immediatamente a 1 (indivisibile), il processo corrente esegue la sezione critica e poi reimposta `lock = 0` cosicché altri processi possano eseguire la sezione critica.

`TS` è **indivisibile** sulla locazione di memoria su architetture:

- **Monoprocessore**: gli <u>interrupt non possono interromperla</u> (dato che è una singola istruzione e si aspetta che finisca prima di gestirli),
- **Multiprocessore**: va <u>impedito alle altre CPU di accedere alla locazione</u> per evitare di eseguire più `TS` al contempo (altrimenti la trovano tutti a 0).

> [!info] Altro
> Ci possono anche essere delle varianti, tipo TSL (*test and set lock*), TS con un 2° parametro che indica dove salvare il valore del test se non nel bit CC e l'istruzione `exchange` (o `swap`) che non trattiamo nello specifico.
> Ad alto livello non è comunque possibile usare la `TS`, ma ci sono diversi modi per implementare le sezioni critiche: 1) usando un approccio algoritmico (corretto, non come i precedenti), 2) usando ***primitive software*** (*system call* o funzioni di libreria *wrapper*) o 3) costrutti ad hoc per la programmazione concorrente.

#### Algoritmi

I seguenti algoritmi sono implementazioni corrette di sezioni critiche fatte per diversi casi:

##### Algoritmo di Dekker

L'**algoritmo di Dekker** è simile all'esempio in [[#Variabili di turno condivise 4]] ma fa uso anche della variabile `turn` per decidere quale processo accede alla sezione critica quando entrambi vogliono farlo (con inizializzati: `c1 = false`, `c2 = false` e `turn = 0`):

```c
// Codice P1
while (true) {
	//...
    c1 = true;
	while (c2) {
		if (turn == 1) {
			c1 = false;
			while (turn == 1) {} 
			c1 = true;
		}
	}
	// { critical section }
	turn = 1;
	c1 = false;
	//...
}
// Codice P2
while (true) {
	//...
    c2 = true;
	while (c1) {
		if (turn == 0) {
			c2 = false;
			while (turn == 0) {} 
			c2 = true;
		}
	}
	// { critical section }
	turn = 0;
	c2 = false;
	//...
}
```

Questa soluzione è corretta e rispetta la proprietà del progresso, tuttavia è valida solo per 2 processi (per $n$ processi si complica notevolmente).

##### Algoritmo di Peterson

Un'altra soluzione valida è l'**algoritmo di Peterson** in cui: ogni processo ha una flag booleana (che usa per dire di voler accedere alla sezione critica) e se entrambi vogliono eseguirla si usa sempre `turn` ma ogni processo da il turno all'altro subito prima di vedere se può entrare e aspetta che l'altro finisca.

```c
bool flag[] = {false, false}; 
int turn = 0;
// Codice P1
while (true) {
	//...
    flag[0] = true; 
    turn = 1;
	while (flag[1] && turn == 1) {}
	// { critical section }
	flag[0] = false;
	//...
}
// Codice P2
while (true) {
	//...
    flag[1] = true; 
    turn = 0; 
    while (flag[0] && turn == 0) {}
    // { critical section }
	flag[1] = false;
	//...
}
```

###### Algoritmi per più di 2 processi

2 algoritmi per l'implementazione delle sezioni critiche con $n > 2$  sono:

- L'**algoritmo Eisenberg-McGuire** (che estende l'algoritmo di Dekker al caso $n$),
- L'**algoritmo di Lamport**.

#### Semafori

Un **semaforo** (`sem`) è una variabile intera condivisa che può assumere solo valori non negativi e su cui sono possibili solo 3 operazioni:

- (**Inizializzazione**): con un valore $\geq$ 0,
- `wait(sem)`: operazione indivisibile che <u>decrementa il valore del semaforo se > 0</u>, altrimenti se il <u>valore è = 0 il processo</u> che ha chiamato `wait` <u>va in waiting</u>,
- `signal(sem)`: operazione indivisibile che <u>aumenta il valore del semaforo se non ci sono processi in waiting su esso</u>, altrimenti <u>pone uno di tali processi a ready</u>.

> [!important] Nota
> - Non è specificata l'implementazione di `wait` e `signal` ma si assume che siano indivisibili,
> - La logica di scelta del processo da liberare dopo una `signal` non è specificata ma generalmente è **FIFO** (*First In First Out*),
> - (Solo per semafori utilizzati come [[#Semafori come mutex|mutex]]) quando ci sono dei processi bloccati da un semaforo, il suo valore è sempre 0 in quanto: se > 0, il processo non si può bloccare, mentre se ci sono dei processi bloccati, la `signal` non può incrementare il semaforo,

##### Implementazione

Per gestire le sezioni critiche e coordinare l'accesso di processi alle risorse, si possono usare i semafori in 2 modi:

###### Semafori come mutex

Una ***mutex*** è un meccanismo implementabile con semafori che garantisce correttezza e progresso (e volendo anche *bounded wait* se si usa logica FIFO) per una sezione critica. In questo caso il semaforo viene inizializzato a 1 (per indicare che solo 1 processo può accedere alla risorsa) così che quando un processo fa la `wait`, il semaforo viene decrementato a 0 impedendo ad altri di accedere alla sezione critica mandandoli in *waiting*:

```c
int mutex = 1;
//...
while (true) {
	//...
	wait(mutex);               // mutex = 0 --> altri processi vanno in waiting qui
	// { critical section }
	signal(mutex);             // mutex = 1 --> abilita 1 altro processo in waiting ad eseguire la sezione critica
	//...
}
//...
```

Nota:

- Se la mutex fosse inizializzata a un valore > 1 non sarebbe rispettata la <u>correttezza</u> perché più processi potrebbero eseguire la sezione critica al contempo,
- Se la mutex fosse inizializzata a 0, non sarebbe rispettato il <u>progresso</u> in quanto nessun processo potrebbe accedere al semaforo,
- Le mutex sono solo un'"astrazione" degli algoritmi (la parte complicata è nascosta e scontata), ma comunque è il dev che deve rispettare la sequenza `wait` - sezione critica - `signal`.

> [!error] Attenzione
> L'uso dei semafori non è banale: supponiamo di avere 2 semafori `x = 1` e `y = 1`, un processo $P_{1}$ che chiama in ordine `wait(x)` e `wait(y)` ed un altro $p_{2}$ che chiama in ordine `wait(y)` e `wait(x)`; questo modello rischia di portare al ***deadlock***:
> ![](https://i.imgur.com/2ETfoDz.png)

###### Semafori normali

L'implementazione normale dei semafori invece prevede che i semafori possano essere inizializzati a qualsiasi valore $\geq$ 0; e sono usati per specificare quanti processi possono usufruire in contemporanea di una risorsa prima che questa venga (temporaneamente) esaurita, cosicché, quando ciò accade, possono bloccare (mandare in *waiting*) tutti gli altri processi che provano ad accedervi:

```c
int sem = 0;    // Semaforo inizializzato a 0 --> indica che la risorsa è già non più disponibile
int sem = n;    // Semaforo inizializzato a 0 --> indica che al max n processi possono usufruire della risorsa
```

#### Problemi classici di sincronizzazione

Questi sono importanti per gli esami in quanto molti degli esercizi sui semafori si basano su questi:

##### Produttori e consumatori

Questo tipo di problemi si compone di un ***pool* finito di buffer** (possono essere pieni o vuoti, di solito non interessa cosa ci va scritto dentro), dei **processi produttori** (*producers*) che scrivono nei buffer e dei **processi consumatori** (*consumer*) che consumano le info nei buffer (leggono il dato e svuotano il buffer).

La soluzione di questi problemi è valida se:

- L'accesso ai singoli buffer è in mutua esclusione (ma più processi possono accedere a più buffer diversi per volta),
- I produttori non possono sovrascrivere info su buffer pieni,
- I consumatori non possono svuotare buffer vuoti.

> [!warning] Nota
> Le soluzioni non devono includere *busy waiting* (altrimenti non sarebbero esercizi coi semafori) ed deve essere consentito l'accesso concorrente a buffer diversi.

###### Singolo buffer

Con un buffer singolo bastano 2 semafori: `full = 0` (diventa 1 quando è pieno) e `empty = 1` (diventa 1 quando è vuoto). Esempio:

```c
// Producer
while (true) { 
	// ... 
	int item = produce();  // Crea item
	wait(empty);           // Entra se empty > 0 (se buffer vuoto), altrimenti waiting
	buffer = item;         // Scrive nel buffer
	signal(full);          // Aggiorna full (indica che il buffer è ora pieno)
	// ... 
}
// Consumer
while (true) { 
	// ... 
	wait(full);            // Entra se full > 0 (se buffer pieno), altrimenti waiting
	int item = buffer;     // Consuma info nel buffer
	signal(empty);         // Aggiorna empty (indica che il buffer è ora vuoto)
	// ... 
}
```

###### Buffer multipli

Con buffer multipli ($n$) essi sono di solito organizzati in una lista circolare da scorrere con 2 indici (`i` = index 1° buffer vuoto e `j` = index 1° buffer pieno); in più si hanno `full = 0`, `empty = n` e altri 2 semafori: `sp = 1` (mutex per indice produttore `i`) e `sc = 1` (mutex per indice consumatore `j`). Esempio:

```c
// Producer
while (true) { 
	// ... 
	int item = produce();
	wait(empty);
	wait(sp);
	buffer[i] = item;
	i = (i + 1) % n;
	signal(sp);
	signal(full);
	// ... 
}
// Consumer
while (true) { 
	// ... 
	wait(full);
	wait(sc);
	int item = buffer[j];
	j = (j + 1) % n;
	signal(sc);
	signal(empty);
	// ...
}
```

> [!info] Nota
> Certo, non servirebbero 2 semafori `full` e `empty` siccome il valore dell'uno è calcolabile da quello dell'altro, ma non è consentito fare calcoli sui semafori.

##### Lettori e scrittori

Questo tipo di problemi è composto da un'insieme di dati condivisi (tipo una classe o array), dei processi scrittori (*writers*) che modificano i dati e dei processi lettori (*readers*) che leggono solamente i dati (senza cancellarli). 

Una soluzione valida per essi rispetta certe regole:

- Sono ammesse letture concorrenti,
- Non è ammessa la concorrenza tra scritture (perdita di dati) e nemmeno tra letture e scritture (lettura di dati inconsistenti).

###### Caso generale lettori/scrittori

Per questi sono necessari 2 semafori `sr = 0` (semaforo che indica quanti lettori stanno leggendo), `sw = 0` (semaforo che indica se uno scrittore sta scrivendo) e una `mutex = 1` per l'accesso a 4 variabili condivise: `runR` (lettori attivi), `runW` (scrittori attivi), `totR` (lettori totali), `totW` (scrittori totali).

I valori di variabili e semafori devono rispettare le seguenti regole:

![](https://i.imgur.com/hXoAh0t.png)

Esempio:

```c
// Reader
while (true) { 
	// Guardia: a lettore creato check se può già leggere
	wait(mutex); 
	totR++;          // Non gestita fuori perché l'aggiornamento serve ai writer
	if (runW == 0) { 
		runR++; 
		signal(sr);  // Aumenta sr così che questo processo possa già leggere
	} 
	signal(mutex);
	
	// Lettura
	wait(sr); 
	{Read} 
	
	// Guardia: update + check writer
	wait(mutex); 
	runR--; 
	totR--; 
	if (runR == 0 && runW < totW /* o [&& totW > 0] */) {  // Check nessun reader attivo
		runW = 1; 
		signal(sw);  // Aggiunge 1 posto per writer
	} 
	signal(mutex);
}
// Writer
while (true) { 
	// Guardia: a scrittore creato check se può già scrivere
	wait(mutex); 
	totW++; 
	if (runW == 0 && runR == 0) { 
		runW = 1;    // o runW++ 
		signal(sw);  // Aumenta sw così che questo processo possa scrivere 
	} 
	signal(mutex);
	
	// Scrittura
	wait(sw); 
	{Write}
	
	// Guardia: update + run readers + check reader
	wait(mutex); 
	runW--;       // o runW = 0 
	totW--; 
	while (runR < totR) {  // Fa leggere tutti i reader in attesa
		runR++; 
		signal(sr); 
	} 
	if (runR == 0 && runW < totW /* o [&& totW > 0] */) {  // Check nessun reader attivo
		runW = 1; 
		signal(sw);  // Aggiunge 1 posto per writer
	} 
	signal(mutex);
}
```

##### Filosofi a cena

Questo tipo di problemi prevede $n$ 

n filosofi che condividono 2 posate (forks) 1 con quello a sinistra a l'altra con quello a destra, filosofo o pensa (fa nulla) oppure mangia, ma gli è concesso solo con entrambe le bacchette (quindi per ogni filosofo che mangia i 2 suoi adiacenti non mangeranno).

3 stati (THINKING, HUNGRY, EATING), 1 mutex per accesso all'array di stati e un array di n semafori (tanti quanti filosofi) tutti init a 0.

IMPLEMENTAZIONE DI THINK E EAT NON E' RILEVANTE PER I PROBLEMI (negli esami).

###### Codice

```c
// Philosopher
void philosopher(int i) { 
	while (true) { 
		think(); 
		take_forks(i); 
		eat(); 
		put_forks(i); 
	}
}
// Forks
void take_forks(int i) { 
	wait(mutex); 
	state[i] = HUNGRY; 
	test(i); 
	signal(mutex); 
	wait(sem[i]); 
}
void put_forks(int i) { 
	wait(mutex); 
	state[i] = THINKING; 
	test(LEFT); 
	test(RIGHT); 
	signal(mutex); 
}
void test(int i) { 
	if (state[i] == HUNGRY && state[LEFT] != EATING && state[RIGHT] != EATING) { 
		state[i] = EATING; 
		signal(sem[i]);
	}
}
```

---

Prossima lezione: [[8 - Memoria]]

