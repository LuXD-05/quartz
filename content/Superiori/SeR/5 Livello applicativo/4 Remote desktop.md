---
public: true
modified_at: 15/06/2024 16:40:04
edited_seconds: 120
---
### Cos'è?
Protocollo che permette a un <u>client (locale) di funzionare come terminale di un pc remoto server</u>.
- Tutto ciò che è fatto dal client viene inviato al server, che lo interpreta come se fosse stato fatto su di sé,
- Tutto ciò che il server mostra in output (allo schermo), è trasmesso al client via internet e questo lo visualizza.
Il pc server usa la console del client per l’I/O, quindi ciò che il client scrive in console è interpretato e eseguito su server.

### Protocolli e app
Hint: telnet, SSH, PuTTY
##### Telnet
È un <u>protocollo client/server basato su TCP</u> (server <u>port 23</u>) e il nome del sw che avvia sessioni con l’host remoto. Per la progettazione del protocollo e la sua flessibilità, con programmi Telnet è possibile stabilire connessioni a altri servizi internet, come SMTP (port 25) o HTTP (port 80). 
Telnet è **insicuro**, quindi di default è disabilitato sui server in rete (anche su windows) e i dati sono trasmessi in chiaro.
##### SSH
**SSH** (*Secure Shell*) dà agli amministratori di rete un modo sicuro per accedere a un host remoto. Usa la <u>porta 22</u> ed molto usato per: gestione remota di sistemi e app, accedere ad host in rete, eseguire comandi e spostare file tra pc… 
Se serve, SSH usa la <u>crittografia a chiave pubblica</u> per autenticare l’host remoto e consentirgli di autenticare l’utente (ovviamente tutti i dati di auth, i comandi, l’output e i file trasferiti sono crittati).
##### PuTTY
**PuTTY** è un programma client per remote desktop per OS windows e implementa protocolli client, tipo Telnet e SSH.
