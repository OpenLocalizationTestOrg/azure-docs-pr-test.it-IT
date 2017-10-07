---
title: aaaBuild la prima data factory (REST) | Documenti Microsoft
description: In questa esercitazione viene creata una pipeline di esempio di Azure Data Factory usando l'API REST di Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Esercitazione: Creare la prima data factory di Azure usando l'API REST di Data Factory
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-build-your-first-pipeline.md)
> * [Portale di Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


In questo articolo, utilizzare API REST di Data Factory toocreate prima data factory di Azure. esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello.

pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**. Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input. pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine.

> [!NOTE]
> In questo articolo non copre tutti hello API REST. Per una documentazione completa sull'API REST, vedere [Data Factory REST API Reference](/rest/api/datafactory/) (Informazioni di riferimento sull'API REST di Data Factory).
> 
> Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a>Prerequisiti
* Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.
* Installare [Curl](https://curl.haxx.se/dlwiz/) nel computer. Lo strumento di CURL hello con altri comandi toocreate una data factory.
* Seguire le istruzioni disponibili in [questo articolo](../azure-resource-manager/resource-group-create-service-principal-portal.md) per:
  1. Creare un'applicazione Web denominata **ADFGetStartedApp** in Azure Active Directory.
  2. Ottenere i valori per l'**ID client** e la **chiave privata**.
  3. Ottenere l' **ID tenant**.
  4. Assegnare hello **ADFGetStartedApp** applicazione toohello **Data Factory collaboratore** ruolo.
* Installare [Azure PowerShell](/powershell/azure/overview).
* Avviare **PowerShell** e hello esecuzione comando seguente. Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell. Se si chiude e riapre, è necessario comandi hello toorun nuovamente.
  1. Eseguire **accesso AzureRmAccount** e immettere nome utente hello e la password usati toosign in toohello portale di Azure.
  2. Eseguire **Get AzureRmSubscription** tooview tutti hello sottoscrizioni per questo account.
  3. Eseguire **AzureRmSubscription di Get - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** sottoscrizione hello tooselect da toowork con. Sostituire **NameOfAzureSubscription** con nome hello della sottoscrizione Azure.
* Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando in hello PowerShell seguente:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   Alcuni dei passaggi di hello in questa esercitazione si supponga di utilizza il gruppo di risorse di hello denominato ADFTutorialResourceGroup. Se si utilizza un gruppo di risorse diverso, è necessario il nome hello toouse del gruppo di risorse al posto di ADFTutorialResourceGroup in questa esercitazione.

## <a name="create-json-definitions"></a>Creare le definizioni JSON
Creare i seguenti file JSON nella cartella hello curl.exe in cui si trova.

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nome deve essere globalmente univoco, pertanto è consigliabile toomake ADFCopyTutorialDF tooprefix/suffisso è un nome univoco.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Sostituire **accountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure. toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

| Proprietà | Descrizione |
|:--- |:--- |
| ClusterSize |Dimensioni del cluster HDInsight hello. |
| TimeToLive |Specifica il tempo di inattività hello per il cluster HDInsight hello, prima che venga eliminato. |
| linkedServiceName |Specifica l'account di archiviazione hello toostore utilizzati hello registri generati da HDInsight |

Si noti hello seguenti punti:

* Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello sopra JSON. Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
* È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta. Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato di HDInsight su richiesta, un cluster HDInsight viene creato ogni volta che viene elaborata una sezione a meno che non vi è un cluster esistente in tempo reale (**timeToLive**) e viene eliminata quando viene eseguita un'elaborazione hello.

    Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.

Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
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

Hello JSON definisce un set di dati denominato **AzureBlobInput**, che rappresenta i dati di input per un'attività nella pipeline hello. Inoltre, specifica che i dati di input hello si trovano nel contenitore di blob hello chiamato **adfgetstarted** e cartella hello denominata **inputdata**.

Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

| Proprietà | Descrizione |
|:--- |:--- |
| type |proprietà tipo Hello è impostato tooAzureBlob perché risiedono dati nell'archiviazione blob di Azure. |
| linkedServiceName |si riferisce toohello StorageLinkedService creato in precedenza. |
| fileName |Questa proprietà è facoltativa. Se si omette questa proprietà, vengono selezionati tutti i file hello folderPath hello. In questo caso, viene elaborato solo hello input.log. |
| type |file di log Hello sono in formato testo, permette di usare TextFormat. |
| columnDelimiter |nei file di log hello colonne sono delimitate da una virgola () |
| frequenza/intervallo |frequenza impostata tooMonth e l'intervallo è 1, che significa che le sezioni di input hello sono disponibili ogni mese. |
| external |Questa proprietà è impostata tootrue se i dati di input hello non viene generati dal servizio Data Factory hello. |

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Sostituire **storageaccountname** con il nome del proprio account di archiviazione di Azure.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

Nel frammento di codice JSON hello, si sta creando una pipeline che è costituito da una singola attività che utilizza dati tooprocess Hive in un cluster HDInsight.

file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **StorageLinkedService**) e in **script**  cartella nel contenitore hello **adfgetstarted**.

Hello **definisce** sezione specifica le impostazioni di runtime script hive toohello passati come valori di configurazione di Hive (ad esempio ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

Hello **avviare** e **fine** le proprietà della pipeline hello specifica periodo attivo di hello della pipeline hello.

In formato JSON dell'attività hello, specificare tale script Hive hello viene eseguito sul calcolo hello specificato da hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.

> [!NOTE]
> Vedere la sezione "JSON di Pipeline" in [pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md) per dettagli sulle proprietà JSON utilizzato in hello sopra riportato.
>
>

## <a name="set-global-variables"></a>Configurare le variabili globali
In Azure PowerShell, eseguire hello seguenti comandi dopo la sostituzione di valori hello con valori personalizzati:

> [!IMPORTANT]
> Per istruzioni su come ottenere i valori per ID client, segreto client, ID tenant e ID sottoscrizione, vedere la sezione [Prerequisiti](#prerequisites) .
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Eseguire l'autenticazione con AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
In questo passaggio viene creata un'istanza di Azure Data Factory denominata **FirstDataFactoryREST**. Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Ad esempio, un'attività di copia toocopy i dati da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform di dati di script Hive. Eseguire hello data factory di comandi toocreate hello seguenti:

1. Assegnare toovariable comando hello denominato **cmd**.

    Verificare che nome hello di hello data factory specificato (ADFCopyTutorialDF) corrispondenze hello nome specificato in hello **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se hello data factory è stata creata correttamente, viene visualizzato hello JSON per data factory di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.

    ```PowerShell
    Write-Host $results
    ```

Si noti hello seguenti punti:

* nome Hello di hello Azure Data Factory deve essere globalmente univoco. Se viene visualizzato l'errore hello nei risultati: **"FirstDataFactoryREST" nome della Data factory non è disponibile**, hello i passaggi seguenti:
  1. Modifica il nome hello (ad esempio, yournameFirstDataFactoryREST) in hello **datafactory.json** file. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .
  2. Nel primo comando hello in hello **$cmd** variabile viene assegnato un valore, sostituire FirstDataFactoryREST con nome hello ed eseguire il comando di hello.
  3. Eseguire hello due comandi successivi tooinvoke hello API REST toocreate hello data factory e stampa hello risultati dell'operazione di hello.
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

Prima di creare una pipeline, è necessario toocreate alcune entità Data Factory prima. Creare innanzitutto i dati di servizi collegati toolink archivi/calcola tooyour dati archiviano, definiscono l'input e output dati toorepresent set di dati in archivi dati collegati.

## <a name="create-linked-services"></a>Creare servizi collegati
In questo passaggio è collegare l'account di archiviazione di Azure e una factory del dati tooyour cluster Azure HDInsight su richiesta. contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio. servizio collegato di HDInsight Hello è toorun usato uno script Hive specificato nell'attività hello della pipeline hello in questo esempio.

### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
In questo passaggio si collega la data factory tooyour account di archiviazione di Azure. In questa esercitazione, si utilizza hello stesso account di archiviazione di Azure i dati di input/output toostore e hello HQL file di script.

1. Assegnare toovariable comando hello denominato **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se collegato hello servizio è stato creato correttamente, hello JSON per il servizio collegato hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Creare un servizio collegato Azure HDInsight
In questo passaggio si collega una factory del dati tooyour cluster HDInsight su richiesta. cluster HDInsight Hello viene automaticamente creato in fase di esecuzione ed eliminato al termine per l'elaborazione e inattività per l'intervallo di tempo specificato hello. È possibile usare il proprio cluster HDInsight anziché un cluster HDInsight su richiesta. Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .

1. Assegnare toovariable comando hello denominato **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se collegato hello servizio è stato creato correttamente, hello JSON per il servizio collegato hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Creare set di dati
In questo passaggio creare set di dati toorepresent hello input e output dei dati per l'elaborazione Hive. Questi set di dati di riferimento toohello **StorageLinkedService** creata precedentemente in questa esercitazione. Hello tooan punti di servizio collegato account di archiviazione di Azure e i set di dati specificare contenitore, cartella, nome del file nell'archiviazione hello che contiene l'input e output di dati.

### <a name="create-input-dataset"></a>Creare set di dati di input
In questo passaggio è creare hello set di dati input toorepresent dati di input memorizzati nell'archiviazione Blob di Azure hello.

1. Assegnare toovariable comando hello denominato **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Creare il set di dati di output
In questo passaggio è creare hello output dataset toorepresent output dei dati archiviati in archiviazione Blob di Azure hello.

1. Assegnare toovariable comando hello denominato **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>Creare una pipeline
In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** . Sezione di input è disponibile ogni mese (frequenza: mese, intervallo: 1), sezione di output viene prodotta ogni mese e hello dell'utilità di pianificazione per l'attività hello viene anche impostata toomonthly. le impostazioni di Hello per set di dati output hello e utilità di pianificazione attività hello devono corrispondere. Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output. Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione.

Assicurarsi di visualizzare hello **input.log** file hello **adfgetstarted/inputdata** cartella hello archiviazione blob di Azure e hello fase della pipeline hello toodeploy dei comandi seguenti. Poiché hello **avviare** e **fine** volte in cui vengono impostate in hello precedente e **isPaused** è toofalse set, pipeline hello esecuzioni (attività nella pipeline hello) immediatamente dopo la distribuzione.

1. Assegnare toovariable comando hello denominato **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.

    ```PowerShell
    Write-Host $results
    ```
4. La creazione della prima pipeline tramite Azure PowerShell è così completata.

## <a name="monitor-pipeline"></a>Monitorare la pipeline
In questo passaggio è utilizzare le sezioni di toomonitor API REST di Data Factory viene generate dalla pipeline hello.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti). Pertanto, prevedere hello pipeline tootake **circa 30 minuti** tooprocess hello sezione.
>
>

Eseguire Invoke-Command hello e hello successivo finché non viene visualizzata la sezione hello in **pronto** stato o **Failed** stato. Quando la sezione hello è nello stato pronto, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.  creazione di Hello di un cluster di HDInsight su richiesta richiede in genere del tempo.

![Dati di output](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> file di input Hello eliminato quando la sezione hello viene elaborata correttamente. Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.
>
>

È inoltre possibile utilizzare le sezioni toomonitor portale Azure e risolvere eventuali problemi. Per i dettagli, vedere [Creare la prima data factory di Azure usando il portale di Azure/l'editor di Data Factory](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .

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
| [Informazioni di riferimento sull'API REST di Data Factory](/rest/api/datafactory/) |Vedere la documentazione completa sui cmdlet di Data factory |
| [Pipeline](data-factory-create-pipelines.md) |In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda. |
| [Set di dati](data-factory-create-datasets.md) |Questo articolo fornisce informazioni sui set di dati in Azure Data Factory. |
| [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) |Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory. |
| [Monitorare e gestire le pipeline con l'app di monitoraggio](data-factory-monitor-manage-app.md) |In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App. |
