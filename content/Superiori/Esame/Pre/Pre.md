---
modified_at: 19/06/2024 22:44:35
edited_seconds: 4660
---
# Esame
### Traccia
![[ITIA_SUP18.pdf]]

### Risoluzione
##### Intro
Viene presentata una realtà di interesse caratterizzata da un complesso industriale appartenente alla società MyStart composto da tre capannoni relativamente vicini l'uno all'altro ed adibiti a scopi diversi:
- Il 1° capannone (C1) è suddiviso in due aree: un'area uffici (C1U), per la stessa società MyStart, ed una sala server (C1S), nella quale saranno ospitati i principali sistemi di gestione dell'intera infrastruttura di rete.
- Il 2° e il 3° capannone (C2 e C3) invece sono suddivisi ognuno in 8 aree (C2.1, C2.2...), ciascuna delle quali è destinata ad ospitare una diversa startup.
Dunque, è richiesta l'elaborazione di una rete (fisica e logica) che permetta di offrire i vari servizi alle startup, tra cui:
- Connettività cablata e wireless,
- Collocazione di server e hosting di servizi nella sala server,
- Accesso remoto e gestione dei servizi sui server dovunque,
- Sicurezza e controllo degli accessi...
#### Parte 1
##### 1)
Come illustrato nel disegno di rete, supponendo che non sia presente alcuna infrastruttura di rete preesistente eccetto, saranno necessari:
Dal punto di vista **hardware**:
- 1 **router** che fungerà da *default gateway* della rete interna e fornirà connettività. Siccome dovranno essere gestite varie startup in 2 capannoni, si potrebbe pensare di usare un dual-WAN router (router con 2 porte WAN) e prevedere 1 linea di connessione ad internet per capannone così da sostenere il traffico di entrambi i capannoni senza problemi. Inoltre il collegamento sarà fatto in fibra ottica, per avere diritto ad una velocità di download/upload ottimale, FTTH oppure almeno FTTC;
- Un **NGFW** (eventualmente *embedded* nel router) per filtrare il traffico di rete, avente anche le funzioni di un IPS per la prevenzione dei tentativi di intrusione, le funzioni di un *proxy server* con l'opzione di "*application level filtering*" attivata per filtrare il traffico a livello applicativo ed anche la capacità di permettere o meno il traffico VPN;
- Vari switch, 1 per ogni area dei capannoni + le altre reti (C1U, C1S e DMZ) (+ 2 al posto dei router C2 e C3???),
- Diversi AP (1 per ogni area dei capannoni + 1 nella rete C1U) con il supporto almeno dello standard WiFi 5 per garantire velocità di navigazione adeguate anche ai dispositivi mobili, del PoE, così da poter distribuire l'alimentazione di essi tramite lo stesso cavo ethernet, dell'autenticazione con RADIUS e di una protezione di sistema con auth WPA2;
- I server della DMZ (Web server, App server, Mail server...),
- I server interni (con DBMS phpmyadmin e mysql, NAS e storage configurato in RAID 5, DNS (?), Server RADIUS per la sola autenticazione dei dispositivi appartenenti a membri di MyStart o delle startup ospitate nei capannoni (?), VM (???)...),
- Tutto il necessario per il cablaggio ((strutturato secondo lo standard EIA/TIA 568)) (cavi ethernet *shielded twisted pair* in abbondanza per tutti i possibili host e per i collegamenti dei server, per i quali saranno eventualmente previsti dei cavi in fibra ottica),
- ...
Dal punto di vista **software** (supponendo che dipendenti di MyStart e startup abbiano i loro portatili): 
- Antivirus e antimalware nelle macchine server,
- Programma VPN Server per il router (mentre non sarà necessario prevedere delle VPN *site-to-site* tra i capannoni data la distanza copribile anche con collegamenti *point-to-point*, bisognerà prevedere delle VPN *remote access* per l'accesso remoto di utenti (sempre con autenticazione) ai server),
- Software di virtualizzazione e di gestione delle VM *type-1* (*bare-metal*), per esempio VMWare,
- ...

Per quanto riguarda l'indirizzamento invece, partiamo dal presupposto che ci sono 3 capannoni, 1 diviso tra server (64 host) ed uffici (64 host) e 2 con 8 zone, ogni zona con massimo 8 pc cablati e 16 dispositivi wireless (24 x 16 zone) + stampanti condivise, in totale si arriva ad avere (se per ogni zona si prevede uno spazio di indirizzamento pari a 32, quindi 5 bit) 640 host totali, per cui servirà uno spazio di indirizzamento totale di 10 bit e quindi si utilizzerà una subnet mask = /22.
Si useranno quindi indirizzi di classe C nell'ordine del 192.168.xxx.xxx (da fare nel disegno). La prima cosa che sarà necessaria fare sarà impostare un IP statico ai server ed alle stampanti cosicché siano sempre indirizzabili in rete in modo univoco; poi bisognerà implementare un DHCP server anche in sala server, estendendo la sua azione alle altre reti tramite dei DHCP relay agent e permettendo l'assegnazione automatica di IP dinamici a tutti gli host della rete.

Infine è richiesto che sia garantita la *business continuity*; perciò saranno necessarie precauzioni di *fault tolerance* per prevenire guasti all'infrastruttura o interruzioni di servizio:
- Ridondanza degli apparati (cone detto RAID 5 x NAS)
- Gruppi di continuità per salvaguardare il sistema nel caso si verifichino *blackout*,
- (gia detto) firewall e antivirus x prevenire attacchi ed interruzioni,
- Eventuale duplicazione di cavi e collegamenti (costosa),
- Sistemi di backup adeguatamente configurati,
- 
##### 2)
Innanzitutto, se i capannoni sono divisi in aree, si presuppone che questi siano divisi anche fisicamente; perciò, al fine di proteggere fisicamente gli accessi una startup dalle altre è necessario adoperare dei badge RFID che identifichino gli utenti e che permettano l'ingresso alle aree solo agli utenti che ne hanno l'autorizzazione.
Per quanto riguarda il traffico di rete poi, oltre al filtraggio del firewall, sarebbe ideale definire le autorizzazioni alle risorse di ogni startup tramite delle ACL (*access control lists*) a livello di router; inoltre è possibile suddividere le varie zone nei capannoni a livello logico con VLAN, questo però prevede anche che vengano adottati degli switch che supportano lo standard 802.1q, ovvero che siano in grado di taggare il traffico.
(Server sono virtualizzati, quindi auto divisione del traffico ??? ...)
Infine, per la sala server, oltre all'azione del NGFW ed alle suddette ACL, è sempre possibile abilitare l'accesso fisico solo ai membri di MyStart sempre con badge RFID; e poi sarebbe ideale prevedere porte blindate e videosorveglianza.
##### 3)
??? DHCP? DNS? ???
##### 4)
La 1a tecnica, meno complessa, prevede semplicemente l'uso di un client SSH installato sui pc dei membri delle startup, implementando quindi un servizio di remote desktop cosicché sia possibile accedere direttamente ai server da un qualsiasi luogo.
La 2a tecnica invece prevede l'uso di VPN. In questo caso sarebbe possibile usufruire o di una VPN remote access o di una VPN SSL. Per i server aziendali cambia poco in quanto va comunque installato e configurato un programma VPN server; mentre per quanto riguarda gli utenti è sia possibile installare un VPN client ed accedere alle risorse della propria startup da remoto attraverso una remote access VPN oppure, per comodità, si può usufruire di un qualsiasi servizio di VPN SSL lato client tramite browser per accedere ai server aziendali.
Ovviamente in entrambe le soluzioni, il NGFW a 3 porte dovrà consentire il traffico VPN in entrata per i dispositivi autenticati, verificandone anche le varie autorizzazioni.
#### Parte 2
##### 1)

##### 2)


# Altro
### Analisi
3 capannoni distanti 100m su terreno privato.
C1 = area uffici per MyStart e sala server. 5 uffici ognuno con 1 pc con internet wired e in corridoio 1 stampante condivisa.
C2 e C3 = divisi ognuno in 8 aree, con ogni area per 1 start-up.
##### Rete
C1U (uffici) = **128 host**? supponendo che ogni dipendente di MyStart abbia pc, cell e altro...
C1S (server) = (16 startup tot) **64 host** (8 host in server a startup??? + sistemi di monitoraggio degli uffici di MyStart ???)
C2 = (C2.1, C2.2 ...) 8 pc + 16 mobile = **24 host** = 32 (2^5) (x 8)
C3 = ("") " = **24 host** = 32 (2^5) (x 8)
##### Richieste implicite
- Offrire (a ogni start-up):
	- Connettività (cablata x max 8 pc e wireless per max 16 host),
	- Server (su cui pubblicare servizi tipo web server, web app e database) + accesso da rete locale ai server in C1 cosicché ogni start-up possa gestire i propri servizi (con soluzioni idonee anche diverse, tra OS, linguaggi web, DBMS...), 
	- Continuità di servizio,
	- Gestione remota,
	- (Stampante condivisa),
##### Richieste esplicite (1a parte)
1) Disegno di rete +:
   - Hw e sw necessari + criteri di dimensionamento dove necessari,
   - Piano di indirizzamento (VLSM)
   - Caratteristiche del collegamento ad internet (?)
   - Soluzioni per continuità del servizio (ridondanza, virtualizzazione, tutte misure dei datacenter e di business continuity)
2) Tecniche di controllo accessi per proteggere da quelli non autorizzati (locali, di altre startup o esterni) + tecniche di protezione dei server da attacchi interni ed esterni (fisici e logici?).
3) Principali servizi di rete necessari (tipo: identificazione utenti, assegnazione config di rete ai client, risoluzione dei nomi...) con esempi delle configurazioni per 1 a scelta.
4) 2 possibili soluzioni per le startup per gestire i propri servizi accedendo ai server da remoto.
##### Richieste esplicite (2a parte)
1) ER e modello logico del db necessario + pagine web (codificazione di una parte significativa) per gestire: autenticazione utenti degli uffici MyStart (presso sito) e visualizzazione elenco candidature startup.
2) Vantaggi e svantaggi dell'adozione di VM in sala server + motivazioni.


PRIMA PARTE
In un comprensorio industriale costituito da tre capannoni, distanti fra loro meno di un centinaio di metri e dislocati su un terreno privato, la società di servizi MyStart vuole realizzare un “incubatore di imprese” in cui ospitare delle start-up (piccole aziende nascenti, con un progetto innovativo), offrendo loro servizi amministrativi e tecnologici. Tra questi ultimi, MyStart vuole offrire a ciascuna start-up la connettività ad Internet e la possibilità di usufruire di sistemi server su cui pubblicare i propri servizi web, le proprie applicazioni ed organizzare banche dati. Alle aziende start-up dovrà essere garantita la continuità dei servizi offerti e la possibilità di poterli gestire anche da remoto.
Nel primo capannone sono previsti un’area uffici per la stessa società MyStart ed un locale tecnico (sala server) con i principali sistemi di gestione dell’intera infrastruttura di rete. Gli uffici sono in tutto 5, ciascuno con un singolo personal computer da collegare ad Internet, mentre nel corridoio comune è presente una stampante condivisa.
Ognuno degli altri due capannoni sarà suddiviso in 8 aree, ciascuna destinata ad ospitare una diversa start-up. Per ciascuna di queste aree dovranno essere disponibili:
 la connettività cablata per un massimo di 8 computer, con accesso ad Internet;
 una stampante condivisa;
 la connettività wifi per dispositivi mobili (smartphone, tablet, laptop,…) fino ad un massimo di 16;
 l’accesso via rete locale ai sistemi server presenti nel primo capannone, in modo che ogni start-up possa gestire i propri servizi (ad esempio portali web, pubblicazione di listini online, cataloghi di prodotti, etc.), utilizzando le piattaforme che più ritiene idonee (anche con differenti sistemi operativi, linguaggi web, DBMS, …).

Il candidato, formulate le opportune ipotesi aggiuntive, sviluppi i seguenti punti:
1. Proponga un progetto, anche grafico, dell’architettura dell’infrastruttura di rete necessaria a
rispondere alle esigenze sopra descritte dettagliando:
a) le risorse hardware e software necessarie, indicandone, ove utile, i criteri di
dimensionamento;
b) un opportuno piano di indirizzamento;
c) le caratteristiche del collegamento ad Internet;
d) le soluzioni possibili per assicurare la continuità del servizio.
2. Individui e descriva possibili tecniche per proteggere ciascuna start-up da accessi anche locali
non autorizzati da parte di personale appartenente alle altre start-up, e per proteggere i server nel
locale tecnico da attacchi esterni ed interni.
3. Proponga i principali servizi di rete necessari (tra cui ad es. identificazione degli utenti,
assegnazione della configurazione di rete ai vari client, risoluzione dei nomi, …), esemplificando
le relative configurazioni per uno di essi a sua scelta.
4. Proponga due possibili soluzioni per consentire alle start-up la gestione dei propri servizi
mediante accesso remoto ai server.

SECONDA PARTE
I. In relazione al tema proposto nella prima parte, la società MyStart ha predisposto un modulo online con cui una società nascente può candidarsi per diventare una start-up e usufruire dei servizi descritti. Le candidature sono visualizzabili, previa autenticazione, dai responsabili della società MyStart. Il candidato realizzi il modello concettuale e logico della porzione di base di dati necessaria a questo scopo; progetti poi le pagine web per la visualizzazione dell’elenco delle candidature, e ne codifichi in un linguaggio a sua scelta una parte significativa.
II. In relazione al tema proposto nella prima parte, il candidato discuta vantaggi e svantaggi dell’adozione di eventuali macchine virtuali sui sistemi server nel locale tecnico (primo capannone) per implementare i servizi delle start-up, motivando le scelte effettuate.