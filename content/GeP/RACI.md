### Cos'è?

La **RACI** permette di andare a definire le **responsabilità** dei singoli all'interno di un progetto.

##### Tipi di responsabilità

###### R

Questa è la responsabilità **operativa**: chi la ha, **ha un compito da fare** concreto (obbligatoria).

###### A

Questa è la responsabilità **esclusiva** (**1 sola per attività**) e la figura che la detiene **autorizza** e **approva** il **lavoro di R** (obbligatoria).

###### C

Quelli con responsabilità **C** sono **figure**/risorse che vengono **consultate** per prendere decisioni (facoltativa).

###### I

Quelli con responsabilità **I** sono **figure**/risorse che vengono **informate** (della **SAL** o *Stato Avanzamento Lavori*) ed eventualmente dicono cosa fare (facoltativa).

##### Come assegnare R e A

Ci può essere una risorsa sia R sia A (eventualmente) quando devo sia fare sia autorizzare (generalmente sono separate, siccome se un esterno fa entrambi, poi al destinatario del lavoro magari non va bene siccome il R/A fa come vuole).

Prendiamo il PBS/WBS:

Analisi esigenze, progetto esigenze, sviluppo, db, arch rete. Chi fa che cosa?

- Analisi esigenze (R/A = PM) (C = UP)
- Progettazione esigenze (R = SV, DBA, SYS) (A = PM)
- Sviluppo (R = SV) (A = PM)
- Database (R = DBA) (A = PM)
- Arch rete (R/A = SYS)

Questa dovrebbe essere grafica, con l'OBS in gerarchia sopra e a sinistra le fasi del PM (o attività) che si collegano con delle linee verticali che scendono dall'OBS e dove si incontrano ci sono le responsabilità.

### TABELLA RACI

Team di progettazione

| (Attività)         | SV  | PM  | DBA | SYS | UP  |
| ------------------ |:---:|:---:|:---:|:---:|:---:|
| Analisi esigenze   |  C  | R/A |  I  |  I  |  C  |
| Progetto esigenze  |  R  |  A  |  R  |  R  |     |
| Sviluppo           |  R  |  A  |  I  |  I  |     |
| Progetto DB        |  I  |     | R/A |  I  |     |
| Progetto arch rete |  I  |     |  I  | R/A |     |

PASSI:

1) OBS 
2) RACI (grafica)
3) RACI (tabella)

1 riga di sommario per OBS
1 riga di sommario per RACI (both)

