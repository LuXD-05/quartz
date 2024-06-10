### Rete a 1 zona

Esempio: una rete in cui le comunicazioni sono iniziate <u>solo</u> dall'interno verso dei server esterni, tipicamente reti domestiche (vedi [[3 NAT#UPnP e P2P|UPnP]]).

In questo nella rete vi sono gli host interni, connessi tramite switch o alberi di switch (eventualmente con *access point*), ad un firewall che filtra il traffico e che lo inoltra al default gateway; il quale ha 2 interfacce:

- Una per la **LAN**: avente un **IP locale**,
- Una per la **WAN**: associata ad un **IP pubblico**.

![](https://i.imgur.com/VUZ0O1z.png)

### Rete a 2 zone

Esempio: una rete in cui vi siano delle risorse o dei servizi pubblici (server accessibili da internet) che gli utenti devono poter accedere in sicurezza dall'esterno (impedendo l'accesso alle risorse private); questo è un tipico contesto aziendale.

In questo caso la rete è divisa in 2 zone:

##### DMZ

La **DMZ** (*DeMilitarized Zone*) o rete perimetrale, è una rete intermedia tra la rete esterna insicura (internet) e la rete interna sicura (intranet). In pratica è una subnet in cui vengono esposti dei servizi all'esterno, rendendoli pubblici e accessibili.

La DMZ è quindi insicura (al pari di internet) ed al suo interno si mettono servizi pubblici quali: web server, FTP server, DNS server, mail server... Le DMZ inoltre si configurano come delle VLAN (o *subnet*).

###### Accesso

Una DMZ è accessibile quindi sia dall'interno sia dall'esterno, ma da essa sono consentite connessioni solo verso l'esterno e non verso l'interno. 

Questo si fa per prevenire intrusioni dall'esterno in caso di compromissione di un host nella DMZ (siccome è esposto, non gli è permesso accedere all'interno).

##### Zona interna sicura

Qui invece sono posti i servizi che gestiscono info interne, riservate e critiche, tipicamente organizzati in db o file repository.

#### Dividere le 2 zone

Per separare la DMZ dalla rete interna ci sono 2 modi:

- ***3-port firewall***: viene usato un singolo firewall a (almeno) 3 porte che filtra i pacchetti indirizzando i pacchetti per la DMZ ad essa, mentre il resto (traffico sicuro) alla rete interna. 

  ![](https://i.imgur.com/FuatoQc.png)

- **Doppio firewall**: è un design + sicuro rispetto al design *3-port firewall* (in caso di attacco un hacker dovrebbe hackerare 2 firewall) in cui c'è un 1° firewall che viene implementato tra internet e la DMZ (che consente solo i pacchetti esterni alla DMZ) e poi un 2° firewall posizionato tra la DMZ e la rete interna (che consente solo il traffico sicuro indirizzato dalla DMZ alla rete interna).

  ![](https://i.imgur.com/GGO23p2.png)

