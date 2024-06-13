# Livello rete

### IPsec

(*IP security*) è un insieme di protocolli che fornisce sicurezza al protocollo IP garantendo autenticazione e riservatezza. (Siccome è di livello rete, è usabile sia da TCP sia da UDP).

Si usa per trasferire dati in modo sicuro in internet senza usare linee dedicate (con VPN).

###### Implementazioni

IPsec può essere implementato:

- Sui **terminali** (*host-to-host*):

  ![](https://i.imgur.com/i0x688d.png)

- Su dei ***security gateway*** (*gateway-to-gateway*):

  ![](https://i.imgur.com/aD6ZiH5.png)

### Modalità di incapsulamento

##### Transport mode

La ***transport mode*** è una modalità usata per le comunicazioni *host-to-host* in cui i pacchetti mantengono l'*header* IP originale e sono trattati a livello rete come se non avessero IPsec. Quindi:

- IPsec è implementato sugli host (*security endpoints*) per sicurezza *end-to-end*.
- Viene aggiunto un *header IPsec* tra l'*header* IP originale (quindi IP sorgente e destinatario rimangono in chiaro) e il *payload* (TCP o UDP) da proteggere.

![](https://i.imgur.com/24lIone.png)

##### Tunnel mode

La ***tunnel mode*** è usata + spesso per comunicazioni *gateway-to-gateway* e prevede la creazione di un nuovo *header* contenente (oltre all'*header IPsec*) gli IP dei *security endpoints* indipendentemente dal fatto che questi coincidano con i *data endpoints*. Quindi:

- IPsec è implementato nei *security gateway* (non è necessario negli host),
- Il pacchetto IP originale viene completamente (*header* + *payload* nascosti) incapsulato in un altro avente IP sorgente e destinatario dei *security gateway*.

![](https://i.imgur.com/10AvG2z.png)

### Protocolli di sicurezza

##### AH

(*Authentication Header*), fornisce autenticazione e integrità dell'intero pacchetto IP tramite un *header AH* (tranne per alcuni campi dell'*header*, tipo flags, fragment offset, TTL e header checksum siccome sono modificati dai nodi intermedi).

![](https://i.imgur.com/nCxIxfG.png)

Qui tutto è sempre autenticato (ma niente è cifrato).

##### ESP

(*Encapsulation Security Payload*), fornisce invece autenticazione ed integrità solo al *payload* + *header ESP* (non a "IP" in *transport* o "new IP" in *tunnel*), mentre garantisce riservatezza al *payload*.

Oltre all'*header ESP*, aggiunge un *trailer* composto da un *ESP trailer* (autenticato e riservato) e da una *ESP auth* (in chiaro).

![](https://i.imgur.com/XNEZT3v.png)

- ESP in *transport mode*: IP sorgente e destinatario originali sono in chiaro,
- ESP in *tunnel mode*: IP sorgente e destinatario originali sono crittografati.

# Livello trasporto

### TLS

**SSL/TLS** (*Secure Socket Layer / Transport Layer Security*) si colloca <u>tra TCP e il livello applicazione</u>. (**SSL** è vietato dalla IETF in quanto ritenuto **insicuro** dalla versione TLS 1.3 del 2018).

**TLS** è un protocollo crittografico per la trasmissione sicura dei dati su una rete e va usato sopra un <u>protocollo affidabile</u>: **TCP**. Quindi:

- **TLS cifra** i dati ricevuti dal protocollo applicativo trasmittente e li passa al TCP trasmittente,
- **TLS decifra** i dati ricevuti dal TCP ricevente e li passa al protocollo applicativo ricevente.

![](https://i.imgur.com/v6mmuoe.png)

###### Garanzie

TLS garantisce:

- **Riservatezza**: cifra i dati con chiave di sessione scambiata con algoritmi a chiave asimmetrica,
- **Autenticazione**: client e server si autenticano tramite algoritmi a chiave pubblica e scambiandosi certificati,
- **Integrità**: funzioni *hash* generano *digest* a lunghezza fissa dei messaggi.

##### HTTPS

Se HTTP effettua una connessione TCP diretta con il server su porta 80, HTTPS (*HTTP secure* o *HTTP over SSL/TLS*):

- Usa porta 443,
- Prima avviene il ***TLS handshake*** (effettuata connessione sicura col server) con cui si scambia la chiave di sessione,
- Poi ***TLS Record Protocol*** crea un pacchetto coi dati dell'applicazione comprimendoli, aggiungendovi un MAC (*Message Authentication Code*), autenticandoli, cifrandoli con la chiave di sessione e infine passandoli a TCP.

### DTLS

(*Datagram TLS*) è un protocollo molto simile a TLS ma che lavora sopra UDP. Inoltre è usato soprattutto per l'IoT insieme a [[3.2 CoAP]].

![](https://i.imgur.com/NyF6xTK.png)

