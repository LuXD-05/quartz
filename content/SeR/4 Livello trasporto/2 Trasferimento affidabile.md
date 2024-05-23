### Affidabilità

Un protocollo è **affidabile** quando ritrasmette pacchetti alterati/persi, quindi detto **ARQ** (*Automatic Repeat reQuest*). Un protocollo ARQ garantisce l’affidabilità tramite:

1) **Rilevamento degli errori**: con un campo di controllo (checksum o CRC in base al livello del protocollo),
2) **Feedback dal ricevente**: che informa il trasmettitore sull’esito della ricezione, di 2 tipi:

   - **ACK**: ***positive** acknowledgement*,

   - **NAK**: ***negative** acknowledgement*.

3) **Ritrasmissione** dei **pacchetti** riscontrati con NAK.

### Protocollo send-and-wait

I protocolli ***send-and-wait*** o ***stop-and-wait***, prevedono che il trasmittente invii (***send***) un pacchetto e si ponga poi in attesa (***wait***) del riscontro dal ricevente (**ACK** se checksum/CRC corretti, altrimenti **NAK**). Nel caso di perdita del pacchetto in rete (ricevente non riceve) si usa un ***countdown timer*** che parte dopo l’invio del pacchetto.

Il <u>trasmittente</u> è in attesa del **riscontro** e:

- Se questo arriva **prima** che il timer scada, il timer è resettato e si gestisce il riscontro,
- Se scade il timer e questo **non** è ancora **arrivato**, il pacchetto è ritrasmesso.

Il <u>destinatario</u>, ricevuto il pacchetto e verificato che riscontro inviare, è in attesa del **prossimo pacchetto** e:

- Se questo arriva prima che il timer scada, il timer è resettato e si gestisce il nuovo pacchetto,
- Se scade il timer e questo non è ancora arrivato, il riscontro è ritrasmesso.

In entrambe le situazioni è possibile che un pacchetto abbia invece preso un percorso lungo o lento, quindi nasce il problema della **duplicazione dei pacchetti** in rete, che si risolve con **n° di sequenza** dato a ogni pacchetto, cosi che il ricevente capisca se lo ha già ricevuto (duplicato) o no. (Nei protocolli ***send-and-wait*** il ricevente aspetta **1 pacchetto alla volta** perché il trasmittente **non può trasmettere** se prima non arriva **l’ACK** o scade il ***countdown* *timer***, quindi i pacchetti numerati solo con **0** o **1**).

### Protocolli sliding window

I protocolli ***sliding window*** prevedono di trasmettere ***N* pacchetti** (**N** = **apertura della finestra**) prima di attendere riscontri. Il momento in cui sono riscontrati gli *N* pacchetti dipende dal tipo di trasmissione, che può essere:

- **Half-duplex**: il ricevente deve aver ricevuto tutti gli *N* pacchetti prima di inviare il riscontro,
- **Full-duplex**: il ricevente può inviare riscontri senza dover attendere l’arrivo di tutti i pacchetti (se il riscontro è inserito in un **pacchetto di dati** reinviato al trasmittente, si parla di ***piggybacking***, “portare in groppa”).

Capita che alcuni degli *N* pacchetti trasmessi si **perdano** o arrivino **alterati**, per risolvere ciò ci sono 2 tecniche:

##### Go-back-N

Il ricevente, quando riceve un pacchetto errato (CRC/checksum) o fuori sequenza (qualche pack prima perso), **ignora** i pacchetti **successivi** e reinvia al trasmittente un riscontro del pacchetto ***N-1*** (sequenza di pacchetti precedente) che comporterà la ritrasmissione di tutti i pacchetti a partire dal pacchetto ***N***. Riscontrando il pacchetto *N-1* è implicito il riscontro positivo (ACK) di tutti i pacchetti precedenti (N-1, N-2…), ciò è detto ***acknowledgement cumulativo***.

##### Selective repeat

Il ricevente accetta e memorizza tutti i pacchetti ricevuti corretti (sia in sequenza sia non) poi agisce in 2 modi:

- Manda un **ACK** specifico per ogni **pacchetto** ricevuto **corretto**,
- Manda un **NAK** per i singoli **pacchetti corrotti** o **fuori sequenza**.

(Diversi modi provocano problemi tra trasmittente e ricevente; ricevente deve anche pensare al riordino pacchetti fuori sequenza).

