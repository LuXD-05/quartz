---
public: true
edited_seconds: 800
modified_at: 02/04/2024 11:11:15
---
### Ridondanza
Questa è il + grande difetto dei db. Perché:
1) Occupa spazio inutile,
2) Intralcia le SELECT 
3) Rende i dati duplicati e inconsistenti, che non portano informazione.
### Normalizzazione
Questa è un processo che normalizza un db definendo delle regole (modificando lo schema logico del db) al fine di evitare inconsistenze dei dati ed anomalie nelle operazioni.
##### Steps
1) Analisi della realtà d'interesse,
2) [[Progettazione concettuale]],
3) [[Progettazione logica]],
4) [[Normalizzazione]],
5) Schema fisico.
### Anomalie
##### Anomalie d'inserimento
Se nell'inserire un nuovo record si è costretti a inserire info già presenti nel db. Conseguenza: **ridondanza**.
Esempio: in una tabella ordini mista a clienti (sbagliata), non è pensabile far inserire al client ogni volta l'indirizzo a cui spedire il pacco perché magari lo scrive ogni volta in modo diverso. Quindi l'indirizzo deve essere presente in una tabella a parte e la selezione deve essere possibile mediante una ComboBox.
##### Anomalie di cancellazione
Se nel cancellare un record si è costretti a cancellare info che possono ancora essere utili nel db. Conseguenza: **inconsistenze**.
Esempio: in una tabella ordini mista a clienti (sbagliata), cancellando una riga si cancella anche il cliente.
##### Anomalie di aggiornamento
Se dovendo aggiornare un record si è costretti ad aggiornarne altri. Conseguenza: **performance basse**.
Esempio: in una tabella ordini mista a clienti (sbagliata), se l'indirizzo di un cliente cambia allora bisogna cambiarlo in tutte le altre tuple.