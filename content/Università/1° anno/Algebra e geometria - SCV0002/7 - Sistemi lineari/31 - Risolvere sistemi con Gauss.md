# Lezione 31

### Risolvere sistemi con il MEG

Abbiamo stabilito che un qualsiasi sistema di equazioni lineari può essere rappresentato in forma matriciale: $B = A \cdot X$. Si può usare il [[26 - Metodo di riduzione di Gauss#Eliminazione gaussiana|MEG]] per risolvere tali sistemi.

##### Come funziona

Si costruisce la matrice completa $(A|B)$ e la si **riduce a scala**, ottenendo $(A'|B')$. 

Il sistema $B = A \cdot X$ ha soluzione se e solo se anche ${} B' = A' \cdot X$ ce l'ha; e le 2 soluzioni coincidono.

Quindi bisogna avere un'insieme di soluzioni $(c_{1}, \ldots c_{n})$ tale che:

$$B = A \cdot \begin{bmatrix} c_{1} \\ \vdots \\ c_{n} \end{bmatrix} \,\;\;=\;\;\; B' = A' \cdot \begin{bmatrix} c_{1} \\ \vdots \\ c_{n} \end{bmatrix}$$

> [!error] Attenzione
> Se il rank della matrice a scala ottenuta con la riduzione di Gauss è diverso dal rank della matrice a scala <u>completa</u> sempre ottenuta con Gauss, il sistema non ha soluzioni.

# Esercizi

###### 1) Risoluzione sistemi con il MEG

Risolvere il seguente sistema di equazioni lineari:

$$
\left\{\begin{aligned}
& 2x + y + z = 2 \\
& x + y = 1 \\
& x + y + z = 2
\end{aligned}\right.
$$

###### 2) Risoluzione sistemi con il MEG

Risolvere il seguente sistema di equazioni lineari:

$$
\left\{\begin{aligned}
& 2x + 2y = 0 \\
& x + y + z = 1 \\
& 4x + 4y + 2z = 3
\end{aligned}\right.
$$

###### 3) Risoluzione sistemi con il MEG

Risolvere il seguente sistema di equazioni lineari:

$$
\left\{\begin{aligned}
& x + z + h = 1 \\
& 2x + y + h = 0 \\
& y + z = 1
\end{aligned}\right.
$$

###### 4) Risoluzione sistemi con il MEG

Risolvere il seguente sistema di equazioni lineari:

$$
\left\{\begin{aligned}
& x + y + 2z - h = 1 \\
& 2y - z + h = 0
\end{aligned}\right.
$$

# Soluzioni

###### 1)

Riscriviamo il sistema in forma matriciale (completa):

$$
\left\{\begin{aligned}
& 2x + y + z = 2 \\
& x + y = 1 \\
& x + y + z = 2
\end{aligned}\right.
\;\;\rightarrow\;\; 
(A|B) = \begin{bmatrix} 2 & 1 & 1 \;\;|\;\; 2 \\ 1 & 1 & 0 \;\;|\;\; 1 \\ 1 & 1 & 1 \;\;|\;\; 2 \end{bmatrix}
\;\; = \;\;
\begin{bmatrix} 2 & 1 & 1 & 2 \\ 1 & 1 & 0 & 1 \\ 1 & 1 & 1 & 2 \end{bmatrix}
$$

Ora riduciamo la matrice a scala con Gauss:

$$
\begin{bmatrix} {\color{red}{2}} & 1 & 1 & 2 \\ {\color{orange}{1}} & 1 & 0 & 1 \\ {\color{orange}{1}} & 1 & 1 & 2 \end{bmatrix} \rightarrow \begin{aligned} \\ (-\tfrac{1}{2}) \cdot R_{1} \\ (-\tfrac{1}{2}) \cdot R_{1} \end{aligned} \rightarrow \begin{bmatrix} 2 & 1 & 1 & 2 \\ 0 & {\color{red}{\frac{1}{2}}} & -\frac{1}{2} & 0 \\ 0 & {\color{orange}{\frac{1}{2}}} & \frac{1}{2} & 1 \end{bmatrix} \rightarrow \begin{aligned} \\ (-1) \cdot R_{2} \\ (-1) \cdot R_{2} \end{aligned} \rightarrow \begin{bmatrix} {\color{aqua}{2}} & {\color{aqua}{1}} & {\color{aqua}{1}} & {\color{aqua}{2}} \\ 0 & {\color{aqua}{\frac{1}{2}}} & {\color{aqua}{-\frac{1}{2}}} & {\color{aqua}{0}} \\ 0 & 0 & {\color{aqua}{1}} & {\color{aqua}{1}} \end{bmatrix}
$$

Verifichiamo che i rank corrispondano (tra la matrice originale e quella a scala):

$$rank(A) = rank(A') = 3 \;\;\;\land\;\;\; rank(A|B) = rank(A'|B') = 3$$

Dato che $rank = rank(A) = rank(A') = n$ (ovvero il n° incognite in $X$), il teorema di Rouché-Capelli ci dice che il sistema è compatibile ed ammette 1 sola soluzione.

Si può quindi procedere risolvendo $B' = A' \cdot X$ (come si potrebbe anche risolvere l'originale):

$$
\begin{bmatrix} 2 & 1 & \;\; 1 \,\;\;\;|\;\; 2 \\ 0 & \frac{1}{2} & -\frac{1}{2} \;\;|\;\; 0 \\ 0 & 0 & \;\; 1 \,\;\;\;|\;\; 1 \end{bmatrix} \;\rightarrow\; \left\{\begin{aligned} & 2x + y + z = 2 \\ & \tfrac{1}{2}y - \tfrac{1}{2}z = 0 \\ & z = 1 \end{aligned}\right. \rightarrow \left\{\begin{aligned} & 2x + y = 1 \\ & \tfrac{1}{2}y = \tfrac{1}{2} \\ & \end{aligned}\right. \rightarrow \left\{\begin{aligned} & x = 0 \\ & y = 1 \\ & z = 1 \end{aligned}\right.
$$

Infine, controlliamo che $(0,1,1)$ sia una soluzione sostituendo questi valori alle incognite dell'equazione che non abbiamo risolto:

$$
\left\{\begin{aligned}
& 2x + y + z = 2 \\
& x + y = 1 \\
& x + y + z = 2
\end{aligned}\right.
\rightarrow
\left\{\begin{aligned}
& 0 + 1 + 1 = 2 \\
& 0 + 1 = 1 \\
& 0 + 1 + 1 = 2
\end{aligned}\right.
$$

Quindi il sistema è risolto e la soluzione è: $x = 0, y = 1, z = 1$.

###### 2)

###### 3)

###### 4)

---

Prossima lezione: [[32 - Metodo di Cramer]]

