---
public: true
---
# Algebra relazionale
### Definizione
Interrogare un db significa ottenere le info desiderate estraendole da una tabella, una sottotabella o una combinazione di esse. I linguaggi di interrogazione si basano sull’algebra relazionale. 
Il risultato di una query su una relazione è un’altra relazione con grado e cardinalità dipendenti dalle operazioni. (Ripasso necessario per dopo:)
[[Progettazione logica#Grado|Grado di una relazione]], [[Progettazione logica#Cardinalità|Cardinalità di una relazione]]
### Tipi di operazioni
##### Fondamentali
###### Unarie 
Coinvolgono <u>1 sola relazione</u> e sono: **selezione** ($\sigma$), **proiezione** ($\pi$).
###### Binarie 
Coinvolgono <u>2 o + relazioni</u> e sono: **unione** ($\cup$), **differenza** ($-$) e **prodotto cartesiano** ($x$)
##### Derivate
###### Binarie 
Coinvolgono sempre <u>2 o + relazioni</u> e sono: **intersezione** ($\cap$), **join** (⨝).
### Compatibilità all'unione
2 relazioni sono compatibili all’unione se:
- Hanno lo stesso grado (n° attributi),
- Ogni attributo nella stessa posizione è dello stesso tipo (stesso dominio).
$R1(a_11,\; a_12, \;\ldots\; a_1N)$ e $R2(a_21,\; a_22, \;\ldots\; a_2N)$ sono compatibili all’unione se, avendo lo stesso grado N, risulta anche vero che dominio($a_1i$) = dominio($a_2i$) per ogni 1 <= i <= N. I nomi degli attributi nelle posizioni corrispondenti può anche essere diverso.
### Operazioni
##### Unione
Date 2 relazioni ***R*** e ***S*** <u>compatibili all’unione</u>, il risultato dell’**unione** è: 
$$R \;\cup\; S = \{\; t \;\lvert\; t \;\in\; R \;\;OR\;\; t \;\in\; S \;\}$$
Grado(R $\cup$ S) = Grado(R) = Grado(S).
Cardinalità(R $\cup$ S) = Card(R) + Card(S) - n° di tuple ripetute.
##### Intersezione
Date 2 relazioni ***R*** e ***S***, la loro **intersezione** da la relazione composta da tutte le tuple presenti in entrambe le relazioni (non solo in 1 delle 2 e completamente uguali). Il risultato dell’intersezione è:
$$R \;\cap\; S = \{\; t \;\lvert\; t \;\in\; R \;\;AND\;\; t \;\in\; S \;\}$$
Grado(R $\cap$ S) = Grado(R) = Grado(S).
Cardinalità(R $\cap$ S) = MIN(Cardinalità(R), Cardinalità(S)).
##### Differenza
Date 2 relazioni ***R*** e ***S***, la **differenza** di R con S è la relazione data dalla differenza insiemistica R - S (ovviamente è possibile anche il contrario S - R, ma qui non si applica la proprietà commutativa tra le 2 relazioni in quanto $S-R \neq R-S$). Perciò:
$$1) \;\; R - S = \{\; t \;\lvert\; t \;\in\; R \;\;AND\;\; t \;\notin\; S \;\}$$
$$2) \;\; S - R = \{\; t \;\lvert\; t \;\in\; S \;\;AND\;\; t \;\notin\; R \;\}$$
Per il **1° caso**:
Grado(R - S) = Grado(R) = Grado(S).
Cardinalità(R - S) = Cardinalità(R) – n° tuple presenti (oltre che in R) anche in S.
Per il **2° caso**:
Grado(S - R) = Grado(R) = Grado(S).
Cardinalità(S - R) = Cardinalità(S) – n° tuple presenti (oltre che in S) anche in R.
##### Prodotto cartesiano
Date 2 relazioni ***R*** e ***S***, il loro **prodotto cartesiano** è l’insieme di tutte le possibili tuple ottenibili concatenando ogni tupla di R con ogni tupla di S. 

Dalle 2 relazioni R e S, rispettivamente di grado g1 e g2 e cardinalità c1 e c2, il prodotto di R e S è la relazione di grado g1 + g2 e cardinalità c1 * c2 le cui tuple si ottengono concatenando ogni tupla di R con ogni tupla di S.
Siano $R = (a_1,\; a_2, \;\ldots\; a_n)$ e $S = (b_1,\; b_2, \;\ldots\; b_n)$ due tuple; la concatenazione di R e S è data da: R *conc* S = (a1, a2, … an, b1, b2, … bn2).

Il risultato del prodotto cartesiano è: R * S = { t | t = R conc S…t ∈ R AND t ∈ S }
$$R \;x\; S = \{\; t \;\lvert\; t \;=\; r \;\;conc\;\; s,\; r \;\in\; R, \; s \;\in\; S \;\}$$
La **PK** della relazione risultante è data dall'unione delle PK delle 2 relazioni originali.
##### Proiezione
La **proiezione** di una relazione $R = (a_1,\; a_2, \;\ldots\; a_n)$ di grado *N* è un suo sottoinsieme qualunque di attributi $a_1,\; a_2, \;\ldots\; a_k$, ovvero una relazione di grado *K* con solo gli attributi $a_1,\; a_2, \;\ldots\; a_k$ ed eventuali tuple duplicate eliminate.
Il risultato dell’intersezione è:
$$S = {\huge\pi_{a_{1}, a_{2} \;\ldots\; a_{k}}}(R) = \{\; t \;\lvert\; t \;\in\; R \;\}$$
Grado(S) = K.
Cardinalità(S) $\small\leq$ Cardinalità(R).
##### Restrizione
Date una relazione $R(a_11,\; a_12, \;\ldots\; a_1N)$ e una condizione $C$ (espressa sugli attributi di $R$), la **restrizione** di $R$ in base a $C$ è una relazione contenente (tutte e solo) le tuple che soddisfano $C$. Il risultato della restrizione è: 
$$S = {\huge\sigma}_{\small{C}}\,(R) = \{\; t \;\lvert\; t \;\in\; R \;\;AND\;\; C(t) \;=\; true \;\}\}$$
La restrizione difatti seleziona un certo n° di righe della tabella della relazione.
Grado(S) = Grado(R).
Cardinalità(S) $\small\leq$ Cardinalità(R).
###### Problemi della restrizione
- **Formale** = sto usando l'operatore di restrizione per qualcosa che non ? ...
- **Di leggibilità** = con il prodotto cartesiano non si capisce che tabelle si usano in quanto non c'è un operatore specifico che rappresenti la congiunzione delle 2 tabelle.
- **Di ottimizzazione** = Facendo il prodotto cartesiano di 2 tabelle con migliaia di righe, ottenere la tabella risultante richiede tanto tempo e risorse.
 Rispetto al prodotto cartesiano c'è però un'opzione migliore.
# Join
Le **join** permettono di risolvere tutti questi problemi e se prima si faceva il prodotto cartesiano insieme alle altre clausole di restrizione, adesso 
### Cos'è
La **join** è un'operazione binaria che consente di **congiungere** 2 relazioni **concatenandone le tuple** in base a una **condizione** in cui sono utilizzati gli attributi delle 2 relazioni stesse.
### Scopo
Il suo **scopo** è **combinare 2 relazioni** aventi **1 o + attributi in comune** generando una nuova relazione. L'operazione agisce solo se per le 2 relazioni specificato **almeno 1 attributo in comune** tra le 2 (anche con nome diverso, ma dello stesso dominio). 
La join restituisce una relazione che avrà:
- Gli attributi (colonne) sia della 1a sia della 2a relazione senza duplicazioni.
- Le tuple (righe) della 1a relazione concatenate a quelle della 2a in base ai valori dell'attributo in comune.
Sintassi:
$$T = R \underset{\tiny PK = FK}{⨝} S\; = \{\; r \;conc\; s \;\lvert\; r \;\in\; R \;\;AND\;\; s \;\in\; S \;\;AND\;\; R.pk \;=\; S.fk \;\}$$
Generalmente gli attributi in comune saranno la **PK di R** e la relativa **FK di S**.
Grado(T) = Grado(R) + Grado(S) - 1.
Cardinalità(T) = non prevedibile a priori, dato che dipende da quante tuple di R e S soddisfano la condizione data.
##### Inner join
A loro volta divise in:
###### Natural join
**Simbolo**: ⨝.
In questa le uguaglianze sono specificate su tutti gli attributi con lo stesso nome (è dove la FK è = alla PK )
**Questo**: $T = {\large\pi_{targa,modello}}({\large\sigma_{cognome='rossi' \;AND\; CF=fkPersona}}(Persona \;\,x\; Auto))$
**Diventa**: $T = {\large\pi_{targa,modello}}({\large\sigma_{cognome='rossi'}}(Persona \,⨝\, Auto))$
Questo funziona solo se entrambi i 2 attributi delle 2 tabelle si chiamano allo stesso modo (in mysql si definisce lo stesso, qua no).
###### Equi-join
**Simbolo** $\underset{<cond>}{⨝}\;$. Meglio usarla sempre per evitare di sbagliare.
**Questo**: $T = {\large\pi_{targa,modello}}({\large\sigma_{cognome='rossi' \;AND\; CF=fkPersona}}(Persona \;\,x\; Auto))$
**Diventa**: $T = {\large\pi_{targa,modello}}({\large\sigma_{cognome='rossi'}}(Persona \underset{\tiny CF = fkPersona}{⨝} Auto))$
Formalmente bisogna necessariamente scrivere la **chiave** sulla **parte della relazione giusta**, quindi non va bene tipo: (Persona x Auto) e sotto (fkPersona = CF).
##### Outer join
Nelle inner join le congiunzioni sono fatte solo sulle tuple di 2 relazioni distinte con valori = per gli attributi corrispondenti.
Le **outer join** invece, congiungono 2 relazioni restituendo tutte le **tuple** (sempre **concatenando quelle con PK = FK**) **anche se non sono presenti valori = per l'attributo in comune** (sostituiti da NULL).
In sostanza, sono combinate solo le righe della 1a dove il suo attributo comune trova un valore = nella colonna dell'attributo corrispondente della 2a relazione; mentre le altre righe sono ricopiate aggiungendo NULL negli attributi aggiunti/non in comune.
A loro volta divise in:
###### Left join
La **left outer join** elenca tutte le **righe della 1a relazione** <u>congiungendole</u> **con** quelle della **2a** solo **quando l'attributo comune è uguale**. Per **le altre** righe invece, **congiunge impostando NULL agli attributi** concatenati **della 2a relazione**.
###### Right join
La **right outer join** restituisce tutte le **righe della 2a relazione** <u>congiungendogli</u> le righe della **1a** **solo se il valore** di queste **corrisponde** a quello che c'è nell'**attributo comune della 2a** relazione.
###### Full join
La **full outer join** applica contemporaneamente la **left outer join** e la **right outer join**, restituendo tutte le righe della 1a relazione con NULL dove la 2a non ha un valore corrispondente nell'attributo comune + tutte le righe della 2a con NULL dove la 1a non ha un valore corrispondente nell'attributo comune (questo non duplicando le righe uguali indipendentemente dall'ordinamento degli attributi).
**MySQL** <u>non</u> supporta direttamente la **full outer join**, perciò è necessario fare una `UNION` tra la left e la right join che si stanno cercando di effettuare.
