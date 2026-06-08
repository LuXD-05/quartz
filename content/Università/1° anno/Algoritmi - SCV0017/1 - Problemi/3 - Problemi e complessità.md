# Lezione 3

### Problemi

Ad ogni problema $\sqcap$ è associabile una funzione:

$$f_{\sqcap} : D_{\sqcap} \rightarrow S_{\sqcap}$$

Dove:

- ${} D_{\sqcap} \rightarrow$ insieme delle istanze di $\sqcap$,
- $S_{\sqcap} \rightarrow$ insieme delle soluzioni di $\sqcap$, ovvero: $f_{\sqcap}(D_{\sqcap})$.

> [!example] Primalità
> Il problema di "***primalità***" (lo chiamiamo $P$ in questo caso) consiste nell'indicare se un numero è primo o meno:
> $$f_{P} : n \rightarrow \{0,1\}$$
> Infatti: $f_{P}(11) = 1$ e $f_{P}(121) = 0$.

#### Algoritmi

Stesso discorso vale anche per gli algoritmi $\mathcal{A}$, ai quali si associano funzioni (***parziali***):

$$\phi_{\mathcal{A}} : I_{\mathcal{A}} \rightarrow O_{\mathcal{A}}\; \cup \;\{\perp\}$$

Dove:

- ${} \phi_{\mathcal{A}} \rightarrow {}$ funzione associata all'algoritmo,
- $I_{\mathcal{A}} \rightarrow$ insieme degli **input** di $\mathcal{A}$,
- ${} O_{\mathcal{A}} \rightarrow$ insieme degli **output** di $\mathcal{A}$,
- $\{\perp\}$ indica l'insieme di tutti i risultati **non adatti o definiti** alla funzione (tipo quando un <u>algoritmo che dovrebbe concludere va in loop</u>); perciò sono ***parziali***, dato che esistono casi in cui la funzione non termina o non restituisce un valore idoneo.

> [!info] Correttezza
> $\mathcal{A}$ è un algoritmo che risolve $\sqcap$ (quindi è ***corretto***) se e solo se:
> - $I_{\mathcal{A}} = D_{\sqcap}$,
> - $O_{\mathcal{A}} = S_{\sqcap}$,
> - $\forall x \;\rightarrow\; f_{\sqcap}(x) = \phi_{\mathcal{A}}(x)$.
>   Ovvero quando ogni <u>soluzione del problema</u> è = al relativo <u>output dell'algoritmo</u>.

###### Risorse

L'**efficienza** di un algoritmo si basa sulla <u>quantità di risorse usate per risolvere un problema</u>; in particolare:

- **Tempo**: <u>numero</u> totale di <u>istruzioni eseguite</u>,
- **Spazio**: <u>memoria occupata</u> (*programma + dati*).

###### Peso

Per ogni algoritmo $\mathcal{A}$, introduciamo una funzione $W$ (***weight***) che esprime la "***dimensione***" o "***peso***" degli input, il che è espresso tramite un <u>numero intero</u>:

$$W_{\mathcal{A}} : I_{\mathcal{A}} \rightarrow \mathbb{N}$$

Per esempio, se $I_{\mathcal{A}}$ è un <u>array di interi</u>, $W_{\mathcal{A}}$ potrebbe esserne la <u>lunghezza</u>.

> [!warning] Attenzione
> Il **peso discrimina** la **complessità** <u>degli algoritmi</u> (fare una ricerca su 3 interi è sostanzialmente meno complesso rispetto a farla su 300).
> Tuttavia un algoritmo può comportarsi in modo <u>sensibilmente diverso</u> anche per <u>istanze di un problema</u> con **ugual peso** (<u>trovare il minimo</u> in un array in ordine **crescente** è molto <u>meno complesso</u> che farlo in uno ordinato in ordine **decrescente**).

##### Complessità

Si può esprimere la **complessità** di un algoritmo $\mathcal{A}$ tramite la seguente funzione:

$$T_{\mathcal{A}} : \mathbb{N} \rightarrow \mathbb{N}$$

che indica per ogni valore intero $n$ la quantità di risorse impiegata dall'algoritmo per elaborare dati di dimensione $n$.

###### Complessità caso peggiore

La complessità caso **peggiore** di un algoritmo è una funzione (${} T^{w}_{\mathcal{A}}(n) {}$, con $w =$ ***worst***) che implementa l'algoritmo considerandone (per ogni dimensione) le istanze più ***sfavorevoli***.

###### Complessità caso migliore

La complessità caso **migliore** di un algoritmo è una funzione (${} T^{b}_{\mathcal{A}}(n) {}$, con $b =$ ***best***) che implementa l'algoritmo considerandone (per ogni dimensione) le istanze più ***favorevoli***.

###### Complessità in media

La complessità **in media** di un algoritmo è una funzione (${} T^{a}_{\mathcal{A}}(n) {}$, con $a =$ ***average***) che implementa l'algoritmo considerandone il <u>comportamento medio</u>, calcolato con la **media** dei comportamenti delle sue istanze aventi <u>ugual dimensione</u>. Questo:

$$T^{a}_{\mathcal{A}}(n) = \sum\limits_{|i|=n} P_{i}C_{i}$$

Dove:

- ${} P_{i}$ è la **probabilità** dell'istanza $i$,
- ${} C_{i}$ è il **costo** (<u>quantità di risorse</u> impiegata) per elaborare l'istanza $i$.

> [!example] Probabilità
> Consideriamo i costi $C_{i}$ delle istanze <u>distinti</u>: per ogni costo $k$, la probabilità $P_{i}$ delle istanze o input $I$ con $C_{i} = k$ è il n° di esse ($\#I_{k}$) sul totale ($\#I_{\mathcal{A}}$).
> $$T^{a}_{\mathcal{A}}(n) = \sum\limits_{k} k \; \frac{\#I_{k}}{\#I_{\mathcal{A}}}$$
> In caso tutte le istanze/input $I$ siano ***equiprobabili*** rispetto ai costi (<u>ogni istanza ha un costo distinto</u>) si ha:
> $$T^{a}_{\mathcal{A}}(n) = \frac{1}{\#I_{\mathcal{A}}} \sum\limits_{k} k \; \#I_{k} $$

---

Prossima lezione: [[4 - Notazioni asintotiche]]

