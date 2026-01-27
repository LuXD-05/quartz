# Lezione 9

### UML

**UML** (*Unified Model Language*) è un linguaggio visuale per la progettazione di software che copre l'intero processo di produzione ed è standardizzato e gestito dall'[OMG](http://www.omg.org). Esso raggruppa tanti linguaggi che congiunti permettono di descrivere tutti gli aspetti rilevanti di un sistema (in approccio *object-oriented*).

UML usa notazione grafica, linguaggio semi-formale, è un po' dichiarativo un po' operazionale, è indipendente da qualsiasi linguaggio di programmazione, utilizzabile in ambiti diversi e per progetti di diverse dimensioni ed è estendibile (per modellare meglio le realtà).

> [!important] IMPORTANTE
> Si trovano le specifiche di tutti i seguenti diagrammi in lingua inglese (e probabilmente spiegate meglio) al seguente sito: https://www.uml-diagrams.org/.

##### UML views

![](https://i.imgur.com/y9I3gLU.png)

###### Use-Case view

Questa vista <u>descrive dei casi d'uso</u> importanti che vengono <u>usati come esempi per l'architettura del software</u> per mezzo di **Use-Case diagrams**. Ogni use-case può avere diversi scenari possibili, descrivibili testualmente o graficamente tramite *sequence/communication/activity diagrams*.

###### Structural view

Questa rappresenta <u>elementi strutturali per implementare la soluzione</u> in base a requisiti specifici. Fa uso di *class*, *package* e *composite structure diagrams*; e definisce: oggetti di analisi e di progetto, il vocabolario della soluzione, la scomposizione del sistema in livelli e sottosistemi e infine le interfacce del sistema e dei suoi componenti.

###### Behavioral view

Questa rappresenta le varie <u>interazioni dinamiche tra i componenti del sistema</u>, con anche le varie <u>responsabilità</u>, eventuali ***bottleneck*** di interazione o accoppiamento... Molto importante per sistemi distribuiti e rappresentata da UML dinamici quali: *sequence*, *activity*, *state*, *timing* o *interaction overview diagrams*.

###### Implementation view

Questa definisce l'<u>implementazione dei moduli e dei sottosistemi logici</u> (definiti nella [[#Structural view|structural view]]) <u>e le dipendenze tra i vari componenti e le loro interfacce</u> richieste o fornite (può comprendere anche moduli intermedi come librerie o file di dati). Rappresentata da *component* o *composite structure diagrams*.

###### Environment view

Questa rappresenta la mappatura hardware del sistema, ovvero indica <u>come distribuire i moduli componenti software sui nodi hardware</u>. Fornisce informazioni per l'installazione e la configurazione del sistema, utile anche per affidabilità, scalabilità, sicurezza... ed è rappresentata da *deployment diagrams*.

---

Prossima lezione: [[10 - Use-Case diagrams]]

