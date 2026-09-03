# Lezione 13

### Eventi e Observer

Quando un server deve notificare asincronamente più client (pattern Observer/Listener), itera su una lista di riferimenti remoti per chiamare un metodo su di essi. Questo è il contesto _**tipico del 1° esercizio dell'esame**_, il prof inserirà bug di concorrenza subdoli.

#### Le 3 insidie da correggere

1. **Concorrenza sulla lista**: La lista dei client è condivisa tra il thread che notifica (es. `while(true)`) e i thread RMI che gestiscono le chiamate di `add`/`remove` da parte dei client.

2. **Rimozione in iterazione**: Se un client si disconnette, la chiamata lancia `RemoteException` e il server deve rimuoverlo dalla lista. Farlo in un for-each classico crasha tutto il server.

3. **Propagazione eccezioni**: Se il client 3 è crashato, l'eccezione non deve uscire dal ciclo `for`, altrimenti i client 4, 5 e 6 non riceveranno la notifica.

##### Codice generico corretto

Per risolvere tutti e 3 i problemi in un colpo solo:

```java
private final List<RemoteListener> listeners = new ArrayList<>();

// 1. Sincronizza l'accesso alla lista condivisa
private synchronized void notifyListeners(Object param) {
    // 2. Usa l'Iterator per la rimozione sicura
    Iterator<RemoteListener> iter = listeners.iterator();
    while (iter.hasNext()) {
        try {
            iter.next().remoteEvent(param);
        } catch (RemoteException e) {
            // 3. Catch STRETTAMENTE dentro il ciclo: non blocca gli altri client
            iter.remove(); // Rimuove in sicurezza, no ConcurrentModificationException
        }
    }
}
```

> [!warning] Attenzione
> Se vedi `listeners.remove(l)` dentro un ciclo `for (RemoteListener l : listeners)`, **è un errore garantito**. Lancia `ConcurrentModificationException` e fa crashare il server. Usa sempre `Iterator`.

#### Pattern "Wrapper"

Se l'esercizio successivo ti chiede di usare classi locali (come `java.util.Observable`) ma i client sono RMI, non puoi passare l'oggetto remoto alla lista locale. Si usa un _**Wrapper**_ (o Proxy locale):

- Crei una classe locale `WrappedObserver` che implementa l'interfaccia locale (`Observer`).
- Al suo interno tiene un riferimento all'interfaccia remota (`RemoteObserver`).
- Quando la lista locale chiama `update()`, il wrapper fa da ponte e chiama il metodo RMI sul client, gestendo lì la `RemoteException` e rimuovendo se stesso (`deleteObserver(this)`). In pratica disaccoppia la logica di notifica standard di Java dalla logica di rete RMI.

---

Prossima lezione: [[]]

