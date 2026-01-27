# Esami

### Esercizi

##### 1

```c
/* Considerazioni
- Valori array eliminati = 0 (init a 0)
*/

// Var condivise
int[] arr = new int[10];
int i = 0;             // index producer
int j = 0;             // index consumer
sempahore full = 0;    // n° celle piene
semaphore empty = 10;  // n° celle vuote
semaphore sp = 1;      // mutex su i
semaphore sc = 1;      // mutex su j
semaphore tc = 1;      // sem sui 3 (max = 1)
semaphore fc = 2;      // sem sui 5 (max = 2)

// Produttore
while (true) {
	int item = produce();
	if (item == 3) { wait(tc); }
	if (item == 5) { wait(fc); }
	wait(empty);
	wait(sp);
	arr[i] = item;
	i = (i+1) % 10;
	signal(sp);
	signal(full);
}

// Consumatore
int item;
while (true) {
	wait(full);
	wait(sc);
	item = arr[j];
	j = (j+1) % 10;
	signal(sc);
	if (item == 3) { signal(tc); }
	if (item == 5) { signal(fc); }
	signal(empty);
}
```

##### 2

```c
// Variabili condivise
int arr[100];
int i2 = 0;            // index prod % 2 == 0
int i3 = 3;            // index prod % 3 dispari
int iD = 1;            // index prod % 3 != 0
int ic = 0;            // index consumer
semaphore full = 0;    // Sem per n° pos piene
semaphore s2 = 50;     // Sem su pos % 2 == 0
semaphore s3 = 17;     // Sem su pos % 3 dispari
semaphore sD = 33;     // Sem su pos % 3 != 0
semaphore m2 = 1;      // mutex su i2
semaphore m3 = 1;      // mutex su i3
semaphore mD = 1;      // mutex su iD

// Producer
while (true) {
	int item = produce();
	if (item % 2 == 0) {
		wait(s2);
		wait(m2);
		arr[i2] = item;
		i2 = (i2 + 2) % 100;
		signal(m2);
	} else if (item % 3 == 0) {
		wait(s3);
		wait(m3);
		arr[i3] = item;
		i3 == 99 ? i3 = 3 : i3 += 6;
		signal(m3);
	} else {
		wait(sD);
		wait(mD);
		arr[iD] = item;
		while (iD%2==0 && iD%3==0) { iD++; }
		signal(mD);
	}
	signal(full);
}

// Consumer
while (true) {
	wait(full);
	wait(m2);
	wait(m3);
	wait(mD);
	while (arr[ic] < 0) { ic++; }
	int item = arr[ic];
	arr[ic] = -1;
	ic = (ic + 1) % 100;
	if (item % 2) { signal(s2); }
	else if (item % 3) { signal(s3); }
	else { signal(sD); }
	signal(m2);
	signal(m3);
	signal(mD);
}
```

##### 3

```c
// Variabili condivise
int arr[100];

// Producer
while (true) {
	
}

// Consumer
while (true) {
	
}

// ConsPari
while (true) {
	
}
```

##### 4

```c

```

##### Da pdf es uso semafori

###### Sleeping barber

###### Ponte

###### Parcheggio

"Parcheggio / 30 posti" = non necessario array ma solo contatore

"Entra/prenota" = azioni da fare (non implicite con wait e signal), quindi servono contatori di prenotazioni A e B

"Alternativamente" = variabile di turno condivisa

```c
// Variabili condivise
int free = 30, bookA = 0, bookB = 0, turn = 0;
semaphore A = 0;
semaphore B = 0;
semaphore mutex = 1;

// Gate A
while (true) {
	wait(mutex)
	if (free > 0) {
		free--;
		signal(mutex);
	} else {
		bookA++;
		signal(mutex);
		wait(A);
	}
}
// Gate B
while (true) {
	wait(mutex)
	if (free > 0) {
		free--;
		signal(mutex);
	} else {
		bookB++;
		signal(mutex);
		wait(B);
	}
}

// Uscita
while (true) {
	wait(mutex);
	if (free == 0) {
		if ((turn == 0 | bookB == 0) & bookA > 0) {
			bookA--;
			turn = 1;
			signal(A);
		} else if ((turn == 1 | bookA == 0) & bookB > 0) {
			bookB--;
			turn = 0;
			signal(B);
		} else {
			free++;
		}
	} else {
		free++;
	}
	signal(mutex);
}
```

Senza dire scheduler con logica FIFO non, seppur si fa `free++` dopo la `signal` non si sa quale dei processi arriva prima (si rischia di)

### Esami

##### 2023/02/09

###### RC

`int[] A = [30, 10, 20];` con 2 thread che:

`t1 { A[0] = A[0] + A[1]; }`

`t2 { A[0] = A[0] * A[2]; }

$W_{1} = \{ A_{0} \} \;\;\;|\;\;\; R_{1} = \{ A_{0}, A_{1} \}$

$W_{2} = \{ A_{0} \} \;\;\;|\;\;\; R_{2} = \{ A_{0}, A_{2} \}$

Sono interagenti in quanto $W_{1} \cap R_{2} = W_{2} \cap R_{1} = \{ A_{0} \}$, quindi c'è il rischio di race condition.

I risultati da aspettarsi quindi non sono solo: `f1(f2(30)) = f1(600) = 610` e `f2(f1(30)) = f2(40) = 800`; ma potrebbero anche essere:

- `40`: in caso entrambi leggano subito `A[0]` ma l'ultimo a scriverci è `t1`,
- `600`: in caso entrambi leggano subito `A[0]` ma l'ultimo a scriverci è `t2`.

###### Semafori

Tipo la merda sto esercizio

```c
// Variabili condivise
int A[100], wrk12, wrk3, wait1, wait2, wait3;
semaphore s1 = 0;
semaphore s2 = 0;
semaphore s3 = 0;
semaphore mutex = 1;

// T1 (e T2 cambia poco)
while (true) {
	wait(mutex);
	if (wrk12 > 0 || wrk3 > 0) {
		wait1++;
		signal(mutex);
		wait(s1);
	} else {
		wrk12++;
		signal(mutex);
	}
	
	int k = random();
	for(int i = 0; i < A.length; i++) { A[i] += k + i; }
	
	wait(mutex);
	wrk12--;
	if (wait2 > 0) {
		wait2--;
		wrk12++;
		signal(s2);
	} else {
		while (wait3 > 0) {
			wait3--;
			wrk3++;
			signal(s3);
		}
		if (wrk3 == 0 & wait1 > 0) {
			wait1--;
			wrk12++;
			signal(s1);
		}
	}
	signal(mutex);
}

// T3
while (true) {
	wait(mutex);
	if (wrk12 > 0 || wrk3 > 0) {
		wait1++;
		signal(mutex);
		wait(s1);
	} else {
		wrk12++;
		signal(mutex);
	}
	
	signal(mutex);
}
```

##### 2024/01/08

```c
// Variabili condivise
int A[?], B[?], ia = 0, ib = 0;
semaphore sa = 0;
semaphore sb = 0;
semaphore sc = 0;
semaphore mutex = 1;
// workA/B/C, waitA/B/C | cons consuma fino ad ia/ib
// workC è 1 per volta --> poi sveglia quanti ap e bp che può

// A-prod
while (true) {
	
}

// B-prod
while (true) {
	
}

// Consumer
while (true) {
	
}
```

##### 2024/01/24

```c
// Variabili condivise
int tokens = 100, w1 = 0, w2 = 0, w3 = 0;
semaphore s1 = 0;
semaphore s2 = 0;
semaphore s3 = 0;
semaphore mutex = 1;

// T1 (+ T2 e T3, cambiano solo n° di token e lista w)
while (true) {
	wait(mutex);
	if (tokens > 0) {
		tokens -= 1;
		signal(mutex);
	} else {
		w1++;
		signal(mutex);
		wait(s1);
	}
	// gym
	wait(mutex);
	tokens += 1;
	if (tokens >= 3 && w3 > 0) { 
		w3--; 
		tokens -= 3; 
		signal(s3);
	} else if (tokens >= 2 && w2 > 0) { 
		w2--; 
		tokens -= 2;
		signal(s2);
	} else if (tokens >= 1 && w1 > 0) { 
		w1--;
		tokens -= 1;
		signal(s1);
	}
	signal(mutex);
}
```

