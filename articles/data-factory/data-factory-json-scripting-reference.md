---
title: aaaAzure Data Factory - riferimento agli script JSON | Documenti Microsoft
description: "Questo articolo fornisce gli schemi JSON per le entità di Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - Informazioni di riferimento sugli script JSON
Questo articolo fornisce gli schemi JSON ed esempi per la definizione di entità di Azure Data Factory (pipeline, attività, set di dati e servizi collegati).  

## <a name="pipeline"></a>Pipeline 
struttura di alto livello per una definizione di pipeline Hello è come segue: 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Nella tabella seguente vengono descritte le proprietà di hello all'interno della pipeline hello definizione JSON:

| Proprietà | Descrizione | Obbligatorio
-------- | ----------- | --------
| name | Nome della pipeline hello. Specificare un nome che rappresenta l'azione di hello che hello attività o pipeline è toodo configurato<br/><ul><li>Numero massimo di caratteri: 260</li><li>Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</li><li>Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</li></ul> |Sì |
| description |Testo che descrive le attività hello o una pipeline viene utilizzata per | No |
| attività | Contiene un elenco di attività. | Sì |
| start |Data-ora di inizio per la pipeline di hello. Devono essere nel [formato ISO](http://en.wikipedia.org/wiki/ISO_8601), ad esempio: 2014-10-14T16:32:41. <br/><br/>È possibile toospecify un'ora locale, ad esempio un'ora EST. Di seguito è fornito l'esempio `2016-02-27T06:00:00**-05:00`, che indica le 6 EST.<br/><br/>Hello proprietà start ed end insieme specificano il periodo attivo per la pipeline di hello. Le sezioni di output vengono generate solo in questo periodo attivo. |No<br/><br/>Se si specifica un valore per la proprietà di fine hello, è necessario specificare una valore per la proprietà di avvio hello.<br/><br/>Hello ora di inizio e fine può essere entrambi vuoti toocreate una pipeline. È necessario specificare entrambi i valori tooset un periodo attivo per hello pipeline toorun. Se non si specifica l'ora di inizio e fine durante la creazione di una pipeline, è possibile impostare utilizzando il cmdlet Set-AzureRmDataFactoryPipelineActivePeriod hello in un secondo momento. |
| end |Data-ora di fine per la pipeline di hello. Se specificate, devono essere in formato ISO. Ad esempio: 2014-10-14T17:32:41 <br/><br/>È possibile toospecify un'ora locale, ad esempio un'ora EST. Di seguito è fornito l'esempio `2016-02-27T06:00:00**-05:00`, che indica le 6 EST.<br/><br/>pipeline hello toorun specificare in modo indefinito, 9999-09-09 come valore di hello per la proprietà di fine hello. |No <br/><br/>Se si specifica un valore per la proprietà di avvio hello, è necessario specificare una valore per la proprietà di fine hello.<br/><br/>Vedere le note per hello **avviare** proprietà. |
| isPaused |Se set tootrue hello pipeline non viene eseguito. Valore predefinito = false. È possibile utilizzare questa proprietà tooenable o disabilitare. |No |
| pipelineMode |metodo Hello per la pianificazione viene eseguita per la pipeline di hello. I valori consentiti sono scheduled (predefinito) e onetime.<br/><br/>'Pianificata' indica che pipeline hello viene eseguita in un intervallo di tempo specificato in base tooits periodo attivo (ora di inizio e fine). 'Unica' indica che pipeline hello viene eseguito una sola volta. Al momento, dopo aver creato una pipeline monouso non è possibile modificarla o aggiornarla. Per informazioni dettagliate sull'impostazione onetime, vedere la sezione [Pipeline monouso](data-factory-create-pipelines.md#onetime-pipeline) . |No |
| expirationTime |Periodo di tempo dopo la creazione per i quali hello pipeline sia valido e deve rimanere disponibile. Se non è attiva qualsiasi, non è riuscita, o in attesa di esecuzione, la pipeline di hello viene eliminata automaticamente una volta raggiunta l'ora di scadenza hello. |No |


## <a name="activity"></a>Attività 
struttura di alto livello Hello per un'attività all'interno di una definizione di pipeline (elemento di attività) è il seguente:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

Seguente tabella vengono descritti proprietà hello all'interno di attività hello definizione JSON:

| Tag | Descrizione | Obbligatorio |
| --- | --- | --- |
| name |Nome dell'attività hello. Specificare un nome che rappresenta l'azione di hello che attività hello è configurato toodo<br/><ul><li>Numero massimo di caratteri: 260</li><li>Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</li><li>Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</li></ul> |Sì |
| description |Testo che descrive le attività di hello viene utilizzato per. |Sì |
| type |Specifica il tipo di hello di attività hello. Vedere hello [archivi dati](#data-stores) e [le attività di trasformazione dati](#data-transformation-activities) sezioni per diversi tipi di attività. |Sì |
| inputs |Tabelle di input utilizzate dall'attività hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Sì |
| outputs |Tabelle di output utilizzate dall'attività hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Sì |
| linkedServiceName |Nome del servizio hello collegato usato dall'attività hello. <br/><br/>Un'attività potrebbe essere necessario specificare il servizio collegato hello che collega l'ambiente di calcolo necessarie toohello. |Sì per attività di HDInsight, attività di Azure Machine Learning e attività delle stored procedure. <br/><br/>No per tutto il resto |
| typeProperties |Le proprietà nella sezione typeProperties hello dipendono dal tipo di attività hello. |No |
| policy |Criteri che influiscono sul comportamento di hello in fase di esecuzione dell'attività hello. Se vengono omessi, vengono usati i criteri predefiniti. |No |
| scheduler |proprietà "utilità di pianificazione" è utilizzato toodefine desiderato pianificazione per l'attività hello. Le sottoproprietà sono hello stesso hello quelle nella hello [proprietà disponibilità in un set di dati](data-factory-create-datasets.md#dataset-availability). |No |

### <a name="policies"></a>Criteri
Criteri influiscono sul comportamento di hello in fase di esecuzione di un'attività, in particolare quando viene elaborata la sezione hello di una tabella. Hello nella tabella seguente fornisce dettagli hello.

| Proprietà | Valori consentiti | Valore predefinito | Descrizione |
| --- | --- | --- | --- |
| Concorrenza |Integer  <br/><br/>Valore massimo: 10 |1 |Numero di esecuzioni simultanee dell'attività hello.<br/><br/>Determina il numero di hello di esecuzioni di attività parallele che possono verificarsi in sezioni diverse. Ad esempio, se un'attività deve toogo tramite un ampio set di dati disponibili, un valore maggiore di concorrenza di velocizzare l'elaborazione dati hello. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Determina hello ordinamento delle sezioni di dati che vengono elaborate.<br/><br/>Ad esempio nel caso in cui si abbiano 2 sezioni, una alle 16.00 e l'altra alle 17.00, ed entrambe siano in attesa di esecuzione. Se si imposta executionPriorityOrder di hello toobe NewestFirst, slice hello 17: 00 viene elaborata per prima. Allo stesso modo se si imposta executionPriorityORder di hello toobe OldestFIrst, viene elaborato sezione hello 4 ore. |
| retry |Integer <br/><br/>Valore massimo: 10 |0 |Numero di tentativi prima dell'elaborazione dei dati di hello per sezione hello è contrassegnato come errore. Esecuzione di attività per una sezione di dati viene ripetuta backup toohello specificato numero di tentativi. Riprova Hello viene eseguito appena possibile dopo l'errore hello. |
| timeout |TimeSpan |00:00:00 |Timeout per l'attività hello. Esempio: 00:10:00 (implica un timeout di 10 minuti)<br/><br/>Se un valore viene omesso o è 0, hello timeout è infinito.<br/><br/>Se il tempo di elaborazione di dati hello in una sezione supera il valore di timeout di hello, viene annullata e sistema hello tenta l'elaborazione di hello tooretry. numero di tentativi di Hello dipende dalla proprietà retry hello. Quando si verifica il timeout, hello stato tooTimedOut. |
| delay |TimeSpan |00:00:00 |Specificare il ritardo di hello prima dell'elaborazione di dati di hello sezione inizia.<br/><br/>esecuzione di Hello dell'attività per una sezione di dati viene avviata dopo hello ritardo passato hello previsto tempo di esecuzione.<br/><br/>Esempio: 00:10:00 (implica un ritardo di 10 minuti) |
| longRetry |Integer <br/><br/>Valore massimo: 10 |1 |numero di Hello di long tentativi prima dell'esecuzione della sezione hello è non è riuscito.<br/><br/>I tentativi longRetry sono distanziati da longRetryInterval. Pertanto, se è necessario toospecify un intervallo tra tentativi, usare quindi longRetry. Se vengono specificati Retry e longRetry, ogni tentativo longRetry include nuovi tentativi e numero massimo di tentativi di hello è Riprova * longRetry.<br/><br/>Ad esempio, se si dispone delle seguenti impostazioni in criteri attività hello hello:<br/>Retry: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Si supponga che sia presente solo una sezione tooexecute (lo stato è in attesa) e l'esecuzione dell'attività hello ha esito negativo di ogni volta. All’inizio vi saranno tre tentativi di esecuzione consecutivi. Dopo ogni tentativo, lo stato della sezione hello sarà Retry. Dopo aver innanzitutto 3 tentativi di failover, lo stato della sezione hello sarebbe LongRetry.<br/><br/>Dopo un'ora (vale a dire il valore di longRetryInteval), verrà eseguita un'altra serie di 3 tentativi di esecuzione consecutivi. Successivamente, lo stato della sezione hello sarà Failed e non più necessario tentativi. Quindi, sono stati eseguiti 6 tentativi.<br/><br/>Se qualsiasi esecuzione ha esito positivo, lo stato della sezione hello sarà Ready e non più tentativi.<br/><br/>longRetry possono essere utilizzati in situazioni in cui dipendenti dati arrivano a volte non deterministica o hello ambiente generale non è affidabile in cui l'elaborazione dei dati si verifica. In questi casi, potrebbe non aiutare eseguire tentativi uno dopo l'altro e in questo modo, dopo un intervallo di risultati in fase di hello desiderato output.<br/><br/>Attenzione: non impostare valori elevati per longRetry o longRetryInterval. In genere, valori più elevati comportano altri problemi sistemici. |
| longRetryInterval |TimeSpan |00:00:00 |ritardo Hello tra nuovi tentativi lunghi |

### <a name="typeproperties-section"></a>sezione typeProperties
sezione typeProperties Hello è diverso per ogni attività. Le attività di trasformazione dispongono solo le proprietà del tipo hello. Vedere la sezione [Attività di trasformazione dei dati](#data-transformation-activities) in questo articolo per esempi JSON che definiscono le attività di trasformazione in una pipeline. 

**Attività di copia** contiene due sottosezioni nella sezione typeProperties hello: **origine** e **sink**. Vedere [archivi dati](#data-stores) sezione in questo articolo per esempi che mostrano come toouse dati memorizzati come origine e/o un sink di JSON. 

### <a name="sample-copy-pipeline"></a>Esempio di una pipeline di copia
In hello seguente della pipeline di esempio, un'attività di tipo è **copia** in hello **attività** sezione. In questo esempio, hello [attività di copia](data-factory-data-movement-activities.md) copia i dati da un database di SQL Azure tooan di archiviazione Blob di Azure. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Si noti hello seguenti punti:

* Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**.
* Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**.
* In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello.

Vedere [archivi dati](#data-stores) sezione in questo articolo per esempi che mostrano come toouse dati memorizzati come origine e/o un sink di JSON.    

Per una descrizione completa della creazione di questa pipeline, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Esempio di una pipeline di trasformazione
In hello seguente della pipeline di esempio, un'attività di tipo è **HDInsightHive** in hello **attività** sezione. In questo esempio, hello [attività Hive di HDInsight](data-factory-hive-activity.md) Trasforma i dati da un archivio Blob di Azure eseguendo un file di script Hive in un cluster Azure HDInsight Hadoop. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Si noti hello seguenti punti: 

* Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**HDInsightHive**.
* file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **AzureStorageLinkedService**) e in  **script** cartella nel contenitore hello **adfgetstarted**.
* Hello **definisce** sezione è le impostazioni di runtime hello toospecify utilizzati script hive toohello passati come valori di configurazione di Hive (ad esempio `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Vedere la sezione [Attività di trasformazione dei dati](#data-transformation-activities) in questo articolo per esempi JSON che definiscono le attività di trasformazione in una pipeline.

Per una descrizione completa della creazione di questa pipeline, vedere [esercitazione: creare i primi dati tooprocess pipeline utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Servizio collegato
struttura di alto livello per una definizione di servizio collegato Hello è come segue:

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Seguente tabella vengono descritti proprietà hello all'interno di attività hello definizione JSON:

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- | 
| name | Nome del servizio collegato hello. | Sì | 
| proprietà - tipo | Tipo di servizio collegato hello. Ad esempio: archiviazione di Azure, database SQL di Azure. |
| typeProperties | sezione typeProperties Hello dispone degli elementi che sono diverse per ogni archivio dati o l'ambiente di calcolo. Vedere [archivi dati](#datastores) sezione per tutti i dati di hello servizi collegati dell'archivio e [calcolo ambienti](#compute-environments) per hello tutti i servizi collegati di calcolo |   

## <a name="dataset"></a>Set di dati 
Un set di dati in Azure Data Factory viene definito come segue:

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
| name | Nome del set di dati hello. Per le regole di denominazione, vedere [Azure Data Factory: regole di denominazione](data-factory-naming-rules.md) . |Sì |ND |
| type | tipo di set di dati hello. Specificare uno dei tipi di hello supportati da Data Factory di Azure (ad esempio: AzureBlob, AzureSqlTable). Vedere [archivi dati](#data-stores) sezione per tutti hello archivi dati e i tipi di set di dati supportati da Data Factory. | 
| structure | Schema di set di dati hello. Contiene le colonne, i tipi e così via. | No |ND |
| typeProperties | Le proprietà corrispondenti toohello tipo selezionato. Vedere la sezione [Archivi dati](#data-stores) per i tipi supportati e le rispettive proprietà. |Sì |ND |
| external | Valore booleano flag toospecify se un set di dati generata in modo esplicito tramite una pipeline di factory di dati o non. |No |false |
| disponibilità | Definisce l'elaborazione di finestra o sezionamento modello per la produzione di set di dati hello hello hello. Per informazioni dettagliate sul set di dati hello sezionamento modello, vedere [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) articolo. |Sì |ND |
| policy |Definisce i criteri di hello o condizione hello che devono soddisfare le sezioni di hello set di dati. <br/><br/>Per informazioni dettagliate, vedere la sezione [Criteri di set di dati](#Policy) . |No |ND |

Ogni colonna hello **struttura** sezione contiene hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| name |Nome della colonna hello. |Sì |
| type |Tipo di dati della colonna hello.  |No |
| culture |Impostazioni cultura toobe utilizzato quando il tipo specificato e il tipo .NET basato su .NET `Datetime` o `Datetimeoffset`. Il valore predefinito è `en-us`. |No |
| format |Formato stringa toobe utilizzato quando il tipo specificato e il tipo .NET `Datetime` o `Datetimeoffset`. |No |

Nell'esempio seguente di hello, set di dati hello ha tre colonne `slicetimestamp`, `projectname`, e `pageviews` e sono di tipo: String, String e decimali rispettivamente.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Hello nella tabella seguente vengono descritte le proprietà è possibile utilizzare in hello **disponibilità** sezione:

| Proprietà | Descrizione | Obbligatorio | Default |
| --- | --- | --- | --- |
| frequency |Specifica l'unità di tempo hello per la produzione di sezione set di dati.<br/><br/><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese |Sì |ND |
| interval |Specifica un moltiplicatore per la frequenza.<br/><br/>"Intervallo di frequenza x" determina la frequenza con cui hello sezione viene prodotta.<br/><br/>Se è necessario hello toobe dataset sezionati su base oraria, impostare <b>frequenza</b> troppo<b>ora</b>, e <b>intervallo</b> troppo<b>1</b>.<br/><br/><b>Nota</b>: se si specifica Frequency come Minute, si consiglia di impostare hello intervallo toono inferiore a 15 |Sì |ND |
| style |Specifica se la sezione hello deve essere prodotta all'hello inizio/fine dell'intervallo "hello".<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Se Frequency è impostato tooMonth e style è impostato tooEndOfInterval, hello sezione viene prodotta hello ultimo giorno del mese. Se lo stile di hello è impostato tooStartOfInterval, hello sezione viene prodotta hello primo giorno del mese.<br/><br/>Se Frequency è impostato tooDay e style è impostato tooEndOfInterval, sezione hello viene prodotta nell'ultima ora del giorno hello hello.<br/><br/>Se Frequency è impostato tooHour e style è impostato tooEndOfInterval, sezione hello viene prodotta alla fine hello ora hello. Ad esempio, per una sezione per periodo 1 PM – 2 PM, sezione di hello viene prodotta alle 14.00. |No |EndOfInterval |
| anchorDateTime |Definisce una posizione assoluta di hello in utilizzata dai limiti di sezione dell'utilità di pianificazione toocompute set di dati. <br/><br/><b>Nota</b>: se hello AnchorDateTime ha parti di date più granulari frequenza hello in hello parti più granulari verranno ignorate. <br/><br/>Ad esempio, se hello <b>intervallo</b> è <b>oraria</b> (frequenza: ora e intervallo: 1) e hello <b>AnchorDateTime</b> contiene <b>minuti e secondi</b>quindi hello <b>minuti e secondi</b> parti di hello AnchorDateTime verranno ignorate. |No |01/01/0001 |
| offset |Intervallo di tempo da cui hello iniziale e finale di tutte le sezioni di set di dati vengono spostati. <br/><br/><b>Nota</b>: se vengono specificati sia anchorDateTime che offset, il risultato di hello è MAIUSC hello combinato. |No |ND |

Hello seguente sezione di disponibilità specifica il set di dati di output di hello è creati ogni ora (o) input set di dati è disponibile ogni ora:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Hello **criteri** sezione nella definizione di set di dati definisce i criteri di hello o condizione hello hello sezioni di set di dati è necessario soddisfare.

| Nome criterio | Descrizione | Troppo applicato| Obbligatorio | Default |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Convalida i dati di hello un **blob di Azure** hello di soddisfa i requisiti di dimensioni minime (in megabyte). |BLOB Azure |No |ND |
| minimumRows |Convalida i dati di hello un **database SQL di Azure** o **tabella Azure** contiene hello numero minimo di righe. |<ul><li>Database SQL di Azure</li><li>tabella di Azure</li></ul> |No |ND |

**Esempio:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

A meno che un set di dati non sia generato da Azure Data Factory, deve essere contrassegnato come **external**. Questa impostazione si applica in genere input toohello della prima attività in una pipeline, a meno che l'attività o il concatenamento della pipeline in uso.

| Nome | Descrizione | Obbligatorio | Default Value |
| --- | --- | --- | --- |
| dataDelay |Tempo toodelay hello controllo disponibilità hello di dati esterni di hello di hello dato sezione. Ad esempio, se hello i dati sono disponibili ogni ora, hello controllo toosee hello i dati esterni sono disponibili e la sezione corrispondente di hello sia Ready può essere posticipato utilizzando dataDelay.<br/><br/>Si applica solo toohello ora corrente.  Ad esempio, se è 1:00 PM subito e questo valore è 10 minuti, convalida hello inizia alle ore 1:10.<br/><br/>Questa impostazione influisce sulle sezioni in hello precedente (sezioni con ora di fine sezione + dataDelay < ora) vengono elaborati senza alcun ritardo.<br/><br/>Periodo di tempo maggiore di 23:59 ore necessario toospecified utilizzando hello `day.hours:minutes:seconds` formato. Ad esempio, toospecify 24 ore, non utilizzare 24:00:00; Utilizzare invece 1.00:00:00. Il valore 24:00:00 viene considerato 24 giorni (24.00:00:00). Per 1 giorno e 4 ore, specificare 1:04:00:00. |No |0 |
| retryInterval |tempo di attesa Hello tra un errore e hello successivo tentativo. Se un tentativo non riesce, il successivo tentativo di hello è dopo retryInterval. <br/><br/>Se è 1:00 PM al momento, iniziamo hello primo tentativo. Se hello durata toocomplete hello primo controllo di convalida è 1 minuto e operazione hello non riuscita, tentativo successivo di hello è 1:00 + 1 min (durata) + 1 minuto (intervallo tra tentativi) = 1:02 PM. <br/><br/>Per le sezioni hello precedente, non si verifica alcun ritardo. Riprova Hello si verifica immediatamente. |No |00:01:00 (1 minute) |
| retryTimeout |timeout di Hello per ogni nuovo tentativo.<br/><br/>Se questa proprietà è impostata too10 minuti, hello toobe esigenze convalida completata entro 10 minuti. Se impiega più tempo rispetto alla convalida hello tooperform di 10 minuti, hello ripetere verifica il timeout.<br/><br/>Se tutti i tentativi per la convalida di hello scade, sezione hello è contrassegnata come TimedOut. |No |00:10:00 (10 minutes) |
| maximumRetry |Numero di volte in cui toocheck per la disponibilità di dati esterni hello hello. Hello consentito valore massimo è 10. |No |3 |


## <a name="data-stores"></a>Archivi dati
Hello [servizio collegato](#linked-service) descrizioni sezione forniti per gli elementi JSON che sono tipi di servizi collegati tooall comuni. Questa sezione vengono fornite informazioni dettagliate sugli elementi JSON che sono l'archivio dati tooeach specifico.

Hello [Dataset](#dataset) descrizioni sezione forniti per gli elementi JSON che sono tipi di set di dati tooall comuni. Questa sezione vengono fornite informazioni dettagliate sugli elementi JSON che sono l'archivio dati tooeach specifico.

Hello [attività](#activity) descrizioni sezione forniti per gli elementi JSON che sono tipi tooall comuni di attività. Questa sezione vengono fornite informazioni dettagliate sugli elementi JSON che sono l'archivio dati specifico tooeach quando viene utilizzata come origine/sink in un'attività di copia.  

Fare clic sul collegamento hello per archivio hello si è interessati negli schemi JSON hello toosee per il servizio collegato, set di dati e hello origine/sink per attività di copia hello.

| Categoria | Archivio dati 
|:--- |:--- |
| **Azure** |[Archivio BLOB di Azure](#azure-blob-storage) |
| &nbsp; |[Archivio Data Lake di Azure](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Database SQL di Azure](#azure-sql-database) |
| &nbsp; |[Azure SQL Data Warehouse](#azure-sql-data-warehouse) |
| &nbsp; |[Ricerca di Azure](#azure-search) |
| &nbsp; |[Archivio tabelle di Azure](#azure-table-storage) |
| **Database** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **File** |[Amazon S3](#amazon-s3) |
| &nbsp; |[File system](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Altro** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Tabella Web](#web-table) |

## <a name="azure-blob-storage"></a>Archiviazione BLOB di Azure

### <a name="linked-service"></a>Servizio collegato
Esistono due tipi di servizi collegati: servizio collegato di Archiviazione di Azure e servizio collegato di firma di accesso condiviso Archiviazione di Azure.

#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
toolink la data factory tooa account di archiviazione di Azure tramite hello **chiave dell'account**, creare un servizio collegato di archiviazione di Azure. il set hello servizio collegato di toodefine una risorsa di archiviazione di Azure **tipo** di hello servizio collegato troppo**AzureStorage**. Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| connectionString |Specificare le informazioni necessarie tooconnect tooAzure archiviazione per la proprietà connectionString hello. |Sì |

##### <a name="example"></a>Esempio  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a>Servizio collegato di firma di accesso condiviso Archiviazione di Azure
servizio sa di archiviazione di Azure collegati Hello consente toolink un Account di archiviazione Azure tooan data factory di Azure tramite una firma di accesso condiviso (SAS). Fornisce data factory di hello con accesso limitato/scadenza tooall/specifiche risorse (blob/contenitore) nell'archiviazione hello. toolink la data factory tooa account di archiviazione di Azure tramite la firma di accesso condiviso, creare un servizio sa di archiviazione di Azure collegati. il servizio hello set toodefine un SAS di archiviazione di Azure collegato **tipo** di hello servizio collegato troppo**AzureStorageSas**. Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:   

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| sasUri |Specificare le risorse di archiviazione di Azure toohello URI firma di accesso condiviso, ad esempio una tabella, contenitore o blob. |Sì |

##### <a name="example"></a>Esempio

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione BLOB di Azure](data-factory-azure-blob-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati Blob di Azure, hello set **tipo** del set di dati hello troppo**AzureBlob**. Quindi, specificare le proprietà specifiche di Blob di Azure in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Percorso toohello contenitore e della cartella nell'archiviazione blob hello. Esempio: myblobcontainer\myblobfolder\ |Sì |
| fileName |Nome del blob hello. fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.<br/><br/>Se si specifica un nome di file, hello attività (incluso copia) funziona su hello Blob specifico.<br/><br/>Quando non è stato specificato il nome del file, copia include tutti i BLOB in folderPath hello per input set di dati.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: dati. <Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| partitionedBy |partitionedBy è una proprietà facoltativa. È possibile utilizzare è toospecify un dinamica folderPath e filename per dati della serie temporale. Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

#### <a name="example"></a>Esempio

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


Per altre informazioni, vedere [Connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="blobsource-in-copy-activity"></a>BlobSource in attività di copia
Se si copiano dati da un archivio Blob di Azure, impostare hello **tipo di origine** di hello attività di copia troppo**BlobSource**e specificare le seguenti proprietà in hello * * origine * * sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello. |True (valore predefinito), False |No |

#### <a name="example-blobsource"></a>Esempio: BlobSource**
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>BlobSink in attività di copia
Se si copiano dati tooan archiviazione Blob di Azure, impostare hello **tipo di sink** di hello attività di copia troppo**BlobSink**e specificare le seguenti proprietà in hello **sink** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| copyBehavior |Definisce il comportamento di copia hello quando origine hello è BlobSource o file System. |<b>PreserveHierarchy</b>: mantiene hello gerarchia del file nella cartella di destinazione hello. percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.<br/><br/><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello presenti hello primo livelli della cartella di destinazione. i file di destinazione Hello hanno nome generato automaticamente. <br/><br/><b>Oggetto (impostazione predefinita):</b> unisce tutti i file dal file tooone cartella di origine hello. Se viene specificato il nome di File/Blob hello, il nome di file sottoposto a merge hello sarebbe nome specificato hello. in caso contrario, potrebbe essere il nome file generato automaticamente. |No |

#### <a name="example-blobsink"></a>Esempio: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore BLOB di Azure](data-factory-azure-blob-connector.md#copy-activity-properties). 

## <a name="azure-data-lake-store"></a>Archivio Azure Data Lake

### <a name="linked-service"></a>Servizio collegato
un servizio collegato archivio Azure Data Lake toodefine, imposta il tipo di hello hello servizio collegato troppo**AzureDataLakeStore**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type | proprietà di tipo Hello deve essere impostata su: **AzureDataLakeStore** | Sì |
| dataLakeStoreUri | Specificare le informazioni su hello account archivio Azure Data Lake. È presente nel seguente formato hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`. | Sì |
| subscriptionId | Sottoscrizione di Azure toowhich Id archivio Data Lake appartiene. | Richiesto per il sink |
| resourceGroupName | Toowhich di nome gruppo di risorse di Azure archivio Data Lake appartiene. | Richiesto per il sink |
| servicePrincipalId | Specificare un ID client. dell'applicazione hello | Sì (per l'autenticazione di un'entità servizio) |
| servicePrincipalKey | Specificare la chiave dell'applicazione hello. | Sì (per l'autenticazione di un'entità servizio) |
| tenant | Specificare le informazioni di hello tenant (dominio tenant o nome ID) in cui risiede l'applicazione. È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure. | Sì (per l'autenticazione di un'entità servizio) |
| autorizzazione | Fare clic su **Authorize** pulsante hello **Editor delle Data Factory** e immettere le credenziali dell'utente che assegna hello autogenerati autorizzazione URL toothis proprietà. | Sì (per l'autenticazione basata su credenziali utente)|
| sessionId | Id di sessione OAuth della sessione di autorizzazione OAuth hello. Ogni ID di sessione è univoco e può essere usato solo una volta. Questa impostazione viene generata automaticamente quando si usa l'editor di Data Factory. | Sì (per l'autenticazione basata su credenziali utente) |

#### <a name="example-using-service-principal-authentication"></a>Esempio: uso dell'autenticazione basata su entità servizio
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Esempio: uso dell'autenticazione basata su credenziali utente
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di archivio Azure Data Lake, hello set **tipo** del set di dati hello troppo**AzureDataLakeStore**e specificare le proprietà in hello seguenti hello **typeProperties**sezione: 

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| folderPath |Percorso toohello contenitore e della cartella in hello Azure Data Lake archiviare. |Sì |
| fileName |Nome del file hello nell'archivio Azure Data Lake hello. fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole. <br/><br/>Se si specifica un nome di file, attività hello (inclusi copia) funziona su file specifiche hello.<br/><br/>Quando non è stato specificato il nome del file, copia include tutti i file in folderPath hello per input set di dati.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: dati. <Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| partitionedBy |partitionedBy è una proprietà facoltativa. È possibile utilizzare è toospecify un dinamica folderPath e filename per dati della serie temporale. Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

#### <a name="example"></a>Esempio
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties). 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Origine Azure Data Lake Store in attività di copia
Se si copiano dati da un archivio Azure Data Lake, impostare hello **tipo di origine** di hello attività di copia troppo**AzureDataLakeStoreSource**e specificare le seguenti proprietà in hello **origine**  sezione:

**AzureDataLakeStoreSource** supporta le proprietà seguenti hello **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello. |True (valore predefinito), False |No |

#### <a name="example-azuredatalakestoresource"></a>Esempio: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Sink Azure Data Lake Store in attività di copia
Se si copia un archivio dati tooan Azure Data Lake, impostare hello **tipo di sink** di hello attività di copia troppo**AzureDataLakeStoreSink**e specificare le seguenti proprietà in hello **sink**sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| copyBehavior |Specifica il comportamento di copia hello. |<b>PreserveHierarchy</b>: mantiene hello gerarchia del file nella cartella di destinazione hello. percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.<br/><br/><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello della cartella di destinazione. file di destinazione Hello vengono creati con il nome generato automaticamente.<br/><br/><b>Oggetto</b>: unisce tutti i file dal file tooone cartella di origine hello. Se viene specificato il nome di File/Blob hello, il nome di file sottoposto a merge hello sarebbe nome specificato hello. in caso contrario, potrebbe essere il nome file generato automaticamente. |No |

#### <a name="example-azuredatalakestoresink"></a>Esempio: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties). 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine un database di Azure Cosmos collegato **tipo** di hello servizio collegato troppo**DocumentDb**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| **Proprietà** | **Descrizione** | **Obbligatorio** |
| --- | --- | --- |
| connectionString |Specificare le informazioni necessarie tooconnect tooAzure DB Cosmos database. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati di Azure Cosmos DB hello set **tipo** del set di dati hello troppo**DocumentDbCollection**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| **Proprietà** | **Descrizione** | **Obbligatorio** |
| --- | --- | --- |
| collectionName |Nome della raccolta di Azure Cosmos DB hello. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Origine della raccolta Azure Cosmos DB in attività di copia
Se si copiano dati da un database di Azure Cosmos, impostare hello **tipo di origine** di hello attività di copia troppo**DocumentDbCollectionSource**e specificare le seguenti proprietà in hello **origine** sezione:


| **Proprietà** | **Descrizione** | **Valori consentiti** | **Obbligatorio** |
| --- | --- | --- | --- |
| query |Specificare i dati di tooread query hello. |Stringa di query supportata da Azure Cosmos DB. <br/><br/>Esempio: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |No <br/><br/>Se non specificato, hello istruzione SQL eseguita:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Carattere speciale tooindicate che hello documento nidificato |Qualsiasi carattere. <br/><br/>Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate. Data Factory di Azure consente gerarchia toodenote utente tramite nestingSeparator, ovvero "." in hello esempi sopra riportati. Con il separatore di hello, attività di copia hello genererà l'oggetto "Name" hello con elementi tre figli prima, intermedio e ultimo, in base too"Name.First", "Name.Middle" e "." in hello "Cognome" definizione di tabella. |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Sink della raccolta Azure Cosmos DB in attività di copia
Se si copiano dati tooAzure DB Cosmos, impostare hello **tipo di sink** di hello attività di copia troppo**DocumentDbCollectionSink**e specificare le seguenti proprietà in hello **sink**sezione:

| **Proprietà** | **Descrizione** | **Valori consentiti** | **Obbligatorio** |
| --- | --- | --- | --- |
| nestingSeparator |È necessario un carattere speciale nel hello origine colonna nome tooindicate annidati di documento. <br/><br/>Ad esempio sopra: `Name.First` nell'output di hello tabella produce hello seguente struttura JSON nel documento Cosmos DB hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Carattere usato tooseparate livelli di annidamento.<br/><br/>Il valore predefinito è `.` (punto). |Carattere usato tooseparate livelli di annidamento. <br/><br/>Il valore predefinito è `.` (punto). |
| writeBatchSize |Numero parallelo di richieste di documenti di toocreate tooAzure DB Cosmos del servizio.<br/><br/>È possibile ottimizzare le prestazioni di hello quando si copiano dati da e verso Azure Cosmos DB usando questa proprietà. È possibile prevedere prestazioni migliori quando si aumenta viene raggiunto writeBatchSize poiché vengono inviate altre richieste in parallelo tooAzure DB Cosmos. Tuttavia, occorre tooavoid la limitazione delle richieste che possono generare il messaggio di errore hello: "Richiesta frequenza è grande".<br/><br/>La limitazione è dovuta a diversi fattori, inclusi la dimensione dei documenti, il numero di termini nei documenti, i criteri di indicizzazione della raccolta di destinazione, ecc. Per le operazioni di copia, è possibile utilizzare un migliore hello toohave raccolta (ad esempio, S3) la maggior parte delle velocità effettiva disponibile (2.500 richiesta unità al secondo). |Integer |No (valore predefinito: 5) |
| writeBatchTimeout |Tempo di attesa per hello operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Per altre informazioni, vedere l'articolo [Connettore Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).

## <a name="azure-sql-database"></a>Database SQL di Azure

### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un Database di SQL Azure **tipo** di hello servizio collegato troppo**AzureSqlDatabase**e specificare le seguenti proprietà in hello **typeProperties**sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| connectionString |Specificare l'istanza del Database di SQL Azure toohello tooconnect necessarie informazioni per la proprietà connectionString hello. |Sì |

#### <a name="example"></a>Esempio
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di Database SQL di Azure, hello set **tipo** del set di dati hello troppo**AzureSqlTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello o della vista nell'istanza di Database SQL di Azure hello che il servizio collegato fa riferimento a. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Origine SQL nell'attività di copia
Se si copiano dati da un Database SQL di Azure, impostare hello **tipo di origine** di hello attività di copia troppo**SqlSource**e specificare le seguenti proprietà in hello **origine** sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Esempio: `select * from MyTable`. |No |
| sqlReaderStoredProcedureName |Nome di hello stored procedure che legge i dati dalla tabella di origine hello. |Nome di hello stored procedure. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Sink SQL nell'attività di copia
Se si copiano dati tooAzure Database SQL, impostare hello **tipo di sink** di hello attività di copia troppo**SqlSink**e specificare le seguenti proprietà in hello **sink** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |
| writeBatchSize |Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| sqlWriterCleanupScript |Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. |Istruzione di query. |No |
| sliceIdentifierColumnName |Specificare un nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo. |Nome di colonna di una colonna con tipo di dati binario (32). |No |
| sqlWriterStoredProcedureName |Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello. |Nome di hello stored procedure. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |
| sqlWriterTableType |Specificare un toobe nome tipo di tabella utilizzati in hello stored procedure. Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati. Codice della stored procedure può unire dati hello copiati con i dati esistenti. |Nome del tipo di tabella. |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties). 

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine un Data Warehouse di SQL Azure collegato **tipo** di hello servizio collegato troppo**AzureSqlDW**e specificare le seguenti proprietà in hello **typeProperties**sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| connectionString |Specificare l'istanza di Azure SQL Data Warehouse toohello tooconnect necessarie informazioni per la proprietà connectionString hello. |Sì |



#### <a name="example"></a>Esempio

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di Azure SQL Data Warehouse, hello set **tipo** del set di dati hello troppo**AzureSqlDWTable**e specificare le proprietà in hello seguenti hello **typeProperties**sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello o della vista nel database di Azure SQL Data Warehouse hello che hello servizio collegato fa riferimento a. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties). 

### <a name="sql-dw-source-in-copy-activity"></a>Origine SQL DW nell'attività di copia
Se si copiano dati da Azure SQL Data Warehouse, impostare hello **tipo di origine** di hello attività di copia troppo**SqlDWSource**e specificare le seguenti proprietà in hello **origine**sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable`. |No |
| sqlReaderStoredProcedureName |Nome di hello stored procedure che legge i dati dalla tabella di origine hello. |Nome di hello stored procedure. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

### <a name="sql-dw-sink-in-copy-activity"></a>Sink SQL DW nell'attività di copia
Se si copiano dati tooAzure SQL Data Warehouse, impostare hello **tipo di sink** di hello attività di copia troppo**SqlDWSink**e specificare le seguenti proprietà in hello **sink** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. |Istruzione di query. |No |
| allowPolyBase |Indica se toouse PolyBase (se applicabile) anziché meccanismo BULKINSERT. <br/><br/> **Utilizzo di PolyBase è hello consigliato dei dati tooload in SQL Data Warehouse.** |True  <br/>False (impostazione predefinita) |No |
| polyBaseSettings |Un gruppo di proprietà che possono essere specificati quando hello **allowPolybase** impostata troppo**true**. |&nbsp; |No |
| rejectValue |Specifica il numero di hello o la percentuale di righe che può essere rifiutata prima di hello query ha esito negativo. <br/><br/>Informazioni su ulteriori informazioni su del PolyBase hello rifiutare le opzioni di hello **argomenti** sezione [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) argomento. |0 (impostazione predefinita), 1, 2, … |No |
| rejectType |Specifica se l'opzione rejectValue hello è specificato come valore letterale o percentuale. |Value (impostazione predefinita), Percentage |No |
| rejectSampleValue |Determina il numero di hello di tooretrieve righe prima di hello PolyBase Ricalcola percentuale hello di righe rifiutate. |1, 2, … |Sì se **rejectType** è **percentage** |
| useTypeDefault |Specifica la modalità toohandle mancano i valori nel file di testo delimitati quando PolyBase recupera i dati da file di testo hello.<br/><br/>Altre informazioni su questa proprietà dalla sezione argomenti hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (valore predefinito) |No |
| writeBatchSize |Inserisce i dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

## <a name="azure-search"></a>Ricerca di Azure

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine una ricerca di Azure collegato **tipo** di hello servizio collegato troppo**AzureSearch**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| URL | URL per il servizio di ricerca di Azure hello. | Sì |
| key | Chiave di amministrazione per hello del servizio di ricerca di Azure. | Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati di ricerca di Azure, hello set **tipo** del set di dati hello troppo**AzureSearchIndex**e specificare le proprietà in hello seguenti hello **typeProperties** sezione : 

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| type | proprietà di tipo Hello deve essere impostata troppo**AzureSearchIndex**.| Sì |
| indexName | Nome dell'indice di ricerca di Azure hello. Data Factory di creare l'indice di hello. indice di Hello deve esistere in ricerca di Azure. | Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#dataset-properties).

### <a name="azure-search-index-sink-in-copy-activity"></a>Sink Indice di Ricerca di Azure in attività di copia
Se si sta copiando l'indice di ricerca di Azure tooan dati, impostare hello **tipo di sink** di hello attività di copia troppo**AzureSearchIndexSink**e specificare le seguenti proprietà in hello **sink**sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Specifica se toomerge o Sostituisci quando un documento già presente nell'indice hello. | Merge (impostazione predefinita)<br/>Carica| No |
| WriteBatchSize | Carica i dati nell'indice di ricerca di Azure hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. | 1 too1, 000. Il valore predefinito è 1000. | No |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Ricerca di Azure](data-factory-azure-search-connector.md#copy-activity-properties).

## <a name="azure-table-storage"></a>Archiviazione tabelle di Azure

### <a name="linked-service"></a>Servizio collegato
Esistono due tipi di servizi collegati: servizio collegato di Archiviazione di Azure e servizio collegato di firma di accesso condiviso Archiviazione di Azure.

#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
toolink la data factory tooa account di archiviazione di Azure tramite hello **chiave dell'account**, creare un servizio collegato di archiviazione di Azure. il set hello servizio collegato di toodefine una risorsa di archiviazione di Azure **tipo** di hello servizio collegato troppo**AzureStorage**. Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |proprietà di tipo Hello deve essere impostata su: **AzureStorage** |Sì |
| connectionString |Specificare le informazioni necessarie tooconnect tooAzure archiviazione per la proprietà connectionString hello. |Sì |

**Esempio:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a>Servizio collegato di firma di accesso condiviso Archiviazione di Azure
servizio sa di archiviazione di Azure collegati Hello consente toolink un Account di archiviazione Azure tooan data factory di Azure tramite una firma di accesso condiviso (SAS). Fornisce data factory di hello con accesso limitato/scadenza tooall/specifiche risorse (blob/contenitore) nell'archiviazione hello. toolink la data factory tooa account di archiviazione di Azure tramite la firma di accesso condiviso, creare un servizio sa di archiviazione di Azure collegati. il servizio hello set toodefine un SAS di archiviazione di Azure collegato **tipo** di hello servizio collegato troppo**AzureStorageSas**. Quindi, è possibile specificare le seguenti proprietà in hello **typeProperties** sezione:   

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |proprietà di tipo Hello deve essere impostata su: **AzureStorageSas** |Sì |
| sasUri |Specificare le risorse di archiviazione di Azure toohello URI firma di accesso condiviso, ad esempio una tabella, contenitore o blob. |Sì |

**Esempio:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di tabelle di Azure, hello set **tipo** del set di dati hello troppo**AzureTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nell'istanza di Database della tabella di Azure hello che il servizio collegato fa riferimento a. |Sì. Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione. Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato. |

#### <a name="example"></a>Esempio

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#dataset-properties). 

### <a name="azure-table-source-in-copy-activity"></a>Origine Tabella di Azure nell'attività di copia
Se si copiano dati da Archiviazione tabelle di Azure, impostare hello **tipo di origine** di hello attività di copia troppo**AzureTableSource**e specificare le seguenti proprietà in hello **origine**sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query della tabella di Azure. Vedere gli esempi nella sezione successiva hello. |No. Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione. Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato. |
| azureTableSourceIgnoreTableNotFound |Indica se ignorare hello eccezione della tabella non esiste. |TRUE<br/>FALSE |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#copy-activity-properties). 

### <a name="azure-table-sink-in-copy-activity"></a>Sink Tabella di Azure nell'attività di copia
Se si copiano dati tooAzure archiviazione tabelle, impostare hello **tipo di sink** di hello attività di copia troppo**AzureTableSink**e specificare le seguenti proprietà in hello **sink** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Partizione chiave valore predefinito che può essere usato dal sink hello. |Valore stringa. |No |
| azureTablePartitionKeyName |Nome della colonna hello i cui valori vengono utilizzati come chiavi di partizione. Se non specificato, AzureTableDefaultPartitionKeyValue viene utilizzato come chiave di partizione hello. |Nome colonna. |No |
| azureTableRowKeyName |Nome della colonna hello i cui valori di colonna vengono utilizzati come chiave di riga. Se non specificato, usare un GUID per ogni riga. |Nome colonna. |No |
| azureTableInsertType |Hello modalità tooinsert i dati in tabelle di Azure.<br/><br/>Questa proprietà controlla se le righe esistenti nella tabella di output di hello con le chiavi di riga e di partizione corrispondenti hanno valori di sostituzione o unione. <br/><br/>toolearn sul funzionano di queste impostazioni (merge e la sostituzione), vedere [Insert o l'entità di tipo Merge](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [Insert o sostituire entità](https://msdn.microsoft.com/library/azure/hh452242.aspx) argomenti. <br/><br> Questa impostazione si applica a livello di riga hello, non a livello tabella hello, e nessuna delle due opzioni consente di eliminare le righe nella tabella di output di hello che non esistono nell'input hello. |merge (impostazione predefinita)<br/>replace |No |
| writeBatchSize |Inserisce dati nella tabella di Azure hello quando hello di viene raggiunto writeBatchSize o writeBatchTimeout. |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| writeBatchTimeout |Inserisce i dati in tabelle di Azure hello quando viene raggiunto writeBatchSize hello o writeBatchTimeout |Intervallo di tempo<br/><br/>Ad esempio: "00:20:00" (20 minuti) |No (valore di timeout predefinito del client predefinito toostorage 90 secondi) |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Per altre informazioni sui servizi collegati, vedere [Connettore Archiviazione tabelle di Azure](data-factory-azure-table-connector.md#copy-activity-properties). 

## <a name="amazon-redshift"></a>Amazon Redshift

### <a name="linked-service"></a>Servizio collegato
toodefine un Amazon Redshift collegato del servizio, hello set **tipo** di hello servizio collegato troppo**AmazonRedshift**e specificare le seguenti proprietà in hello **typeProperties**sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| server |IP il nome host o indirizzo del server di Amazon Redshift hello. |Sì |
| port |numero di Hello di porta TCP hello hello server Amazon Redshift utilizza toolisten per le connessioni client. |No, valore predefinito: 5439 |
| database |Nome del database Amazon Redshift hello. |Sì |
| username |Nome dell'utente che dispone di accesso toohello database. |Sì |
| password |Password dell'account utente di hello. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di Amazon Redshift set hello **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello hello Amazon Redshift in database in cui il servizio collegato fa riferimento a. |No (se la **query** di **RelationalSource** è specificata) |


#### <a name="example"></a>Esempio

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia 
Se si copiano dati da Amazon Redshift, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable`. |No (se **tableName** di **set di dati** è specificato) |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Per altre informazioni, vedere [Connettore Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un IBM DB2 **tipo** di hello servizio collegato troppo**OnPremisesDB2**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| server |Nome del server DB2 hello. |Sì |
| database |Nome del database DB2 hello. |Sì |
| schema |Nome dello schema hello nel database di hello. nome dello schema Hello è tra maiuscole e minuscole. |No |
| authenticationType |Tipo di autenticazione usato tooconnect toohello DB2 database. I valori possibili sono: anonima, di base e Windows. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione di base o Windows. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve usare database di DB2 tooconnect toohello locale. |Sì |

#### <a name="example"></a>Esempio
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
set di dati toodefine un DB2, set hello **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nell'istanza di Database DB2 hello che il servizio collegato fa riferimento a. tableName Hello è tra maiuscole e minuscole. |No (se la **query** di **RelationalSource** è specificata) 

#### <a name="example"></a>Esempio
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da IBM DB2, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `"query": "select * from "MySchema"."MyTable""`. |No (se **tableName** di **set di dati** è specificato) |

#### <a name="example"></a>Esempio
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Per altre informazioni, vedere [Connettore IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine MySQL collegato **tipo** di hello servizio collegato troppo**OnPremisesMySql**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| server |Nome del server MySQL hello. |Sì |
| database |Nome del database MySQL hello. |Sì |
| schema |Nome dello schema hello nel database di hello. |No |
| authenticationType |Tipo di autenticazione usato toohello tooconnect di database MySQL. I valori possibili sono:`Basic`. |Sì |
| username |Specificare i database di MySQL toohello tooconnect nome utente. |Sì |
| password |Specificare la password per l'account utente di hello specificato. |Sì |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve utilizzare database MySQL di tooconnect toohello locale. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di MySQL, hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nell'istanza di MySQL Database che fa riferimento il servizio collegato a hello. |No (se la **query** di **RelationalSource** è specificata) |

#### <a name="example"></a>Esempio

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da un database MySQL, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable`. |No (se **tableName** di **set di dati** è specificato) |


#### <a name="example"></a>Esempio
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties). 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine Oracle collegato **tipo** di hello servizio collegato troppo**OnPremisesOracle**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| driverType | Specificare i dati del driver toouse toocopy da / tooOracle Database. I valori consentiti sono **Microsoft** o **ODP** (impostazione predefinita). Per informazioni dettagliate sui driver, vedere la sezione [Versione e installazione supportate](#supported-versions-and-installation). | No |
| connectionString | Specificare l'istanza di Oracle Database toohello tooconnect necessarie informazioni per la proprietà connectionString hello. | Sì |
| gatewayName | Nome del gateway hello che viene utilizzato tooconnect toohello server Oracle locale |Sì |

#### <a name="example"></a>Esempio
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati Oracle, hello set **tipo** del set di dati hello troppo**OracleTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nel Database Oracle per il servizio collegato di hello hello fa riferimento a. |No, se **oracleReaderQuery** di **OracleSource** è specificato |

#### <a name="example"></a>Esempio

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).

### <a name="oracle-source-in-copy-activity"></a>Origine Oracle nell'attività di copia
Se si copiano dati da un database Oracle, impostare hello **tipo di origine** di hello attività di copia troppo**OracleSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| oracleReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable` <br/><br/>Se non specificato, hello istruzione SQL eseguita:`select * from MyTable` |No (se **tableName** di **set di dati** è specificato) |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

### <a name="oracle-sink-in-copy-activity"></a>Sink Oracle nell'attività di copia
Se si copia database Oracle tooam di dati, impostare hello **tipo di sink** di hello attività di copia troppo**OracleSink**e specificare le seguenti proprietà in hello **sink** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |
| writeBatchSize |Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. |Numero intero (numero di righe) |No (valore predefinito: 100) |
| sqlWriterCleanupScript |Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. |Istruzione di query. |No |
| sliceIdentifierColumnName |Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo. |Nome di colonna di una colonna con tipo di dati binario (32). |No |

#### <a name="example"></a>Esempio
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Per altre informazioni, vedere [Connettore Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Servizio collegato
toodefine un PostgreSQL collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesPostgreSql**e specificare le seguenti proprietà in hello **typeProperties**sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| server |Nome del server PostgreSQL hello. |Sì |
| database |Nome del database PostgreSQL hello. |Sì |
| schema |Nome dello schema hello nel database di hello. nome dello schema Hello è tra maiuscole e minuscole. |No |
| authenticationType |Tipo di autenticazione usato tooconnect toohello PostgreSQL database. I valori possibili sono: anonima, di base e Windows. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione di base o Windows. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve utilizzare database PostgreSQL locale di tooconnect toohello. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati, PostgreSQL hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello in hello istanza PostgreSQL Database riferito al servizio collegato. tableName Hello è tra maiuscole e minuscole. |No (se la **query** di **RelationalSource** è specificata) |

#### <a name="example"></a>Esempio
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da un database PostgreSQL, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: "query": "select * from \"Schema\".\"Tabella\"". |No (se **tableName** di **set di dati** è specificato) |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un SAP Business Warehouse (BW) **tipo** di hello servizio collegato troppo**SapBw**e specificare le seguenti proprietà in hello **typeProperties**sezione:  

Proprietà | Descrizione | Valori consentiti | Obbligatoria
-------- | ----------- | -------------- | --------
server | Nome del server di hello in SAP BW che hello si trova l'istanza. | string | Sì
systemNumber | Numero di sistema di hello sistema SAP BW. | Numero decimale a due cifre rappresentato come stringa. | Sì
clientId | ID client di client hello in hello sistema SAP W. | Numero decimale a tre cifre rappresentato come stringa. | Sì
username | Nome dell'utente di hello con server di accesso toohello SAP | string | Sì
password | Password utente hello. | string | Sì
gatewayName | Nome del gateway hello hello servizio Data Factory deve utilizzare l'istanza di SAP BW tooconnect toohello locale. | string | Sì
encryptedCredential | stringa di credenziale crittografato Hello. | string | No

#### <a name="example"></a>Esempio

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati SAP BW, hello set **tipo** del set di dati hello troppo**RelationalTable**. Non esistono proprietà specifiche del tipo supportato per il set di dati di hello SAP BW di tipo **RelationalTable**.  

#### <a name="example"></a>Esempio

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da SAP Business Warehouse, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query | Specifica i dati di tooread query MDX hello dall'istanza di SAP BW hello. | Query MDX. | Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties). 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un SAP HANA **tipo** di hello servizio collegato troppo**SapHana**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

Proprietà | Descrizione | Valori consentiti | Obbligatoria
-------- | ----------- | -------------- | --------
server | Nome del server di hello in SAP HANA quali hello si trova l'istanza. Se il server usa una porta personalizzata, specificare `server:port`. | string | Sì
authenticationType | Tipo di autenticazione. | string. "Basic" o "Windows" | Sì 
username | Nome dell'utente di hello con server di accesso toohello SAP | string | Sì
password | Password utente hello. | string | Sì
gatewayName | Nome del gateway hello hello servizio Data Factory deve utilizzare l'istanza di SAP HANA tooconnect toohello locale. | string | Sì
encryptedCredential | stringa di credenziale crittografato Hello. | string | No

#### <a name="example"></a>Esempio

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).
 
### <a name="dataset"></a>Set di dati
toodefine un set di dati SAP HANA, hello set **tipo** del set di dati hello troppo**RelationalTable**. Non esistono proprietà specifiche del tipo supportato per i set di dati SAP HANA hello di tipo **RelationalTable**. 

#### <a name="example"></a>Esempio

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da un archivio dati SAP HANA, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query | Specifica i dati di tooread query SQL hello dall'istanza di SAP HANA hello. | Query SQL. | Sì |


#### <a name="example"></a>Esempio


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>Servizio collegato
Creare un servizio collegato di tipo **OnPremisesSqlServer** toolink una data factory tooa di on-premise SQL Server database. Hello nella tabella seguente fornisce una descrizione del servizio collegato SQL Server locale tooon specifici elementi JSON.

Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooSQL servizio del Server collegato.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OnPremisesSqlServer**. |Sì |
| connectionString |Specificare le informazioni connectionString necessarie tooconnect database di SQL Server on-premise toohello utilizzando l'autenticazione di SQL Server o l'autenticazione di Windows. |Sì |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve utilizzare i database di SQL Server on-premise toohello tooconnect. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione Windows. Esempio: **nomedominio\\nomeutente**. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |

È possibile crittografare le credenziali utilizzando hello **New AzureRmDataFactoryEncryptValue** cmdlet e utilizzarli nella stringa di connessione hello, come illustrato nell'esempio seguente hello (**EncryptedCredential** proprietà):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Esempio: JSON per l'uso dell'autenticazione SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Esempio: JSON per l'uso dell'autenticazione Windows

Se vengono specificati nome utente e password, gateway li utilizza hello tooimpersonate database di SQL Server on-premise toohello tooconnect account utente specificato. In caso contrario, gateway si connetta toohello SQL Server direttamente con il contesto di sicurezza hello del Gateway (il relativo account di avvio).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di SQL Server, hello set **tipo** del set di dati hello troppo**SqlServerTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello o della vista nell'istanza di Database di SQL Server hello che il servizio collegato fa riferimento a. |Sì |

#### <a name="example"></a>Esempio
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Origine SQL nell'attività di copia
Se si copiano dati da un database di SQL Server, impostare hello **tipo di origine** di hello attività di copia troppo**SqlSource**e specificare le seguenti proprietà in hello **origine** sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable`. Può fare riferimento a più tabelle dal database hello hello di un set di dati dell'input a cui fa riferimento. Se non specificato, hello istruzione SQL eseguita: select from MyTable. |No |
| sqlReaderStoredProcedureName |Nome di hello stored procedure che legge i dati dalla tabella di origine hello. |Nome di hello stored procedure. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |

Se hello **sqlReaderQuery** specificato per hello SqlSource, hello attività di copia viene eseguita questa query hello Database di SQL Server tooget hello dati.

In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).

Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.

> [!NOTE]
> Quando si utilizza **sqlReaderStoredProcedureName**, è comunque necessario toospecify un valore per hello **tableName** proprietà hello set di dati JSON. Non sono disponibili convalide eseguite su questa tabella.


#### <a name="example"></a>Esempio
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

In questo esempio, **sqlReaderQuery** specificato per hello SqlSource. Attività di copia Hello consente di eseguire questa query hello dati hello tooget origine di Database di SQL Server. In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri). Hello sqlReaderQuery può fare riferimento a più tabelle all'interno del database hello hello di un set di dati dell'input a cui fa riferimento. Non è limitato tooonly hello tabella impostata come hello typeProperty tableName del set di dati.

Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.

Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Sink SQL nell'attività di copia
Se si desidera copiare i database di SQL Server tooa di dati, impostare hello **tipo di sink** di hello attività di copia troppo**SqlSink**e specificare le seguenti proprietà in hello **sink** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |
| writeBatchSize |Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| sqlWriterCleanupScript |Specificare query per l'attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. Per altre informazioni, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy) . |Istruzione di query. |No |
| sliceIdentifierColumnName |Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo. Per altre informazioni, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy) . |Nome di colonna di una colonna con tipo di dati binario (32). |No |
| sqlWriterStoredProcedureName |Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello. |Nome di hello stored procedure. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |
| sqlWriterTableType |Specificare toobe nome tipo di tabella utilizzati in hello stored procedure. Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati. Codice della stored procedure può unire dati hello copiati con i dati esistenti. |Nome del tipo di tabella. |No |

#### <a name="example"></a>Esempio
pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Servizio collegato
toodefine un Sybase collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesSybase**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| server |Nome del server di Sybase hello. |Sì |
| database |Nome del database di Sybase hello. |Sì |
| schema |Nome dello schema hello nel database di hello. |No |
| authenticationType |Tipo di autenticazione usato tooconnect toohello database di Sybase. I valori possibili sono: anonima, di base e Windows. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione di base o Windows. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve usare database di Sybase tooconnect toohello locale. |Sì |

#### <a name="example"></a>Esempio
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati, Sybase hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello in hello istanza del Database di Sybase riferito al servizio collegato. |No (se la **query** di **RelationalSource** è specificata) |

#### <a name="example"></a>Esempio

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da un database di Sybase, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable`. |No (se **tableName** di **set di dati** è specificato) |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine un Teradata collegato **tipo** di hello servizio collegato troppo**OnPremisesTeradata**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| server |Nome del server Teradata hello. |Sì |
| authenticationType |Tipo di autenticazione usato tooconnect toohello Teradata database. I valori possibili sono: anonima, di base e Windows. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione di base o Windows. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve usare database di Teradata tooconnect toohello locale. |Sì |

#### <a name="example"></a>Esempio
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati Teradata Blob hello set **tipo** del set di dati hello troppo**RelationalTable**. Non sono attualmente presenti proprietà del tipo non supportato per i set di dati Teradata hello. 

#### <a name="example"></a>Esempio
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da un database Teradata, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine**sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable`. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Per altre informazioni, vedere [Connettore Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Servizio collegato
toodefine un Cassandra collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesCassandra**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| host |Uno o più indirizzi IP o nomi host di server Cassandra.<br/><br/>Specificare un elenco delimitato da virgole di indirizzi IP o host nomi tooconnect tooall server contemporaneamente. |Sì |
| port |la porta TCP che hello server Cassandra Hello utilizza toolisten per le connessioni client. |No, valore predefinito: 9042 |
| authenticationType |Di base o anonima |Sì |
| username |Specificare nome utente per l'account utente di hello. |Sì, se authenticationType impostata tooBasic. |
| password |Specificare la password per l'account utente di hello. |Sì, se authenticationType impostata tooBasic. |
| gatewayName |nome Hello del gateway hello tooconnect utilizzati toohello Cassandra database locale. |Sì |
| encryptedCredential |Credenziali crittografate dal gateway hello. |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati Cassandra hello set **tipo** del set di dati hello troppo**CassandraTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| keyspace |Nome di schema nel database Cassandra o di spazio delle chiavi hello. |Sì, se **query** per **CassandraSource** non è definito. |
| tableName |Nome della tabella hello Cassandra database. |Sì, se **query** per **CassandraSource** non è definito. |

#### <a name="example"></a>Esempio

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties). 

### <a name="cassandra-source-in-copy-activity"></a>Origine Cassandra nell'attività di copia
Se si copiano dati da Cassandra, impostare hello **tipo di origine** di hello attività di copia troppo**CassandraSource**e specificare le seguenti proprietà in hello **origine** sezione :

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Query SQL-92 o query CQL. Vedere il [riferimento a CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Quando si utilizza una query SQL, specificare **spazio delle chiavi name.table nome** toorepresent hello tabella tooquery. |No (se tableName e keyspace sul set di dati sono definiti). |
| consistencyLevel |livello di coerenza Hello specifica il numero di repliche deve rispondere tooa richiesta di lettura prima della restituzione dell'applicazione client toohello di dati. Controlli Cassandra hello specificato numero di repliche per hello toosatisfy dati richiesta di lettura. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Per informazioni dettagliate, vedere [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configurazione della coerenza dei dati). |No. Il valore predefinito è ONE. |

#### <a name="example"></a>Esempio
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Servizio collegato
toodefine un MongoDB collegato del servizio, hello set **tipo** di hello servizio collegato troppo**OnPremisesMongoDB**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| server |IP il nome host o indirizzo del server di MongoDB hello. |Sì |
| port |La porta TCP che hello MongoDB server utilizza toolisten per le connessioni client. |Facoltativo, valore predefinito: 27017 |
| authenticationType |Di base o anonima. |Sì |
| username |Utente account tooaccess MongoDB. |Sì (se si usa l'autenticazione di base). |
| password |Password utente hello. |Sì (se si usa l'autenticazione di base). |
| authSource |Nome del database MongoDB hello che si desidera toouse toocheck le credenziali per l'autenticazione. |Facoltativo (se si usa l'autenticazione di base). impostazione predefinita: Usa l'account amministratore hello e database hello specificato utilizzando la proprietà databaseName. |
| databaseName |Nome del database MongoDB hello che si desidera tooaccess. |Sì |
| gatewayName |Nome del gateway hello che accede a hello archivio di dati. |Sì |
| encryptedCredential |Credenziali crittografate in base al gateway. |Facoltativo |

#### <a name="example"></a>Esempio

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati, MongoDB hello set **tipo** del set di dati hello troppo**MongoDbCollection**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| collectionName |Nome dell'insieme di hello nel database di MongoDB. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).

#### <a name="mongodb-source-in-copy-activity"></a>Origine MongoDB nell'attività di copia
Se si copiano dati da MongoDB, impostare hello **tipo di origine** di hello attività di copia troppo**MongoDbSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL-92. Ad esempio: `select * from MyTable`. |No, se **collectionName** di **set di dati** è specificato |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Servizio collegato
toodefine un S3 Amazon collegato del servizio, hello set **tipo** di hello servizio collegato troppo**AwsAccessKey**e specificare le seguenti proprietà in hello **typeProperties** sezione :  

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| accessKeyID |ID della chiave di accesso privata hello. |string |Sì |
| secretAccessKey |chiave di accesso per i segreti Hello stessa. |La stringa segreta crittografata |Sì |

#### <a name="example"></a>Esempio
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
set di dati toodefine un S3 Amazon, hello set **tipo** del set di dati hello troppo**AmazonS3**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| bucketName |nome di bucket Hello S3. |String |Sì |
| key |chiave dell'oggetto Hello S3. |String |No |
| prefix |Prefisso per la chiave dell'oggetto hello S3. Vengono selezionati gli oggetti le cui chiavi iniziano con questo prefisso. Si applica solo quando la chiave è vuota. |string |No |
| version |versione di Hello dell'oggetto S3 se è abilitato il controllo delle versioni S3. |String |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No | |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. livelli di Hello supportato sono: **ottimale** e **Fastest**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No | |


> [!NOTE]
> bucketName + tasto specifica il percorso di hello dell'oggetto hello S3 in bucket è il contenitore radice hello per gli oggetti S3 e la chiave è oggetto di tooS3 hello percorso completo.

#### <a name="example-sample-dataset-with-prefix"></a>Esempio: set di dati di esempio con prefisso

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>Esempio: set di dati di esempio con versione

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>Esempio: percorsi dinamici per S3
Nell'esempio hello, utilizziamo valori fissi per le proprietà di chiave e bucketName nel set di dati hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

È possibile avere Data Factory di calcolare la chiave di hello e bucketName dinamicamente in fase di esecuzione tramite variabili di sistema, ad esempio SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

È possibile eseguire stesso hello per le proprietà prefix hello di un set di dati di Amazon S3. Per un elenco delle funzioni e delle variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .

Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origine File System nell'attività di copia
Se si copiano dati da S3 Amazon, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione :


| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Specifica se l'elenco toorecursively S3 oggetti nella directory hello. |true/false |No |


#### <a name="example"></a>Esempio


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>File system


### <a name="linked-service"></a>Servizio collegato
È possibile collegare una locale file system tooan data factory di Azure con hello **Server File locale** servizio collegato. Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON toohello specifico servizio locale di File Server collegato.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |Verificare che la proprietà di tipo hello sia impostata troppo**OnPremisesFileServer**. |Sì |
| host |Specifica il percorso radice hello della cartella hello che si desidera toocopy. Utilizzare il carattere di escape hello ' \ ' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) . |Sì |
| userid |Specificare ID utente hello con server di accesso toohello hello. |No (se si sceglie encryptedCredential) |
| password |Specificare la password hello per utente hello (userid). |No (se si sceglie encryptedCredential) |
| encryptedCredential |Specificare le credenziali crittografato hello che è possibile ottenere eseguendo il cmdlet New-AzureRmDataFactoryEncryptValue hello. |No (se si sceglie toospecify userid e password in testo normale) |
| gatewayName |Specifica il nome di hello del gateway hello che Data Factory deve usare tooconnect toohello ai file server locali. |Sì |

#### <a name="sample-folder-path-definitions"></a>Definizioni del percorso della cartella di esempio 
| Scenario | Host nella definizione del servizio collegato | folderPath nella definizione del set di dati |
| --- | --- | --- |
| Cartella locale nel computer del gateway di gestione dati:  <br/><br/>Esempi: D:\\\* o D:\cartella\sottocartella\\* |D:\\\\ (per Gateway di gestione dati versione 2.0 e successive) <br/><br/> localhost (per le versioni precedenti alla versione 2.0 di Gateway di gestione dati) |.\\\\ o cartella\\\\sottocartella (per Gateway di gestione dati 2.0 e versioni successive) <br/><br/>D:\\\\ o D:\\\\cartella\\\\sottocartella (per la versione del gateway precedente a 2.0) |
| Cartella condivisa remota:  <br/><br/>Esempi: \\\\myserver\\share\\\* o \\\\myserver\\share\\cartella\\sottocartella\\* |\\\\\\\\myserver\\\\share |.\\\\ o cartella\\\\sottocartella |


#### <a name="example-using-username-and-password-in-plain-text"></a>Esempio: Uso di nome utente e password in testo normale

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Esempio: Uso di encryptedcredential

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati di File System, hello set **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Specifica hello sottopercorso toohello cartella. Utilizzare il carattere di escape hello ' \' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora. |Sì |
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato è in hello seguente formato: <br/><br/>`Data.<Guid>.txt` Esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file. <br/><br/>I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).<br/><br/>Esempio 1: "fileFilter": "*. log"<br/>Esempio 2: "fileFilter": 2016-1-?.txt"<br/><br/>Si noti che fileFilter è applicabile per un set di dati di input FileShare. |No |
| partitionedBy |È possibile utilizzare partitionedBy toospecify dinamica folderPath/nome di file per i dati delle serie temporali. Un esempio è folderPath con parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Optimal** (Ottimale) **Fastest** (Più veloce). vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> Non è possibile usare fileName e fileFilter contemporaneamente.

#### <a name="example"></a>Esempio

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origine File System nell'attività di copia
Se si siano copiando i dati dal File System, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello. |True, False (valore predefinito) |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>Sink File System nell'attività di copia
Se si copiano dati tooFile sistema, impostare hello **tipo di sink** di hello attività di copia troppo**FileSystemSink**e specificare le seguenti proprietà in hello **sink** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| copyBehavior |Definisce il comportamento di copia hello quando origine hello è BlobSource o file System. |**PreserveHierarchy:** mantiene la gerarchia di file hello nella cartella di destinazione hello. Percorso relativo di hello hello origine toohello origine della cartella dei file, ovvero è hello come percorso relativo di hello hello file toohello destinazione della cartella di destinazione.<br/><br/>**FlattenHierarchy:** tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello della cartella di destinazione. file di destinazione Hello vengono creati con un nome generato automaticamente.<br/><br/>**Oggetto:** unisce tutti i file dal file tooone cartella di origine hello. Se viene specificato nome di nome/blob file hello, nome di file uniti hello è nome specificato hello. In caso contrario, verrà usato un nome file generato automaticamente. |No |
auto-

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore File System](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un FTP **tipo** di hello servizio collegato troppo**server FTP**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio | Default |
| --- | --- | --- | --- |
| host |Nome o indirizzo IP del FTP Server hello |Sì |&nbsp; |
| authenticationType |Specificare il tipo di autenticazione |Sì |Di base, anonimo |
| username |Utente che dispone di server di accesso FTP toohello |No |&nbsp; |
| password |Password per l'utente di hello (nomeutente) |No |&nbsp; |
| encryptedCredential |Server FTP di credenziali crittografate tooaccess hello |No |&nbsp; |
| gatewayName |Nome di hello Gateway di gestione dati gateway tooconnect tooan locale server FTP |No |&nbsp; |
| port |Porta su cui hello FTP è in attesa server |No |21 |
| enableSsl |Specificare se toouse FTP attraverso il canale SSL/TLS |No |true |
| enableServerCertificateValidation |Specificare se il server tooenable SSL la convalida del certificato quando si utilizza FTP su canale SSL/TLS. |No |true |

#### <a name="example-using-anonymous-authentication"></a>Esempio: uso dell'autenticazione anonima

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Esempio: uso di nome utente e password in testo normale per l'autenticazione di base

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Esempio: uso di porta, enableSsl, enableServerCertificateValidation

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Esempio: uso di encryptedCredential per autenticazione e gateway

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
set di dati toodefine un FTP, hello set **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Toohello sottocartella percorso. Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora. |Sì 
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: <br/><br/>Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.<br/><br/>I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).<br/><br/>Esempi 1: `"fileFilter": "*.log"`<br/>Esempio 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter è applicabile per un set di dati di input FileShare. Questa proprietà non è supportata con HDFS. |No |
| partitionedBy |partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale. Ad esempio, folderPath con parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Optimal** (Ottimale) **Fastest** (Più veloce). Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Specificare se usare la modalità di trasferimento binario. True per la modalità binaria e false per ASCII. Valore predefinito: True. Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer. |No |

> [!NOTE]
> filename e fileFilter non possono essere usati contemporaneamente.

#### <a name="example"></a>Esempio

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origine File System nell'attività di copia
Se si copiano dati da un server FTP, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello. |True, False (valore predefinito) |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore FTP](data-factory-ftp-connector.md#copy-activity-properties).


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un HDFS **tipo** di hello servizio collegato troppo**Hdfs**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **Hdfs** |Sì |
| Url |URL toohello HDFS |Sì |
| authenticationType |Anonima o Windows. <br><br> toouse **l'autenticazione Kerberos** per connettore HDFS, fare riferimento troppo[in questa sezione](#use-kerberos-authentication-for-hdfs-connector) tooset l'ambiente locale di conseguenza. |Sì |
| userName |Nome utente per l'autenticazione di Windows |Sì (per l'autenticazione di Windows) |
| password |Password per l'autenticazione di Windows |Sì (per l'autenticazione di Windows) |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve usare tooconnect toohello HDFS. |Sì |
| encryptedCredential |[Nuovo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output delle credenziali di accesso hello. |No |

#### <a name="example-using-anonymous-authentication"></a>Esempio: uso dell'autenticazione anonima

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Esempio: uso dell'autenticazione Windows

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati HDFS set hello **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Cartella toohello percorso. Esempio: `myfolder`<br/><br/>Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello. Ad esempio: per cartella\sottocartella specificare cartella\\\\sottocartella e per d:\cartellaesempio specificare l'unità d:\\\\cartellaesempio.<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora. |Sì |
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: <br/><br/>Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| partitionedBy |partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale. Ad esempio, folderPath con parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> filename e fileFilter non possono essere usati contemporaneamente.

#### <a name="example"></a>Esempio

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Origine File System nell'attività di copia
Se si copiano dati da HDFS, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:

**FileSystemSource** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello. |True, False (valore predefinito) |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un SFTP **tipo** di hello servizio collegato troppo**Sftp**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- | --- |
| host | Nome o indirizzo IP del server SFTP hello. |Sì |
| port |Porta su cui hello SFTP server è in ascolto. valore predefinito di Hello è: 21 |No |
| authenticationType |Specificare il tipo di autenticazione. Valori consentiti: **Base**, **SshPublicKey**. <br><br> Fare riferimento troppo[tramite l'autenticazione di base](#using-basic-authentication) e [tramite SSH autenticazione a chiave pubblica](#using-ssh-public-key-authentication) sezioni su altre proprietà e gli esempi JSON rispettivamente. |Sì |
| skipHostKeyValidation | Specificare se tooskip chiave convalida dell'host. | No. Hello valore predefinito: false |
| hostKeyFingerprint | Specificare impronte digitali hello della chiave host hello. | Sì se hello `skipHostKeyValidation` è impostato toofalse.  |
| gatewayName |Nome di hello Gateway di gestione dati tooconnect tooan locale server SFTP. | Sì se si copiano i dati da un server SFTP locale. |
| encryptedCredential | Server SFTP hello tooaccess credenziali crittografate. Generati automaticamente quando si specifica l'autenticazione di base (password e nome utente) o parametri SshPublicKey (nome utente + percorso della chiave privata o contenuto) nella copia guidata o hello ClickOnce finestra di dialogo popup. | No. Applicare solo se si copiano i dati da un server SFTP locale. |

#### <a name="example-using-basic-authentication"></a>Esempio: uso dell'autenticazione di base

impostare l'autenticazione di base toouse, `authenticationType` come `Basic`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- | --- |
| username | Utente che dispone di server di accesso toohello SFTP. |Sì |
| password | Password per l'utente di hello (nomeutente). | Sì |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Esempio: autenticazione di base con credenziali crittografate**

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>Esempio: uso dell'autenticazione con chiave pubblica SSH:**

impostare l'autenticazione di base toouse, `authenticationType` come `SshPublicKey`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- | --- |
| username |Utente che dispone di server di accesso toohello SFTP |Sì |
| privateKeyPath | Specificare un percorso assoluto toohello file di chiave privata accessibile tale gateway. | Specificare entrambi hello `privateKeyPath` o `privateKeyContent`. <br><br> Applicare solo se si copiano i dati da un server SFTP locale. |
| privateKeyContent | Una stringa serializzata del contenuto di chiave privata di hello. Hello Copia guidata è possibile leggere il file di chiave privata di hello ed estrarre automaticamente il contenuto di chiave privata di hello. Se si utilizza qualsiasi altro strumento o SDK, è possibile utilizzare proprietà privateKeyPath hello. | Specificare entrambi hello `privateKeyPath` o `privateKeyContent`. |
| passPhrase | Specificare hello frase/password toodecrypt hello privati passkey se i file di chiave hello è protetto da una passphrase. | Sì se il file di chiave privata di hello è protetto da una passphrase. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Esempio: autenticazione SshPublicKey con contenuto della chiave privata**

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati, SFTP, hello set **tipo** del set di dati hello troppo**FileShare**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Toohello sottocartella percorso. Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora. |Sì |
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: <br/><br/>Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.<br/><br/>I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).<br/><br/>Esempi 1: `"fileFilter": "*.log"`<br/>Esempio 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter è applicabile per un set di dati di input FileShare. Questa proprietà non è supportata con HDFS. |No |
| partitionedBy |partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale. Ad esempio, folderPath con parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Specificare se usare la modalità di trasferimento binario. True per la modalità binaria e false per ASCII. Valore predefinito: True. Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer. |No |

> [!NOTE]
> filename e fileFilter non possono essere usati contemporaneamente.

#### <a name="example"></a>Esempio

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Origine File System nell'attività di copia
Se si copiano dati da un'origine SFTP, impostare hello **tipo di origine** di hello attività di copia troppo**FileSystemSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello. |True, False (valore predefinito) |No |



#### <a name="example"></a>Esempio

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore SFTP](data-factory-sftp-connector.md#copy-activity-properties).


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un HTTP **tipo** di hello servizio collegato troppo**Http**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| URL | URL toohello Server Web di base | Sì |
| authenticationType | Specifica il tipo di autenticazione hello. I valori consentiti sono: **Anonymous**, **Basic**, **Digest**, **Windows** e **ClientCertificate**. <br><br> Vedere rispettivamente toosections riportata sotto questa tabella in più proprietà e gli esempi JSON per i tipi di autenticazione. | Sì |
| enableServerCertificateValidation | Specificare se il server tooenable SSL la convalida del certificato se l'origine è il Server Web HTTPS | No, il valore predefinito è true |
| gatewayName | Nome di hello Gateway di gestione dati tooconnect tooan locale origine HTTP. | Sì se si copiano i dati da un'origine HTTP locale. |
| encryptedCredential | Credenziali crittografate tooaccess hello endpoint HTTP. Generati automaticamente quando si configurano le informazioni di autenticazione hello in copia guidata o hello ClickOnce finestra di dialogo popup. | No. Applicare solo se si copiano i dati da un server HTTP locale. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Esempio: uso dell'autenticazione di base, Digest o Windows
Impostare `authenticationType` come `Basic`, `Digest`, o `Windows`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| username | Nome utente tooaccess hello endpoint HTTP. | Sì |
| password | Password per l'utente di hello (nomeutente). | Sì |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Esempio: uso dell'autenticazione ClientCertificate

impostare l'autenticazione di base toouse, `authenticationType` come `ClientCertificate`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| embeddedCertData | Hello contenuto con codifica Base64 di dati binari del file di scambio di informazioni personali (PFX) hello. | Specificare entrambi hello `embeddedCertData` o `certThumbprint`. |
| certThumbprint | Hello identificazione personale del certificato hello che è stata installata nell'archivio certificati del computer gateway. Applicare solo se si copiano i dati da un'origine HTTP locale. | Specificare entrambi hello `embeddedCertData` o `certThumbprint`. |
| password | Password associata al certificato hello. | No |

Se si utilizza `certThumbprint` per hello e autenticazione il certificato è installato nell'archivio personale di hello del computer locale hello, è necessario che il servizio gateway toogrant hello autorizzazione di lettura toohello:

1. Avviare Microsoft Management Console (MMC). Aggiungere hello **certificati** snap-in tale hello destinazioni **Computer locale**.
2. Espandere **Certificati**, **Personali** e fare clic su **Certificati**.
3. Certificato hello dall'archivio personale hello e scegliere **tutte le attività**->**Gestisci chiavi Private...**
3. In hello **sicurezza** scheda, aggiungere l'account utente di hello in cui è in esecuzione servizio Host di Gateway di gestione di dati con certificato toohello di hello accesso in lettura.  

**Esempio: utilizzo del certificato client:** questo collegato collegamenti al servizio data factory tooan locale HTTP server web. Usa un certificato client è installato nel computer di hello con Gateway di gestione di dati installati.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Esempio: utilizzo di un certificato client in un file
Questo collegato collegamenti al servizio data factory tooan locale HTTP server web. Usa un file del certificato client nel computer di hello con Gateway di gestione di dati installati.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
set di dati toodefine un HTTP, hello set **tipo** del set di dati hello troppo**Http**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| relativeUrl | Una risorsa relativa di URL toohello che contiene dati hello. Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello. <br><br> tooconstruct URL dinamico, è possibile utilizzare [funzioni di Data Factory e le variabili di sistema](data-factory-functions-variables.md), esempio: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | No |
| requestMethod | Metodo HTTP. I valori consentiti sono **GET** o **POST**. | No. Il valore predefinito è `GET`. |
| additionalHeaders | Intestazioni richiesta HTTP aggiuntive. | No |
| requestBody | Il corpo della richiesta HTTP. | No |
| format | Se si desidera toosimply **recuperare i dati di hello da endpoint HTTP come-è** senza analizzarlo, ignorare questa impostazione di formato. <br><br> Se si desidera tooparse hello HTTP risposta contenuto durante la copia, è supportato i seguenti tipi di formato hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

#### <a name="example-using-hello-get-default-method"></a>Esempio: hello metodo GET (impostazione predefinita)

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Esempio: utilizzo di metodo POST hello

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#dataset-properties).

### <a name="http-source-in-copy-activity"></a>Origine HTTP nell'attività di copia
Se si copiano dati da un'origine HTTP, impostare hello **tipo di origine** di hello attività di copia troppo**HttpSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| httpRequestTimeout | Hello timeout (TimeSpan) per hello HTTP richiesta tooget una risposta. È hello timeout tooget una risposta, dati di risposta non hello timeout tooread. | No. Valore predefinito: 00:01:40 |


#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore HTTP](data-factory-http-connector.md#copy-activity-properties).

## <a name="odata"></a>OData

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine OData collegato **tipo** di hello servizio collegato troppo**OData**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| URL |URL del servizio OData hello. |Sì |
| authenticationType |Tipo di autenticazione usato tooconnect toohello un'origine OData. <br/><br/> Per OData in cloud, i valori possibili sono Anonymous, Basic e OAuth. Si noti che Azure Data Factory attualmente supporta solo OAuth basato su Azure Active Directory). <br/><br/> Per OData locale, i valori possibili sono Anonima, Di base e Windows. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione di base. |Sì (solo se si usa l'autenticazione di base) |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |Sì (solo se si usa l'autenticazione di base) |
| authorizedCredential |Se si utilizza OAuth, fare clic su **Authorize** pulsante nell'Editor o hello Data Factory Copia guidata e immettere le credenziali, il valore di hello di questa proprietà verrà generato automaticamente. |Sì (solo se si usa l'autenticazione OAuth) |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve usare servizio OData di tooconnect toohello locale. Specificare solo se si copiano dati da un'origine OData locale. |No |

#### <a name="example---using-basic-authentication"></a>Esempio - Uso dell'autenticazione di base
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Esempio - Uso dell'autenticazione anonima

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Esempio - Uso dell'autenticazione Windows per accedere all'origine OData locale

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Esempio - Uso dell'autenticazione OAuth per accedere all'origine OData cloud
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#linked-service-properties).

### <a name="dataset"></a>Set di dati
toodefine un set di dati OData, hello set **tipo** del set di dati hello troppo**ODataResource**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| path |Percorso toohello risorse OData |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da un'origine OData, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Esempio | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |"?$select=Name, Description&$top=5" |No |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Per altre informazioni, vedere [Connettore OData](data-factory-odata-connector.md#copy-activity-properties).


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un ODBC **tipo** di hello servizio collegato troppo**OnPremisesOdbc**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| connectionString |credenziale è crittografata da parte di credenziali di accesso non Hello di stringa di connessione hello e un parametro facoltativo. Vedere esempi in hello le sezioni seguenti. |Sì |
| credential |parte delle credenziali di accesso Hello hello della stringa di connessione specificato nel formato valore della proprietà specifiche del driver. Esempio: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;". |No |
| authenticationType |Tipo di autenticazione utilizzato l'archivio di dati ODBC toohello tooconnect. I valori possibili sono: anonima e di base. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione di base. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve utilizzare l'archivio di dati ODBC toohello tooconnect. |Sì |

#### <a name="example---using-basic-authentication"></a>Esempio - Uso dell'autenticazione di base

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Esempio - Uso dell'autenticazione di base con credenziali crittografate
È possibile crittografare le credenziali di hello utilizzando hello [New AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versione di Azure PowerShell) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 o versioni precedenti di hello Azure PowerShell).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Esempio: uso dell'autenticazione anonima

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati ODBC, hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nell'archivio di dati ODBC hello. |Sì |


#### <a name="example"></a>Esempio

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da un archivio di dati ODBC, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: `select * from MyTable`. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Per altre informazioni, vedere [Connettore ODBC](data-factory-odbc-connector.md#copy-activity-properties).

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di Salesforce toodefine **tipo** di hello servizio collegato troppo**Salesforce**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| environmentUrl | Specificare l'istanza di URL di Salesforce hello. <br><br> - Il valore predefinito è "https://login.salesforce.com". <br> -toocopy dati dalla sandbox, specificare "https://test.salesforce.com". <br> -toocopy dati da un dominio personalizzato, specificare, ad esempio, "https://[domain].my.salesforce.com". |No |
| username |Specificare un nome utente per l'account utente di hello. |Sì |
| password |Specificare una password per account utente di hello. |Sì |
| securityToken |Specificare un token di sicurezza per l'account utente di hello. Vedere [ottenere token di sicurezza](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) per istruzioni su come un token di sicurezza tooreset/get. in generale, vedere toolearn sui token di sicurezza [API di protezione e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati di Salesforce, hello set **tipo** del set di dati hello troppo**RelationalTable**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello in Salesforce. |No, se è specificata una **query** di **RelationalSource** |

#### <a name="example"></a>Esempio

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origine relazionale nell'attività di copia
Se si copiano dati da Salesforce, impostare hello **tipo di origine** di hello attività di copia troppo**RelationalSource**e specificare le seguenti proprietà in hello **origine** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Query SQL-92 o query [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Ad esempio: `select * from MyTable__c`. |No (se hello **tableName** di hello **set di dati** è specificato) |

#### <a name="example"></a>Esempio  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.

Per altre informazioni, vedere [Connettore Salesforce](data-factory-salesforce-connector.md#copy-activity-properties). 

## <a name="web-data"></a>Dati Web 

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine Web collegato **tipo** di hello servizio collegato troppo**Web**e specificare le seguenti proprietà in hello **typeProperties** sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| Url |Origine di URL toohello Web |Sì |
| authenticationType |Anonimo. |Sì |
 

#### <a name="example"></a>Esempio


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Set di dati
toodefine un set di dati Web hello set **tipo** del set di dati hello troppo**tabella Web**e specificare le proprietà in hello seguenti hello **typeProperties** sezione: 

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |tipo di set di dati hello. deve essere impostato troppo**tabella Web** |Sì |
| path |Una risorsa relativa di URL toohello che contiene la tabella hello. |No. Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello. |
| index |indice di Hello della tabella hello nella risorsa hello. Vedere [indice Get di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) sezione per indice toogetting passaggi di una tabella in una pagina HTML. |Sì |

#### <a name="example"></a>Esempio

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#dataset-properties). 

### <a name="web-source-in-copy-activity"></a>Origine Web nell'attività di copia
Se si copiano dati da una tabella, impostare hello **tipo di origine** di hello attività di copia troppo**WebSource**. Attualmente, quando origine hello in attività di copia è di tipo **WebSource**, non sono supportate proprietà aggiuntive.

#### <a name="example"></a>Esempio

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Per altre informazioni, vedere [Connettore Tabella Web](data-factory-web-table-connector.md#copy-activity-properties). 

## <a name="compute-environments"></a>Ambienti di calcolo
Hello nella tabella seguente elenca gli ambienti di calcolo hello è supportati da Data Factory e hello attività di trasformazione che è possibile eseguire su di essi. Fare clic sul collegamento hello per il calcolo hello si è interessati negli schemi JSON hello toosee per toolink servizio collegato data factory di tooa. 

| Ambiente di calcolo | Attività |
| --- | --- |
| [Cluster HDInsight su richiesta](#on-demand-azure-hdinsight-cluster) o [il proprio cluster HDInsight](#existing-azure-hdinsight-cluster) |[Attività personalizzata .NET ](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig](#hdinsight-pig-activity, [attività MapReduce](#hdinsight-mapreduce-activity), [attività di Hadoop Streaming](#hdinsight-streaming-activityd), [attività Spark](#hdinsight-spark-activity) |
| [Azure Batch](#azure-batch) |[Attività personalizzata .NET](#net-custom-activity) |
| [Azure Machine Learning](#azure-machine-learning) | [Attività di esecuzione batch di Machine Learning](#machine-learning-batch-execution-activity), [Attività della risorsa di aggiornamento di Machine Learning](#machine-learning-update-resource-activity) |
| [Azure Data Lake Analytics.](#azure-data-lake-analytics) |[Attività U-SQL di Data Lake Analytics](#data-lake-analytics-u-sql-activity) |
| [Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1) |[Stored procedure](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>Cluster HDInsight di Azure su richiesta
Hello servizio Azure Data Factory può creare automaticamente un dati di tooprocess di basati su Windows o Linux su richiesta HDInsight cluster. Hello cluster viene creato nella stessa area dell'account di archiviazione hello (proprietà linkedServiceName in JSON hello) associata a cluster hello hello. È possibile eseguire hello seguire le attività di trasformazione di questo servizio collegato: [attività personalizzate .NET](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig] (#hdinsight--attività pig, [attività MapReduce ](#hdinsight-mapreduce-activity), [Hadoop streaming attività](#hdinsight-streaming-activityd), [nascita attività](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Servizio collegato 
Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di HDInsight su richiesta.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà tipo Hello deve essere impostato troppo**HDInsightOnDemand**. |Sì |
| clusterSize |Numero di nodi di lavoro o dati in cluster hello. cluster HDInsight Hello viene creato con 2 nodi head e il numero di hello di nodi di lavoro che è specificato per questa proprietà. nodi Hello sono di dimensioni Standard_D3 con 4 core, pertanto un cluster di nodi di 4 lavoro accetta 24 core (4\*4 = 16 core per i nodi di lavoro, più 2\*4 = 8 core per i nodi head). Vedere [cluster basati su Linux creare Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) per informazioni dettagliate su livello hello Standard_D3. |Sì |
| timeToLive |Hello consentito tempo di inattività per il cluster HDInsight su richiesta di hello. Specifica quanto tempo rimarrà attivo cluster HDInsight su richiesta di hello dopo il completamento di un'attività eseguita se non sono disponibili altri processi attivi cluster hello.<br/><br/>Ad esempio, se un'attività eseguita richiede 6 minuti e la proprietà timetolive è impostato too5 minuti, hello cluster rimane attivo per 5 minuti dopo hello 6 minuti di elaborazione di esecuzione dell'attività hello. Se l'esecuzione di un'altra attività viene eseguita con finestra 6 minuti hello, che viene elaborato dalla hello dello stesso cluster.<br/><br/>Creazione di un cluster di HDInsight su richiesta è un'operazione dispendiosa (potrebbe richiedere un po' di tempo), quindi utilizzare questa impostazione prestazioni tooimprove necessari per una data factory riutilizzando un cluster di HDInsight su richiesta.<br/><br/>Se si imposta la proprietà timetolive valore too0, cluster hello viene eliminato non appena l'esecuzione di attività hello in elaborato. In hello invece se si imposta un valore elevato, cluster hello può rimanere inattivo inutilmente risultante in costi elevati. Pertanto, è importante impostare hello di valore appropriato in base alle proprie esigenze.<br/><br/>Più pipeline possono condividere hello stessa istanza del cluster HDInsight su richiesta di hello se il valore della proprietà timetolive hello è impostato in modo appropriato |Sì |
| version |Versione del cluster HDInsight hello. Per informazioni dettagliate vedere le [versioni supportate di HDInsight in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |No |
| linkedServiceName |Servizio collegato di archiviazione Azure: toobe utilizzato dal cluster di hello su richiesta per l'archiviazione e l'elaborazione dei dati. <p>Attualmente, è possibile creare un cluster HDInsight su richiesta che utilizza un archivio Azure Data Lake come archiviazione hello. Se si desiderano dati del risultato hello toostore dal HDInsight l'elaborazione in un archivio Azure Data Lake, utilizzare un attività di copia toocopy hello dati dall'archiviazione Blob di Azure di hello toohello archivio Azure Data Lake.</p>  | Sì |
| additionalLinkedServiceNames |Specifica l'account di archiviazione aggiuntivi per hello HDInsight servizio collegato in modo che il servizio di Data Factory hello può registrare per conto dell'utente. |No |
| osType |Tipo di sistema operativo. I valori consentiti sono: Windows (impostazione predefinita) e Linux |No |
| hcatalogLinkedServiceName |nome Hello del collegato SQL Azure database HCatalog toohello punto del servizio. cluster di HDInsight su richiesta Hello viene creato utilizzando il database di SQL Azure hello come metastore hello. |No |

### <a name="json-example"></a>Esempio di JSON
Hello JSON seguente definisce un servizio di collegato di HDInsight su richiesta basati su Linux. Hello servizio Data Factory crea automaticamente un **basati su Linux** cluster HDInsight durante l'elaborazione di una sezione di dati. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Per altre informazioni, vedere l'articolo relativo ai [servizi collegati di calcolo](data-factory-compute-linked-services.md). 

## <a name="existing-azure-hdinsight-cluster"></a>Cluster HDInsight di Azure esistente
È possibile creare cluster HDInsight un tooregister di servizio collegato di HDInsight di Azure con Data Factory. È possibile eseguire hello seguente attività di trasformazione dei dati in questo servizio collegato: [attività personalizzate .NET](#net-custom-activity), [attività Hive](#hdinsight-hive-activity), [attività Pig] (#hdinsight--attività pig, [MapReduce attività](#hdinsight-mapreduce-activity), [Hadoop streaming attività](#hdinsight-streaming-activityd), [nascita attività](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Servizio collegato
Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di HDInsight di Azure.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà tipo Hello deve essere impostato troppo**HDInsight**. |Sì |
| clusterUri |URI del cluster HDInsight hello Hello. |Sì |
| username |Specificare nome hello di hello utente toobe utilizzata cluster di HDInsight tooconnect tooan esistente. |Sì |
| password |Specificare la password per l'account utente di hello. |Sì |
| linkedServiceName | Nome di servizio collegato di archiviazione di Azure che fa riferimento nell'archiviazione blob di Azure toohello hello utilizzato da hello cluster HDInsight. <p>Attualmente non è possibile specificare un servizio collegato di Azure Data Lake Store per questa proprietà. È possibile accedere ai dati hello archivio Azure Data Lake dagli script Hive o Pig se il cluster di HDInsight hello dispone di accesso toohello archivio Data Lake. </p>  |Sì |

Per le versioni dei cluster di HDInsight, vedere le [versioni supportate di HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Azure Batch
È possibile creare un pool di Batch di macchine virtuali (VM) di un tooregister di servizio collegato di Azure Batch con una data factory. È possibile eseguire le attività .NET personalizzate utilizzando Batch Azure o Azure HDInsight. Su questo servizio collegato è possibile eseguire un' [attività personalizzata .NET](#net-custom-activity). 

### <a name="linked-service"></a>Servizio collegato
Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di Azure Batch.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà tipo Hello deve essere impostato troppo**AzureBatch**. |Sì |
| accountName |Nome dell'account Azure Batch hello. |Sì |
| accessKey |Chiave di accesso per account Azure Batch hello. |Sì |
| poolName |Nome del pool di hello delle macchine virtuali. |Sì |
| linkedServiceName |Nome del servizio collegato di archiviazione di Azure associato a questo servizio collegato di Azure Batch hello. Questo servizio collegato viene utilizzato per i file di gestione temporanea attività hello toorun e l'archiviazione dei log di esecuzione di attività hello obbligatori. |Sì |


#### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Azure Machine Learning
Creare un tooregister di servizio collegato di Azure Machine Learning punteggio endpoint con una data factory di un batch di Machine Learning. Su questo servizio collegato è possibile eseguire due attività di trasformazione dati: [Attività di esecuzione batch di Machine Learning](#machine-learning-batch-execution-activity), [Attività della risorsa di aggiornamento di Machine Learning](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Servizio collegato
Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione di hello Azure JSON di un servizio collegato di Azure Machine Learning.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| Tipo |proprietà di tipo Hello deve essere impostata su: **Azure ml**. |Sì |
| mlEndpoint |URL di punteggio batch di Hello. |Sì |
| apiKey |Hello pubblicati API del modello di area di lavoro. |Sì |

#### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics.
Si crea un **Azure Data Lake Analitica** collegati toolink servizio una factory di dati di Azure tooan del servizio di calcolo di Azure Data Lake Analitica prima di utilizzare hello [attività Data Lake Analitica U-SQL](data-factory-usql-activity.md) in una pipeline .

### <a name="linked-service"></a>Servizio collegato

Hello nella tabella seguente vengono fornite descrizioni per le proprietà di hello utilizzate nella definizione JSON hello di un servizio di Azure Data Lake Analitica collegato. 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| Tipo |proprietà di tipo Hello deve essere impostata su: **AzureDataLakeAnalytics**. |Sì |
| accountName |Nome dell'account di Azure Data Lake Analytics. |Sì |
| dataLakeAnalyticsUri |URI di Azure Data Lake Analytics. |No |
| autorizzazione |Codice di autorizzazione viene recuperato automaticamente dopo aver fatto clic **Authorize** pulsante hello Editor delle Data Factory e completamento dell'account di accesso hello OAuth. |Sì |
| subscriptionId |ID sottoscrizione di Azure |No (se non specificato, sottoscrizione di hello viene utilizzata una data factory). |
| resourceGroupName |Nome del gruppo di risorse di Azure |No (se non specificato, il gruppo di risorse di hello viene utilizzata una data factory). |
| sessionId |id di sessione dalla sessione di autorizzazione OAuth hello. Ogni ID di sessione è univoco e può essere usato solo una volta. Quando si utilizza l'Editor delle Data Factory di hello, questo ID viene generato automaticamente. |Sì |


#### <a name="json-example"></a>Esempio di JSON
Hello di esempio seguente fornisce una definizione JSON per un servizio di Azure Data Lake Analitica collegato.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Database SQL di Azure
È possibile creare un servizio collegato SQL Azure e usarlo con hello [attività Stored Procedure](#stored-procedure-activity) tooinvoke una stored procedure da una pipeline di Data Factory. 

### <a name="linked-service"></a>Servizio collegato
il set hello servizio collegato di toodefine un Database di SQL Azure **tipo** di hello servizio collegato troppo**AzureSqlDatabase**e specificare le seguenti proprietà in hello **typeProperties**sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| connectionString |Specificare l'istanza del Database di SQL Azure toohello tooconnect necessarie informazioni per la proprietà connectionString hello. |Sì |

#### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Vedere l’articolo [Connettore di Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su questo servizio collegato.

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
È possibile creare un servizio collegato di Azure SQL Data Warehouse e usarlo con hello [attività Stored Procedure](data-factory-stored-proc-activity.md) tooinvoke una stored procedure da una pipeline di Data Factory. 

### <a name="linked-service"></a>Servizio collegato
il servizio hello set toodefine un Data Warehouse di SQL Azure collegato **tipo** di hello servizio collegato troppo**AzureSqlDW**e specificare le seguenti proprietà in hello **typeProperties**sezione:  

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| connectionString |Specificare l'istanza di Azure SQL Data Warehouse toohello tooconnect necessarie informazioni per la proprietà connectionString hello. |Sì |

#### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Per altre informazioni, vedere [Connettore Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

## <a name="sql-server"></a>SQL Server 
Creare un servizio collegato SQL Server e usarlo con hello [attività Stored Procedure](data-factory-stored-proc-activity.md) tooinvoke una stored procedure da una pipeline di Data Factory. 

### <a name="linked-service"></a>Servizio collegato
Creare un servizio collegato di tipo **OnPremisesSqlServer** toolink una data factory tooa di on-premise SQL Server database. Hello nella tabella seguente fornisce una descrizione del servizio collegato SQL Server locale tooon specifici elementi JSON.

Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooSQL servizio del Server collegato.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OnPremisesSqlServer**. |Sì |
| connectionString |Specificare le informazioni connectionString necessarie tooconnect database di SQL Server on-premise toohello utilizzando l'autenticazione di SQL Server o l'autenticazione di Windows. |Sì |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve utilizzare i database di SQL Server on-premise toohello tooconnect. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione Windows. Esempio: **nomedominio\\nomeutente**. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |

È possibile crittografare le credenziali utilizzando hello **New AzureRmDataFactoryEncryptValue** cmdlet e utilizzarli nella stringa di connessione hello, come illustrato nell'esempio seguente hello (**EncryptedCredential** proprietà):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Esempio: JSON per l'uso dell'autenticazione SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Esempio: JSON per l'uso dell'autenticazione Windows

Se vengono specificati nome utente e password, gateway li utilizza hello tooimpersonate database di SQL Server on-premise toohello tooconnect account utente specificato. In caso contrario, gateway si connetta toohello SQL Server direttamente con il contesto di sicurezza hello del Gateway (il relativo account di avvio).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Per altre informazioni, vedere [Connettore SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).

## <a name="data-transformation-activities"></a>ATTIVITÀ DI TRASFORMAZIONE DEI DATI

Attività | Descrizione
-------- | -----------
[Attività Hive di HDInsight](#hdinsight-hive-activity) | attività Hive di HDInsight in una pipeline di Data Factory Hello esegue query Hive per proprio conto o il cluster HDInsight basati su Windows o Linux su richiesta. 
[Attività Pig di HDInsight](#hdinsight-pig-activity) | attività Pig di HDInsight in una pipeline di Data Factory Hello esegue query Pig autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta.
[Attività MapReduce di HDInsight](#hdinsight-mapreduce-activity) | attività MapReduce di HDInsight in una pipeline di Data Factory Hello esegue i programmi MapReduce autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta.
[Attività di streaming di HDInsight](#hdinsight-streaming-activity) | Hello attività Streaming di HDInsight in una pipeline di Data Factory esegue i programmi di Hadoop Streaming autonomamente o il cluster HDInsight basati su Windows o Linux su richiesta.
[Attività HDInsight Spark](#hdinsight-spark-activity) | attività HDInsight Spark in una pipeline di Data Factory Hello esegue programmi Spark nel cluster HDInsight. 
[Attività di esecuzione batch di Machine Learning](#machine-learning-batch-execution-activity) | Servizio per analitica predittiva web di Azure consente di Data Factory è tooeasily creare pipeline che utilizzano una versione pubblicata di Azure Machine Learning. Utilizza hello attività di esecuzione del Batch in una pipeline di Data Factory di Azure, è possibile richiamare un stime di toomake servizio web Machine Learning sui dati hello in batch. 
[Attività della risorsa di aggiornamento di Machine Learning](#machine-learning-update-resource-activity) | Nel corso del tempo, modelli predittivi di hello in hello Machine Learning esperimenti punteggio necessario toobe ripetere il training utilizzando il nuovo set di dati di input. Dopo avere completato con ripetizione di training, si desidera hello tooupdate punteggio servizio web con hello Training modello di Machine Learning. È possibile utilizzare servizio web di attività di aggiornamento risorsa tooupdate hello hello con hello appena training del modello.
[Attività stored procedure](#stored-procedure-activity) | È possibile utilizzare l'attività di Stored Procedure hello in tooinvoke di pipeline una stored procedure in uno dei seguenti archivi dati hello una Data Factory: Database SQL di Azure, Azure SQL Data Warehouse, il Database di SQL Server nell'organizzazione o una macchina virtuale di Azure. 
[Attività U-SQL di Data Lake Analytics](#data-lake-analytics-u-sql-activity) | L'attività U-SQL di Data Lake Analytics esegue uno script U-SQL in un cluster di Azure Data Lake Analytics.  
[Attività personalizzata .NET](#net-custom-activity) | Se è necessario tootransform dati in modo che non è supportato da Data Factory, è possibile creare un'attività personalizzata con la logica di elaborazione dei dati e utilizzare attività hello nella pipeline hello. È possibile configurare hello personalizzato .NET attività toorun utilizzando un servizio Azure Batch o un cluster Azure HDInsight. 

     
## <a name="hdinsight-hive-activity"></a>Attività Hive di HDInsight
È possibile specificare le proprietà in una definizione del formato JSON dell'attività Hive seguenti hello. deve essere di proprietà del tipo Hello attività hello: **HDInsightHive**. È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightHive attività:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| script |Specificare hello Hive script inline |No |
| script path |Hello archivio Hive script in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file. Usare la proprietà "script" o "scriptPath". Non è possibile usare entrambe le proprietà. nome del file Hello è tra maiuscole e minuscole. |No |
| defines |Specificare i parametri come coppie chiave/valore per il riferimento all'interno dello script Hive hello utilizzando 'hiveconf' |No |

Queste proprietà sono toohello specifica attività Hive. Altre proprietà (all'esterno di sezione typeProperties hello) sono supportati per tutte le attività.   

### <a name="json-example"></a>Esempio di JSON
Hello JSON seguente definisce un'attività Hive di HDInsight in una pipeline.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

Per altre informazioni, vedere [Attività Hive](data-factory-hive-activity.md). 

## <a name="hdinsight-pig-activity"></a>Attività Pig di HDInsight
È possibile specificare le proprietà in una definizione del formato JSON dell'attività Pig seguenti hello. deve essere di proprietà del tipo Hello attività hello: **HDInsightPig**. È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightPig attività: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| script |Specificare hello Pig script inline |No |
| script path |Archiviare lo script Pig hello in una risorsa di archiviazione blob di Azure e fornire hello percorso toohello file. Usare la proprietà "script" o "scriptPath". Non è possibile usare entrambe le proprietà. nome del file Hello è tra maiuscole e minuscole. |No |
| defines |Specificare i parametri come coppie chiave/valore per il riferimento all'interno di uno script Pig hello |No |

Queste proprietà sono toohello specifica attività Pig. Altre proprietà (all'esterno di sezione typeProperties hello) sono supportati per tutte le attività.   

### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

Per altre informazioni, vedere [Attività Pig](#data-factory-pig-activity.md). 

## <a name="hdinsight-mapreduce-activity"></a>Attività MapReduce di HDInsight
È possibile specificare hello seguenti proprietà in una definizione del formato JSON dell'attività MapReduce. deve essere di proprietà del tipo Hello attività hello: **HDInsightMapReduce**. È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightMapReduce attività: 

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| jarLinkedService | Nome di hello collegato del servizio di archiviazione di Azure che contiene i file JAR hello hello. | Sì |
| jarFilePath | Percorso file JAR di toohello in hello archiviazione di Azure. | Sì | 
| className | Nome della classe principale di hello in file JAR hello. | Sì | 
| arguments | Un elenco di argomenti delimitato da virgole per il programma MapReduce hello. In fase di esecuzione vedere alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework MapReduce hello. toodifferentiate degli argomenti con argomenti di MapReduce hello, considerare l'utilizzo sia opzione e il valore come argomenti, come illustrato nell'esempio seguente hello (- s, input, --output e così via, sono immediatamente seguite dai valori di opzioni) | No | 

### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Per altre informazioni, vedere [Attività MapReduce](data-factory-map-reduce.md). 

## <a name="hdinsight-streaming-activity"></a>Attività di streaming di HDInsight
È possibile specificare le proprietà in una definizione del formato JSON dell'attività di Streaming Hadoop seguenti hello. deve essere di proprietà del tipo Hello attività hello: **HDInsightStreaming**. È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightStreaming attività: 

| Proprietà | Descrizione | 
| --- | --- |
| mapper | Nome del mapper hello eseguibile. Nell'esempio hello cat.exe è mapper hello eseguibile.| 
| reducer | Nome del file eseguibile del reducer hello. Nell'esempio hello wc.exe è file eseguibile del reducer hello. | 
| input | File di input (incluso percorso) per il mapper hello. Nell'esempio hello: "//adfsample @<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample è il contenitore di blob hello, esempio/data/Gutenberg è la cartella hello e davinci.txt è blob hello. |
| output | File di output (incluso percorso) per riduttore hello. output di Hello del processo Hadoop Streaming hello viene scritto toohello percorso specificato per questa proprietà. |
| filePaths | Percorsi per gli eseguibili del mapper e del reducer hello. Nell'esempio hello: "adfsample/example/apps/wc.exe", adfsample è il contenitore di blob hello, example/apps è la cartella hello e wc.exe è hello eseguibile. | 
| fileLinkedService | Servizio collegato di archiviazione Azure che rappresenta l'archiviazione di Azure che contiene file hello specificati nella sezione filePaths hello hello. | 
| arguments | Un elenco di argomenti delimitato da virgole per il programma MapReduce hello. In fase di esecuzione vedere alcuni argomenti aggiuntivi (ad esempio: mapreduce.job.tags) dal framework MapReduce hello. toodifferentiate degli argomenti con argomenti di MapReduce hello, considerare l'utilizzo sia opzione e il valore come argomenti, come illustrato nell'esempio seguente hello (- s, input, --output e così via, sono immediatamente seguite dai valori di opzioni) | 
| getDebugInfo | Un elemento facoltativo. Quando si imposta tooFailure, hello registri vengono scaricati solo in caso di errore. Quando si imposta tooAll, i log vengono sempre scaricati indipendentemente lo stato di esecuzione hello. | 

> [!NOTE]
> È necessario specificare un set di dati di output di hello attività di Streaming di Hadoop per hello **restituisce** proprietà. Questo set di dati può essere solo un dummy set di dati è necessario toodrive hello pipeline pianificazione (oraria, giornaliera, e così via.). Se l'attività hello non accetta un input, è possibile ignorare specificando un set di dati di input per l'attività hello per hello **input** proprietà.  

## <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Per altre informazioni, vedere l'argomento relativo all'[attività Hadoop Streaming](data-factory-hadoop-streaming-activity.md). 

## <a name="hdinsight-spark-activity"></a>Attività Spark di HDInsight
È possibile specificare le proprietà in una definizione del formato JSON dell'attività Spark seguenti hello. deve essere di proprietà del tipo Hello attività hello: **HDInsightSpark**. È necessario creare innanzitutto un servizio collegato di HDInsight e specificare il nome di hello di esso come valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooHDInsightSpark attività: 

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| rootPath | contenitore di Blob di Azure Hello e della cartella che contiene file Spark hello. nome del file Hello è tra maiuscole e minuscole. | Sì |
| entryFilePath | Cartella radice di percorso relativo toohello di hello Spark codice o del pacchetto. | Sì |
| className | Classe principale Java/Spark dell'applicazione | No | 
| arguments | Un elenco di programmi di Spark toohello gli argomenti della riga di comando. | No | 
| proxyUser | programma di Hello utente account tooimpersonate tooexecute hello Spark | No | 
| sparkConfig | Proprietà di configurazione di Spark. | No | 
| getDebugInfo | Specifica quando i file di log Spark hello toohello copiato archiviazione di Azure usati dal cluster HDInsight (o) specificato da sparkJobLinkedService. Valori consentiti: None, Always o Failure. Valore predefinito: None. | No | 
| sparkJobLinkedService | servizio collegato di archiviazione di Azure che contiene i registri, le dipendenze e hello Spark processo file Hello.  Se non si specifica un valore per questa proprietà, viene utilizzata l'archiviazione di hello associato al cluster HDInsight. | No |

### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Si noti hello seguenti punti: 

- Hello **tipo** impostata troppo**HDInsightSpark**.
- Hello **rootPath** è troppo**adfspark\\pyFiles** dove adfspark è il contenitore di Blob di Azure hello e pyFiles è cartella correttamente in tale contenitore. In questo esempio hello archiviazione Blob di Azure è hello uno associato al cluster Spark hello. È possibile caricare tooa file hello archiviazione di Azure diversi. In tal caso, creare un toolink di servizio collegato di archiviazione di Azure che data factory toohello account di archiviazione. Quindi, specificare il nome di hello del servizio hello collegato come valore per hello **sparkJobLinkedService** proprietà. Vedere [le proprietà dell'attività di Spark](#spark-activity-properties) per informazioni dettagliate su questa proprietà e altre proprietà supportate dall'attività Spark hello.
- Hello **entryFilePath** è impostato toohello **test.py**, ossia file python hello. 
- Hello **getDebugInfo** impostata troppo**sempre**, ovvero i file di log hello vengono sempre generati (esito positivo o negativo).  

    > [!IMPORTANT]
    > È consigliabile non impostare tooAlways questa proprietà in un ambiente di produzione a meno che non si sta risolvendo un problema. 
- Hello **restituisce** sezione ha un set di dati di output. Anche se il programma di spark hello non genera alcun output, è necessario specificare un set di dati di output. pianificazione di hello unità per set di dati di output Hello per pipeline hello (oraria, giornaliera, e così via.).

Per ulteriori informazioni sulle attività hello, vedere [attività Spark](data-factory-spark.md) articolo.  

## <a name="machine-learning-batch-execution-activity"></a>Attività di esecuzione batch di Machine Learning
È possibile specificare le proprietà in una definizione di Azure ML Batch esecuzione attività JSON seguenti hello. deve essere di proprietà del tipo Hello attività hello: **AzureMLBatchExecution**. È necessario creare un Azure Machine Learning innanzitutto il servizio collegato e specificare il nome di hello di esso come un valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooAzureMLBatchExecution attività:

Proprietà | Descrizione | Obbligatorio 
-------- | ----------- | --------
webServiceInput | Hello toobe di set di dati passato come input per hello servizio web di Azure ML. Questo set di dati deve essere incluso anche in input hello per attività hello. |Usare webServiceInput o webServiceInputs. | 
webServiceInputs | Specificare i set di dati toobe passate come input per hello servizio web di Azure ML. Se il servizio web hello accetta più input, è possibile utilizzare proprietà webServiceInputs hello anziché proprietà WebServiceInputActivity hello. Set di dati che fanno riferimento hello **webServiceInputs** deve essere incluso anche in attività hello **input**. | Usare webServiceInput o webServiceInputs. | 
webServiceOutputs | Hello set di dati che vengono assegnati come output per il servizio web di Azure ML hello. servizio web Hello restituisce i dati di output in questo set di dati. | Sì | 
globalParameters | Specificare i valori per parametri del servizio web hello in questa sezione. | No | 

### <a name="json-example"></a>Esempio di JSON
In questo esempio, attività hello presenta dataset hello **MLSqlInput** come input e **MLSqlOutput** come output di hello. Hello **MLSqlInput** viene passato come un servizio web di input toohello da utilizzando hello **WebServiceInputActivity** proprietà JSON. Hello **MLSqlOutput** viene passato come un servizio Web toohello di output da utilizzando hello **webserviceoutputs della** proprietà JSON. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

Nell'esempio hello JSON hello distribuito Azure Machine Learning Web servizio utilizza un lettore e un writer modulo tooread/scrittura di dati da / tooan Database SQL di Azure. Questo servizio Web espone hello seguenti quattro parametri: nome del server, nome del Database, nome Server dell'account utente e password dell'account utente Server di Database.

> [!NOTE]
> Solo input e output dell'attività AzureMLBatchExecution hello possono essere passati come parametri toohello servizio Web. Ad esempio, in hello sopra frammento di codice JSON, MLSqlInput è un input toohello AzureMLBatchExecution attività, che viene passato come un input toohello servizio Web tramite un parametro webServiceInput.

## <a name="machine-learning-update-resource-activity"></a>Attività della risorsa di aggiornamento di Machine Learning
È possibile specificare hello seguenti proprietà in una definizione di Azure ML aggiornamento risorsa attività JSON. deve essere di proprietà del tipo Hello attività hello: **AzureMLUpdateResource**. È necessario creare un Azure Machine Learning innanzitutto il servizio collegato e specificare il nome di hello di esso come un valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooAzureMLUpdateResource attività:

Proprietà | Descrizione | Obbligatorio 
-------- | ----------- | --------
trainedModelName | Nome di hello ripetere il training del modello. | Sì |  
trainedModelDatasetName | Set di dati puntamento toohello iLearner file restituito dall'operazione di ripetizione di training hello. | Sì | 

### <a name="json-example"></a>Esempio di JSON
Hello pipeline dispone di due attività: **AzureMLBatchExecution** e **AzureMLUpdateResource**. l'attività di esecuzione Batch di Azure ML Hello accetta i dati di training hello come input e genera un file iLearner come output. attività Hello richiama il servizio web di formazione hello (esperimento di training esposta come servizio web) con input hello i dati di training e riceve file ilearner hello dal servizio Web hello. placeholderBlob Hello è solo un set di dati del fittizio output richiesto dalla pipeline di hello toorun di hello Data Factory di Azure del servizio.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Attività U-SQL di Data Lake Analytics
È possibile specificare le proprietà in una definizione del formato JSON dell'attività U-SQL seguenti hello. deve essere di proprietà del tipo Hello attività hello: **DataLakeAnalyticsU SQL**. È necessario creare un servizio di Azure Data Lake Analitica collegato e specificare il nome di hello di esso come un valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di attività tooDataLakeAnalyticsU-SQL: 

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| scriptPath |Toofolder percorso che contiene lo script hello U-SQL. Nome del file hello è tra maiuscole e minuscole. |No (se si usa uno script) |
| scriptLinkedService |Servizio collegato che si collega archiviazione hello che contiene una data factory di hello script toohello |No (se si usa uno script) |
| script |Specificare lo script inline anziché scriptPath e scriptLinkedService. Ad esempio: "script": "CREATE DATABASE test". |No (se si usano le proprietà scriptPath e scriptLinkedService) |
| degreeOfParallelism |numero massimo di Hello di nodi utilizzati contemporaneamente processo hello toorun. |No |
| priority |Determina innanzitutto quali processi, tra tutti quelli accodati devono essere toorun selezionato. Hello hello numero inferiore, priorità più alta hello hello. |No |
| parameters |Parametri per hello U-SQL script |No |

### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Per altre informazioni, vedere [Attività Data Lake Analytics U-SQL](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Attività stored procedure
È possibile specificare hello seguenti proprietà in una definizione di Stored Procedure formato JSON dell'attività. deve essere di proprietà del tipo Hello attività hello: **SqlServerStoredProcedure**. È necessario creare un uno dei seguenti servizi collegati hello e specificare il nome di hello del servizio hello collegato come un valore per hello **linkedServiceName** proprietà:

- SQL Server 
- Database SQL di Azure
- Azure SQL Data Warehouse

salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooSqlServerStoredProcedure attività:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| storedProcedureName |Specificare il nome di hello della routine di hello archiviato nel database di SQL Azure hello o Azure SQL Data Warehouse è rappresentato dal servizio hello collegato che Usa tabella di output di hello. |Sì |
| storedProcedureParameters |Specificare i valori dei parametri della stored procedure. Se è necessario toopass null per un parametro, utilizzare la sintassi di hello: "param1": null (lettere minuscole). Vedere hello seguente toolearn esempio sull'utilizzo di questa proprietà. |No |

Se si specifica un set di dati di input, deve essere disponibile (in stato "Pronto") per hello stored procedure toorun di attività. set di dati Hello input non può essere utilizzato nella procedura hello archiviato come parametro. È solo toocheck utilizzati hello dipendenza prima hello Inizia attività stored procedure. È necessario specificare un set di dati di output per un'attività della stored procedure. 

Set di dati di output specifica hello **pianificazione** per hello attività stored procedure (ogni ora, settimanale, mensile, ecc.). Hello set di dati di output deve utilizzare un **servizio collegato** che fa riferimento tooan Database SQL di Azure o di un Data Warehouse di SQL Azure o di un Database di SQL Server in cui si desidera hello toorun stored procedure. Hello set di dati di output può essere utilizzato come un risultato hello toopass modo procedure hello archiviato per l'elaborazione successiva da un'altra attività ([concatenamento di attività](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) nella pipeline hello. Tuttavia, Data Factory non scrive automaticamente output di hello di un set di dati toothis stored procedure. È hello stored procedure di scritture tooa SQL tabella punti di set di dati di output di hello. In alcuni casi, il set di dati di hello output può essere un **set di dati fittizio**, che viene utilizzato solo pianificazione hello toospecify per l'esecuzione di hello attività stored procedure.  

### <a name="json-example"></a>Esempio di JSON

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Per altre informazioni, vedere [Attività stored procedure](data-factory-stored-proc-activity.md). 

## <a name="net-custom-activity"></a>Attività personalizzata .NET
È possibile specificare le proprietà in un'attività personalizzata .NET definizione JSON seguenti hello. deve essere di proprietà del tipo Hello attività hello: **DotNetActivity**. È necessario creare un servizio collegato di HDInsight di Azure o un Batch di Azure collegato del servizio e specificare il nome di hello del servizio collegato hello come valore per hello **linkedServiceName** proprietà. salve le proprietà seguenti sono supportate in hello **typeProperties** sezione quando si imposta il tipo di hello di tooDotNetActivity attività:
 
| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| AssemblyName | Nome dell'assembly hello. Nell'esempio hello è: **MyDotnetActivity.dll**. | Sì |
| EntryPoint |Nome della classe hello che implementa l'interfaccia IDotNetActivity hello. Nell'esempio hello è: **MyDotNetActivityNS.MyDotNetActivity** dove MyDotNetActivityNS è lo spazio dei nomi hello e MyDotNetActivity è la classe hello.  | Sì | 
| PackageLinkedService | Nome del servizio collegato di archiviazione di Azure che punta toohello archiviazione di blob che contiene i file zip di attività personalizzata hello hello. Nell'esempio hello è: **AzureStorageLinkedService**.| Sì |
| PackageFile | Nome del file zip hello. Nell'esempio hello è: **customactivitycontainer/MyDotNetActivity.zip**. | Sì |
| extendedProperties | Proprietà estese che è possibile definire e passare al codice .NET toohello. In questo esempio hello **SliceStart** variabile è impostata un valore tooa in base alla variabile di sistema SliceStart hello. | No | 

### <a name="json-example"></a>Esempio di JSON

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Per altre informazioni, vedere l'articolo relativo all'[uso delle attività personalizzate in Data Factory](data-factory-use-custom-activities.md). 

## <a name="next-steps"></a>Passaggi successivi
Vedere hello seguenti esercitazioni: 

- [Esercitazione: Creare una pipeline con un'attività di copia](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Esercitazione: Creare una pipeline con un'attività di Hive](data-factory-build-your-first-pipeline-using-editor.md)