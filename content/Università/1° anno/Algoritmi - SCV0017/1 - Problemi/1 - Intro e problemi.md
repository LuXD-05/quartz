# Lezione 1

### Problemi

Segue una semplice introduzione a ciò di cui si occuperà il corso con 2 problemi.

##### Problema della celebrità

Un'azienda cerca uno sponsor per un suo prodotto e sceglie una celebrità (per *astrazione matematica*, una persona che non conosce "nessuno" ma che è nota a "tutti", quindi c'è 1 sola celebrità (se $x$ conosce $y$, $x$ non è una celebrità e viceversa)). 

Tramite domande tipo "$x$ consce $y$?" determinare se c'è una celebrità. 

###### Soluzione inefficiente

Date $n$ persone, bisogna chiedere ad ognuno se conosce tutti gli altri: $n \cdot (n-1)$.

Inoltre, ad ogni persona bisogna sia chiedere se conosce altri, sia chiedere ad altri se è conosciuta, il che raddoppia il n° di domande totali da fare. 

Alla fine si arriverà a $2n \cdot (n-1)$ domande totali da porre.

###### Soluzione efficiente

Si prendono coppie di persone anche a caso e ci si pone la domanda "$x$ conosce $y$?"; quindi:

- Se $x$ <u>non lo conosce</u>, allora $y$ **non è una celebrità** (<u>e lo si scarta</u>),
- Se $x$ <u>lo conosce</u>, allora $x$ **non è una celebrità** (<u>e lo si scarta</u>).

Alla fine, con $n-1$ domande si ottiene un potenziale candidato ad essere una celebrità; quindi: 

- Per verificare che non conosca nessuno sono altre $n-1$,
- Più altre $n-2$ domande per capire se tutti lo conoscono.

È $n-2$ dato che si fanno $n-1$ domande meno l'ultima fatta al candidato per determinare se esso fosse effettivamente un candidato (in base a tale domanda, $n-2$ possono anche essere le domande per verificare che esso non conosca nessuno).

In totale dovranno essere fatte $3n - 4$ domande ($C_{n} = n-1 + n-1 + n-2$).

##### Problema del chirurgo

Considerando che la superficie di un paio di guanti può essere usata solo se non infetta, per un chirurgo che opera in una zona contaminata, quante persone è possibile operare con $n$ paia di guanti in modo che non ci siano contatti tra tessuti e superfici infette?

###### Soluzione inefficiente

Un paio di guanti per intervento, quindi $n$.

###### Soluzione efficiente

I guanti sono infilabili uno sopra l'altro ed hanno 2 superfici; ci sono 2 soluzioni:

- Si infilano tutti gli $n$ guanti sulle mani e si fanno $n$ operazioni. Si tiene l'ultimo paio e si mette l'ultimo paio contaminato su ma **risvoltato**, cosicché la superficie esterna non sia contaminata e permetta di operare; questo si fa quindi con tutti i guanti rimanenti.
- Si infilano 2 guanti e si fa un'operazione, si toglie il guanto esterno e se ne mette su uno nuovo fino a finirli, poi si fa un'operazione con il paio di guanti iniziale e infine per ogni guanto infetto lo si risvolta cosicché le superfici infette dei 2 guanti siano a contatto, permettendo di usare nuovamente la superficie sterile del guanto.

Per entrambe, il n° massimo di operazioni possibili è $2n -1$.

---

Prossima lezione: [[2 - Fair division]]

