---
modified_at: 28/09/2024 14:22:00
---
# Todo
### Mate
#### Lista
##### Pre
- [ ] CE (in generale, tipo denom != 0 oppure | x | --> per ogni x in R)

##### Monomi e polinomi
###### Divisione tra polinomi
- [x] Divisione euclidea (con resto)
- [x] Divisione con metodo di Ruffini (+ considerazioni sul teorema del resto)
##### Sistemi
###### Sistemi lineari
- [x] Sistemi lineari
##### Geometria analitica
###### Piano cartesiano

###### Vettori

###### Fasci di rette
- [ ] Fasci di rette (def)
- [ ] Teorema di Talete ("piccolo" e "grande")
- [ ] (Omotetie?)
##### Radicali
###### Generale
- [ ] Definizione, indice e radicando
- [ ] CE (indice pari = radicando >= 0) + casi e risoluzione (normale, radicale pari radicando fratto, radicali pari multipli, nessuna x in R)
- [ ] Proprietà invariantiva (radicali equivalenti e proprietà ())
- [ ] Proprietà (+ trasporti fuori/sotto radice), CE
- [ ] Operazioni (+, -, \*, /, ^, $\sqrt{n}$)
###### Altro
- [ ] (radicali quadratici doppi???)
- [ ] Razionalizzazione
- [ ] Equazioni, disequazioni e sistemi con radicali
- [ ] Numeri irrazionali
##### Equazioni e disequazioni

#### Teoria ed esercizi
##### Pre
###### CE

##### Monomi e polinomi
###### Divisione euclidea
Supponiamo di avere 2 polinomi (rispettivamente dividendo e divisore):
$A(x) = 6x^{3} - 4x^{2} + 1$
$B(x) = 2x^{2} + 1$
Ci sono quindi 4 passi da rispettare (ed eventualmente rifare/reiterare finché il resto parziale ha grado minore di quello del divisore):
1) Ordinare i 2 polinomi in modo decrescente in base agli esponenti (in caso ne manchi qualcuno nel dividendo, lo si riscrive con coefficiente nullo).
2) Dividere il termine con grado massimo del dividendo per il termine di grado massimo del divisore, ottenendo il 1° termine del quoziente.
3) Moltiplicare (solo) il termine appena ottenuto del quoziente per l'intero divisore e sommare poi tale risultato al dividendo cambiandogli però prima i segni e ottenendo il 1° resto parziale.
4) Ripetere i passi 2 e 3 (assumendo come nuovo dividendo il resto parziale) finché non si ottiene un resto parziale avente grado minore di quello del divisore; a questo punto la divisione è conclusa e si hanno quoziente e resto.
(Per soluzioni relative all'esercizio: [[#Divisione normale]])
###### Divisione con Ruffini
Si può dividere utilizzando il metodo di Ruffini solo se:
- Il divisore è un binomio di 1° grado,
- Il coefficiente del termine non noto del divisore è 1.
Supponiamo quindi di avere 2 polinomi (rispettivamente dividendo e divisore):
$A(x) = 2x^{3} - 5x^{2} + 2x - 3$
$B(x) = x + 1$
Ci sono diversi passi da rispettare:
1) Ordinare i 2 polinomi in modo decrescente in base agli esponenti (in caso ne manchi qualcuno nel dividendo, lo si riscrive con coefficiente nullo).
2) Costruire lo schema con i coefficienti del dividendo nella 1a riga (tutti in mezzo tranne il termine noto in 3a colonna) e l'<u>opposto del termine noto del divisore</u> in una 2a riga (e nella 1a colonna).
3) Ricopiare il 1° coefficiente "abbassandolo" in una 3a riga.
4) Moltiplicare l'opposto del termine noto per il numero appena scritto in 3a riga e scrivere il risultato in 2a riga incolonnato sotto il coefficiente successivo.
5) Sommare il coefficiente al di sopra del numero appena scritto con lo stesso e riportare il risultato nella stessa colonna in 3a riga.
6) Ripetere i punti 4 e 5 finché non si sommano il termine noto del dividendo ed il numero incolonnato sotto di esso, ottenendo quindi (nella stessa colonna in 3a riga) il resto R e (in 2a colonna e 3a riga) i coefficienti del quoziente (con 3 coefficienti a, b e c, si avrà un trinomio così: $ax^{2} + bx + c$, considerando anche i segni negativi dei coefficienti).
(Per soluzioni relative all'esercizio: [[#Divisione con metodo di Ruffini]])
![](https://i.imgur.com/qyWPsVj.jpeg)
##### Sistemi
###### Sistemi lineari
I sistemi lineari sono semplicemente gruppi di 2 o + equazioni di 1° grado in 1 o + incognite. Si dividono in 3 tipi:
- Determinati: hanno una sola soluzione (una n-upla che, se sostituita alle n incognite risolve tutte le equazioni),
- Indeterminati: ammettono infinite soluzioni,
- Impossibili: non ammettono soluzioni.
###### Risoluzioni
Sono diversi i modi coi quali è possibile risolvere i sistemi lineari:
\1) **Sostituzione**
Consiste semplicemente nell'isolare un'incognita in 1 delle equazioni del sistema per poi sostituire il valore di essa (ciò che c'è dall'altra parte dell'uguale) al posto della stessa incognita nelle altre equazioni del sistema.
\2) **Confronto**
Come per la sostituzione, si isola un'incognita ma stavolta lo si fa in entrambe (nel caso semplice di un sistema a 2 equazioni) le equazioni del sistema.
Mentre poi 1 delle 2 equazioni si riscrive, al posto dell'altra si mette il valore dell'incognita della 1a = al valore dell'incognita della 2a; in seguito si ricava il valore dell'altro termine non noto e si sostituisce infine nella 1a equazione.
\3) **Riduzione**
https://www.youmath.it/lezioni/algebra-elementare/equazioni/168-metodi-di-risoluzione-per-sistemi-lineari-3-riduzione.html
\4) **Metodo di Cramer**
https://www.youmath.it/lezioni/algebra-elementare/equazioni/170-metodi-di-risoluzione-per-sistemi-lineari-4-cramer.html
##### Geometria analitica
###### Piano euclideo
(short)
Nel piano euclideo sono definiti 3 concetti primitivi:
- Punti: si indicano con lettere maiuscole dell'alfabeto,
- Rette: ... minuscole ... 
- Piani: ... lettere dell'alfabeto greco.

Importante è poi definire degli assiomi (o postulati), teorie assunte e accettate come vere senza giustificarle e sono:

> [!important] Assioma 1
> Ogni piano è un'insieme di punti.
> Ogni retta è un sottoinsieme del piano.

> [!important] Assioma 2 (assiomi di appartenenza della retta)
> 1) A ogni retta appartengono almeno 2 punti distinti,
> 2) Per 2 punti passa (per entrambi) 1 e 1 sola retta alla quale appartengono,
> 3) Data una retta in un piano esiste almeno un punto di esso che non appartiene alla retta.

> [!important] Assioma 3 (assiomi di ordine della retta)
> 1) Dati 2 punti distinti A e B in una retta (tali che A precede B) esiste sempre un punto P compreso tra A e B (A > P > B),
> 2) Dato un punto P in una retta, esistono sempre 2 punti A e B tali che A precede P e P precede B (A > P > B).

(semirette, segmenti e poligonali)

(semipiani, angoli e poligoni)

###### Piano cartesiano

###### Vettori
Geometricamente un vettore è un segmento (chiamiamolo AB) orientato caratterizzato da diverse proprietà:
- **Direzione**: la retta che passa per entrambi gli estremi del vettore,
- **Verso**: il verso in cui va il vettore inteso (tipo da A a B o viceversa),
- **Modulo**: (o lunghezza) in pratica la misura dello stesso segmento AB.
Se inteso invece nel piano cartesiano, una più semplice e accessibile spiegazione del concetto di vettore permette di definirlo come una sorta di "quantità" misurata in coordinate x, y (ed eventualmente z in casi di piano a 3 dimensioni) in base alla quale un punto si dovrebbe spostare sul piano cartesiano.
Per esempio, al punto P(0,0) viene applicato un vettore AB(2,3); il punto P si sposterà su entrambi gli assi cartesiani di quanto il vettore indica, ritrovandosi alla fine alle coordinate (2,3).

(Vettori equipollenti e relazioni tra vettori).

###### Fasci di rette
Prima di dire cosa sono, i fasci di rette sono di 2 tipi:
- Fasci **propri**: insieme delle rette che passano per un punto specifico di un piano detto centro del fascio,
- Fasci **impropri**: insieme delle rette parallele tra loro in un piano.
Le rette possono anche distribuirsi in 3 dimensioni (affinché a tutte appartenga lo stesso punto (stella di rette) o tutte siano sempre parallele).

Se si considera l'equazione di una retta normale:
$$y = mx+q$$
Quando si parla di fasci di rette **propri**, questa viene modificata con un parametro aggiuntivo detto "$k$" moltiplicato alla pendenza ed all'intercetta ("$k$" è un'incognita, le 2 seguenti non sono sempre = anche se variano, quella della "$q$" indica una sempre una certa intercetta mentre quella della "$m$" indica la differente pendenza/inclinazione di ogni retta, al fine di diversificarle l'una dall'altra):
$$y = m(k)x + q(k)$$
oppure (per rette passanti per un centro noto in $x_{0},y_{0}$):
$$(y - y_{0}) = m(k)(x - x_{0})$$
> [!important] Come si passa da una all'altra?
> Dato il seguente grafico:
> ![](https://i.imgur.com/Ax1T2Vc.png)
> Dall'equazione generica di una retta: $y = mx + q$
> Si ricava l'equazione generica di un suo punto: $y_{0} = mx_{0} + q$
> Sottraendo alla 1a la 2a, si ottiene l'equazione di una retta generica passante per un punto: $y - y_{0} = m(x - x_{0})$.
> Tale equazione descrive, al variare di $m$, tutte le rette del fascio di centro ($x_{0},y_{0}$) (eccetto quella verticale con $x = x_{0}$).
> (TIP: si nota come da qui è semplice spiegare come è calcolata la formula inversa per la $m$).

> [!important] Attenzione!
> In alcuni esercizi ci si troverà davanti un'equazione del genere:
> $$(k + 2)x - (k - 1)y + k - 2 = 0$$
> Tale formula è semplicemente ricavabile:
> 1) Prendiamo 2 equazioni di 2 rette in forma implicita dette "generatrici del fascio":
>    $ax + bx + c = 0$
>    $a'x + b'y + c' = 0$
> 2) Da queste (supponendo che non siano parallele, altrimenti si avrebbe un fascio improprio) si ottiene un'equazione in tale forma:
>    $ax + by + c + k(a'x + b'y + c') = 0$
> 3) Sembra difficile, ma spostando le lettere si ottiene l'equazione equivalente: 
>    $(a + ka')x + (b + kb')y + (c + kc') = 0$
>    La quale è l'equazione del fascio generato dalle 2 rette generatrici.
> 4) Guarda caso, considerando ciò che sta dentro le parentesi come (per esempio) una lettera (supponiamo in ordine: a, b, c) si ottiene:
>    $ax + bx + c = 0$
> 5) Si può anche ottenere y e riportare l'equazione in forma esplicita con qualche spostamento:
>    ![](https://i.imgur.com/LEFr3kr.png)

Per quanto riguarda invece i fasci di rette **impropri**, anche qui si aggiunge un (solo) parametro "$k$" all'intercetta (siccome le varie rette si traslano tutte verticalmente ed hanno la stessa pendenza):
$$y = mx + q(k)$$
Sappiamo che un fascio di rette proprio è un insieme di rette con $q$ ed $m$ variabili (solitamente in base ad un parametro $k$) che passano tutte per un punto detto centro.

###### Teorema di Talete
Il "piccolo" teorema di Talete riguarda le corrispondenze (dette di Talete) tra segmenti omologhi creati su 2 o + linee trasversali rispetto ad un fascio di rette parallele (improprio).
![](https://i.imgur.com/CVj9AAs.png)
Viene quindi sancita la seguente proporzione:
$$AB : CD = A'B' : C'D'$$
secondo la quale è poi possibile trovare 1 dei segmenti della proporzione dati gli altri 3 (p.s., valgono anche BC e B'C', come anche AD e A'D'...).

Il corollario del teorema ne espande l'uso anche nello studio dei triangoli; in particolare nel caso in cui ci sia un triangolo che viene tagliato in 2 da una retta orizzontale (quindi dal segmento BB'):
![](https://i.imgur.com/dZ3ABzX.png)
Vale il rapporto di proporzionalità precedentemente sancito.
###### Esercizi pt. 1
\1) Determinare l'equazione della retta passante per P(1;3) e con coefficiente angolare (m) = $\frac{1}{2}$.
\2) Determinare l'equazione della retta passante per P1(1;1) e P2(2;3).
\3) Determinare il coefficiente angolare delle rette $r$ e $s$ con $r$ passante per A(3,-4) e B(-2,-4); e con $s$ passante per C(0,2) e D(0,-1)
\4) Determinare quali rette sono parallele e quali sono perpendicolari tra:
$$2x+3y-2=0\;\;\;3x-y+6=0\;\;\;-6x+2y=0\;\;\;3x-2y-8=0$$
\5) Dire se le rette $y=x-1$ e  $y=-\frac{1}{2}x+2$ si incrociano e trovare le coordinate dell'eventuale punto di intersezione.
\6) Calcolare la distanza di P(-2,2) dalla retta $y = x + 2$
\7) Scrivere l'equazione del fascio di rette con centro P(2,0)
###### Esercizi pt. 2
\1) Scrivi l'equazione della retta passante per $A(-\frac{1}{2},2)$ e $B(4,-\frac{3}{2})$ e trova la coordinata mancante del punto $C(-1,?)$
\2) Determina se i punti $A(2,1)$ e $B(1,1)$ appartengono alla retta di equazione $2x + y - 5 = 0$
\3) Data la retta di equazione $2x - y + 3 = 0$ ed il punto $A(h + 2, 3 - 2h)$, determina per quale valore di h il punto A appartiene alla retta
\4) ![](https://i.imgur.com/EMBUrk9.png)
\5) Determina se le le rette $r: 2x - 4y + 1 = 0$ e $s: x - 2y + 4$ sono parallele o perpendicolari; poi, nel 1° caso, calcolane la distanza, altrimenti la distanza tra l'origine ed il punto di intersezione.
\6) Dato il fascio di rette di equazione $y-2=m(x+5)$, determina in esso: a) il centro, b) la retta passante per il punto $B(-1,-2)$, c) la retta perpendicolare a quella di equazione $3x+8y+2=0$, d) la retta che dista $\frac{7\sqrt{2}}{2}$ dall'origine degli assi.
##### Radicali
http://www.iisviasilvestri.it/files/Malpighi_Masci.pdf
https://mc3-a2-01-numeri-reali.readthedocs.io/en/latest/02_Radicali.html#:~:text=non%20esiste%2C%20radicando%20negativo.,il%20risultato%20sia%20sicuramente%20positivo.
###### Intro
> [!important] Radicale
> Definizione: dati 2 numeri reali $a$ e $b$, si definisce radice n-esima di $a$ il numero reale $b$ la cui potenza n-esima è = ad $a$ (n pari: $a \ge 0, b \ge 0$).

$\sqrt[indice \;\rightarrow\; 3]{8} \;\leftarrow\; radicando$

Nonostante $5^{2} = 25$ e $(-5)^{2} = 25$, $\sqrt{25} = +5 \; (e \; \not= -5)$
Perciò non esiste un numero il cui **quadrato** sia = a un numero negativo; quindi $\sqrt{-25}$  non esiste. (Però la $\sqrt[3]{-125} = -5$)
###### CE
La CE nei radicali si ha solo se il loro **indice** è **pari** ed è: $\;\;[radicando] \,\ge\, 0$
(In caso di radicali fratti: $N \ge 0$ e $D > 0$)

ESERCIZI
Trova le CE di:
1) $\sqrt{x - 2}$
2) $\sqrt[4]{\dfrac{x - 1}{x + 2}}$
3) $\sqrt{x+2} - \sqrt{-x-3}$

###### Studio del segno (?)
https://youtu.be/VzpJJirpbWQ?list=PLkD_roTRRfAGu0lZmvitaxwve3wEhP5dy

###### Proprietà
> [!important] Invariantiva
> Dato un radicale con radicando positivo o 0, se ne ottiene uno equivalente moltiplicandone (o dividendone) l'indice e l'esponente del radicando per uno stesso numero:
> $$\sqrt[n]{a^{m}} \;=\; \sqrt[n * p]{a^{m * p}}$$
> (con $a \ge 0$ e $m, n, p$ numeri naturali != 0)
 
Quindi è possibile moltiplicare indice e radicando di un radicale per uno stesso numero dato che il valore del radicale stesso non cambia.

Al fine di confrontare 2 radicali (quasi come con le frazioni) è necessario ridurli allo stesso indice e confrontarne i radicandi.

La semplificazione dei radicali è quindi quell'operazione che si fa quando si dividono indice ed esponente del radicando di un radicale; però va fatta una considerazione quando si semplificano radicali con radicandi negativi o letterali.

Esempio (usato un radicando letterale perché non si sa che segno abbia, quindi si considera sia il caso in cui è positivo e sia quello in cui è negativo):
$\sqrt[4]{x^{2}} \;\rightarrow\; \sqrt[4:2]{x^{2:2}} = \sqrt[2]{x} \;\rightarrow\;$ valido solo se $x \ge 0$   (impossibile con x = -2)
${} \sqrt[4]{x^{2}} \;\rightarrow\; \sqrt[4:2]{x^{2:2}} = \sqrt[2]{|x|} \;\rightarrow\;$ valido sempre ($\forall x \in \mathbb{R}$)   (x = -2 in ogni caso diventa x = 2 grazie al modulo)

Quindi: in qualsiasi semplificazione che tratti un radicando letterale, quando si divide indice ed esponente del radicando per un numero pari **e** si ottiene un nuovo radicando con esponente **dispari**, bisogna rendere il radicando un valore assoluto col modulo, siccome sostituendo al nuovo radicando risultante un numero negativo, il radicale (se avente indice pari dopo la semplificazione) avrebbe come radicando un numero negativo.
Se invece il radicando semplificato ha esponente pari, non è necessario il modulo dato che elevando a potenza pari un numero negativo, si ottiene sempre un numero positivo.

ESERCIZI
1) Quali delle seguenti coppie sono equivalenti?
   $\sqrt{5},\sqrt[4]{125}$
   $\sqrt{6},\sqrt[6]{216}$
2) Quale radicale è maggiore tra: $\sqrt{3} \;e\; \sqrt[3]{5}$ ?
3) ![](https://i.imgur.com/w5BaCGn.png)
4) Semplificazione (hard): ![](https://i.imgur.com/uJdZajw.png)
   (se mai considerarle nel caso y >= 0)
5) ![](https://i.imgur.com/u5y5fUr.png)
###### Operazioni coi radicali
add, sott, molt, div ...
https://www.youtube.com/watch?v=SPhluqJfJN8&list=PLkD_roTRRfAGu0lZmvitaxwve3wEhP5dy&index=9&pp=iAQB
https://www.youtube.com/watch?v=v4ZSGZ79aP8&list=PLkD_roTRRfAGu0lZmvitaxwve3wEhP5dy&index=6&pp=iAQB

###### Portare fuori radice
https://www.youtube.com/watch?v=MUw6OFiA6O0&list=PLkD_roTRRfAGu0lZmvitaxwve3wEhP5dy&index=7&pp=iAQB

###### Razionalizzazione
https://www.youtube.com/watch?v=PkjyjQCmy5A&list=PLkD_roTRRfAGu0lZmvitaxwve3wEhP5dy&index=8&pp=iAQB

###### Equazioni di 2° grado con radicali
https://www.youtube.com/watch?v=7dALo7c4FNQ&list=PLkD_roTRRfAGu0lZmvitaxwve3wEhP5dy&index=10&pp=iAQB

###### Equazioni irrazionali con 2 radicali
https://www.youtube.com/watch?v=AzgwnCxzo3g&list=PLkD_roTRRfAGu0lZmvitaxwve3wEhP5dy&index=11&pp=iAQB

#### Soluzioni
##### Monomi e polinomi
###### Divisione normale
![](https://i.imgur.com/T00IjV2.jpeg)
![](https://i.imgur.com/8t5GHji.jpeg)
###### Divisione con metodo di Ruffini
![](https://i.imgur.com/tIFgPRa.jpeg)
![](https://i.imgur.com/qoUINso.jpeg)
##### Sistemi lineari
###### Risoluzione per sostituzione

###### Risoluzione per confronto

###### Risoluzione per riduzione

###### Risoluzione con metodo di Cramer
?
##### Geometria analitica
###### Determinare l'equazione della retta
\1) 
==m = 1/2,   P = (1;3),   q = ?==
Innanzitutto abbiamo il coefficiente angolare, che lo si sostituisce: 
$$y = \dfrac{1}{2} x + q$$
Poi, dato che ci vengono date le coordinate di un punto P (1;3) per cui la retta passa, basta sostituirle a $x$ e $y$ dell'equazione per trovare q:
$$3 = \dfrac{1}{2} * 1 + q \;\;\rightarrow\;\;q = \dfrac{5}{2}$$
Quindi l'equazione finale sarà:
$$y = \dfrac{1}{2} x + \dfrac{5}{2}$$
(TIP: è necessario prima sostituire la m, cosicché sostituendo poi x e y del punto dato, solo la q rimanga isolata).
(TIP: ovviamente, se venivano dati P e q, si faceva il percorso identico ma al fine di calcolare la m).

\2) 
P1 = (1;1),  P2 = (2;3)
In esercizi del genere, è necessario l'uso di un sistema per determinare l'equazione della retta (siccome sostituendo x e y dei punti all'equazione generale della retta si hanno sempre 2 incognite: m e q):
$$
\left\{\,\begin{aligned}
& 1 = m * 1 + q \\
& 3 = m * 2 + q 
\end{aligned}\right.
\;\;\rightarrow\;\,
\left\{\,\begin{aligned}
& m + q = 1 \\
& 2m + q = 3 
\end{aligned}\right.
\;\;\rightarrow\;\,
\left\{\,\begin{aligned}
& q = 1 - m \\
& 2m + (1 - m) = 3
\end{aligned}\right.
\;\;\rightarrow\;\,
\left\{\,\begin{aligned}
& q = 1 - (2) = - 1 \\
& m = 2
\end{aligned}\right.
$$
(TIP: è possibile anche prima calcolare la m con la formula: $m = \dfrac{y_{b} - y_{a}}{x_{b} - x_{a}}$ e poi sostituire di x e y con uno dei 1 punti e calcolare la q isolandola).
###### Trovare il coefficiente angolare di una retta
\3) 
==Formula m==: $\dfrac{y_{b} - y_{a}}{x_{b} - x_{a}}$
$r$ passa per A(3,-4) e B(-2,-4)
$$m_{r} = \dfrac{-4 - (-4)}{3 - (-2)} = \dfrac{0}{5} = 0$$
Quindi: se le y dei 2 punti per cui passa una retta sono uguali, la retta avrà m = 0.
$s$ passa per C(0,2) e D(0,-1)
$$m_{s} = \dfrac{2 - (-1)}{0 - 0} = \dfrac{3}{0} = non\;esiste$$
Quindi: se le x dei 2 punti per cui passa una retta sono uguali, la retta sarà verticale e non avrà m.
###### Determinare parallelismi e perpendicolarità
\4) 
$$\begin{aligned}
& 2x+3y-2=0 \;\rightarrow\; y=-\frac{2}{3}x+\frac{2}{3} \\
& 3x-y+6=0 \;\rightarrow\; y=3x+6 \\
& -6x+2y=0 \;\rightarrow\; y=3x \\
& 3x-2y-8=0 \;\rightarrow\; y=\frac{3}{2}x-4
\end{aligned}$$
Rette parallele: $m_{1} = m_{2} \;\;\rightarrow\;\;$ rette 2 e 3
Rette perpendicolari: $m_{1} = -\dfrac{1}{m_{2}} \;\;\rightarrow\;\;$ rette 1 e 4
###### Intersezioni tra 2 rette
\5)
${} r_{1} \;\rightarrow\; y=x-1$
$r_{2} \;\rightarrow\; y=-\frac{1}{2}x+2$
Si fa sempre con un sistema e questa volta lo risolviamo per confronto:
$$
\left\{\,\begin{aligned}
& y = x - 1 \\
& y = -\frac{1}{2}x + 2 
\end{aligned}\right.
\;\;\rightarrow\;\,
x - 1 = -\frac{1}{2} + 2
\;\;\rightarrow\;\,
3x = 6 
\;\;\rightarrow\;\,
x = 2
$$
Sostituendo la x alle equazioni delle 2 rette si ottiene 1 (in entrambe il risultato è uguale perché altrimenti non sarebbe un'intersezione); quindi il punto di intersezione ha coordinate: x = 2 e y = 1 --> P(2,1)
(TIP: quando le m delle 2 equazioni sono uguali (rette parallele), si ottiene un sistema con solo i termini noti; nel caso in cui i termini noti siano uguali, le rette sono sovrapposte e il punto di intersezione è indeterminato; altrimenti le rette sono solo parallele ed il punto di intersezione di 2 rette che danno vita ad un sistema impossibile non esiste).
###### Distanza di un punto da una retta
\6) 
Formula distanza: $d = \dfrac{|y_{0}-mx_{0}-q|}{\sqrt{1+m^{2}}}$
$$d = \dfrac{|2-1*(-1)-2|}{\sqrt{1+1^{2}}} = \frac{2}{\sqrt{2}} = \sqrt{2}$$
###### Determinare l'equazione di un fascio di rette proprio dato il centro
\7)
P (centro) = (2,0) 
$$y - y_{0} = m(x - x_{0}) \;\;\rightarrow\;\; y = m(x - 2)$$
###### Varie richieste con fasci generati da 2 rette
8)
https://youtu.be/9vwFhe4Sdpg?list=PLF304133989EE90EA
###### PARTE 2
1)
Sostituire a equazione generale di retta x e y dei 2 punti (2 volte) e mettere le 2 risultanti a sistema (a 2 incognite: m e q) e risolvere con confronto.
![](https://i.imgur.com/tpC8i0d.png)
2)
Sostituire a x e y dell'equazione i valori di x e y del punto
![](https://i.imgur.com/29GTqlI.png)
3)
(come il 2) ma leggermente + complesso in quanto si deve risolvere per h)
h = -1
4)
formula m
![](https://i.imgur.com/lC5rZzj.png)
5)
formula m + confronto
parallele
formula distanza
d = ${} \frac{7\sqrt{5}}{10}$
6)
trovare le generatrici e stabilire se proprio (si)
a) porre a sistema le generatrici e fare confronto, si trova il punto comune (intersezione / centro)
b) mettere a sistema 2 eq di rette sostituendovi in una le coord del punto B e nell'altra quelle del centro
c) trovare opposto e reciproco di m della retta data, trovare retta dati quella m ed il centro
d) sostituire a formula distanza (qualcosa???)
![](https://i.imgur.com/MYGIzFi.png)

##### Radicali
###### CE
\1) 
$$x - 2 \ge 0 \;\rightarrow\; x \ge 2$$
2)
$$\begin{aligned} 
& x - 1 \ge 0 \;\rightarrow\; x \ge 1 \\
& x + 2 > 0 \;\rightarrow\; x > -2
\end{aligned}$$
(studio del segno con zeri)
CE  = $\;x < -2 \;\;U\;\; x \ge 1$
3)
(Stessa cosa di 2), però soluzione non esiste per nessuna x)
CE = $\;\not\exists x \in \mathbb{R}$
###### Proprietà
\1)
$\sqrt{5} = \sqrt[4]{5^{2}} \not= \sqrt[4]{125}$
$\sqrt{6} = \sqrt[6]{6^{3}} = \sqrt[6]{216}$
2)
$\sqrt{3}$
3)
TODO
https://youtu.be/A10pCDp2tTU?t=347
4) ![](https://i.imgur.com/Pl4WTI4.png)
5) ![](https://i.imgur.com/6sHKuFV.png)