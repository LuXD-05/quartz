### Firma digitale

##### Cos'è

> [!important] Firma digitale
> Consiste nella creazione di un **file** (detto "<u>busta crittografica</u>") che <u>racchiude il documento originale</u>, la <u>firma digitale</u> e la <u>chiave</u> per la verifica di quest'ultima (a sua volta contenuta nel <u>certificato</u> emesso a nome del firmatario).
> L'**autenticità** del certificato è garantita da un'<u>autorità di certificazione</u>.

##### Documento firmato

Un **documento firmato** digitalmente <u>ha piena efficacia giuridica</u>, a <u>condizione</u> che **non** sia stato **modificato dopo la firma**.

![](https://i.imgur.com/3Wk6KYX.png)

### Tipi di firme

Esistono **3 tipi di firme digitali** definite da standard europei (usati anche in Italia): le firme **CAdES**, **PAdES** e <u>XAdES</u> (l'ultima non trattata).

#### CAdES

##### Cos'è

Un **file firmato CAdES** è un file con estensione "*.p7m*" il cui contenuto è visualizzabile solo con <u>sw idonei</u> in grado di "sbustare" il documento.

- **Vantaggio**: con tale formato è <u>possibile firmare qualsiasi tipo di file</u>,
- **Svantaggio**: è <u>necessario un sw specifico</u> per visualizzare il documento.

##### Firme multiple

Col formato CAdES è possibile <u>apporre 2 o + firme</u> in 2 modi:

- **Controfirme**: (o "*firme matrioska*) ovvero <u>re-imbustando in una nuova busta CAdES la busta precedente</u> (documento già prima firmato).

  ![](https://i.imgur.com/HpbBPwl.png)

 - **Firme congiunte**: cioè aggiungendo una <u>firma ulteriore</u>, accompagnata dal relativo <u>certificato</u>, <u>alla busta</u>.

   ![](https://i.imgur.com/p4L9Eza.png)

##### Aggiunta di dati dopo la firma

In <u>entrambi i casi</u> precedenti, il documento firmato rimarrà unico e **non sarà possibile modificarne i dati (o aggiungerne)** dopo. Ciò perché, anche se si <u>esportasse il documento</u> nella busta al <u>formato originale non firmato</u>, le **modifiche invaliderebbero le firme** (se riapplicate). Alla fine si avrebbe un documento firmato ed un altro con i dati aggiuntivi non firmato.

#### PAdES

##### Cos'è

Un file firmato PAdES è un file con estensione "*.pdf*" (firma detta anche "*firma PDF*"), leggibile con un qualsiasi PDF *reader*.

- **Vantaggi**: prevede <u>diverse modalità di firma</u> ed è <u>facilmente accessibile</u>,
- **Svantaggio**: consente <u>solo la firma di PDF</u>.

##### Predisposizione del PDF

Si possono <u>predisporre documenti</u> (tipo di word) <u>alla firma digitale</u> con strumenti conformi allo **standard PDF** (<u>ISO 32000</u>, tipo *Acrobat Reader*); quindi a tal fine serve:

1) <u>Cambiarne il formato in PDF</u>,
2) <u>Predisporre i campi firma</u> (nei PDF collocabili fisicamente in un qualsiasi punto deciso),
3) (Eventualmente) predisporre <u>campi di testo per</u> l'inserimento di <u>info successive alla firma</u>.
4) (Eventualmente) <u>rendere il documento usabile</u> anche con <u>versioni non professionali di app</u> conformi allo <u>standard PDF</u> (tipo *Adobe Reader*).

##### Firme multiple

Il formato PAdES permette **firme multiple** implementando il ***versioning***, per cui <u>ogni versione successiva</u> del file <u>contiene</u> anche la <u>versione originale del documento precedente</u> (firme vecchie comprese).

![](https://i.imgur.com/UrMAVnj.png)

##### Aggiunta di dati dopo la firma

Il *versioning* torna comodo anche per l'**aggiunta di dati** al documento **dopo la firma** (tipo annotazioni) in quanto, nonostante le versioni successive con le modifiche, quelle <u>precedenti</u> (+ le firme vecchie) sono **comunque accessibili e conservano** la loro **efficacia giuridica** (anche se alcuni programmi non le riconoscono correttamente come segue).

![](https://i.imgur.com/NxqPoBX.png)

