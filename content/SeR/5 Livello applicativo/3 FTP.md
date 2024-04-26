### Cos'è?

L’**FTP** (*File Transfer Protocol*) permette il **trasferimento di file** tra host su una rete senza bisogno di loggarsi o saper usare il sistema remoto destinatario, dando l’accesso a file system remoti con comandi molto semplici. È un servizio <u>client/server</u>, i cui trasferimenti di file sono <u>sia in download che in upload</u>. Utenti client interfacciati col servizio con ***FTP User Agent***.

FTP prevede il **controllo degli accessi** per chi accede a files, per mezzo di una **auth** (username e password) **non cifrata**, per questo è un protocollo <u>non sicuro</u> (al contrario di **SFTP**); ed è il **server FTP** che verifica i privilegi di accesso.

FTP usa TCP (come HTTP), però usa <u>2 connessioni TCP separate</u>:

- **Connessione di controllo**: per l’invio di <u>info di controllo</u> tra gli host (per auth e comandi),
- **Connessione dati**: per il <u>trasferimento di file</u>.

Per questo si dice che **FTP** è ***out-of-band***, al contrario di **HTTP**, che invece invia le <u>info di controllo negli header</u> dei messaggi e usa una <u>connessione unica</u> (***in-band***).

### Modalità

L’FTP ha **2 modalità** di funzionamento:

##### Modalità attiva

All’apertura della porta di comando (client), il client dice al server di voler usare la **modalità attiva** inviandogli un **n° di porta non privilegiata e casuale** (> 1024) **aperta** sullo stesso. Il <u>server</u> apre quindi 2 collegamenti:

- Tra la porta **well-known 20** e l’**IP del server**,
- Tra **porta** specificata dal **client** e l’**IP del client**.

In modalità attiva:

- La **connessione di controllo** è aperta dall’**FTP client**,
- La **connessione dati** è aperta dall’**FTP server**.

Il client deve essere abilitato ad accettare collegamenti tramite qualsiasi porta > 1024; ma i **firewall** impediscono spesso le connessioni in entrata dai server FTP, per cui è stata definita la **modalità passiva**.

##### Modalità passiva

All’apertura della porta di comando (client), il client richiede di voler usare la **modalità passiva**, quindi il <u>server gli fornisce</u> un **n° di porta non privilegiata e casuale** (> 1024) **aperta** sullo stesso. Il <u>client</u> apre quindi 2 collegamenti:

- Tra la **porta** specificata dal **server** e l’**IP del server**,
- Tra una **porta non privilegiata casuale** e l’**IP del client**.

In modalità passiva

- La **connessione di controllo** è aperta dall’**FTP client**,
- La **connessione dati** è aperta dall’**FTP client**.

Con la modalità passiva viene limitato il range delle porte non privilegiate del server FTP, riducendo le porte aperte sul server e semplificando la creazione delle regole del firewall per il server. 

##### Per entrambe le modalità

La **connessione dati** <u>non è persistente</u>, è aperta e chiusa per ogni trasferimento di file.

La **connessione di controllo** <u>è persistente</u>, ovvero mantenuta attiva per tutta la sessione di trasferimento dei file; inoltre è anche ***stateful***, mantiene gli stati, perché il server deve associarla con un utente specifico e la sua directory.

Il salvataggio di informazioni comporta l’uso di RAM, quindi <u>a parità di risorse</u>, un <u>server FTP può mantenere in contemporanea molte meno connessioni rispetto ad un server HTTP</u>.

