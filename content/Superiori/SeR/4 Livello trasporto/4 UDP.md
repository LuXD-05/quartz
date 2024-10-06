---
public: true
modified_at: 16/06/2024 21:56:30
edited_seconds: 260
---
### Caratteristiche e ambiti applicativi
Hint: caratteristiche (4) e ambiti applicativi (3)
::
UDP è:
- ***Connectionless***
- ***Unreliable***
- **Non *full-duplex***
- Sia ***unicast*** che ***multicast***
UDP è usato in:
- App che **tollerano perdite** ma non **ritardi** e che richiedono l’**elaborazione senza buffer** (***real-time***).
- App che **inviano pacchetti piccoli** (quindi non richiedono segmentazione) o **notifiche** (tipo DHCP e DNS).
- App che **spediscono pacchetti a + destinatari** (IP **multicast**), tipo Skype, UPnP, auto-config e attività di *discovery*.
<!--SR:!2024-04-30,2,200-->

### Descrizione
Hint: cosa fa, unreliable, stateless, altro
::
Definito nella **RFC 768**, **UDP** (*User Datagram Protocol*) fornisce un servizio simile a IP ma al livello applicativo.
##### Come lavora
Essendo un protocollo di livello trasporto esegue le attività di ***multiplexing*** (in **uscita**) e ***demultiplexing*** (in **entrata**), per mezzo dei **n° di porta**. Con **UDP non c’è bufferizzazione** (al contrario di TCP), quindi permette un controllo più preciso a livello applicativo su quanti dati inviati e su quando sono stati inviati ed elaborati.
**UDP**, impacchetta i dati e li trasferisce al livello inter-rete **appena li riceve** dal livello applicativo (con controllo di flusso e congestione del TCP, una app non può sapere se dati inviati o ancora nel buffer); e inoltre **non fa *handshake*** e quindi **non introduce ritardi**.
##### Unreliable
UDP è **inaffidabile**, quindi **non esegue controlli in ricezione** (oltre al ***checksum***), quindi riassembla i pacchetti nell’**ordine di arrivo**, non di partenza, senza controllare se vi siano **perdite** o **duplicazioni**. Se l’app ritiene importante l’ordine dei segmenti, dovrà gestirne la corretta sequenza, stabilendo come processare i dati. Una **app UDP** può essere resa **affidabile** inserendo nell’app stessa dei meccanismi di **notifica** e **ritrasmissione**.
##### Stateless
**UDP** è **stateless**, **non memorizza informazioni sulle sessioni di comunicazione** (1 server UDP può gestire molti + client UDP).
##### Altro
L’***header*** dell’**UDP** è di **8 byte** al contrario dei 20 del TCP.
Anche se presenta vantaggi in **velocità**, mandare pacchetti alla loro frequenza di produzione nella rete **senza controllo di congestione** implica **sovraccarichi** della rete e il **rischio** che tanti pacchetti vengano **persi**.
<!--SR:!2024-04-30,2,200-->

### Datagram UDP
Hint: SLC
::
Il pacchetto UDP è detto **datagram**, per sottolineare il servizio ***best-effort*** dato. Il suo **overhead** è di **8 byte**. I campi:
- **Source port** e **Destination port** (16 + 16 bit): usati per identificare l’app e per multiplexing e demultiplexing,
- **Length** (16 bit): **Lunghezza** dell’intero **datagram** (*header* + dati),
- **Checksum** (16 bit): **Campo** di **controllo** dell’**errore** (check di header + payload).
<!--SR:!2024-04-30,2,200-->