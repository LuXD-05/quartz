# Tecnologie per reti IoT

### Problema

La diffusione dell'IoT è rallentata a causa di: 

- Frequenti ricorsi a tecnologie proprietarie invece che a standard aperti 
- Numero di tecnologie differenti tra cui scegliere elevato.

### Come rendere un dispositivo smart?

Per rendere un dispositivo *smart* (capace di percepire cambiamenti della realtà e trasmettere i dati a qualcuno) serve:

- Identificarlo univocamente,
- Renderlo capace di comunicare (con tecnologie wireless o cablate),
- Abilitarlo a percepire la realtà (tramite sensori) ed eventualmente ad agire (tramite attuatori),
- Renderlo monitorabile e controllabile da remoto attraverso un terminale (per esempio una app mobile per controllarlo o anche una in cloud per storage ed elaborazione di dati inviati).

Per fare tutto ciò occorre inserire materialmente nel dispositivo dei chip che permettano di implementare i suddetti punti.

##### Criticità

Una criticità si ha nel decidere quale standard trasmissivo usare per l'invio di dati, soprattutto se si decide che questo sarà wireless in quanto vi sono tantissime tecnologie tra cui scegliere, tra cui: WiFi, BT, BLE, ZigBee, cellulare (2/3/4/5G), LoRa...

### Alcune tecnologie

Esistono delle tecnologie adatte per vari tipi di reti IoT: 

- **[[6.1 Short range|WiFi e BLE]]** per ***short range*** (pochi metri),
- **[[6.2 Medium range|Tecnologie cellulari]]** per ***range* medio-grandi** (centinaia di metri),
- Tecnologie LPWAN (*Low Power WAN*), tipo **[[6.3 Long range|LoRa]]**, per ***long range*** (diversi km) e con bassi consumi energetici.

Per capire quale tecnologia usare, occorre valutare quale sia la + adatta in base a *range* e *bandwidth*.

![](https://i.imgur.com/9oIcqJa.png)

