---
public: true
edited_seconds: 680
modified_at: 21/05/2024 17:19:54
---
### Cos'è?
::
Secondo la stessa logica usata col metodo dei rettangoli, vi è anche la possibilità di calcolare il volume di solidi di rotazione che ruotano attorno all'asse x di un grafico.
![](https://i.imgur.com/DszyUiU.png)
Il volume di tali solidi si ottiene con la seguente formula:
$$V \;=\; \lim_{N\,\to\,\infty} \; \sum_{i\,=\,1}^{N} \; S_{c_{i}} * \Delta x \;\;=\; \Big(\int^{b}_{a} S(x) \; dx\Big) \;\;\;\;\;\rightarrow\;\;\;\;\; V \;=\; \pi * \int^{b}_{a}[f(x)]^{2} \; dx$$
###### Esempio
Calcolo dell'area di un cilindro ottenuto facendo ruotare attorno all'asse x la funzione: $y = r$ nell'intervallo compreso tra \[0; h\].
$\displaystyle V = \pi * \int^{h}_{0} r^{2} \; dx = \pi \biggr{[} r^{2}x \biggr{]}^{h}_{0} = \pi * (r^{2} * h - 0) = \pi r^{2} h$
<!--SR:!2024-05-25,4,200-->

---

Vedi poi: [[15 Teorema della media]]