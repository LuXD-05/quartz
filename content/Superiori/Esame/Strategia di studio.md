---
edited_seconds: 6590
modified_at: 29/04/2024 16:47:57
---
### Raccolta prove
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_Ollari-Tema_Esame_2004.pdf
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_Ollari-Tema_Esame_2006.pdf
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_Ollari-Tema_Esame_2008.pdf
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_Ollari-Tema_Esame_2011.pdf
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_Ollari-Tema_Esame_2012.pdf
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_Svolgimento_Sistemi_2013-2014.pdf
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_SistemieReti_SecondaProva_Esame_di_Stato_AS2015-2016.pdf
- https://online.scuola.zanichelli.it/provatecnici-files/Reti/Zanichelli_SistemieReti_Esame2018_Ollari.pdf

### Buone pratiche
- TRACCE NON SEMPRE UNIVOCAMENTE INTERPRETABILI: formulare ipotesi **ragionevoli** (<u>né troppo limitate né troppo complesse</u>), **realistiche** e **specifiche**, al fine di comprendere e circoscrivere il tema proposto.
- PAGINE WEB NON TROPPO COMPLESSE: il codice della pagina web deve dare dei casi o un esempio generale che dimostrino la competenza raggiunta senza spaziare troppo nel dettaglio.

### Struttura prove
Generalmente le prove sono composte da:
##### Parte 1
###### Traccia
Nella traccia è presentata la realtà d'interesse e, implicitamente, alcune richieste e necessità. Identificare e distinguere bene, tra le richieste poste, quali siano:
- Richieste generali: cose da gestire o chiarire con ipotesi aggiuntive o nel testo della prova.
- Richieste specifiche: necessità relative ad un certo ambito che possono sia essere da discutere, sia dover essere un punto a sé stante della relazione.
###### Vincoli
Dopo la traccia sono esposti esplicitamente dei vincoli da considerare durante lo sviluppo del tema.
###### Richieste
Infine, sono fatte delle richieste nelle quali è specificato su quali punti bisognerà concentrarsi maggiormente durante lo svolgimento della prova; queste possono riguardare lo sviluppo della rete, la progettazione di una base di dati, delle specifiche di app o siti web...
##### Parte 2
Nella 2a parte invece sono semplicemente riportati 4 quesiti tra i quali solo 2 dovranno essere scelti per essere sviluppati e risolti.
Questi potrebbero prevedere delle estensioni di funzionalità già previste nelle richieste oppure delle aggiunte completamente nuove (tipo implementazioni di VPN o protezione accessi DBMS con `GRANT` e `REVOKE`...).

### Strategia
#### Applicazione test
##### Richieste dalla traccia (implicite)
<u>POI</u> monumentali (chiese, luoghi storici...) e artistici (musei, mostre...) distribuiti.
Erogazione contenuti con 2 <u>pagine web</u>:
- **Pagina multimediale base** con:
	- Breve video presentativo del POI (1 min) solo in ita (sub-eng),
	- Max 3 immagini del POI (architettura, quadri...) con didascalia in ita e in ing.
- **Pagina multimediale avanzata** con:
	- Video presentativo approfondito del POI (5 min) in 7 possibili lingue compreso italiano,
	- Una galleria con circa 20 immagini con descrizione (circa 500 char) in 7 lingue tra cui l'italiano.
<u>InfoPoint</u> (distribuiti/dislocati) in città vendono il servizio ai turisti.
Turisti comprano <u>biglietti</u> (= servizio) con 3 tariffe:
- "base": fruizione pagina base di ogni POI
- "intermedia": fruizione pagine avanzate per 3 POI e di tutte le base
- "piena": fruizione di tutto per ogni POI.
Ogni biglietto ha una <u>pw</u> di accesso (univoca x turista) associata alla tariffa e con validità giornaliera.
##### Richieste dalla traccia (esplicite)
- Navigazione pagine solo ai minitablet forniti col biglietto, dopo consegnato carta d'identità o n° di carta di credito validi.
- Dati vanno salvati su server (non su minitablet) per facilitare update periodico
- Accesso alle pagine possibile solo dopo l'inserimento (a inizio visita???) della pw nel biglietto.
- Accesso alle pagine di un POI possibile solo in prossimità o all'interno del POI stesso.
- Restituzione minitablet va fatta nell'InfoPoint dove lasciata la carta d'identità o in uno qualsiasi se lasciato il n° di carta di credito.
##### Richieste da sviluppare 1
- Progetto dell'infrastruttura tecnologica/informatica (anche grafico) per gestire il servizio nel complesso, con:
	- Architettura di rete, server e luoghi in cui installare questi,
	- Modalità di comunicazione tra server e host (con protocolli e servizi sw per gestire rete e pagine),
	- Elementi di infrastruttura utili alla fruizione dei contenuti solo nei pressi di POI a cui si riferiscono.
- Progettazione database (ER e modello logico),
- Progettazione pagine web (in particolare x clienti con biglietto tariffa base la fruizione dei contenuti del POI in cui si trova) codificandone una porzione significativa,
- Analisi di massima della gestione delle 3 fasce tariffarie, delle opzioni offerte per la scelta dei 3 POI di tariffa intermedia e scelta della lingua per tariffe intermedia e piena.
##### Richieste da sviluppare 2
- Possibilità di votare un POI (integrazione db + pagina per visualizzazione dei voti per ogni POI),
- Possibilità di allargare la fruizione di contenuti ai dispositivi personali degli utenti in particolare:
	- Individuando soluzioni (come fatto per i minitablet) per consentire l'accesso solo nei pressi dei POI.
	- Permettendo la fruizione al dispositivo sempre nei limiti imposti della tariffa associata e con autenticazione con pw del biglietto.
- Gestire meglio la sicurezza (con GRANT e REVOKE in DBMS) per la gestione dei db analoga a come studenti non possono modificare voti ma docenti si in un sistema scolastico.
- Approfondire il discorso VPN per l'accesso a sedi dislocate e remote (con esempi con azienda con 2 sedi e con agenti commerciali che devono accedere ma da remoto perché si spostano).

##### Trasmutazione richieste in requisiti
Città media = max 200 visitatori al giorno
Monumento/opera/museo... = in base a grandezza edificio gestire subnet


#### Strategia free
##### Intro
0) Lettura della traccia.
1) Sottolineare informazioni e cose importanti nella traccia.
2) Nel mentre che si rilegge, ogni qualvolta si arriva incontro ad una richiesta o obiettivo, scriverli.
3) Quando si ha terminato con l'identificazione delle richieste, individuare quelle ambigue e circoscriverle formulando ipotesi aggiuntive.
4) Eventualmente, scrivere brevemente dopo una richiesta (o dopo tutte) una soluzione in qualche parola oppure qualche spunto da scrivere in seguito (matita? lasciare cmq un po' di spazio).
##### Requisiti
A questo punto, è possibile definire i requisiti per ogni richiesta pensando a cosa sia necessario per compierla. Bisogna suddividerli però in categorie:
###### Rete e infrastruttura
- **Dimensionamento** (n° nodi/host necessari)
- **Subnetting** (IP/subnet di base o da usare (in base a quanti host)? FLSM o VLSM (+ prob VLSM)? ip statici o DHCP? eventuali VLAN?)
- Connessione a internet (NAT? proxy/firewall software? config router? IPv6 o IPv4?)
- **Topologia** (quale è la migliore per gestire l'infrastruttura esposta?)
- **Tipologia** (che tipologia usare? in base alla distanza richiesta? in base alla configurazione di rete presentata? in base ai vincoli? quale meglio? (LAN, WAN...))
- **Geografia**/posizionamento dispositivi/aree (in base alla geografia esposta, ai vincoli esposti o a propria discrezione) + <u>wired</u> (Ethernet, fibra...) o <u>wireless</u> (WiFi, BT/BLE, ZigBee, LoRaWAN)
- **Dispositivi** (tipi di host/client, router, switch, sensori/attuatori IoT, server, firewall, gruppi di continuità impianti di climatizzazione, storage, ridondanza...)
- **Cablaggio** (quanto ne serve in base a distanza? tipo di mezzi trasmissivi? punti di accesso ai servizi (corrente, internet...)?)
###### Dati, comunicazione e protocolli
- Tipo di traffico (se pesante tipo video o leggero tipo dati IoT)
- Larghezza di banda e velocità necessarie (se serve veloce per criticità oppure se con + o - latenza non c'è differenza (real time o no))
- Affidabilità (se connection oriented o connectionless),
- (in generale) Protocolli (che protocollo usare per ... ? Perché? Vantaggi e svantaggi?)
###### Costi e tempi
- Costi (dispositivi, lavori... rientrano in budget? (se non c'è va proposto uno adatto))
- Tempo previsto (con che soluzione è possibile realizzare il sistema rimanendo entro un tempo ragionevole?)
- Considerazioni per il futuro (???)
###### Pagamenti
- Pagamento (necessario predisporne uno per gli utenti? se si come?)
###### Legalità e permessi
- Permessi (servono permessi specifici per fare ... ?)
- Bandi (sono necessari bandi e/o concorsi pubblici?)
- Normative o standard (ci sono " o " da rispettare (tipo cookie e GDPR o qualche RFC)? il progetto rispetta tali norme e standard?)
###### Privacy e security (logica)
- Sicurezza di dati (necessaria crittografia? se si quando? con che protocolli (HTTPS, SSL, SSH, certificati, crittografia...)?)
- Controllo degli accessi (serve una DMZ? quali servizi vanno protetti e messi al suo interno?)
- Autenticazione (necessari meccanismi di auth? come si gestiscono e quali vincoli devono rispettare?)
- Permessi (controllo se l'utente ha i permessi specifici per fare certe azioni...)
- Protezione da malware e attacchi (setuppati firewall/IPS/IDS? setuppati antivirus? protezione da SQL injection?)
- Accesso da remoto (necessario accesso da remoto? come gestirlo in sicurezza con VPN o altro?)
###### Privacy e security (fisica)
- Sicurezza fisica (server/storage o dispositivi IoT sono protetti fisicamente (eventi naturali o azioni umane)? --> perciò predisporre videocamere IP, sensori di movimento, antifurti e geolocalizzatori)
- Ridondanza e high availability (predisposti sistemi in RAID? duplicazione sistemi critici? collegamenti ad internet multipli? ISP diversi?)
- Backup (gestione backup?????)
###### Persone
- Formazione e *know-how* (serve predisporre materiali per formazione?)
- 
###### Altro
- Scalabilità nel tempo (cosa fare per rendere la struttura facilmente scalabile nel tempo?)
- Logging (???)
- Servizi ulteriori (necessari altri servizi tipo mail, stampa, FTP, NAS repo...?)
- Server/cloud (on-premise o outsourced)
- Tipo di app (web? nativa? multiplatform? tutto x IoT)
- Virtualizzazione (necessaria? se si, impiego?)

### Lista competenze
##### Rete
- Dispositivi base cisco (host, switch, router, cavi...)
- Dispositivi IoT (sensori, attuatori...)
- 
##### Protocolli
###### Fisico

###### Datalink

###### Rete

###### Trasporto

###### Applicativo

##### Sicurezza
- Crittografia
- VPN (site-to-site, SSL, remote access, personal...)
- Firewall/IPS/IDS
- DMZ (logicamente)
##### Altro


### Altro
Video 1
https://youtu.be/B-irxoFGJGo
Video 2
https://youtu.be/mfzGor5B1q0
Video 3
https://youtu.be/h7T561hz2TI
Video 4
https://youtu.be/sJYNFSwkVKw
Video 5
https://youtu.be/cDnenOV1rFs
