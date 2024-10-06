---
public: true
modified_at: 16/06/2024 15:14:18
edited_seconds: 270
---
### Affidabilità
Hint: ARQ, caratteristiche (3)
::
Un protocollo è **affidabile** quando ritrasmette pacchetti alterati/persi, quindi detto **ARQ** (*Automatic Repeat reQuest*). Un protocollo ARQ garantisce l’affidabilità tramite:
1) **Rilevamento degli errori**: con un campo di controllo (*checksum* o *CRC* in base al protocollo),
2) **Feedback dal ricevente**: che informa il trasmettitore sull’esito della ricezione, di 2 tipi:
   - **ACK**: *positive acknowledgement*,
   - **NAK**: *negative acknowledgement*.
3) **Ritrasmissione** dei **pacchetti** riscontrati con NAK.
<!--SR:!2024-04-30,2,200-->

### Protocollo send-and-wait
Hint: cosa fanno, se si perde un pacchetto in rete, trasmettitore/destinatario POV, duplicazione dei pacchetti in rete
::
I protocolli ***send-and-wait*** o ***stop-and-wait***, prevedono che il trasmittente <u>invii</u> (*send*) <u>un pacchetto e si ponga poi in attesa</u> (*wait*) <u>del riscontro dal ricevente</u> (**ACK** se checksum/CRC corretti, altrimenti **NAK**). 
##### Countdown timer
Nel caso di <u>perdita del pacchetto in rete</u> (ricevente non riceve) si usa un ***countdown timer*** che parte dopo l’invio del pacchetto.
Il <u>trasmittente</u> è in attesa del **riscontro** e:
- Se questo arriva **prima** che il timer scada, il timer è resettato e si gestisce il riscontro,
- Se scade il timer e questo **non** è ancora **arrivato**, il pacchetto è ritrasmesso.
Il <u>destinatario</u>, ricevuto il pacchetto e verificato che riscontro inviare, è in attesa del **prossimo pacchetto** e:
- Se questo arriva prima che il timer scada, il timer è resettato e si gestisce il nuovo pacchetto,
- Se scade il timer e questo non è ancora arrivato, il riscontro è ritrasmesso.
###### Duplicazione dei pacchetti in rete
In entrambe le situazioni è possibile che un pacchetto abbia invece preso un percorso lungo o lento, quindi nasce il problema della **duplicazione dei pacchetti** in rete, che si risolve con **[[3 TCP#Sequence number|n° di sequenza]]** dato a ogni pacchetto, cosicché il ricevente capisca se lo ha già ricevuto (duplicato) o no. 
(Nei protocolli *send-and-wait* il ricevente aspetta <u>1 pacchetto alla volta</u> perché il trasmittente non può trasmettere se prima non arriva l’ACK o scade il *countdown timer*, quindi i <u>pacchetti numerati solo con 0 o 1</u>).
<!--SR:!2024-04-30,2,200-->

### Protocolli sliding window
Hint: cosa prevedono, tipo di trasmissione, risolvere perdite (go-back-N e selective-repeat)
::
I protocolli ***sliding window*** prevedono di <u>trasmettere N pacchetti</u> (*N* = apertura della finestra) <u>prima di attendere riscontri</u>. 
##### Trasmissione
Gli <u>N</u> pacchetti sono riscontrati in base al <u>tipo di trasmissione</u>, che può essere:
- **Half-duplex**: il ricevente deve aver ricevuto tutti gli *N* pacchetti prima di inviare il riscontro,
- **Full-duplex**: il ricevente può inviare riscontri senza dover attendere l’arrivo di tutti i pacchetti (se il riscontro è inserito in un <u>pacchetto di dati</u> reinviato al trasmittente, si parla di ***piggybacking***, “portare in groppa”).
##### Tecniche
Capita che alcuni degli *N* pacchetti trasmessi si **perdano** o arrivino **alterati**, per risolvere ciò ci sono 2 tecniche:
###### Go-back-N
Il ricevente, quando riceve un <u>pacchetto errato</u> (per CRC/checksum) o <u>fuori sequenza</u> (qualche pacchetto precedente si è perso), **ignora i successivi** e reinvia al trasmittente un ACK del pacchetto ***N-1*** (pacchetti precedenti validi) che comporterà la ritrasmissione dei pacchetti a partire dal pacchetto ***N***. 
Riscontrando il pacchetto *N-1* è <u>implicito il riscontro positivo (ACK) di tutti i pacchetti precedenti (N-1, N-2…)</u>, ciò è detto ***acknowledgement cumulativo***.
###### Selective repeat
Il ricevente <u>accetta e memorizza tutti i pacchetti ricevuti corretti</u> (sia in sequenza sia non) poi agisce in 2 modi:
- Manda un **ACK** specifico per ogni **pacchetto** ricevuto **corretto**,
- Manda un **NAK** per i singoli **pacchetti corrotti** o **fuori sequenza**.
(Diversi modi provocano problemi tra trasmittente e ricevente; ricevente deve anche pensare al riordino pacchetti fuori sequenza).
<!--SR:!2024-04-30,2,200-->