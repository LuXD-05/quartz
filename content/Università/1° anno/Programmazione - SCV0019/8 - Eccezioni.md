# Lezione 8

### Eccezioni

Durante l'esecuzione si possono verica anomalie che non consentono alla JVM di proseguire la normale esecuzione, tali sono segnalate con degli oggetti detti ***eccezioni***.

###### Gerarchia

![](https://i.imgur.com/SNQtgwQ.png)

##### Gestione

Per gestire le eccezioni esiste uno specifico blocco, ovvero il `try-catch-finally`:

```java
try {
	//...
} catch (Exception e1) {
	//...
} catch (...) {
	//...
} finally {
	//...
}
```

In pratica:

- Nella `try` ci deve stare il codice potenzialmente soggetto alla generazione di eccezioni,
- Nelle varie `catch` deve esserci del codice preposto a gestire il tipo di eccezione specificata nel caso essa si verifichi,
- Nella `finally` invece c'è del codice che viene eseguito <u>in ogni caso</u>, che un eccezione venga lanciata o meno.

###### Generazione di eccezioni

Si possono "generare" eccezioni personalizzate o standard con la keyword `throw new Exception(...)`.

##### Tipi di exception

Esistono 2 tipi di eccezioni: quelle [[#Eccezioni controllate|controllate]] e quelle [[#Eccezioni non controllate|non controllate]]:

![](https://i.imgur.com/yJojXet.png)

Si differenziano principalmente per come sono trattate dal compilatore.

###### Eccezioni controllate

Le **eccezioni controllate** (*checked*) sono tutte le istanze di `Exception` che <u>non sono istanze di</u> `RuntimeException`.

Queste si dicono così perché è necessario gestirle, questo in 2 modi:

- Con un blocco `try-catch` per il codice suscettibile ad eccezioni,
- Delegandole al chiamante dichiarandole con `throws`:

  ```java

  public static void main() throws FileNotFoundException {

      Scanner scanner = new Scanner(new File("file.txt")); 

  }

  ```

###### Eccezioni non controllate

Le **eccezioni non controllate** (*unchecked*) sono tutte le istanze di `RuntimeException`. Queste sono generalmente legate ad errori di programmazione e normalmente non dovrebbero venire generate (esempio: `string.length()` quando `String string = null`, genera `NullPointerException`).

##### Lista

![](https://i.imgur.com/yFTU2pt.png)

![](https://i.imgur.com/3OWVvw2.png)

![](https://i.imgur.com/a8hYEC6.png)

# Esercizi

# Soluzioni

---

Prossima lezione: [[9 - File e stream]]

