#SQL (Structured Query Language) è il linguaggio di interrogazione db. Ha delle **keywords** case **insensitive** (come nomi di tabelle e attributi) al contrario del resto da cui è composto.
# Sottolinguaggi
### DDL
(O Data Definition Language), comprende le istruzioni usate per definire e modificare le strutture dati.
##### CREATE
Comando usato per la creazione di:
- ###### DATABASE
```sql
CREATE DATABASE db;
```
- ###### TABLE
```sql
CREATE TABLE Studenti (
	id int PRIMARY KEY AUTO_INCREMENT,
    nome varchar(20) NOT NULL,
    nascita date CHECK(nascita > "1900-01-01"), 
    fkClasse int,
    FOREIGN KEY (fkClasse) REFERENCES Classe(id) ON UPDATE SET NULL ON DELETE SET NULL
) ENGINE = InnoDB;
```        
##### USE 
Comando usato per indicare che d'ora in poi si usa un certo db per eseguire le query.
```sql
USE my_db;
```
##### ENGINE
Usato in istruzioni `CREATE`, indica il **motore di memorizzazione** con cui viene creata la tabella. (Se non specificato si usa quello di default del DBMS). Può essere di 2 tipi:
- **MyIsam**, motore che gestisce tabelle per max 256TB (veloce, grande capacità ma non gestisce relazioni, quindi no FK)
- **InnoDB**, motore che permette di implementare vincoli e associazioni (controlli dei dati immessi, un po' più lento e gestisce fino a 65TB)
##### DESCRIBE 
Descrive il parametro passato.
##### DROP
Elimina qualcosa, che può essere: `TABLE "..."`, `DATABASE "..."`, ...
##### ALTER
Usato principalmente su `TABLE`, ne modifica la struttura attraverso diverse operazioni:
- ###### MODIFY 
Modifica il tipo di una colonna (ma non il nome).
```sql
ALTER TABLE Studenti MODIFY nome varchar(30) NOT NULL;
```
- ###### RENAME 
Modifica il nome di una colonna (ma non il tipo). Può anche modificare il nome della tabella con `ALTER TABLE Studenti RENAME TO Alunni;`.
```sql
ALTER TABLE Studenti RENAME COLUMN nome TO nominativo;
```
- ###### CHANGE
Può modificare il tipo di una colonna, ma necessita anche di cambiarne il nome.
```sql
ALTER TABLE Studenti CHANGE nome nominativo varchar(30) NOT NULL;
```
- ###### ADD
Aggiungere una colonna alla tabella (e ne definisce eventuali constraint) o un constraint a una colonna. `AFTER` indica dopo quale colonna aggiungere la nuova, mentre `FIRST` permette di aggiungerla in prima posizione, altrimenti di default viene aggiunta alla fine.
```sql
ALTER TABLE Studenti ADD cognome varchar(30) NOT NULL AFTER nome;
```
Si possono anche aggiungere constraints a colonne già esistenti (esempio `CHECK` su data):
```sql
ALTER TABLE Studenti ADD CONSTRAINT chk_constraint_1 CHECK(nascita > "1900-01-01");
```
- ###### DROP
Elimina una colonna o un constraint di una colonna dalla tabella.
```sql
ALTER TABLE Studenti DROP COLUMN cognome;
```
Si possono anche eliminare constraints a colonne già esistenti (esempio `CHECK` su data):
```sql
ALTER TABLE Studenti DROP CONSTRAINT chk_constraint_1;
```
### DML
##### INSERT INTO 
Inserisce dati all'interno di una tabella. I campi `AUTO_INCREMENT` sono omissibili. Si possono rimuovere anche tutti i nomi di colonna, ma lì i valori vanno scritti tutti e in ordine. Si possono anche inserire record multipli in una volta sola, ma separati da ",".
```sql
INSERT INTO Studenti (nome, nascita, fkClasse) 
VALUES
    ('bulzo', '2000-01-01', 1),
    ('gil', '2000-01-01', 2),
    ('dis', '2000-01-01', 3);
```
##### UPDATE
Aggiorna l'attibuto con il valore dato (se non applicate restrizioni aggiorna tutta la colonna). Si possono aggiornare più campi di un record in una volta sola, ma separati da ",".
```sql
UPDATE Studenti SET nome = 'gil', nascita = '2000-01-01' WHERE 1;
```
##### DELETE FROM 
Elimina record da una tabella in base a una restrizione (se omessa, tutti i record saranno eliminati).
```sql
DELETE FROM Studenti WHERE 1;
```
### QL
##### SELECT 
Seleziona certi record di certe tabelle in base a certe condizioni.
```sql
SELECT * FROM Studenti;
```
Si possono selezionare gli attributi che si vogliono. In questo caso si usa * per selezionarli tutti, altrimenti vanno scelti e scritti gli attributi separati da "," come per le tabelle.
- ###### WHERE
Esegue una restrizione sui campi delle tabelle su cui avrà effetto la query.
```sql
SELECT * FROM Studenti WHERE nome = 'gil';
```
- ###### AS
Definisce l'alias di una tabella o attributo. L'alias verrà riportato come nome di colonna della `SELECT` se selezionato e si riferirà sempre a una sola tabella univocamente.
```sql
SELECT s.nome, s.nascita FROM Studenti AS s;
```
- ###### DISTINCT
Permette alla query di selezione di ritornare solo valori distinti dei campi selezionati.
```sql
SELECT DISTINCT fkClasse FROM Studenti;
```
# Constraints
Detti anche vincoli interrelazionali, sono i vincoli che vengono posti agli attributi per gestirne i valori assunti. Comprendono:
##### PRIMARY KEY
Indica che il campo è PK. Implica anche UNIQUE e NOT NULL (a volte anche AUTO_INCREMENT).
##### AUTO_INCREMENT
Incrementa in automatico il campo (che deve essere int) quando si inserisce una tupla (rende innecessario specificarlo nelle query INSERT).
##### UNIQUE
Indica che il campo non ammette duplicati nel dominio.
##### NOT NULL
Indica che il campo non accetta valori NULL.
##### DEFAULT()
Indica tra () il valore che il campo assumerà se scritto "default" al posto del valore del campo specificato nelle query di `INSERT` (anche NULL).
##### CHECK()
Indica tra () l'espressione logica che il campo deve soddisfare.
##### FK
Indica che il campo è una FK. La sintassi è:
```sql
FOREIGN KEY Studenti.fkClasse REFERENCES Classe(Classe.id) ON UPDATE NO ACTION ON DELETE NO ACTION; 
```
`ON UPDATE` e `ON DELETE` hanno 4 tipi di azioni:
- **NO ACTION**, (in MySQL = a `RESTRICT`), è di default e verifica che non siano violate le relazioni tra le tabelle impedendo di cancellare o modificare la FK di una *parent row* se ha associate 1 o + *child rows*.
- **SET DEFAULT**, imposta il valore referenziato al default di colonna quando la *parent row* referenziata viene eliminata o modificata.
- **SET NULL**, imposta il valore referenziato a NULL quando la *parent row* referenziata viene eliminata o modificata.
- **CASCADE**, propaga i cambiamenti fatti sulle *parent rows* alle *child rows*, per esempio se una *parent row* è modificata allora lo saranno anche le *child* che referenzia; mentre se viene eliminata, anche le *child* che referenzia verranno eliminate.
# Datatypes e altro
##### Di testo
- **char** --> 1 char fisso da 1 byte,
- **char(N)** --> N char fissi da N byte,
- **varchar(N)** --> stringa lunga max N byte.
##### Di numero
- **int**,
- **smallint**,
- **real**,
- **numeric**,
- **float/double(n_cifre, precisione)**.
##### Di byte
- **BLOB** --> stringa binaria (non oltre 4KB).
##### Di tempo
- **date** --> solo data, scritta come stringa tra "", formato: "yyyy-MM-dd", 
- **time** --> solo tempo, scritto come stringa tra "", formato: "hh:mm:ss",
- **datetime** --> data e ora, scritti come stringa tra "", formato: "yyyy-MM-dd hh:mm:ss",
- **timestamp** --> timestamp come in PHP, formato: "yyyy-MM-dd hh:mm:ss.xxxxxx".
##### Altro
- **enum(...)** --> campo lista che accetta solo i tipi specificati, tipo menu a tendina (campi specificati possono essere qualsiasi cosa),
- (Anche possibile creare il proprio tipo di dato).
### Operatori e altre keywords
Gli operatori logici sono i soliti `AND`, `OR` e `NOT`; e vanno scritti in maiuscolo per intero. Esistono poi altri operatori particolari:
- ###### BETWEEN
Verifica se il valore di un attributo è compreso tra 2 valori (`BETWEEN` funziona con numeri e date):
```sql
WHERE Studente.eta BETWEEN 15 AND 20;
```
- ###### LIKE
Verifica se il valore stringa di un attributo rispetta la condizione specificata; tipo una regex:
```sql
WHERE Studente.nome LIKE "Mar%*";
```
I caratteri jolly sono:
"\*" --> (in alcuni motori anche "\_"), sostituisce 1 solo carattere,
"%" --> sostituisce una sequenza di caratteri di lunghezza indefinita.
- ###### IN
Verifica se il valore di un attributo è contenuto in un certo range:
```sql
WHERE Studente.nome IN("Mario", "Maria", "Gilberto");
```
### Altro
- Le stringhe vanno inserite tra apici (singoli o doppi),
- Segno uguale è singolo (=), non doppio (\==),
- Segno diverso è "!=" o "<>".
### Preverifica
Pianta(id, NomeComune, NomeScientifico, TipoPianta, Origine, Descrizione, fkSpecie) 
Famiglia(id, NomeFamiglia, Descrizione) 
Specie(id, fkFamiglia, NomeSpecie, Descrizione, Pericolosità) 
Ambiente(id, NomeAmbiente, Descrizione, (elevazione)) 
PiantaAmbiente(id, fkPianta, fkAmbiente) 
- Scrivere l'istruzione SQL che consente la creazione della tabella Specie, sapendo che la pericolosità può assumere solo valori compresi tra 1 e 5. Eventuali operazioni su tale tabella devono far ricadere gli effetti anche nelle tabelle correlate 
- Modificare il nome della tabella Pianta in arbusto 
- Modificare l'attributo descrizione in Famiglia in modo che possa contenere massimo 2000 caratteri 
- Modificare la tabella Ambiente inserendo l'elevazione rispetto al mare, la presenza di questo valore è obbligatoria 
- Eliminare l'attributo elevazione dalla tabella Ambiente 
- Eliminare tutte le piante della specie gelsomino. 
- Assegnare a tutte le rose l'origine Gallarate 
- Inserire i dati di 3 ambienti 
- Visualizza tutte le piante con il nome comune "Rosa"
- Visualizza tutte le piante appartenenti alla famiglia "Liliaceae" 
- Visualizza tutte le piante che possono crescere in un ambiente "boscoso" 
- Visualizza tutte le piante con nome scientifico che contiene la parola "rosea" 
- Visualizza quante piante ci sono per ogni tipo di pianta 
- Visualizza per ogni famiglia il numero di specie presenti, in ordine discendente 
- Visualizza il numero di piante che crescono ad altezze comprese tra 1000 e 2000 metri 
- Visualizza le specie più pericolose per l'uomo 
- Visualizza il numero di piante di cui si conosce l'origine che crescono nelle paludi e possono causare danni all'uomo.