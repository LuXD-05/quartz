---
public: true
modified_at: 28/04/2024 11:50:42
edited_seconds: 30
---
### ICMP
Hint: intro, header (3), messaggi di errore e di informazione
::
L'**ICMP** (*Internet Control Message Protocol*) è un protocollo che funge da **supporto** ad **IP** in quanto **segnala errori o scambia informazioni**; ma **non esegue correzioni** ai messaggi, perciò **non rende affidabile IP**. Esistono **ICMPv4** e **ICMPv6**.
##### Header ICMP
I messaggi ICMP sono incapsulati e inviati come pacchetti IP. Il loro header conta 8 byte di dati, che sono:
- **Tipo**: indica la **categoria** del messaggio ICMP.
- **Codice**: da un'ulteriore **descrizione** al messaggio (Esempio: tipo 3 indica destinazione non raggiungibile e i codici specificano: 0 = rete destinazione | 1 = host destinazione | 3 = porta destinazione ...).
- **Checksum**: verifica l'**integrità** dei dati.
###### Messaggi di errore
- ***Destination_Unreachable***: indica che la destinazione non è raggiungibile (per vari problemi: l'host è spento / l'host rifiuta i pacchetti per errori coi protocolli / il <u>pacchetto deve essere frammentato ma il flag DF = 1</u> ...).
- ***Redirect***: quando un gateway intermedio si accorge che il prossimo gateway è già nella stessa subnet del mittente (segnala una via + breve).
- ***Time_Exceeded***: indica che il TTL del pacchetto è stato decrementato a 0, per cui non può + essere inoltrato.
###### Messaggi di informazione
- ***Echo_Request***: il mittente chiede al destinatario di reinviare indietro lo stesso pacchetto.
- ***Echo_Reply***: la destinazione che ha ricevuto l'*echo request* rimanda indietro il pacchetto ricevuto.
- ***Timestamp*** e ***Timestamp_Reply***: (funzionano come i precedenti e) sono usati per sincronizzare i clock di 2 dispositivi.
<!--SR:!2024-04-30,2,200-->

### Ping
Hint: cos'è, funzionamento, usi (3)
::
Il **ping** è un comando che invia **4 pacchetti ICMP** a un host per verificarne la raggiungibilità in rete e fa uso di *echo request* ed *echo reply*. Funzionamento:
1) **HostA** fa **ping** con **argomento HostB**,
2) Il programma manda una ***echo request*** al secondo da HostA a HostB,
3) Se HostB riceve le *echo request*, risponderà con ***echo reply*** (se HostA non riceve le *echo reply* entro un certo ***timeout***, verrà visualizzato un messaggio di richiesta scaduta).
##### Usi di ping
###### Loopback
Un ping a 127.0.0.1 (IPv4) o ::1 (IPv6) che ottiene risposta, indica che TCP/IP è installato e funzionante.
###### Ping locale
Pingando un altro host locale o il default gateway, un riscontro positivo indica che la rete + entrambi i dispositivi funzionano.
###### Ping remoto
Pingando un host remoto vi verifica, oltre la comunicazione locale, anche l'operatività del default gateway e degli altri router lungo il percorso.
<!--SR:!2024-05-01,3,220-->

### Traceroute
Hint: cos'è, funzionamento (+ RTT + router sovraccaricati)
::
Genera l'**elenco dei router** attraversati **per** raggiungere un **destinatario** e usa il campo **TTL** / **Hop Limit** + il messaggio ***Time_Exceeded*** ICMP.
##### Funzionamento
Delle ***echo request*** sono inviate in successione **incrementando ogni volta il TTL** / Hop Limit, cosicché i pacchetti **scadano ad ogni router** ritornando varie informazioni al mittente, fino a raggiungere la **destinazione** finale che rimanda una *echo reply*.
Con **Traceroute** si ottiene l'RTT o ***Round-Trip Time***, ovvero il tempo necessario ad un pacchetto per raggiungere la destinazione e tornare indietro.
Quando l'*echo reply* non torna entro un certo **tempo limite**, il traceroute scrive "**\***" in console per indicare che il router è **sottodimensionato/sovraccaricato**. Con questo, traceroute può trovare link problematici lungo i percorsi.
<!--SR:!2024-05-01,3,220-->