---
public: true
edited_seconds: 110
modified_at: 14/06/2024 17:46:13
---
### Il livello applicativo
::
Il livello applicativo riguarda le applicazioni di rete, progettate con architetture client/server o P2P. I processi applicativi inviano messaggi in rete e li ricevono da essa attraverso un socket, un’interfaccia software tra il livello applicativo e il livello trasporto all’interno di un host (mezzo usato da app per richiedere l’uso di 1 protocollo liv. trasporto).
<!--SR:!2024-04-30,2,200-->

### Sevizi
::
Alle app sono offerti dei servizi a livello trasporto, con **TCP** (affidabile) e **UDP** (inaffidabile). Questi però non garantiscono:
- **Throughput alto**: frequenza con cui un processo invia bit al ricevente (app sensibili a throughput = sensibili alla banda).
- **Temporizzazione**: molte app tollerano ritardi end-to-end solo nell’ordine di decimi di secondo.
- **Sicurezza**: potrebbe essere necessario rendere i dati riservati con crittografia end-to-end.
<!--SR:!2024-04-30,2,200-->

### Web
::
Una app web è una **app** che permette la **navigazione tra pagine web**. È composta da:
- **Web server**: o **HTTPd** (*HTTP Daemon*), è il programma **HTTP server** (tipo Apache o IIS),
- **Web browser**: (tipo Chrome, Safari, Opera, Firefox…),
- **HTTP**: (*HyperText Transfer Protocol*), è il programma **HTTP client**.
<!--SR:!2024-04-30,2,200-->