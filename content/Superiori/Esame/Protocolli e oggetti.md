---
edited_seconds: 3360
modified_at: 03/05/2024 09:53:46
---
### Oggetti IoT
##### RFID
Chip con capacità di elaborazione, memoria e un'antenna. Scambia dati con gli RFID reader. I chip possono essere attivi (alimentati a batteria, trasmettono sempre) o passivi (trasmettono se alimentati dalla RF del reader). 
**Range**: < 1m (short)
**Traffico**: piccolo (pochi dati, tipo credenziali o identificatori)
**Uso**: identificazione di cose e persone + in sensori e attuatori
**Localizzazione**: fino a 5m (passiva), tipo antitaccheggio supermercato
##### NFC
Sottoclasse di RFID, sia modalità attiva (chip NFC genera RF per trasmissione) che passiva (legge campo RF di altro chip NFC)
**Range**: < 10cm (per scopi di sicurezza) (short)
**Traffico**: piccolo (credenziali o id)
**Uso**: specialmente per pagamenti e documenti elettronici per la sicurezza e crittografia DES (sono in tanti telefoni)
##### Beacons
Sensori attivi alimentati a batteria basati sulla tecnologia BLE (la quale permette una durata prolungata delle batterie) e dotati di antenna. Necessitano di auth di bluetooth e geolocalizzazione.
**Range**: < 50m (short)
**Traffico**: normale/medio
**Uso**: ottimi per musei (tipo mostrare info su un quadro di cui si è in prossimità), aeroporti (capire dove andare) e proximity marketing (ads localizzati in base a zone)
**Localizzazione**: fino a 5m, consumo basso e richiede un'app. Anche con LoRaWAN (?)
##### QR e barcode
Codici grafici leggibili da reader o fotocamere di cellulari. Corruttibili e impossibile la lettura massiva. Però sono ottimi per identificazione di cose e piccoli dati tipo URL.
### Tecnologie
##### VLC
Permette la trasmissione di dati attraverso lampadine LED (cicli di on/off impercettibili a occhio umano) e anche la localizzazione attraverso *fingerprinting* (si basa sulla forza del segnale ricevuto).
Ideale per la salute, no interferenze e usabile infrastruttura esistente. Tuttavia la luce può essere schermata, intercettata e non va outdoors.
**Range**: 10/15m (short)
**Traffico**: ?
**Consumo**: basso (LED) e alto (dispositivi con fotocamera)
**Uso**: usato in ambienti domestici o indoors per trasmettere dati o localizzare dispositivi.
##### BT
Tecnologia principalmente PAN, poco ideale per IoT per elevato consumo.
**Range**: < 100m (anche se + sui 10m, short)
**Traffico**: medio/alto (1/3Mbps)
**Consumo**: elevato (fino a 30mA)  
**Uso**: buono per dispositivi *wearable*
##### BLE
Come BT ma consuma molto meno ed è + ideale per l'IoT
**Range**: < 50/150 m (anche se è sui 5/10m (dipende da beacon), short)
**Traffico**: medio (~1Mbps)
**Consumo**: ridotto (fino a 15mA)  
**Uso**: principalmente in beacon o IoT domestico (o luoghi chiusi)
Con BLE è anche possibile la localizzazione indoor tramite **beacon**. Si usano 2 tecniche: <u>trilaterazione</u> (calcola <u>distanza da (3) beacon</u> in base al tempo di invio e ricezione di messaggi) e <u>triangolazione</u> (misura l'angolo di arrivo dei messaggi e quindi la direzione dell'host)
##### ZigBee
Standard IEEE 802.15.4 per PAN wireless a basso tasso trasmissivo. Necessita di un hub (*ZigBee coordinator*) che inizializzi la rete, ma supporta fino a 65000 nodi.
Rete Zigbee si compone di coordinator (1) che inizializza la rete e poi si comporta da router, i router, collegati in mesh e tramite cui sono scambiati pacchetti, e end-device, associati ad uno ZR (maz 14 x ZR) periodicamente richieste di polling a ZR.
**Range**: < 10/100 m (short)
**Traffico**: basso (~250Kbps)
**Consumo**: basso
**Uso**: indoor, distanze limitate, velocità e carico limitati, mesh, bassa latenza (real time), tanti nodi, pochi muri o ostacoli.
##### WiFi
Standard usato molto in case e LAN, permette grandi tassi trasmissivi a costo di maggiore consumo di corrente (necessaria alimentazione).
**Range**: < 50 m (short)
**Traffico**: alto (150/200 Kbps (max 600))
**Consumo**: molto elevato
**Uso**: comune in abitazioni e LAN
##### LoRaWAN
Standard datalink per dispositivi LoRa (con localizzazione integrata) per app long range. Supporta milioni di nodi.
LoRa (come Zigbee però a lungo raggio) non richiede alti tassi trasmissivi (tipo WiFi) e risolve il problema dello short range (BLE). 
**Range**: 2/5 km (urbana) o 15 km (rurale) (long)
**Traffico**: molto basso (0.3/50 Kbps) 
**Consumo**: molto basso
**Uso**: utile per smart city e reti con tantissimi nodi. ottimi per rilevamento incendi (inoltre sempre accesi). smart parking. coprono anche + piani di edificio, geolocalizzazione nativa. AES-128, sia in che out doors, sia public che private.
Gli end-nodes mandano info ai concentrators, questi poi le inoltrano al network server, il quale reinvia i dati al cloud e alle app.
USARE: outdoors, per avere + batteria, grandi distanze, non real time, tanti nodi.
##### Cellulare
Sono 2/3/4(LTE)/5G, long range, alti tassi trasmissivi ma costi e consumi alti.
**Range**: (long)
**Traffico**: molto alto 
**Consumo**: molto alto
**Uso**: soprattutto per smartphone con SIM ed eSIM
###### MPN
Mobile Private Network, prevedono l'adozione di SIM private con costi molto minori rispetto a quelle normali che comunicano solo con un'azienda.
### Altro
##### GNSS
GNSS è un sistema di radionavigazione per qualunque tipo di veicolo/oggetto che include un ricevitore GNSS (chiamati di norma GPS).
**Range**: globale
**Uso**: usato per la geolocalizzazione globale <u>non</u> al coperto (indoor, in tunnel o sott'acqua).
##### Cosa definire per localizzazione
- Tipo di app (C/S o webservice)
- TCP e MQTT (con HTTP, non va bene per app in mobilità) o UDP e CoAP (adatto x IoT in mobilità)
- Client: definire sistema elaborazione, stringhe da trasmettere, terminatori, checksum o no, ...
- Server: db, servizi x localizzazione (Maps API) e misure per ostruzione GPS.
##### MQTT 
MQTT è un protocollo client/server di livello applicativo per lo scambio di messaggi. Usa TCP a livello trasporto (quindi *reliable* e *connection oriented*).
Si basa sul modello pub/sub, secondo cui degli MQTT publishers (client) pubblicano messaggi associati a dei topic (argomenti) verso degli MQTT broker (server); i quali, a loro volta, inoltrano i messaggi agli MQTT subscriber (client) inscritti ai relativi topic.
Con TCP e SSL/TLS è sicuro, reliable, con connessioni persistenti, con overhead basso e quindi usato per app real-time (latenza < 200 ms). Importante perché separa publisher da subscriber rendendo non necessarie sincronizzazioni di dati, tempi e luoghi/connessioni.
###### Esempio
Per esempio, per l'uso di sensori ambientali per monitorare e ridurre il rischio di incendio boschivo in una foresta remota. I sensori rilevano temperatura, umidita, gas e fuoco.
###### Quando?
- **Quando è richiesta una comunicazione *real-time***.
- **Quando è necessario un trasferimento efficiente**: in un'area remota, con connettività e risorse limitate, un trasferimento efficiente è fondamentale per risparmiare energia e ottimizzare la larghezza di banda (grazie a formato leggero di MQTT).
- **Quando basta una bassa velocità dei dati**: siccome è monitoraggio ambientale, i dati potrebbero non avere un alto volume; il che rende MQTT adatto grazie al suo *overhead* minimo e alle dimensioni ridotte.
- **Quando è necessaria l'affidabilità**: in un contesto critico (*mission critical*) tipo incendio boschivo, un trasferimento affidabile è essenziale; ed è garantito dai servizi di QoS di MQTT.
- **Quando è richiesto un trasferimento asincrono**: in aree remote, la connettività potrebbe essere intermittente; la natura asincrona di MQTT permette ai sensori di pubblicare dati e ai ricevitori di recuperarli quando la connettività c'è.
- **Quando è necessaria elevata scalabilità**: una foresta potrebbe avere molti sensori in vaste aree; il modello Pub/Sub di MQTT permette a nuovi sensori e ricevitori di pubblicare e ricevere dati.
##### CoAP
CoAP è un protocollo client/server di livello applicativo per lo scambio di messaggi. Usa UDP a livello trasporto (quindi *unreliable* e *connectionless*). Più adatto ad ambienti *constrained* (vincolati da poche risorse).
CoAP è REST e scambia messaggi con un modello basato su richieste e risposte x risorse identificate da URL, perciò i messaggi sono compatibili e traducibili (tramite dei proxy) da CoAP a HTTP e viceversa.
###### Esempio
Per esempio in un sistema domotico, dove vari dispositivi IoT devono comunicare con un gateway/server centrale. Il sistema necessita di bassa latenza, trasferimento veloce, basso consumo energetico e bassa velocità.
###### Quando?
- **Quando sono necessari bassa latenza e trasferimento veloce**: CoAP è progettato per app a bassa latenza e che richiedono trasferimenti veloci (per la sua leggerezza e le caratteristiche di UDP (*connectionless*...)).
- **Quando è necessario un basso consumo energetico**: molti dispositivi domotici sono a batteria, ma anche qui la leggerezza di CoAP e la comunicazione in UDP minimizzano il consumo energetico.
- **Quando si ha bassa velocità di trasferimento**: le app domotiche di solito trasmettono piccole quantità di dati (tipo letture di sensori). Per gli stessi motivi di prima CoAP ottimizza la larghezza di banda della rete.
##### HTTP
Non adatto ad app constrained per overhead, pull di grandi qtà di dati e solo unicast.
###### Esempio
Per esempio con un totem multimediale (tipo quelli al McDonald's). Per implementarli serve l'integrazione web, la logica di interazione uomo-macchina, una configurazione del firmware e il supporto agli aggiornamenti.
###### Quando?
- **Quando è richiesta l'integrazione web**: di base perché è il protocollo per eccellenza per la comunicazione in internet, ma nell'esempio specifico serve fornire al totem un collegamento ad internet per visualizzare dei contenuti e per permettere all'utilizzatore di mandare dati attraverso il totem ad un server.
- **Quando serve far interagire uomo e dispositivo**: siccome i totem hanno dei touchscreen per mostrare dati, questo rende possibile la visualizzazione di pagine web e l'interazione diretta con esse.
- **Per aggiornamenti e configurazione (firmware)**: semplicemente perché HTTP permette di aggiornare e configurare il totem da remoto.
- **Nei gateway IoT**: perché la comunicazione viene tradotta in MQTT/CoAP e viceversa.
##### VPN