---
public: true
edited_seconds: 30
modified_at: 12/06/2024 11:49:58
---
### Livello percezione
::
##### Sensori e attuatori
Per rilevare dati dall'ambiente si usano i **sensori** (da grandezza fisica a grandezza elettrica), da interfacciare ad un hw adatto per creare un sistema di rilevamento.
Per trasmettere invece info all'ambiente si usano gli **attuatori** (da grandezza elettrica a grandezza fisica), tipo motori o relè.
Per quanto riguarda i **sensori** poi, bisogna tenere in considerazione:
- Frequenza di campionamento dei dati,
- Tempi richiesti di memorizzazione dei dati,
- Frequenza di invio dati al cloud (o l’app in *fogging*),
- Latenza.
###### Piattaforme hardware
- **Arduino**: scheda microcontrollore, quindi, dotata di un *single-chip computer*, monoprogrammato e senza OS.
- **Raspberry PI**: è un *Single Board Computer*, cioè un computer su un'unica scheda, sulla quale è presente un processore e una memoria dedicati e dove viene eseguito l'OS multiprogrammato (Linux o Raspberry PI OS)

### Livello rete
::
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
::
Scelta la tecnologia di comunicazione è possibile inviare i dati ad un servizio cloud (autoprodotto o scelto e gratis o a pagamento). Ottenuto il ***back-end*** cloud (programma che elabora i dati ricevuti implementando funzionalità), è poi possibile usare il sistema IoT; e per farlo, si può costruire un ***front-end*** (app con interfaccia su telefono o pc con cui si può interagire con i dispositivi *smart*) tramite cui si possa controllare il sistema.
Il cliente non ha il controllo del cloud ma può usarne alcune risorse (app SaaS o storage/elaborazione tramite IaaS); in questo modo IoT può beneficiare delle risorse cloud per superare i suoli limiti tecnici.