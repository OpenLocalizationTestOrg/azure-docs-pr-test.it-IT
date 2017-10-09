## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Definizione della struttura per i set di dati rettangolari
Hello struttura sezione hello i set di dati JSON è un **facoltativo** sezione per le tabelle rettangolare (con righe e colonne) e contiene una raccolta di colonne per tabella hello. Sezione relativa alla struttura hello si utilizzerà per entrambi che fornisce informazioni sul tipo per le conversioni di tipo oppure al mapping delle colonne. Hello le sezioni seguenti descrizione queste funzionalità in modo dettagliato. 

Ogni colonna contiene hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| name |Nome della colonna hello. |Sì |
| type |Tipo di dati della colonna hello. Vedere la sezione sulle conversioni del tipo di seguito per altre informazioni su quando specificare le informazioni sul tipo |No |
| culture |Impostazioni cultura toobe utilizzato quando il tipo specificato e .NET Datetime o Datetimeoffset basato su .NET. Il valore predefinito è "en-us". |No |
| format |Formato stringa toobe utilizzato quando il tipo specificato e .NET Datetime o Datetimeoffset. |No |

Hello esempio seguente viene illustrato il sezione di struttura hello JSON per una tabella con tre colonne userid, il nome e lastlogindate.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Hello indicazioni su quando utilizzare informazioni "struttura" tooinclude e quali tooinclude in hello **struttura** sezione.

* **Per le origini dati strutturati** che archiviano informazioni dello schema e il tipo di dati insieme ai dati hello stesso (origini come SQL Server, Oracle, tabelle di Azure e così via), è necessario specificare sezione "struttura" hello solo se si desidera eseguire i mapping di colonne di specifico colonne di origine sono colonne toospecific sink e i nomi dei hello non uguale (vedere i dettagli nella sezione seguente mapping delle colonne). 
  
    Come indicato in precedenza, nella sezione "struttura" informazioni sul tipo hello è facoltativi. Per le origini strutturate, le informazioni sul tipo è già disponibile come parte della definizione di set di dati nell'archivio dati hello, pertanto non è necessario includere le informazioni sul tipo quando si include la sezione "struttura" hello.
* **Per lo schema su origini dei dati letti (in particolare blob di Azure)** è possibile scegliere i dati toostore senza archiviare le informazioni di tipo o schema con dati hello. Per questi tipi di origini dati è necessario includere "struttura" in hello 2 casi seguenti:
  * Si desidera toodo mapping della colonna.
  * Quando set di dati hello è un'origine in un'attività di copia, è possibile fornire informazioni sul tipo "struttura" e data factory di questo tipo di informazioni per i tipi di conversione toonative per il sink hello. Vedere [spostare tooand dati da Blob di Azure](../articles/data-factory/data-factory-azure-blob-connector.md) per ulteriori informazioni.

### <a name="supported-net-based-types"></a>Tipi supportati basati su .NET
Data factory supporta hello seguente .NET conformi a CLS in base a valori di tipo per fornire informazioni sul tipo "struttura" per lo schema su origini dei dati letti come blob di Azure.

* Int16
* Int32 
* Int64
* Single
* Double
* Decimale
* Byte[]
* Booleano
* String 
* Guid
* Datetime
* Datetimeoffset
* TimeSpan 

Per Datetime e Datetimeoffset è anche possibile specificare "culture" e "format" toofacilitate analisi delle stringhe della stringa di data/ora personalizzata. Vedere l'esempio seguente di conversione del tipo.

