# Lezione 32

##### Memory wall

La **[legge di Moore](https://en.wikipedia.org/wiki/Moore%27s_law)** stabilisce che il numero di transistor nelle CPU si raddoppi ogni ~18 mesi, con anche potenza e velocità delle stesse.

Il ***[memory wall](https://en.wikipedia.org/wiki/Random-access_memory#Memory_wall)*** è la prova che ciò <u>non si applica anche alle memorie</u>, infatti dal 1980 ad oggi, la **latenza** delle memorie (*memory latency*, ovvero il loro <u>tempo di risposta</u>) è dimezzata solo ogni <u>~10 anni</u> (dimezzamento latenza = raddoppio prestazioni).

![](https://i.imgur.com/GIc0ZA0.png)

### Memorie

Per colmare il divario del *[[#Memory wall|memory wall]]* si è creata una **gerarchia di memoria**, che classifica la memoria in diversi livelli a seconda di **costi e prestazioni**; quindi, per un buon compromesso tra essi, l'uso di diversi livelli di memoria è fondamentale.

![](https://i.imgur.com/RCIo9JZ.png)

Più si è alti nella piramide, maggiori sono costi e velocità (ma piccola capacità), mentre più si è in basso, maggiori sono latenza e capacità (però molto economiche).

In confronto:

- Registri: dimensioni entro i 1000 bytes ma latenza < 10 ns,
- Cache: dimensioni da KB a MB ma latenza dai 10 ai 100 ns,
- RAM: dimensioni in GB ma latenza dai 200 ai 500 ns,
- Mass memory: dimensioni in TB ma latenza nell'ordine dei ms.

##### Bus

I registri (ma anche delle cache) sono direttamente connessi all'ALU dato che ne salvano i risultati. Le altre memorie però devono comunicare con essi e per ciò si usano i **bus**.

![](https://i.imgur.com/uzyiEc4.png)

Ci sono diversi tipi di bus (solitamente i registri li usano tutti, mentre le RAM solo dati):

- ***Data bus***: scambia ***word*** da leggere o scrivere,
- ***Address bus***: scambia segnali con gli **indirizzi** dei dati da leggere o scrivere,
- ***Control bus***: scambia **segnali di controllo** per la memoria.

##### Unità di organizzazione

Le memorie sono organizzate in modi differenti date le loro caratteristiche, ovvero:

###### Words

Una ***word*** (o *parola*) è la <u>quantità di dati che un processore</u> (o un circuito sequenziale) <u>può elaborare/trasferire/memorizzare in una singola operazione</u>.

La sua **dimensione** è in <u>bit</u> e indica (oltre a dipendere da):

- Dimensione dei **registri** (registro a $n$ bit = *word* a $n$ bit),
- Dimensione del **bus dati**,
- ...

###### Blocks

Un ***block*** (o *blocco*) è semplicemente un'<u>insieme di</u> *[[#Words|word]]* <u>contigue in RAM</u> (sia cache che normali RAM).

###### Pages

# Esercizi

# Soluzioni

---

Prossima lezione: [[33 - Registro parallelo]]

