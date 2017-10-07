---
title: aaaBuild la prima data factory (PowerShell) | Documenti Microsoft
description: In questa esercitazione viene creata una pipeline di esempio di Azure Data Factory usando Azure PowerShell.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Esercitazione: Creare la prima data factory di Azure con Azure PowerShell
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-build-your-first-pipeline.md)
> * [Portale di Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

In questo articolo, utilizzare Azure PowerShell toocreate prima data factory di Azure. esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello.

pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**. Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input. pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine. 

> [!NOTE]
> pipeline di dati Hello in questa esercitazione Trasforma i dati di output tooproduce di dati di input. Non copia dati da un archivio dati di origine dati archivio tooa destinazione. Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Prerequisiti
* Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.
* Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall versione più recente di Azure PowerShell nel computer in uso.
* (facoltativo) In questo articolo non copre tutti i cmdlet di hello Data Factory. Vedere [Riferimento ai cmdlet di Data factory](/powershell/module/azurerm.datafactories) per la documentazione completa sui cmdlet di Data factory.

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
In questo passaggio, si usa Azure PowerShell toocreate una Data Factory di Azure denominato **FirstDataFactoryPSH**. Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Dati di input, ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive. Iniziamo con la creazione di data factory di hello in questo passaggio.

1. Avviare PowerShell di Azure ed eseguire hello comando seguente. Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell. Se si chiude e riapre, è necessario toorun questi comandi nuovamente.
   * Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione. La sottoscrizione deve essere hello uguali a quelli hello usato nel portale di Azure hello.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando seguente:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Alcuni dei passaggi di hello in questa esercitazione si supponga di utilizza il gruppo di risorse di hello denominato ADFTutorialResourceGroup. Se si utilizza un gruppo di risorse diverso, è necessario toouse, al posto di ADFTutorialResourceGroup in questa esercitazione.
3. Eseguire hello **New AzureRmDataFactory** cmdlet che crea una factory di dati denominata **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Si noti hello seguenti punti:

* nome Hello di hello Azure Data Factory deve essere globalmente univoco. Se viene visualizzato l'errore hello **"FirstDataFactoryPSH" nome della Data factory non è disponibile**, modificare il nome di hello (ad esempio, yournameFirstDataFactoryPSH). Durante l'esecuzione di passaggi in questa esercitazione usare questo nome anziché ADFTutorialFactoryPSH. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .
* le istanze di Data Factory toocreate, è necessario toobe un amministratore o un collaboratore di hello sottoscrizione di Azure
* nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.
* Se viene visualizzato l'errore hello: "**questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory**", effettuare una delle seguenti hello e riprovare:

  * In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è stato registrato:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Account di accesso tramite hello sottoscrizione di Azure in hello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o). Questa azione registra automaticamente i provider di hello.

Prima di creare una pipeline, è necessario toocreate alcune entità Data Factory prima. Creare innanzitutto i dati di servizi collegati toolink archivi/calcola tooyour dati archiviano, definiscono l'input e output dei dati di input/output toorepresent di set di dati in archivi dati collegato e quindi creare pipeline hello con un'attività che utilizza questi set di dati.

## <a name="create-linked-services"></a>Creare servizi collegati
In questo passaggio è collegare l'account di archiviazione di Azure e una factory del dati tooyour cluster Azure HDInsight su richiesta. contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio. servizio collegato di HDInsight Hello è toorun usato uno script Hive specificato nell'attività hello della pipeline hello in questo esempio. Identificazione dei dati archivio/calcolo servizi vengono utilizzati nello scenario e collegano tali toohello data factory di servizi mediante la creazione di servizi collegati.

### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
In questo passaggio si collega la data factory tooyour account di archiviazione di Azure. Utilizzare hello stesso account di archiviazione di Azure i dati di input/output toostore e hello HQL file di script.

1. Creare un file JSON denominato StorageLinkedService.json nella cartella C:\ADFGetStarted hello con hello seguente contenuto. Creare la cartella hello ADFGetStarted se non esiste già.

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    Sostituire **nome account** con nome hello dell'account di archiviazione di Azure e **chiave dell'account** con la chiave di accesso hello di hello account di archiviazione di Azure. toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. In Azure PowerShell, passare toohello ADFGetStarted cartella.
3. È possibile utilizzare hello **New AzureRmDataFactoryLinkedService** cmdlet che crea un servizio collegato. Questo cmdlet e gli altri cmdlet di Data Factory da usare in questa esercitazione richiede valori toopass per hello *ResourceGroupName* e *DataFactoryName* parametri. In alternativa, è possibile utilizzare **Get AzureRmDataFactory** tooget un **DataFactory** , quindi passare l'oggetto hello senza digitare *ResourceGroupName* e  *DataFactoryName* ogni volta che si esegue un cmdlet. Comando che segue hello fase output di hello tooassign di hello **Get AzureRmDataFactory** cmdlet tooa **$df** variabile.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. A questo punto, eseguire hello **New AzureRmDataFactoryLinkedService** cmdlet che crea hello collegato **StorageLinkedService** servizio.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Se non è stato eseguito hello **Get AzureRmDataFactory** cmdlet e hello assegnato output toohello **$df** variabile, sarebbe necessario valori toospecify per hello *ResourceGroupName*e *DataFactoryName* parametri come indicato di seguito.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Se si chiude Azure PowerShell centro hello di esercitazione hello, è necessario hello toorun **Get AzureRmDataFactory** cmdlet successivo avvio di esercitazione hello toocomplete di Azure PowerShell.

### <a name="create-azure-hdinsight-linked-service"></a>Creare un servizio collegato Azure HDInsight
In questo passaggio si collega una factory del dati tooyour cluster HDInsight su richiesta. cluster HDInsight Hello viene automaticamente creato in fase di esecuzione ed eliminato al termine per l'elaborazione e inattività per l'intervallo di tempo specificato hello. È possibile usare il proprio cluster HDInsight anziché un cluster HDInsight su richiesta. Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .

1. Creare un file JSON denominato **HDInsightOnDemandLinkedService**JSON in hello **C:\ADFGetStarted** cartella con hello dopo contenuto.

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
    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

   | Proprietà | Descrizione |
   |:--- |:--- |
   | ClusterSize |Specifica dimensioni hello del cluster HDInsight hello. |
   | TimeToLive |Specifica il tempo di inattività hello per il cluster HDInsight hello, prima che venga eliminato. |
   | linkedServiceName |Specifica l'account di archiviazione hello toostore utilizzati hello registri generati da HDInsight |

    Si noti hello seguenti punti:

   * Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello JSON. Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
   * È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta. Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
   * Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (**timeToLive**). cluster Hello viene eliminato automaticamente quando viene eseguita un'elaborazione hello.

       Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.

     Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
2. Eseguire hello **New AzureRmDataFactoryLinkedService** cmdlet che crea hello collegato servizio denominato HDInsightOnDemandLinkedService.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Creare set di dati
In questo passaggio creare set di dati toorepresent hello input e output dei dati per l'elaborazione Hive. Questi set di dati di riferimento toohello **StorageLinkedService** creata precedentemente in questa esercitazione. Hello tooan punti di servizio collegato account di archiviazione di Azure e i set di dati specificare contenitore, cartella, nome del file nell'archiviazione hello che contiene l'input e output di dati.

### <a name="create-input-dataset"></a>Creare set di dati di input
1. Creare un file JSON denominato **InputTable.json** in hello **C:\ADFGetStarted** cartella con hello seguente contenuto:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    Hello JSON definisce un set di dati denominato **AzureBlobInput**, che rappresenta i dati di input per un'attività nella pipeline hello. Inoltre, specifica che i dati di input hello si trovano nel contenitore di blob hello chiamato **adfgetstarted** e cartella hello denominata **inputdata**.

    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

   | Proprietà | Descrizione |
   |:--- |:--- |
   | type |proprietà tipo Hello è impostato tooAzureBlob perché risiedono dati nell'archiviazione blob di Azure. |
   | linkedServiceName |si riferisce toohello StorageLinkedService creato in precedenza. |
   | fileName |Questa proprietà è facoltativa. Se si omette questa proprietà, vengono selezionati tutti i file hello folderPath hello. In questo caso, viene elaborato solo hello input.log. |
   | type |file di log Hello sono in formato testo, permette di usare TextFormat. |
   | columnDelimiter |le colonne nei file di log hello sono delimitate dal carattere virgola di hello (,). |
   | frequenza/intervallo |frequenza impostata tooMonth e l'intervallo è 1, che significa che le sezioni di input hello sono disponibili ogni mese. |
   | external |Questa proprietà è impostata tootrue se i dati di input hello non viene generati dal servizio Data Factory hello. |
2. Eseguire hello comando nel set di dati Data Factory hello toocreate Azure PowerShell seguente:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Creare il set di dati di output
È quindi possibile creare hello output dataset toorepresent hello output dati archiviati in archiviazione Blob di Azure hello.

1. Creare un file JSON denominato **OutputTable.json** in hello **C:\ADFGetStarted** cartella con hello seguente contenuto:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    Hello JSON definisce un set di dati denominato **AzureBlobOutput**, che rappresenta i dati di output per un'attività nella pipeline hello. Inoltre, specifica che i risultati di hello vengono archiviati nel contenitore blob hello chiamato **adfgetstarted** e cartella hello denominata **partitioneddata**. Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotto su base mensile.
2. Eseguire hello comando nel set di dati Data Factory hello toocreate Azure PowerShell seguente:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>Creare una pipeline
In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** . Sezione di input è disponibile ogni mese (frequenza: mese, intervallo: 1), sezione di output viene prodotta ogni mese e hello dell'utilità di pianificazione per l'attività hello viene anche impostata toomonthly. le impostazioni di Hello per set di dati output hello e utilità di pianificazione attività hello devono corrispondere. Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output. Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione. proprietà Hello utilizzate nei hello JSON seguente sono illustrate alla fine di hello in questa sezione.

1. Creare un file JSON denominato MyFirstPipelinePSH.json nella cartella C:\ADFGetStarted hello con hello seguente contenuto:

   > [!IMPORTANT]
   > Sostituire **storageaccountname** con nome hello dell'account di archiviazione in hello JSON.
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    Nel frammento di codice JSON hello, si sta creando una pipeline che è costituito da una singola attività che utilizza Hive tooprocess dati in un cluster HDInsight.

    file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **StorageLinkedService**) e in **script**  cartella nel contenitore hello **adfgetstarted**.

    Hello **definisce** sezione è le impostazioni di runtime hello toospecify utilizzati che essere passato script hive toohello come valori di configurazione di Hive (ad esempio ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

    Hello **avviare** e **fine** le proprietà della pipeline hello specifica periodo attivo di hello della pipeline hello.

    In formato JSON dell'attività hello, specificare tale script Hive hello viene eseguito sul calcolo hello specificato da hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Vedere la sezione "JSON di Pipeline" in [pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md) per dettagli sulle proprietà JSON che vengono utilizzati nell'esempio hello.

2. Assicurarsi di visualizzare hello **input.log** file hello **adfgetstarted/inputdata** cartella hello archiviazione blob di Azure e hello fase della pipeline hello toodeploy dei comandi seguenti. Poiché hello **avviare** e **fine** volte in cui vengono impostate in hello precedente e **isPaused** è toofalse set, pipeline hello esecuzioni (attività nella pipeline hello) immediatamente dopo la distribuzione.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. La creazione della prima pipeline tramite Azure PowerShell è così completata.

## <a name="monitor-pipeline"></a>Monitorare la pipeline
In questo passaggio, utilizzare Azure PowerShell toomonitor cosa accade in un data factory di Azure.

1. Eseguire **Get AzureRmDataFactory** e assegnare hello output tooa **$df** variabile.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Eseguire **Get AzureRmDataFactorySlice** tooget dettagli su tutte le sezioni di hello **EmpSQLTable**, che è una tabella di output di hello della pipeline hello.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    Si noti che è possibile specificare StartDateTime hello hello che stessa ora di inizio specificata in formato JSON della pipeline hello. Ecco l'output di esempio hello:

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Eseguire **Get AzureRmDataFactoryRun** tooget hello dettagli dell'attività viene eseguita per una specifica sezione.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Ecco l'output di esempio hello: 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    È possibile mantenere in esecuzione questo cmdlet finché non viene visualizzata la sezione hello in **pronto** stato o **Failed** stato. Quando la sezione hello è nello stato pronto, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.  La creazione di un cluster HDInsight su richiesta di solito richiede tempo.

    ![Dati di output](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti). Pertanto, prevedere hello pipeline tootake **circa 30 minuti** tooprocess hello sezione.
>
> file di input Hello eliminato quando la sezione hello viene elaborata correttamente. Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.
>
>

## <a name="summary"></a>Riepilogo
In questa esercitazione, creato un Azure factory tooprocess dati tramite l'esecuzione di script Hive in un cluster di HDInsight hadoop. È stato utilizzato hello Editor delle Data Factory in hello toodo portale Azure hello alla procedura seguente:

1. Creare un'istanza di Azure **Data Factory**.
2. Creare due **servizi collegati**:
   1. **Archiviazione di Azure** collegati toolink servizio di archiviazione blob di Azure che contiene una data factory toohello di file di input/output.
   2. **Azure HDInsight** toolink servizio collegato su richiesta di una factory del dati toohello cluster HDInsight Hadoop su richiesta. Data Factory di Azure crea un HDInsight Hadoop dati di input tooprocess just-in-time di cluster e generare dati di output.
3. Creare due **set di dati**, che descrivono i dati di input e outpui per l'attività Hive di HDInsight nella pipeline hello.
4. Creare una **pipeline** con un'attività **Hive di HDInsight**.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta di Azure. toosee toouse un dati toocopy attività di copia da un tooAzure Blob di Azure SQL, vedere [esercitazione: copiare i dati da un tooAzure Blob di Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Vedere anche
| Argomento | Descrizione |
|:--- |:--- |
| [Informazioni di riferimento sui cmdlet di Data factory](/powershell/module/azurerm.datafactories) |Vedere la documentazione completa sui cmdlet di Data factory |
| [Pipeline](data-factory-create-pipelines.md) |In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda. |
| [Set di dati](data-factory-create-datasets.md) |Questo articolo fornisce informazioni sui set di dati in Azure Data Factory. |
| [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) |Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory. |
| [Monitorare e gestire le pipeline con l'app di monitoraggio](data-factory-monitor-manage-app.md) |In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App. |
