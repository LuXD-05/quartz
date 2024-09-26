# Protocolli per reti IoT

### Intro

Per app IoT sono necessarie regole di comunicazione a livello applicativo client/server in quanto non esiste un protocollo standard per esso. Comunque ne esistono molti, però qui sono presentati 2 standard aperti che facilitano la scelta ai progettisti, e sono **MQTT** e **CoAP**.

Sono dei protocolli ***constrained*** (adatti ad ambienti vincolati), quindi adatti a realtà con dispositivi con problemi di alimentazione, larghezza di banda ridotta, scarse capacità di elaborazione e incapaci di stabilire direttamente una connessione a internet sicura (al contrario di HTTP).

I 2 protocolli sono differenti, ma per quanto riguarda il protocollo livello trasporto:

- **MQTT = TCP**
- **CoAP = UDP**

