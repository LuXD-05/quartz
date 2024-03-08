# HTML
### 1) DEFAULT
Di base ricordarsi di inserire:
- !DOCTYPE html>
- html>...</html
    - head>...</head
        - title></title
        - style></style {+ eventuale <script}

### TAGS
Form
(per metterlo in mezzo):
    form, form > * {             
        margin: auto;
        width: fit-content;
        display: block;
    }
)
    - action="..."
        "" --> dopo submit va alla pagina corrente (ma è meglio "?")
        "pagina.php" --> submitta alla pagina specificata (pagina.php)
    - method="..."
        GET --> Passa il contenuto dei tag con l'attributo 'name=""' nella query string, da usare 
                solo quando non mi interessa che i miei dati vengano visti da chiunque
        POST --> Passa il contenuto dei tag con l'attributo 'name=""' nel payload, da usare
                 quando voglio passare dei dati in segreto, senza che altri li vedano in plain sight
        
3) input
    - type="..."
        button              image
        checkbox            number
        color               password
        radio               date                --> tb con data
        text                submit              --> invia dati al contenuto di action del form e ricarica
        email               datetime-local      --> come date ma con ore e minuti
        file                time                --> solo ore e minuti
        hidden              url
    - name="..."
        il contenuto dell'input sarà disponibile all'action del form attraverso:
        $_{METHOD}["{name}"]; --> quindi: name="a" + method="get" --> $_GET["a"]
    - value="..."
        Testo dell'input, tipo per il submit
        
4) select
    - name="..." --> (come input)
    option (<option>...</option>)
        - value --> Inserire sia qui sia in ... il valore della option      (this di indicizzazione?)
        - ...   --> Inserire sia qui sia in value il valore della option    (this di valore?)
        
5) table
    - border=1
        Da un bordo semplice alla tabella
    tr (Indica una TableRow (sia per header che per row))
        th (TableHeader, è in grassetto)
        td (Table?, riga normale)

6) img

      

############################# VARIABILI #############################

Variabili non sono tipizzate, auto riconoscimento del tipo da PHP.

1) DICHIARAZIONE
    generica    --> $var = ...;
    array       --> $arr = [...];   o   $arr = array(...);

2) FUNZIONI GENERICHE
empty($var)     --> true se la variabile contiene "" (string vuota) o 0
isset($var)     --> true se la variabile è inizializzata
is_null($var)   --> true se la variabile è null
unset($var)     --> distrugge l'argomento (disalloca il contenuto della variabile, che sia connessioni, files, array...)
print_r($var)   --> stampa info sull'argomento (simile a echo $var;)
is_[int/float/string/array/numeric]($var) --> true se la $var è [...]. 
    ATTENZIONE: is_numeric restituisce true anche con: is_numeric("7");

3) FUNZIONI DI STRINGHE
trim($s)            --> toglie leading (LEFT) e trailing (RIGHT) spaces
ltrim($s)           --> toglie leading (LEFT) spaces
rtrim($s)           --> toglie trailing (RIGHT) spaces
strlen($s)          --> length string
strpos($s1, $s2)    --> ritorna la posizione (indice) di $s2 in $s1 se la trova, altrimenti false
strstr($s1, $s2)    --> cerca $s2 in $s1, restituendo $s1 dal punto in cui trova $s2 in $s1
strtolower($s)      --> toLower
strtoupper($s)      --> toUpper
ucfirst($s)         --> upper 1° carattere
ucwords($s)         --> upper ogni carattere iniziale di ogni parola della stringa
explode($c, $s)     --> splitta $s per $c (togliendo i $c) e ritorna un array
substr($s, $n, [$l])    --> ritorna substring a partire dall'indice passato $n, lunga $l char
str_replace($s1, $s2, $s3) --> mette $s1 in $s2 quando lo trova ($s2) in $s3

4) FUNZIONI DI ARRAY
count($arr)             --> length array
sort($arr)              --> ordina in ordine crescente (valori e chiavi)
rsort($arr)             --> ordina in ordine crescente reversato (valori e chiavi)
asort($arr)             --> come sort (solo valori)
arsort($arr)            --> come rsort (solo valori)
in_array($var, $arr)    --> true se $var è nell'array (valore)
array_search($var, $arr)        --> ritorna la chiave dell'elemento che ha trovato, altrimenti falso
array_reverse($arr, [...])      --> inverte ordine elementi array. Default inverte valori. Se passo true al [...] inverte anche chiavi
array_key_exists($var, $arr)    --> come true se $var è nell'array (chiave)

Aggiunta elemento ad array
    MEGLIO: $arr[] = $var;
    PEGGIO: array_push($arr, $var);

Rimozione elemento da array
    EASY: unset($arr[$key]);            --> Non riordina keys
    HARD: array_splice($arr, $i, $n);   --> rimuove dall'array $n elementi dall'indice $i, riordina keys


############################# GET/POST #############################

1) GET
Quando passo all'action con method = GET, parametri visibili e passati in query string
Parametri = content di elementi aventi name="...", accessibili con $_GET["..."];

2) POST
Quando passo all'action con method = POST, parametri non visibili e passati in payload
Parametri = content di elementi aventi name="...", accessibili con $POST["..."];


############################# CLASSI (E MODULI) #############################

1) SINTASSI
    - Classe
        class Classe
        {
            
        }

    - Attributi
        public $Var; //(Tipo in automatico, non sono proprietà)

    - Costruttore
        function __construct($var)
        {
            $this -> Var = $var;
        }

2) OGGETTI
    - Istanze
        $c = new Classe($var);

    - Acesso attributi di un oggetto
        $c -> Var = ...     
        (è come fare c.Var in C#)

3) MODULI
    Avendo un modulo php contenente una classe o delle funzioni, posso includerlo in un altro e usarne le funzionalità:
    - Aggiunta a file.php
        include "utils.php";


############################# FILES #############################

1) FUNZIONI
    - file_get_contents($path)
        Ritorna il contenuto del file nel $path (string) in stringa (se riesce a leggerlo)
    - file_put_contents($path, $data)
        Scrive il contenuto di $data (tipo mixed) nel file nel $path
    - scandir($dir)
        Ottiene tutti gli elementi di una cartella. Di base ha sempre:
        [0] => "."      (dir relativa/corrente)
        [1] => ".."     (dir parent)
        (per pulirla da questi ci sono 2 modi:)    
        - Saltare i primi 2 indici
        - $arr = array_diff(scandir($dir), array('..', '.'));

2) ATTENZIONE
    Quando si va a fare scandir o qualsiasi altra cosa con file in cui si usa una cartella,
    fare attenzione alla var come parametro perché:
    - deve iniziare con ./cartella/... (nel caso di directory corrente, altrimenti ../...)
    - se file, deve essere presente nel path anche l'estensione


############################# JSON #############################

1) FUNZIONI
    json_encode($var);
        Codifica l'oggetto (mixed) $var in formato json
    json_decode($var)
        Decodifica una stringa formato json in un oggetto

2) JSON + FILE
    Scrivere un json:
        file_put_contents("file.json", json_encode($arr));
    Leggere un json:
        $arr = json_decode(file_get_contents("file.json"));