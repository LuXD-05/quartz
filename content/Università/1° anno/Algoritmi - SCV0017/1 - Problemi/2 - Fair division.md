# Lezione 2

### Fair division

I problemi di ***fair division*** prevedono la spartizione di un insieme di oggetti ($A$), aventi un certo valore complessivo ($V$), in parti di equo valore tra $n$ individui. L'algoritmo deve rispettare le seguenti condizioni:

- <u>Non è possibile formare coalizioni</u> a danni di altri (più individui si accordano preventivamente per ottenere una parte maggiore),
- Se $x$ riceve $A_{1}$ il cui valore è < $\frac{V}{n}$, la <u>responsabilità è solo sua</u> (nessuno si può lamentare per ciò che egli stesso sceglie),
- <u>Nessuno deve poter invidiare</u> qualcun altro se $A_{n}$ ha valore $\geq \frac{V}{n}$.

###### 2 individui

Con <u>2 individui</u> è semplice perché:

1) $x_{1}$ divide $A$ in 2 partizioni per lui di equo valore: $A_{1} \cup A_{2}$,
2) $x_{2}$ sceglie una delle 2 parti e $x_{1}$ riceve l'altra.

$x_{1}$ non si può lamentare perché ha diviso lui le parti e così nemmeno $x_2$ perché è stato lui stesso a sceglierne una.

###### 3 individui

1) $x_{1}$ crea le partizioni di $A = A_{1} \cup A_{2} \cup A_{3}$,
2) $x_{2}$ indica la partizione $A_{i}$ che per lui ha <u>meno valore</u> ($V_{i} \leq \frac{A}{3}$),
3) Se per $x_{3}$, $A_{i}$ vale meno delle altre, allora essa viene assegnata ad $x_{1}$ e il resto si divide tra $x_{2}$ e $x_{3}$ come fatto [[#2 individui|qui]]. Se invece per $x_{3}$, $A_{i}$ ha più valore delle altre partizioni, lui si tiene $A_{i}$ e gli altri si dividono il resto sempre come fatto [[#2 individui|qui]].

---

Prossima lezione: [[3 - Problemi e complessità]]

