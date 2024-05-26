# Cisco Packet Tracer

## Creazione della rete

Per creare una rete servono dei router, degli switch e dei pc host.

##### Router

I router generalmente discriminano una rete, la quale può contenere degli host o altre sottoreti (tramite switch).

Ce ne sono di vari modelli, ma generalmente si usa il 2901 o il 2911, che consentono 2 collegamenti con **cavo seriale con clock**. Se fossero necessarie + interfacce seriali usare un router ISR4331 (sia per questo che per gli altri è comunque necessario aggiungere il componente per le interfacce seriali dalla configurazione esterna del router).

##### Switch

Gli switch discriminano una rete all'interno di un router, la quale contiene <u>direttamente</u> gli host; quindi ad un router è possibile collegare 1 o + switch cosicché ognuno di essi rappresenti una rete. 

Per comodità, usare sempre il 2960; inoltre gli switch vanno connessi ai router con cavi *copper straight-through*, ma il collegamento <u>non</u> si attiva subito, perciò è necessario configurare l'interfaccia.

##### Host

Gli host sono dei semplici pc di una rete che si collegano agli switch sempre con dei *copper straight-through*, e il collegamento si attiva automaticamente, ma hanno comunque bisogno della configurazione IPv4 o IPv6 per essere indirizzabili.

##### Laptop

Usato per accedere ai router per la loro configurazione interna tramite cavo console, che nel laptop va attaccato alla porta "RS 232", mentre nel router/switch alla porta "console".

## Configurazione

Dopo aver creato la rete bisogna configurarne:

### Host

Cliccare sul pc e:

**Desktop** $\;\rightarrow\;$ **IP Configuration**

###### IPv4

Impostare (vedi [[Subnetting#Esempio|subnetting]]):

- **IPv4 address** = indirizzo IPv4 dell'host (scritto solo il 1° nel subnetting, quindi aumentare ogni volta in base al n° di host inseriti).
- **Subnet mask** = subnet mask della rete in cui si trova l'host.
- **Default gateway** = indirizzo di gateway della rete in cui si trova l'host.

###### IPv6

...

### Router (esterna)

Cliccare sul router (2901) e:

1) Spegnere il router,
2) Aggiungere il modulo HWIC-2T (da 2 porte seriali),
3) Aggiungere il modulo HWIC-4ESW (da porte gigabit ethernet),
4) Riaccendere il router.

(Nel caso servissero 3 interfacce gigabit/seriali, usare l'ISR4331 con moduli GLC-TE e NIM-2T).

### Router (interna)

Ci sono 2 modi per configurare internamente un router:

- Configurarlo cliccando sul router stesso e andando sulla scheda "Config".
- Collegare il laptop (porta "RS 232") al router (porta "console") con cavo console, andare sulla scheda "Desktop" e cliccare poi su "Terminal" $\;\rightarrow\;$ "Ok" $\;\rightarrow\;$ (eventualmente) usare la configurazione rapida, se no configurare ciò che si vuole come segue:

##### Dare nome a router

Dopo `enable` e `conf t` (come i comandi successivi):

```
Router1(config)# hostname R1
```

##### Impostare il motd

Per il **motd** (*Message of The Day*) si specifica prima un carattere con cui verrà terminato il messaggio, poi si inserisce il messaggio terminandolo con il carattere specificato prima:

```
R1(config)# banner motd #
R1(config)# messaggio #
```

##### Protezione accesso con cavo console

Al posto di "Cisco" è possibile mettere una propria password:

```
R1(config)# line console 0
R1(config)# password Cisco
R1(config)# login
```

##### Impostare password per enable

Al posto di "Cisco" è possibile mettere una propria password:

```
R1(config)# enable secret Cisco
```

##### Attivare il servizio di crittazione password

Altrimenti nella configurazione le password sarebbero in chiaro:

```
R1(config)# service password-encryption
```

##### Visualizzare la configurazione corrente

```
R1# show running-config
```

##### Salvare la configurazione corrente

Per prevenire perdite di dati in seguito a spegnimento del router:

```
R1# copy running-config startup-config
```

##### Assegnare IPv4 all'interfaccia

###### Gigabit (switch)

Qui è "g0/0" perché il router 2901 è fatto così, ma potrebbero essere diverse (tipo "g0/0/0").

```
R1(config)# int g0/0
R1(config-if)# ip add 192.168.0.1 255.255.255.0
R1(config-if)# no sh
```

Questo considerando il caso in cui:

- "192.168.0.1" sia l'indirizzo di **gateway** della rete associata all'interfaccia,
- "255.255.255.0" sia la **subnet mask** della rete associata all'interfaccia.

Comando generico: `ip add (gateway) (subnet mask)`.

###### Seriale (router)

Qui è "s0/3/0", ma potrebbe anche essere "s0/0". <u>Iniziare a configurare dall'interfaccia con clock</u> (se si va in hover col mouse sul triangolo sul cavo appare).

```
R1(config)# int s0/3/0
R1(config-if)# ip add 192.168.1.1 255.255.255.252
R1(config-if)# clock rate 4000000
R1(config-if)# no sh
```

Questo considerando il caso in cui:

- "192.168.1.1" è l'indirizzo dell'**interfaccia seriale del gateway** nella **rete di collegamento** (per le interfacce di **invio** usare l'indirizzo in "**Gateway1**", mentre per quelle di **ricezione** usare l'**altro**),
- "255.255.255.252" è la **subnet mask** della **rete di collegamento** (teoricamente sempre così),

"Clock rate ..." va usato solo sull'interfaccia seriale con clock, mentre "no sh" su entrambe. Diventa comodo configurare le interfacce:

- O facendo tutte quelle di 1 router per volta (non bisogno di cambiare schede ma bisogno di cercare IP interfacce),
- Oppure facendo quelle di ogni rete di collegamento per volta (bisogno di cambiare schede ma basta incrementare di 1 l'indirizzo dell'interfaccia di invio per avere quello dell'interfaccia di ricezione).

Comando generico: `ip add (gateway1/2 colleg) (subnet mask colleg)`.

##### Creazione rotte statiche

Le rotte permettono di far transitare i pacchetti verso una destinazione. Per ogni destinazione a cui deve essere possibile instradare pacchetti bisogna definire una rotta e il next hop (per dare la direzione al pacchetto; nelle reti ad anello a senso unico è sempre il prossimo router di senso per tutte le rotte di un router).

```
R1(config)# ip route 192.168.1.0 255.255.255.0 192.168.2.1
```

Questo considerando il caso in cui:

- "192.168.1.0" è l'**indirizzo di rete** della rete di **destinazione**,
- "255.255.255.0" è la **subnet mask** della rete di **destinazione**,
- "192.168.2.1" è l'indirizzo della **prossima interfaccia seriale** (*next hop*) a cui verranno inviati per primi i pacchetti, definito come "Gateway 1/2" nella rete di collegamento tra le 2 reti.

Per tutte le rotte da definire su un router (in rete anello <u>senso unico</u>) il next hop sarà il medesimo. 

Comando generico: `ip route (ind rete dest) (subnet mask dest) (ind next serial int colleg)`.

##### Visualizzare rotte statiche configurate

```
R1# show ip route
```

##### Creazione rotte dinamiche

...

##### Abilitare l'uso di IPv6

```
R1(config)# ipv6 unicast-routing
```

##### Assegnare IPv6 a un'interfaccia

Stesso discorso di IPv4:

###### Gigabit (switch)

```
R1(config)# int g0/0
R1(config-if)# ipv6 add .../64
R1(config-if)# ipv6 add FE80::1 link-local
R1(config-if)# no sh
```

###### Seriale (router)

...

### Switch

Gli switch sono configurabili sia cliccando sul dispositivo e andando sulla scheda "Config", sia collegandocisi con un cavo console e andando in "Desktop $\rightarrow$ Terminal". 

Configurandoli da "Terminal", sugli switch possono essere eseguiti gli stessi comandi di base eseguibili suo router, i principali sono:

- [[#Dare nome a router|Assegnare hostname al dispositivo]],
- [[#Protezione accesso con cavo console|Proteggere l'accesso con cavo console]],
- [[#Impostare password per enable]],
- [[#Attivare il servizio di crittazione password]]
- ...

Gli switch sono principalmente usati per la configurazione di [[8 VLAN#VLAN|VLAN]].

##### Mostrare tutte le VLAN di uno switch

```
S1(config)# show vlan brief
```

##### Configurare VLAN in switch

Accedere al terminale dello switch e, dopo `conf t`, creare la **VLAN**:

```
S1(config)# vlan 10
S1(config-vlan)# name V1
```

Quando si creano le VLAN, è buona pratica dargli dei **VID numericamente distanti** e proporzionati in base alla grandezza della rete nel caso serva creare altre VLAN.

##### Configurazione access port

Negli switch vanno configurate le ***access port*** per le interfacce a cui si collegano **host** (se allo switch si collegano **+ VLAN**, <u>vanno configurate tutte</u>), quindi:

```
S1(config)# int fa0/1
S1(config-if)# switchport access vlan 10
```

Questo nel caso in cui l'host sia attaccato all'interfaccia "**FastEthernet0/1**" e si voglia associarlo alla **VLAN** con VID **10**.

##### Configurazione trunk port

Per configurare le ***trunk port*** si configurano le interfacce di collegamento tra switch (il comando `switchport trunk allowed vlan add N` va fatto per <u>ogni VLAN che si deve mettere in comunicazione con l'altro switch</u>):

```
S1(config)# int g0/1
S1(config-if)# switchport mode trunk
S1(config-if)# sh
S1(config-if)# switchport trunk allowed vlan none
S1(config-if)# switchport trunk allowed vlan add 10
S1(config-if)# no sh
```

Va fatto per <u>entrambe le interfacce del collegamento</u> (prima per S1 e poi per S2). 

**ATTENZIONE**: il procedimento va fatto anche per le interfacce degli switch collegate con router (non per quelle dei router).

###### Spiegazione passi

1) Si entra nell'interfaccia dello switch a cui gli si collega un altro switch (nel caso questa sia l'ingerfaccia "**GigabitEthernet0/1**"),
2) Con `switchport mode trunk` si imposta l'interfaccia come ***trunk***.
3) Bisogna poi <u>spegnere l'interfaccia</u>.
4) Si **rimuovono** tutte le **VLAN conosciute** nello switch.
5) Si **aggiungono** le **VLAN necessarie**, ovvero quelle di cui l'interfaccia vuole inviare il traffico.
6) Va poi <u>riaccesa l'interfaccia</u>.

##### Abilitare l'inter-VLAN routing

Questo supponendo che il VID della VLAN sia 10:

```
R1(config)# int g0/0
R1(config-if)# no sh
R1(config-if)# exit
R1(config)# int g0/0.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip add 192.168.0.1 255.255.255.0
```

Con:

- "192.168.0.1" = gateway della rete
- "255.255.255.0" = subnet mask della rete

Imposto gateway per tutte le VLAN che mandano traffico all'interfaccia

##### Cancellare una VLAN

Supponendo che si voglia cancellare la VLAN con VID 10:

```
S1(config)# no vlan 10
```

## Hotkeys

##### CTRL + SHIFT + 6

Sblocca ping errati.

...

## Esempio

### Problema

- RC
	- RUA = 210 host = 256
	- RLA = 555 host = 1024
- RP = 28 host  = 32
- RD = 124 host = 128
- RCP = 4
- RPD = 4
- RDC = 4

Tutte le sedi devono comunicare, traffico senso antiorario. 

Rete base: 192.254.96.0/22

### Subnetting

Tot = 1024 + 256 + 128 + 32 + 4 + 4 + 4 = 1452 = 2^11 --> nn ci stiamo, quindi prendo una /21

RLA = 1024 = 10

rete = 192.254.96.0

gatw = 192.254.96.1

host = 192.254.96.2

brod = 192.254.99.255

subn = 255.255.252.0 = /22

RUA = 256 = 8

rete = 192.254.100.0

gatw = 192.254.100.1

host = 192.254.100.2

brod = 192.254.100.255

subn = 255.255.255.0 = /24

RD = 128 = 8

rete = 192.254.101.0

gatw = 192.254.101.1

host = 192.254.101.2

brod = 192.254.101.127

subn = 255.255.255.128 = /25

RP = 32 = 5

rete = 192.254.101.128

gatw = 192.254.101.129

host = 192.254.101.130

brod = 192.254.101.255

subn = 255.255.255.240 = /27

RCD = 4 = 2

rete = 192.254.102.0

gtw1 = 192.254.102.1

gtw2 = 192.254.102.3

brod = 192.254.102.4

subn = 255.255.255.252 = /30

RDP = 4 = 2

rete = 192.254.102.5

gtw1 = 192.254.102.6

gtw2 = 192.254.102.7

brod = 192.254.102.8

subn = 255.255.255.252 = /30

RPC = 4 = 2

rete = 192.254.102.9

gtw1 = 192.254.102.10

gtw2 = 192.254.102.11

brod = 192.254.102.12

subn = 255.255.255.252 = /30

### Cisco

##### Rete

![](https://i.imgur.com/pQ6HOkf.png)

##### RD

Prendiamo la RD come esempio:

###### Host configuration

![](https://i.imgur.com/obo09La.png)

###### Router-switch gigabit interface

![](https://i.imgur.com/6v5Vjfl.png)

###### Serial port (send to RP)

![](https://i.imgur.com/ZgQltt9.png)

###### Serial port (receive from RC)

![](https://i.imgur.com/dDQtn12.png)

###### Static routes

![](https://i.imgur.com/gJAHfLu.png)

