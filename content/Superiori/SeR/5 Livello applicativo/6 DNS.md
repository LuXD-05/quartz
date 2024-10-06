---
public: true
modified_at: 15/06/2024 18:10:48
edited_seconds: 500
---
### Cos'è
Hint: 
::
Il **DNS** (*Domain Name System*) da la possibilità agli utenti in internet di riferirsi alle risorse (siti, caselle di posta, servizi cloud su una macchina avente IP) attraverso **nomi mnemonici** e <u>non tramite i loro indirizzi IP</u>.
Per fare questo è stata predisposta una <u>rubrica</u> (*directory*) che associa i nomi mnemonici (detti **nomi di dominio**) ai corrispondenti **IP**. Questa è implementata con un <u>database distribuito</u> si vari pc detti ***name server***, i quali eseguono un sw *DNS server* che risponde alle richieste di risoluzione dei nomi.
**DNS** quindi realizza il <u>servizio di directory di internet</u>. Si risolve un nome di dominio in un IP quando un utente cerca di accedere a un sito, in quanto, usando HTTP o HTTPS, la connessione (socket) che si deve creare con il server web necessita del suo IP.

## Componenti
Il DNS riguarda vari componenti e processi:

### 1) Richiesta della risoluzione
Hint: 
::
##### Step
1) Viene mandata una richiesta di risoluzione di un nome di dominio da una app (tipo browser) al ***Resolver*** (sw *DNS client*) fornito dall'OS dell'host. 
2) Il *Resolver* fa la richiesta al ***Recursor*** (o <u>DNS server locale</u> o *name server*), il quale avvia la ricerca dell'IP corrispondente al nome. L'informazione, se trovata, viene rimandata al *Resolver* come risposta, altrimenti questo riceverà un codice di errore.
##### Altro
In ogni host va configurato il **default DNS server locale** immettendone l'**IP** (manualmente in modo statico o col DHCP in modo dinamico, come per il *default gateway*).
I ***Recursor*** sono ridondati per rendere il sistema + robusto/disponibile; infatti ci sono sempre un ***name server*** primario e uno secondario, i cui IP sono solitamente forniti dall'ISP.
Esistono però dei DNS server locali **alternativi** a quelli dell'ISP, tipo:
- <u>Google</u>: 8.8.8.8 (primario) e 8.8.4.4 (secondario).
- <u>Cloudflare</u>: 1.1.1.1 (primario) e 1.0.0.1 (secondario).
##### Perché scegliere Cloudflare
Ci sono varie ragioni per scegliere il *Recursor* di Cloudflare (rispetto a quello dell'ISP):
###### Sicurezza
Differisce da molti altri ISP che non usano tecniche di cifratura forte o non supportano il protocollo [[#DNSSEC]] sui loro *name server*; per questo (le query di) molti utenti sono esposti ad attacchi tipo *[[9 Sicurezza informatica#Attività di hacking|man-in-the-middle]]*.
###### Prestazioni
- Spesso gli ISP usano i record DNS per tracciare le attività e i comportamenti degli utenti.
- La velocità dei *Recursor* degli ISP può non essere molto alta.
- Gli ISP possono eseguire politiche di filtraggio per certi siti bloccandone la risoluzione dei nomi.

### 2) Ricerca della soluzione
Hint: 
::
Il *Recursor* inizia la ricerca degli IP interrogando i ***name server*** aventi il db distribuito. Ci sono 3 tipi di *name server*:
![](https://i.imgur.com/BerPLxq.png)
##### Root
Il ***Root name server*** è il 1° *name server* cui si rivolge il *Recursor* per risolvere un nome (ogni *Recursor* deve conoscere tutti i *root name server*). Questo accetta le query del *Recursor* e risponde indirizzandolo verso il *TLD name server*.
Risposta: RR NS.
##### TLD
Un ***Top Level Domain name server*** memorizza i dati per tutti i nomi che condividono un dominio *top level* (tipo ".com"). Un *TLD name server* può essere ***authoritative*** per 1 o + nomi di dominio e può non esserlo per altri.
##### Authoritative
> [!important] Authoritative
> Un *name server* è ***authoritative*** (autorevole) per un nome di dominio se questo è registrato presso di lui (quindi se nel suo db è presente l'IP ("RR A" o "AAAA") per quel nome + le altre info necessarie alla registrazione).
 
Un ***Authoritative name server*** amministra (possiede (nel db)) i dati di un nome di dominio, quindi è detto *authoritative* solo per i nomi che gestisce.
![](https://i.imgur.com/Lv0WA1k.png)

### 3) Gerarchia dei nomi di dominio
Hint: 
::
I nomi di dominio hanno una struttura gerarchica ad albero che rispecchia la gerarchia dei *name server*:
![](https://i.imgur.com/VATKQKO.png)
Un nome di dominio è costituito da tutte le parole della gerarchia collegate con un ".". Ogni parola (parte) del nome di dominio è detta ***label*** e può essere di max 63 byte; inoltre:
- Ad un certo livello della gerarchia, non ci potranno essere 2 etichette uguali.
- C'è sempre una **label riservata** *null* di lunghezza 0, usata per la ***root***.
###### Esempio
Prendiamo il nome di dominio "example.com." (in foto). Per leggere i livelli si fa da destra a sinistra e:
1) "**.**": è il 1° e + alto livello (***root***),
2) "**com**": è il livello **TLD**,
3) "**example**": è il livello **SLD**.
Un nome di dominio che presenta anche il "." finale di *root* è detto ***fully qualified domain name***. La gerarchia dei nomi costituisce il ***namespace***. I dati per risolvere i nomi sono memorizzati nella **gerarchia di *name server***.
##### Zona e Zone file
> [!important] Zona
> Insieme dei dati relativi sotto una certa amministrazione
 
Le **zone** sono salvate in dei file di testo detti ***zone file***. Una zona può riguardare 1 o + domini e sottodomini:
![](https://i.imgur.com/L29pxu2.png)
##### Root zone
I dati della ***root zone*** sono gestiti dai ***root name server*** e sono salvati nel ***[root zone file](https://www.internic.net/domain/root.zone)***. 
Ci sono 13 IP diversi riservati per i *root name server* (per i limiti dell'architettura DNS originale) e ognuno è associato a vari *name server* ridondati ([root-servers.org](https://root-servers.org/), 1757 distribuiti nel mondo) i quali usano l'***anycast routing***.
L'***anycast routing*** permette di assegnare a + pc lo **stesso IP**, così da **distribuire** le richieste in base al **carico** e alla **vicinanza**, fornendo un servizio **uniforme** su vaste aree geografiche. Per questo e la **ridondanza**, i *root name server* sono molto affidabili.
I 13 IP sono gestiti da varie organizzazioni e sono etichettati da una lettera dalla **A** alla **M**.
![](https://i.imgur.com/Lt2lo50.png)
Dato che i *root name server* sono in cima alla gerarchia dei *name server*, i loro IP non possono essere risolti tramite DNS; quindi ogni *Recursor* contiene implementati nel sw, i 13 IP.
##### Albero dei nomi di dominio
I nomi di dominio sono organizzati in una struttura ad albero:
1) Dominio di **root** ("**.**" = null)
2) **TLD** (*Top Level Domains*, tipo ".com", ".it"...), domini di 1° livello, a loro volta suddivisi in:
   - **Nazionali** o **ccTLD** (*country-code TLD*), usati da stati o territori e costituiti da 2 lettere (it, eu...),
   - **Generici** o **gTLD** (*generic TLD*), usati da particolari classi di organizzazioni e fatti da 3 o + lettere.
     La > parte dei gTLD sono disponibili in tutto il mondo, ma .gov, .mil e .edu sono riservati a governo, militari ed enti educativi statunitensi.
3) **SLD** (*Second Level Domains*), domini di 2° livello e corrispondenti ad aziende, enti e persone.
4) ***Subdomains*** (sottodomini), nomi definiti sotto un dominio SLD (tipo "**mail**.google.com").
Oltre al *namespace* pubblico, un'azienda può definire un *namespace* privato per i domini locali dell'azienda, così di rendere identificabili i server interni con nomi e non con IP.
##### Zone file e name server primario e secondario
I dati di una zona sono usati da **1** *name server* primario <u>e</u> da **almeno 1** *name server* secondario:
- Il *name server* **primario** gestisce i dati (**RR *authoritative***) di dominio o i domini della zona controllata. I dati sono salvati in uno *zone file* nel file system locale. 
  **Modifiche** a record DNS di una zona possono essere fatte solo sul **server primario** della stessa (*zone file* in lettura/scrittura).
- I *name server* **secondari** lavorano sui dati acquisiti dal primario tramite una procedura automatica detta ***zone-transfer*** (DNS port 53 TCP), dove lo *zone file* è una copia *readonly*. 
  I *name server* secondari forniscono **ridondanza** aumentando la **robustezza** del sistema e, grazie al ***load balancing***, aumentano la **disponibilità del servizio**.
##### Zone file e dati DNS - RR
I dati DNS sono organizzati in **RR** (***Resource Record***), contenuti negli *zone file* e forniscono info riguardo a un certo dominio. Ogni RR contiene dati formattati secondo le regole dell'RFC 1035.
Struttura generale di un RR: \[Name] \[TTL] \[Class] \[Type] \[Resource data] $\;\rightarrow\;$ "google.com. 300 IN A 74.125.131.138". Campi:
- **Name**: nome di cui l'RR fornisce info,
- **TTL**: per quanti secondi l'info può restare in cache,
- **Class**: in internet è sempre "IN",
- **Type**: tipo di RR fornito, a sua volta (per capirne le funzioni: [[#5) Servizi aggiuntivi|link]]):
	- **A** (*IPv4*): record con in "Resource data" l'IPv4 corrispondente a "Name";
	- **AAAA** (*IPv6*): record con in "Resource data" l'IPv6 corrispondente a "Name";
	- **CNAME** (*Canonical name*): in "Resource data" vi è il nome ***vero*** (<u>canonico</u>) del nome (<u>alias</u>) in "Name" (per arrivare all'IP risolvere il nome canonico);
	- **MX** (*Mail eXchange*): in "Resource data" vi è il **nome** del **mail server** associato a "Name";
	- **NS** (*Name Server*): da il ***referral*** (riferimento) a un ***authoritative name server*** ("Resource data" quindi contiene il nome del prossimo *name server* di livello inferiore da contattare);
- **Resource data** (*RDATA*): è il valore dell'info fornita (dipende da Type). 
##### Esempi di "Type"
###### A
Fornisce l'**IPv4 cercato**. Solitamente i siti hanno <u>1 solo record A</u>, ma alcuni ne hanno di + siccome il sito è <u>replicato su + web server</u>; questo al fine di usare il ***load balancing*** di DNS, che (in ***round-robin***) fa ruotare gli RR e usa il 1° in lista.
###### AAAA
Fornisce l'**IPv6 cercato** (resto come "A").
###### CNAME
Fornisce il **nome canonico** di un ***alias*** (<u>non contiene un IP</u>, ma **un altro nome da risolvere**). Il nome canonico è fornito quando un dominio è un *alias* di un altro, ovvero è un nome pubblico diverso da quello privato interno ad un'azienda.
###### MX
Questo permette di risolvere un nome di dominio di un *mail server*. (Come "CNAME") un record MX <u>non contiene un IP</u>, ma il nome del ***mail server*** da **risolvere**.
###### NS
Fornisce il nome di un ***authoritative name server*** per un certo nome di dominio. <u>Non contiene IP</u>, bensì i nomi dei ***name server*** contenenti **RR** per i **nomi di dominio** con quell'**estensione**.
Un dominio di solito ha **+ record NS**: **1** per il *name server* **primario** e **almeno 1** per il **secondario**. <u>Senza NS configurati correttamente</u>, una <u>risorsa sarà irraggiungibile</u>.
I **record NS** sono dati da un *name server* di livello superiore (**root** o **TLD**) per raggiungere, prima o poi, l'*authoritative name server* per il nome cercato. Questi record sono detti ***referral*** perché sono un rinvio ad un altro nome.

### 4) Risoluzione
Hint: 
::
##### Tipi di query
Un nome di dominio viene risolto accedendo ai dati (RR) del db distribuito per mezzo di ***query***, che in DNS possono essere di 2 tipi:
![](https://i.imgur.com/DYPVm2h.png)
###### Ricorsive
- A una richiesta, si ha in risposta:
	- O la soluzione (l'indirizzo IP: "*A*" o "*AAAA*"),
	- O un errore.
- Sono fatte dal ***Resolver*** al ***Recursor***.
###### Iterative
- A una richiesta si ha in risposta:
	- O la soluzione (l'indirizzo IP: "*A*" o "*AAAA*"), 
	- O un suggerimento per ottenerla (*referral* NS al *name server* successivo).
- Sono fatte dal ***Recursor*** a un ***name server***.
##### Query e protocollo di trasporto
Il protocollo DNS usa (in **porta 53**):
- **UDP** per payload **< 512** byte, quindi, per le **query di risoluzione** dei nomi.
- **TCP** per payload **> 512** byte, quindi, per trasferire ***zone files*** (tra server primari e secondari).
##### Query e caching
Il processo di risoluzione di un nome di dominio in IP prevede vari passi e quindi molto tempo. Per <u>limitare i tempi di risposta</u> (velocizzarlo), il DNS prevede un sistema di ***caching* delle risposte alle query**.
**Scopo**: memorizzazione <u>temporanea</u> dei dati, per migliorare le prestazioni della ricerca DNS. 
Il ***caching*** è fatto <u>il + vicino possibile a chi fa le richieste</u>, per limitare il n° di query necessarie alla risoluzione di un nome. I record in *cache* sono mantenuti per un certo tempo (**TTL**).
Il salvataggio in cache dei RR può avvenire:
- Nei browser,
- Nei *Resolver* (OS),
- Nei *Recursor*,
- Nei *name server* della gerarchia.

### 5) Servizi aggiuntivi
Hint: 
::
Tramite le info nei RR e le query, il DNS offre:
- ***DNS Lookup***: (o risoluzione dei nomi di dominio) con i record "**A**" e "**AAAA**".
- ***Host aliasing***: differenziazione tra il nome pubblico e quello privato interno all'organizzazione tramite i record "**CNAME**".
- ***Mail server aliasing***: (come gli host ma) uso dello stesso nome sia per *web server* che per *mail server* tramite i record "**MX**".
- "***Load balancing***": tramite la tecnica ***round-robin*** usata nella distribuzione delle query tra il server primario e i secondari.

### 6) Registrare nomi di dominio
Hint: 
::
Per pubblicare un sito serve scegliere un **nome di dominio** e un **TLD**. Ci sono delle parti che hanno un ruolo nel processo di pubblicazione di un sito:
##### Registrant
<u>Entità</u> (individuo, azienda...) a cui <u>serve un certo nome di dominio</u> per un servizio. 
Quando un ***Registrant*** registra un dominio, esso diventa **proprietario del diritto di usare il nome**, <u>non del nome in sé</u>. Inoltre la registrazione ha una **durata definita** ma **rinnovabile**.
Per registrare un nome di dominio, il *Registrant* si dovrà rivolgere al ***Registrar***, il quale si occuperà del **TLD** scelto.
##### Registrar
<u>Azienda</u>, accreditata dalla **ICANN** (*Internet Corporation for Assigned Names & Numbers*), che 1) <u>"vende" nomi di dominio</u> e 2) <u>raccoglie e invia le info di registrazione ad un ***Registry***</u>.
I *Registrar* registrano i TLD; alcuni si occupano dei **gTLD** e altri dei **ccTLD**. 
##### Registry
(O ***Registry Operator***) è un'<u>organizzazione che amministra i TLD di una zona</u>. Riceve dai *Registrar* dei **RR** (info) di un nome e **aggiorna** con essi lo ***zone file***.
**Obiettivo**: mantenere funzionante l'infrastruttira (*name server* + db) che rende possibile il *DNS Lookup*.

## DNSSEC
Hint: 
::
##### Problema
Quando si accede a un sito, il *Recursor* dell'ISP interrogherà tutti i livelli della gerarchia dei DNS *name server* (dal *Root name server* all'*authoritative name server* per quel sito) ottenendo infine l'IP.
Gli hacker potrebbero eseguire del ***cache poisoning***, ovvero modificare dei dati (RR authoritative o in cache) inserendo dei valori falsi e far risolvere il nome di dominio con un IP che porta ad un altro sito web invece che all'originale.
##### Soluzione
**DNSSEC** (*DNS Secure*) protegge il DNS basandosi su delle ***signatures* crittografate** (firme), con cui si firmano i record negli *authoritative name server*.
Come <u>HTTPS cifra il traffico, DNSSEC firma gli RR</u> cosicché i falsi siano rilevabili.