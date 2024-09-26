### Sicurezza

Gli amministratori di rete devono usare strumenti per proteggere la propria rete ed impedirne l'accesso ai malintenzionati, in particolare riguardo alla comunicazione sicura. Per garantire la sicurezza (di una comunicazione) bisogna rispettare <u>4 principi</u>:

###### Autenticazione

Una comunicazione è **autenticata** solo se <u>mittente e destinatario</u> sono <u>certi dell'identità della controparte</u>.

###### Riservatezza

Una comunicazione tra 2 parti è **riservata** se i <u>messaggi scambiati</u> in essa sono <u>comprensibili solo a loro</u>.

###### Integrità

Un messaggio è **integro** quando <u>non subisce alterazioni durante la trasmissione</u> (né casuali, né volute).

###### (Disponibilità)

Un sistema sicuro deve garantire la **disponibilità** dei propri servizi quando richiesti.

##### Debolezze dei sistemi

Gli attacchi a una rete possono provenire sia dall'interno che dall'esterno. Le debolezze dei sistemi nascono da:

- **Reti**: il solo connettere dei pc a internet li espone a potenziali rischi,
- **Dati**: avere info aziendali critiche rende dei soggetti dei *target* rilevanti,
- **App**: potrebbero contenere vulnerabilità o malware che compromettano il sistema,
- **Complessità dell'architettura di rete**: + un sistema è complesso e ampio, + è difficile garantirne la sicurezza.

### Definizioni

> [!important] Sicurezza
> Insieme delle misure fisiche, tecnologiche ed organizzative che assicurano solo agli utenti autorizzati l'uso di certe risorse (nei tempi e modi prefissati).
> La ***policy*** di un'azienda è poi costituita dalle regole di autenticazione (chi), autorizzazione (cosa) e controllo degli accessi (come) definite per un sistema (vedi [[4.1 AAA]]).

### Componenti

##### Firewall

I firewall sono componenti hw o sw usati per collegare una **rete privata*[](4.1%20AAA.md) (fidata) e quindi <u>sicura</u>, con una <u>non sicura</u>, solitamente **internet**. I firewall <u>controllano il traffico in entrata e in uscita dalla rete da proteggere filtrandolo</u> in base a delle *policy* di sicurezza.

##### Sistemi di rilevamento delle intrusioni

Sono dei sistemi che eseguono un <u>controllo profondo del traffico che vi ci passa</u>, così da individuare <u>attività sospette</u> e inviare <u>avvertimenti</u> all'amministratore di rete (IDS) o anche <u>bloccare il traffico</u> sospetto (IPS).

