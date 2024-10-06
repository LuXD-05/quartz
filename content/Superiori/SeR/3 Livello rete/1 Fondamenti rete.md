---
public: true
modified_at: 28/04/2024 11:22:37
edited_seconds: 80
---
### Fondamenti
Hint: intro, addressing, encapsulation, routing, de-encapsulation
::
Il livello rete esegue una consegna **host-to-host** dei pacchetti. Tra gli host ci possono essere 1 o + reti (IPv4 o IPv6).
##### Addressing
Gli host sono configurati con un **indirizzo univoco** (**IP**) per identificarli in rete (unico anche nelle inter-reti).
##### Encapsulation
Il livello rete **incapsula i dati da inviare** in **pacchetti** a cui è aggiunto un **header** con **IP mittente e destinatario**.
##### Routing
Il livello rete **dirige i pacchetti a destinazione**. Il **destinatario** può essere:
- Il **mittente stesso** (*loopback*),
- Un **host locale** (sulla stessa rete del mittente),
- Un **host remoto** (su una rete diversa (remota) da quella del mittente). Qui i pacchetti sono inviati a un **router** che sceglie il percorso migliore per arrivare a destinazione.
##### De-encapsulation
Quando il pacchetto arriva al **livello rete** del **destinatario**, questo controlla l’**header IP** del pacchetto; e se l’IP di destinazione corrisponde col suo, l’header è rimosso e il pacchetto è deincapsulato a **PDU 4** e passato a livello **trasporto**.
<!--SR:!2024-05-01,3,220--> 

### Modelli di rete
Hint: circuito virtuale, datagram
::
##### A circuito virtuale
(Detto anche ATM, *Asynchronous Transfer Mode*), è un modello **orientato alla connessione** dove, prima di comunicare, tra i nodi va setuppato un **circuito virtuale** che verrà utilizzato durante la comunicazione. Può essere:
- **Permanente**, tipo connessioni preconfigurate e dedicate,
- **Temporaneo**, basato su servizi “*a chiamata*” e scartato al termine dello scambio dei dati.
##### A datagram
Qui i pacchetti sono immessi in rete senza handshake e raggiungono il destinatario con un IP destinazione. È:
- ***Connectionless***: nessuna connessione è stabilita prima di inviare un pacchetto,
- ***Best-effort***: protocollo IP è <u>inaffidabile</u> perché non è garantita la consegna del pacchetto,
- ***Media independent***: indipendente dal mezzo su cui viaggia. Pacchetto è portato in frame diversi in base al link.
<!--SR:!2024-05-01,3,220-->

#### MTU e Frammentazione
::
L'**MTU** (*Maximum Transmission Unit*) è la dimensione max per i pacchetti trasportabili su ciascun link. È imposto dal livello **datalink** e se i frame che arrivano a un router sono **> dell’MTU** del link successivo, il router li **frammenterà** in dimensioni adatte. Il processo di frammentazione però causa **latenza**.
<!--SR:!2024-05-01,3,220-->

### Router
Hint: porte ingresso, porte uscita, switching fabric, routing processor
::
##### Porte di ingresso
Hanno una coda detta **buffer di ingresso** dove i segnali prelevati dal link sono prima **decodificati in binario**, e poi **organizzati in frames**. Dei frame integri (con *FCS* ok) e diretti al router ne viene estratto il payload.
##### Switching fabric
**Connette** fisicamente le porte di **ingresso** a quelle di **uscita**.
##### Porte di uscita
**Memorizzano e trasmettono i frame** ottenuti dalla *switching fabric*. Per farlo il buffer datalink di uscita esegue il **framing**, ovvero crea frame giusto per il link e inserisce il datagram IP livello 3 in esso.
##### Routing processor
Fa **algoritmi di routing** e sceglie il percorso dei pacchetti aggiornando le corrispondenze della ***routing table***, di 2 tipi:
- **Rotte statiche**: fisse, create da amministratori di rete.
- **Rotte dinamiche**: dinamiche, gestite in base ai cambiamenti di rete con dei ***routing protocols***.
<!--SR:!2024-05-01,3,220-->