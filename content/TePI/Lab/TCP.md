---
public: true
edited_seconds: 1090
modified_at: 24/03/2024 16:44:07
---
### TCP in C\#
In C# è possibile creare connessioni TCP tra un client e un server mediante l'uso di diverse cose.
### Lato client
##### Grafica
La grafica solitamente è composta da elementi di inserimento dati (TextBox...), elementi di invio dati (Button...) ed elementi di visualizzazione dati (TextBlock, ListView...). L'esempio sarà la gestione delle ordinazioni di un ristorante per i vari tavoli.
```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="*"></RowDefinition>
        <RowDefinition Height="7*"></RowDefinition>
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"></ColumnDefinition>
        <ColumnDefinition Width="2*"></ColumnDefinition>
    </Grid.ColumnDefinitions>
    
    <!-- tavolo -->
    <TextBlock HorizontalAlignment="Center" VerticalAlignment="Center">Tavolo</TextBlock>
    <TextBox Name="tbTavolo" Grid.Column="1" Height="30" Width="160"></TextBox>
    
    <!-- ordina -->
    <Button Name="btnOrder" Click="btnOrder_Click" Height="30" Width="140" Grid.Row="1" VerticalAlignment="Center">Ordina</Button>
    
    <!-- cibo -->
	<StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
		<Label Height="30" Width="140" Content="Ordine"/>
		<TextBox Name="tbCibo" Height="30" Width="140"/>
	</StackPanel>
	
</Grid>
```
##### TcpManager
Verrà poi creata la classe TcpManager, la quale prevede dei metodi per l'invio e per la ricezione di messaggi da parte del client. Questa richiede `System.Net.Sockets` per il TCP e `System.Text` per le conversioni da `byte[]` a `string` e viceversa.
```c#
public class TcpManager
{
    TcpClient client;
    NetworkStream ns;

    public TcpManager()
    {
        client = new TcpClient("127.0.0.1", 12345);
        ns = client.GetStream();
    }

    public void Send(string s)
    {
        byte[] data = new byte[1024];
        data = ASCIIEncoding.ASCII.GetBytes(s);
        ns.Write(data, 0, data.Length);
    }

    public string Receive()
    {
        byte[] arr = new byte[1024];
        int bytes = ns.Read(arr, 0, arr.Length);
        return ASCIIEncoding.ASCII.GetString(arr, 0, bytes);
    }
}
```
##### Client code-behind
Il codice del client (WPF) si struttura così:
```c#
public partial class MainWindow : Window
{
    TcpManager m;

    TcpClient client;
    NetworkStream ns;

    public MainWindow()
    {
        InitializeComponent();
        m = new TcpManager();
    }

    private void btnOrder_Click_1(object sender, RoutedEventArgs e)
    {
        var s = tbCibo.Text;
        var t = tbTavolo.Text;

        if (!string.IsNullOrEmpty(s) && !string.IsNullOrEmpty(t) && int.TryParse(t, out _))
        {
            m.Send(t + "-" + s);

            string res = m.Receive();

            if (!res.StartsWith("Ordine confermato"))
            {
                var g = MessageBox.Show(res, "a", MessageBoxButton.YesNo);

                if (g == MessageBoxResult.Yes)
                    m.Send(t + "-" + s);
                else
                    m.Send("no");

                res = m.Receive();
                MessageBox.Show(res);
            }
        }
    }
}
```
### Lato server
##### Entry point
Il server invece sarà una semplice applicazione console, il cui entry point sarà:
```c#
static void Main()
{
    Manager m = new Manager();
    while (true)
        m.Listen();
}
```
##### Manager
Il manager sarà invece la classe in cui saranno presenti i metodi per la gestione dei dati, oltre che parte centrale del programma server referenziante anche il TcpManager e il FileManager:
```c#
public class Manager
{
    TcpManager m;

    public Manager()
    {
        m = new TcpManager("127.0.0.1", 12345);
        FileManager.CreateDbIfNotExists();
    }

    public void Listen()
    {
        if (m.Connect())
            new Thread(Do) { IsBackground = true }.Start();
    }

    public void Do()
    {
        var mess = m.Receive();
		var tavolo = mess.Split('-')[0];

        List<string> ordini = FileManager.Read();

        if (ordini.Contains(mess))
        {
            ordini.Add(mess);
            FileManager.Write(ordini);

            m.Send("Ordine confermato");
        }
        else
        {
            m.Send("Hai già un ordine in sospeso. Aggiungere cmq?");

            mess = m.Receive();

            if (mess == "no")
                m.Send("Ordine non aggiunto");
            else
            {
                ordini.Add(mess);
                FileManager.Write(ordini);

                m.Send("Ordine aggiunto comunque");
            }
        }
    }
}
```
##### TcpManager
Il TcpManager sarà simile a quello del client, ma con qualche aggiunta in più:
```c#
public class TcpManager
{
    TcpListener listener;
    TcpClient client;
    NetworkStream ns;

    public TcpManager(string ip, int port)
    {
        listener = new TcpListener(IPAddress.Parse(ip), port);
        listener.Start();
    }

    public bool Connect()
    {
        bool res;

        try
        {
            client = listener.AcceptTcpClient();
            ns = client.GetStream();
            res =  true;
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
            res = false;
        }

        return res;
    }

    public void Send(string s)
    {
        byte[] data = new byte[1024];
        data = ASCIIEncoding.ASCII.GetBytes(s);
        ns.Write(data, 0, data.Length);
    }

    public string Receive()
    {
        byte[] arr = new byte[1024];
        int bytes = ns.Read(arr, 0, arr.Length);
        return ASCIIEncoding.ASCII.GetString(arr, 0, bytes);
    }
}
```
##### FileManager
Per quanto riguarda il FileManager, la gestione + semplice è fatta con i seguenti metodi:
```c#
public static class FileManager
{
    static string path = @"./db.txt";

    public static void CreateDbIfNotExists()
    {
        if (!File.Exists(path))
            File.Create(path).Close();
    }

    public static List<string> Read()
    {
        return File.ReadAllLines(path).ToList();
    }

    public static void Write(List<string> s)
    {
        File.WriteAllLines(path, s);
    }
}
```