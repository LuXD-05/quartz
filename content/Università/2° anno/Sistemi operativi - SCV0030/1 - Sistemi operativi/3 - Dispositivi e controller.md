# Lezione 3

### Dispositivi I/O

I dispositivi I/O si distinguono tra:

- **Dispositivi** veri e propri (gestiti dai *controller*),
- ***Controller*** (o *adapter*): componenti elettroniche che comunicano con la CPU (tramite bus di sistema) e gestiscono (contemporaneamente) più dispositivi simili coi quali si interfacciano attraverso .

###### Interfacce

Mentre le interfacce tra controller e dispositivi sono standard (tipo SATA, USB...), quella tra <u>controller e CPU</u>

![](https://i.imgur.com/TEVM5nR.png)

È composta da:

- **Registri di controllo** (nel controller): detti anche **porte I/O** che permettono invio di comandi, risultati (dei comandi) e stato dei dispositivi tra CPU e controller,
- **Buffer**: un buffer usato per memorizzare i dati durante le operazioni di I/O.

> [!info] Driver
> Tale interfaccia è usata dai ***driver***: programmi dell'OS che gestiscono i dispositivi.

##### Comunicazione tra CPU e porte I/O

Esistono 2 soluzioni per la comunicazione tra la CPU e le porte di I/O:

###### Istruzioni macchina ad hoc

Ad esempio:

![](https://i.imgur.com/c8bmci8.png)

Quindi:

- <u>Tali istruzioni devono essere privilegiate</u> dato che le interazioni coi dispositivi vanno gestite solamente dall'OS,
- Le <u>parti dei driver che le usano vanno scritte in assembly</u> in quanto i linguaggi ad alto livello non hanno istruzioni corrispondenti.

###### Memory mapped I/O

Qui invece si <u>assegna ad ogni porta I/O</u> un **indirizzo di memoria**, quindi:

- Tali <u>indirizzi non sono visibili dai programmi</u>, cosicché l'accesso ai dispositivi sia permesso solo mediante l'OS,
- I <u>driver possono essere scritti in linguaggio ad alto livello</u> (tipo C),
- Si <u>complica la gestione della cache</u> dato che anche i dispositivi (oltre alla CPU) possono modificare il contenuto di queste locazioni di memoria.

##### Esecuzione dell'I/O

Per eseguire operazioni di I/O (tipo passare dei dati dal PC al buffer del dispositivo) ci sono 3 possibili soluzioni:

###### Programmed I/O

Su richiesta di un programma, i *driver* dell'OS eseguono:

```c
for (int i = 0; i < data_length; i++) {
	while (device_status_reg != READY) {} // busy waiting
	buffer = data_bytes[i];
}
```

Quindi finché la porta I/O non è pronta (`device_status_reg != ready`) l'OS aspetta in ***busy waiting***; mentre quando il dispositivo è pronto, si trasferisce un singolo byte nel buffer, poi il ciclo si ripete finché non sono stati trasferiti tutti i bytes.

Così, mentre il dispositivo <u>non è pronto</u>, la CPU è usata solo per <u>controllarne lo stato</u>, tuttavia sarebbe <u>più opportuno che continuasse ad eseguire altri programmi</u>.

###### Interrupt driven I/O

Il *driver* dell'OS esegue:

```c
while (device_status_reg != READY) {} // busy waiting (ma solo all'inizio)
buffer = data_bytes[0];
i = 1;
scheduler(); // sospende questo processo x dare la CPU ad un altro
```

Qui la CPU sta in *busy waiting* solo finché (e se) il dispositivo non è pronto all'inizio, poi quando è disponibile manda 1 byte, aggiorna il contatore a 1 e chiama lo *scheduler* (questo per sottrarre la CPU al programma che voleva trasferire dati al dispositivo che deve aspettare il trasferimento così che può essere assegnata ad altri).

Quando è finito il trasferimento di un byte al buffer, il ***controller*** genera un interrupt per chiamare un ***handler*** che esegue il seguente codice (legato al precedente):

```c
if (i < data_length) {
	buffer = data_bytes[i];
	i++;
} else {
	unblock_user(); // riassegna la CPU al programma che voleva trasferire i byte
}
return_from_interrupt();
```

Quindi se mancano ancora dati da inviare, viene inviato il prossimo byte (con conseguente ennesimo interrupt quando finirà il suo trasferimento), altrimenti il trasferimento è finito e la CPU è riassegnata al programma che ha richiesto il trasferimento di dati al dispositivo.

Questa soluzione evita il *busy waiting* perenne della CPU per ogni singolo byte, tuttavia ci saranno tanti interrupt quanto grande è `data_length`, causando **overhead**.

###### DMA

Con questa l'architettura prevede un controller chiamato **DMA** (*Direct Memory Access*) che può <u>accedere alla memoria</u> e lavorare in <u>parallelo con la CPU</u>:

![](https://i.imgur.com/aTChF7Y.png)

Quindi il *driver* (in seguito alla richiesta da parte del programma) esegue:

```c
setup_DMA_controller();
scheduler();
```

Ovvero richiede al DMA di fare un trasferimento, specificandogli n° di byte e indirizzo di partenza; per poi invocare lo scheduler ed assegnare la CPU ad un altro programma. 

A quel punto il DMA effettua il trasferimento in parallelo alla CPU ed interagendo col controller del dispositivo al suo posto, impostandone i registri di controllo per inviare i byte e ricevendo gli $n$ interrupt di fine trasferimento. Alla fine il DMA invia un interrupt alla CPU cosicché l'*handler* esegua:

```c
unblock_user();
return_from_interrupt();
```

Riassegnando la CPU al programma che ha richiesto il trasferimento.

Grazie al DMA si ha una notevole riduzione dell'*overhead* per la CPU (dato che riceve 1 solo interrupt invece di $n$); e questa è la soluzione usata nei sistemi attuali.

---

Prossima lezione: [[4 - Processi]]

