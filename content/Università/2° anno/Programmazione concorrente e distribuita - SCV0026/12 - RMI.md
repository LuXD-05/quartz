# Lezione 12

### RMI

**RMI** (*Remote Method Invocation*) è una tecnologia Java che permette a processi distribuiti di comunicare attraverso una rete (tipo `String res = server.func()`).

Un <u>processo</u> (client) può <u>invocare metodi su un oggetto remoto</u> (server) come se fosse locale, con _**location transparency**_ (client ignora dove si trova l'oggetto remoto).

##### Architettura

L'architettura RMI si basa su:

\- **Server**: crea oggetti remoti, li rende visibili e aspetta invocazioni,

\- **Client**: ottiene riferimenti a tali oggetti remoti e invoca metodi su di essi,

\- **Registry**: servizio che permette ai client di trovare gli oggetti remoti tramite un nome.

> [!info] Funzionamento *registry*
> 1\) Il server registra il proprio oggetto remoto sul `Registry`,
> 2\) Il client cerca l'oggetto per nome sul `Registry`,
> 3\) Il client ottiene un riferimento remoto e invoca metodi su di esso.

###### Metodi registry

L'interfaccia `Registry` fornisce:

- `bind(name, obj)`: associa un nome a un oggetto (fallisce se già presente)
- `rebind(name, obj)`: come bind ma sovrascrive se già presente
- `unbind(name)`: rimuove l'associazione
- `lookup(name)`: restituisce l'oggetto associato al nome
- `list()`: restituisce array di nomi registrati

La classe `LocateRegistry` permette di:

- `getRegistry()`: ottenere riferimento a registry esistente (default localhost:1099)
- `createRegistry(port)`: creare un nuovo registry

##### Invocazione remota

L'invocazione di un metodo remoto è praticamente un <u>passaggio di un messaggio</u> (ad un oggetto), e si fa con:

- ***Stub*** (lato client): oggetto locale che "imita" un oggetto remoto ma, invece di eseguire metodi, costruisce e manda un messaggio (di invocazione) a tale oggetto remoto.
- ***Skeleton*** (lato server): riceve il messaggio dello *stub*, ricostruisce i parametri e chiama il metodo sull'oggetto reale.

> [!info] Nota
> Nelle versioni recenti di Java, stub e skeleton sono gestiti in modo trasparente dal sistema, senza bisogno di generazione esplicita.

##### Passaggio di parametri

Ci sono 3 tipi di parametri passabili ad un server remoto:

- **Tipo primitivo**: <u>passato</u> normalmente <u>per valore</u> all'oggetto remoto,
- **Oggetto locale**: si <u>serializza una copia dell'oggetto</u> (*deep copy*, che passa anche i riferimenti ad altri oggetti),
- **Oggetto remoto**: si passa il <u>riferimento</u> dell'oggetto remoto.

> [!important] ***Dynamic class loading***
> Se l'oggetto remoto non conosce la classe di un'oggetto passato, con RMI è possibile passare anche il codice di tale classe.

###### Regole di serializzazione

Gli oggetti locali passati a/da metodi remoti:

1\) Devono implementare `Serializable`,

2\) Devono avere `serialVersionUID` dichiarato,

3\) Se contengono riferimenti ad altri oggetti, anche questi devono essere serializzabili,

4\) I campi `static` e `transient` non vengono serializzati.

```java
public class MyClass implements Serializable {
    private static final long serialVersionUID = 1L;  // OBBLIGATORIO
    private int value;
    private transient String cache;  // Non viene serializzato
    //...
}
```

#### App RMI

Per creare un'applicazione RMI:

1\) Definire l'<u>interfaccia remota</u>: deve estendere `java.rmi.Remote` e i metodi devono lanciare `RemoteException`,

2\) Implementare l'<u>oggetto remoto</u>: deve implementare l'interfaccia e estendere `UnicastRemoteObject` (o usare `exportObject()`),

3\) Implementare il <u>client</u>: deve ottenere un riferimento remoto tramite il Registry.

##### Interfaccia remota

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface Interfaccia extends Remote {
    String process(String input) throws RemoteException;
    Result compute(Task task) throws RemoteException;
}
```

##### Server

###### Con UnicastRemoteObject

```java
import java.rmi.server.UnicastRemoteObject;
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class RemoteObj extends UnicastRemoteObject implements Interfaccia {
    private static final long serialVersionUID = 1L;
    
    public RemoteObj() throws RemoteException {
        super();  // Obbligatorio
    }
    
    public String process(String input) {
        return "Processed: " + input;
    }
    
    public static void main() throws Exception {
        RemoteObj obj = new RemoteObj();
        Registry registry = LocateRegistry.createRegistry(1099);
        registry.rebind("Interfaccia", obj);
        System.out.println("Server ready");
    }
}
```

###### Con exportObject()

```java
public class RemoteObj implements Interfaccia {
    // Non estende UnicastRemoteObject
    
    public String process(String input) {
        return "Processed: " + input;
    }
    
    public static void main() throws Exception {
        RemoteObj obj = new RemoteObj();
        Interfaccia stub = (Interfaccia) UnicastRemoteObject.exportObject(obj, 0);  // 0 = porta automatica
        Registry registry = LocateRegistry.createRegistry(1099);
        registry.rebind("Interfaccia", stub);
        System.out.println("Server ready");
    }
}
```

##### Client

```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class Client {
    public static void main() throws Exception {
        Registry registry = LocateRegistry.getRegistry("localhost", 1099);
        Interfaccia stub = (Interfaccia) registry.lookup("Interfaccia");
        
        String result = stub.process("test");
        System.out.println(result);
    }
}
```

#### Callback RMI

Il callback permette al server di invocare metodi sul client:

1. Il client deve essere a sua volta un oggetto remoto

2. Il client passa il proprio riferimento al server

3. Il server usa questo riferimento per chiamare metodi sul client

##### Esempio

**Interfaccia client (remota)**

```java
public interface ChatClient extends Remote {
    void receiveMessage(String message) throws RemoteException;
    String getName() throws RemoteException;
}
```

**Implementazione client**

```java
public class ChatClientImpl extends UnicastRemoteObject implements ChatClient {
    private String name;
    
    public ChatClientImpl(String name) throws RemoteException {
        this.name = name;
    }
    
    public void receiveMessage(String message) {
        System.out.println(message);
    }
    
    public String getName() {
        return name;
    }
    
    public static void main(String[] args) throws Exception {
        ChatClientImpl client = new ChatClientImpl("User1");
        ChatServer server = (ChatServer) LocateRegistry.getRegistry().lookup("ChatServer");
        server.join(client);  // Passa il riferimento remoto del client
        // ...
    }
}
```

**Server con callback**

```java
public class ChatServerImpl extends UnicastRemoteObject implements ChatServer {
    private List<ChatClient> clients = new ArrayList<>();
    
    public synchronized void join(ChatClient client) {
        clients.add(client);
    }
    
    public synchronized void broadcast(String message, ChatClient sender) {
        for (ChatClient c : clients) {
            try {
                c.receiveMessage(sender.getName() + ": " + message);  // Callback!
            } catch (RemoteException e) {
                clients.remove(c);  // Rimuove client non raggiungibile
            }
        }
    }
}
```

> [!warning] Attenzione
> Nei metodi che gestiscono liste di client remoti (come `broadcast`), è necessario gestire le `RemoteException` per rimuovere client non più raggiungibili, altrimenti il server si bloccherebbe.

#### Shutdown ordinato del server

Per terminare un server RMI in modo pulito:

```java
public void shutdown() throws RemoteException {
    Registry registry = LocateRegistry.getRegistry();
    try {
        registry.unbind("MyService");  // Rimuove dal registry
    } catch (NotBoundException e) {}
    
    // Delega l'unexport a un thread per permettere il completamento della chiamata remota
    new Thread(() -> {
        try {
            Thread.sleep(2000);  // Attende che il client finisca
            UnicastRemoteObject.unexportObject(this, false);  // false = non forza se ci sono chiamate in corso
        } catch (Exception e) {}
    }).start();
}
```

> [!info] Nota
> `UnicastRemoteObject.unexportObject(obj, force)` rende l'oggetto non più remoto. Se `force` è `false` e ci sono chiamate in corso, restituisce `false` senza effettuare l'unexport.

#### Sicurezza in RMI

Per applicazioni distribuite su macchine diverse, è necessario un `SecurityManager`:

```java
if (System.getSecurityManager() == null) {
    System.setSecurityManager(new SecurityManager());
}
```

Il `SecurityManager` richiede un file di policy che specifica i permessi:

```java
grant {
    permission java.net.SocketPermission "*:1024-65535", "connect,accept";
    permission java.security.AllPermission;  // Permissivo (solo per test!)
};
```

Esecuzione con policy: `java -Djava.security.policy=policy.txt Server`

> [!warning] Attenzione
> Se client e server girano sulla stessa macchina, il SecurityManager non è necessario (ma è buona pratica usarlo).

#### Deployment

In ambiente distribuito, le classi necessarie sono:

- **Server**: interfaccia remota + implementazione server + classi serializzabili
- **Client**: interfaccia remota + implementazione client + classi serializzabili
- **Registry**: interfaccia remota (se separato dal server)

Per il dynamic class loading (classi non disponibili localmente), usare: `java -Djava.rmi.server.codebase=http://serverhost/classes/ Server`

---

Prossima lezione: [[]]

