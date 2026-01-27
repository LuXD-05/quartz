# Lezione 6

### Thread

<u>Problema</u>: i programmi possono dover gestire più ***task*** contemporanei e ciò è implementabile se vengono forniti i costrutti per la <u>programmazione concorrente</u>, coi quali si modellano flussi sequenziali di operazioni in <u>processi</u>; tuttavia, seppur semplice, questa soluzione è <u>poco efficiente</u> a causa dell'<u>overhead</u> dato dai numerosi *context switch* e del fatto che tali processi devono <u>condividere memoria</u> (da implementare con scambio di messaggi).

La soluzione sono i ***thread***: esecuzioni di un programma o sottoprogramma (inteso anche come una <u>procedura</u>) che usa le risorse di un processo. Per ogni processo è possibile che vi siano associati più *thread* che ne usano le risorse.

###### TCB

Le <u>risorse logiche, fisiche e le aree di testo e dati</u> sono **condivise** tra i *thread* di un processo, mentre ognuno di essi contiene nel proprio **TCB** (*Thread Control Block*):

- **TID** (*Thread Identifier*),
- **Stato della CPU**,
- **Stack**,
- **Stato** (proprio: *ready*, *running*, *waiting*...).

> [!info] Nota
> Come per i **PCB**, i *thread* sono organizzati in una ***thread table***.

###### Esempio thread

Un esempio di tale implementazione fa uso dello standard POSIX:

```c
int x;    // variabile condivisa
void *func(void *num) { 
	printf("Thread %ld creato\n", (long)num); 
	x++;
	printf("x = %d\n", x);
	pthread_exit(NULL);                                 // Termina il thread corrente
} 
int main(void) { 
	x = 0;
	pthread_t th[3];                                    // Array di 3 thread
	for (long t = 0; t < 3; t++) {
	    printf("Creo thread %ld\n", t);
		pthread_create(&th[t], NULL, func, (void *)t);  // Crea un thread associandolo ad una funzione
	}
}
/* POSSIBILE ESECUZIONE:
Creo thread 0
Creo thread 1
Thread 0 creato
x = 1
Creo thread 2
Thread 2 creato
x = 2
Thread 1 creato
x = 3
*/
```

Qui abbiamo:

- `pthread_t`: un tipo che rappresenta un thread,
- `pthread_create`: è una funzione che permette di creare un thread (ritorna 0 in caso di successo o un codice di errore altrimenti), i cui parametri sono: 1) indirizzo di memoria in cui salvare il TID, 2) attributi del thread (`NULL` per default), 3) la funzione eseguita dal thread (di tipo `void*`) e 4) il parametro (sempre di tipo `void*`) da passare.
- `pthread_exit`: termina il thread corrente.

> [!warning] Attenzione 
> Ci sono 2 cose da notare nell'esempio fatto:
> 1) La creazione e schedulazione dei thread è **imprevedibile** (come si vede dalla possibile esecuzione),
> 2) Il programma è soggetto a ***race condition*** in quanto, in base a come si alterna l'esecuzione dei thread, alcuni incrementi di `x` potrebbero essere persi.

##### Thread switching

Il ***thread switching*** si basa sullo stesso principio del *context switching* ma ha effetti diversi ed introduce <u>meno overhead</u> in quanto:

- Non serve aggiornare i dati della MMU relativi alle aree di testo e dati,
- Per la condivisione di testo e dati, la cache della RAM può richiedere meno aggiornamenti,
- Per la condivisione dei file, la cache del disco può richiedere meno aggiornamenti.

> [!info] Efficienza
> Anche la gestione di un thread è più efficiente rispetto a quella di un processo, in quanto:
> - Serve creare meno dati (il TCB ha meno dati del PCB),
> - Non serve allocare memoria per testo e dati (alla creazione),
> - I dati sono sono condivisi, perciò è semplice scambiarsi informazioni (non servono *system call* per scambiarsi messaggi come tra processi, quindi meno *overhead*)

##### Implementazioni

Le funzioni `pthread_create` e `pthread_exit` sembrano *wrapper* di *system call*, ma non è detto che lo siano, infatti ci sono 2 modi di implementare i thread:

###### Implementazione in kernel area

Implementandoli nella *kernel area* (funzioni sono *wrapper*), i *thread* sono gestiti dall'OS:

![](https://i.imgur.com/Ph5xLv1.png)

Inoltre:

- La *thread table* con i TCB è una struttura dati nella *kernel area*,
- Lo *scheduler* deve schedulare i singoli *thread* invece degli interi processi,
- I *thread* sono gestiti tramite *system call* (chiamabili o direttamente in assembly o tramite wrapper come in C).

###### Implementazione in user area

Implementandoli nella *user area* (funzioni non sono *wrapper*), l'OS non sa nulla dei *thread* e gestisce solo processi:

![](https://i.imgur.com/K5nyTpX.png)

Inoltre:

- I *thread* sono gestiti da una libreria di procedure (**sistema runtime**) che eseguono in *user mode*,
- Lo *scheduler* dei *thread* è un procedura della libreria e la *thread table* è situata nell'area di RAM assegnata al processo (quindi nella *user area*),
- Il programmatore gestisce i *thread* con le procedure della libreria (creazione, terminazione... persino schedulazione con `pthread_yield`).

> [!info] Vantaggi e svantaggi
> **Vantaggi**: 1) funzionano su OS che non implementano *thread*, 2) il *thread switching* è più veloce e non richiede l'intervento dell'OS e 3) scheduling personalizzabile.
> **Svantaggi**: 1) con CPU multi-thread/core il parallelismo è possibile solo coi *kernel thread* e 2) se un *thread* fa una *system call* blocca il suo intero processo.
> Perciò di solito si usano soluzioni miste.

---

Prossima lezione: [[7 - Sincronizzazione]]

