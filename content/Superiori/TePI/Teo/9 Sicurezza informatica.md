# Sicurezza informatica

### Sicurezza delle reti

La **sicurezza** ha il compito di mantenere un sistema funzionante e operativo in ogni momento, garantendo l'accesso ai dati solo al personale autorizzato. Chi minaccia la sicurezza di un sistema è detto generalmente "***hacker***", termine spesso inteso in senso negativo. 

##### Tipi di hacker

- ***White hat*** (o *ethical hackers*), che vengono assunti dalle aziende per testare i loro sistemi e la loro difesa,
- ***Black hat*** (o *crackers*), hacker che compiono azioni illegali e penetrano nei sistemi approfittando delle loro vulnerabilità per un certo tornaconto (personale o meno),
- (***Grey hat***, una via di mezzo tra i precedenti).

### Risk management

Col tempo gli attacchi sono evoluti e incrementati, trovando dalla parte di chi subisce una generale impreparazione e mancanza di infrastrutture di sicurezza. Comunque, nonostante la sicurezza assoluta non esista, le aziende devono fare il possibile per difendersi; quindi si ricorre al ***risk management***.

La gestione del rischio è legata a: 1) la probabilità che un evento accada, e 2) al danno che ne deriverebbe; quindi questa, per la protezione di un sistema informatico, prevede un piano per valutare il rischio di attacchi e i danni che ne deriverebbero. Da ricordare poi è il grado di fiducia (*assurance*) che si è disposti a dare a qualcosa (tipo alla protezione di un firewall o a un software), per cui gli standard della famiglia ISO 27000 impongono criteri a cui attenersi.

### Il Cybersecurity Cube

All'inizio degli anni 90, <u>John McCumber</u>, allora grande esperto di sicurezza informatica, realizzò un modello (detto il "***Cybersecurity Cube***") in cui sono rappresentate graficamente le leve su cui agire per garantire cybersecurity. Questo cubo ha 3 dimensioni:

- <u>1° dimensione</u>: evidenzia i 3 <u>principi della sicurezza</u>: **Confidentiality** (Riservatezza), **Integrity** (Integrità) e **Availability** (Disponibilità).
- <u>2° dimensione</u>: si occupa della <u>protezione dei dati nelle loro fasi</u>: durante la **Trasmissione**, la **Memorizzazione** e l'**Elaborazione**.
- <u>3° dimensione</u>: si concentra sul <u>fattore umano</u> e su competenze/abilità per proteggere i dati: **padronanza delle tecnologie**, **capacità di definire linee guida** e pratiche di sicurezza e la **consapevolezza delle minacce** sempre dietro l'angolo.

(foto)

### Il triangolo CIA

Il triangolo CIA ha ai suoi vertici 3 elementi che rappresentano gli obiettivi della sicurezza informatica, ovvero:

##### Confidentiality (riservatezza)

Garantisce che i dati siano disponibili solo a chi è autorizzato, cosicché gli altri non possano intercettarli e manipolarli/usarli. Ciò è fatto con crittografia, auth, privilegi e controllo degli accessi.

##### Integrity (Integrità)

I dati, durante tutte le loro fasi e modalità d'uso, non devono essere alterati e devono essere riconducibili a un'origine certa (non ripudio, questo grazie a *checksum* e *hashing*).

##### Availability (Disponibilità)

Bisogna garantire che i dati siano sempre accessibili nonostante la situazione nei modi e tempi prestabiliti. Le minacce sono varie, ma per evitare problemi di indisponibilità si usano sistemi ridondanti e di backup + manutenzione e aggiornamento di hw e sw + piani di *disaster recovery*.

### Vulnerabilità

Questa è legata ai punti deboli di un sistema (quali pw debole, configurazioni sbagliate, errato controllo degli accessi...) che creano delle falle nella sicurezza (*security hole*) attraverso cui è facile attentare alla sicurezza dei dati. Questi:

- Da una parte potrebbero essere fonti di minacce che cercano di compiere azioni mirate al fine di compromettere le risorse,
- E dall'altra errori involontari o disastri naturali che danneggiano i dati o le infrastrutture.

Il MITRE fornisce un elenco di **vulnerabilità** (*Common Vulnerabilities and Exposures* - **CVE**) e di **debolezze** (*Common Weaknesses and Exposures* - **CWE**) sempre aggiornato.

##### Termini di cybersecurity

- **Asset**: insieme di beni necessari che vanno protetti,
- **Risk**: prodotto di probabilità che un evento dannoso si verifichi e il suo impatto,
- **Vulnerability**: è una debolezza interna e intrinseca di un sistema informatico (tipo CVE-2016-5195, le *race conditions* in Linux),
- **Weakness**: sono errori che possono condurre a vulnerabilità (tipo CVE-120, il *Classic Buffer Overflow*),
- **Threat**: le minacce sono eventi esterni a un sistema che violano qualche obiettivo di sicurezza (volontariamente o meno),
- **Exploit**: è il tentativo di sfruttare una vulnerabilità,
- **Attack**: attività volontaria svolta da un hacker che concretizza una minaccia sfruttando una vulnerabilità. Divisi in:
	- Passivi: rubano info riservate spiando il traffico e non compiendo azioni dirette, tipo *sniffing* o *port scanning*,
	- Attivi: prevedono azioni intenzionali, come alterazioni di messaggi o attacchi DoS (*Denial of Service*).
- **Contromisure**: azioni e processi che permettono di ridurre o eliminare le vulnerabilità.

##### Minacce

- Fisiche: sono tutti i possibili malfunzionamenti verificabili nei dispositivi + eventi naturali distruttivi,
- Di rete: sono i malfunzionamenti della rete (danni a cavi, nodi non auth in rete, danni a router e switch, assenza di crittografia, *sniffing*...),
- Al sw di sistema (OS e DBMS): sono eventuali carenze nella gestione della sicurezza dell'OS (errori di periferiche, dischi o memoria) che possono danneggiare anche i DBMS e interrompere il servizio,
- Di fattore umano: ovvero rischi legati all'intervento umano sul sistema; è il livello + critico per l'imprevedibilità del comportamento delle persone, sia intenzionali che non.

###### Dove colpisce un attacco

Anni fa gli attacchi sfruttavano le debolezze dei dispositivi (USB, dischi, Wi-Fi non protette...) e le aziende si difendevano come potevano con firewall e DMZ. Oggi la situa è cambiata per l'aumento di rischi e minacce, soprattutto per l'IoT.

### Tipi di attacchi

Gli attacchi informatici si classificano in 2 (3) categorie:

##### Malware (e keylogger)

I *malware* sono programmi malevoli con varie funzioni pericolose; ci si protegge da essi con antimalware e antivirus. Si distinguono in:

- **Virus**: si agganciano a programmi esistenti variandone la dimensione e si caricano in memoria centrale dove stanno residenti per poi infettare altri programmi e file con cui si diffondono. 
- **Worm**: programmi autonomi che sfruttano bug di programmazione e usano l'OS della macchina per eseguiti (o anche l'utente li esegue).
- **Trojan**: sw che si spacciano per programmi utili ma che nascondono altre intenzioni, come alterare dati e programmi e sono spesso scaricati inconsapevolmente perché contenuti in giochi, applicazioni non attendibili...
- **Ransomware** (o CryptoLocker): infettano i sistemi, ne crittografano i contenuti e richiedono un pagamento per decrittarli.
- **Keylogger**: sono programmi molto leggeri che registrano ciò che l'utente scrive sulla tastiera passando inosservati; quindi rendono semplice il furto di password e dati sensibili. Sono di 2 tipi:
	- Hardware: questi si collegano al cavo della tastiera intercettando ciò che passa,
	- Software: questi sono installati di nascosto nel pc.

##### Attività di hacking

- **Spyware**: sw che raccolgono in segreto info sugli utenti tramite internet, per scopi pubblicitari.
- **Adware**: sw integrati in programmi gratuiti che inseriscono annunci pubblicitari in essi. talvolta fungono anche da spywares.
- **Phishing**: consiste nell'invio di email fraudolente a utenti, spacciandosi per banche o enti, cercando di truffarli o rubargli l'identità (vittima clicca link e mandata su un sito clone dove mette info personali).
- **Backdoor**: sono installate da malware su OS, app e servizi, e aprono una "porta" per accedervi da remoto o raccoglierne i dati (anche per usi leciti di debug).
- **Spam**: sono email non richieste con materiale pubblicitario e link pericolosi, spesso sgrammaticate.
- **SQL injection**: consiste nello sfruttare errori di programmazione e la superficialità dei dev nel controllo dei dati immessi nelle app (soprattutto tramite campi input di form web). Senza controllo, qualunque cosa ci sia scritta nel campo è iniettata nel db e con certi parametri può anche permettere di visualizzare l'intero db.
- **Man in the Middle** (MITM): è un attacco basato sullo spionaggio che prevede un *middleman* che si pone tra mittente e destinatario di una conversazione e che ne intercetta i dati, eventualmente alterandoli.
- **Zero-day exploit**: è un attacco che si basa sulla rapidità di attacco da quando si scopre una vulnerabilità, sperando che la vittima non abbia ancora aggiornato (o avuto il tempo di aggiornare) il sistema.
- **Denial of Service (DoS)**: è un attacco di *brute force* che sovraccarica un server inondandolo di richieste e impedendogli di rispondere a quelle legittime. Se tanti pc sferrano un'attacco coordinato, allora si parla di DDoS (Distributed DoS).
- **Ping of death**: si invia una serie ripetitiva di ping di dimensioni + grandi del max previsto bloccando l'host ricevente.
- **Mail bomb**: si invia una grande quantità di email di grosse dimensioni così da affossare il mail server e impedire agli utenti l'accesso al servizio.
- Attacchi TCP/IP:
	- **IP spoofing**: si altera il valore del campo "Source Address" di IP per far credere che il pacchetto sia stato inviato da un host attendibile.
	- **Hijacking**: modifica gli header TCP e IP dirottando l'utente su un sito pirata.
	- **Port scanning**: sono inviati dei messaggi che sondano (*probing*) e trovano i servizi associati alle porte well-known.
- **SYN flood**: qui un client ostile inonda un server di pacchetti TCP con il flag SYN attivo e IP falsi, facendo rispondere con SYN/ACK e quindi allocare risorse al server, però non rispondendo con il pacchetto ACK; quindi non si completa il 3-way handshake e le comunicazioni rimangono aperte fino alla paralisi del server.
- **Social engineering**: è la capacità di spacciarsi per ciò che non si è, convincendo e manovrando gli altri per estrapolare loro info riservate (per contrastarla servono precauzioni: non dare pw, chiedere tessere e id...).
- **Advanced Persistent Threats** (APT): è un tipo di attacco complesso e mirato il cui scopo è introdursi nei sistemi per rimanervi e strappare le informazioni senza che la vittima ne sia consapevole. Questi attacchi sfruttano l'ingegneria sociale al massimo per penetrare nei sistemi e aprirvi delle backdoor così da rimanere in essi il + possibile e controllarli.

### Input vulnerabilities

L'input utente è spesso ciò che viene usato per sfruttare vulnerabilità di sistemi; alcuni esempi sono:

##### Buffer overflow

Questo è una debolezza che è legato alla gestione della memoria e si riscontra quando in un programma si tenta di scrivere oltre la dimensione del buffer (tipo quando eccedi i limiti di un array) andando a scrivere nelle aree di memoria adiacenti e provocando danni devastanti.

##### SQL injection

Come già detto, con la SQL injection si rischia di poter ottenere l'intero db; basta infatti inserire "OR 1 = 1" in un campo username di un form e la query, se non parametrizzata, verrà eseguita nel db ritornando tutti gli utenti in quanto la condizione è sempre vera per ogni riga. Per proteggersi è necessario parametrizzare le query o fare diversi controlli sui dati inseriti.

##### OS command injection

Bisogna prestare attenzione anche alle applicazioni che eseguono dei file per esempio ".sh", che eseguono delle istruzioni di OS e che se intercettati, potrebbero venir alterati e far eseguire codice fraudolento con privilegi.

##### Cross-site scripting (XSS)

Queste vulnerabilità permettono a hacker di inserire script dannosi in siti e app, per inserire malware nei browser e raccogliere info.

### Strumenti di monitoraggio e attacco

Wireshark, shodan, ping sweep, port scan, NMAP e ZENMAP.

### Progettare la sicurezza

Il problema della **sicurezza** va affrontato a livello **manageriale** definendo un piano con politiche di sicurezza non solo **tecniche** (tipo antivirus e crittografia) ma anche **organizzative** (se impiegati scrivono pw su foglietti e li lasciano in giro cosa si fa?). Serve quindi un metodo preciso e strutturato, che è rappresentato in un documento che definisce quali sono i problemi e come risolverli (+ why piano, parti coinvolte, comportamenti, metodi auth, storico e come gestire attacchi).

#### Politiche di sicurezza

- **Plan**: (identifica/analizza problema + pianifica azioni correttive),
- **Do**: (si attuano le azioni + si attivano test),
- **Check**: (si verificano risultati confrontandoli con aspettative),
- **Act**: (rileva/controlla risultati buoni + add fattori correttivi x migliorare).

#### Analisi dei rischi

Per identificare la chance di incidenti o attacchi, un'azienda analizza il rischio concentrandosi sulle **probabilità che l'evento accada** e sul **danno che ne deriverebbe**. Per questo occorre:

- Stimare il valore degli asset e le loro vulnerabilità,
- Considerare minacce intenzionali/accidentali e interne/esterne assegnando loro un grado d'importanza.

Mettendo in relazione la probabilità di incidente e il relativo danno, si ottiene un grafico con una curva che discrimina il rischio accettabile da quello che non lo è.

(foto)

##### Modalità di approccio del rischio

Il ***risk management*** presuppone **5 modalità** di approccio del rischio, sancendo che esso può essere:

- **Evitato**: non attuando l'attività o delegando il servizio a esterni (*outsourcing*), (per rischio inevitabile, ridurne l'impatto con *disaster recovery*),
- **Accettato**: se il rischio è sostenibile,
- **Mitigato**: riducendone l'impatto (tipo con firewall e regole di accesso),
- **Affrontato**: preparandosi a fronteggiarlo con delle contromisure (tipo backup),
- **Trasferito**: delegando ad altri soggetti l'attivitò.

### Standard

I dati sensibili sono 1 dei maggiori fattori di rischio per le aziende poiché soggetti ad attacchi e incidenti. La famiglia di standard **ISO 27000** (46 standard) definisce delle norme per migliorare la sicurezza dei dati aziendali. Comprende:

- **ISO 27001**: avente i requisiti di implementazione per un ISMS (*Information Security Management System*),
- **ISO 27002**: discute i controlli di sicurezza attuabili dalle aziende per implementare la valutazione del rischio,
- **ISO 27017 e 27018**: con regole per la protezione di dati sensibili nel cloud e online,
- **ISO 27701**: copre il PIMS (*Privacy Security Management System*).

### GDPR

Il **GDPR** (o *General Data Protection Regulation*) è in funzione dal **2018** in tutti gli stati UE e contiene diverse novità, in particolare si rivolge alle imprese che trattano i dati di cittadini europei sia che siano nell'UE sia che siano estere.

