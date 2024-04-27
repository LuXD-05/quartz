### Il livello applicativo

Il livello applicativo riguarda le applicazioni di rete, progettate con architetture client/server o P2P.

I processi applicativi inviano messaggi in rete e li ricevono da essa attraverso un socket, un’interfaccia software tra il livello applicativo e il livello trasporto all’interno di un host (mezzo usato da app per richiedere l’uso di 1 protocollo liv. trasporto).

### Sevizi necessari

Alle app sono offerti dei servizi a livello trasporto, con **TCP** (affidabile) e **UDP** (inaffidabile). Questi però non garantiscono:

- **Throughput alto**: frequenza con cui un processo invia bit al ricevente (app sensibili a throughput = sensibili alla banda). 
- **Temporizzazione**: molte app tollerano ritardi end-to-end solo nell’ordine di decimi di secondo. 
- **Sicurezza**: potrebbe essere necessario rendere i dati riservati con crittografia end-to-end.

### SSL/TLS

Riservatezza, auth e integrità dei dati sono critiche per molte app, quindi per garantirle si usa un protocollo appena sopra il TCP: l'SSL/TLS (*Secure Socket Layer / Transport Layer Security*). (HTTPS = TCP + SSL/TLS).

### Web

Una app web è una **app** che permette la **navigazione tra pagine web**. È composta da:

- **Web server**: o **HTTPd** (*HTTP Daemon*), è il programma **HTTP server** (tipo Apache o IIS), 
- **Web browser**: (tipo Chrome, Safari, Opera, Firefox…),
- **HTTP**: (*HyperText Transfer Protocol*), è il programma **HTTP client**.
