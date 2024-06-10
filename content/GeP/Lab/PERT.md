### Storia

Nel 1900, industrializzazione crea la necessità della gestione di progetto per processi produttivi ma anche per guerra, tutto considerando il fattore tempo. (Tipo Gantt nel 1917)

Nel 1958 è inventato il PERT da una ditta di consulenza ingegneristica per l'ufficio progetti speciali della marina USA.

L'obiettivo era di ridurre i tempi e i costi per la progettazione e la costruzione di sottomarini nucleari armati con missili Polaris, coordinando migliaia di fornitori e subappaltatori (delegati dall'appaltatore)

### Cos'è?

Il PERT (o *Project Evaluation & Review Technique*) è un metodo statistico per determinare i tempi delle attività di progetto ( applicabile anche a costi) 

##### Valori

Se CPM stimava tempi attraverso 1 solo valore, il PERT usa 3 valori: 

- durata pessimistica --> minor tempo necessario x un'attività
- durata ottimistica --> maggior tempo necessario x un'attività
- durata probablie --> stima migliore di quanto tempo serve per un'attività

L'uso di questi ci permette di valutare progetti con una durata ad elevata incertezza. PERT è + preciso e affidabile, ma anche + complesso.

##### PERT vs CPM

Quando scegliere il PERT rispetto al CPM? quasi mai se non in situazioni di vincoli di tempo molto stretti o quando serve una stima molto precisa e affidabile in progetti molto critici e dove l'unità di tempo ha impatto significativo.

(In ambito costruzione inutile perché non serve la precisione all'ora per progetto che richiede settimane)

##### Vantaggi

- Consente analisi approfondita di risorse, prestazioni e progetto PRIMA del suo avvio
- Aiuta a promuovere la responsabilità perche tutti hanno ruoli e tempi molto ben definiti
- Mitiga meglio le incertezze e considera i contrattempi

##### Svantaggi

- Nodi e grafici mostrano le aspettative ma non lo stato in tempo reale
- Non sempre l'effort devoluto nel calcolo del PERT è motivato (se ci metto 10 g per fare il PERT ma poi nn serve ho perso 10 giorni)
- Non di facile lettura per i non addetti ai lavori (come anche il CPM però)

### Procedimento

##### 1) Calcolo tempi e sigma

Nella tabella (oltre a stime ottimistica, pessimistica e probabile) è aggiunto il **valore atteso**, una media pesata dei valori delle 3 stime dei tempi.

b = durata pessimistica

m = durata probabile

a = durata ottimistica

Il tempo atteso (te) si fa: te = (b + 4m + a) / 6

Poi il calcolo procede calcolando [sigma], data da: (b - a) / 6

(Poi servirà [sigma]^2)

##### 2) Disegno PERT

Bisogna fare poi il reticolo PERT, come il CPM, ma con 2 differenze:

- Parte da 0
- Non considera più i +1 e -1 passando da un'attività all'altra

##### 3) La distribuzione normale standardizzata

Innanzitutto si hanno:

z = (dl - td) / rad(somm([sigma]^2))

dl = Deadline

td = Somma delle durate della attività critiche

(denom) = radice della sommatoria delle [sigma]^2 della attività critiche

Nel grafico della distribuzione normale standardizzata (campana di Gauss), z è un punto individuato sull'asse x, per cui stiamo dentro ai tempi del progetto se siamo prima di z, altrimenti no

Per questo troviamo l'intervallo di valori (che vanno bene) con:

$$f(z) = \int_{-\infty}^{z} \left(\frac{1}{\sqrt{2\pi}}\right) e^{-\frac{1}{2} t^2} \, dt$$

Per calcolare la normale standardizzata si usano delle tavole pitagoriche e su queste prendiamo il valore della 1a cifra sulle righe e il valore della 2a cifra sulle colonne (tipo con 0,89, 8° riga e 9° colonna). Il risultato * 100 sarà la % di riuscita del progetto entro una certa deadline.

##### Standard

- 100 - 80 --> progetto parte
- 80 - 60 --> solitamente il progetto va ottimizzato, senza possibilmente toccare il contratto
- < 60/50 --> richiesta una rettifica dei paletti contrattuali (nn si può fare, cliente: o aumenti la DL o chiedi altro)
