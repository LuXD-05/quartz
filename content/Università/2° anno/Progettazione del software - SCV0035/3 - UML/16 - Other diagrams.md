# Lezione 16

### Altri diagrammi

Ci sono tanti altri tipi di diagrammi nello standard, ma qui vediamo:

#### Timing diagrams

I ***timing diagrams*** servono per rappresentare <u>cambiamenti di stati e valori in base ad eventi</u> rispetto al **tempo**, evidenziando vincoli temporali e la durata degli eventi (utili per rappresentare vincoli non funzionali relativi alle prestazioni).

##### Lifeline

La ***lifeline*** indica le variazioni nel valore degli stati e gli eventi ed è possibile disegnarla o con valori discreti (*state lifeline*) o con valori continui (*value lifeline*).

![](https://i.imgur.com/IKGeayY.png)

Se la scala dell'asse delle $x$ è la stessa, allora più *lifelines* possono essere nello stesso diagramma.

![](https://i.imgur.com/v3dAl6U.png)

> [!info] Nota
> Ogni transizione può essere dovuta a:
> - Un evento,
> - Un vincolo temporale (che indica entro quanto deve avvenire un certo evento),
> - Una durata (che indica quanto a lungo deve durare tale stato).

#### Component diagrams

Un ***component*** è una parte modulare di un sistema che:

- Incapsula dei contenuti,
- Ha un comportamento definito tramite interfacce richieste e fornite,
- Solitamente implementato con classi/oggetti (> livello di astrazione rispetto a un *class diagram*),
- Può avere più implementazioni intercambiabili.

> [!example] In pratica
> In pratica è un diagramma più astratto dei componenti di un sistema, che siano software, hardware, risorse umane...
> ![](https://i.imgur.com/IKo1gv3.png)

#### Deployment diagrams

I ***deployment diagrams*** invece indicano l'architettura del sistema e specificano come gli ***artifacts*** vengono assegnati ai nodi; tali nodi sono <u>dispositivi hardware</u> (server, istanze, PC...) e possono essere annidati, in rete...

> [!example] Esempio
> ![](https://i.imgur.com/ZyYdEPd.png)

###### Artifacts

Gli **artefatti** sono la specifica di un'informazione fisica prodotta o usata da un processo di un sistema, alcuni esempi sono: file di codice, eseguibili, tabelle di database...

---

Prossima lezione: [[17 - Design patterns]]

