### I capisaldi

I 3 capisaldi di progetto sono la pianificazione di costi, tempi e risorse (in ordine). Per i tempi non si possono usare le tecniche usate per costi e risorse; però le tecniche usate possono comunque essere reiterate + volte, però la pianificazione non è un processo standardizzabile.

### Pianificazione delle risorse

La pianificazione di risorse consiste nell'elencare le risorse necessarie per ogni attività della WBS. Con questo si ottiene la **RBS** (*Resource Breakdown Structure*).

##### Categorie di risorse

Le risorse sono divisibili in diverse categorie:

- Lavoro, che può essere:
	- Diretto: UR che partecipano alla produzione di un prodotto / a contatto con esso.
	- Indiretto: UR che supportano indirettamente la realizzazione del *deliverable* (tipo formatori).
	- Amministrativo: UR che svolgono attività specifiche di progetto, a capo di contabilità, amministrazione o altre risorse.
- Materiali: risorse che fanno parte del prodotto finale.
- Attrezzature: risorse materiali che non fanno parte del prodotto finale ma che sono necessarie per la sua realizzazione. Valutate in quota di ammortamento (nel senso che questi costi vanno ammortizzati, al contrario di quelli delle risorse materiali che sono fatti pagare tutti al cliente), per cui si distribuisce il costo invece di addebitarlo tutto insieme (questi costi sono suddivisi di solito in + periodi contabili, oppure, per esempio: camion = 1000€ e clienti = 20, quindi ogni cliente paga 50€).
- Altro = altri costi fissi necessari per la realizzazione del prodotto finito.

### Pianificazione dei costi

Questa fase successiva prevede:

##### Analisi dei costi

Questa è strettamente correlata alla pianificazione di tempi e risorse, è quasi sempre completamente responsabilità del PM ed è la fase + critica: se fallisce, fallisce il progetto.

Con questa si ottiene il budget di progetto, ovvero la previsione della spesa di progetto totale (preventivo). Sono però necessari dei controlli periodici (*timenow*).

##### Stima dei costi

Si possono usare 3 tecniche per stimare i costi:

- Per analogia (c'è una risorsa con costo simile, quindi si stima per somiglianza: affidabile ma necessita di eventuali correzioni).
- Parametrica (informazioni oggettive derivate dal mercato sono raccolte e vengono parametrizzate per il contesto).
- A 3 punti, calcolabile in 2 modi:
	- Con la distribuzione normale standardizzata (tipo PERT), con i tempi: atteso, ottimistico e pessimistico,
	- Con (il metodo) beta, che tiene conto di impatto min (m), impatto max (M) e probabile (p) di una risorsa, da cui il costo.

###### Processi di stima

Sono uguali quelli di risorse e tempi, e si usano 2 tecniche:

- Bottom-up (+ comune, prevede la somma delle sotto-attività).
- Top-down (prevede la ripartizione dei costi in sotto-componenti).

### Realizzazione capitolato tecnico

(è risulato di tutto ciò) Prendere attività, individuare risorse per realizzarla, realizzare disegno che fa capire la struttura della nostra rete

tab excel con: attività e risorse di cui si ha bisogno con: classificazione(lavoro, materiali, attrezzatura, altro) con anche la sottoclassificazione (ES: UR per apparati rete? lavoro diretto) + descrizione + unità/qtà (ES: ore/uomo, pezzi)

Tenere da conto che poi serve preventivo per i costi. è anche possibile inserire colonne aggiuntive, tipo il peso di un componente se è significativo e serve

x stimare risorse? si prende la raci e si vedono le responsabilità assegnate

(In excel mettere filtri per suddividere costi e risorse per attività, per classificazione, ... così da distinguere meglio i dati)

LIVELLI DI ACCURATEZZA

ballpark (da approfondire)

budget (affidabile)

definitivo (più precisa)

CALCOLO

per n risorse individuate bisogna trovare la quantità e il prezzo unitario

Costo (ci) = quantità (qi) * prezzo unitario (pui)

