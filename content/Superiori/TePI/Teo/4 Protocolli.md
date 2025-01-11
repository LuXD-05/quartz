# Protocolli

> [!important] Protocollo
> **Insiemi di regole e convenzioni usate nel dialogo tra livelli.**

### TCP

Il TCP è un protocollo livello **trasporto** che fornisce supporto a altri protocolli liv applicativo (HTTP, FTP, SMTP, SSH…).

È importante perché **permette** di **operare contemporaneamente con applicativi distinti**. (Tipo utenti in internet possono usare + app internet, non solo TCP ma anche UDP)

Ciò avviene grazie alle **porte**, numeri interi di 16 bit (0-65535). (nelle trasmissioni viene dopo l'IP destinatario separato da ":", tipo: 192.168.0.1:80)

È **orientato alla connessione** (stabilire connessione prima di trasferimento) al contrario di **UDP**.

### Porte

**Identificano univocamente l'applicazione a cui instradare i pacchetti**, soprattutto in caso ci siano tante applicazioni che vanno riconosciute in rete. Divise in:

###### Well-Known (0 – 1023)

Riservate per servizi e app standard dei server, e settate di default sui client per essi. (client non dovrebbero usarle)

###### Registrate (1024 – 49151)

Usate per servizi privati, il client le usa per farci quello che vuole

###### Dinamiche (49152 – 65535)

Libere per essere assegnate dinamicamente da processi applicativi, usate per servizi passivi, tipo P2P.

##### Porte di default

TCP 80

Abbiamo 2 pc, 1 client e 1 server. Il server attende sempre per 1° una richiesta dal client, ma questo deve sapere il suo IP e la porta del servizio che deve usare. Il server non può usare una porta casuale per quel servizio, se no il client come lo raggiunge? Per questo si è definita la porta TCP 80 come predefinita per accedere a un qualsiasi server HTTP.

- TCP 25: Server SMTP
- TCP21: Server FTP
- UDP 53: Server DNS
- TCP 443: HTTPs
