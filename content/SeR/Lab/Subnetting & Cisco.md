# Subnetting
##### Classi
Prima IP erano in classi:
A: 8 bit rete, 24 bit host  | [0|...]   | host configurabili: 2^24 - 1 = 16M
B: 16 bit rete, 16 bit host | [10|...]  | host configurabili: 2^16 - 1 = 65K
C: 24 bit rete, 8 bit host  | [11|...]  | host configurabili: 2^8 - 1 = 255
D: per multicast | E: per usi sperimentali

192.168.1.0/24
è di classe C perché la subnet sarebbe 255.255.255.0 (possibile fare con subnet mask o CIDR)

Indirizzi:
- rete --> 1° bit 
- broadcast --> ultimo bit
- gateway --> 1° (ma anche ultimo) bit senza rete e broadcast

### Tipi di subnetting
##### FLSM (Fixed Length Subnetting Mortemarinale)
  Da usare quando in una rete gli host sono sempre quelli (al max diminuiscono), ma non eccedono mai il n° max statico fisso specificato
  ES: 
    (Per configurare 100 pc divisi in 10 subnet)
    n° pc = (10 + 1 + 1 + 1?) = 13 (tra IP dei pc, ind rete, ind broadcast e gateway?) --> 2^4 = 16 bit (dimensione rete a multipli di 2)
    10 reti da 16 bit = 160 bit < 255 bit (2^8 - 1) Quindi sì, ci stiamo in un classe C, ma ci stiamo meglio in una /28??? PERCHE????
    R1 = 192.168.1.0/28 | Broadcast = ...15
    R2 = 192.168.1.16/28 | Broadcast = ...31
    ...
    R10 = 192.168.1.144/28 | Broadcast = ...159 
##### VLSM (Variable Length Subnetting Mortemarinale)
  Da usare quando non si conosce il n° degli host a prescindere, e questi potrebbero variare (aumentando o diminuendo)
  ES:
    (Devo fare delle reti:) - 1 da 8 host, 2 da 17 host e 5 da 60 host
    1 - 8 host --> 1 * 16 bit
    2 - 17 host --> 2 * 32 bit
    5 - 60 host --> 5 * 64 bit
    tot = 400 bit --> quindi useremo una classe B? 172.168.0.0/16 no, questa è quella disponibile, si parte con la subnet fatta da 32 - bit rete >, quindi 26 (32 - 6)
    Perciò:
    - Reti da 64 a 6 bit
      R1 = 172.168.0.0/26 | Broadcast = ..0.63
      R2 = 172.168.0.64/26 | Broadcast = ..0.127
      R3 = 172.168.0.128/26 | Broadcast = ..0.191
      R4 = 172.168.0.192/26 | Broadcast = ..0.255
      R5 = 172.168.1.0/26 | Broadcast = ..1.63
    - Reti da 32 a 5 bit
      R6 = 172.168.1.64/27 | Broadcast = ..1.95
      R7 = 172.168.1.96/27 | Broadcast = ..1.127
    - Rete da 16 a 4 bit
      R8 = 172.168.1.0/28 | Broadcast = ..0.143

ES RIPASSO 1 ----------------------------------------------------------------------------------------------------------------------------
Oltre a ogni host c'e ind rete, broadcast, gateway
IP dato: 192.168.0.0/16 (SOLO NEI CASI IN CUI è CHIESTO DI DARE UN INDIRIZZO INIZIALE ALLORA SI FA SOMMA DI TUTTI GLI HOST E SI PRENDE LA POTENZA DI 2 >, SE GIà DATO ALLORA ANDARE CON POTENZA DI RETE PIU GRANDE)

R1 = 11300 host = 2^14 = 16384
- Rete        --> 192.168.0.0
- Gateway     --> 192.168.0.0
- 1° host     --> 192.168.0.0
- Broadcast   --> 192.168.0.0
- Last host   --> 192.168.0.0
- Subnet mask --> 255.255.192.0 = /18

R2 = 4500 host = 2^13 = 8192
- Rete        --> 192.168.0.0
- Gateway     --> 192.168.0.0
- 1° host     --> 192.168.0.0
- Broadcast   --> 192.168.0.0
- Last host   --> 192.168.0.0
- Subnet mask --> 192.168.0.0 = /19

R3 = 1744 host = 2^11 = 2048
- Rete        --> 192.168.0.0
- Gateway     --> 192.168.0.0
- 1° host     --> 192.168.0.0
- Broadcast   --> 192.168.0.0
- Last host   --> 192.168.0.0
- Subnet mask --> 192.168.0.0 = /21

R4 = 400 host = 2^9 = 512
- Rete        --> 192.168.0.0
- Gateway     --> 192.168.0.0
- 1° host     --> 192.168.0.0
- Broadcast   --> 192.168.0.0
- Last host   --> 192.168.0.0
- Subnet mask --> 192.168.0.0 = /23

R5 = 7 host = 2^4 = 16
- Rete        --> 192.168.0.0
- Gateway     --> 192.168.0.0
- 1° host     --> 192.168.0.0
- Broadcast   --> 192.168.0.0
- Last host   --> 192.168.0.0
- Subnet mask --> 192.168.0.0 = /28

R6 = 6 host = 2^4 = 16
- Rete        --> 192.168.0.0
- Gateway     --> 192.168.0.0
- 1° host     --> 192.168.0.0
- Broadcast   --> 192.168.0.0
- Last host   --> 192.168.0.0
- Subnet mask --> 192.168.0.0 = /28

ES RIPASSO 2 ----------------------------------------------------------------------------------------------------------------------------
: 192.168.192.0/18
tot = ? < /18 (2^14 bit = 16384) --> quindi ok

R1 = 1020 host = 2^10 = 1024
- Rete        --> 192.168.192.0
- Gateway     --> 192.168.192.1
- 1° host     --> 192.168.192.2
- Last host   --> 192.168.195.254
- Broadcast   --> 192.168.195.255 --> 11|000000 = ..192. (indirizzo base), se aggiungo bit a 1 broadcast = 11|000011 = 195
- Subnet mask --> 255.255.252.0 = /22

R2 = 499 host = 2^9 = 512
- Rete        --> 192.168.196.0
- Gateway     --> 192.168.196.1
- 1° host     --> 192.168.196.2
- Last host   --> 192.168.197.254
- Broadcast   --> 192.168.197.255 --> 11|000011... (metodo: aggiungo bit (qui 512) e tolgo 1 x broadcast)
- Subnet mask --> 255.255.254.0 = /23

R3 = 121 host = 2^7 = 128
- Rete        --> 192.168.198.0
- Gateway     --> 192.168.198.1
- 1° host     --> 192.168.198.2
- Last host   --> 192.168.198.126
- Broadcast   --> 192.168.198.127
- Subnet mask --> 255.255.255.128 = /25

R4 = 103 host = 2^7 = 128
- Rete        --> 192.168.198.128
- Gateway     --> 192.168.198.129
- 1° host     --> 192.168.198.130
- Last host   --> 192.168.198.254
- Broadcast   --> 192.168.198.255
- Subnet mask --> 255.255.255.128 = /25

R5 = 61 host = 2^6 = 64
- Rete        --> 192.168.199.0
- Gateway     --> 192.168.199.1
- 1° host     --> 192.168.199.2
- Last host   --> 192.168.199.62
- Broadcast   --> 192.168.199.63
- Subnet mask --> 255.255.255.192 = /26

R6 = 8 host = 2^4 = 16
- Rete        --> 192.168.199.64
- Gateway     --> 192.168.199.65
- 1° host     --> 192.168.199.66
- Last host   --> 192.168.199.78
- Broadcast   --> 192.168.199.79
- Subnet mask --> 255.255.255.240 = /28

ES RIPASSO 3 ----------------------------------------------------------------------------------------------------------------------------
R1 	= ROvini = 1000 bestie
R2 	= RCapre = 794 bestie
R3 	= RLatteRaccolta = 8 cisterne
R4	= RLattePastorizzazione = 3 bidoni 
RC 	= RLatteImbottigliamento = 5 supplychain dove ogni catena ha 25 sensori (ogni sottorete è una IN)
R5 	= RUfficiAmministrativo = 15 dipendenti (ognuno con pc e smartphone)
R6	= RUfficiCommerciale = 15 dipendenti (pc, smartphone e tablet) + 3 stampanti 3d
Varie SN reti di collegamento
NonnoNanni, dal suo ufficio, vuole sapere dove si trova ogni capo. Reparti comunicano tra loro

R1 = 1000 host = 2^10 = 1024
R2 = 794 host = 2^10 = 1024
R3 = 8 host = 2^4  = 16
R4 = 3 host = 2^3  = 8
I1 = 25 host = 2^5 = 32
I2 = 25 host = 2^5 = 32
I3 = 25 host = 2^5 = 32
I4 = 25 host = 2^5 = 32
I5 = 25 host = 2^5 = 32
R6 = 15 * 2 host = 30 = 2^6 = 64
R7 = 5 * 3 + 3 host = 18 = 2^5 = 32
RN = 1 host = 2^2 = 4
S1 = 2 host = 2^2 = 4
S2 = 2 host = 2^2 = 4
S3 = 2 host = 2^2 = 4
SA = 5 host = 2^3 = 8
Sim = 6 host = 2^3 = 8
S9 = 2 host = 2^2 = 4
S10 = 2 host = 2^2 = 4

Tot = 2368 = 2^12 = 4096 = subs --> /20
ind base = 172.100.0.0/20

R1 = 1000 host = 2^10 = 1024
- Rete        --> 172.100.0.0
- Gateway     --> 172.100.0.1
- 1° host     --> 172.100.0.2
- Last host   --> 172.100.3.254
- Broadcast   --> 172.100.3.255
- Subnet mask --> 255.255.252.0 = /22

R2 = 794 host = 2^10 = 1024
- Rete        --> 172.100.4.0
- Gateway     --> 172.100.4.1
- 1° host     --> 172.100.4.2
- Last host   --> 172.100.7.254
- Broadcast   --> 172.100.7.255
- Subnet mask --> 255.255.252.0 = /22

R6 = 30 host = 2^6 = 64
- Rete        --> 172.100.8.0
- Gateway     --> 172.100.8.1
- 1° host     --> 172.100.8.2
- Last host   --> 172.100.8.62
- Broadcast   --> 172.100.8.63
- Subnet mask --> 255.255.255.192 = /26

R7 = 18 host = 2^5 = 32
- Rete        --> 172.100.8.64
- Gateway     --> 172.100.8.65
- 1° host     --> 172.100.8.66
- Last host   --> 172.100.8.94
- Broadcast   --> 172.100.8.95
- Subnet mask --> 255.255.255.224 = /27

I1 = 25 host = 2^5 = 32
- Rete        --> 172.100.8.96
- Gateway     --> 172.100.8.97
- 1° host     --> 172.100.8.98
- Last host   --> 172.100.8.126
- Broadcast   --> 172.100.8.127
- Subnet mask --> 255.255.255.224 = /27

I2 = 25 host = 2^5 = 32
- Rete        --> 172.100.8.128
- Gateway     --> 172.100.8.129
- 1° host     --> 172.100.8.130
- Last host   --> 172.100.8.158
- Broadcast   --> 172.100.8.159
- Subnet mask --> 255.255.255.224 = /27

I3 = 25 host = 2^5 = 32
- Rete        --> 172.100.8.160
- Gateway     --> 172.100.8.161
- 1° host     --> 172.100.8.162
- Last host   --> 172.100.8.190
- Broadcast   --> 172.100.8.191
- Subnet mask --> 255.255.255.224 = /27

I4 = 25 host = 2^5 = 32
- Rete        --> 172.100.8.192
- Gateway     --> 172.100.8.193
- 1° host     --> 172.100.8.194
- Last host   --> 172.100.8.222
- Broadcast   --> 172.100.8.223
- Subnet mask --> 255.255.255.224 = /27

I5 = 25 host = 2^5 = 32
- Rete        --> 172.100.8.224
- Gateway     --> 172.100.8.225
- 1° host     --> 172.100.8.226
- Last host   --> 172.100.8.254
- Broadcast   --> 172.100.8.255
- Subnet mask --> 255.255.255.224 = /27

R3 = 8 host = 2^4 = 16
- Rete        --> 172.100.9.0
- Gateway     --> 172.100.9.1
- 1° host     --> 172.100.9.2
- Last host   --> 172.100.9.14
- Broadcast   --> 172.100.9.15
- Subnet mask --> 255.255.255.240 = /28

R4 = 3 host = 2^3 = 8
- Rete        --> 172.100.9.16
- Gateway     --> 172.100.9.17
- 1° host     --> 172.100.9.18
- Last host   --> 172.100.9.22
- Broadcast   --> 172.100.9.23
- Subnet mask --> 255.255.255.248 = /29

SA = 5 host = 2^3 = 8
- Rete        --> 172.100.9.24
- Gateway     --> 172.100.9.25
- 1° host     --> 172.100.9.26
- Last host   --> 172.100.9.30
- Broadcast   --> 172.100.9.31
- Subnet mask --> 255.255.255.248 = /29

Sim = 6 host = 2^3 = 8
- Rete        --> 172.100.9.32
- Gateway     --> 172.100.9.33
- 1° host     --> 172.100.9.34
- Last host   --> 172.100.9.38
- Broadcast   --> 172.100.9.39
- Subnet mask --> 255.255.255.248 = /29

RN = 1 host = 2^2 = 4
- Rete        --> 172.100.9.40
- Gateway     --> 172.100.9.41
- 1° host     --> 172.100.9.42
- Last host   --> 172.100.9.42
- Broadcast   --> 172.100.9.43
- Subnet mask --> 255.255.255.252 = /30

S1 = 2 host = 2^2 = 4
- Rete        --> 172.100.9.44
- Gateway     --> 172.100.9.45
- 1° host     --> 172.100.9.46
- Last host   --> 172.100.9.46
- Broadcast   --> 172.100.9.47
- Subnet mask --> 255.255.255.252 = /30

S2 = 2 host = 2^2 = 4
- Rete        --> 172.100.9.48
- Gateway     --> 172.100.9.49
- 1° host     --> 172.100.9.50
- Last host   --> 172.100.9.50
- Broadcast   --> 172.100.9.51
- Subnet mask --> 255.255.255.252 = /30

S3 = 2 host = 2^2 = 4
- Rete        --> 172.100.9.52
- Gateway     --> 172.100.9.53
- 1° host     --> 172.100.9.54
- Last host   --> 172.100.9.54
- Broadcast   --> 172.100.9.55
- Subnet mask --> 255.255.255.252 = /30

S4 = 2 host = 2^2 = 4
- Rete        --> 172.100.9.56
- Gateway     --> 172.100.9.57
- 1° host     --> 172.100.9.42
- Last host   --> 172.100.9.42
- Broadcast   --> 172.100.9.43
- Subnet mask --> 255.255.255.252 = /30

manca 1



--------------------------------------------------------------------

192.168.69.0/19
r1 = 5h
r2 = 1500h
r3 = 1000h
r4 = 55h
r5 = 2000h
r6 = 1000h

