# Reti Client/Server e P2P

Tipi di reti

In condivisione c'è sempre 1 pc che mette a disposizione roba e un altro che riceve.

Client/Server

Dei pc (**server**) che **mettono a disposizione delle risorse** o offrono servizi **ad** altri pc (**client**).

Se client non può diventare server e viceversa, il server è detto **server dedicato**.

In altri casi (come in **> parte delle reti locali**) **non vi è** una **distinzione** predefinita **tra client e server**, perché un pc può condividere dati e al contempo usare quelli di un altro pc.

*In reti grandi spesso pc + potente è il server, detto host (distribuisce servizi e risorse a rete) ma pc obsoleti possono fare da server*

P2P

Tutti i **pc** sono **sullo stesso livello** e condividono risorse comuni. Qui tutti i pc sono sia client sia server.

Messaggi

**Insieme di caratteri e dati che devono essere trasferiti da un sistema a un altro**.

*(Quindi un insieme di info organizzate in modo da formare un'entità trasmissibile tra 2 sistemi di rete)*

Pacchetti

Per favorire la trasmissione, i messaggi sono suddivisi in **pacchetti** (perché un mess piccolo è + semplice che trovi una linea che abbia spazio per lui e può lasciare spazio ad altri mess)

I pacchetti hanno anche info riguardanti: il **destinatario** e **l'ordine di ricomposizione** una volta giunti a destinazione.

Reti C/S (Client-Server)

Quando si stabilisce una comunicazione tra client e server, inizia l'erogazione del servizio richiesto, con 2 possibilità:

Esecuzione lato client o locale

**Il programma è trasmesso dal server, caricato in RAM ed eseguito dal client stesso**

1) *Client*: invia richiesta x prog
2) *Server*: elabora e invia il prog
3) *Client*: riceve e usa il prog per avere risultati

Esecuzione lato server o remota

**Il programma è eseguito sul server che trasmette i dati al client**

1) *Client*: invia richiesta per una elaborazione
2) *Server*: elabora richiesta, la esegue, risponde con il dato
3) *Client*: riceve il dato

Vantaggi esecuzione lato server

- **unica installazione**: prog installato solo su server e non su tutti i client
- **aggiornamenti e manutenzione + easy**: siccome è su 1 macchina, e lo stesso livello di update tra tutti i sistemi
- **diminuzione costi**: di licenze
- **> sicurezza di dati**: solo 1 backup da fare

Cloud

**Insieme di risorse, applicazioni e servizi disponibili e distribuiti su tutta la rete**. (vantaggi di prima sono alla base del cloud computing)

Reti P2P (+ usata in reti locali dove ogni pc condivide dati)

Non vi è distinzione tra client e server, bensì i pc di una rete sono detti **nodi** (ovvero, **ogni pc è sia client sia server**)

Un pc è client quando riceve dati e server quando li fornisce.

Esempio comune è il file-sharing tramite internet., fatto con programmi tipo eMule o bitTorrent, dove un pc si connette a un altro per scaricare dei file che lui mette a disposizione.

Vantaggi

- **semplice da gestire** (dato che non necessita amministrazione)

Svantaggi

- **meno sicura nel controllo di accessi e utenti** (dato che non c'è amministrazione)

Differenze

Client/Server

- **L'accesso** alle risorse è **gestito da** un **database di sicurezza** centralizzato
- **Whitelist** del server **con utenti e** rispettive **password**
- Gli **utenti** possono **accedere solo** a **determinate risorse** a cui sono autorizzati
- **Pochi problemi al ridimensionamento**

P2P

- Implementano una **rete overlay astratta** a **livello applicazione** sulla topologia fisica
- Idea di base è **condividere risorse** in **modo economico**
- Solo gli **utenti** finali possono **controllare l'accesso** alle **risorse** (con password in punti di condivisione che creano)
- **< prestazioni al ridimensionamento**
