### Sicurezza

Gli amministratori di rete devono usare strumenti per proteggere la propria rete ed impedirne l'accesso ai malintenzionati, in particolare riguardo alla comunicazione sicura. Per garantire la sicurezza (di una comunicazione) bisogna rispettare 4 principi:

###### Autenticazione

Una comunicazione è autenticata solo se mittente e destinatario sono certi dell'identità della controparte.

###### Riservatezza

Una comunicazione tra 2 parti è riservata se i messaggi scambiati in essa sono comprensibili solo a loro.

###### Integrità

Un messaggio è integro quando non subisce alterazioni durante la trasmissione (né casuali, né volute).

###### Disponibilità

Un sistema sicuro deve garantire la disponibilità dei propri servizi quando richiesti.

##### Debolezze dei sistemi

Gli attacchi a una rete possono provenire sia dall'interno che dall'esterno. Le debolezze dei sistemi nascono da:

- **Reti**: il solo connettere dei pc a internet li espone a potenziali rischi,
- **Dati**: avere info aziendali critiche rende dei soggetti dei *target* rilevanti,
- **App**: potrebbero contenere vulnerabilità o malware che compromettano il sistema,
- **Complessità dell'architettura di rete**: + un sistema è complesso e ampio, + è difficile garantirne la sicurezza.

### Definizioni

> [!important] Sicurezza
> Insieme delle misure fisiche, tecnologiche ed organizzative che assicurano solo agli utenti autorizzati l'uso di certe risorse (nei tempi e modi prefissati).
> La ***policy*** di un'azienda è poi costituita dalle regole di autenticazione (chi), autorizzazione (cosa) e controllo degli accessi (come) definite per un sistema.

### Componenti

##### Firewall

I firewall sono componenti hw o sw usati per collegare una rete privata *trusted* (fidata) e quindi sicura, con una non sicura, solitamente internet. I firewall controllano il traffico in entrata e in uscita dalla rete da proteggere filtrandolo in base a delle *policy* di sicurezza.

Tipi: packet filter, stateful packet filter, proxy server, personal firewall.

##### Sistemi di rilevamento delle intrusioni

Sono dei sistemi che eseguono un controllo profondo del traffico che vi ci passa, così da individuare attività sospette e inviare avvertimenti all'amministratore di rete (IDS) o anche bloccare il traffico sospetto (IPS).

Tipi: IDS, IPS.

