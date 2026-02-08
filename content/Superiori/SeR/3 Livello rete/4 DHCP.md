### DHCP

Il **DHCP** (*Dynamic Host Configuration Protocol*) assegna automaticamente gli IP agli host di una LAN, senza interventi umani necessari e senza creare conflitti. Esso, oltre all'IP, fornisce anche delle informazioni aggiuntive:

- **Subnet mask**,
- **IP** del **default gateway**,
- **IP** del **DNS server locale**,
- Un ***lease time*** (di connessione quando il DHCP sta comunicando con un nuovo host nella LAN per assegnargli un IP).

Il DHCP è un **protocollo client/server** ed è detto ***plug-&-play*** o ***0-conf*** in quanto automatizza la configurazione degli host in LAN.

##### Funzionamento

Di base ogni host deve essere fornito di un **DHCP client** (altrimenti non funziona).

1) Quando un host si collega alla rete, cerca il **DHCP server** mandando (col DHCP client) un **DHCP DISCOVER** in UDP e porta 67 dall'IP "0.0.0.0" a "255.255.255.255" (broadcast limitato).
2) Il DHCP server (o anche + di 1) risponde con una **DHCP OFFER** (con IP destinazione sempre il broadcast limitato), che contiene: IP offerto, subnet mask, IP del default gateway, IP del DNS server locale e *lease time*.
3) Il DHCP client (eventualmente sceglie 1 DHCP server e) risponde con una **DHCP REQUEST** (con gli stessi parametri precedenti per accettarli).
4) Il DHCP server conferma quindi i parametri con un **DHCP ACK**, chiudendo la conversazione.

Il DHCP può dare lo stesso IP sempre allo stesso host. Viene dato il *lease time* perché la validità della connessione è limitata nel tempo (ma è rinnovabile).

#### DHCP Relay Agent

Il DHCP Relay Agent sostituisce il DHCP server in una rete assegnando gli IP agli host della stessa comunicando con un DHCP server di un'altra rete.

(foto)

