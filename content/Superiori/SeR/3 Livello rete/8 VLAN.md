---
public: true
edited_seconds: 16150
modified_at: 28/04/2024 13:03:03
---
### VLAN
Hint: problema, soluzione, definizione
::
###### Problema
Una rete in cui sono presenti solo switch livello 2 costituisce un unico ***broadcast domain***, nel quale i pacchetti broadcast limitato ("255.255.255.255", che vengono incapsulati in frame broadcast "FF-FF-FF-FF-FF-FF") arrivano a tutte le interfacce sul link. In LAN grandi, con <u>grandi domini broadcast</u>, questi broadcast creano spesso **traffico inutile** e **sovraccaricano la rete** (+ comune che un host parla con un gruppo di host, non con tutti).
###### Soluzione
Per ovviare a ciò è stato definito lo **standard IEEE 802.1q** per gli **switch 802.1q** (diversi da switch di livello 3, questi non eseguono routing), che permette di <u>suddividere una LAN in</u> un insieme di **VLAN** (*Virtual LAN*). Ogni **VLAN** in sé costituisce un **dominio di broadcast separato**, quindi un broadcast mandato in una VLAN viene elaborato solo dagli host appartenenti alla stessa.
##### Definizione
> [!important] VLAN
> Una **VLAN** è una rete locale che raggruppa host **logicamente** e indipendentemente dal tipo di rete.
<!--SR:!2024-04-30,2,205-->

Le porte che collegano host a switch 802.1q sono diverse dalle porte che collegano 2 switch 802.1q (vedi [[#Tipi di porte]]). Una singola VLAN può inoltre essere configurata su un solo switch 802.1q o su più.
<!--SR:!2024-04-30,2,200-->

### Modalità di raggruppamento VLAN
Hint: porte, MAC, IP
::
##### Per porte
Si possono associare delle VLAN a 1 o + porte (interfacce) di uno switch 802.1q.
**Problema**: questo metodo non è efficace per il fatto che è possibile cambiare manualmente la porta a cui è connesso un host e quindi cambiare la VLAN in cui è stato configurato.
##### Per indirizzi MAC
Si possono associare anche gli indirizzi MAC degli host a certe VLAN.
**Problema**: esistono appositi programmi che permettono a un pc di modificare il proprio indirizzo MAC anche senza autorizzazione.
##### Per indirizzi IP
In questo modo è <u>come se la LAN fosse subnettata</u> e ad **ogni subnet è associata una VLAN**. Questo è il metodo + diffuso grazie alle minori criticità di sicurezza presentate.
###### Configurazione switch VLAN
La configurazione di uno switch VLAN può essere fatta in modo statico (reti piccole) o dinamico (reti grandi con tanti switch VLAN, in cui si usano software per il controllo delle VLAN tipo **VTP**, *VLAN Trunking Protocol*).
<!--SR:!2024-05-01,3,220-->

#### Fondamenti 802.1q
Le VLAN (secondo lo standard) sono identificate tramite un VID (*VLAN Identifier*); inoltre, le VLAN raggruppate per IP:
- Sono identificate da un VID (numero da 1 a 4096, 12 bit),
- Hanno un proprio range di indirizzi IP (con indirizzo rete e subnet mask, come le subnet),
- Vanno definite negli switch 802.1q (configurandone le interfacce assegnando ognuna a 1 sola VLAN),
- Ricevono solo il traffico trasmesso al loro interno.

### Tipi di porte
Hint: access, trunk, native
::
Ci sono 3 modi per configurare le porte di uno switch 802.1q:
##### Access port (untagged)
Queste porte sono configurate in modo che vi si possano collegare gli host, cosicché siano associati a una singola VLAN. I frame in uscita da una *access port* <u>non</u> hanno VLAN tag.
##### Trunk port (tagged)
A queste vi si collegano altri switch VLAN o router (per l'[[8 VLAN#Routing inter-VLAN|inter-VLAN routing]]) e su esse viaggia il traffico qualsiasi VLAN. Sul ***trunk*** (cavo di collegamento ***cross*/incrociato**) viaggiano dei frame 802.1q aventi un VLAN tag (detto traffico 1Q) e il traffico delle ***native VLAN*** senza tag.
##### Native port
A queste si collegano gli switch legacy (non 802.1q) o hub, che non sanno taggare il traffico. Quando uno switch 802.1q riceve un frame *untagged*, lo invia a tutte le trunk e native ports (fino ad arrivare a vicoli ciechi, dove viene poi scartato).
Alla *native VLAN* va associato un certo VID, unico per tutti gli switch 802.1q in rete.
<!--SR:!2024-04-30,2,200-->

### Inoltro frame VLAN
::
Gli switch 802.1q usano delle tabelle d'inoltro (strutturate tipo: "**port | MAC | VID**") per inoltrare frame VLAN. Quando un frame ethernet arriva a uno switch VLAN viene esaminata la tabella d'inoltro e, prima di viaggiare per il *trunk*, lo switch rende il frame *tagged* inserendovi un tag con il VID della VLAN di destinazione. Arrivato allo switch VLAN di destinazione, questo gli toglierà il VLAN tag e lo invierà alla *access port* corretta.
Solo gli switch d'infrastruttura devono essere 802.1q-compatibili, al contrario di NIC degli host, hub, switch legacy...
<!--SR:!2024-04-30,2,200-->

### VLAN voce
Hint: modi di collegamento telefono VoIP e pc, vantaggi aux vlan
::
Potrebbe essere necessario collegare anche dei <u>telefoni VoIP</u> a internet con cavo ethernet. Ci sono 2 modi:
- Usando <u>2 cavi</u> (1 per pc e 1 per VoIP) collegati <u>a 2 porte dello switch</u> (poco pratico).
- Usando lo **switch a 3 porte ethernet** <u>integrato nel telefono VoIP</u>, con <u>1 porta</u> collegata allo <u>switch di infrastruttura</u>, <u>1 al telefono </u>e l'<u>altra al pc</u> (migliore).
Col 2° metodo, la <u>separazione tra il traffico del telefono da quello del pc</u> è fatta con una ***aux VLAN***, che prevede che:
- Il <u>link tra lo switch</u> d'infrastruttura e <u>quello del telefono</u> è **trunk** (traffico ***tagged*** appartenente o al telefono o al pc),
- Il <u>link tra lo switch del telefono</u> e il <u>pc</u> è **access** (traffico ***untagged*** appartenente solo al pc).
<!--SR:!2024-05-01,3,220-->

### Routing inter-VLAN
Hint: legacy, router-on-a-stick, switch L3
::
L'***inter-VLAN routing*** (ovvero la comunicazione tra 2 VLAN) è possibile solo con un dispositivo di livello 3 (switch L3 o router) in quanto le VLAN sono reti IP diverse. Sono possibili 3 metodi per l'*inter-VLAN routing*:
##### Legacy inter-VLAN routing
Si usa un router di cui ogni interfaccia è una ***VLAN-subnet***, mentre il router stesso è il **default gateway** di ogni VLAN. Le porte che connettono il router agli switch sono **access**.
**Problema**: metodo poco usato per il n° limitato di interfacce presenti nei router.
##### Router-on-a-stick
Qui il traffico delle VLAN è portato su un'unica interfaccia del router con un un **trunk**, alla quale sono connessi più switch 802.1q "in serie" (senza limiti sul n° di switch e quindi di subnet).
**Problema**: questo crea un ***bottleneck***, quindi serve un'interfaccia sufficientemente veloce.
##### Switch L3
Si collegano gli switch 802.1q da far comunicare a uno switch L3 con dei **trunk** (risolvendo il problema delle poche interfacce e del *bottleneck*). Sullo switch L3, pr ogni VLAN di cui instradare il traffico anche non direttamente collegata ad esso, vanno configurate delle SVI (*Switch Virtual Interface*), che fungono da default gateway per ogni VLAN.
<!--SR:!2024-04-30,2,200-->

#### Switch L2 vs Switch L3 vs Router


### Benefici VLAN
::
Le VLAN portano vari benefici:
- Separazione logica dei nodi in base al tipo di traffico (*workgroups*) e non in base alla distribuzione geografica,
- Aumento delle prestazioni per la suddivisione di un grande dominio di broadcast in parti + piccole,
- Elevata sicurezza:
	- Segmenti di rete isolati impediscono accessi senza auth,
	- Possibile l'impostazione di policy di accesso, di assegnazione IP...
	- Possibile implementazione di diverse politiche di sicurezza per ogni VLAN.
##### Esempi d'uso
Esempi d'uso contano:
- Separazione logica di aree di rete (tipo area clienti da area dipendenti),
- Costruzione di **DMZ** (*DeMilitarized Zones*)
<!--SR:!2024-05-01,3,220-->
