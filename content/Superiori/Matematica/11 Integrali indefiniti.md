---
public: true
edited_seconds: 1970
modified_at: 21/05/2024 16:34:47
---
### Primitive
Hint: cosa sono, def, es e (non sono uniche)
::
L'**integrazione** è l'<u>operazione inversa alla derivazione</u>; e se $f(x) = 2x$ è una funzione derivata, si definisce **primitiva** la sua funzione integrata $F(x) = x^{2}$.
> [!important] Primitiva
> Una funzione $F(x)$ è una **primitiva** di $f(x)$ se $F(x)$ è **derivabile** e la sua **derivata** è $f(x)$, per cui: $F'(x) = f(x)$
###### Esempio
Nell'esempio iniziale, la primitiva $F(x) = x^{2}$ è derivabile e la sua derivata è $f(x) = 2x$.
Le **primitive** però, non <u>sono uniche per le loro derivate</u> in quanto derivare una funzione alla quale si <u>aggiunge o si toglie un numero</u> $c$ reale risulterà sempre nella stessa derivata: $F'(x) + c = f(x)$.
![](https://i.imgur.com/YKDMYfn.png)
<!--SR:!2024-05-29,8,240-->

### Integrale indefinito
Hind: def, notazione + f(x) integranda e primitiva
::
> [!important] Integrale indefinito
> L'**integrale indefinito** di una funzione $f(x)$ è l'**insieme** di tutte le sue **primitive** $F(x) + c$
###### Altro
**Notazione**: $\displaystyle \int[f(x)] \; dx \;=\; [F(x)] + c$
Dove:
- $f(x)$ = funzione ***integranda***.
- $F(x)$ = funzione **primitiva**.
<!--SR:!2024-06-01,11,242-->

### Derivabilità vs continuità vs integrabilità
::
--- start-multi-column: ID_5r5c
```column-settings
Number of Columns: 2
Largest Column: standard
Alignment: center
Border: off
```
 
![](https://i.imgur.com/eDfuJf7.png)
 
--- column-break ---
 
- **Derivabili**: sono funzioni sempre **Continue** e sempre **Integrabili**.
- **Continue**: sono funzioni sempre **Integrabili** ma <u>non</u> sempre **Derivabili**.
- **Integrabili**: sono funzioni <u>non</u> sempre **Continue** o **Derivabili**.
 
--- end-multi-column
<!--SR:!2024-05-29,8,242-->

### Applicazioni in fisica
Hint: relazione tra spazio, velocità e accelerazione + formula spazio
::
$\displaystyle S \;=\; \int V\,dx \;\;\;\rightarrow\;\;\; V \;=\; \int a\,dx$
$S(t) \;=\; \dfrac{1}{2}at^{2} + V_{0}t + S_{0}$
<!--SR:!2024-05-23,2,215-->

### Proprietà
Hint: (2)
::
###### 1
> [!important] Linearità 1
> L'integrale di una somma di funzioni è uguale alla somma delle singole funzioni integrate:
> $\displaystyle \int[f(x) + g(x)] \; dx \;=\; \int f(x) \; dx \;+\; \int g(x) \; dx$
###### 2
> [!important] Linearità 2
> L'(integrale di una funzione moltiplicata per una costante) è uguale all'(integrale della funzione) moltiplicato per la costante:
> $\displaystyle \int k * f(x) \; dx \;=\; k * \int f(x) \; dx$
<!--SR:!2024-05-23,11,240-->

### Tabella integrali immediati
(tab quad)

### Tabella integrali composti
(tab 1241)

### Tipi di integrazione
##### Sostituzione

###### Esempio

##### Per parti

###### Esempio

##### Di funzioni razionali (semplici)

###### Esempio: numeratore derivata del denominatore

###### Esempio: denominatore di 1° grado

##### Di funzioni razionali (denominatore di 2° grado)

###### Caso delta > 0

###### Caso delta = 0

###### Caso delta < 0

###### Caso delta < 0 (speciale)


---
Vedi poi: [[12 Integrali definiti]]