# Lezione 34

### Registro a scorrimento

Il **registro a scorrimento** è composto da $n \geq 1$ **[[30 - Flip-Flop e sincronizzazione sul fronte#Flip-Flop|flip-flop D]]** (sincronizzati sul fronte) collegati ***in cascata***; e, ad ogni ciclo di clock, fa <u>scorrere a destra di 1 bit la parola memorizzata</u> e <u>aggiunge a sinistra</u> (nel 1° flip-flop) il <u>bit più a destra del segnale</u> presente <u>nel</u> suo <u>ingresso seriale</u>.

**Ingressi**: $S$ (seriale di $n$ bit) + $CK$ (clock)

**Uscite**: $n$ ($U_{1}, \ldots U_{n}$)

> [!error] Attenzione
> Se si usassero dei bistabili sincronizzati **[[29 - Clock e sincronizzazione sul livello#Sincronizzazione sul livello|sul livello]]**, si rischia **trasparenza** e di conseguenza il malfunzionamento del circuito (<u>un bit potrebbe propagarsi attraverso l'intera catena di bistabili</u>).

##### Struttura

La seguente è la struttura di un registro a scorrimento a **4 bit** (*DX*):

![](https://i.imgur.com/xB9LkQu.png)

Ed è così simboleggiato:

![](https://i.imgur.com/UZ6AGnn.png)

###### Diagramma temporale

![](https://i.imgur.com/YMDuNk3.png)

#### Varianti

Ci sono anche altre varianti di registri a scorrimento:

- **Registro a scorrimento DX o SX**,
- **Registro a scorrimento DX e SX** (dotato di un comando di scelta del verso di scorrimento),
- **Registro a scorrimento universale**, ovvero dotato di funzioni $CLR$, $PR$ e di scelta del verso di scorrimento),
- **Registro universale** (riunisce le funzioni dei registri paralleli e a scorrimento universali).

# Esercizi

# Soluzioni

---

Prossima lezione: [[35 - Register File]]

