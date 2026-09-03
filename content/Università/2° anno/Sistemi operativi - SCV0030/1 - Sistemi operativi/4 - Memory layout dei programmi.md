# Lezione 4

### Aree di memoria

L'esecuzione di un programma necessita di <u>3 aree di memoria</u> (***memory regions***):

- **Area di testo**: contiene il <u>codice del programma</u> (istruzioni in linguaggio macchina, non modificabile dal programma stesso),
- **Area dati**: contiene le <u>variabili globali</u> e le <u>strutture dati dinamiche</u> (si trovano nell'area ***heap***, a cui puntano le variabili che fanno riferimento a tali strutture),
- **Area di stack**: contiene i ***frame*** (<u>record di attivazione</u>) delle procedure non terminate chiamate (l'indirizzo della cima è salvato nel registro SP); ogni record contiene:
  - Parametri attuali,
  - Variabili locali,
  - ***Return address*** (l'indirizzo della prossima istruzione da eseguire al termine della procedura, ottenuto salvando il PC al momento della chiamata),
  - Un puntatore alla cima del record di attivazione della proceduta <u>chiamante</u>.

> [!info] Nota
> Entrambe le aree **dati** e **di stack** hanno <u>contenuto e dimensioni variabili</u> (il <u>contenuto</u> di entrambe varia con assegnamenti alle variabili) mentre:
> - **Area dati**: la <u>dimensione</u> varia per la presenza delle strutture dati dinamiche.
> - **Area di stack**: la <u>dimensione</u> varia quando vengono chiamate o terminano le procedure.

###### Esempio

Assumendo che gli indirizzi siano a 16 bit (4 cifre esadecimali), `main()` è all'indirizzo $A12E$ ed `f1()` è all'indirizzo $A39F$:

```c
// Variabili globali
int a = 5; 
int b = 6;

int main(void) { 
	int x = 10;         // Variabile locale 
	// (punto 1) 
	int y = f1(x, b);   // Variabile locale 
	// (punto 5) 
	printf("ecco il valore di y: %d\n", y); 
}

int f1(int s, int t) { 
	int u = a + s + t;  // Variabile locale 
	// (punto 2) 
	int v = f2(u);      // Variabile locale 
	// (punto 4) 
	return v; 
}

int f2(int h) { 
	int k = h + 15;     // Variabile locale 
	// (punto 3) 
	return k; 
}
```

Dal punto di vista della memoria:

![](https://i.imgur.com/ieyl0Vg.png)

##### Indirizzi di memoria

Il codice del programma contiene <u>indirizzi di memoria</u> che si riferiscono alle aree: **testo** (istruzioni `jump`), **dati** (variabili globali) e **di stack** (variabili locali e parametri). Questi però sono **indirizzi virtuali** <u>tradotti in linguaggio macchina</u> a *runtime* dalla **MMU** (*Memory Management Unit*) per convertirli in **indirizzi reali**; dato che non si sa quali parti della RAM saranno effettivamente assegnate al programma per l'esecuzione, gli indirizzi virtuali <u>partono da 0</u> per poi venir tradotti in indirizzi reali.

> [!warning] Attenzione
> Se il codice contenesse indirizzi reali non servirebbe la MMU, tuttavia:
> - Non si potrebbero caricare in memoria programmi (diversi o più istanze del medesimo) con ***overlapping*** di memoria (con alcuni indirizzi in comune),
> - I compilatori dovrebbero gestire l'*overlapping* (molto complesso soprattutto su PC),
> - I programmi non sarebbero portabili.

###### Traduzione degli indirizzi

Supponendo che ad ogni programma venga assegnata un'area di memoria **contigua** (non come nei sistemi moderni), un semplice meccanismo di traduzione degli indirizzi da virtuali a reali è l'uso di un ***Relocation Register*** (RR):

![](https://i.imgur.com/0oFN0KS.png)

In pratica se il programma inizia da una locazione di memoria $a$, l'RR assume valore $a$; quindi tutti gli <u>indirizzi a cui il programma stesso accede</u> saranno **sommati** ad $a$ (quindi se accede a 75300 ed il programma parte da 100k si avrà che l'indirizzo reale è 100k + 75300 che va bene affinché stia al di sotto dell'**UBR**).

Così la MMU sarebbe composta solo <u>dal RR e da un sommatore</u>; con anche la protezione della memoria con LBR e UBR si può usare direttamente LBR come RR.

---

Prossima lezione: [[5 - Processi]]

