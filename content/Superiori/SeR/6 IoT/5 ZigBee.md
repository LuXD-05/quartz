---
public: true
edited_seconds: 700
modified_at: 12/06/2024 11:12:21
---
### Cos'è?
Hint: cos'è è caratteristiche (5)
::
**ZigBee** è una specifica per <u>reti wireless</u> molto usata per far comunicare dispositivi <u>domotici</u> *smart*. Le reti ZigBee sono reti wireless apposite dove alcuni nodi wireless inoltrano i dati ad altri dispositivi. 
##### Caratteristiche
- Adotta lo standard livello fisico/datalink IEEE 802.15.4 con <u>frequenza 2,4GHz con 16 canali separati</u> e usa <u>CSMA/CA</u> per evitare le collisioni, ACK ad ogni *hop* e ACK *end-to-end*.
- **Topologia mesh**, la quale fornisce:
	- Portata estesa tramite multi-hop,
	- Formazione rete ad-hoc,
	- Rilevamento automatico del percorso + riparazione automatica in caso di guasto di un nodo.
- (Grazie alla rete a mesh) i dati di un nodo possono raggiungere qualsiasi altro nodo ZigBee indipendentemente dalla distanza purché ci siano dei nodi ripetitori che trasmettano il messaggio.
- Supporto **unicast, multicast e broadcast**.

### Componenti di una rete ZigBee
Hint: ZC, ZR, ZED
::
Le reti ZigBee prevedono 3 tipi di dispositivi: i ***coordinator***, i ***router*** e gli ***end-device***.
![](https://i.imgur.com/J6F3476.png)
##### ZigBee Coordinator
(O **ZC**) esegue il ***bootstrap*** della rete e, nel mentre, sceglie l'identificatore PAN e il canale radio fisico che verranno usati dalla rete; dopo questo però, si comporta come uno [[#ZigBee Router|ZR]] (caratteristiche identiche). Ce n'è 1 per rete e deve essere sempre attivo, quindi anche sempre collegato all'alimentazione (no batterie).
##### ZigBee Router
(O **ZR**) questi si collegano tra loro implementando una rete (mesh) tramite cui sono scambiati i pacchetti, e:
- Sono **sempre attivi** (quindi vanno anche sempre collegati all'alimentazione e non usano batterie),
- Fungono da **ripetitori** dei pacchetti,
- Sono responsabili di <u>scoprire le rotte</u> della rete e della creazione di una **tabella di routing** (le rotte sono create dinamicamente in base alla connettività di rete e, se le condizioni cambiano, queste si modificano).
(Esempi: lampadine, prese smart, interruttori...)
##### ZigBee End-Device
(O **ZED**) sono dei <u>dispositivi associati logicamente ad uno ZR</u> e, nonostante siano **spenti per la > parte del tempo** (quindi non in grado di ricevere il traffico inviatogli), si **attivano periodicamente** (o secondo una logica definita dal dev) per inviare richieste di polling allo ZR associato per farsi mandare i messaggi che questo salva in un buffer e invia on-demand (in un qualsiasi momento siccome è sempre attivo). Uno ZR può associare max 14 ZED.

### Quando e dove usare ZigBee?
Hint: recap caratteristiche ZigBee + ambiti di applicazione. Da sapere superficialmente.
::
(Rispetto a [[6.3 Long range#Quando e dove usare LoRaWAN?|quando e dove usare LoRaWAN]]), ZigBee è ideale per reti wireless in un'area localizzata e offre una connessione wireless affidabile, a bassa latenza e adatta al controllo *real-time*. Quindi:
- **Indoor**,
- **Distanze limitate** (10/100m),
- Frequenza ISM (senza licenza) 2.4GHz (interferisce con WiFi, cell e microonde),
- **Bassa velocità** (20-250kbps),
- **Basso carico** (70 byte),
- Topologia **mesh** (con coordinatore = alta affidabilità di rete),
- **Bassa latenza** (<200ms = adatto ad app *real-time*),
- Max 65000 nodi,
- Sicurezza AES-128,
- Scarsa capacità di penetrare i muri.
##### Applicazioni
Case e aziende smart (porte/finestre automatiche, telecomandi, luci, TV, frigoriferi, lavatrici, pc, condizionatori, sensori di fumo, acqua e perdite di gas, illuminazione, interruttori, dispositivi e applicazioni sanitarie, assistenza agli anziani con sensori poco appariscenti posizionati in casa per monitoraggio).