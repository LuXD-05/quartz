### Cos'è?

> [!important] Controllo di congestione
> (Servizio *host-to-network*), **capacità** di un trasmittente **di rallentare la trasmissione di pacchetti** quando si accorge che la **rete** (**router** di infrastruttura) **non riesce ad elaborarli con la dovuta velocità**.

La **congestione** riguarda la rete e i router di infrastruttura e si ha in 2 situazioni:

- All’**inizio** di essa, quando il **tempo di transito** nella rete (**RTT**) **aumenta**.
- All’**aumento** di essa, quando i **pacchetti si perdono** per il ***timeout*** (***countdown timer*** che **scade**).

  (Per esempio passando da collegamenti più veloci ad altri più lenti, tipo da gigabit ad ADSL, pacchetti rallentano).

Il controllo di congestione evita la perdita di pacchetti nei router per l’***overflow* dei loro buffer di ricezione o inoltro**.

### Approfondimento

TCP impone al mittente un **limite alla frequenza di invio dei segmenti** in base al **livello** “percepito” della **congestione**, grazie al **RTT** (usato dato che è a livello rete, di router e non trasporto). Il **throughput** (quantità di dati trasmessi nell’unità di tempo) di una comunicazione TCP è limitato da:

##### Finestra di congestione

Contiene la **qta di byte trasmissibili in 1 segmento** e cerca di non superare la capacità di rete. È **dinamica** e varia in base alla congestione della rete adattandosi ai sovraccarichi. Variabile ***cwnd***, è = al **n° di pacchetti inviabili per volta**.

##### Finestra di ricezione

Contiene la **qta di byte trasmissibili prima di** aspettare **1 ACK** e cerca di non superare la capacità del ricevitore di elaborare dati. Variabile ***rwnd***, è = al **limite max che la *cwnd* può assumere** (dimensione finestra ricezione destinatario).

#### Modalità di invio pacchetti

TCP usa le variabili *cwnd* (***congestion window***) e ***ssthresh*** (***slow-start threshold***, soglia/limite) per le modalità di invio pacchetti:

##### Slow start

All’avvio la ***cwnd*** è messa a **1** MSS e ad ogni **ACK positivo** (quindi non c’è congestione e c’è banda) il suo valore è **raddoppiato** (IF *cwnd* < *ssthresh* THEN ***cwnd* $*$= 2**) fino al valore max di ***ssthresh*** (fase ***slow start***).

##### Congestion avoidance

Superato l’***ssthresh***, si passa dal raddoppiamento all’**incremento** della cwnd (IF *cwnd* >= *ssthresh* THEN ***cwnd*++**), (fase ***congestion avoidance***).

Quando TCP rileva **perdite**, considera la rete **congestionata** e cambia **modalità** (ciò per **timeout** o **3 o + ACK duplicati**).

#### Rilevamento perdite

Si vede come in entrambi i casi i pacchetti spediti in 1 volta **aumentano**, di conseguenza aumenta anche il **n°** degli **ACK da riscontrare**. Quando la rete si congestiona, qualche pacchetto **si perde**; e ognuno ha il suo ***acknowledgement number***, che indica il **successivo *sequence number*** aspettato.

Quando alla destinazione arriva un pacchetto fuori sequenza, l’***acknowledgement number* rimane** quello **precedente** anche per i successivi, ad indicare che quello non è arrivato (ES: pack 6, ACK non c’è).

