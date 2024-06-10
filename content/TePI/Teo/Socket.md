# Socket

Perché?

Per lo scambio di messaggi tra processi su host diversi, serve un modo per i processi di identificare il destinatario, quindi le applicazioni in rete vanno riconosciute in qualche modo; ciò grazie al port address.

Port address

**N° che identifica** le **porte logiche** (su 2 byte, da 0 a 65535) e **individua** un **canale** da usare **per la comunicazione**.

I **n° di porta logica** sono **univocamente assegnati al relativo protocollo** (porta TCP != porta UDP, anche se a volte usata una unica per entrambi). La sola **porta non rende** una **connessione univoca**, perché processi di host diversi potrebbero ascoltare tutti sulla stessa. Per questo **la porta viene combinata con l’indirizzo IP** (socket).

**Socket**

È scritto così: “**[IP]:[port]**”. La coppia è:

**IP**: che identifica l’host avente il processo destinatario con cui comunicare.

**Port**: identifica la porta usata dal processo dell’host destinatario.

Permette di comunicare in rete con la pila TCP/IP (mess esce da socket mittente e arriva a socket dest).

In un server TCP abbiamo 2 tipi di socket:

- 1 per accettare le connessioni (condiviso) che si chiama *connection socket*,
- 1 per funzioni send() e receive() (non condiviso) detto *data socket*.

Socket & client/server

In rete ci sono client e server. Il **server** (o meglio **processi server** che girano **su un host che erogano servizi ad altri processi** in rete) ha più controllo perché lui **crea i socket**. Più client possono comunicare sullo stesso socket.

Un processo **client deve conoscere il socket del server** (con eventuale richiesta), mentre il **server deve acquisire le info sull’host client**, come il suo **n° di porta** per inviare le risposte. Passaggi:

1) **Inizializzazione** dei **processi** (si **crea un socket**),
2) **Client effettua** la **richiesta di collegamento** (nel socket ci sono delle **code** con le **richieste** in logica **FIFO**),
3) Il server accetta la richiesta e stabilisce il collegamento (**se esaurisco la coda**, il **server rischia di crashare** per troppe richieste, quindi **controlla** il **socket** e **vede quante ne arrivano e da quali IP**. Se ne arrivano troppe da un IP magari può essere un DDoS e prendere contromisure).

Il server quando accetta la richiesta realizza un canale virtuale tra il client e un suo nuovo socket, al fine di lasciare libero il primo per ulteriori richieste?????

Processi si scambiano dati con funzioni **read()** e **write()** fino a **chiusura** del **canale** o a chiamata della primitiva **close()**.

Famiglie di socket

Ci sono 2 famiglie di socket (o domini):

- Unix Domain Socket (AF_UNIX): pathname valido nel file system della macchina, permette trasferimento dati tra processi sulla stessa macchina UNIX;
- Internet socket (AF_INET): usato nelle applicazioni per il trasferimento dati tra processi su macchine remote connesse tramite una LAN o internet; specificato da 2 valori:
- **Indirizzo IP** (32 bit), che individua un unico host Internet,
- **N° di porta** (16 bit), che specifica una porta dell’host.

Tipi di socket

Ci sono 3 tipi di socket:

- Stream Socket: **Protocollo TCP/IP** (affidabile con connessione, quindi connessioni punto-punto unicast),
- Datagram Socket: **Protocollo UDP** (non affidabile, usato anche per multicast),
- Raw Socket: Usati per realizzare protocolli.
