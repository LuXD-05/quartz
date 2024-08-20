# Todo

### Mate

#### Lista

##### Pre

- [ ] CE (in generale, tipo denom != 0 oppure | x | --> per ogni x in R)

##### Monomi e polinomi

###### Divisione tra polinomi

- [ ] Divisione euclidea (con resto)
- [ ] Divisione con metodo di Ruffini (+ considerazioni sul teorema del resto)

##### Sistemi

###### Sistemi lineari

- [ ] Sistemi lineari

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

##### Geometria analitica

###### Piano cartesiano

###### Vettori

###### Fasci di rette

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
