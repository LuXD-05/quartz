# Lezione 1

### Modelli di sviluppo del software

Molti non usano un modello di riferimento per lo sviluppo di software (metodologia ***code & fix***, cioè *coding* e poi *fixing* degli errori che si trovano prima o durante il test). Ora verranno presentati i 2 modelli principali, tuttavia non è necessario adattarsi ad essi, infatti esistono tante variazioni ed ogni azienda di solito tende a definire un modello di sviluppo personale.

> [!question] Quando è ideale NON usare un modello di riferimento per sviluppare software?
> **MAI**, è una cattiva pratica in quanto non prevede analisi preventiva o progettazione; e il correggere errori quando emergono causa inefficienza, bug frequenti e > costi.

##### Waterfall

Il "***waterfall***" è il modello di sviluppo tradizionale che suddivide il ciclo di vita del software in varie <u>fasi</u> che si susseguono una dopo l'altra "a cascata"; esso:

- <u>Identifica fasi</u> <u>forzando un progresso lineare da una all'altra</u>,
- <u>Non "permette" di ritornare indietro</u> (si può ma è costoso in termini di risorse, perciò serve un buon piano che non ammetta errori),
- <u>Standardizza gli output</u> (detti "***artefatti***") di ogni fase.

> [!info] Quando si usa il modello *waterfall* 
> - Quando le richieste sono certe e inalterabili (non ammessi cambi a metà del processo),
> - Quando clienti e utenti non sono coinvolti nello sviluppo (commissionano il lavoro e ricevono quanto prodotto anche se le loro esigenze cambiano).

###### Problema *waterfall*

Al giorno d'oggi, quando si sviluppa un software per un cliente, ci si trova spesso a dover modificare quanto fatto fino a un certo punto a causa di alterazioni nelle esigenze e richieste del cliente; perciò, la metodologia *waterfall* si dimostra troppo rigida per lo sviluppo efficiente di software in tali condizioni.

##### Agile

L'"***Agile***" è invece un modello più recente e creato per colmare le mancanze del *waterfall*, permettendo collaborazione col cliente e riallineamento del software in base alle nuove richieste dello stesso durante lo sviluppo; esso è:

- <u>Incrementale</u> (mira a costruire il software finito sviluppandone piccole parti per volta e in cicli rapidi, detti ***[[#Sprint]]***),
- <u>Cooperativo</u> (favorisce la comunicazione tra clienti e sviluppatori così da riallineare periodicamente gli interessi di entrambi),
- <u>Diretto</u> (semplice da imparare e modificare),
- <u>Adattivo</u> (permette cambiamenti anche all'ultimo).

> [!info] Quando si usa il modello *agile* 
> - Con richieste incerte o volatili,
> - Quando il cliente è incluso nel progetto e ne capisce,

###### *Sprint*

Il modello *agile* fa uso degli ***sprint***, cicli ripetuti di brevi durate (da 1 settimana a 1 mese) nei quali viene sviluppata una piccola parte del software (seguendo le solite [[#Fasi|fasi]]) per poi fare delle ***review*** alla fine di ogni *sprint* per capire a che punto si è e riallinearsi con le esigenze del cliente.

![](https://i.imgur.com/doRi7jY.png)

##### *Waterfall* vs *Agile*

Alla fine la differenza principale tra i 2 modelli è che:

- Il ***waterfall*** è una ***[blackbox](https://it.wikipedia.org/wiki/Modello_black_box)*** dall'inizio alla fine e necessita che le richieste siano comprese e stabili (cosa che accade molto raramente), 
- L'***agile*** è flessibile e trasparente, ovvero vi è la possibilità di effettuare controlli preventivi e di riallinearsi periodicamente con le esigenze volatili del cliente.

![](https://i.imgur.com/x2b8g5I.png)

### Fasi

![](https://i.imgur.com/2PVhbXI.png)

###### Feasibility study

Lo **studio di fattibilità** è fondamentale perché permette di <u>determinare se un progetto è fattibile e se ha senso farlo</u> tenendo da conto spese e potenziali profitti; tutto ciò che vi si trae è delineato nel **FSD** (*feasibility study document*), contenente problemi, soluzioni, costi, tempistiche e modello di sviluppo.

> [!info] Vincoli
> Lo studio di fattibilità è soggetto a dei **vincoli** (*pressure*): di **tempo** (si perde tempo a fare lo studio) e di **costi** (il cliente potrebbe non accettare l'offerta); a causa di ciò c'è la possibilità di tralasciare certe alternative migliori o di non assestare bene i rischi.

###### Requirement Analysis & Specification

L'**analisi delle richieste** porta ad identificare tutto il necessario per lo sviluppo del software nel **RASD** (*Requirements Analysis & Specification Document*), che deve essere preciso, completo, consistente, comprensibile e modificabile.

###### Design

La fase di ***design*** mira a progettare l'architettura del software (i suoi componenti e come interagiscono) al fine di <u>separare le responsabilità per favorire sviluppo parallelo</u>.

###### Coding & Unit Test

Ogni componente (**modulo**) è implementato con il linguaggio scelto e poi testato singolarmente dal programmatore.

###### Integration & System Test

I moduli testati sono integrati in sottosistemi e questi ultimi vengono ritestati; questo processo si ripete finché non si ottiene e testa il sistema completo.

###### Deployment

Col ***deploy*** si distribuiscono ed installano le soluzioni sui sistemi dei clienti e ci si accerta che funzionino correttamente.

###### Maintenance

L'ultima fase è il **mantenimento** delle soluzioni offerte, ovvero il supporto *post-deployment* del cliente e l'eventuale correzione di bug ed errori trovati dal cliente. Gli interventi durante questa fase sono di 3 tipi: **correttivi** (~20%), **adattivi** (~20%) e **perfettivi** (~50%).

> [!quote] Maintenance
> Per quanto riguarda errori che richiedono interventi correttivi, spesso se ne trovano tanti (soprattutto in moduli complessi) anche a causa di scarso *testing*; in più eliminare errori costa e può introdurne di nuovi (per questo grandi sistemi si stabilizzano ad un certo tasso di errori).
> Gli interventi adattivi e perfettivi invece sono fatti a causa di cambi di richieste e specifiche sbagliate o non dette fin da subito; per questo cambiamenti e mancanze vanno previsti, in questo modo si arriva a progettare software assicurando semplicità e bassi costi ad interventi per cambiamenti futuri.

---

Prossima lezione: [[2 - ISO 9126]]

