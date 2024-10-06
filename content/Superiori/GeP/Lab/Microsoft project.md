---
public: true
modified_at: 20/06/2024 20:03:10
edited_seconds: 40
---
# Intro

### Gestionali
Quando do un gestionale a un cliente, bisogna considerarne:
##### Scalabilità
Il programma quanto è scalabile?
##### Licensing
Che costo è l'acquisto di licenze per un'azienda? Da calcolare in base al n° di utenti.
##### Modello
Se l'applicazione è *on premise* o *on cloud*. Unica differenza è che con l'*on cloud* è + semplice la collaborazione.

# Microsoft Project
...
### Composizione
...
### Foglio di lavoro
##### Composizione
...
##### Init
Da "Formato" del Gantt mostrare tutto.
##### Gestione attività
Inserire attività scrivendone i nomi in "Nome attività"
###### Sotto-attività
"ALT + SHIFT + freccia destra" per rendere 1 o + attività delle sotto-attività
##### Schedulazione attività
Si può fare:
- **Manualmente**: tramite il bottone in basso a sinistra
- **Automaticamente**: selezionando la colonna "Modalità attività" e poi cliccando in "programma automaticamente"
##### Precedenze
Si fa sulla colonna "Predecessori" e bisogna mettervi dentro l'**ID di Project**, ovvero il **n° della riga del progetto**.
Inoltre, è possibile parallelizzare le attività con:
- Doppio click su attività,
- Andare in tab "predecessori"
- Impostare "tipo" da inizio a inizio
- (eventualmente dargli un ritardo)
##### Calendario
Facendo doppio click sull'attività > scheda "Avanzate", è possibile cambiare il calendario dell'attività. Vedi poi [[#Scheda progetto]].
##### Attività critiche
In "Formato" del Gantt checkare "Attività critiche" e "Margine di flessibilità"
##### Milestones
Si può creare una ***milestone*** dando ad un'attività 0 giorni di durata.
Oppure, per forzare un'attività con una durata > 0 come *milestone*, doppio click su task > "Avanzate" > "Segna come attività cardine"

### Scheda progetto
##### Project information
Mostra informazioni sul progetto, come:
- Start date: data di inizio
- End date: disabilitata di default perché auto-calcolata in base alle attività
- Calendar: è modificabile il calendario di lavoro, con la possibilità di aggiungere eccezioni o modificarlo.
##### Modifica orario di lavoro
Qui è possibile cambiare tipo di calendario, fare altre cose e aggiungere eccezioni e definire le settimane lavorative.


# Diagramma di Gantt
### Cos'è
Diagramma che permette di rappresentare cronologicamente le attività e la loro durata.
### Composizione
Si presenta con barre orizzontali che rappresentano delle attività in un range di tempo e collegate con frecce.
##### Caratteristiche
...
##### Barre
- Bordi sfumati: attività di sola durata
- Colore scuro: attività automatiche
- Colore chiaro: attività manuali
- Con linea orizzontale interna: indica il completamento dell'attività
- Bianche: attività disabilitate
##### Riepiloghi 
Sono mezze barre parallele alle altre che comprendono delle sotto-attività?
- normale
- Grigio: riepilogo di progetto
##### Rombi
Sono milestones
##### Frecce
- Verso il basso: scadenza

### Gestione delle risorse
Per gestire le risorse, cliccare sulla 2a scheda da destra "Elenco risorse" in basso a destra.
##### Risorse
(In project mancano le risorse "attrezzatura" e le risorse di tipo "altro").
Per aggiungerle cliccare su "Aggiungi risorse" e selezionare il tipo di risorsa voluta.
##### Tipi
###### Lavoro
Facendo doppio click (€/h) si apre un form. Qui si può gestire
Noleggio muletto, ha un costo all'ora ma anche 
###### Materiali (contiene le risorse attrezzatura)
Non hanno a che fare con le ore (anche se calendario lo specifico per la sua disponibilità, non per il suo uso)
###### Costi (comprende le risorse altro)
In queste non è possibile impostare costi, in quanto non è possibile definirli a priori (il costo è definito al momento di allocazione della risorsa ma è comunque variabile). Esempi:
- Elettricità: 
- Subappalti (consulenze): 
##### Pool di risorse
Strumento che permette di gestire le risorse in un archivio condiviso tra + progetti.
In questo modo è possibile gestire l'allocazione delle risorse per evitarne la sovrapposizione dato che sono condivise tra + progetti.
###### Condivisione
Il modo migliore è con un file unico con solo risorse. Questo sarà poi condiviso con gli altri in questo modo:
Nel progetto principale, andare su "Pool di risorse" > "Consividi risorse" > selezionare il file di risorse desiderato.
##### Assegnazione


### Gestione dei costi
Quando si completano le attività, gli si assegna una % di completamento. Questo si fa andando in: 
"Attività" > "Diagramma di Gantt" > "Gestione attività"
Qui usciranno tutte le attività + le risorse assegnate.
##### EVM
Si possono aggiungere gli indici dell'EVM autocalcolati. Ciò si fa con:
"View" > "Tabelle" > "Altre tabelle" > "Costo realizzato"
##### Report
Si possono generare dei report, questo si fa con:
"Report" > "Relazioni grafiche" > "Relazione costo realizzato nel tempo" e bottone "Visualizza".