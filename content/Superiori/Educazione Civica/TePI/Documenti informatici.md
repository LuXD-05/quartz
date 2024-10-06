---
public: true
modified_at: 08/05/2024 18:02:48
edited_seconds: 7130
---
# Introduzione

### Le linee guida AgID
Hint: cosa sono, scopi (2), soggetti interessati (4) 
::
Le "*Linee guida sulla formazione, gestione e conservazione dei documenti informatici*" di **AgID** (*Agenzia Italia Digitale*) regolano <u>formazione, gestione e conservazione</u> del <u>patrimonio documentario aziendale</u>.
##### Scopo
Le "Linee guida" hanno 2 scopi:
1) **Aggiornare le regole** che riguardano <u>la formazione, la protocollazione, la gestione e la conservazione dei documenti informatici</u>,
2) Definire un'**unica normativa** per tutte le regole e le circolari riguardanti gli ambiti sopracitati.
##### Soggetti interessati
Le "Linee guida" sono destinate a:
- **PA** (*pubbliche amministrazioni*),
- **Enti pubblici**,
- **Società pubbliche**,
- **Privati** (alcune parti).

### Principi generali di gestione documentale
Hint: 
::
La gestione documentale si divide in: formazione, gestione e conservazione.

Si distinguono 3 tipi di archivi (in base all'organizzazione e uso dei documenti):
- **Corrente**: contenente i documenti delle attività in corso, 
- **Di deposito**, contenente i documenti ancora utili per fini amministrativo-giuridici ma non indispensabili per le attività in corso,
- **Storico**: contenente i documenti storici che vanno conservati permanentemente.

Nella fase di formazione dei documenti informatici, sono essenziali obiettivi di qualità, efficienza e regolamentazione. Per tali servono manuali di gestione documentale, workflow documentali e sistemi di gestione dei documenti automatizzati e interoperabili sul web. 
Questi vanno costantemente aggiornati. Infine, la pubblicazione dei manuali di gestione documentale e di conservazione sui siti istituzionali rappresenta un obbligo per la Pubblica Amministrazione, conforme alle disposizioni normative in materia.

Gli articoli 68 e 69 del CAD sanciscono che:
- Programmi e sistemi di gestione delle PA devono essere riusabili, automatizzati ed interoperabili,
- Le PA che forniscono applicativi devono anche fornire il codice sorgente completo di documentazione gratuitamente e in licenza aperta.

# Formazione dei documenti

### Documento informatico
Hint: cos'è, caratteristiche (), 
::
##### Cos'è
> [!important] Documento informatico
> Rappresentazione <u>informatica</u> di un qualsiasi contenuto rilevante (tipo testo, audio e video).
##### Caratteristiche
###### Identificazione
I documenti informatici devono essere **identificati univocamente**. Per le PA l'identificazione si esegue:
- Associando al documento la <u>segnatura di protocollo univoca</u>,
- (Eventualmente) mediante associazione al documento di una <u>impronta crittografica basata su funzioni di</u> ***hash*** <u>sicure</u>.
###### Immodificabilità
Un documento informatico è **immodificabile** (involontariamente o senza autorizzazioni) una volta creato e salvato in <u>forma digitale</u>, garantendone <u>integrità e affidabilità</u>.
L'<u>immodificabilità</u> è garantita da:
- Apposizione di <u>firma elettronica qualificata</u> e/o <u>firma digitale</u>,
- Memorizzazione regolata da misure di sicurezza,
- Trasferimento a terzi in modo sicuro, tipo tramite **PEC**...
###### Memorizzazione
I documenti informatici devono essere **conservati** in un <u>sistema di archiviazione e gestione</u> (anche delegabile a terzi) che si attenga a <u>procedure e standard di sicurezza</u> specifici.
###### Riferimento temporale
Ogni documento informatico immodificabile deve avere associato un **riferimento temporale** (una <u>data</u>).
###### Metadati
Alla formazione del documento informatico immodificabile, devono essere generati e associati permanentemente ad esso i relativi **metadati**.
#### Formazione del documento informatico
Un documento informatico può essere formato con i seguenti modi:
1) Redazione del documento con sw appositi,
2) Acquisizione del documento informatico stesso / della copia informatica di un documento analogico / della copia di un documento analogico per immagine,
3) Memorizzazione informatica di dati da transazioni/processi/moduli,
4) Generazione e raggruppamento di dati e registrazioni da 1 o + db.

### Copie di documenti
Hint: 
::
##### Copie per immagine
Si può fare una copia (informatica) un documento (analogico) tramite una sua immagine. Serve accertarsi che questa sia identica all'originale analogico (soprattutto se si fanno tante copie spesso).
###### Certificazione di processo
A tal fine si può usufruire della "**certificazione di processo**", cioè la certificazione di una copia per mezzo di sistemi certificati che la certifichi.
###### Altre certificazioni
La certificazione di una copia è possibile (in più) mediante l'apposizione di **firma digitale**. Eventualmente è possibile apporre la firma su un <u>documento diverso che però attesti l'autenticità e la validità della copia</u>.
##### Copie con formato diverso ed estratti
###### Problema
C'è un problema quando le copie presentano un'"**evidenza informatica**" (<u>modalità di rappresentazione digitale delle info</u>) differente, ovvero con:
- **Copie** del documento **a cui** è stato **cambiato il formato** (tipo da ".pdf" a ".docx"),
- **Estratti** di un documento (anche con formato identico).
###### Validità
Le **copie** hanno il <u>medesimo valore legale</u> del documento originale **solo se** la loro conformità non è contestata; per ciò si usano 2 metodi:
- <u>Confronto diretto con l'originale</u>,
- Ottenimento di una <u>certificazione di processo</u>.

# Gestione dei documenti

### Registrazione dei documenti
Hint: 
::
##### Registrazione
La registrazione informatica di un documento corrisponde all'insieme di dati associati allo stesso per identificarlo univocamente. Divisa in 2 parti (effettuate contemporaneamente):
###### Registrazione di protocollo
> [!important] Registrazione di protocollo
> L'**insieme di metadati** che il <u>registro di protocollo</u> (libro in cui memorizzati dati di documenti ricevuti/inviati) deve memorizzare per tutti i documenti <u>in uscita e in entrata</u> delle PA, al fine di <u>tracciarli</u> ed <u>identificarli tutti univocamente</u>.
###### Segnatura di protocollo
> [!important] Segnatura di protocollo
> L'**associazione** ai documenti informatici, in modo <u>immodificabile e permanente</u>, delle **info** <u>riguardanti i documenti stessi</u>. Questa è ciò che ne permette l'<u>identificazione univoca</u>.
##### Annullamento
Il protocollo informatico deve garantire che ogni operazione (anche quelle di annullamento), sia tracciata e archiviata nel sistema, in particolare:
- Info di <u>oggetto</u>, <u>mittente</u> e <u>destinatario</u> di una registrazione possono <u>solo</u> essere **annullate**,
- Le <u>uniche info</u> **modificabili** di una registrazione sono quelle <u>interne</u> e relative ad <u>assegnazione e classificazione</u>,
- Il sistema deve tracciare non solo le info **modificate**, ma anche quelle **annullate**.
##### Sicurezza
Per quanto concerne la **sicurezza**, il sistema di protocollo deve garantire:
- **Autenticazione** degli <u>utenti</u>,
- **Controllo degli accessi** (<u>solo a risorse per cui si è abilitati</u>),
- **Tracciamento** di <u>ogni azione di modifica e del suo autore</u>.

### Classificazione dei documenti
Hint: 
::
##### La classificazione
Con la classificazione si organizzano (logicamente) i documenti informatici di un ente. Essa si basa su un piano di classificazione, che definisce le categorie di documenti + un'unica modalità per organizzarli.
##### Aggregazioni documentali informatiche
Le PA gestiscono i loro documenti informatici aggregandoli, ci sono diversi tipi di aggregazione:
###### Fascicoli informatici
Sono delle **aggregazioni digitali di documenti** che appartengono allo <u>stesso argomento o attività</u>.
###### Serie
Le PA gestiscono anche aggregazioni diverse dai fascicoli, le **serie di aggregazione**. Queste sono:
- **Serie documentarie**: costituite da **documenti singoli** accorpati in base al tipo,
- **Serie di fascicoli**: costituite da **fascicoli** accorpati in base al tipo.
I fascicoli appartenenti a <u>serie diverse</u> possono essere <u>collegati tra loro</u>.
###### Registri e repertori informatici
I registri (tipo quello di protocollo) e i repertori sono anch'essi forme di aggregazione delle info. Questi, però, non sono compilati a mano, ma sono riempiti automaticamente dal sistema informatico (che prende dati da vari db e li organizza secondo una struttura logica predefinita).

### Compiti del responsabile di gestione documentale
Hint: 
::
##### Intro
Nelle PA, il **responsabile della gestione documentale** è incaricato di gestire tutto ciò che riguarda i documenti dell'ente nel rispetto delle relative normative. 
###### Compiti
Oltre ai suoi compiti principali (registrazione, organizzazione ed archiviazione di documenti) il responsabile della gestione documentale deve:
- **Gestire ed autorizzare accessi e operazioni** (decide chi può visualizzare, inserire o modificare documenti),
- **Conservare i documenti in sicurezza** (si occupa dei registri di protocollo, della conservazione dei documenti e della loro sicurezza),
- **Gestire le emergenze** (si assicura di ripristinare il + velocemente possibile le funzionalità del sistema in caso di guasti o malfunzionamenti),
- **Monitorare** (controlla il rispetto delle regole del personale e delle operazioni).

### Manuale di gestione documentale
Hint: 
::
##### Intro
Il responsabile della gestione documentale deve redigere un **manuale** che regoli gestione, trasmissione e accesso ai documenti informatici nel basato su normative e sul manuale di conservazione (deve anche includere un piano per la sicurezza informatica).
Ogni PA deve pubblicare il proprio manuale sul proprio sito web.
###### Contenuto
Il contenuto del manuale comprende aspetti riguardanti:
- **Organizzazione**: come creare, registrare, assegnare, condividere e archiviare documenti informatici.
- **Formato dei documenti**: quali tipi di file (estensioni) da usare per i documenti, come valutarne la compatibilità e come convertirli.
- **Protocollo informatico**: come registrare le informazioni, dei documenti, modificate ed annullate.
- **Classificazione**: come classificare i documenti e in base a cosa.
- **Aggregazioni**: le regole di aggregazione dei vari documenti.
- ***Workflow***: il flusso di lavoro interno alle PA per gestire i documenti.
- **Archiviazione**: la struttura dell'archivio per garantire attività chiare e trasparenti.
- **Sicurezza dei dati personali**: le misure per proteggere i dati e garantirne la sicurezza.
- **Conservazione**: per quanto i documenti vanno conservati prima di archiviarli o eliminarli.

### Formati
Hint: 
::
Le linee guida stabiliscono i **formati** da utilizzare per i documenti informatici (elencano quelli "buoni" perché <u>aperti, standard e leggibili</u> da diversi tipi di sistemi); e le <u>PA devono usarli sempre</u> (salvo in <u>casi specifici eccezionali o limitazioni</u> particolari per le PA stesse).
###### Valutazione di interoperabilità
Al fine di individuare errori ed incongruenze nel sistema documentale informatico con quanto appena detto, è necessaria una **valutazione di interoperabilità** dei formati dei file (periodica almeno 1 volta all'anno).
###### Riversamento
A seguito della valutazione di interoperabilità, è possibile valutare l'esigenza di effettuare il riversamento (conversione) di un file in un altro formato che soddisfa le condizioni esposte precedentemente.

### Conservazione dei documenti
Hint: 
::
Documenti informatici ed aggregazioni di essi vanno trasferiti al sistema di conservazione entro i tempi previsti dalla normativa e dal piano di conservazione (è possibile la selezione e lo scarto di documenti prima di passare alla conservazione).
Prima di spostare documenti di rilevanza storico-culturale, è necessario chiedere il consenso al ministero (soprattutto se si intende affidarli a terzi).

### Sicurezza
Hint: 
::
Le PA devono presentare un piano di sicurezza per il trattamento dei dati personali nei documenti digitali. Questo deve essere concordato con i responsabili di: conservazione, transizione digitale e protezione dati. Eventuali violazioni della privacy vanno notificate.
###### Gestione esterna
In caso di gestione documentale esterna, sarà l'azienda esterna la responsabile del trattamento dei dati personali e dovrà redigere e far applicare il piano di sicurezza.

# Conservazione dei documenti

### Sistema di conservazione
I sistemi di gestione documentale delle PA trasferiscono ai sistemi di conservazione documenti informatici, documenti amministrativi informatici e aggregazioni chiusi (ma anche ancora aperti se richiesto dall'ente) per conservarli secondo regolamentazioni e tecniche appropriate.
Il sistema di conservazione deve essere logicamente separato da quello di gestione (dei documenti).
##### Pacchetti informativi
Gli oggetti conservati si distinguono in pacchetti informativi di 3 tipi:
- Di versamento (PdV),
- Di archiviazione (salvato nel sistema di archiviazione),
- Di distribuzione (da distribuire agli utenti).
##### Modelli organizzativi
La conservazione può essere interna o esterna ad un ente. Tutto ciò che riguarda la conservazione è responsabilità di chi se ne fa carico e tale entità deve anche definire il manuale di conservazione.
I fornitori di servizi di conservazione comunque, al fine di garantire autenticità, affidabilità, leggibilità e reperibilità dei documenti, devono attenersi allo standard ISO/IEC 27001, ISO 14721 OAIS e ETSI TS 101 533-1.
##### Ruoli
Ci sono vari ruoli che prendono parte al processo di conservazione:
- Proprietario dell'oggetto conservato,
- Produttore dei PdV (interno nelle PA, spesso responsabile/coordinatore della gestione documentale),
- Utente abilitato (all'accesso ai documenti per reperire info), 
- Responsabile della conservazione,
- Conservatore.
###### Responsabile della conservazione
Il responsabile della conservazione si assicura che i documenti informatici siano conservati in modo sicuro e conforme alle normative. Può essere interno o esterno (purché terzo rispetto al conservatore). Ha vari compiti:
- Definisce e attua politiche di conservazione,
- Verifica regolarmente l'integrità e la leggibilità dei documenti,
- Si occupa della sicurezza fisica e logica del sistema (anche duplicando documenti per ridondanza).
Ruolo e responsabilità di questa figura vanno definiti nel contratto; ma, se il un conservatore esterno offre il servizio di conservazione, alcuni suoi compiti possono essere delegati al responsabile di conservazione.
##### Manuale di conservazione
Il manuale di conservazione è un documento con cui si definisce l'organizzazione e il funzionamento del sistema di conservazione. Esso contiene info su:
- Soggetti coinvolti, i loro ruoli e le loro responsabilità,
- Procedure e tecnologie per garantire autenticità, integrità e leggibilità dei documenti,
- Tipi di documenti digitali conservati + formati gestiti + metadati associati,
- Procedure per il trasferimento dei documenti in conservazione, gestione duplicati, tempi di trasferimento e scarto dei documenti...
Le PA (o i conservatori esterni a cui è affidata la gestione del servizio) devono redigere, adottare e pubblicare il manuale di conservazione sul proprio sito.
##### Processo di conservazione
Il processo di conservazione avviene attraverso vari step:
1) Generazione del PdV (secondo quanto specificato nel manuale) e acquisizione di esso + verifica di conformità rispetto alle modalità del manuale e ai formati specificati.
2) (In caso di anomalie il PdV è rifiutato ma) se il PdV supera la verifica, si genera un rapporto di versamento (con riferimento temporale e impronte crittografiche) univoco e firmato digitalmente.
3) Si prepara il pacchetto di archiviazione, firmandolo e gestendolo secondo quanto nel manuale di conservazione.
4) (Se l'utente lo richiede) sono preparati e firmati pacchetti di distribuzione (conformi allo standard UNI 11386 per l'interoperabilità) con al loro interno 1 o + pacchetti di archiviazione.
5) (Se l'utente lo richiede) si producono duplicati riversati in base alle necessità dell'utente stesso.
6) Alla scadenza dei termini di conservazione previsti, può avvenire lo scarto del pacchetto di archiviazione dal sistema di conservazione.
##### Infrastrutture
Hw e sw usati nei sistemi di conservazione delle PA e dei conservatori devono essere logicamente segregati.
##### Modalità di accesso
Il sistema di conservazione agli autorizzati di accedere direttamente agli oggetti conservati, anche da remoto. Questo ovviamente avviene con modalità in grado di garantire un livello di sicurezza proporzionato al rischio.
##### Selezione e scarto di documenti
Il responsabile di conservazione può effettuare delle selezioni e degli scarti sui pacchetti da conservare. Per ciò fa un elenco di pacchetti di archiviazione da scartare e lo da al responsabile della gestione documentale.
Una volta autorizzato, il titolare dell'oggetto di conservazione distrugge i pacchetti di archiviazione scartati. Tutti gli scarti sono tracciati sul sistema e, al termine di ognuno, il titolare comunica l'esito agli organi di tutela ed al ministero dell'interno se coinvolti dati riservati (solo dopo l'aggiornamento delle copie di sicurezza del sistema da parte loro l'operazione di scarto è raggiunta).