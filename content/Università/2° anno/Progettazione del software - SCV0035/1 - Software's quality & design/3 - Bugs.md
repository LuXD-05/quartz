# Lezione 3

### Bugs

##### Terminologia

Definiamo 3 termini importanti:

- ***Error*** (*mistake*): azione umana che produce un risultato errato (errori logici nel codice, architettura sbagliata, poca comunicazione...),
- ***Fault*** (*defect*): un passo o processo errati di un componente che rendono un sistema non più in grado di funzionare,
- ***Failure***: quando un sistema fallisce nel raggiungere i propri requisiti (*crash*, risultati errati, non rispetta vincoli, falle di sicurezza...).

> [!important] Nota
> Un *error* può causare più *faults* (seppur un *fault* può essere causato da più *errors*) e un *fault* può causare più *failures* (anche ognuno di questi causabili da più *faults*).
> ![](https://i.imgur.com/1Anb6aq.png)
> È difficile riprodurre i *failures* (soprattutto in programmi concorrenti) in quanto gli errori sono difficili da trovare; perciò servono tool di monitoraggio daeguati.

##### Tipi di bug

![](https://i.imgur.com/vp2A0aI.png)

![](https://i.imgur.com/kphFSaK.png)

![](https://i.imgur.com/RbjJYeM.png)

##### Failure severity

Ci sono dei gradi di gravità dei *failures* (ordine crescente): *mild*, *moderate*, *annoying*, *disturbing*, *serious*, *very serious*, *extreme*, *intolerable*, *catastrophic*, *infectious*.

###### Fixing costs

![](https://i.imgur.com/zgneIgl.png)

---

Prossima lezione: [[]]

