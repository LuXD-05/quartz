# Crittografia

La **crittografia** è la **disciplina che studia le tecniche matematiche per rendere sicuri i dati** in termini di **confidenzialità**, **integrità**, **auth** e **non ripudio**. Strumenti usati sono **cifrari** e funzioni **hash**.

Il suo **scopo** è **mantenere segrete le info**, trasformando il messaggio originale (in chiaro) in uno cifrato per mezzo di algoritmi di crittografia.

## Tipi di crittografia

### Crittografia simmetrica

Gli algoritmi a **crittografia simmetrica** (a **chiave segreta**) sono degli algoritmi noti che prevedono che la **codifica** e la **decodifica** dei **dati** avvengano usando la **stessa chiave** (per questo "chiave **simmetrica**"), detenuta da entrambi gli interlocutori.

<font color="#aaaaaa">(Un messaggio (m) viene crittografato (C) con un algoritmo con chiave (k), ottenendo il messaggio crittografato $D_k(m)$. Questo viene decriptato (D) usando lo stesso algoritmo con la stessa chiave (k), ottenendo il messaggio originale: $D_k(C_k(m))=m)$</font>.

![[Pasted image 20240305192435.png]]

Questa crittografia però necessita dello **scambio di chiavi**, il che **non è sicuro**.

### Crittografia asimmetrica

Nel 1976 venne introdotta la **crittografia asimmetrica** (o a **chiave pubblica**), che adotta sempre algoritmi pubblici, ma che usano **2 chiavi diverse per cifrare e decifrare il messaggio**. Qui vi sono 2 tipi di chiavi:

- Quelle **pubbliche** (*kpb*), chiavi di cifratura che il **destinatario** ricava e **condivide**. Il destinatario invia la sua al mittente così che questo **critti il messaggio con essa**, rendendolo **decrittabile solo con la sua *kpr***. 
- Quelle **private** (*kpr*), chiavi segrete di decodifica **non condivisibili** posseduta **solo dal destinatario**. Sono **associate ad altre *kpb*** e vengono usate dal destinatario per **decrittare messaggi crittati con la *kpb* associata**.

La sicurezza del metodo si basa sul fatto che ricavare la chiave privata dalla chiave pubblica sia troppo **complesso**. Quindi: $D_{kpr}(C_{kpb}(m))=m$.

![[Pasted image 20240305192755.png]]

### L'algoritmo RSA

L'algoritmo **RSA** (Rivest, Shamir, Adleman) si basa sulla teoria di scomposizione in **fattori primi** di un numero e usa sempre una coppia di chiavi generate in modo che sia impossibile ricavare una dall'altra. Pubblicato nel 1978, era considerato sicuro fino a poco tempo fa e prevede 3 passi:

##### Determinazione *kpb* e *kpr*

Si trovano chiave pubblica e privata in 5 step:

1) Si scelgono 2 numeri *p* e *q* primi e molto grandi (almeno 300 cifre, così grandi per rendere impossibile ricavare i fattori dal prodotto),
2) Si trova $n = p * q$
3) Si trova $m = (p-1) * (q-1)$
4) Si determina un numero *e* primo rispetto a *m* (senza divisori in comune con *m*),
5) Si trova *k* tale che: $[(e * k) |m|] = 1 \rightarrow k = (m * h + 1)/e$ con *h* intero e positivo.

Quindi:

- La *kpb* è data dalla coppia (*e, n*),
- La *kpr* è data dalla coppia (*k, n*).

##### Cifratura del messaggio

Il messaggio viene cifrato con la *kpb*. 

Per evitare attacchi basati sull'analisi delle frequenze, il messaggio è convertito in binario e diviso in blocchi di *g* bit, con *2g* < *m*; e ogni blocco è cifrato con la *kpb*. Se *M* è un blocco, un blocco cifrato *C* è: $C = (M_{e}|n|)$.

##### Decifratura del messaggio

Il messaggio ricevuto viene infine decifrato dal destinatario con la sua *kpr*, questo anche per i blocchi, che decifrati sono: $M = (C_{k}|n|)$.

#### Crittografia a chiave di sessione

Poiché gli **algoritmi a chiave asimmetrica** sono molto **complessi** e **onerosi**, alcune applicazioni li usano per scambiarsi **solo 1 chiave segreta** da usare per la **sessione** (**chiave di sessione**, che cambia ad ogni sessione).

## Sicurezza delle reti

### I dati

La sicurezza in archiviazione e trasmissione dati richiede adeguate misure di protezione. La tecnica di base è la **crittografia** nelle sue 2 forme più diffuse: **simmetrica** e **asimmetrica**; a questa sono legati argomenti come la **firma digitale** e la **certificazione**. 

Il problema è rilevante quando si vanno a trattare **dati sensibili** (tipo per i pagamenti digitali) con operazioni che richiedono un certo livello di sicurezza. Garantire la protezione è possibile con delle funzionalità implementate nel punto di accesso tra il provider e l'internet (secondo la ISO Security Architecture) divise in 5 classi:

##### Autenticazione

**Verifica che chi richiede un servizio sia effettivamente chi dichiara di essere**; infatti si basa sul fatto che chi deve autenticarsi deve dimostrarlo con qualcosa di riservato.

Auth con usr e pwd è poco affidabile per un sistema di rete in quanto, a differenza di auth in app, qui la trasmissione di pwd a chi autentica espone a rischi; perciò è necessaria la **crittografia**.

##### Controllo degli accessi

Quando l’auth è fatta, è possibile **limitare gli accessi degli utenti alle risorse**:

- In caso di pc, ciò è riferito a risorse del file system (directory, file, driver, permessi di lettura, scrittura, esecuzione…),
- In caso di rete invece, si controlla l'accesso e la visibilità degli altri pc in rete (e quindi i loro servizi) mediante firewall.

##### Riservatezza

Quando si usa un servizio, bisogna **assicurarsi che i dati scambiati tra mittente e destinatario non siano usati da terzi**. Anche se mira ad evitare che i dati siano estraibili dal traffico, la riservatezza è generalmente interpretata come **crittografia** dei dati.

##### Integrità

I dati devono comunque poter **raggiungere la destinazione senza modifica di terzi**; quindi anche per info pubbliche, bisogna verificare la corrispondenza di quanto ricevuto con quanto trasmesso.

C'è quindi bisogno di un **codice di controllo** che rileva alterazioni dei dati il quale, per garantire l'integrità, può viaggiare anche non protetto; ma per garantire la sicurezza, bisogna fare in modo che solo il mittente lo possa generare per evitare manomissioni.

##### Non ripudio

Per le comunicazioni (tipo transazioni) bisogna **garantire che le parti di uno scambio non neghino di aver preso parte allo stesso**. Ciò si risolve con **firme digitali** sempre crittografate.

#### Sicurezza delle comunicazioni

Di queste: **auth, riservatezza e integrità**, riguardano aspetti di protezione **indipendenti dai dati**. Perciò le loro funzionalità sono fornite e **implementate da apparati di rete** (firewall...) o **programmi** generici (browser...).

#### Sicurezza delle applicazioni

Le restanti: **controllo degli accessi e non ripudio**, sono **legate alle app e ai dati** scambiati.

- Le modalità di controllo degli accessi variano in base al OS usato, dall'applicazione...
- Per il non ripudio invece le modalità per eseguire la **firma digitale** sono standard, le infrastrutture necessarie sono diffuse e sono usate per proteggere comunicazioni interpersonali e transazioni.

### Firme digitali

Queste funzionalità però non garantiscono del tutto l'affidabilità dei documenti perché bisogna sapere **chi ne è l'autore**, per garantirne l'**integrità e impedirne il ripudio**.

Una soluzione a ciò è la **firma digitale** (*digital signature*), che usa l'algoritmo **RSA a chiave pubblica** per **cifrare un documento con la *kpr* del mittente** rendendolo **decifrabile con la *kpb* associata** in modo da essere certi dell'identità del mittente.

Dato che il messaggio è crittato con la *kpr* del mittente, chiunque potrà leggerlo (dato che la *kpb* è pubblica); quindi per garantire sia segretezza che autenticazione, il **mittente** deve:

- **Crittare** il messaggio **con la propria *kpr*** (autenticità),
- **Crittare** il messaggio firmato **con la *kpb* del destinatario** (segretezza).

Mentre il **destinatario** dovrebbe:

- **Decrittare** il messaggio con la **propria *kpr*** (segretezza),
- **Decrittare** il messaggio con la ***kpb* del mittente** (autenticità).

#### Digest

**Crittografare l'intero messaggio è oneroso e troppo lungo**, perciò si usa il ***digest***: un **riassunto** estratto dal messaggio originale che **crittato va a costituire la firma**. Questo si ottiene applicando funzioni di ***hash*** al messaggio originale, ottenendo quindi una stringa molto **+ corta**, **dipendente da esso** e che **identifica univocamente il documento e il mittente** (siccome è **impossibile modificare il messaggio senza modificarne l'hash**).

##### Step

- **Si ricava il *digest*** dal messaggio,
- Il ***digest* viene cifrato con la *kpr* del mittente** (autenticità),
- Il **messaggio +** la firma (***digest*** cifrato) sono **trasmessi**,
- Il **ricevitore ricalcola il *digest* dal messaggio** e lo **confronta con quello estratto dalla firma** (ottenuto con la *kpb* del mittente),
- **Se** i 2 *digest* sono **uguali**, il **documento è integro e la firma è autentica**.

![[Pasted image 20240305221655.png]]

###### Approfondimento

Per scoprire modifiche apportate da esterni si usano funzioni di *hash*, che rendono impossibile modificare il testo senza modificarne l'*hash* e hanno bassissima probabilità di avere 2 *hash* uguali.

Tra gli algoritmi più usati c'è **MD5** (Message Digest Algorithm 5, oggi non del tutto sicuro) e **SHA** (Secure Hash Algorithm). Quest'ultimo produce un *digest* di lunghezza fissa da un messaggio di lunghezza variabile ed è sicuro perché:

- La funzione **non è reversibile** (**non si può tornare al messaggio dal *digest***),
- **Non deve essere possibile creare 2 messaggi diversi con lo stesso *digest***.

A questa famiglia appartengono SHA-1, SHA-256 e SHA-512.

### Certificati digitali

Sono dei **file** con **validità temporale limitata**, che **garantiscono l’identità di un soggetto** (dispositivo o persona che sia) **assicurando l'auth della sua *kpb***. (In pratica sono degli alter ego dei documenti d'identità nella vita reale). Sono usati ogni volta per problemi di sicurezza tipo:

- Quando si forniscono/usano servizi online con pagamenti e consultazione di dati riservati,
- Quando si scambiano email, dove il mittente che compare non assicura niente, ma è riconosciuto con la firma digitale,
- Quando si vuole verificare la validità di documenti caricati in / scaricati da internet.

##### CA

I certificati digitali sono rilasciati dalle **CA** (*Certification Authorities*) o da enti detti "autorità di rilascio certificati autonome". Le CA rilasciano certificati agli utenti che ne fanno richiesta dopo una verifica della loro identità e mantengono:

- Un **registro pubblico dei certificati**, che permette a chiunque di verificare la validità di un certificato,
- Una ***Certification Revocation List***, una lista dei certificati revocati.

### Protocollo SSL/TLS

Garantisce la **sicurezza** di un collegamento garantendone:

- **Privatezza**: con la crittografia usata dopo un **handshake iniziale** per definire una **key segreta** (perché per crittografare i dati si usa la crittografia simmetrica, tipo DES, RC4...).
- **Autenticazione**: l’identità delle connessioni è autenticata con la **crittografia asimmetrica o a key pubblica** (tipo RSA...) così che client sono sicuri di parlare col server giusto (entrambi da certificare).
- **Affidabilità**: il livello trasporto include un ***integrity check*** del mess basato su un **MAC** (*Message Authentication Code*) che usa funzioni **hash sicure** (SHA, MD5...) per verificare che i dati non siano stati alterati durante la trasmissione.

L'SSL/TLS ha lo scopo di fornire **riservatezza** e **affidabilità** alle comunicazioni. Si compone di 2 strati:

- **SSL Record Protocol** (inferiore), usato per la **trasmissione dei messaggi protetti**,
- **SSL Handshake Protocol** (superiore), che si **interfaccia sull'SSL Record Protocol e permette a client e server di autenticarsi a vicenda negoziando algoritmi di crittografia e chiavi**.
