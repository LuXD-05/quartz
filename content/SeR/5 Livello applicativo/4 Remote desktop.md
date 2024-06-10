### Cos'è?

Protocollo che permette a un client (locale) di funzionare come terminale di un pc remoto server.

- Tutto ciò che è fatto dal client viene inviato al server, che lo interpreta come se fosse stato fatto su di sé,
- Tutto ciò che il server mostra in output (allo schermo), è trasmesso al client via internet e questo lo visualizza.

Il pc server usa la console del client per l’I/O, quindi ciò che il client scrive in console è interpretato e eseguito su server.

### Telnet

È un protocollo client/server basato su TCP (server port 23) e il nome del prog che avvia sessioni con l’host remoto. Per la progettazione del protocollo e la sua flessibilità, con programmi Telnet è possibile stabilire connessioni a altri servizi internet, come SMTP (port 25) o HTTP (port 80). 

Telnet è insicuro, quindi di default è disabilitato sui server in rete (anche su windows) e i dati sono trasmessi in chiaro.

### PuTTY

PuTTY è un programma client per remote desktop per OS windows e implementa protocolli client, tipo Telnet e SSH.

### SSH

SSH (Secure Shell) dà agli amministratori di rete un modo sicuro per accedere a un host remoto. Usa la porta 22.

È molto usato per: gestione remota di sistemi e app, accedere ad host in rete, eseguire comandi e spostare file tra pc… 

Se serve, SSH usa la crittografia a chiave pubblica per autenticare l’host remoto e consentirgli di autenticare l’utente (ovviamente tutti i dati di auth, i comandi, l’output e i file trasferiti sono crittati).

