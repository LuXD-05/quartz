# Esami

### Modalità d'esame

Prova in 2 parti (per ognuna delle quali va conseguito un punteggio di almeno 18):

1) Domande di teoria: (generalmente 6), valgono 1/3 della prova.
2) Esercizi: (generalmente 3), valgono 2/3 della prova.

##### Risoluzione

In generale potrebbero esserci esercizi con documenti di specifica dei requisiti, perciò è necessario:

1) Leggere e identificare gli oggetti/tabelle del sistema,
2) Sottolineare e risolvere le ambiguità/indecisioni,
3) Separare bene le frasi di specifica dei dati da quelle di specifica delle operazioni,
4) Costruire la base di dati e poi realizzarne le operazioni richieste.

###### ER

1) Identificare le entità principali ed associarle in modo tale da comporre uno scheletro,
2) Semplificare e raggruppare i requisiti dal documento collegati allo scheletro,
3) (Per ogni sotto-problema o gruppo di requisiti) creare i vari sotto-schemi,
4) Integrare il tutto nello scheletro,
5) Verificare se lo schema rispetta tutti i requisiti del documento.

###### Query

# Esercizi

### 1 - Domande teoria

##### 1 - Intro

###### 1 - Quali affermazioni sono vere? 

L'indipendenza dei dati permette:

- di scrivere programmi senza conoscere le strutture fisiche dei dati,
- di modificare le strutture fisiche dei dati senza dover modificare i programmi che accedono alla base di dati,
- di formulare interrogazioni senza conoscere le strutture logiche dei dati.

###### 2 - Quali affermazioni sono vere? 

Il fatto che le basi di dati siano condivise favorisce:

- l'efficienza dei programmi che le utilizzano,
- permette di ridurre ridondanze e inconsistenze,
- rende necessaria la gestione del controllo dell’accesso.

###### 3 - Quali affermazioni sono vere? 

Il fatto che le basi di dati siano persistenti:

- ne garantisce l'affidabilità,
- favorisce l'efficienza dei programmi.

###### 4 - Quali affermazioni sono vere? 

- la distinzione fra DDL e DML corrisponde alla distinzione fra schema e istanza,
- il DML permette di interrogare il db <u>e anche</u> di modificarlo,
- il DDL permette di specificare la struttura del db <u>ma non</u> di modificarla,
- esistono linguaggi che includono sia istruzioni DDL sia istruzioni DML (quali?).

###### 5 - Altro

Illustrare (supponendo di rivolgersi ad un non esperto) le caratteristiche fondamentali dei db e il loro ruolo nei SI.

Illustrare il concetto di indipendenza dei dati.

##### 3 - SQL

###### 6 - Es DDL

![](https://i.imgur.com/mHxa5bk.png)

Specifica le istruzioni per creare queste tabelle, imponendo questi vincoli:

- Impossibile cancellare un corso se il corso è in orario,
- Cancellare un corso comporta la cancellazione di tutti i suoi iscritti,
- Se un organizzatore del corso viene rimosso, è possibile fare in modo che tale corso non sia assegnato a nessuno (momentaneamente),
- Se un istruttore viene rimosso, i corsi da lui tenuti devono avere codice = 7253,
- Il livello di default di corso è "intermedio".

###### 7 - Es DDL

Sempre dell'esercizio 6, in più:

- Modificare lo schema per memorizzare anche l'email degli iscritti (facoltativa) e degli istruttori (obbligatoria),
- Cambiare il livello di default di corso a "base".

###### 8 - Es join

![](https://i.imgur.com/mHxa5bk.png)

![](https://i.imgur.com/bDaf7NV.png)

###### 9 - Es subquery

![](https://i.imgur.com/Q4GNEjJ.png)

1\) Trovare il dipartimento che spende in totale il massimo in stipendi,

2\) Trovare id dipartimento e n° degli impiegati che guadagnano + di 40000 €, per ogni dipartimenti con + di 5 impiegati,

3\) Trovare il nome degli impiegati che non lavorano in un progetto controllato dal dipartimento 5.

Soluzioni circa da pagina 47 della slide sulle subquery.

###### 10 - Es generale

![](https://i.imgur.com/BlFLFIb.png)

![](https://i.imgur.com/4OX0D3d.png)

1\) Trovare i cantanti che hanno inciso brani (sia) nel 2022 e (sia) nel 2023,

2\) Trovare i cantanti che non hanno mai registrato una canzone da solisti,

3\) Trovare il numero di serie delle "collezioni di successi" (dischi in cui tutte le canzoni sono cantate da 1 solo cantante e in cui almeno 3 registrazioni sono precedenti all'anno di pubblicazione del disco).

Soluzioni circa da pagina 110 delle slide sulle subquery.

