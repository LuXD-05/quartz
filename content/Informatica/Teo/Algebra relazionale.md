# Definizione
Interrogare un db = ottenere info desiderate estraendole da una tabella, una sottotabella o una combinazione di esse. I linguaggi di interrogazione si basano sull’algebra relazionale. 
Il risultato di una query su una relazione è un’altra relazione con grado e cardinalità dipendenti dalle operazioni.
Operazioni: unione, differenza, prodotto, proiezione, restrizione, intersezione, join.
## Tipi di operazioni
Fondamentali
- Unarie (1 relazione): selezione (σ), proiezione (π)
- Binarie (2 o + relazioni): Unione (U), differenza (-), prodotto cartesiano (X)
Derivate
- Binarie: intersezione (), join (infinito a triangoli).
## Compatibilità
2 relazioni sono compatibili all’unione se:
- Hanno lo stesso grado (n° attributi),
- Ogni attributo nella stessa posizione è dello stesso tipo (stesso dominio)
R1(a11, a12, … a1N) e R2(a21, a22, … a2N) sono compatibili all’unione se, avendo lo stesso grado N, risulta anche vero che dominio(a1i) = dominio(a2i) per ogni 1 <= i <= N.
# Operazioni
### Unione
Date 2 relazioni R e S compatibili all’unione, il risultato dell’unione è: R ∪ S = { t | t ∈ R  OR  t ∈ S }
(R unione S è l’insieme ( {} ) delle tuple t tali che ( | ) t appartiene (e) a R oppure t appartiene ad S).
### Intersezione
Date 2 relazioni R e S, l’intersezione di R e S da la relazione fatta da tutte le tuple presente sia in R sia in S. 
Il risultato dell’intersezione è  R ∩ S = { t | t ∈ R  AND  t ∈ S }
Grado(RintS) = grado r = grado s
Cardinalità = ?
### Differenza
Date 2 relazioni R e S, la differenza di R con S è la relazione data dalla differenza insiemistica R - S. 
Il risultato della  è  R-S = { t | t ∈ R  AND  t ∉ S } 
Grado = grado r = grado s
Card() = Card r – n° tuple contenute (oltre che in R) anche in S
Mentre quello della differenza S-R = { t | t ∈ S  AND  t ∉ R }
Grado = grado r = grado s
Card() = Card S – n° tuple contenute (oltre che in S) anche in R
(ES: date le 2 relazioni Clienti(…) e Fornitori(…) visualizzare solo i clienti)
### Prodotto cartesiano
Date 2 relazioni R e S, il loro prodotto cartesiano è la relazione data da R * S. 
Il prodotto cartesiano di 2 relazioni è l’insieme di tutte le possibili tuple ottenibili concatenando ogni tupla di R con ogni tupla di S. 
Dalle 2 relazioni R e S, rispettivamente di grado g1 e g2 e cardinalità c1 e c2, il prodotto di R e S è la relazione di grado g1 + g2 e cardinalità c1 * c2 le cui tuple si ottengono concatenando ogni tupla di R con ogni tupla di S.
Siano r = (a1, a2, … an) e S = (b1, b2, … bn) due tuple; la concatenazione di R e S è data da:
R conc S = (a1, a2, … an, b1, b2, … bn2)
Il risultato del prodotto cartesiano è  R * S = { t | t = R conc S…t ∈ R AND t ∈ S }
### Proiezione
La proiezione di una relazione R (a1, a2, … an) di grado N su un suo sottoinsieme qualunque di attributi a1, a1, … ak e una relazione di grado K 
Il risultato dell’intersezione è  π_(a1,a2…)  = { t ┤|  t∈R }
…
Grado (rel. Risultante) = K
Card (rel. Risultante) <= card(R)
### Restrizione
Data una relazione R (a11, a12, … a1n) e una condizione C, espressa sugli attributi di R, la restrizione di R in base a C è una elazione contenente tutte e solo le uple che soddisfano la condizione data.
Il risultato della restrizione è: σ_C (R)= { t ┤|  t∈R AND C(t)= true }
ES: Studente(id, nome, cognome, classe, voto) --> T = (sigma)cognome=”rossi”(studente) --> R = (pi)voto(T)
Grado(rel ris) = grado(orig)
Card(rel ris) <= card(orig)
