---
public: true
modified_at: 12/06/2024 17:21:46
edited_seconds: 2130
---
### Motivi
Hint: 6 motivi x usare WLAN
::
Ci sono vari motivi per cui si vorrebbe usufruire di una wireless LAN:
- (Prima di tutto) per la <u>comodità</u> della connettività wireless,
- <u>Non servono cavi</u> ed è un tipo di rete <u>poco invasiva</u> (si possono installare WLAN anche in ambienti con stretti vincoli architetturali),
- Non <u>vincola ad un luogo fisso o ad un ambiente ristretto</u> (non si deve stare sulla scrivania, ma prende in tutta la casa),
- Prevede anche la creazione di <u>hotspot</u> per clienti o esterni in visita per collegarsi alla rete pubblica aziendale,
- Notevoli <u>risparmi sul cablaggio</u> strutturato dell'edificio (cioè canaline, cavi...).
- La <u>rete è scalabile</u> (distribuendo *WAP* o *Wireless Extender*).

### Problemi
Hint: problema principale, intercettazione (3), interferenza (2)
::
Alla base di tutti i problemi delle WLAN sta la **natura non confinabile del segnale radio**:
##### Di intercettazione
Questi sono risolti di solito con sistemi [[4.1 AAA|AAA]], di cui molti sono basati su crittografia:
- Rischio di <u>intercettazione</u> non autorizzata dei dati trasmessi (se non protetti),
- Rischio di <u>alterazione</u> dei dati trasmessi,
- <u>Accessi non autorizzati</u> che possono causare danni (*spoofing*) o ridurre la banda agli utenti legittimi.
##### Di interferenza
Questi sono prevenibili effettuando <u>ricognizioni preventive</u> dell'area interessata alla WLAN per rilevare altre WiFi adiacenti. Inoltre bisogna anche prestare attenzione ai **canali di frequenza** usati. Quindi:
- <u>Sovrapposizione di segnali</u> provenienti da <u>altre WLAN</u>,
- Presenza di dispositivi che generano <u>onde dello stesso spettro della WLAN</u> (tipo un <u>microonde</u>).

### Componenti
Hint: componenti WLAN (4)
::
La progettazione di una WLAN prevede di norma i seguenti componenti:
- **Host wireless**: un dispositivo in cui viene eseguito del sw che richiede l'accesso alla WLAN,
- **WAP** (*Wireless Access Point*), un dispositivo in grado di:
  - Implementare funzioni di controllo dell'accesso (SSID + password) per consentire o negare agli host l'accesso alla rete,
  - Cifrare il traffico wireless,
  - Scambiare le chiavi di cifratura con l'host wireless proteggendo il traffico di rete,
  - Inviare richieste ad un servizio AAA (se implementato).
  Inoltre un WAP può essere un:
  - AP (*Accesso Point*),
  - *Wireless router*: integra funzioni di AP e router, spesso da anche firewall, switch, DNS e DHCP,
  - *Wireless WAN router*: un *wireless router* con una porta WAN e implementa NAT.
- **Servizio AAA**: un server che centralizza le funzioni di autenticazione, autorizzazione e *accounting*. Spesso su usa il protocollo **[[4.1 AAA#RADIUS|RADIUS]]** (*Remote Authentication Dial-In User Service*) per tali scopi.
  Sul server (RADIUS) ci sono tutte le info per le attività [[4.1 AAA|AAA]], organizzate in *directory* accessibili con il protocollo **LDAP** (*Lightweight Directory Access Protocol*).
- **LAN cablata**: la rete interna.

### Considerazioni
Hint: considerazioni su varie esigenze (7)
::
Progettando una WLAN, è necessario fare delle considerazioni su:
###### Preesistenza di LAN wired
In questo caso è <u>sufficiente acquistare gli AP da collegare alla LAN</u> opportunamente.
###### Esistenza di WLAN adiacenti
In caso di <u>esistenza di altre WLAN adiacenti</u>, sarà necessario scegliere un **canale trasmissivo non sovrapposto** a quelli già in uso.
###### Alimentazione degli AP
Gli AP dovrebbero essere installati in <u>posizioni elevate</u> (vicino a soffitto), tuttavia è difficile che vi siano prese elettriche in quei punti. Perciò bisogna prevedere che gli AP abbiano il supporto della tecnologia **PoE** (*Power over Ethernet*), cosicché la corrente arrivi dallo stesso cavo Ethernet.
###### Caratteristiche delle zone da coprire
Le **prestazioni** delle WLAN dipendono dall'<u>intensità del segnale</u> emesso dagli AP, però qualsiasi **ostacolo** tra l'host e l'AP <u>attenua il segnale</u> (per riflesso o assorbimento); perciò gli AP vanno messi in punti alti e - schermati possibile.
Nel caso in cui non sia possibile coprire bene tutta l'area con 1 AP, se ne possono usare <u>molteplici</u> connettendoli alla LAN.
Nel caso non sia possibile connettere gli altri AP alla LAN, si possono usare degli ***Wireless Range Extender***, ripetitori wireless che lavorano nello stesso canale dell'AP associato (entrambi devono supportare lo standard WDS, *Wireless Distribution System*).
###### Tipo di app e traffico
Fondamentale è valutare il fabbisogno di banda necessario. 2 situazioni frequenti sono:
- **Uso aziendale**: (per email, accesso web e stampanti) in cui il traffico è <u>discontinuo</u>, con <u>picchi intensi ma brevi</u>. Se il n° di host non è eccessivo, basta anche 1 solo AP con alte prestazioni, per gestire adeguatamente i *burst* di traffico.
- **Uso personale**: (per download, streaming, file sharing e accesso a database) in cui il traffico è <u>continuo e regolare</u> e tutte le <u>stazioni competono</u> per l'accesso alla rete. Qui va ampliata il + possibile la banda disponibile, perciò si installeranno + AP (non *range extender*) operanti su canali non sovrapposti per massimizzare le capacità della rete.
###### Numero di stazioni da servire
- Se il n° di host da servire è <u>elevato</u> (tipo in luoghi pubblici per fornire hotspot pubblici), è meglio usare <u>+ AP</u> operanti in canali diversi per aumentare la banda e ripartire il traffico.
- Se il n° di host da servire è + <u>contenuto</u> e questi sono <u>vicini</u> tra loro, forse è + appropriata una <u>LAN wired</u>.
###### Esigenze di sicurezza
Bisogna valutare il <u>tipo di dati</u> da gestire per scegliere gli standard di crittografia + adatti alla situazione. 
Poi ogni AP genera *beacon frame* per informare gli host vicini del proprio SSID e, in caso non si voglia questo comportamento, è possibile disattivare tale funzione.