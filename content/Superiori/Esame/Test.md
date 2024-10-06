---
edited_seconds: 4230
modified_at: 29/04/2024 16:00:19
---
# 1st try
### Analisi
###### FISICO
Città con centro storico e fuori InfoPoint per acquisto biglietti
Centro storico ha monument e art
###### BIGLIETTI
Ogni biglietto contiene password valida solo x il giorno
3 tariffe:
- "base": da pagina base per ogni POI
- "media": come "base" + 3 pagine avanzate scelte fra i POI
- "piena": come "media" ma comprende tutte le pagine avanzate di tutti i POI
###### DISPOSITIVI 
Tablet rilasciati da InfoPoint previa consegna documento identità o n° carta di credito
Solo tablet possono accedere a pagine web
###### PAGINE WEB
2 pagine:
- Pagina base: avente video di 1 minuto in ita e sub eng + max 3 immagini del POI + didascalia in italiano e inglese.
- Pagina avanzata: con video di 5 minuti in 7 lingue (compreso ita) + 20ina di immagini con relativa descrizione (circa 500 char) in 7 lingue (compreso ita).
Accesso a pagine web solo presso POI 
Accesso a pagine web solo dopo inserimento pw a "inizio di visita" 
###### DATI
Salvarli su server

### Traduzione in requisiti
##### Rete
Città media = max 500 turisti al giorno
RCS = Rete centro storico (dimensioni???)
\> RM = Rete POI monumentali
\> RA = Rete POI artistici
RIP = rete InfoPoint (dimensione città = MAN/WAN)

### Chiarire
Pagine web visualizzabili dopo inserimento pw "all'inizio della visita" (si intende entrata nel centro storico? oppure quando???)

### Testo prova
##### Intro
Al fine di realizzare ... bisogna chiarire certe cose:
...

##### Rete (e geografia/posizionamento)
Si suppone che in città media ci saranno dai 500 ai 1000 turisti al giorno.
Considerando che molti sono famiglie, si suppone che famiglie prendono 1 tablet a testa (perché si figuri lasciarlo in mano a bambini), quindi si prevedono max 512 host giornalieri.
(fare 1024 per stare sicuri?)
RCS ha 2 subnet: RA (arte) e RM (monumenti). Poi c'è anche RIP (InfoPoint) diffusi per la città.
Si suppongono 6 RA, 6 RM (6 luoghi d'arte e 6 monumenti) + una 30ina di IP sparsi per il paese
(Va bene? o troppo?)

##### Comunicazione (e protocolli)

##### Dati (e salvataggio)

##### Clienti 
Arrivano a InfoPoint, comprano biglietto con certa tariffa (dando carta identità/credito) e ottengono tablet, inseriscono la pw sul tablet (QUANDO?) (accesso bloccato finché non in range di POI), vanno nel POI (in qualche modo: BLE, BT, WiFi...) tablet riconosce che è nel POI e abilita la relativa pagina web ... utente finisce e tablet mostra maps con InfoPoint + vicino (se carta credito) o InfoPoint originale (se carta identità).

##### 

# 2nd try (real)
Siccome questo è un sistema che richiede una user/client interaction, è possibile suddividere la risoluzione della traccia in fasi temporali.
### Intro
Si vuole realizzare un sistema per favorire il turismo culturale in una città d'arte media, sviluppando a tal fine un'infrastruttura tecnologica che permetta agli utenti (descrizione di richieste) con 2 pagine web (descrizione di pagine) e biglietti con pw e 3 tariffe (descrizione tariffe).
Accesso a pagine web consentito solo se: fatto da minitablet fornito, fatto dopo l'inserimento di una pw sul biglietto, fatto solo nei pressi di un POI e fatto per la giornata in cui si acquista il biglietto ed entro la sua fine.
### Struttura
La città include al suo interno un centro storico con 6 attrazioni totali (3 monumentali e 3 artistiche), ognuna delle quali ... (sarà una VLAN separata? deve comunicare con le altre? se si come lo fa?...) ..., inoltre queste saranno interconnesse grazie ad un collegamento diretto per mezzo di cavi ethernet sotterranei verso l'edificio contenente i server centrali, il che si presuppone che si trovi relativamente vicino al centro storico, altrimenti sarà necessario prevedere un router intermedio tra i POI e la sala server per gestire meglio il traffico.
Ogni POI dovrà prevedere tanti indirizzi IP da assegnare ai visitatori quanta la capacità massima di visitatori nella zona. Per esempio, musei e POI artistici contenuti in spazi chiusi dovranno avere uno spazio di indirizzamento di almeno 100 host (o di più se il museo può ospitare + di 100 visitatori per volta), mentre per i monumenti, siccome si trovano in luoghi pubblici, sarà necessario prevedere un n° di indirizzi disponibili ancora maggiore data la presenza di luoghi pubblici di riposo e ristoro, giardini o panchine (fondamentale è prevedere eventuali mostre storiche importanti in questi luoghi, in quanto va considerato il rischio di un'affluenza > del normale e quindi di un possibile esaurimento dello spazio di indirizzamento).
Per quanto riguarda gli InfoPoint invece, essi sono situati all'esterno del centro storico e saranno direttamente connessi alla sala server sempre tramite cavi ethernet sotterranei o sopraelevati. 

In tutto ciò, siccome i tablet hanno bisogno di una connessione ad internet per visualizzare le pagine web, sarà necessario preconfigurarli e connetterli preventivamente alla rete WiFi del POI, così che questi se la ricordino. Inoltre il protocollo livello datalink CSMA/CD compierà un lavoro fondamentale nel separare i dispositivi nelle bande di frequenza 1, 6 e 11
### Fase 1: utente compra biglietto
Gli utenti ... si recheranno presso uno degli N InfoPoint ... per acquistare un biglietto. L'operatore dell'InfoPoint si accerterà che l'utente inserisca dati corretti (o li inserisce direttamente lui) e fornisca carta identità o di credito per la registrazione. Altro...
Dopo che tutto (e anche pagamento) è andato a buon fine, utente riceve biglietto con propria tariffa ... (caratteristiche e specifiche su biglietto) ... e il minitablet ... (caratteristiche minitablet, tipo geolocalizzazione, connessione ad internet, ...) ... Tablet è abilitato Google Maps cosicché si possano raggiungere I POI o gli InfoPoint seguendo una mappa predefinita (oltre a fotocamera abilitata). La password del biglietto è inserita 1 volta e vale per la giornata o finché tablet non è riconsegnato.
### Fase 2: utente visita POI
Dopo l'accensione del tablet, l'autenticazione e l'arrivo al POI, l'utente ... (in qualche modo accede alla pagina specifica e in qualche altro modo gli è detto se è possibile o no in base a vicinanza al POI o altro) (scannerizza QRcode con link sito web, NFC lo abilita alla pagina, geolocalizzazione sfruttata in qualche modo...) ...
L'utente ha quindi la possibilità di visitare il POI col tablet e la pagina desiderata.
I POI dovranno prevedere telecamere di sicurezza IP a circuito chiuso e altre guardie fisiche così da monitorare i tablet (geolocalizzati) per impedire furti o tentativi di hacking (prevedibile anche un softlock del dispositivo se si allontana dall'area o se non più raggiungibile con una LoRaWAN).
### Fase 3: terminata visita utente
Alla fine della visita, (il minitablet potrebbe presentare un sistema di spegnimento automatico in base a un tempo limite imposto all'inizio o nell'OS del dispositivo), sul minitablet appare (o utente clicca su una mappa) il percorso per arrivare all'InfoPoint + vicino (se carta di credito) o a quello iniziale (se carta identità).

### Altro
ToDo
- (A parte sistemare ancora meglio quanto scritto)
- Includere protocolli (o studiare un punto in cui inserirli: nel testo a cazzo? o in una sezione dedicata dopo?) e altra roba
- progettazione di rete va bene la precedente
- vedere per sicurezza e pagamenti
- boh





