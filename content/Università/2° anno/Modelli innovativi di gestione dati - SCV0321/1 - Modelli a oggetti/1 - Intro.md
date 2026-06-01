# Lezione 1

### Modelli di dati

Oltre a quello relazionale ci sono vari tipi di modelli di dati:

###### Object-oriented

Il modello ***object-oriented*** rappresenta i dati come un *type system* di un linguaggio ad oggetti, esteso con un linguaggio di interrogazione (tipo SQL) ed implementandovi la persistenza dei dati.

###### Object-relational

Il modello ***object-relational*** si basa invece sul modello relazionale, esteso con certe caratteristiche della OOP, tra cui: tipi, gerarchie di tipi, metodi associati a tabelle...

###### Tree-based

Il principale esempio di modello ***tree-based*** (o semi-strutturato) è **XML** e viene operato con vari linguaggi standardizzati dal W3C: il linguaggio di interrogazione ***XQuery*** (col sottoinsieme ***XPath***) e il linguaggio ***XML Schema*** (per la definizione dello schema dei dati).

XML non ha rimpiazzato il modello relazionale me vi è stato integrato (tipo SQL/XML); è invece stato ampiamente usato come formato di interscambio di dati prima di essere sostituito da JSON e altri a causa della sua verbosità.

###### Graph-based

I modelli ***graph-based*** sono efficaci per la rappresentazione di dati sottoforma di reti (costituite da nodi e archi) e ne esistono di vari tipi:

- **RDF** (***Resource Description Framework***): insieme di concetti per la rappresentazione di grafi, standardizzato dal W3C con anche un'appostito l'inguaggio di interrogazione: SPARQL.
- ***Property graph***: grafi in cui nodi ed archi possono essere etichettati con altri dati (esistono diversi linguaggi per questi, tipo Cypher, G-Core e GQL ma sono complessi).
- ***Knowledge graph***: evoluzione dei *property graph*, generalmente usati per rappresentare in modo più ricco possibile l'informazione.

---

Prossima lezione: [[2 - Modello object-oriented]]

