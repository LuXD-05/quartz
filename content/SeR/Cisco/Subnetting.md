# Subnetting

### Classful

Prima IP erano in classi:

- A: 8 bit rete, 24 bit host \[0|...\] Host configurabili: 2^24 - 1 = 16M
- B: 16 bit rete, 16 bit host \[10|...\]. Host configurabili: 2^16 - 1 = 65K
- C: 24 bit rete, 8 bit host \[11|...\]. Host configurabili: 2^8 - 1 = 255
- D: per multicast | E: per usi sperimentali

### Indirizzi

##### Normale subnet

###### Indirizzo di rete

L'indirizzo di rete di una subnet è sempre il 1° bit disponibile.

###### Broadcast

L'indirizzo di broadcast solitamente è riservato all'ultimo bit disponibile.

###### Gateway

L'indirizzo del gateway della sottorete è il 2° bit disponibile (1° dopo indirizzo di rete) ma potrebbe anche essere il penultimo (prima del broadcast).

###### Esempio

```
R1 = 2^8 bit = 256 host
rete      = 192.168.0.0
gateway   = 192.168.0.1
1° host   = 192.168.0.2
last host = 192.168.0.254
broadcast = 192.168.0.255
subnet m. = 255.255.255.0 = /24
```

### Tipi di subnetting

##### FLSM (Fixed Length Subnetting Method)

Da usare quando in una rete gli host sono sempre quelli (al max diminuiscono), ma non eccedono mai il n° max statico fisso specificato

###### FLSM Steps

Configurare 100 pc divisi in 10 subnet. Indirizzo base: 192.168.0.0/24:

1) Trovare il n° di host in ogni rete:

	   10 pc + ind. rete + broadcast + gateway = 13 host (per rete)

2) Trovare il n° di bit necessari per contenere gli host delle reti:

	   4 (perché $2^{4}$ = 16 e 16 > 13, quindi 13 host ci stanno)

3) Trovare il n° totale dei bit necessari per rete, sommarli e trovare i bit necessari per contenere questa somma. Se i bit necessari superano la capienza dell'indirizzo di base dato, richiederne uno adatto:

	   10 reti \* 16 bit = 160 bit totali. Servono quindi 8 bit (perché $2^8$ = 256 e 256 > 160, quindi sì, ci stiamo in una /24)

##### VLSM (Variable Length Subnetting Method)

Da usare quando non si conosce il n° degli host a prescindere, e questi potrebbero variare (aumentando o diminuendo)

###### VLSM Steps

0) Ottenere tutte le reti, le sottoreti e il n° di host che conterranno.
1) Ordinare le reti dalla + grande alla + piccola, calcolando per ognuna la minima potenza di 2 che possa contenerla, tenendo conto che oltre agli host, bisogna specificare:

   - Per le reti normali, l'indirizzo di rete, l'indirizzo del gateway e l'indirizzo di broadcast.

   - Per le reti di collegamento (quelle tra 2 router che comprendono già le loro interfacce), l'indirizzo di rete e il broadcast.

2) Sommare tutte le potenze di 2 trovate, trovare la minima potenza di 2 che contenga queste e considerare l'esponente come il n° di bit necessari per tutti gli host; quindi:

   - Se 32 - il n° di bit necessari è $\small\ge$ della subnet data con l'indirizzo di partenza, ci stiamo.

   - Se invece il calcolo è < della subnet data, richiedere un nuovo indirizzo con una subnet adeguata.

3) Per ogni rete, trovare gli indirizzi di:

   - Rete,

   - Gateway,

   - 1° host,

   - Ultimo host,

   - Broadcast,

   - (Subnet mask in *dotted decimal*, poi serve in Cisco).

4) Per le reti di collegamento tra i router invece (partendo da dove si arriva con le precedenti) calcolare gli indirizzi di:

   - Rete,

   - 1° gateway,

   - 2° gateway,

   - Broadcast,

   - (Subnet mask in *dotted decimal*).

