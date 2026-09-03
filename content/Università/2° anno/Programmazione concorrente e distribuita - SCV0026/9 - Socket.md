# Lezione 9

### Socket

(Salto le nozioni base di reti non utili per l'esame) un ***socket*** è una coppia `[IP]:[port]` che serve per <u>identificare applicativi</u> sulle macchine e per la <u>comunicazione</u> tra loro. 

Java (package `java.net`) mette a disposizione delle classi:

- `InetAddress`: rappresenta un indirizzo IP (con sottoclassi per IPv4 `Inet4Address` e per IPv6 `Inet6Address`),
- `InetSocketAddress`: rappresenta un socket `IP:port`. 

###### Concetto e proprietà

Un *socket* è proprio come un terminale di connessione che gli oggetti che vogliono comunicare usano, come nell'esempio:

![673](https://i.imgur.com/kVOoTdR.png)

Qui si parte da un server con IP `y.y.y.y` avviato che esegue un <u>mail server</u> (porta 25), poi un client con IP `x.x.x.x` si connette al server tramite dei **socket** i quali si nota hanno diverse proprietà, tra cui `IP:port` locali e remoti. Quando la connessione viene stabilita, client e server aprono degli stream di input/output sui rispettivi socket.

(Stream per comunicazione TCP, altrimenti ? per comunicazione UDP)

#### Socket TCP

Se si sceglie il protocollo TCP per la comunicazione via socket, essa avviene tra ***server*** (che stanno in ascolto e rispondono alle richieste) e ***client*** (che inviano richieste al server).

*Client* e *server* fanno uso di classi diverse per comunicare:

- **Server**: usa la classe `ServerSocket` per ascoltare le connessioni in input (necessita solo la porta su cui accettare connessioni ed ha un metodo `accept()` che ritorna un oggetto `Socket` col quale comunicare),
- **Client**: usa la classe `Socket` per avviare connessioni (sul client necessita di IP e porta del server a cui connettersi e fornisce `getInputStream()` e `getOutputStream()` per la comunicazione, ma è possibile usare qualsiasi altro [[1 - Streams#Streams|stream]] già visto).

##### Server

Codice:

```java
import java.io.*;
import java.net.*; // con Socket e ServerSocket

public class Server {
    private static final int PORT = 4444;  // Porta dell'app server
    
    public static void main() {
        try (ServerSocket server = new ServerSocket(PORT)) {  // Crea socket server (auto-chiude alla fine)
            while (true) {  // while(true) x accettare connessioni
                Socket client = server.accept();  // Blocca finché non si accetta una connessione
                new Thread(() -> handleClient(client)).start();  // Altro thread x gestire client
            }
        } catch (IOException e) {
	        System.err.println("Errore: " + e.getMessage());
        }
    }
    
    private static void handleClient(Socket socket) {
        // Auto chiude socket client alla fine
        try (socket;
	        // I/O streams x comunicazione
	        BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            PrintWriter out = new PrintWriter(
                socket.getOutputStream(), true
            ))
        {
	        // Qui si dice come il server interpreta i messaggi e risponde al client
            // (ricezione messaggi su stream "in")
            // (invio messaggi su stream "out")
        } catch (IOException e) {
            System.err.println("Client error: " + e.getMessage());
        }
    }
}
```

> [!info] Nota
> L'IP di ascolto del `ServerSocket` se non specificato è `0.0.0.0` che implica che il server può ricevere messaggi da <u>qualsiasi IP</u>, se invece si specifica tipo: `ServerSocket("localhost", PORT)`, allora il server accetterà connessioni solamente da tale IP (in questo caso la stessa macchina su cui gira).

##### Client

Codice:

```java
import java.io.*;
import java.net.*;

public class Client {
    private static final String SERVER_IP = "localhost";
    private static final int SERVER_PORT = 4444;
    
    public static void main() {
	    // Crea socket verso server e I/O streams (auto-chiude tutto poi)
        try (Socket socket = new Socket(SERVER_IP, SERVER_PORT);
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            PrintWriter out = new PrintWriter(
                socket.getOutputStream(), true
            ))
        {
            // Qui si dice cosa il client invia al server e come elabora risposte
            // (ricezione messaggi su stream "in")
            // (invio messaggi su stream "out")            
        } catch (IOException e) {
	        System.err.println("Errore: " + e.getMessage());
        }
    }
}
```

> [!info] Nota
> L'IP del server dato al socket client può avere un qualsiasi IP, tra cui:
> - `localhost` o `127.0.0.1`: indica che client e server girano sulla stessa macchina,
> - `x.x.x.x`: un'IP locale o pubblico sul quale gira il server.

#### Socket UDP

Usando UDP, le applicazioni comunicano sempre in architettura client-server però inviando ***datagrams*** (messaggi indipendenti e auto-contenuti il cui arrivo, tempo di arrivo e contenuto non sono garantiti). Java (`java.net`) fornisce 3 classi per UDP:

- `DatagramPacket`: classe che rappresenta un *datagram*,
- `DatagramSocket`: socket che consente invio/ricezione di *datagrams*,
- `MulticastSocket`: socket usato per inviare messaggi *multicast* (indirizzati a più client).

##### Server

```java
import java.io.IOException;
import java.net.*; // con DatagramPacket e DatagramSocket

public class Server {
    private static final int PORT = 9876;
    private static final int SIZE = 1024;

    public static void main() throws IOException {
        try (DatagramSocket socket = new DatagramSocket(PORT)) {    // Crea socket server
            while (true) {
	            // Preparo buffer di ricezione (anche "byte[] receiveBuffer = new byte[SIZE];")
                DatagramPacket receivePacket = new DatagramPacket(
	                new byte[SIZE], SIZE  // Args: byte[] buffer + la sua dimensione
	            );
                socket.receive(receivePacket);   // Blocca finché non riceve un datagram

                // Esempio String: estrae il mess ricevuto dal datagram
                String data = new String(receivePacket.getData(), 0, receivePacket.getLength());
				//...

                // Ottiene IP e port del client
                InetAddress clientIP = receivePacket.getAddress();
                int clientPort = receivePacket.getPort();

				// Costruisce risposta
                String response = "ECHO: " + data;
                byte[] sendBuffer = response.getBytes();  // Istanzia un byte[] con i bytes di "response"

                // Crea il datagram di risposta
                DatagramPacket sendPacket = new DatagramPacket(
                    sendBuffer,
                    sendBuffer.length,
                    clientIP,
                    clientPort
                );
                socket.send(sendPacket);  // Invia la risposta
                
                // In caso elaborazione risposta è pesante, si può fare:
                // new Thread(() -> handlePacket(socket, ip, port)).start();
            }
        }
    }
}
```

###### Multicast socket

La classe `MulticastSocket` sostituisce semplicemente `DatagramSocket` (in server e in client) e permette l'invio di datagram a <u>gruppi multicast</u> (server cambia niente, basta che `InetAddress` dei datagram sia di un gruppo multicast, mentre client deve fare `socket.joingroup(address)` per iscriversi al gruppo e riceverne i messaggi).

##### Client

```java
import java.io.*;   // con BufferedReader, InputStreamReader e IOException
import java.net.*;  // con DatagramPacket, DatagramSocket e InetAddress

public class Client {
    private static final String SERVER_IP = "localhost";
    private static final int SERVER_PORT = 9876;
    private static final int SIZE = 1024;

    public static void main() throws IOException {        
        try (DatagramSocket socket = new DatagramSocket()) {
            // Inserimento messaggio da console
            String message;
            System.out.println("Messaggio: ");
			try (BufferedReader console = new BufferedReader(new InputStreamReader(System.in))) {
			    message = console.readLine();
			}

            // Preparazione datagram da inviare + invia
            byte[] sendBuffer = message.getBytes();
            DatagramPacket sendPacket = new DatagramPacket(
                sendBuffer,
                sendBuffer.length,
                InetAddress.getByName(SERVER_IP),  // InetAddress
                SERVER_PORT                        // int
            );
            socket.send(sendPacket);

            // Preparo buffer di ricezione + fa receive() (bloccante)
			DatagramPacket receivePacket = new DatagramPacket(
				new byte[SIZE], SIZE
			);
			socket.receive(receivePacket);

			// Esempio String: estrae il mess ricevuto dal datagram
			String data = new String(receivePacket.getData(), 0, receivePacket.getLength());
			//...
        }
    }
}
```

---

Prossima lezione: [[]]

