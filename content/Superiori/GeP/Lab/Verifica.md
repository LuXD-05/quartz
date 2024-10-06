---
modified_at: 11/05/2024 00:12:30
edited_seconds: 590
---
### Verifica
##### 1
###### Dire cos'è l'EVM, su quali valori opera e in quali contesti è utile.
L'EVM è un metodo molto usato in *project management* che permette di monitorare l'andamento di costi e tempi in un progetto e di fare previsioni su questi in base a certi valori:
- ***Timenow***: un valore temporale, compreso nella periodo di realizzazione del progetto, nel quale si vogliono fare delle previsioni.
- **PV** (*Planned Value*): è alla somma delle stime costi che si avrebbe dovuto sostenere al *timenow*, rispetto alla durata totale del progetto.
- **AC** (*Actual Cost*): è la somma dei costi effettivamente sostenuti fino al *timenow*.
- **EV** (*Estimated Value*): è la somma delle stime dei costi che si avrebbe dovuto sostenere al *timenow* in base alla % di completamento effettiva delle attività.

Inoltre, l'EVM permette il calcolo di 4 indici per monitoraggio e previsioni:
- CPI: indice che indica la *performance* dei **costi** al *timenow* (entro BT se > 1, altrimenti oltre il BT).
- SPI: indice che indica la *performance* dei **tempi** al *timenow* (entro TT se > 1, altrimenti oltre il TT).
- EAC: è il costo totale del progetto, se l'andamento dei costi rimane = a quello verificato al *timenow*.
- SAC: è la durata totale del progetto, se l'andamento dei tempi rimane = a quello verificato al *timenow*.

Può essere utile in vari contesti: banalmente, oltre che in situazioni in cui si deve capire l'andamento del progetto e dei costi e tempi, l'EVM è uno strumento che, in base alle previsioni che può far fare, si usa quando si vogliono riconoscere rischi legati al corrente andamento del progetto (costi e tempi), incentivando azioni correttive preventive.

###### Descrivere le 2 procedure per il calcolo del BEP
Il BEP (*BreakEven Point*) indica il punto in cui, in un progetto, i costi totali sono pari ai ricavi totali, ovvero il punto in cui l'impresa non genera né profitti né perdite. Esso è calcolabile in 2 modi:
Con un procedimento matematico ovvero, in un progetto, prendendo prima i costi fissi (CF), il costo per produrre un pezzo (cv) e il prezzo unitario di vendita (p); e poi calcolando il n° di prodotti da vendere necessari guadagnare tanto quanto si spende (Q), con la formula: $Q \;=\; \dfrac{CF}{p - cv}$. Questo è il punto (in n° di prodotti venduti) in cui i ricavi saranno pari ai costi.
Oppure con un procedimento grafico, per cui servirà il *breakeven chart*, diagramma rappresentante 2 funzioni: una curva dei ricavi totali ($p * x$) e una curva dei costi totali ($cv * x + CF$). Quindi così:
![](https://i.imgur.com/mGMfdMU.png)

###### Calare in un contesto reale una tecnica per la riduzione del BEP
Poniamo il caso di un'azienda che produce scarpe sta facendo fatica a raggiungere il suo BEP quest'anno. Questo può darsi in quanto (si suppone) che la domanda per scarpe nel mercato si stia abbassando, per cui i prezzi dei prodotti di questo genere calano generalmente per tentare di sopperire alla diminuzione delle vendite.
Tutto ciò contribuisce all'innalzamento del BEP dell'azienda in questione siccome questa, dovendosi adattare ai costi di mercato per essere competitiva e vendere, non genera più lo stesso profitto di prima malgrado lo stesso numero di vendite. 
Per risolvere la situazione sarebbe ideale: prima eseguire un'analisi di mercato e scoprire (sempre ipoteticamente) che le cinture stanno andando particolarmente di moda in questi tempi; e dopo, dati opportuni presupposti e verifiche, reingegnerizzare i processi aziendali e convertirli alla produzione di cinture (supponendo che gli eventuali costi in materie prime e macchinari non ci siano o siano relativamente bassi).

###### Descrivere come vengono gestite le risorse in Project e come questa aiuta nel project management
[[Microsoft project#Gestione delle risore|Risorse]]

##### 2
Azienda con 5 ospedali vuole rifare l'infrastruttura di rete di tutti in 1 anno. Budget di 250k con 35% in cablaggio e 65% in rete. Valutare l'avanzamento del progetto a 7 mesi sapendo che la rete è stata installata in 3 ospedali al costo di 96k, mentre il cablaggio è stato completato dappertutto con 86k totali.
###### Analisi
(5 strutture tot)
TT = 12 mesi
BT = 250k
35%BT = cablaggio (87500)
65%BT = rete (162500)
Timenow = 7 mesi
(3 strutture al timenow completate) 
Cablaggio = 86000€ (100%)
Rete = 96000€ (60%)
###### Indicatori 1
PV = 100% 86000 + 58,3% 162500 = 180737,5€
AC = 86000 + 96000 = 182000€
EV = 100% 86000 + 60% 162500 = 183500€
###### Indicatori 2
CPI = 183500/182000 = 1,008
SPI = 183500/180737,5 = 1,015
EAC = 182000 + (250000 - 183500) / 1,008 = 246468,7€
SAC = 12 / 1,015 = 11,8 mesi

##### 3
Azienda fa sensori IoT e spende:
- 300k di stipendi,
- 100k di affitto magazzino,
- 4€ costo unitario produzione sensore,
- 7.50€ prezzo unitario vendita sensore.
Stabilire il punto di equilibrio.
###### Indicatori 1
Quindi si hanno:
- CF = 300k + 100k = 400k
- cv = 4€
- p = 7.50€
###### Indicatori 2
$Q \;=\; 400k \;:\; (7.5 - 4) \;=\; 114286 \;$ sensori.
(Spese totali / guadagno da ogni pezzo = n° pezzi necessari per equipararle)
$R_{c} \;=\; 7.5 * 114286 - (4 * 114286 + 400k) \;=\; 857143 - (457143 + 400k) \;=\; 0$
Supponendo che si prevede di vendere 120000 sensori, l'MS:
$MS \;=\; (120000 - 114286) / 120000 = 5714 / 120000 = 0,0476 * 100 = 4,78\%$

##### 4
![](https://i.imgur.com/YJAnfmd.png)
1 = 4 (aumento costi x stipendi)
2 = 3 (tipo se progetto all'aperto e non posso lavorare con pioggia)
3 = 1 (troppo generico per specificare)
4 = 3 (dato che magari ci si mette troppo a produrre l'output)
5 = 1/5 (tipo che ci mette poco tempo? potrebbe anche non significare niente)
6 = 3 (sovrallocamenti indesiderati... + tempo?)
7 = 1 (nessun sovrallocamento o stalli... - tempo?)
8 = 1? (perché lo si fa in meno tempo se di scarsa qualità?)
9 = 4 (perché previsti costi minori di quelli effettivi (ma anche tempi) quindi si sfora ???)
10 = 1/5 (perché previsti costi > di quelli effettivi (ma anche tempi) quindi è come se fosse molto veloce ???)
