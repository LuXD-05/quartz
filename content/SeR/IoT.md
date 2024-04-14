---
public: true
edited_seconds: 11310
modified_at: 14/04/2024 23:05:13
---
# Fondamenti
### Cos'è?
Il termine ***Internet of Things*** fu coniato da Kevin Ashton (CEO di auto-ID del MIT) per indicare una rete globale di oggetti dotati di RFID (*Radio-Frequency Identifier*).
> [!important] IoT
> Insieme di tecnologie che permettono a qualunque tipo di dispositivo di collegarsi autonomamente ad internet.

Gli oggetti compresi nella definizione di IoT sono dotati di un piccolo componente elettronico capace di renderlo un dispositivo *smart*, ovvero in grado di far comunicare il mondo reale con internet (esempi: luce che si accende quanto rileva suono o movimento, auto che frena da sola in vista di ostacoli...).
### Tecnologie
##### Componenti
L'IoT si compone di:
- **Oggetti** (**dispositivi**): univocamente indirizzabili (globalmente) e provvisti di sensori e attuatori (*embedded*), che abilitano l'invio e la ricezione di dati.
- **Sistemi di comunicazione** (con adeguata **connettività**): permettono la comunicazione tra gli oggetti e i servizi cloud in internet.
- **Piattaforma cloud**: in grado di ricevere, archiviare ed elaborare dati provenienti dagli oggetti.
- **Applicazioni**: in grado di analizzare i dati ricevuti dagli oggetti, controllarli (oggetti) da remoto (con app su telefono o pc) o per generare report spesso per fini statistici.
- ***Edge***: sono gateway, server locali o nodi periferici che elaborano i dati localmente con bassa latenza e velocità garantita (si stanno diffondendo).
![](https://i.imgur.com/tT0upk0.png)
##### Caratteristiche
###### Connettività tra oggetti e cloud
Si ottiene in 2 modi:
- **Direttamente**: tramite una WiFi locale, Ethernet o una rete cellulare.
- **Indirettamente**: tramite un IoT gateway che a sua volta si collega a una rete locale o cellulare.
###### Rendere oggetti smart
Per rendere un oggetto ***smart***, bisogna dotarlo di componenti capaci di:
- **Trasmettere** dati relativi alla realtà: questo con sensori ed elementi che rilevano grandezze fisiche.
- **Ricevere** dati dalla realtà: questo con attuatori, elementi in grado di compiere azioni (motori, relè, elettrovalvole...).
###### Tipi di comunicazione
La comunicazione può essere a breve, media o lunga distanza, e richiede tecnologie trasmissive diverse (spesso wireless).
###### Tipi di dati
Quasi tutti i dispositivi IoT generano innumerevoli quantità di dati, distinguibili in:
- **Strutturati**: dati che usano un **formato predefinito**, con campi fissi (transazioni...),
- **Non strutturati**: dati senza definizione che possono assumere **qualunque forma o dimensione** (immagini, video, audio, file...),
- **Semi-strutturati**: dati <u>non strutturati</u> ma con l'aggiunta di ***metadati***, che contengono info sufficienti per <u>catalogare, cercare ed analizzare i dati</u> (file html, xml, email...).
##### Data analytics
L'elaborazione di tutti questi viene fatta per mezzo di sistemi di ***data analytics*** (analisi dei dati), che (localmente o da remoto) permettono di guidare ulteriori azioni coi dati, individuando ***pattern*** (modelli) ed effettuando previsioni. (Per esempio, i dati dei sensori di umidità di un giardino potrebbero determinare il programma di irrigazione ottimale per la situazione). Si parla quindi di:
> [!important] Big data
> Termine con cui ci si riferisce a dei ***dataset*** il cui ***volume*** (<u>dimensione</u>), ***variety*** (<u>tipo</u>: [[#Tipi di dati]]) o ***velocity*** (<u>velocità di generazione</u>) superano la capacità di rappresentazione ed elaborazione dei DBMS relazionali tradizionali.

> [!important] Data mining
> Processo di **analisi** di **grandi volumi di dati** <u>eterogenei ed in rapido cambiamento</u>, al fine di scoprire dei ***pattern***, correlazioni o altre info *nascoste* nei dati
### Apparati elettronici base per l'IoT
##### RFID
Elemento chiave dell'IoT è il **tag RFID** (*RadioFrequency IDentification*): un **chip** con capacità di <u>elaborazione</u>, di <u>memoria</u> ed un'<u>antenna</u> (le cui <u>funzionalità</u> dipendono dalla <u>forma e dimensioni</u>). Il tag scambia dati in lettura e scrittura tramite un ***RFID reader***.
La sua area di copertura, variabile in funzione della frequenza, è di solito < 1m.
![](https://i.imgur.com/ByrAdXu.png)
In origine gli RFID si usavano per identificazione univoca di cose e persone (con l'inserimento nella sua memoria di un id), ma poi il loro uso si è allargato a sensori ed attuatori.

--- start-multi-column: ID_24ms
```column-settings
Number of Columns: 2
Largest Column: standard
Border: disabled
Alignment: center
```

![](https://i.imgur.com/0UMK64q.png)

--- column-break ---

![](https://i.imgur.com/ICuQRtF.png)

--- end-multi-column
###### Caratteristiche
- Alla costruzione, nella memoria del tag RFID è inserito un **TID** (*Tag IDentifier*), un **codice seriale identificativo unico** del dispositivo (**non falsificabile**, pena il danneggiamento del tag stesso). 
  Il **TID** <u>non può identificare l'oggetto a cui è applicato il tag</u>, ma è usato per applicazioni nell'ambito dell'**anti-contraffazione**.
- Gli RFID possono essere:
	- **Attivi**: trasmettono continuamente un segnale e sono alimentati a batteria.
	- **Passivi**: trasmettono dati quando alimentati dall'energia della RF del reader.
- Un RFID, oltre che **leggibile**, è **scrivibile** e può fornire servizi aggiuntivi, quali <u>password di accesso</u> e <u>crittografia delle info memorizzate</u>.
- I reader possono leggere + tag RFID per volta.
- Per i tag RFID vi sono vari **standard** per la **codifica** e **decodifica** dei loro dati (<u>ogni tag contiene lo standard usato</u>).
- Il **costo** dei tag RFID dipende dalla **memoria** e dal **supporto fisico** (di solito <u>basso</u>, da pochi centesimi in su).
##### NFC
I tag **NFC** (*Near Field Communication*), sono una <u>sottoclasse dell'RFID</u>, caratterizzati da un'area di copertura molto stretta per scopi di sicurezza (< 10 cm).
In un chip NFC sono integrate sia le funzioni di reader che quelle di tag, perciò ogni NFC può operare in:
- ***Active mode***: ogni nodo NFC genera il proprio campo RF per trasmettere dati.
- ***Passive mode***: 1 dei 2 dispositivi genera un campo RF e l'altro lo legge.

--- start-multi-column: ID_25ms
```column-settings
Number of Columns: 3
Largest Column: standard
Border: disabled
Alignment: center
```

![](https://i.imgur.com/Ixkf0Rg.png)

--- column-break ---

![](https://i.imgur.com/7r6XPfQ.png)

--- column-break ---

![](https://i.imgur.com/9lBNdt4.png)

--- end-multi-column
###### Caratteristiche
- Gli NFC sono <u>+ sofisticati</u> dei tag RFID (+ funzionalità), per cui anche il **costo è >.**
- I **reader** possono leggere **1 NFC per volta** (<u>frequenza NFC = 13,56MHz</u>).
- I **reader** dei tag **NFC** sono **integrati** nella > parte degli **smartphone** (uso di NFC possibile autonomamente dai consumatori).
- La **tecnologia NFC** è stata sviluppata con attenzione per la **sicurezza** di dati e transazioni con standard molto sicuri sia per accesso ai dati sia per eventuale *sniffing* di info. Vi sono vari livelli di sicurezza, tra cui:
	- Completamente aperto e **non criptato**,
	- Sistema complesso con **crittografia DES** (usati per <u>pagamenti</u> e nei <u>documenti elettronici</u>)
- Gli NFC sono integrabili in **oggetti piccoli** (soluzione + semplice sono le **etichette**, ma anche <u>all'interno dei prodotti stessi</u>) e quindi sono applicabili in molti settori (tipo pagamento, antitaccheggio, trasferimento dati, ricarica di batterie, tracciamento...).
##### Beacon
I beacon sono dei sensori attivi (cioè alimentati a batteria), basati sulla tecnologia **BLE** (*Bluetooth Low Energy*, dallo standard 4.0) e dotati di un circuito e un'antenna.
![](https://i.imgur.com/NMKr6pQ.png)
Hanno bisogno di un'**app** da installare sullo smartphone dell'utente (alla quale va dato il <u>consenso a ricevere info</u>) che deve avere **bluetooth** e **geolocalizzazione abilitati**.
Quando un dispositivo mobile entra nell'are di copertura di un beacon, questo gli invia in broadcast un **UUID** (*Universally Unique IDentifier*). Il dispositivo trasmetterà a sua volta l'UUID a un server (locale o cloud) cosicché esso potrà localizzarlo, identificarlo e inviargli messaggi personalizzati.
![](https://i.imgur.com/w6GV9po.png)
###### Caratteristiche
- **Facili** da installare e disporre,
- Possono essere collegati in **qualsiasi luogo** e a **qualsiasi oggetto**,
- Permettono il **trasferimento** di **dati** con la > parte dei **dispositivi mobili**,
- Sono anche usati per la **localizzazione *indoor* ad alta precisione**,
- **Raggio** di comunicazione raggiunge i **50m**.
###### Applicazioni
- Musei: per visualizzare dati audiovideo relativi alle opere esposte o redirectare l'utente verso un sito.
- Aeroporti: per inviare messaggi ai viaggiatori su quando spostarsi tra le zone e notificare aggiornamenti sul volo.
- ***Proximity marketing***: un servizio **geolocalizzato** (<u>si attiva quanto l'utente passa in una certa area</u>) che permette di creare e **inviare**, a *target* di una zona, **contenuti personalizzati e contestualizzati** (tipo coupon) sul loro smartphone.
##### Barcode e QR Code
Pur non essendo elettronici, i codici a barre e QR Code si trattano come parte dell'IoT. 
###### Barcode
I codici a barre diportano numeri seriali di produttori, nazioni, prodotti o pallet. Sono letti con un ***barcode reader*** a infrarossi, ma anche tramite la fotocamera di uno smartphone e quelli standard sono mediamente lunghi 4/5cm e contengono 12/16 caratteri.
Un'etichetta barcode non costa niente, ma per leggerla vanno rispettati dei requisiti:
- Il codice deve essere integro (non stinto, graffiato o spiegazzato),
- Il codice deve essere applicato in modo + piano e disteso possibile (non su angoli o aree con eccessive curvature),
- Deve esserci una condizione di luce accettabile.
La lettura, diretta e frontale, scansiona max 1 codice alla volta.
![](https://i.imgur.com/AP4cxkW.png)
###### QR Code
I **QR Code** (codici bidimensionali o *Data Matrix*) possono contenere un **> numero di info**, ma presentano gli <u>stessi problemi di corruttibilità</u> e <u>lettura non massiva</u>.
![](https://i.imgur.com/Kv87jGG.png)
### Topologie reti IoT
Per reti IoT si usano generalmente 2 topologie:
###### Stella
Tutti i nodi sono connessi ad un **hub** (nodo centrale), il quale è connesso a (o coincide con) il **default gateway** per il collegamento ad internet.
Tipicamente in una rete IoT si usa il **WiFi**, quindi l'**hub** è un **AP** (*access point*), ma si può usare anche il **bluetooth** (tipo con **BLE**) ed un **hub BT**.
![](https://i.imgur.com/f1zhDUh.png)
###### Mesh
Tutti i **nodi** sono **interconnessi** tra loro, alcuni sono però connessi al **default gateway** per il collegamento ad internet.
![](https://i.imgur.com/Z0qIFKG.png)
### Tipologie reti IoT
###### PAN
Solitamente hanno un'**area** di copertura di **10m**, sono **wireless** e caratterizzare da **bassa potenza** e **batterie** (esempio: switch collegato a telefono via BT).
###### LAN
Solitamente coprono un'**area** di **100m** e possono essere **wireless**, **wired** o una **combinazione** delle 2 (esempio: casa con alexa).
###### WAN
L'area che coprono <u>dipende dalla tecnologia</u> (da decine di km a centinaia), (esempio: *smart city*).
### Interoperability standards
> [!important] Interoperability
> Capacità di scambiare info tra dispositivi eterogenei essendo questi poi in grado di utilizzarle

Per far comunicare efficacemente i dispositivi *smart* è necessario affrontare una delle principali sfide dell'IoT: definire standard di comunicazione che permettano lo scambio e l'utilizzo di info tra dispositivi eterogenei.
Degli standard definiti o in definizione (riguardanti comunicazione wireless a livello fisico e datalink), le differenze riguardano:
- Dimensione del payload,
- Range (distanza raggiungibile),
- Requisiti di alimentazione (durata di batterie),
- Topologia della rete.
### Ambiti applicativi
##### Distanze
Si distinguono 2 ambiti applicativi per quanto riguarda le distanze:
- Short range: (PAN e LAN) caratterizzato dalla presenza di un default gateway locale che coordina il *cluster* di oggetti smart e provvede alla comunicazione con il cloud.
- Long range: (WAN) dove gli oggetti sono direttamente in comunicazione con il cloud attraverso un'infrastruttura di stazioni radio nel territorio (tipo reti cellulari).
![](https://i.imgur.com/wSnFW5K.png)
##### Servizi
I settori applicativi dell'IoT sono tanti e possono essere classificati in:
- Massive IoT: applicazioni con bassi costi, consumi e capacità di comunicazione ma anche da un gran n° di dispositivi connessi (comprendono: trasporti, logistica, ambiente, domotica, smart city, agricoltura...).
- Mission Critical IoT: applicazioni con bassa latenza, alta affidabilità e alta capacità (comprendono: automotive, smart grid, medicina, sicurezza, RA, automazione...).
![](https://i.imgur.com/8M5dsLf.png)
### Standard trasmissivi
##### BT
(*Bluetooth*) per applicazioni short range, tipo per l'IoT wearable, permette il trasferimento anche di grandi quantità di dati. Non è ideale per l'IoT dato l'elevato consumo di corrente (fino a 30mA)
Caratteristiche: frequenza = 2.4GHz, distanza = ~100m, velocità = 1/3Mbps.
##### BLE
(*Bluetooth Low Energy*) per applicazioni short range, è come il BT ma consuma meno corrente (fino a 15mA) e però non permette il trasferimento di grosse quantità di dati (ha un payload + piccolo di BT, solo pochi dati).
Caratteristiche: frequenza = 2.4GHz, distanza = 50 - 150m, velocità = 1Mbps.
##### ZigBee
Per applicazioni short range, si basa sullo standard IEEE 802.15.4, uno standard per reti PAN wireless a basso tasso trasmissivo (pochi dati e a bassa velocità). Una rete ZigBee necessita di un hub ZigBee, un dispositivo coordinatore che inizializzi la rete; inoltre (la rete) supporta un n° di nodi < 65000.
Caratteristiche: frequenza = 2.4GHz, distanza = 10 - 100m, velocità = 250Kbps.
##### WiFi
Per applicazioni short range, è la tecnologia + scelta, soprattutto per applicazioni domestiche e LAN. Supporta trasferimenti ad alta velocità di grosse quantità di dati, però presenta consumi molto elevati.
Caratteristiche: frequenza = 2.4/5GHz, distanza <= 50m, velocità = 150 - 200 Mbps (max 600 Mbps, dipende dallo standard).
##### LoRaWAN
(*Long Range WAN*) per applicazioni long range, è uno standard WAN a basso consumo ed è indicato per comunicazioni mobili IoT, smart city e applicazioni industriali. Supporta reti con milioni di nodi.
Caratteristiche: frequenza in Europa = 869MHz (<1GHz), distanza = 2/5km (urbana) o 15km (suburbana), velocità = 0.3/50Kbps, batterie da 2000mAh durano ~105 mesi.
##### Cellulare
Per applicazioni mobili long range, permette la trasmissione di grosse quantità di dati ma ha costi (SIM, eSIM) e consumi di corrente molto alti.
Caratteristiche: dipende dallo standard (2G = 35 Km, 3G = 200 Km, 4G ..., 5G ...).
![](https://i.imgur.com/9UomDiC.png)
### Edge e fog computing
All'inizio dell'IoT, i dispositivi di periferia erano solo sensori che raccoglievano dati, mentre le risorse di calcolo per elaborarli erano nel cloud. Con l'aumento esponenziale dei dispositivi e dei dati si iniziò a incorrere in latenza elevata; quindi, per evitarla, si è pensato di distribuire l'intelligienza anche in periferia.
> [!important] Edge/Fog Computing
> Architettura le cui risorse di gestione ed elaborazione sono poste vicino a sensori ed attuatori. Mentre l'***edge computing*** avviene direttamente sui sensori o su un gateway vicino ad essi, il ***fog computing*** avviene fisicamente + lontano dai sensori che generano dati (ma sempre in loro prossimità).

![](https://i.imgur.com/a3tR8dm.png)
Le risorse locali variano da memorie per storage, dispositivi di calcolo locale per elaborazione dati, controllo del sistema *smart* e configurazione in rete.
Mentre un qualunque dispositivo con capacità di calcolo, storage dati e connettività di rete (locale o internet) può essere un ***nodo edge***, i ***nodi fog*** sono realizzati grazie a pc, server dedicati...
![](https://i.imgur.com/lE7CCPS.png)
L'analisi dei dati IoT vicino a dove sono generati riduce latenza, consumo di energia, costi di comunicazione, traffico in rete e i problemi di sicurezza e privacy (dato che mantiene i dati all'interno della rete privata). Inoltre, con quest'analisi ***on the edge***, eventuali avvisi "urgenti" sono recapitati immediatamente consentendo interventi tempestivi.
### Sicurezza
Con l'IoT sono aumentate anche le minacce: i rischi di compromissione e i danni non si limitano + solo a dati e app virtuali, ma possono estendersi agli oggetti. Alla peggio, è messa a rischio l'incolumità delle persone (tipo con videocamere IoT accessibili ovunque e da chiunque: [insecam](http://www.insecam.org/)).
Per proteggersi, si può ricorrere a: auth (per permettere agli utenti di identificarsi verso un dispositivo) e cifratura (per proteggere i dati in locale e in transito tra i dispositivi e il cloud).
### Industry 4.0
> [!important] Industry 4.0
> Adozione, in ambito industriale e manifatturiero, di ***Smart Technologies***, tecnologie digitali innovative capaci di aumentare l'interconnessione e la cooperazione delle risorse (tra beni fisici, persone e info) usate nei processi operativi sia interni ai luoghi di produzione sia esterni.

Con questa la fabbrica si digitalizza diventando una ***Smart Factory***, ovvero una fabbrica in cui tutti i componenti, sia fisici che virtuali, sono interconnessi e operano in modo coordinato.
Questo implica la presenza di sensori che rilevano specifici dati, i quali verranno poi integrati in sw ERP (*Enterprise Resource Planning*, gestionali), *supply chain*, servizi di assistenza clienti e altri sistemi aziendali, ampliando ed integrando le info.
![](https://i.imgur.com/jR7Z2id.png)
##### Smart Technologies
Delle *Smart Technologies* fanno parte:
- L'IoT (inteso come sensori, attuatori, gateway e altri oggetti connessi),
- Il *cloud computing*, che consente l'archiviazione e l'elaborazione di grandi quantità di dati in modo economico, vantaggioso e scalabile. Con questo tipo di servizio, i produttori possono:
	- Accedere ***on demand*** a risorse quali potenza di calcolo e storage necessari senza dover mantenere un'infrastruttura fisica,
	- Analizzare efficacemente i dati da dispositivi IoT e altre fonti per migliorare l'efficienza produttiva e la qualità del prodotto,
	- Facilitare la collaborazione e la condivisione dei dati tra le parti della *supply chain*, migliorandone la gestione.
- L'analisi dei ***Big data*** (per attività predittive),
- L'***additive manufacturing***, ovvero la stampa 3D per realizzare oggetti in 1 unico processo di stampa aggiungendo un layer sopra l'altro (al posto di tradizionali metodi di produzione sottrattiva con frese e torni),
- La robotica avanzata, cioè robot *smart* per applicazioni in ambiente ostile o di servizio, quindi: "creature meccaniche che possono funzionare autonomamente" ("creature" perché attuano il processo di *decision making* autonomamente con sensori (percezione), attuatori (azione) e sw IA (ragionamento); mentre "meccaniche" perché costruiti dall'uomo).
- I dispositivi *wearable* tipo *smart glasses* accompagnati dall'uso di:
	- VR (*Virtual Reality*): che richiede l'uso di specifici *headset VR* che mostrano all'utente contenuti 3D virtuali generati,
	- AR (*Augmented Reality*): che lavora con qualsiasi smartphone o con *AR glasses* e permette di vedere il mondo reale con aggiunti contenuti virtuali.
### Considerazioni
- Non ci sono ancora abbastanza modelli standard per l'IoT.
- Nell'IoT sono critici gli elementi spaziali (posizione geografica di un oggetto) e dimensionali (dimensione di un oggetto).
- La sicurezza è uno degli aspetti + critici dell'IoT, e presenta caratteristiche peculiari rispetto alle reti tradizionali.
- Anche dal punto di vista della privacy, l'IoT presenta vari problemi, che vanno affrontati e risolti se si vuole ottenere la fiducia degli utenti.
# Localizzazione

# MQTT e CoAP

# Considerazioni di progetto
### Livello percezione
##### Sensori e attuatori
Per rilevare dati dall'ambiente si usano i **sensori** (da grandezza fisica a grandezza elettrica), da interfacciare ad un hw adatto per creare un sistema di rilevamento.
Per trasmettere invece info all'ambiente si usano gli **attuatori** (da grandezza elettrica a grandezza fisica), tipo motori o relè.
Per quanto riguarda i **sensori** poi, bisogna tenere in considerazione:
- Frequenza di campionamento dei dati,
- Tempi richiesti di memorizzazione dei dati,
- Frequenza di invio dati al cloud (o l’app in *fogging*),
- Latenza.
###### Piattaforme hardware
- Arduino: scheda microcontrollore, quindi, dotata di un *single-chip computer*, monoprogrammato e senza OS.
- Raspberry PI: è un *Single Board Computer*, cioè un computer su un'unica scheda, sulla quale è presente un processore e una memoria dedicati e dove viene eseguito l'OS multiprogrammato (Linux o Raspberry PI OS)
### Livello rete
##### Trasmissione
Realizzato il dispositivo, si vorrà che questo trasmetta i dati da qualche parte:
- Ad un dispositivo locale (***on the edge*** o in ***fogging***) wireless: con BT, BLE, WiFi, ZigBee, LoRa.
- Ad un dispositivo remoto (cloud):
	- Direttamente: SIM + tecnologia cellulare (2G, 3G, 4G, 5G) ma anche MPN.
	- Indirettamente (tramite gateway): DSL, fibra, WAN Ethernet, LoRaWAN, FWA.
- Ad un altro nodo della rete (mesh): ZigBee, LoRa.
Poi, in relazione a contesto, *range*, sicurezza, potenza, dati... si sceglieranno 1 o anche + tecnologie.
##### Bande di frequenza
Con l'IoT bisogna affrontare il problema dell'affollamento all'interno delle bande di frequenza ISM e di quelle con licenza (4G, 5G) dato il n° molto alto di dispositivi wireless interconnessi. Perciò bisogna permettere a + comunicazioni di avvenire contemporaneamente, senza interferenze:
- Nella banda *short range* (2.4GHz), ci sono le tecnologie WiFi, BT e ZigBee oltre ad altre interferenze esterne (esempio: microonde), e queste:
	- Sono usate per applicazioni a breve distanza (da 1m a 100m in spazi aperti e meno se negli edifici),
	- Permettono tassi trasmissivi nell'ordine dei Mbps,
	- Si usano in ambienti interni (indoors).
- Nelle bande *long range* (sub-1GHz: 434MHz e 868MHz), sono usate tecnologie tipo LoRaWAN e:
	- Sono usate per applicazioni a lunga distanza (da 100m a 20km in spazi aperti),
	- Permettono tassi trasmissivi nell'ordine dei 100 bps,
	- Si usano in ambienti esterni (outdoors).
Per risolvere il problema dell'affollamento delle bande migliorando le prestazioni dei sistemi wireless poi, si usano tecnologie che consentono a + utenti di condividere lo stesso insieme di frequenze.
### Livello applicazione
Scelta la tecnologia di comunicazione è possibile inviare i dati ad un servizio cloud (autoprodotto o scelto e gratis o a pagamento). Ottenuto il ***back-end*** cloud (programma che elabora i dati ricevuti implementando funzionalità), è poi possibile usare il sistema IoT; e per farlo, si può costruire un ***front-end*** (app con interfaccia su telefono o pc con cui si può interagire con i dispositivi *smart*) tramite cui si possa controllare il sistema.
Il cliente non ha il controllo del cloud ma può usarne alcune risorse (app SaaS o storage/elaborazione tramite IaaS); in questo modo IoT può beneficiare delle risorse cloud per superare i suoli limiti tecnici.
# ZigBee

# LoRaWAN

# ZigBee vs LoRaWAN

# Mobile app