# Lezione 10

### Char

Nel tempo e con le varie popolazioni, sono stati inventati migliaia di caratteri. 

1) All'inizio sono stati codificati quelli occidentali, con 10 numeri, 26 lettere minuscole e 26 maiuscole + altri segni di uso comune. 
2) I numeri si codificano con certe sequenze di bit, mentre per le lettere o altro una qualsiasi sequenza andava bene.

Il fatto è che la codifica dei caratteri deve essere universale e accettata da tutti, perciò va definita da uno standard.

##### ASCII

L'**ASCII** (*American Standard Code for Information Interchange*) è lo standard più noto ed utilizzato e definisce valori per 128 char, di cui 33 (0-31, 127) non stampabili.

![](https://i.imgur.com/btVEaTT.png)

###### Char di controllo

Per gestire del testo servono anche dei char "di controllo", tipo:

- **CR** (*Carriage Return*) e **LF** (*Line Feed*): per segnalare la fine di una riga (derivano dalle macchine da scrivere, dove <u>CR</u> indica lo spostamento all'inizio della riga del "cursore" mentre <u>LF</u> indica lo spostamento di esso nella riga successiva sottostante),
- **EOT** (*End of text*): che indica la fine di un testo/documento,
- **Del**: che indica la cancellazione di un char precedentemente inserito.

###### ISO 8859/1 (ISO Latin-1)

L'ASCII usa solo 7 degli 8 bit di un byte e non è del tutto completo (mancano lettere accentate).

Soluzione: lo **standard ISO 8859/1** (usato nel web) permette l'uso di tutti gli 8 bit ed è retrocompatibile con l'ASCII (i primi 7 bit corrispondono mentre gli altri sono lettere accentate e altri simboli).

###### Altri alfabeti

Per scrivere caratteri in altri alfabeti sono stati inventati diversi codici a 8 bit per alfabeti non latini, ma questi comunque non bastano.

Sono quindi stati inventati altri standard come l'**UNICODE** e l'**ISO/IEC 10646** che consentono la rappresentazione di qualsiasi carattere grazie al n° variabile di bit usati.

##### Interpretazione delle informazioni

Se in un byte di memoria c'è 01000001, il calcolatore non sa se interpretarlo come intero (65) o char (A); perciò sta ai programmi ricordarsi di che tipo è il contenuto di una variabile, assegnandole un "tipo".

# Esercizi

# Soluzioni

---

Prossima lezione: [[11 - Segnali e informazioni]]

