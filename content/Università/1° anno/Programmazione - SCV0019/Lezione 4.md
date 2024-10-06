---
modified_at: 01/10/2024 12:40:50
edited_seconds: 830
public: true
---
### Istruzioni condizionali
Esiste la possibilità di "scegliere" il flusso che il codice segue grazie ai **blocchi condizionali**, che si basano sulla validità o meno delle loro **condizioni**.
Il blocco che permette di scegliere cosa fare in base ad una condizione è:
```java
if (true)
{
	// Fai qualcosa se questa condizione è vera
}
else if (false)
{
	// Fai qualcosa se quest'altra condizione è vera
}
//...
else
{
	// Altrimenti fai qualcos'altro se le altre condizioni sono false
}

// oppure
if (true)
{
	if (true)
	{
		//...
	}
	else 
	{
		//...
	}
}

// oppure
if (true)
	// singola istruzione/condizione/ciclo...
else
	// singola istruzione/condizione/ciclo...
```
Tra le parentesi dell'`if` si inserisce una condizione che restituisce `true` o `false` e:
- Se la condizione è vera (ritorna `true`) allora esegue il 1° blocco di istruzioni,
- Altrimenti se la condizione è falsa (ritorna `false`) allora esegue l'altro blocco di istruzioni,
- (Eventualmente, in caso di presenza di 1 o più `else if (...)`, il codice nel suo blocco è eseguito se le condizioni precedenti sono tutte false).
Inoltre:
- Si possono innestare varie condizioni una dentro l'altra per verifiche più avanzate,
- Se un blocco condizionale è costituito da una sola istruzione in una sola riga, allora è possibile omettere le parentesi graffe (che sia un assegnamento o una funzione, però anche altre condizioni/cicli possono essere innestati, PERSINO scrivendo le graffe dato che l'istruzione "effettiva" è sempre di 1 riga, anche se non sembra),
- 