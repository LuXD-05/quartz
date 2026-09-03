# Lezione 10

### Proxy

Nelle app client-server si vuole separare la logica applicativa dai meccanismi per la comunicazione, i quali vengono gestiti da un componente intermedio detto ***proxy***.

Tale proxy è come un'implementazione locale del server remoto con gli stessi metodi che gestiscono la comunicazione a basso livello e inoltrano le richieste del client al server.

#### Proxy client

Un <u>proxy lato client</u> ha dei metodi specifici che il client chiama, i quali si occupano di inoltrare una richiesta specifica al server:

```java
import java.io.*;
import java.net.*;

public class Proxy implements AutoCloseable {  // interfaccia AutoCloseable --> fornisce close()
    private Socket socket;
    private BufferedReader in;
    private PrintWriter out;

	// Istanzia socket, inputStream e outputStream in ctor
    public Proxy(String host, int port) throws IOException {
        socket = new Socket(host, port);
        in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        out = new PrintWriter(socket.getOutputStream(), true);
    }

	// Metodi d'interfaccia (*)
    public String send(String msg) throws IOException {
        out.println(msg);
        String response = in.readLine();
        if (response == null) { /* throw IOException(...) */ }
        return response;
    }
    // Metodi d'interfaccia (*)

    @Override
    public void close() throws IOException {  // auto-chiamato a fine di try-with-resources
        in.close();
        out.close();
        socket.close();
    }
}

public class Client {
	private static final String SERVER_IP = "localhost";
    private static final int SERVER_PORT = 8888;
    
	public static void main() throws IOException {
        try (Proxy proxy = new Proxy(SERVER_IP, SERVER_PORT)) {
            // Logica applicativa client
        }
    }
}
```

Per ora non gestiamo il server in quanto è praticamente identico alle versioni precedenti in [[9 - Socket|Socket]].

###### Metodi d'interfaccia (\*)

I metodi del `Proxy` sono definiti in modo da essere (solitamente) corrispondenti a quelli nel server (o nel proxy lato server) cosicché nel client il metodo `x()` comunica col metodo `x()` del proxy server. Tali metodi possono anche essere definiti in un'**interfaccia** implementata sia dal proxy client che dal proxy server la quale implementa anche `AutoCloseable` nel mentre:

```java
// Chiamabile come si vuole?
public interface ServerInterface extends AutoCloseable {
	static final int PORT = 8888;
	// Sopra send() è generale, si avrebbe anche potuto avere:
	int get() throws IOException;
	void set(int value) throws IOException;
	// Altri metodi da ridefinire poi...
	void close() throws IOException;
}
```

(a mio avviso è solamente *boilerplate*, nel senso che se sto facendo sia client + proxy che server + proxy so quali metodi devo implementare da entrambe le parti).

```java
// Implementazioni get() e set() --> (cambia poco da usare param x msg)
public int get() throws IOException {
	out.println("get");
	String response = in.readLine();
	if (response == null) { /* throw IOException(...) */ }
	return response;
}
public void set(int value) throws IOException {
	out.println("set " + value);
	String response = in.readLine();
	if (response == null) { /* throw IOException(...) */ }
}
```

#### Proxy server

Un <u>proxy lato server</u> o ***skeleton*** fa la stessa cosa del client ma gestendo le richieste in entrata e usando la logica applicativa del server per poi rispondere. Qui si hanno 2 classi: `Server` che è la solita e `SharedResource` che è una qualsiasi risorsa condivisa sulla quale va gestita la concorrenza:

```java
import java.io.*;
import java.net.*;
// Risorsa condivisa base
public class SharedResource {
    private int value = 0;
    public synchronized int get() { return value; }
    public synchronized void set(int v) { this.value = v; }
}
// Server con multi-client + risorsa condivisa + skeleton
public class Server {
    private static final int PORT = 8888;

    public void start() throws IOException {
	    // 1 risorsa condivisa tra tutti i client
	    SharedResource resource = new SharedResource();
	    
        try (ServerSocket ss = new ServerSocket(PORT)) {
            // Ciclo di accept() di client
            while (true) {
                Socket socket = ss.accept();  // Accetta 1 client
                new Thread(new Skeleton(socket, resource)).start();  // Avvia thread con skeleton x tale client
            }
        }
    }
}
```

##### Per delega

Nell'implementazione **per delega**, `Skeleton` contiene un riferimento al server o alla risorsa condivisa (che contiene i metodi e la logica applicativa):

```java
import java.io.*;
import java.net.*;

public class Skeleton implements Runnable {
    private Socket socket;
    private SharedResource resource;  // Riferimento alla risorsa condivisa

    public Skeleton(Socket socket, SharedResource resource) {
        this.socket = socket;
        this.resource = resource;
    }

    @Override
    public void run() {
        try (BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true)) 
        {
		    // Legge comando 
            String cmd;
			while ((cmd = in.readLine()) != null) {
				int result = 0;
				
				// Switch meglio (più ez così se in cmd ci sono anche parametri)
				if (cmd.equals("get")) {
					out.println(resource.get());
					
				} else if (cmd.startsWith("set ")) {
					int v = Integer.parseInt(cmd.split(" ")[1]);
					resource.set(v);
					out.println("ok");
					
				} else {
					out.println("err")
				}
				
			}
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try { socket.close(); } catch (IOException _) {}
        }
    }
}
```

##### Per ereditarietà

Nell'implementazione **per ereditarietà**, `Skeleton` <u>eredita</u> da server o dalla risorsa condivisa espandendolo con la logica di comunicazione. Questa implementazione è quasi identica alla precedente, solo che: `SharedResource` non è più condivisa in quanto, dato che `Skeleton` la estende, ogni thread che gestisce 1 client avrà il suo `Skeleton` con la propria `Resource` privata (infatti non la si istanzia nel server e non la si passa più allo `Skeleton` thread).

---

Prossima lezione: [[]]

