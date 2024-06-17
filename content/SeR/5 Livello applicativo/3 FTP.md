### Cos'è?

L’**FTP** (*File Transfer Protocol*) permette il **trasferimento di file** tra host su una rete senza bisogno di loggarsi o saper usare il sistema remoto destinatario, dando l’accesso a file system remoti con comandi molto semplici. 

È un servizio <u>client/server</u>, i cui trasferimenti di file sono <u>sia in download che in upload</u>. Utenti client interfacciati col servizio con ***FTP User Agent***.

FTP prevede un **controllo degli accessi** ai file, tramite un'**autenticazione non cifrata**, perciò <u>non è sicuro</u> (al contrario di **SFTP**); ed è il **server FTP** che verifica i privilegi di accesso.

**FTP** usa <u>TCP</u>, però usa <u>2 connessioni TCP separate</u> (***out-of-band***, al contrario di [[2 HTTP|HTTP]]):

- **Connessione di controllo**: per l’invio di <u>info di controllo</u> tra gli host (per auth e comandi),
- **Connessione dati**: per il <u>trasferimento di file</u>.

### Modalità

##### Modalità attiva

<u>Stabilita la connessione di comando</u> (porta 21), il client dice al server di voler usare la **modalità attiva** inviandogli un **n° di porta non privilegiata e casuale** (> 1024) **aperta** sullo stesso. Il <u>server</u> apre quindi la <u>connessione dati</u> tra:

- Socket server con: \[**IP server** + **porta 20**\],
- Socket client con: \[**IP client** + **porta specificata dal client**\].

In modalità attiva:

- La **connessione di controllo** è aperta dall’**FTP client**,
- La **connessione dati** è aperta dall’**FTP server**.

Il client deve essere abilitato ad accettare collegamenti tramite qualsiasi porta > 1024; ma i **firewall** impediscono spesso le connessioni in entrata dai server FTP, per cui è stata definita la **modalità passiva**.

##### Modalità passiva

<u>Stabilita la connessione di comando</u> (porta 21), il client richiede di voler usare la **modalità passiva**, quindi il <u>server gli fornisce</u> un **n° di porta non privilegiata e casuale** (> 1024) **aperta** sullo stesso. Il <u>client</u> apre quindi la <u>connessione dati</u> tra:

- Socket server con: \[**IP server** + **porta specificata dal server**\],
- Socket client con: \[**IP client** + **porta non *well-known* casuale del client**\].

In modalità passiva

- La **connessione di controllo** è aperta dall’**FTP client**,
- La **connessione dati** è aperta dall’**FTP client**.

Con la modalità passiva viene limitato il range delle porte non privilegiate del server FTP, riducendo le porte aperte sul server e semplificando la creazione delle regole del firewall per il server.

##### Per entrambe le modalità

La **connessione dati** <u>non è persistente</u>, è aperta e chiusa per ogni trasferimento di file.

La **connessione di controllo** <u>è persistente</u>, ovvero mantenuta attiva per tutta la sessione di trasferimento dei file; inoltre è anche ***stateful***, mantiene gli stati, perché il server deve associarla con un utente specifico e la sua directory.

Il salvataggio di informazioni comporta l’uso di RAM, quindi <u>a parità di risorse</u>, un <u>server FTP può mantenere in contemporanea molte meno connessioni rispetto ad un server HTTP</u>.

