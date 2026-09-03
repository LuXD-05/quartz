# Lezione 7

### XSchema

**XSchema** (*XML Schema*), rispetto a DTD, usa i namespace, è molto espressivo riguardo ai tipi di dati, comprende concetti *object-oriented* (tipo ereditarietà).

Seppur complesso, esso permette di serializzare (scrivere) i propri schemi in XML.

##### Componenti

###### Tipi semplici

Un **tipo semplice** definisce un <u>insieme di valori</u> che sono (in pratica) <u>stringhe di caratteri</u>. Si hanno:

- **Tipi primitivi**: (i soliti predefiniti),
- **Tipi derivati**: ovvero <u>restrizioni sui tipi predefiniti</u> (tipo numeri interi in un certo intervallo).

###### Tipi complessi

Un **tipo complesso** <u>definisce la struttura degli elementi di tale tipo</u> tramite <u>requisiti e vincoli</u> su attributi, sotto-elementi e dati char.

###### Elementi

Un **elemento** è una semplice <u>associazione di un nome ad un tipo semplice o complesso</u> che, per essere valida, le sue istanze devono soddisfarne i requisiti definiti dal tipo.

Se tutti gli elementi nel documento sono validi, allora lo è anche l'intero documento.

###### Attributi

Un **attributo** è un'<u>associazione di un nome ad un tipo semplice</u> (non complessi siccome gli attributi permettono <u>solo testo</u> nel valore).

##### Esempio

Il seguente schema (contenuto in un file con estensione `.xsd`) definisce un elemento di tipo complesso:

![455](https://i.imgur.com/MYrkTIt.png)

Di cui un esempio di documento XML valido per tale schema è:

![](https://i.imgur.com/tQuotff.png)

Nello schema si hanno poi:

- `targetNamespace`: attributo che specifica l'URI del namespace da associare allo schema (con alias `s` nel documento, mentre `xsd` è l'alias di XSchema che contiene tutti i nomi dei tag dello schema).
- `Voto`: è un tipo semplice derivato, definito come restrizione del tipo predefinito `xsd:integer` tra i valori da 0 a 100.
- `Studente`: è invece un tipo complesso contenente gli attributi `id` e `voto` entrambi obbligatori (`required`).

---

Prossima lezione: [[8 - XPath]]

