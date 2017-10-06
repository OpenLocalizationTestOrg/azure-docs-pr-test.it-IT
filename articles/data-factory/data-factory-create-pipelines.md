---
title: "Pipeline di aaaCreate/pianificazione, le attività di catena in Data Factory | Documenti Microsoft"
description: Informazioni su una pipeline di dati in Azure Data Factory toomove toocreate e trasformare i dati. Creare un dati basato su informazioni toouse pronto tooproduce di flusso di lavoro.
keywords: pipeline di dati, flusso di lavoro basato sui dati
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Pipeline e attività in Azure Data Factory
In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e usarli tooconstruct end-to-end basato sui dati dei flussi di lavoro per lo spostamento dei dati e gli scenari di elaborazione dei dati.  

> [!NOTE]
> Questo articolo si presuppone che sia già stata consultata [tooAzure introduzione Data Factory](data-factory-introduction.md). Se non si ha esperienza diretta nella creazione di data factory, l'[esercitazione sulla trasformazione dei dati](data-factory-build-your-first-pipeline.md) e/o [quella sullo spostamento dei dati](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) può essere utile per comprendere meglio questo articolo.  

## <a name="overview"></a>Panoramica
Una data factory può comprendere una o più pipeline. Una pipeline è un raggruppamento logico di attività che insieme eseguono un compito. attività Hello in una pipeline definire tooperform azioni sui dati. Ad esempio, si potrebbero utilizzare un copia attività toocopy dati da un tooan di SQL Server on-premise archiviazione Blob di Azure. Quindi, utilizzare un'attività Hive che esegue uno script Hive in dati di tooprocess/trasformare un cluster Azure HDInsight da dati di output di hello blob archiviazione tooproduce. Infine, utilizzare una seconda copia attività toocopy hello output dati tooan Azure SQL Data Warehouse in cui la business intelligence (BI) soluzioni di report vengono compilate. 

Un'attività può non avere alcun [set di dati](data-factory-create-datasets.md) di input o può averne più di uno e generare uno o più [set di dati di output](data-factory-create-datasets.md). Hello diagramma seguente mostra hello relazione tra set di dati, pipeline e attività in Data Factory: 

![Relazione tra pipeline, attività e set di dati](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Una pipeline consente attività toomanage come set anziché ognuna singolarmente. Ad esempio, è possibile distribuire, pianificare, sospendere e riprendere una pipeline, anziché gestiscono le attività nella pipeline hello in modo indipendente.

Data Factory supporta due tipi di attività: attività di spostamento dei dati e attività di trasformazione dei dati. Ogni attività può non avere alcun [set di dati](data-factory-create-datasets.md) di input o può averne più di uno e generare uno o più set di dati di output.

Un set di dati di input rappresenta hello l'input per un'attività nella pipeline hello e un set di dati di output rappresenta l'output di hello per attività hello. I set di dati identificano i dati all'interno dei diversi archivi dati, come tabelle, file, cartelle e documenti. Dopo aver creato un set di dati, è possibile usarlo con le attività in una pipeline. Ad esempio, un set di dati può essere configurato come set di dati di input o di output di un'attività di copia o un'attività HDInsightHive. Per altre informazioni sui set di dati, vedere l'articolo [Set di dati in Azure Data Factory](data-factory-create-datasets.md).

### <a name="data-movement-activities"></a>Attività di spostamento dei dati
Attività di copia in Data Factory copia dati da un archivio dati di origine dati archivio tooa sink. Data Factory supporta hello seguenti archivi dati. È possibile scrivere dati da qualsiasi origine tooany sink. Fare clic su un toolearn archivio dati come toocopy tooand di dati dall'archivio.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Archivia i dati con * può essere locale o in Azure IaaS e richiedono tooinstall [Gateway di gestione dati](data-factory-data-management-gateway.md) in un computer di IaaS in locale o Azure.

Per altre informazioni, vedere l'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Attività di trasformazione dei dati
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Per altre informazioni, vedere l'articolo [Attività di trasformazione dei dati](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Attività .NET personalizzate 
Se sono necessari dati toomove a/da un tipo di dati archivio hello attività di copia non supporta, o trasformare i dati usando la logica personalizzata, creare un **attività .NET personalizzata**. Per i dettagli sulla creazione e l'uso di un'attività personalizzata, vedere l'articolo [Usare attività personalizzate in una pipeline di Azure Data Factory](data-factory-use-custom-activities.md).

## <a name="schedule-pipelines"></a>Pianificare le pipeline
Una pipeline è attiva solo tra l'ora di **inizio** e l'ora di **fine**. Non viene eseguita prima dell'ora di inizio hello o dopo l'ora di fine hello. Se la pipeline di hello è sospesa, non venga eseguito indipendentemente dal relativo ora di inizio e fine. Per toorun una pipeline, consigliabile non sospesa. Vedere [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) toounderstand funzionamento di pianificazione e l'esecuzione in Azure Data Factory.

## <a name="pipeline-json"></a>Pipeline JSON
Osserviamo più da vicino come viene definita una pipeline nel formato JSON. struttura generica di Hello per una pipeline è simile al seguente:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Tag | Descrizione | Obbligatorio |
| --- | --- | --- |
| name |Nome della pipeline hello. Specificare un nome che rappresenta l'azione di hello che hello pipeline esegue. <br/><ul><li>Numero massimo di caratteri: 260</li><li>Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</li><li>Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</li></ul> |Sì |
| description | Specificare il testo hello che descrive le pipeline hello viene utilizzata per. |Sì |
| attività | Hello **attività** sezione può avere uno o più attività definite all'interno di esso. Vedere hello sezione successiva per informazioni dettagliate sull'elemento di hello attività JSON. | Sì |  
| start | Data-ora di inizio per la pipeline di hello. Devono essere nel [formato ISO](http://en.wikipedia.org/wiki/ISO_8601), Ad esempio: `2016-10-14T16:32:41Z`. <br/><br/>È possibile toospecify un'ora locale, ad esempio un'ora EST. Di seguito viene riportato un esempio: `2016-02-27T06:00:00-05:00`, che indica le 06:00 EST.<br/><br/>Hello proprietà start ed end insieme specificano il periodo attivo per la pipeline di hello. Le sezioni di output vengono generate solo in questo periodo attivo. |No<br/><br/>Se si specifica un valore per la proprietà di fine hello, è necessario specificare una valore per la proprietà di avvio hello.<br/><br/>Hello ora di inizio e fine può essere entrambi vuoti toocreate una pipeline. È necessario specificare entrambi i valori tooset un periodo attivo per hello pipeline toorun. Se non si specifica l'ora di inizio e fine durante la creazione di una pipeline, è possibile impostare utilizzando il cmdlet Set-AzureRmDataFactoryPipelineActivePeriod hello in un secondo momento. |
| end | Data-ora di fine per la pipeline di hello. Se specificate, devono essere in formato ISO. Ad esempio: `2016-10-14T17:32:41Z` <br/><br/>È possibile toospecify un'ora locale, ad esempio un'ora EST. Di seguito è fornito l'esempio `2016-02-27T06:00:00-05:00`, che indica le 6 EST.<br/><br/>pipeline hello toorun specificare in modo indefinito, 9999-09-09 come valore di hello per la proprietà di fine hello. <br/><br/> Una pipeline è attiva solo tra l'ora di inizio e l’ora di fine. Non viene eseguita prima dell'ora di inizio hello o dopo l'ora di fine hello. Se la pipeline di hello è sospesa, non venga eseguito indipendentemente dal relativo ora di inizio e fine. Per toorun una pipeline, consigliabile non sospesa. Vedere [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) toounderstand funzionamento di pianificazione e l'esecuzione in Azure Data Factory. |No <br/><br/>Se si specifica un valore per la proprietà di avvio hello, è necessario specificare una valore per la proprietà di fine hello.<br/><br/>Vedere le note per hello **avviare** proprietà. |
| isPaused | Se non viene eseguito insieme tootrue, pipeline hello. È in hello stato sospeso. Valore predefinito = false. È possibile utilizzare questa proprietà tooenable o disabilitare una pipeline. |No |
| pipelineMode | metodo Hello per la pianificazione viene eseguita per la pipeline di hello. I valori consentiti sono scheduled (predefinito) e onetime.<br/><br/>'Pianificata' indica che pipeline hello viene eseguita in un intervallo di tempo specificato in base tooits periodo attivo (ora di inizio e fine). 'Unica' indica che pipeline hello viene eseguito una sola volta. Al momento, dopo aver creato una pipeline monouso non è possibile modificarla o aggiornarla. Per informazioni dettagliate sull'impostazione onetime, vedere la sezione [Pipeline monouso](#onetime-pipeline) . |No |
| expirationTime | Periodo di tempo dopo la creazione per i quali hello [pipeline monouso](#onetime-pipeline) sia valido e deve rimanere disponibile. Se non è attiva qualsiasi, non è riuscita, o in attesa di esecuzione, la pipeline hello viene automaticamente eliminato una volta raggiunge scadenza hello. valore predefinito di Hello:`"expirationTime": "3.00:00:00"`|No |
| set di dati |Elenco di set di dati toobe utilizzate dalle attività definite nella pipeline hello. Questa proprietà può essere utilizzato toodefine i set di dati sono pipeline toothis specifico e non è definito all'interno di data factory di hello. I set di dati definiti all'interno di questa pipeline possono essere usati solo da questa pipeline e non possono essere condivisi. Per informazioni dettagliate, vedere la sezione [Set di dati con ambito](data-factory-create-datasets.md#scoped-datasets) . |No |

## <a name="activity-json"></a>Attività JSON
Hello **attività** sezione può avere uno o più attività definite all'interno di esso. Ogni attività dispone di hello seguente struttura di livello principale:

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
    },
    "scheduler":
    {
    }
}
```

Nella tabella seguente vengono descritte le proprietà dell'attività hello definizione JSON:

| Tag | Descrizione | Obbligatorio |
| --- | --- | --- |
| name | Nome dell'attività hello. Specificare un nome che rappresenta l'azione di hello che esegue attività hello. <br/><ul><li>Numero massimo di caratteri: 260</li><li>Deve iniziare con una lettera, un numero o un carattere di sottolineatura (_)</li><li>Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\"</li></ul> |Sì |
| description | Testo che descrive le attività hello o viene utilizzate per |Sì |
| type | Tipo di attività hello. Vedere hello [attività lo spostamento dei dati](#data-movement-activities) e [le attività di trasformazione dati](#data-transformation-activities) sezioni per diversi tipi di attività. |Sì |
| inputs |Tabelle di input utilizzate dall'attività hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Sì |
| outputs |Tabelle di output utilizzate dall'attività hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Sì |
| linkedServiceName |Nome del servizio hello collegato usato dall'attività hello. <br/><br/>Un'attività potrebbe essere necessario specificare il servizio collegato hello che collega l'ambiente di calcolo necessarie toohello. |Sì per Attività di HDInsight e Attività di assegnazione punteggio batch di Azure Machine Learning  <br/><br/>No per tutto il resto |
| typeProperties |Le proprietà in hello **typeProperties** sezione dipendono dal tipo di attività hello. proprietà del tipo toosee per un'attività, fare clic su attività toohello collegamenti nella sezione precedente hello. | No |
| policy |Criteri che influiscono sul comportamento di hello in fase di esecuzione dell'attività hello. Se vengono omessi, vengono usati i criteri predefiniti. |No |
| scheduler | proprietà "utilità di pianificazione" è utilizzato toodefine desiderato pianificazione per l'attività hello. Le sottoproprietà sono hello stesso hello quelle nella hello [proprietà disponibilità in un set di dati](data-factory-create-datasets.md#dataset-availability). |No |


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

## <a name="sample-copy-pipeline"></a>Esempio di una pipeline di copia
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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Si noti hello seguenti punti:

* Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**.
* Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**. Vedere l'articolo [Set di dati](data-factory-create-datasets.md) per la definizione di set di dati in JSON. 
* In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello. In hello [attività lo spostamento dei dati](#data-movement-activities) fare clic su hello archivio dati che si vuole toouse come un'origine o un sink toolearn più sullo spostamento dei dati da e verso tale archivio dati. 

Per una descrizione completa della creazione di questa pipeline, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Esempio di una pipeline di trasformazione
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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Si noti hello seguenti punti: 

* Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**HDInsightHive**.
* file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **AzureStorageLinkedService**) e in  **script** cartella nel contenitore hello **adfgetstarted**.
* Hello `defines` sezione è le impostazioni di runtime hello toospecify utilizzati script hive toohello passati come valori di configurazione di Hive (ad esempio `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Hello **typeProperties** sezione è diversa per ogni attività di trasformazione. toolearn sulle proprietà del tipo supportato per un'attività di trasformazione, fare clic su attività di trasformazione hello in hello [le attività di trasformazione dati](#data-transformation-activities) tabella. 

Per una descrizione completa della creazione di questa pipeline, vedere [esercitazione: creare i primi dati tooprocess pipeline utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Attività multiple in una pipeline
pipeline di esempio due precedenti Hello avere una sola attività in essi contenuti. È possibile avere più di un'attività in una pipeline.  

Se si dispone di più attività in una pipeline e output di un'attività non è un input di un'altra attività, le attività di hello possono essere eseguite in parallelo se gli intervalli di dati di input per le attività di hello pronti. 

È possibile concatenare le due attività con i set di dati di un'attività come set di dati input hello di hello output di hello altre attività. seconda attività Hello viene eseguita solo se hello prima uno stato completato correttamente.

![Concatenamento di attività in hello stessa pipeline](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

In questo esempio, hello pipeline dispone di due attività: Activity1 e Activity2. accetta Dataset1 come input e produce un output di Hello Activity1 Dataset2. Hello attività accetta Dataset2 come input e produce un output Dataset3. Dall'output di hello di Activity1 (Dataset2) è input hello di Activity2, hello Activity2 viene eseguita solo dopo hello attività viene completata correttamente e produce hello sezione Dataset2. Se hello Activity1 per qualche motivo non riesce e non produce sezione hello Dataset2, hello attività 2 non viene eseguito per tale sezione (ad esempio: STO too10 AM 9). 

È anche possibile concatenare le attività che si trovano in pipeline diverse.

![Concatenamento di attività in due pipeline](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

In questo esempio, Pipeline1 ha una sola attività che accetta come input Dataset1 e genera come output Dataset2. Hello Pipeline2 dispone anche di una sola attività che accetta Dataset2 come input e Dataset3 come output. 

Per altre informazioni, vedere [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Creare e monitorare le pipeline
È possibile creare pipeline usando uno di questi strumenti o SDK. 

- Copia guidata. 
- Portale di Azure
- Visual Studio
- Azure PowerShell
- Modello di Azure Resource Manager
- API REST
- API .NET

Vedere hello seguenti esercitazioni per istruzioni dettagliate per la creazione di pipeline utilizzando uno di questi strumenti o il SDK.
 
- [Creare una pipeline con un'attività di trasformazione dati](data-factory-build-your-first-pipeline.md)
- [Creare una pipeline con un'attività di spostamento dati](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Una volta una pipeline creata distribuito, è possibile gestire e monitorare le pipeline utilizzando hello pannelli portali Azure o monitoraggio e gestione di App. Hello seguenti argomenti per informazioni dettagliate, vedere. 

- [Monitorare e gestire le pipeline con i pannelli del portale di Azure](data-factory-monitor-manage-pipelines.md).
- [Monitorare e gestire le pipeline con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Pipeline monouso
È possibile creare e pianificare un toorun pipeline periodicamente (ad esempio: su base oraria o giornaliera) all'interno di hello inizio e di fine specificate nella definizione di pipeline hello. Per informazioni dettagliate, vedere la sezione [Pianificazione delle attività](#scheduling-and-execution) . È anche possibile creare una pipeline che viene eseguita una sola volta. toodo in tal caso, si imposta hello **pipelineMode** proprietà hello pipeline definizione troppo**unica** come illustrato nel seguente esempio JSON hello. il valore predefinito Hello per questa proprietà è **pianificato**.

```json
{
    "name": "CopyPipeline",
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
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Si noti hello segue:

* **Avviare** e **fine** non sono specificati i tempi per la pipeline di hello.
* **Disponibilità** di input e output del set di dati è specificato (**frequenza** e **intervallo**), anche se non utilizza i valori hello Data Factory.  
* Le pipeline monouso non vengono visualizzate nella vista Diagramma. Questo comportamento dipende dalla progettazione.
* Le pipeline monouso non possono essere aggiornate. È possibile clonare una singola pipeline, rinominarlo, aggiornare le proprietà e distribuirlo toocreate un altro.


## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sui set di dati, vedere l'articolo [Creare i set di dati](data-factory-create-datasets.md). 
- Per altre informazioni sulle modalità di pianificazione ed esecuzione delle pipeline, vedere l'articolo [Pianificazione ed esecuzione in Azure Data Factory](data-factory-scheduling-and-execution.md). 
  

