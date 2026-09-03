# Lezione 1

### Streams

Gli ***stream*** sono flussi di dati che le applicazioni usano per leggere dati da una sorgente o per scriverli su una destinazione. Sono definiti nel package `java.io` e si dividono in:

- ***Input streams***: *stream* aperti da applicazioni per <u>leggere sequenzialmente dati</u> da una sorgente,
- ***Output streams***: *stream* aperti da applicazioni per <u>scrivere sequenzialmente dati</u> in una destinazione (in RAM, su disco, remota...).

> [!info] File
> Gli OS usano dei ***path*** per identificare dei *file* all'interno delle *directory* e java dispone della classe `File`, le cui istanze creano collegamenti coi file fisici usando i loro *path*.
> ```java
> File file = new File("path"); // "path" è il percorso del file
> ```

##### Byte streams

I ***byte stream*** si usano per I/O su file binari (+ immagini ed altri tipi di file) dove l'unità di informazione è il **byte** (8 bit) e le classi base per I/O sono `InputStream` e `OutputStream`.

###### FileInputStream

`FileInputStream` permette la <u>lettura</u> di file binari attraverso il metodo `read()` che ritorna il byte letto (sequenzialmente) castato ad int o `-1` se il file è stato letto interamente (ovvero legge il char `EOF`); al termine della lettura, lo stream va chiuso con `close()`.

```java
// In caso di errore dello stream viene lanciata IOException
public static void main() throws IOException {
	int c = 0;
	FileInputStream in = new FileInputStream("file.bin");
	// Finché char letto (in c) != -1 (quindi != EOF)
	while ((c = in.read()) != -1) {
		System.out.print((char)c);
	}
	in.close();
}
```

###### FileOutputStream

`FileOutputStream` permette la <u>scrittura</u> di file binari attraverso il metodo `write(int c)` che scrive 1 byte (alla volta, sequenzialmente) sul file; al termine della lettura, lo stream va chiuso con `close()`.

```java
public static void main() throws IOException {
	List<Integer> ints = new ArrayList<>(...);
	FileOutputStream out = new FileOutputStream("file.bin");
	for (int i : ints) {
		out.write(i);
	}
	out.close();
}
```

##### Character streams

I ***char stream*** si usano per I/O su file di testo che contengono caratteri Unicode (il ***char*** è l'unità di informazione a 16 bit) e le classi base per I/O sono `Reader` e `Writer`.

###### FileReader

`FileReader` permette la <u>lettura</u> di file di testo sempre con il metodo `read([buffer])` e lancia nativamente `FileNotFoundException` in caso il parametro dell'oggetto (path del file da leggere) non esiste; va poi sempre chiuso con `close()`.

```java
// Versione normale --> legge 1 char per volta
public static void main() throws IOException {
	FileReader fr = new FileReader("file.txt");
	int c = 0;
	while ((c = fr.read()) != -1)
		System.out.print((char)c);
	fr.close();
}

// Versione con buffer --> n char letti per volta
public static void main() throws IOException {
	char[] buffer = new char[10]; // n = 10
	FileReader fr = new FileReader("file.txt");
	int n = 0;
	while ((n = fr.read(buffer)) != -1)
		for(int i = 0; i < n; i++) {
			System.out.print(buffer[i]);
	}
	fr.close();
}
```

> [!important] `read()` con buffer
> Di base il metodo `read()` non ha parametri e ritorna un int compreso tra 0 e 65535 o -1 se legge `EOF`; tuttavia è possibile passargli un <u>array di char</u> (`char[]`) detto ***buffer*** come parametro; in questo caso, se il buffer ha dimensione `n`, `read()` leggerà `n` char e li inserirà nelle posizioni del *buffer*, oltre a ritornare il <u>n° di byte letti</u> (eccetto `EOF`, che legge in un ciclo separato per ritornare -1).

###### FileWriter

`FileWriter` permette la <u>scrittura</u> di file di testo (aprendolo o creandolo se non esiste) attraverso il metodo `write(char c)` che scrive 1 char (alla volta, sequenzialmente) sul file; al termine della lettura, lo stream va chiuso con `close()`.

```java
// java 7 version (better version in snippets)
public static void main() {
	FileWriter fw = null;
	try {
		fw = new FileWriter("file.txt");
		fw.write('a');
		//...
	} catch (Exception e) { /* ... */ }
	finally {
		try {
			if(fw != null) {
				fw.flush();
				fw.close();
			}
		} catch (IOException e) { /* ... */ }
	}
}
```

> [!important] `flush`
> `flush()` è un metodo di `FileWriter` che "applica" i char scritti sul file fino a quando non è invocato (`write()` scrive in un buffer, non direttamente nel file). 
> Di norma non si usa in quanto è chiamato all'interno di `close()`, però può essere utile quando si vuole che i dati scritti su un file siano disponibili in esso prima di chiudere lo stream (tipo in app client-server o quando gli stream sono aperti verso oggetti remoti).

###### BufferedReader

`BufferedReader` è una classe che ha come parametro un `Reader` (tipo un `FileReader`) che <u>legge</u> una **linea** (stringa terminata con `\r\n` o l'***EndOfLine*** char in base all'OS) con il metodo `readLine()` e la ritorna senza l'*EndOfLine* char (ritorna `null` se lecce `EOF`).

```java
public static void main() throws IOException {
	// Prof ha deciso di omettere il try-catch
	FileReader fr = new FileReader("file.txt");
	BufferedReader br = new BufferedReader(fr);
	String s;
	while ((s = br.readLine()) != null)
		System.out.println(s);
	br.close();
	fr.close(); // ridondante --> br.close() chiama già fr.close()
}
```

###### PrintWriter

`PrintWriter` è l'analogo del precedente ma per <u>scrivere</u> in un file di testo (ha come parametro un `Writer`) e, come `System.out`, dispone di `print(String s)` e `println(String s)`, che fanno la stessa cosa ma `println` aggiunge un char *EndOfLine* alla fine del testo da scrivere.

```java
public static void main() throws IOException {
	// Prof ha deciso di omettere il try-catch
	FileWriter fw = new FileWriter("file.txt");
	PrintWriter pw = new PrintWriter(fw);
	pw.println("...");
	pw.close();
	fw.close(); // ridondante --> pw.close() chiama già fw.close()
}
```

###### PrintStream

`PrintStream` è una classe particolare che permette di convertire dati in **sequenze di byte**; ha come parametro un `OutputStream` e ha diversi metodi `print` e `println`:

![](https://i.imgur.com/Uj2JxRy.png)

```java
public static void main() {
	File file = new File("file.txt");
	FileOutputStream fos = new FileOutputStream(file);
	PrintStream ps = new PrintStream(fos);
	// file.txt conterrà i seguenti valori convertiti in stringhe
	ps.println("Ciao");
	ps.println(100);
	ps.println(3/4.0);
	ps.println(true && false);
	ps.close();
}
```

---

Prossima lezione: [[]]

