---
public: true
tags:
  - "#matematica/integrali"
---
# Steps
0) Sono date 2 funzioni ed è richiesto di trovare quanto vale l'area della loro intersezione. 
1) Calcolare (per parabole) le coordinate del vertice delle funzioni non note "a occhio" (una nota ad occhio è $y = x^2$, al contrario di $y = -x^{2}+2$) con: $x_{v}= -\dfrac{b}{2a}$ e $y_v$ si trova sostituendo il valore di $x_v$ alle $x$ della funzione originale.
2) Trovare (per le funzioni che intersecano l'asse x e/o y) i punti di intersezione con tali assi (fatto per il meme, in realtà non serve).
3) Trovare i punti di intersezione tra le 2 funzioni ponendole in un sistema e risolvere facendo poi $f(x) = g(x)$. Le coordinate x dei 2 punti saranno trovate (ovviamente) quando si trova $x = \ldots$ , ma per trovare le coordinate y sarà necessario sostituire i valori di queste 2 x alla 1a funzione dell'uguaglianza iniziale ($f(x)$).
4) (Siccome si ha tutto il necessario) fare il grafico delle funzioni.
5) Calcolare l'area facendo l'integrale tra i 2 punti di intersezione appena trovati e la differenza: ($f(x)$ con margine dell'area + in alto) - ($f(x)$ con margine dell'area + in basso).
# Esempi
### Area tra 2 f(x) n° 1
Calcolare l'area delle 2 funzioni date.
$$
y = x^{2} \;\;\lvert\;\; y = -x^{2}+2 \;\;\lvert\;\; A = ?
$$
Qui abbiamo come funzione nota "ad occhio" $y = x^{2}$, in quanto è risaputo che ha vertice e intersezione con l'asse x in (0,0); perciò si procede col vertice della seconda.
$$
x_{v} = -\dfrac{b}{2a} = -\dfrac{0}{2*(-1)} = 0 \;\;\;\;\; \lvert \;\;\;\;\; y_{v}= 0 + 2 = 2
$$
Si vanno a trovare le intersezioni con gli assi:
$$
int. y
\left\{\begin{aligned} 
x &= 0 \\
y &= 2
\end{aligned}\right.
\;\;\;\;\;\;\; \lvert \;\;\;\;\;\;
int. x
\left\{\begin{aligned} 
y &= 0 \\
x &= -x^{2} + 2 = 0
\end{aligned}\right.
\;\; \rightarrow \;\;
\left\{\begin{aligned} 
x^{2} = 2
\end{aligned}\right.
\;\; \rightarrow \;\;
\left\{\begin{aligned} 
x = \pm\sqrt{2}
\end{aligned}\right.
$$
Ora si calcolano le intersezioni con il sistema:
$$
\left\{\begin{aligned} 
y &= x^{2} \\
y &= -x^{2} + 2
\end{aligned}\right.
\;\; \rightarrow \;\;
\left\{\begin{aligned} 
x^{2} = -x^{2} + 2 \\
\end{aligned}\right.
\;\; \rightarrow \;\;
\left\{\begin{aligned} 
2x^{2} = 2 \\
\end{aligned}\right.
\;\; \rightarrow \;\;
\left\{\begin{aligned} 
x^{2} = 1 \\
\end{aligned}\right.
\;\; \rightarrow \;\;
\left\{\begin{aligned} 
x = \pm 1 \\
\end{aligned}\right.
\;\; \rightarrow \;\;
\left\{\begin{aligned} 
y &= \pm 1^{2} = 1 \\
x &= \pm 1
\end{aligned}\right.
$$
Il grafico:
```tikz
\begin{document} 
\begin{tikzpicture}[domain=-4:4] 
\draw[very thin,color=gray] (-4,-3) grid (4,4); 
\draw[->] (-3.2,0) -- (3.2,0) node[right] {$x$}; 
\draw[->] (0,-2.2) -- (0,3.2) node[above] {$y$};
\clip (-3,-2) rectangle (3,3);
\draw[thick,color=red,domain=-4:4,smooth] plot (\x,{(\x)^2}) node[right] {$f(x) = x^2$}; 
\draw[thick,color=blue,domain=-4:4,smooth] plot (\x,{-(\x)^2+2}) node[right] {$f(x) = -x^{2} + 2$}; 
\end{tikzpicture} 
\end{document}
```
Le intersezioni trovate sono quindi: (1;-1) e (1;1). Si procede infine con il calcolo dell'area:
$$
\int^{1}_{-1} [(-x^{2}+2)-(x^{2})] \; dx
\;\; = \;\;
\left[-\dfrac{x^{3}}{3} + 2x - \dfrac{x^{3}}{3}\right]^{1}_{-1}
\; = \;\;
\left[-\dfrac{2x^{3}}{3} + 2x\right]^{1}_{-1}
\; = \;\;
\left(-\dfrac{2}{3} + 2\right)-\left(\dfrac{2}{3} - 2\right)
\;\; = \;\;
-\dfrac{4}{3} + 4 \;\; = \;\; -\dfrac{8}{3}
$$