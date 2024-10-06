---
public: true
modified_at: 28/04/2024 00:30:00
---
### NAT
Hint: NAT, perché, funzioni router NAT, port forwarding
::
Il NAT (*Network Address Translation*) è una tecnica che consente di **mappare + IP privati su un IP pubblico**, permettendo quindi a + host di una rete privata di comunicare con l'esterno.
##### Perché?
- **Risparmio degli indirizzi IP**: gli ISP non devono più dare tanti IP tutti pubblici per gli host di una rete privata.
- **Facilità di amministrazione della rete**:
	- Gli IP privati sono modificabili liberamente senza dover notificare niente a nessuno.
	- Si può cambiare ISP senza dover cambiare la configurazione di IP privati.
- **Sicurezza**: gli host della LAN non sono visibili dall'esterno ma sono indirizzabili (dall'esterno).
#### Funzioni del router NAT
Un router abilitato NAT:
- Sostituisce in ogni datagram uscente la coppia \[IPv4 sorgente (privato) : porta\] con \[IPv4 pubblico : nuova porta (generata da NAT)\],
- Registra nella **NAT Table** la corrispondenza tra le coppie.
Questo permette a NAT di gestire + richieste contemporaneamente da applicazioni **sullo stesso host** (<u>stesso IP ma porte diverse</u>) o su **host diversi** (<u>stessa porta ma IP diverso</u>).
##### Port forwarding
Per connettersi invece **dall'esterno alla LAN**, non è chiaro a quale host connettersi. Si potrebbero usare rotte **statiche** che inoltrano tutti i pacchetti a un host, ma è una soluzione poco pratica.
Per questo si usa il ***port forwarding***, che permette a NAT di inoltrare i pacchetti a diversi host in LAN in base a **protocollo** e **porta** usati. Con le porte quindi, varie applicazioni da vari host possono comunicare distintamente con l'esterno. La coppia \[**IPv4:port**\] è detta **socket**.
<!--SR:!2024-05-01,3,220-->

### NAT Traversal
NAT traversal, P2P e UPnP
::
L’associazione di NAT (\[IPv4 sorgente : porta\] = \[IPv4 pubblico : nuova porta\]) è fatta sui pacchetti **in uscita** dalla LAN (quindi i **pacchetti in entrata** possono essere **accettati solo dopo quelli in uscita, in risposta ad essi**).
Quindi un utente in LAN con un NAT può connettersi a un server remoto, ma un utente remoto non può connettersi al server della LAN. Per ovviare a questo si usa il **NAT Traversal**.
##### UPnP e P2P
La tecnica di NAT Traversal + diffusa è **UPnP** (*Universal Plug & Play*, spesso usata da app P2P). Questa permette automaticamente a un **host LAN** (o a un'**app** su un host) di **richiedere**, **per una** qualsiasi **porta**, una **corrispondenza statica NAT** per un certo ***lease time*** tra l'app LAN e l'host/app remota. Se UPnP accetta, inserisce la corrispondenza nella sua tabella di traduzione e i 2 host possono istanziare connessioni TCP l'uno verso l'altro.
<!--SR:!2024-05-01,3,220-->