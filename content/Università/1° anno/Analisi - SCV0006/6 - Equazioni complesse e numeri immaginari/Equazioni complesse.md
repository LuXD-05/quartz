# Lezione 

### Numeri immaginari

C = insieme complessi

i = unità immaginaria

> [!important] Quanto vale $i$?
> Supponiamo di scrivere la $i$ come numero complesso a sé: $i = 0 + i \cdot 1$:
> - ${} i = {}$
> - $i^{2} = (0 + i \cdot 1)^{2} \cdot (0 + i \cdot 1) = -1$
> - $i^{3} =$
> - $i^{4} = 1$

##### Numeri complessi

Un **numero complesso** $z$ è una coppia $(x,y)$ in cui $x$ è la parte reale e $y$ è la parte immaginaria; e corrisponde a: $z = x + iy$ (con eventuali coefficienti): nota che il suo valore corrisponde alla somma tra la sua parte reale e quella immaginaria (non è proprio una coppia di elementi come se fossero coordinate x e y!).

Notazione: $Re(z)$ corrisponde a $x$ (la parte reale di $z$), mentre $Im(z)$ è $y$ (la parte immaginaria).

###### Operazioni

Le operazioni di addizione e moltiplicazione sono possibili anche tra numeri complessi; quindi, dati 2 numeri complessi $z_{1} = x_{1} + iy_{1}$ e $z_{2} = x_{2} + iy_{2}$:

**Addizione**: $z_{1} + z_{2} = (x_{1} + x_{2}) + i(y_{1} + y_{2})$

**Moltiplicazione**: $z_{1} \cdot z_{2} = (x_{1}x_{2} - y_{1}y_{2}) + i(x_{1}y_{2} + x_{2}y_{1})$

**Divisione** (vedi prima modulo e complesso coniugato):

$$\frac{z_{1}}{z_{2}} = \frac{x_{1} + iy_{1}}{x_{2} + iy_{2}} = \frac{(x_{1} + iy_{1}) \cdot (x_{2} - iy_{2})}{(x_{2} + iy_{2}) \cdot (x_{2} - iy_{2})} = \frac{x_{1}x_{2} - ix_{1}y_{2} + ix_{2}y_{1} - i^{2}y_{1}y_{2}}{x^{2} + y^{2}} = \color{yellow}{\frac{x_{1}x_{2} + y_{1}y_{2}}{x^{2} + y^{2}} + i\frac{y_{1}x_{2}-x_{1}y_{2}}{x^{2} + y^{2}}} \in \mathbb{C}$$

##### Altro ???

###### Modulo

Si indica con $|z|$ quanto segue: $|z| = \sqrt{x^{2} + y^{2}}$

###### Complesso coniugato

Il complesso coniugato di un numero complesso $z$ è $\overline{z} = x - iy$; ed i 2 sono **simmetrici**:

![](https://i.imgur.com/i9K4r8G.png)

Proviamo ora a fare il prodotto di $z$ e del suo complesso coniugato:

$$z \cdot \overline{z} = (x + iy) \cdot (x - iy) = x^{2} - (-1)y^{2} = x^{2} + y^{2}$$

Perciò, dato il modulo $|z|$: $\;\;z \cdot \overline{z} = |z|^{2}$

##### Forma trigonometrica

...

---

Prossima lezione: [[]]

