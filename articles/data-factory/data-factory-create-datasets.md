---
title: set di dati aaaCreate nella Data Factory di Azure | Documenti Microsoft
description: "Informazioni su come toocreate set di dati in Data Factory di Azure, con esempi che utilizzano le proprietà come offset e anchorDateTime."
keywords: creare set di dati, esempio di set di dati, esempio di offset
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Set di dati in Azure Data Factory
In questo articolo vengono descritti i set di dati, la procedura di definizione dei set in formato JSON e le modalità di utilizzo nelle pipeline di Azure Data Factory. Fornisce informazioni dettagliate su ogni sezione (ad esempio, struttura, disponibilità e criteri) nella definizione di hello set di dati JSON. Hello articolo sono inoltre disponibili esempi per l'utilizzo di hello **offset**, **anchorDateTime**, e **stile** proprietà in una definizione di set di dati JSON.

> [!NOTE]
> Se si tooData nuova Factory, vedere [tooAzure introduzione Data Factory](data-factory-introduction.md) per una panoramica. Se non si dispone di familiarità con la creazione di data factory, è possibile acquisire una comprensione migliore per la lettura hello [esercitazione sulle trasformazioni dati](data-factory-build-your-first-pipeline.md) hello e [esercitazione lo spostamento dei dati](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Panoramica
Una data factory può comprendere una o più pipeline. Una **pipeline** è un raggruppamento logico di **attività** che insieme eseguono un compito. attività Hello in una pipeline definire tooperform azioni sui dati. Ad esempio, è possibile utilizzare un copia attività toocopy di dati da un tooAzure di SQL Server locale nell'archiviazione Blob. Quindi, è possibile utilizzare un'attività Hive che esegue uno script Hive in dati di tooprocess un cluster Azure HDInsight da dati di output tooproduce archiviazione Blob. Infine, è possibile utilizzare una seconda copia attività toocopy hello output dati tooAzure SQL Data Warehouse, in cui la business intelligence (BI) reporting soluzioni vengono compilate. Per altre informazioni su pipeline e attività, vedere [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md).

Un'attività può non avere alcun **set di dati** di input o averne più di uno e generare uno o più set di dati di output. Un set di dati di input rappresenta hello l'input per un'attività nella pipeline hello e un set di dati di output rappresenta l'output di hello per attività hello. I set di dati identificano i dati all'interno dei diversi archivi dati, come tabelle, file, cartelle e documenti. Ad esempio, un set di dati Blob di Azure specifica contenitore blob hello e cartelle nell'archiviazione Blob da cui hello pipeline deve leggere i dati di hello. 

Prima di creare un set di dati, creare un **servizio collegato** toolink toohello data factory di archiviano i dati. Servizi collegati sono molto simili a stringhe di connessione, che definiscono le informazioni di connessione hello necessarie per le risorse di tooexternal tooconnect Data Factory. Set di dati di identificare i dati in archivi dati hello collegato, ad esempio tabelle SQL, file, cartelle e documenti. Ad esempio, una risorsa di archiviazione di Azure collegati collegamenti al servizio una data factory toohello account di archiviazione. Un set di dati Blob di Azure rappresenta il contenitore di blob hello e la cartella di hello contenente hello input BLOB toobe elaborati. 

Di seguito è riportato uno scenario di esempio. toocopy dati dal database SQL tooa archiviazione Blob, creare due servizi collegati: archiviazione di Azure e Database SQL di Azure. Quindi, creare due set di dati: set di dati Blob di Azure (che fa riferimento il servizio di archiviazione di Azure collegati toohello) e set di dati di tabelle di SQL Azure (che fa riferimento il servizio di Database SQL di Azure collegati toohello). Hello archiviazione di Azure e Database SQL di Azure servizi collegati contengono stringhe di connessione che utilizza Data Factory in fase di esecuzione tooconnect tooyour di archiviazione di Azure e Database SQL di Azure, rispettivamente. set di dati Blob di Azure Hello specifica contenitore blob hello e la cartella di blob che contiene i BLOB di input hello nell'archiviazione Blob. set di dati tabella di SQL Azure Hello specifica tabella SQL hello nei dati SQL database toowhich hello toobe copiati.

Hello diagramma seguente illustra le relazioni di hello tra pipeline, attività, set di dati e il servizio collegato in Data Factory: 

![Relazione tra pipeline, attività, set di dati, i servizi collegati](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>Set di dati JSON
Un set di dati in Data Factory viene definito in formato JSON come segue:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Hello nella tabella seguente vengono descritte le proprietà in hello sopra JSON:   

| Proprietà | Descrizione | Obbligatorio | Default |
| --- | --- | --- | --- |
| name |Nome del set di dati hello. Per le regole di denominazione, vedere [Azure Data Factory: regole di denominazione](data-factory-naming-rules.md) . |Sì |ND |
| type |tipo di set di dati hello. Specificare uno dei tipi di hello supportati da Data Factory (ad esempio: AzureBlob, AzureSqlTable). <br/><br/>Per informazioni dettagliate, vedere [Tipo di set di dati](#Type). |Sì |ND |
| structure |Schema di set di dati hello.<br/><br/>Per informazioni dettagliate, vedere [Struttura del set di dati](#Structure). |No |ND |
| typeProperties | le proprietà di tipo Hello sono diverse per ogni tipo (ad esempio: Blob di Azure, tabelle di SQL Azure). Per informazioni dettagliate sui tipi di hello supportato e le relative proprietà, vedere [tipo Dataset](#Type). |Sì |ND |
| external | Valore booleano flag toospecify se un set di dati generata in modo esplicito tramite una pipeline di factory di dati o non. Se hello input set di dati per un'attività non viene generato dalla pipeline corrente hello, impostare questo flag tootrue. Impostare questo flag tootrue per set di dati input hello della prima attività hello nella pipeline hello.  |No |false |
| disponibilità | Definisce hello finestra di elaborazione (ad esempio, oraria o giornaliera) o hello sezionamento modello per la produzione di hello set di dati. Ogni unità di dati usata e prodotta da un'esecuzione di attività prende il nome di sezione di dati. Se la disponibilità di hello di un set di dati di output è toodaily set (frequenza - Day, intervallo di-1), una sezione viene prodotta ogni giorno. <br/><br/>Per informazioni dettagliate, vedere [Disponibilità dei set di dati](#Availability). <br/><br/>Per informazioni dettagliate sul set di dati hello sezionamento modello, vedere hello [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) articolo. |Sì |ND |
| policy |Definisce i criteri di hello o condizione hello che devono soddisfare le sezioni di hello set di dati. <br/><br/>Per informazioni dettagliate, vedere hello [criteri Dataset](#Policy) sezione. |No |ND |

## <a name="dataset-example"></a>Esempio di set di dati
Nell'esempio seguente di hello, hello set di dati rappresenta una tabella denominata **MyTable** in un database SQL.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Si noti hello seguenti punti:

* **tipo** è impostato tooAzureSqlTable.
* **tableName** (tipo tooAzureSqlTable specifico) è impostata tooMyTable.
* **linkedServiceName** fa riferimento a servizio tooa collegato di tipo AzureSqlDatabase, definita nel frammento JSON seguente hello. 
* **frequenza di disponibilità** è impostata, tooDay e **intervallo** è impostato too1. Ciò significa che tale sezione del set di dati hello viene prodotta ogni giorno.  

**AzureSqlLinkedService** è definito come segue:

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Nel precedente frammento di codice JSON di hello:

* **tipo** è impostato tooAzureSqlDatabase.
* **connectionString** proprietà di tipo specifica informazioni tooconnect tooa SQL database.  

Come si può notare, hello servizio collegato definisce come database SQL tooa tooconnect. set di dati Hello definisce quale tabella viene utilizzato come input e output per l'attività hello in una pipeline.   

> [!IMPORTANT]
> Se non è in corso un set di dati di produzione dalla pipeline di hello, deve essere contrassegnato come **esterno**. Questa impostazione si applica in genere tooinputs della prima attività in una pipeline.   


## <a name="Type"></a> Tipo di set di dati
tipo Hello del set di dati hello dipende dall'archivio dati hello che è utilizzare. Vedere la seguente tabella per un elenco di archivi di dati supportati da Data Factory hello. Fare clic su un toolearn archivio dati come toocreate un servizio collegato e un set di dati per tali dati archivio.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Gli archivi dati con * possono essere locali o in un'infrastruttura distribuita come servizio (IaaS) di Azure. Questi archivi dati richiedono tooinstall [Gateway di gestione dati](data-factory-data-management-gateway.md).

Nell'esempio hello nella sezione precedente di hello, tipo di hello del set di dati hello è impostato troppo**AzureSqlTable**. Analogamente, per un set di dati Blob di Azure, hello tipo di set di dati hello è impostato troppo**AzureBlob**, come illustrato nella seguente JSON hello:

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <a name="Structure"></a>Struttura del set di dati
Hello **struttura** sezione è facoltativa. Definisce schema hello di hello set di dati contenente una raccolta di nomi e i tipi di dati delle colonne. Utilizzare hello struttura sezione tooprovide le informazioni sul tipo tooconvert utilizzati tipi e il mapping delle colonne hello origine toohello di destinazione. Nell'esempio seguente di hello, set di dati hello ha tre colonne: `slicetimestamp`, `projectname`, e `pageviews`. Sono rispettivamente di tipo String, String e Decimal.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Ogni colonna della struttura di hello contiene hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| name |Nome della colonna hello. |Sì |
| type |Tipo di dati della colonna hello.  |No |
| culture |. Le impostazioni cultura basate su NET toobe usato quando il tipo di hello è un tipo .NET: `Datetime` o `Datetimeoffset`. valore predefinito di Hello è `en-us`. |No |
| format |Formato stringa toobe usato quando il tipo di hello è un tipo .NET: `Datetime` o `Datetimeoffset`. |No |

Hello linee guida seguenti consentono di determinare quando tooinclude struttura informazioni e quali tooinclude in hello **struttura** sezione.

* **Per le origini dati strutturati**, specificare sezione struttura hello solo se si desidera eseguire il mapping di colonne toosink colonne di origine e i relativi nomi sono hello non uguali. Questo tipo di origine di dati strutturati archivia le informazioni dello schema e il tipo di dati insieme ai dati hello stesso. Alcuni esempi di origini dati strutturate sono SQL Server, Oracle e la tabella di Azure. 
  
    Informazioni sul tipo è già disponibile per le origini dati strutturati, non è necessario includere le informazioni sul tipo quando si include una sezione di struttura hello.
* **Per lo schema su origini dei dati letti (in particolare, archiviazione Blob)**, è possibile scegliere i dati toostore senza archiviare le informazioni di tipo o schema con dati hello. Per questi tipi di origini dati, è possibile includere struttura quando si desidera toomap origine colonne toosink colonne. Includere inoltre struttura quando hello set di dati è un input per un'attività di copia e tipi di dati del set di dati di origine devono essere convertito toonative tipi per il sink hello. 
    
    Data Factory supporta i seguenti valori per fornire informazioni sul tipo di struttura hello: **Int16, Int32, Int64, Single, Double, Decimal, Byte [], valore booleano, stringa, Guid, Datetime, Datetimeoffset e Timespan**. Sono valori dei tipi basati su .NET e conformi a CLS (Common Language Specification).

Data Factory esegue automaticamente le conversioni di tipo quando si spostano dati da un'origine tooa archiviano dati sink. 
  

## <a name="dataset-availability"></a>Disponibilità dei set di dati
Hello **disponibilità** sezione in un set di dati definisce l'elaborazione finestra hello (ad esempio orario, giornaliero, o settimanale) per hello set di dati. Per altre informazioni sugli intervalli di attività, vedere [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).

Hello seguente sezione di disponibilità specifica che hello set di dati di output è sia generate ogni ora o set di dati input hello è disponibile ogni ora:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Se la pipeline hello ha hello dopo l'ora di inizio e fine:  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Hello set di dati di output viene generato all'interno della pipeline hello inizio ogni ora e di fine. Questa pipeline genera quindi cinque sezioni di set di dati, una per ogni intervallo di attività (00:00 - 01:00, 01: 00 - 02:00, 02:00 - 03:00, 03:00 - 04:00, 04:00 - 05:00). 

Hello nella tabella seguente vengono descritte le proprietà che è possibile utilizzare nella sezione di disponibilità hello:

| Proprietà | Descrizione | Obbligatorio | Default |
| --- | --- | --- | --- |
| frequency |Specifica l'unità di tempo hello per la produzione di sezione set di dati.<br/><br/><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese |Sì |ND |
| interval |Specifica un moltiplicatore per la frequenza.<br/><br/>"Intervallo di frequenza x" determina la frequenza con cui hello sezione viene prodotta. Ad esempio, se è necessario hello toobe dataset sezionati su base oraria, impostare <b>frequenza</b> troppo<b>ora</b>, e <b>intervallo</b> troppo<b>1</b>.<br/><br/>Si noti che se si specifica **frequenza** come **minuto**, è necessario impostare hello intervallo toono inferiore a 15. |Sì |ND |
| style |Specifica se deve essere prodotta sezione hello hello inizio o alla fine dell'intervallo "hello".<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Se **frequenza** è troppo**mese**, e **stile** è troppo**EndOfInterval**, hello sezione viene prodotta hello ultimo giorno del mese. Se **stile** è troppo**StartOfInterval**, hello sezione viene prodotta hello primo giorno del mese.<br/><br/>Se **frequenza** è troppo**giorno**, e **stile** è troppo**EndOfInterval**, hello sezione viene prodotta nell'ultima ora del giorno hello hello.<br/><br/>Se **frequenza** è troppo**ora**, e **stile** è troppo**EndOfInterval**, hello sezione viene prodotta alla fine hello ora hello. Ad esempio, per una sezione per hello periodo 1 PM - 2 PM, sezione di hello viene prodotta alle 14.00. |No |EndOfInterval |
| anchorDateTime |Definisce una posizione assoluta di hello in utilizzata dai limiti di intervallo di hello dell'utilità di pianificazione toocompute set di dati. <br/><br/>Si noti che se questo propoerty ha parti di date più granulari di hello specificato frequenza, hello parti più granulari verranno ignorate. Ad esempio, se hello **intervallo** è **oraria** (frequenza: ora e intervallo: 1), hello e **anchorDateTime** contiene **minuti e secondi**, quindi hello minuti e secondi parti di **anchorDateTime** vengono ignorati. |No |01/01/0001 |
| offset |Intervallo di tempo da cui hello iniziale e finale di tutte le sezioni di set di dati vengono spostati. <br/><br/>Si noti che se entrambi **anchorDateTime** e **offset** viene specificato, il risultato di hello MAIUSC hello combinato. |No |ND |

### <a name="offset-example"></a>Esempio di offset
Per impostazione predefinita, le sezioni giornaliere (`"frequency": "Day", "interval": 1`) iniziano alle 00.00 (mezzanotte) UTC (Coordinated Universal Time). Se si desidera hello inizio ora toobe 6: 00 UTC ora invece, impostare hello offset come illustrato nel seguente frammento di codice hello: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Esempio di anchorDateTime
Nell'esempio seguente di hello, hello set di dati viene prodotta una volta ogni 23 ore. Hello prima sezione viene avviato in hello momento specificato dal **anchorDateTime**, questo valore è impostato troppo`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Esempio di offset/style
Hello seguente set di dati è mensile e viene prodotta hello 3 ° di ogni mese alle ore 8:00 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>Criteri di set di dati
Hello **criteri** sezione nella definizione di set di dati hello definisce i criteri di hello o condizione hello hello sezioni di set di dati è necessario soddisfare.

### <a name="validation-policies"></a>Criteri di convalida
| Nome criterio | Descrizione | Troppo applicato| Obbligatorio | Default |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Convalida i dati di hello **archiviazione Blob di Azure** hello di soddisfa i requisiti di dimensioni minime (in megabyte). |Archivio BLOB di Azure |No |ND |
| minimumRows |Convalida i dati di hello un **database SQL di Azure** o **tabella Azure** contiene hello numero minimo di righe. |<ul><li>Database SQL di Azure</li><li>Tabella di Azure</li></ul> |No |ND |

#### <a name="examples"></a>esempi
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>Set di dati esterni
Set di dati esterni sono quelli che non sono state prodotte da una pipeline in esecuzione in data factory di hello hello. Se il set di dati hello è contrassegnato come **esterno**, hello **ExternalData** criteri possono essere definiti tooinfluence hello comportamento di disponibilità di sezione hello set di dati.

A meno che non sia generato da Data Factory, il set di dati deve essere contrassegnato come **external**. Questa impostazione si applica in genere input toohello della prima attività in una pipeline, a meno che l'attività o il concatenamento della pipeline in uso.

| Nome | Descrizione | Obbligatorio | Valore predefinito |
| --- | --- | --- | --- |
| dataDelay |tempo di Hello hello toodelay verificare hello disponibilità di dati esterni di hello per hello assegnato sezione. Ad esempio, è possibile ritardare un controllo orario usando questa impostazione.<br/><br/>Hello impostazione si applica solo toohello ora corrente.  Ad esempio, se è 1:00 PM subito e questo valore è 10 minuti, convalida hello inizia alle ore 1:10.<br/><br/>Si noti che questa impostazione non influisce sulle sezioni in hello precedente. Le sezioni con **Slice End Time** + **dataDelay** < **Now** vengono elaborate senza alcun ritardo.<br/><br/>Volte maggiore di 23:59 ore devono essere specificate tramite hello `day.hours:minutes:seconds` formato. Ad esempio, toospecify 24 ore, non utilizzare 24:00:00. Usare invece 1.00:00:00. Il valore 24:00:00 viene considerato 24 giorni (24.00:00:00). Per 1 giorno e 4 ore, specificare 1:04:00:00. |No |0 |
| retryInterval |tempo di attesa Hello tra un tentativo successivo di errore e hello. Questa impostazione si applica ora toopresent. Se non è riuscita, provare precedente hello successivo tentativo di hello è dopo hello **retryInterval** periodo. <br/><br/>Se è 1:00 PM al momento, iniziamo hello primo tentativo. Se hello durata toocomplete hello primo controllo di convalida è 1 minuto e operazione hello non riuscita, tentativo successivo di hello è 1:00 + 1 min (durata) + 1 minuto (intervallo tra tentativi) = 1:02 PM. <br/><br/>Per le sezioni hello precedente, non si verifica alcun ritardo. Riprova Hello si verifica immediatamente. |No |00:01:00 (1 minute) |
| retryTimeout |timeout di Hello per ogni nuovo tentativo.<br/><br/>Se questa proprietà è impostata too10 minuti, la convalida di hello deve essere completata entro 10 minuti. Se impiega più tempo rispetto alla convalida hello tooperform di 10 minuti, hello ripetere verifica il timeout.<br/><br/>Se tutti i tentativi per timeout convalida hello hello sezione è contrassegnata come **TimedOut**. |No |00:10:00 (10 minutes) |
| maximumRetry |Hello numero di volte in cui toocheck per la disponibilità di dati esterni hello hello. Hello valore massimo consentito è 10. |No |3 |


## <a name="create-datasets"></a>Creare set di dati
È possibile creare set di dati usando uno di questi strumenti o SDK: 

- Copia guidata 
- Portale di Azure
- Visual Studio
- PowerShell
- Modello di Azure Resource Manager
- API REST
- API .NET

Hello seguenti esercitazioni per istruzioni dettagliate per la creazione di pipeline e set di dati utilizzando uno di questi strumenti o il SDK, vedere:
 
- [Creare una pipeline con un'attività di trasformazione dati](data-factory-build-your-first-pipeline.md)
- [Creare una pipeline con un'attività di spostamento dati](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Dopo una pipeline viene creata e distribuita, è possibile gestire e monitorare le pipeline utilizzando hello pannelli portali Azure o un'app di gestione e monitoraggio hello. Hello seguenti argomenti per informazioni dettagliate, vedere: 

- [Monitorare e gestire le pipeline di Azure Data Factory con il portale di Azure e PowerShell](data-factory-monitor-manage-pipelines.md)
- [Monitorare e gestire le pipeline con hello monitoraggio e gestione delle app](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Set di dati con ambito
È possibile creare set di dati con ambito tooa pipeline utilizzando hello **set di dati** proprietà. Questi set di dati possono essere usati solo dalle attività all'interno di questa pipeline, non da quelle in altre pipeline. Hello di esempio seguente definisce una pipeline con due set di dati (InputDataset rdc e OutputDataset rdc) toobe utilizzati all'interno della pipeline hello.  

> [!IMPORTANT]
> Set di dati con ambito sono supportati solo con le pipeline monouso (dove **pipelineMode** è troppo**OneTime**). Per i dettagli vedere [Pipeline monouso](data-factory-create-pipelines.md#onetime-pipeline) .
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulle pipeline, vedere [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md). 
- Per altre informazioni sulle modalità di pianificazione ed esecuzione delle pipeline, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md). 
