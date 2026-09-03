# Lezione 8

### Modelli

(Sta parte è un po' inutile, skippabile a mio avviso).

Progettare e sviluppare sistemi è difficile, per questo si usano i **modelli** che permettono rappresentali in maniera visuale aiutando a gestire la complessità e ad analizzare specifiche qualità o aspetti del sistema in questione.

##### Astrazione

Un sistema ha tantissime caratteristiche ma solo alcune di esse sono effettivamente rilevanti (in base al contesto); perciò l'astrazione permette di descrivere un sistema includendo solo tali caratteristiche. Esempio: un software per una banca deve avere informazioni come nome, cognome, IBAN... di una persona, ma non sono rilevanti dettagli come gruppo sanguigno, altezza...

##### Modularità

Un sistema deve essere modulare al fine di gestire la complessità (come detto prima, moduli fortemente coesi e con interconnessioni minime), solito *divide et impera*.

###### Criteri

Bisogna modularizzare secondo certi criteri:

- **Scomponibilità**: scomporre grandi problemi in sottoproblemi più piccoli e semplici,
- **Componibilità**: aggregare moduli esistenti per risolvere nuovi problemi (riusabilità),
- **Comprensibilità**: i moduli devono essere auto-descrittivi, ovvero si deve capire cosa fanno osservandoli "dall'esterno" (senza dover capire il codice dentro),
- **Continuità**: modifiche alle specifiche del modulo non devono richiedere interventi eccessivi per "sistemare" altri moduli dipendenti,
- **Protezione**: errori sorti in un modulo restare devono restare confinati in esso e non propagarsi nell'intero sistema.

###### Metodi

Invece, come si può ottenere modularità in un sistema?

![](https://i.imgur.com/5fU4XhQ.png)

##### Viste

Per descrivere un sistema complesso generalmente non basta un solo modello, perciò si usano più **viste** focalizzate ognuna su aspetti diversi.

#### Linguaggi descrittivi

Sviluppando un software, oltre ai linguaggi di programmazione e alla lingua della documentazione, esistono linguaggi di **descrizione** che servono per rappresentare in modo strutturato il sistema, esprimendone le caratteristiche.

###### Caratteristiche

Caratteristiche di un buon linguaggio di descrizione:

![](https://i.imgur.com/KnZc8Ox.png)

###### Gradi di formalità

I linguaggi descrittivi possono essere usati con diversi gradi di formalità:

- **Informale**: in linguaggio naturale, usato spesso coi clienti per facilitare la comprensione,
- **Semi-formale**: sintassi definita ma semantica non rigorosa (tipo UML),
- **Formale**: sintassi e semantica rigorosamente definite, con basi logico-matematiche per eliminare l'ambiguità e permettono analisi automatizzate per la maggior parte.

##### Stili

![](https://i.imgur.com/IQvPQWa.png)

###### Descrittivo

Lo stile descrittivo definisce le proprietà che il sistema deve avere senza indicare come ottenerle. È:

- **Compatto**: facilita il ragionamento sul sistema,
- **Astratto**: rende più difficile capire i comportamenti del sistema.

###### Operativo

Lo stile operativo descrive invece il comportamento del sistema passo dopo passo come una macchina astratta suggerendone un'implementazione. È:

- Semplifica l'implementazione e la verifica di quanto sia in linea con la descrizione,
- Però è vincolante in riguardo alla logica predefinita e poco adatto alla verifica formale delle proprietà.

---

Prossima lezione: [[9 - Intro]]

