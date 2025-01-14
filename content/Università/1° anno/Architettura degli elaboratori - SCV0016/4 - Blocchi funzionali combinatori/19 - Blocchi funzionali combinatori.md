# Lezione 19

### Blocchi funzionali combinatori

La rappresentazione a tavole di verità e con le mappe di Karnaugh <u>non è sufficiente</u> per descrivere moderni circuiti integrati, in quanto per tali sarebbe richiesta la sintesi di reti *molto* più grandi e con *molte* più variabili.

Per questo motivo, al fine di rappresentare i suddetti circuiti, è necessario <u>combinare sottoreti piccole in reti più grandi</u>. Le sottoreti piccole sono dette ***blocchi funzionali***.

##### Astrazione

Quello che avviene è un processo (come quelli tra gli artefatti [[15 - Artefatti e relazioni#Artefatti e relazioni|qui]]) di ***astrazione***, che semplifica ragionamenti e schemi in quanto permette di:

- Considerare componenti semplici come delle [blackbox](https://it.wikipedia.org/wiki/Modello_black_box) ed usarli in circuiti più grandi,
- Sostituire a più <u>input</u> di una tavola di verità una l'<u>output della funzione che li relaziona</u> (per semplificare il tutto),
- ...

Ciò non vale solo per circuiti e porte, ma anche per i **cavi**:

![](https://i.imgur.com/M08Ll4z.png)

---

Prossima lezione: [[20 - Decoder]]

