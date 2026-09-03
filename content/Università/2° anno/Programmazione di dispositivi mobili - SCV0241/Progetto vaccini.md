# Progetto vaccini

### Todo

- [ ] 

### Specs

##### Traccia

###### Base

App dove utenti:

1\) inseriscono la propria terapia e i propri parametri clinici,

2\) vaccini vengono valutati (in base alla loro situa e a dati reali) in 3 categorie: <u>raccomandati, rimandati o controindicati</u> (vaccini "vivi" sono spesso controindicati),

3\) le informazioni ricavate sono presentate all'utente.

Le indicazioni di valutazione dipendono da diversi fattori:

\- **Di terapia**: tipo anti-TNF, anti-IL17, anti-IL23 o altri immunosoppressori.

\- **Del paziente**: tipo età, patologie concomitanti, storia vaccinale...

I vaccini vanno valutati in base a dati provenienti da fonti ufficiali; le principali sono: linee guida EULAR, linee guida CDC, linee guida nazionali, raccomandazioni delle società scientifiche... (queste andranno presentate come regole logiche nel progetto).

Quindi avremo tipo:

\- Input: terapia biologica, età paziente, condizioni cliniche...

\- Output: vaccini raccomandati, possibili (rimandati?) e controindicati.

###### Espansione

Sistema di registrazione e login al fine di salvare persistentemente i dati del paziente e i vaccini valutati per esso (così da non avere dati solo a runtime).

Aggiunta di altre terapie con altri vaccini (sempre basati su linee guida ufficiali).

Mantenimento di uno storico per ogni utente con risultati delle valutazioni dei vaccini anche per consultazione futura.

Eventuale dashboard x la visualizzazione dei vaccini x ogni utente con possibilità di accettare/rifiutare quelli opzionali + schedulazione delle varie date di appuntamento x vaccinazione con magari visualizzazione a calendario (se non il cancro da fare) altrimenti tabella.

##### ...

