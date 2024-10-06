---
public: true
modified_at: 23/06/2024 18:18:59
---
# VPN
### Cosa sono?
Una **VPN** (*Virtual Private Network*) è una **rete privata virtuale** che **usa una rete pubblica** per **collegare** tra loro **pc remoti come se** appartenessero alla **stessa rete locale**. Le VPN sono:
- "**Private**" perché la comunicazione fa apparire le **LAN remote come se comunicassero su una stessa rete privata** (condividendo gli stessi indirizzamenti privati e le policy di sicurezza).
- "**Virtuali**" perché i **collegamenti sono logici (non dedicati/fisici) sopra un'infrastruttura di rete pubblica** (solito internet, ma aziende si appoggiano a reti fornite da un operatore con specifici protocolli).
Le VPN permettono di creare dei "**tunnel virtuali**" in cui i dati viaggiano **cifrati** per garantire **sicurezza** in una rete pubblica come internet.
### Vantaggi
I vantaggi delle VPN sono tanti:
- **Riduzione dei costi**: non serve affittare linee dedicate e costose per comunicare tra sedi in sicurezza,
- **Uso di risorse preesistenti**: si usano i normali collegamenti ad internet già presenti,
- **Flessibilità di accesso alle risorse**: (con permessi), si può accedere a una risorsa aziendale indipendentemente dalla sede,
- **Connessioni sicure**: le trasmissioni sono cifrate,
- **Scalabilità**: è semplice aggiungere sedi alla rete aziendale,
- (Supporto **voce e video cifrati**),
- (**Semplicità**).
### Perché usare una VPN?
Sono 2 i motivi principali per usare una VPN:
- **Necessità di proteggere la privacy con l'anonimato** e di **aggirare *region locks*** che bloccano l'accesso a risorse (questo con ***VPN ad accesso remoto***),
- **Esigenza di collegare sedi lontane** da quella centrale dell'azienda **in modo sicuro** (questo con ***VPN site-to-site***).
##### VPN ad accesso remoto
Le **VPN ad accesso remoto** consentono (garantendo privacy) di **raggiungere risorse in rete altrimenti irraggiungibili**. Prevedono la creazione di un **tunnel VPN** (**crittografato**) tra: 
- Un **client che acquista il servizio VPN da un ISP** e che **installa** un "**VPN client**" **impostandoci** il **server del provider**,
- Un **server VPN del fornitore** a cui sono **mandati i messaggi crittografati** che **decritterà e invierà in internet dal proprio IP, mascherandone l'origine**. 
(Questo è utile per **eludere** le risorse protette da ***region lock*** e pere i dipendenti fuori sede che possono accedere alle risorse aziendali tramite un client VPN aziendale).
##### VPN site-to-site
Le **VPN site-to-site collegano** (garantendo sicurezza) **2 o + LAN dislocate utilizzando internet**. Il tunnel qui è stabilito tra dei **CPE** (*Customer Premises Equipment*, ovvero **router**/gateway) **delle sedi remote** per impedire l'intercettazione dei messaggi trasmessi. Qui i dispositivi **non necessitano di un client VPN**, ma inoltrano i messaggi attraverso i **router VPN**. Le VPN site-to-site sono ulteriormente classificabili in:
- **Intranet**, reti di uffici/sedi di una stessa azienda collegati per mezzo di una VPN,
- **Extranet**, dove la VPN connette l'azienda a un partner o cliente.
### Tipi di VPN
Le VPN possono usare **2 tipi di meccanismi per trasferire dati** (la combinazione di queste 2 origina una *hybrid VPN*):
##### Trusted VPN
Questo prevede di **appoggiarsi a un ISP che crea dei tunnel sui i suoi circuiti privati come se fossero virtuali**. (La soluzione + diffusa si basa sul protocollo **MPLS**, in cui a ogni pacchetto è assegnata una label che rende il traffico efficiente in quanto ordina i pacchetti fornendogli delle priorità).
**Vantaggi**:
- Il cliente non si preoccupa del servizio (fa tutto l'ISP),
- Garantire la sicurezza è a carico dell'ISP,
- La QoS è anch'essa gestita dal fornitore,
- Tempi di *fault recovery* brevi per algoritmi di rete basati su priorità,
- Cliente gestisce l'indirizzamento IP (come se fosse tutto su una LAN privata logica).
**Svantaggi**: costi elevati e rigidità.
##### Secure VPN
Questo prevede di **sfruttare la rete pubblica crittografando i dati che viaggiano**. Sulle funzioni di rete fornite da un ISP, l'utente sovrappone una propria ***overlay network***, una topologia logica in cui definisce lui dei collegamenti punto-punto. (Quindi i dati viaggiano in un tunnel virtuale protetto, ma non ci sono imposizioni su quale percorso devono seguire). La **sicurezza è data da altri protocolli tipo IPsec**.
In questa categoria di VPN rientrano le ***clientless* o *web* VPN**, che usano **SSL** per permettere a utenti dislocati di accedere a risorse in internet da ovunque. Non necessitano aperture di porte... ma solo auth.
### La sicurezza nelle VPN
Le VPN devono garantire:
- **Riservatezza**, fatta **crittografando i dati**. Per questa si usano dei protocolli tra cui **IPsec, L2TP e SSL**.
- **Integrità**, (**non permettere alterazioni** di dati nel transito). Esempio: IPsec impedisce modifiche ed elimina i pacchetti compromessi.
Serve poi anche **accertarsi dell'identità del mittente** per proteggersi da *spoofing*; infatti quando un utente remoto richiede la creazione di un tunnel, un server AAA verifica certe cose:
- **Autenticazione** ("chi sei"): si verifica l'identità di un utente (tipo con username e password),
- **Autorizzazione** ("cosa puoi fare"): si verifica a quali risorse l'utente può accedere e gli si da l'accesso solo a quelle,
- **Accounting** ("cosa hai fatto"): traccia l'uso delle risorse dell'utente per fini di sicurezza, statistici e di tariffazione.
In sostanza è la crittografia che garantisce la sicurezza in generale e questa, se applicata a protocolli del modello TCP/IP rende anche quelli superiori sicuri.
#### VPN IPsec
(***Internet Protocol Security***), implementa la **crittografia a livello rete** (quindi fornendo sicurezza al protocollo IP) e permette di creare un **percorso sicuro tra 2 host comunicanti** per mezzo di una **VPN** in una rete non sicura.
##### Protocolli di sicurezza IPsec
IPsec garantisce la sicurezza (riservatezza e auth) con 2 protocolli.
- **AH** (***Authentication Header***), garantisce **auth del mittente e integrità** (ovvero che la sua **identità non sia stata cambiata** da un attacco di *spoofing*), <u>senza</u> però garantire **riservatezza/crittografia**.
- **ESP** (***Encapsulation Security Protocol***), opera sul **messaggio** (**non sul mittente come AH**) e del suo **payload** (**no header**) garantisce **autenticità**, **integrità** e **riservatezza**/**crittografia**.
##### Modalità di incapsulamento IPsec
<u>Entrambi</u> i protocolli (AH e ESP) possono essere implementati nelle **2 modalità di incapsulamento** previste da **IPsec**:
###### Transport mode
Questa è usata per **collegamenti sicuri tra 2 host** (*end-to-end*) **aventi IP pubblico**. **Non crea** alcun **tunnel**. Se usata **con AH, garantisce autenticità e integrità di tutto il messaggio**, se no con **ESP garantisce in + la riservatezza ma solo del payload**. Funzionamento: **tra l'header IPv4 e l'header TCP è aggiunto un *IPsec header*** (questi collegati da *next header*) che può essere o **AH o ESP**.
(foto?)
###### Tunnel mode
Questa è usata per i collegamenti **VPN tra reti private che accedono a router pubblici** (*gateway-to-gateway*). Viene creato un **tunnel** per il transito sicuro dei pacchetti IP, che vengono completamente **cifrati** e **incapsulati** in un altro pacchetto, **nel cui header sono contenuti gli IP mittente e destinatario dei 2 router che sono gli estremi del tunnel**. (Con ESP si impedisce di conoscere la sorgente del pacchetto, ottimo grado di riservatezza).
(foto?)
##### Funzioni e protocolli di supporto alla sicurezza
- **SA** (*Security Association*): proprietà che definiscono come realizzare una comunicazione sicura tra 2 host. SA descrive: tipo connessione sicura da instaurare + meccanismi, algoritmi di cifratura e la *kpr* (+ transport o tunnel e AH o ESP).
- **SAD** (*SA Database*): Database delle SA attive di un sistema.
- **SP** (*Security Policy*): regole che informano IPsec di quali flussi di dati devono essere usati da una SA (IP source e dest, porte, AH/ESP, transport/tunnel).
- **SPD** (*SP Database*): db con politiche per gestione pacchetti. Sono: 1) "scarta", scarta pacchetto entrata/uscita, 2) "non applicare", non applica sicurezza in entrata/uscita e 3) "applica", applica sicurezza in entrata/uscita.
- **IKE** (*Internet Key Exchange*): (porta 500 UDP) permette la configurazione automatica delle SA generando dinamicamente chiavi di sessione diverse per ogni blocco dati inviato (se hacker ottiene dato e chiave non fa niente perché il resto dei pacchetti è crittato con chiavi diverse). Scambio di keys IPsec avviene con l'algoritmo DH (Diffie-Hellman, dove le parti si scambiano info su generazione della chiave che poi è protetta con hash).
#### (VPN) SSL
**TLS** (*Transport Layer Security*) / **SSL** (*Secure Socket Layer*) è un protocollo che si colloca tra i livelli **trasporto** e **applicazione**, garantendo una comunicazione sicura (riservatezza e integrità) ai protocolli livello trasporto e applicazione relativi. La sicurezza è data da un meccanismo che configura una **key simmetrica con una crittografia a key asimmetrica** (client critta con una **key segreta di sessione random ogni volta crittografando** il **tutto con la *kpb* del server**). Obiettivo è **garantire**:
- **Riservatezza**, dati protetti con crittografia simmetrica (DES o RC4),
- **Auth**, client e server sono autenticati con crittografia asimmetrica (RSA) e si scambiano certificati,
- **Integrità**, effettuati check sull'integrità del messaggio con funzioni hash (SHA o MD5).
##### Architettura di SSL
SSL opera su **2 strati**:
###### SSL Handshake
Il **livello + alto** che si interfaccia col livello **applicazione**; è **usato per l'handshake** iniziale e si divide in 4 fasi:
1) **Avvio di una nuova connessione**: consente a **client e server di negoziare l'algoritmo di generazione di chiavi**. Client manda un messaggio "*client hello*" con la sua **versione di SSL** e gli **algoritmi** supportati (a volte dopo esser stato sollecitato dal server che gli manda "*hello request*") e il server risponde con un "*server hello*" con **versione SSL e l'algoritmo scelto**.
2) **Auth del server**: qui server manda al client un **certificato** (rilasciato e con firmato digitalmente da una CA) contenente la **sua *kpb*** con "*server certificate*" (ed **eventualmente richiede auth client**). Quando entrambi hanno inviato il proprio certificato e verificato quello dell'altro, il server finisce con un "*server hello done*".
3) **Scambio chiavi di sessione**: il **client genera una chiave di sessione**, la **critta con la *kpb* del server** e gliela **invia** con "*client key exchange*". Poi manda "*change cipher spec*" per dire che i **prossimi messaggi codificati con la chiave inviata**.
4) **Chiusura dell'handshake**: Il **server risponde** al "*change cipher spec*" con lo stesso messaggio, poi il **client chiude** mandando un "*client finished message*" e **stessa cosa fa il server** con un "*server finished message*".
###### SSL Record Protocol
Si poggia sul **livello trasporto** e permette una **conversazione sicura tra le 2 parti**. Prevede che i **dati** siano **frammentati in blocchi**, **compressi e integrati con un MAC** (*Message Authentication Code*) generato con **hash** per l'integrità. Il messaggio prodotto è poi **cifrato con la chiave di sessione**, gli viene **aggiunto un header SSL e viene mandato al livello trasporto**. Il ricevente applicherà il **processo inverso ai blocchi**, quindi li decifra, decomprime, riassembla e passa all'app. 