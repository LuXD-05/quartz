### La localizzazione

Nell'IoT, spesso è richiesta l'<u>individuazione in tempo reale</u> della <u>posizione di oggetti e persone</u> (sia all'**interno** che all'**esterno** di edifici).

###### Scopi

- Industriale (localizzazione di lavoratori),
- Logistico (localizzazione di operatori e mezzi)
- Controllo accessi (localizzazione di persone e permessi di accesso)
- Sanitario e assistenziale (localizzazione di operatori sanitari e pazienti)
- Eventi (localizzazione persone in spazi aperti)
- Sportivo (tracciamento movimenti e traiettorie degli atleti)

### Localizzazione outdoors

Per questa sono usati i <u>sistemi di posizionamento satellitare globale</u> **GNSS** (*Global Navigation Satellite System*).

##### GNSS

I sistemi GNSS sono dei sistemi di radionavigazione disponibili per navi, aerei e veicoli in moto; i quali sono detti ricevitori GNSS (anche se chiamati di norma GPS). Alcuni sistemi GNSS sono:

![](https://i.imgur.com/6IYEAIs.png)

###### Datum geodetico

Li differenzia il ***datum*** geodetico, ovvero il sistema  che permette di **georeferenziare** punti ed oggetti sulla terra, ovvero, esprimere la loro posizione sottoforma di **coordinate**.

La definizione di un *datum* si realizza effettuando delle **misurazioni** su dei **punti** a cui sono associate delle **coordinate** sulla superficie terrestre. Questa è detta **rete di inquadramento** e il sistema GPS usa quella mondiale **WGS 84** (17 stazioni). (Le misurazioni sono fatte periodicamente per aggiornare la rete).

![](https://i.imgur.com/Ac9mVJF.png)

Ugni GNSS usa un ***datum* diverso** e ciò comporta che le <u>coordinate di 1 punto cambino a seconda del sistema</u> (da centimetri a 1 metro di margine di errore). Un <u>ricevitore GNSS comune</u> che usa + costellazioni apporta delle "**correzioni**" per riportare il tutto in **WGS 84**.

#### GPS

###### Storia

Creato nel 1983 per scopi militari e di uso pubblico dagli anni '90 (tipo navigazione aero-marina e scopi civili), il **GPS** (*Global Positioning System*) è il sistema satellitare degli USA ed il suo nome completo è **NAVSTAR GPS** (*NAVigation Satellite Timing And Ranging* GPS).

###### Funzione

Il **GPS** consente di <u>individuare la posizione di un qualsiasi punto</u> sulla (o vicino alla) superficie terrestre. Detto ***globale*** dato che è valido per l'intero globo e usa un sistema di coordinate unico e valido in tutto il mondo (**WGS 84**) ma **non** in ambienti <u>interni</u>, <u>sottoterra</u> o <u>sott'acqua</u>.

###### Composizione

Esso consiste in una rete di:

- **24 satelliti artificiali** (+ <u>7 di riserva</u>),
- **5 stazioni di controllo a terra** lungo l'<u>equatore</u> e sempre in collegamento con i satelliti per mantenere <u>aggiornata la posizione esatta</u> e la <u>sincronizzazione dell'orologio atomico</u> di ogni satellite.

Un ricevitore GPS riceve dai satelliti il valore della **distanza** che li separa (grazie all'<u>orologio atomico</u> che calcola al <u>millesimo</u> il tempo tra richiesta e risposta).

![](https://i.imgur.com/Rn0709T.png)

###### Triangolazione e precisione

Viene determinata la posizione del ricevitore (espressa secondo <u>WGS 84</u> in **latitudine**, **longitudine** e **altitudine**) mediante una **triangolazione** (anche se serve un <u>4° satellite</u> per l'altitudine).

La **precisione** della triangolazione dipende da:

- <u>N° di satelliti agganciati</u>,
- **Qualità del segnale** (con <u>riflessioni/interferenze</u> o no)
- <u>Qualità</u> e <u>tecnologia</u> del **ricevitore GPS**.

(I GPS negli smartphone permettono una precisione intorno ai 2/3 metri, mentre i GPS professionali sotto al metro). 

La **ricezione** del **segnale GPS** avviene solo in **spazi aperti**, senza nulla che ostruisca la visibilità satellitare. 

![](https://i.imgur.com/wEej6lh.png)

Per questo (e per migliorare <u>precisione</u>, <u>affidabilità</u> e <u>integrità</u> del GPS) sono stati definiti degli ***augmentation systems***, sistemi che permettono di <u>combinare le info di navigazione</u> ottenute <u>dai vari satelliti</u>.

##### A-GPS

###### Problema

Uno dei problemi principali dei ricevitori GPS è il ***fixing*** (ovvero la **1a localizzazione**), in quanto (all'attivazione) i ricevitori devono ottenere la lista dei satelliti attualmente in vista per potervisi agganciare e calcolare la posizione; però questo è un processo dispendioso in termini di tempi e risorse, perciò si è ovviato con l'**A-GPS** (*Assisted GPS*).

###### Funzionamento

Per il ***fixing***, un ricevitore A-GPS si collega con la <u>rete cellulare</u> ad un ***assistance server*** (anche gestito dall'operatore stesso) a cui viene detto a quale **cella** l'utente è agganciato. (<u>Presupponendo che i satelliti che vede la cella sono gli stessi del ricevitore</u>) il server determina la **lista dei satelliti** in vista della **cella telefonica** e li <u>invia al ricevitore</u> GPS.

##### Applicazioni GPS

Quando si progetta un sistema di localizzazione GPS è necessario sviluppare un'app per elaborarne i dati; la quale riceverà le stringhe NMEA generate dal ricevitore.

NMEA (*National Marine Electronics Association*) è l'agenzia che definisce formato e contenuto di tali stringhe (codificate in ASCII) e ne esistono diverse, tipo:

--- start-multi-column: ID_hgod
```column-settings
Number of Columns: 2
Largest Column: standard
```

![](https://i.imgur.com/KX9oKjk.png)

--- column-break ---

![](https://i.imgur.com/Y7vl1PP.png)

--- end-multi-column

#### Galileo

Oltre a USA, URSS e Cina, anche l'UE ha il suo sistema satellitare: Galileo. Questo è ancora in fase di completamento, ma quando sarà completo con 30 satelliti (ora 26), fornirà servizi estremamente precisi in quanto è una tecnologia completamente civile (al contrario di GPS e GLONASS).

### Localizzazione indoors

Come già detto, il GPS non funziona sottoterra, con la pioggia, nei canyon urbani negli interni o sott'acqua (oltre a necessitare contatto visivo con satelliti). 

Tuttavia è possibile determinare la posizione in aree non coperte da GPS basandosi sulle ultime misurazioni o ricorrendo ad altre tecnologie.

##### Tecnologie

- **WiFi**: range 10/15m, accuratezza 1/7m, consumo alto (può essere usato in un'infrastruttura preesistente).
- **BLE Beacons**: range 3/5m, accuratezza 3/5m, consumo basso (richiede un'app). Possibile anche con **LoRaWAN + Beacons**.
- **VLC**: range 2/10m (area illuminabile), accuratezza stanza, consumo basso (può essere usata un'infrastruttura LED preesistente e richiede un'app).
- **RFID** passivi: range 3/5m, accuratezza 1/2m, consumo bassissimo.

#### Localizzazione con BLE

Si può usare **BLE** (standard BT > 4.0, stessa portata di BT tra 10/30m, consuma < energia, pareti e metallo limitano molto la ricezione ma non dispositivi elettrici o radio) per la **localizzazione *indoor***.

A questo scopo servono dei ***beacon*** (anch'essi basati sul principio <u>trasmettitore/ricevitore</u>) a <u>batteria</u> (da 2 a 8 anni) o <u>corrente</u>.

![](https://i.imgur.com/311SmFk.png)

##### Tecniche di localizzazione BLE

Per determinare la posizione di un oggetto (<u>3 beacon</u> per **2D** e <u>4 beacon</u> per **3D**), si usano 2 tecniche:

###### Trilaterazione

Sfrutta il concetto di "***Time of Arrival***", per cui la distanza tra trasmettitore e ricevitore è calcolabile in base al tempo intercorso tra invio e ricezione del segnale. Il ricevitore si trova quindi nell'intersezione di 3 circonferenze (con tempo = raggio).

###### Triangolazione

Sfrutta il principio di "***Angle of Arrival***" (solo per i client con 3 o + antenne). Confrontando i tempi di ricezione di uno segnale inviato ad almeno 3 antenne (ricezione), si può ottenere la direzione da cui esso è trasmesso. Con + trasmettitori, la posizione del client si ottiene misurando l'angolo con cui il segnale arriva.

##### Esempio

Esempio di uso (*indoors*/*outdoors*) della tecnologia:

![](https://i.imgur.com/9KVD3xO.png)

Si ha una griglia di antenne (collegate con **PoE**, *indoors* = a soffitto, *outdoors* = a pali) che rilevano la posizione dei tag BLE di oggetti/persone. Le antenne poi inviano la posizione di ogni tag a un server che elabora i dati e li integra eventualmente in un'app (con BT si localizza ogni cosa che lo abbia, non solo tag).

#### Localizzazione con VLC

###### Tecnologia 

La tecnologia VLC (*Visible Light Communication*) permette il trasferimento dei dati con la luce; ciò grazie alle lampadine LED (dispositivi a semiconduttore), con cui si possono trasmettere dati a velocità elevatissime, a bassi costi e ad alta affidabilità per la loro capacità di accendersi e spegnersi a velocità tali che l'occhio umano non riesce a percepire.

In questo modo si usano i LED sia per l'illuminazione sia per il trasferimento di dati binari, i quali vengono acquisiti da un ricevitore (smartphone con fotocamera) che ritrasforma la luce in un flusso di bit.

##### Fingerprinting

Si determina la posizione degli oggetti con il ***fingerprinting*** (eseguita in una fase offline in cui crea un db di info utili per la successiva fase online di posizionamento).

La tecnica sfrutta il concetto di ***Received Signal Strength*** (RSS), secondo cui la distanza tra trasmettitore e ricevitore è ottenibile misurando la potenza con cui è trasmesso il segnale e la potenza con cui esso arriva al ricevitore.

###### Funzionamento

Nell'ambiente in cui si opera, si definiscono dei ***reference points***, per ognuno dei quali si rilevano le potenze percepite da tutti gli ***access points***, generando così l'insieme di tutte le potenze (RSS) percepite associate al singolo *reference point*. I valori di ogni *reference point* vengono poi salvati in un db.

![](https://i.imgur.com/rILQk1k.png)

Questi valori verranno poi inviati a tutti i terminali, che li salveranno in db locali. Questi terminali devono eseguire un algoritmo che confronta le potenze ricevute con quelle nel db per trovare i *reference point* + "simili" e ottenere la loro posizione.

![](https://i.imgur.com/uRDpOFm.png)

###### Vantaggi

- Sicurezza per la salute (trasmissioni luminose),
- Non crea interferenze (tipo in ambienti delicati),
- Basso consumo energetico,
- Semplicità nella limitazione del segnale (schermando la luce),
- Non necessario hw aggiuntivo, solo infrastruttura LED.

###### Svantaggi

- La luce può essere tagliata di netto bloccando la trasmissione (è consigliabile che il percorso sia il + possibile privo di ostacoli),
- La luce può essere intercettata (serve crittografia per sicurezza),
- Il ***range*** è limitato (ok per *indoors* ma no per *outdoors*).

#### Localizzazione con RFID

Per questa serve un trasmettitore (tag RFID passivo) e un ricevitore. La distanza tra questi va da pochi cm a 1m; e la localizzazione è molto puntuale (comunque si può integrare questa tecnica con altre). Viene usato in settori di produzione e logistica per localizzare e identificare oggetti.

![](https://i.imgur.com/zrOifJC.png)

#### Localizzazione con LoRaWAN

La rete LoRa opera nella banda 868MHz (sub-1GHz) ed una ha latenza elevata (dai 30 secondi ai 5 min) che la rende inadatta ai sistemi di localizzazione *real-time*.

LoRaWAN può essere usata combinando tag LoRa/BLE e beacon BLE, questi ultimi che inviano dati ai tag LoRa/BLE, i quali li invieranno al backend tramite un gateway speciale. Questo è adatto per scenari con pochi oggetti ma tracciati su aree estese.

![](https://i.imgur.com/9PxdF3x.png)

### Localizzazione subacquea

La localizzazione subacquea si basa sul rilevamento di angoli e distanze di un trasmettitore e di un beacon (ricetrasmettitore) installato sull'oggetto. Quindi:

- Le **distanze** sono calcolate col tempo impiegato dal suono a percorrere la strada trasmettitore-beacon e ritorno.
- Gli **angoli** sono determinati con varie tecniche (generalmente prevedono 3 o + trasmettitori sul fondale o sull'oggetto) e a seconda del sistema usato, la posizione verrà calcolata o dal beacon o dai trasmettitori.

![](https://i.imgur.com/0w9ncrV.png)

### Applicazioni per localizzazione indoors

2 metodi:

##### Localizzazione basata su client

Il dispositivo esegue un'app avente un db locale delle posizioni (*fingerprint*) indicizzato tramite il valore del segnale (ricevuto da AP WiFi o beacon BLE). L'indicizzazione serve per recuperare la posizione corrente presalvata nel db (metodo adatto per la navigazione interna se si ha un'infrastruttura WiFi o beacon esistente).

##### Localizzazione basata su server

Un dispositivo WiFi, tag o beacon BT/BLE invia una chiave univoca (indirizzo MAC, UUID) al ricevitore che acquisisce i segnali e li trasmette a un server, il quale li userà per calcolare la posizione (metodo adatto per il monitoraggio di risorse e personale aziendali, tipo per notifiche antifurto di quando un'oggetto lascia una certa area).

### Applicazioni per localizzazione outdoors

Qui, servirà un sistema di elaborazione locale (che fungerà da gateway verso il server) e un server (locale *on the edge* o remoto *cloud*) che analizzerà i dati e gestirà le azioni conseguenti. Perciò bisogna definire delle cose in base al contesto.

##### Cosa definire

- Il tipo di applicazione: se fare un'app client/server o un webservice.
- Il protocollo: TCP o UDP,
	- Optando per qualcosa tipo HTTP (che usa TCP/TLS e non va bene per app in mobilità perché richiede una connessione stabile),
	- Usare qualcosa tipo CoAP (che usa UDP/DTLS e che è + adatto per IoT in mobilità).
- Lato client:
	- Identificatore del sistema di elaborazione locale (tipo Arduino),
	- Stringa da trasmettere (con info GPS necessarie dalla stringa NMEA),
	- Terminatore di stringa,
	- Checksum o nessun controllo,
	- La frequenza trasmissiva,
- Lato server:
	- Database,
	- I servizi applicativi da usare per la localizzazione (tipo Google Maps tramite le loro API),
	- Misure preventive (e aspettative non altissime) per i soliti limiti di ostruzione del GPS.
