# PID
- Su word creare stile formattazione personalizzato per titolo e titolo paragrafo, poi impostare un sommario
- Indice automatico, tag fatti, copertina e tabelle pronti
- 1a pag copertina con titolo grande + tabella in fondo alla pagina
- 2a pag con sommario 
# PBS
Serve ad avere un quadro completo di tutte le fasi del progetto, rappresentandole gerarchicamente (per fare una cosa devo svolgerne un'altra prima, da basso verso alto) ed è una struttura ad albero, dall'alto verso il basso, composta da nodi. I nodi che derivano da un altro formano il 100% del nodo da cui derivano. 

# OBS
Inseriamo tutte le persone che hanno attività e compiti nel progetto + esterni che interagiscono (si dovranno togliere persone, perché in un ambiente non collaborano tutti, pero magari ci sono anche persone esterne).
###### ES segreteria scolastica
OBS (Va fatto come schema gerarchico, con PM sopra da cui derivano gli altri)
- Project Manager (PM)
	- Sviluppatori (SV)
	- DBA
	- Sistemisti (SYS)
	- Ufficio Personale (UP)
# RACI
Responsabilità di tipo:
**R** --> **operativa**, ha un compito da fare, concreto [OBBLIGATORIO]
**A** --> **esclusiva** (1 sola per attività) e questa approva il lavoro di R (autorizza e approva i lavori) [OBBLIGATORIO]
**C** --> figura/risorsa che viene consultata (gli si chiede qualcosa e risponde attivamente) [FACOLTATIVO]
**I** --> Risorsa che viene informata (dello Stato Avanzamento Lavori o SAL) e magari dice che fare [FACOLTATIVO]
###### Come assegnare R e A
Ci può essere una risorsa sia R sia A (eventualmente) quando devo sia fare sia autorizzare (generalmente sono separate, siccome se un esterno fa entrambi, poi al destinatario del lavoro magari non va bene siccome il R/A fa come vuole).
Prendiamo il PBS/WBS:
Analisi esigenze, progetto esigenze, sviluppo, db, arch rete. Chi fa che cosa?
- Analisi esigenze (R/A = PM) (C = UP)
- Progettazione esigenze (R = SV, DBA, SYS) (A = PM)
- Sviluppo (R = SV) (A = PM)
- Database (R = DBA) (A = PM)
- Arch rete (R/A = SYS)
Questa dovrebbe essere grafica, con l'OBS in gerarchia sopra e a sinistra le fasi del PM (o attività) che si collegano con delle linee verticali che scendono dall'OBS e dove si incontrano ci sono le responsabilità.

### TABELLA RACI
Team di progettazione

| (Attività)         | SV  | PM  | DBA | SYS | UP  |
| ------------------ |:---:|:---:|:---:|:---:|:---:|
| Analisi esigenze   |  C  | R/A |  I  |  I  |  C  |
| Progetto esigenze  |  R  |  A  |  R  |  R  |     |
| Sviluppo           |  R  |  A  |  I  |  I  |     |
| Progetto DB        |  I  |     | R/A |  I  |     |
| Progetto arch rete |  I  |     |  I  | R/A |     |
PASSI:
1) OBS 
2) RACI (grafica)
3) RACI (tabella)

1 riga di sommario per OBS
1 riga di sommario per RACI (both)

# CPM
?
# PERT
(Project Evaluation & Review Technique) è un metodo statistico per determinare i tempi delle attività di progetto ( applicabile anche a costi) 

Se CPM stimava tempi attraverso 1 solo valore, il PERT usa 3 valori: 
- durata pessimistica --> minor tempo necessario x un'attività
- durata ottimistica --> maggior tempo necessario x un'attività
- durata probablie --> stima migliore di quanto tempo serve per un'attività
L'uso di questi ci permette di valutare progetti con una durata ad elevata incertezza. PERT è + preciso e affidabile, ma anche + complesso.

Nel 1900, industrializzazione crea la necessità della gestione di progetto per processi produttivi ma anche per guerra, tutto considerando il fattore tempo. (Tipo Gantt nel 1917)
Nel 1958 è inventato il PERT da una ditta di consulenza ingegneristica per l'ufficio progetti speciali della marina USA.
L'obiettivo era di ridurre i tempi e i costi per la progettazione e la costruzione di sottomarini nucleari armati con missili Polaris, coordinando migliaia di fornitori e subappaltatori (delegati dall'appaltatore)

Quando scegliere il PERT rispetto al CPM? quasi mai se non in situazioni di vincoli di tempo molto stretti o quando serve una stima molto precisa e affidabile in progetti molto critici e dove l'unità di tempo ha impatto significativo.
(In ambito costruzione inutile perché non serve la precisione all'ora per progetto che richiede settimane)

Vantaggi:
- consente analisi approfondita di risorse, prestazioni e progetto PRIMA del suo avvio
- Aiuta a promuovere la responsabilità perche tutti hanno ruoli e tempi molto ben definiti
- Mitiga meglio le incertezze e considera i contrattempi

Svantaggi:
- Nodi e grafici mostrano le aspettative ma non lo stato in tempo reale
- Non sempre l'effort devoluto nel calcolo del PERT è motivato (se ci metto 10 g per fare il PERT ma poi nn serve ho perso 10 giorni)
- Non di facile lettura per i non addetti ai lavori (come anche il CPM però)

Nella tabella (oltre a stime ottimistica, pessimistica e probabile) è aggiunto il valore atteso, una media pesata dei valori delle 3 stime dei tempi.
b = durata pessimistica
m = durata probabile
a = durata ottimistica
Il tempo atteso (te) si fa: te = (b + 4m + a) / 6
Poi il calcolo procede calcolando [sigma], data da: (b - a) / 6
(Poi servirà [sigma]^2)

Bisogna fare poi il reticolo PERT, come il CPM, ma con 2 differenze:
- Parte da 0
- Non considera più i +1 e -1 passando da un'attività all'altra

La tabella risultante (con le varie stime, il valore atteso, [sigma] e [sigma]^2)
Si fa con tutte le attività evidenziando quelle critiche (margine scorr a 0)

z = (dl - td) / rad(somm([sigma]^2))
dl = Deadline
td = Somma delle durate della attività critiche
(denom) = radice della sommatoria delle [sigma]^2 della attività critiche

Grafico distribuzione normale standardizzata (campana di Gauss)
z è un punto individuato sull'asse x della campana di gauss, per cui stiamo dentro ai tempi del progetto se siamo prima di z, altrimenti no
Per questo troviamo l'intervallo di valori (che vanno bene) con:

f(z) = $\int_{-\infty}^{z} \left(\frac{1}{\sqrt{2\pi}}\right) e^{-\frac{1}{2} t^2} \, dt$

Per calcolare la normale standardizzata (?) 
Sulle tavole pitagoriche, prendiamo il valore della 1a cifra sulle righe e il valore della 2a cifra sulle colonne 
(tipo con 0,89 --> 8a riga e 9a colonna, quella è la percentuale di riuscita entro una certa deadline a fare il prog)

Standard:
- 100 - 80 --> progetto parte
- 80 - 60 --> solitamente il progetto va ottimizzato, senza possibilmente toccare il contratto
- < 60/50 --> richiesta una rettifica dei paletti contrattuali (nn si può fare, cliente: o aumenti la DL o chiedi altro)