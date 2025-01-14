# Lezione 9

### Stream

Per leggere e scrivere dati da/verso una fonte, i programmi aprono degli ***stream*** in lettura/scrittura da/verso una sorgente, da cui leggono/scrivono sequenzialmente dati.

> [!info] Flussi standard
> Disponibili sottoforma di campi statici di `java.lang.System`:
> ![](https://i.imgur.com/QZPaoa8.png)

#### Tipi di stream

Il pacchetto `java.io` è fatto da 2 parti principali:

- `character stream` (flussi di char): dove l'unità di informazione sono `char` Unicode a 16 bit (stream divisi a loro volta in `reader` e `writer`, classi astratte) e le classi che li realizzano si distinguono per il tipo di **sorgente** con cui dialogano.

  ![](https://i.imgur.com/3UuqP0l.png)![](https://i.imgur.com/eGt4DX3.png)

- `byte stream` (flussi di byte): dove l'unità d'informazione è il **byte** (stream a loro volta divisi in `InputStream` e `OutputStream`, classi astratte) e anche qui le loro classi si distinguono per il tipo di sorgente.

  ![](https://i.imgur.com/WF6poGn.png)![](https://i.imgur.com/Z5xJHq5.png)

> [!important] File
> Gli oggetti di tipo `File` permettono la creazione di collegamenti coi file stessi indipendentemente dal sistema dei pathname gerarchici del OS:
> ```java
> 	File file = new File(name);
> 	FileOutputStream fos = new FileOutputStream(file);
> 	//...
> ```

##### Character stream

###### FileReader

`FileReader` è una classe usata per leggere file di char (`character stream`):

**Costruttore**: `public FileReader(String file) throws FileNotFoundException`, lancia l'eccezione se `file` non esiste.

**Metodi**:

![](https://i.imgur.com/xcBm2e7.png)

###### BufferedReader

`BufferedReader` è una "classe filtro" per la lettura file, ovvero una che permette di organizzare le info di uno stream rendendo (in questo caso) più efficiente il processo di lettura.

Metodi:

- `public String readLine()`: legge una linea di resto (considerata conclusa da `\r`, `\n` o `\r\n`). Se legge la fine del file ritorna `null`.

##### Byte stream

###### PrintStream

`PrintStream`, estensione di `OutputStream`, scrive dati come sequenze di byte verso una destinazione. Simile a `ConsoleOutputManager` (ha vari metodi `print()` e `println()`), solo che il costruttore accetta un `OutputStream` come parametro e la destinazione è un file:

```java
File file = new File(name);
FileOutputStream fos = new FileOutputStream(file);
PrintStream ps = new PrintStream(fos);

ps.println("Stampa su file");
```

#### Serializzazione

Molte classi implementano l'interfaccia `Serializable`, con la quale è possibile convertirne gli oggetti in stream di byte per leggerli o scriverli; questo grazie alle classi `ObjectInputStream` e `ObjectOutputStream`.

###### Serializzazione

`ObjectOutputStream` permette di convertire un oggetto in una sequenza di byte per poi inviarlo lungo un `OutputStream` con un processo detto **serializzazione**.

![](https://i.imgur.com/yImgifz.png)

![](https://i.imgur.com/LbuQql4.png)

```java
FileOutputStream fs = new FileOutputStream("today");
ObjectOutputStream os = new ObjectOutputStream(fs);
os.writeObject("Data di oggi:");
os.writeObject(new Data());
os.flush();
```

###### Deserializzazione

`ObjectInputStream` permette di convertire una sequenza di byte da un `InputStream` in un oggetto o dato primitivo con un processo detto **deserializzazione**.

![](https://i.imgur.com/1PUSyPA.png)

![](https://i.imgur.com/vp3D6Vz.png)

```java
FileInputStream fs = new FileInputStream("today");
ObjectInputStream is = new ObjectInputStream(fs);
String today = (String)is.readObject();
Date date = (Date)is.readObject();
```

# Esercizi

# Soluzioni

---

Prossima lezione: [[10 - Algoritmi di sorting e searching]]

