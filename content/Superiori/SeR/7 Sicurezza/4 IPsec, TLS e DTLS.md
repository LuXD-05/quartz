# Livello rete

### IPsec

(*IP security*) è un insieme di protocolli che <u>fornisce sicurezza al protocollo IP</u> garantendo <u>autenticazione e riservatezza</u>. (Siccome è di livello <u>rete</u>, è usabile sia da TCP sia da UDP).

Si usa per trasferire dati in modo sicuro in internet senza usare linee dedicate (con **VPN**).

###### Implementazioni

**IPsec** può essere implementato:

- Sui **terminali** (*host-to-host*):

  ![](https://i.imgur.com/i0x688d.png)

- Su dei ***security gateway*** (*gateway-to-gateway*):

  ![](https://i.imgur.com/aD6ZiH5.png)

### Modalità di incapsulamento

##### Transport mode

La ***transport mode*** è una modalità usata per le comunicazioni *host-to-host* in cui i pacchetti mantengono l'*header* IP originale e sono trattati a livello rete come se non avessero IPsec.

Quindi:

- **IPsec** è implementato sugli **host** (*security endpoints*) per sicurezza *end-to-end*.
- Viene **aggiunto un *header IPsec* tra l'*header* IP originale** (IP sorgente e destinatario rimangono <u>in chiaro</u>) **e il *payload*** (TCP o UDP) da proteggere.

![](https://i.imgur.com/24lIone.png)

##### Tunnel mode

La ***tunnel mode*** è usata + spesso per comunicazioni *gateway-to-gateway* e prevede la creazione di un nuovo *IP header* avente gli IP dei *security endpoints* (indipendentemente dal fatto che questi coincidano con i *data endpoints*) oltre all'aggiunta dell'*header IPsec*.

Quindi:

- **IPsec** è implementato nei ***security gateway*** (non è necessario negli host) con l'*IPsec header* tra il *new IP header* e il pacchetto originale completamente protetto,
- Il **pacchetto IP originale** viene (*header* + *payload* nascosti) **incapsulato in un altro avente IP sorgente e destinatario dei *security gateway*** (*new IP header*).

![](https://i.imgur.com/10AvG2z.png)

### Protocolli di sicurezza

##### AH

(*Authentication Header*), fornisce **autenticazione e integrità** dell'<u>intero pacchetto IP</u> tramite un ***header AH*** (tranne per alcuni campi dell'*header*, tipo flags, fragment offset, TTL e header checksum siccome sono modificati dai nodi intermedi).

![](https://i.imgur.com/nCxIxfG.png)

Qui tutto è sempre autenticato (ma niente è cifrato).

##### ESP

(*Encapsulation Security Payload*), fornisce invece **autenticazione ed integrità** a ***payload* + *header ESP*** (non a "IP" in *transport* o "new IP" in *tunnel*), mentre garantisce sempre **riservatezza** al *payload*.

Oltre all'*header ESP*, aggiunge un ***trailer*** composto da un ***ESP trailer*** (autenticato e riservato) e da una ***ESP auth*** (in chiaro).

![](https://i.imgur.com/XNEZT3v.png)

- ESP in ***transport mode***: IP sorgente e destinatario originali sono <u>in chiaro</u>,
- ESP in ***tunnel mode***: IP sorgente e destinatario originali sono <u>crittografati</u>.

# Livello trasporto

### TLS

**SSL/TLS** (*Secure Socket Layer / Transport Layer Security*) si colloca <u>tra TCP e il livello applicazione</u>. (**SSL** è vietato dalla IETF in quanto ritenuto **insicuro** dalla versione TLS 1.3 del 2018).

**TLS** è un <u>protocollo crittografico per la trasmissione sicura dei dati su una rete</u> e va usato sopra un protocollo affidabile: **TCP**. Quindi:

- **TLS cifra** i dati ricevuti dal protocollo applicativo trasmittente e li passa al TCP trasmittente,
- **TLS decifra** i dati ricevuti dal TCP ricevente e li passa al protocollo applicativo ricevente.

![](https://i.imgur.com/v6mmuoe.png)

###### Garanzie

TLS garantisce:

- **Riservatezza**: cifra i dati con chiave di sessione scambiata con algoritmi a chiave asimmetrica,
- **Autenticazione**: client e server si autenticano tramite algoritmi a chiave pubblica e scambiandosi certificati,
- **Integrità**: funzioni *hash* generano *digest* a lunghezza fissa dei messaggi.

### HTTPS

Se HTTP effettua una connessione TCP diretta con il server su porta 80, **HTTPS** (*HTTP secure* o *HTTP over SSL/TLS*) invece usa la porta **443** e prosegue poi grazie ai suoi 2 strati (in origine solo di SSL):

###### SSL Handshake

(Superiore, + vicino al livello applicativo), si occupa di stabilire una connessione sicura col server per mezzo di un ***TLS/SSL handshake*** (inizio <u>connessione e scambio parametri</u>, <u>auth di server e client con certificati</u>, <u>scambio di chiave di sessione</u>, <u>chiusura della connessione</u>).

###### SSL Record Protocol

(Inferiore, + vicino al livello trasporto), crea un <u>pacchetto coi dati</u> dell'applicazione <u>frammentandoli</u>, <u>comprimendoli</u>, aggiungendovi un <u>MAC</u> (*Message Authentication Code*), <u>autenticandoli, cifrandoli con la chiave di sessione e</u> infine <u>passandoli a TCP</u>.

### DTLS

(*Datagram TLS*) è un protocollo molto simile a TLS ma che lavora sopra **UDP**. Inoltre è usato soprattutto per l'IoT insieme a [[3.2 CoAP]].

![](https://i.imgur.com/NyF6xTK.png)

