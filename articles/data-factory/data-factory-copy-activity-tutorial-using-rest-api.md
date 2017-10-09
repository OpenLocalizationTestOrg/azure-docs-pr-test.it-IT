---
title: 'Esercitazione: Utilizzare l''API REST toocreate una pipeline di Data Factory di Azure | Documenti Microsoft'
description: "In questa esercitazione è utilizzare API REST toocreate una pipeline di Data Factory di Azure con i dati di toocopy un attività di copia da un archivio blob di Azure, un database SQL di Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Esercitazione: Utilizzare l'API REST toocreate un dati toocopy della pipeline di Data Factory di Azure 
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copia guidata](data-factory-copy-data-wizard-tutorial.md)
> * [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modello di Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

In questo articolo viene illustrato come toouse REST API toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure. Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.   

In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati. Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).

Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> In questo articolo non copre tutti hello API REST di Data Factory. Per la documentazione completa sui cmdlet di Data Factory, vedere [Informazioni di riferimento sull'API REST di Data Factory](/rest/api/datafactory/) .
>  
> pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione. Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Prerequisiti
* Seguire i passaggi [esercitazione Panoramica](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completo **prerequisito** passaggi.
* Installare [Curl](https://curl.haxx.se/dlwiz/) nel computer. Lo strumento di Curl hello con altri comandi toocreate una data factory. 
* Seguire le istruzioni disponibili in [questo articolo](../azure-resource-manager/resource-group-create-service-principal-portal.md) per: 
  1. Creare un'applicazione Web denominata **ADFCopyTutorialApp** in Azure Active Directory.
  2. Ottenere i valori per l'**ID client** e la **chiave privata**. 
  3. Ottenere l' **ID tenant**. 
  4. Assegnare hello **ADFCopyTutorialApp** applicazione toohello **Data Factory collaboratore** ruolo.  
* Installare [Azure PowerShell](/powershell/azure/overview).  
* Avviare **PowerShell** e hello i passaggi seguenti. Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell. Se si chiude e riapre, è necessario comandi hello toorun nuovamente.
  
  1. Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione. Sostituire  **&lt;NameOfAzureSubscription** &gt; con nome hello della sottoscrizione Azure. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando in hello PowerShell seguente:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Se il gruppo di risorse hello esiste già, specificare se tooupdate è (Y) o mantenerlo come (N). 
     
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
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Sostituire **accountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure. toolearn modalità di accesso di archiviazione di tooget chiave, vedere [visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

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

Per informazioni dettagliate sulle proprietà JSON, vedere [Servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Sostituire **servername**, **databasename**, **username**, e **password** con il nome del server SQL Azure, nome del database SQL, utente account e password per account hello.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Per informazioni dettagliate sulle proprietà JSON, vedere la sezione relativa al [servizio collegato SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

| Proprietà | Descrizione |
|:--- |:--- |
| type | proprietà tipo Hello è troppo**AzureBlob** perché i dati risiedono in una risorsa di archiviazione blob di Azure. |
| linkedServiceName | Fa riferimento toohello **AzureStorageLinkedService** creato in precedenza. |
| folderPath | Specifica il blob hello **contenitore** hello e **cartella** che contiene il BLOB di input. In questa esercitazione, adftutorial è il contenitore di blob hello e cartella è hello radice. | 
| fileName | Questa proprietà è facoltativa. Se si omette questa proprietà, vengono selezionati tutti i file da folderPath hello. In questa esercitazione, **emp.txt** specificato per hello fileName, in modo che solo tale file viene prelevato per l'elaborazione. |
| format -> type |file di input di Hello è in formato testo hello, permette di usare **TextFormat**. |
| columnDelimiter | Hello colonne nel file di input hello sono delimitate da **carattere virgola (`,`)**. |
| frequenza/intervallo | frequenza Hello è troppo**ora** e l'intervallo viene impostato troppo**1**, il che significa che hello di input sono disponibili sezioni **oraria**. In altre parole, hello servizio Data Factory esegue la ricerca di dati di input ogni ora nella cartella radice hello del contenitore di blob (**adftutorial**) specificato. La ricerca di dati hello all'interno di hello pipeline inizio e fine volte, non prima o dopo tali periodi.  |
| external | Questa proprietà è impostata troppo**true** se dati hello non viene generati da questa pipeline. dati di input Hello in questa esercitazione sono nel file di emp.txt hello, che non viene generato da questa pipeline, è necessario impostare tootrue questa proprietà. |

Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

| Proprietà | Descrizione |
|:--- |:--- |
| type | proprietà tipo Hello è troppo**AzureSqlTable** perché dati tabella tooa copiato in un database SQL di Azure. |
| linkedServiceName | Fa riferimento toohello **AzureSqlLinkedService** creato in precedenza. |
| tableName | Hello specificato **tabella** toowhich hello dati vengono copiati. | 
| frequenza/intervallo | Hello frequency è impostato troppo**ora** e l'intervallo è **1**, il che significa che vengono create le sezioni di output di hello **oraria** tra hello pipeline iniziale e finale volte, non prima o Dopo tali periodi.  |

Sono presenti tre colonne: **ID**, **FirstName**, e **LastName** : nella tabella emp hello nel database di hello. ID è una colonna identity, pertanto è necessario solo toospecify **FirstName** e **LastName** qui.

Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

Si noti hello seguenti punti:

- Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md). Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).
- Input per attività hello è troppo**AzureBlobInput** e di output per attività hello è troppo**AzureSqlOutput**. 
- In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello. Per un elenco completo degli archivi di dati supportati dall'attività di copia hello come origini e sink, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn sulla modalità di memorizzazione toouse dati specifici supportati come origine/sink, fare clic su collegamento hello nella tabella hello.  
 
Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo. È possibile specificare solo parte della data hello e Ignora parte dell'ora hello di hello data ora. Ad esempio, "2017-02-03", che equivale troppo "2017-02-03T00:00:00Z"
 
Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). ad esempio 2016-10-14T16:32:41Z. Hello **fine** è facoltativo, ma viene usata in questa esercitazione. 
 
Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**". specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.
 
In hello sopra riportato, sono presenti sezioni dati 24 come ogni sezione di dati viene prodotta ogni ora.

Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md). Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md). Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md). Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).

## <a name="set-global-variables"></a>Configurare le variabili globali
In Azure PowerShell, eseguire hello seguenti comandi dopo la sostituzione di valori hello con valori personalizzati:

> [!IMPORTANT]
> Per istruzioni su come ottenere i valori per ID client, segreto client, ID tenant e ID sottoscrizione, vedere la sezione [Prerequisiti](#prerequisites) .   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Eseguire hello comando seguente dopo l'aggiornamento del nome hello di hello data factory in uso: 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Eseguire l'autenticazione con AAD
Comando che segue di esecuzione hello tooauthenticate con Azure Active Directory (AAD): 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
In questo passaggio si crea un'istanza di Azure Data Factory denominata **ADFCopyTutorialDF**. Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Ad esempio, un attività di copia toocopy da un'origine di destinazione tooa archivio dati. Un toorun attività Hive di HDInsight un tootransform script Hive dati di output tooproduct di dati di input. Eseguire hello data factory di comandi toocreate hello seguenti: 

1. Assegnare toovariable comando hello denominato **cmd**. 
   
    > [!IMPORTANT]
    > Verificare che nome hello di hello data factory specificato (ADFCopyTutorialDF) corrispondenze hello nome specificato in hello **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se hello data factory è stata creata correttamente, viene visualizzato hello JSON per data factory di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.  
   
    ```
    Write-Host $results
    ```

Si noti hello seguenti punti:

* nome Hello di hello Azure Data Factory deve essere globalmente univoco. Se viene visualizzato l'errore hello nei risultati: **"ADFCopyTutorialDF" nome della Data factory non è disponibile**, hello i passaggi seguenti:  
  
  1. Modifica il nome hello (ad esempio, yournameADFCopyTutorialDF) in hello **datafactory.json** file.
  2. Nel primo comando hello in hello **$cmd** variabile viene assegnato un valore, sostituire ADFCopyTutorialDF con nome hello ed eseguire il comando di hello. 
  3. Eseguire hello due comandi successivi tooinvoke hello API REST toocreate hello data factory e stampa hello risultati dell'operazione di hello. 
     
     Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .
* le istanze di Data Factory toocreate, è necessario toobe un amministratore o un collaboratore di hello sottoscrizione di Azure
* nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.
* Se viene visualizzato l'errore hello: "**questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory**", effettuare una delle seguenti hello e riprovare: 
  
  * In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è registrato. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Account di accesso tramite hello sottoscrizione di Azure in hello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o). Questa azione registra automaticamente i provider di hello.

Prima di creare una pipeline, è necessario toocreate alcune entità Data Factory prima. Creare innanzitutto l'origine toolink servizi collegati e i dati di destinazione archivia dati tooyour archiviare. Quindi, definire i set di dati di input e output toorepresent dati in archivi dati collegati. Infine, è possibile creare pipeline hello con un'attività che utilizza questi set di dati.

## <a name="create-linked-services"></a>Creare servizi collegati
Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo. In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics, ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione). Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.  

Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure. Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService collega il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
In questo passaggio si collega la data factory tooyour account di archiviazione di Azure. Specificare il nome di hello e chiave dell'account di archiviazione di Azure in questa sezione. Vedere [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure.  

1. Assegnare toovariable comando hello denominato **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Eseguire il comando hello utilizzando **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Visualizzare i risultati di hello. Se collegato hello servizio è stato creato correttamente, hello JSON per il servizio collegato hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Creare un servizio collegato di Azure SQL
In questo passaggio si collega il tooyour data factory di Azure SQL database. Specificare nome del server SQL Azure hello, nome del database, nome utente e password dell'utente in questa sezione. Vedere [servizio collegato SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato SQL Azure.

1. Assegnare toovariable comando hello denominato **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
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
Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour. In questo passaggio si definiscono due set di dati denominati AzureBlobInput e AzureSqlOutput che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService e AzureSqlLinkedService rispettivamente.

il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. E, set di dati blob di input hello (AzureBlobInput) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.  

Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello. 

### <a name="create-input-dataset"></a>Creare set di dati di input
In questo passaggio, creare un set di dati denominato AzureBlobInput che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService collegato servizio di archiviazione di Azure. Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione. In questa esercitazione, si specifica un valore per il nome file hello. 

1. Assegnare toovariable comando hello denominato **cmd**. 

    ```PowerSHell   
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
servizio collegato Database di SQL Azure Hello specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. Hello output SQL tabella dataset (OututDataset) create in questo passaggio specifica tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.

1. Assegnare toovariable comando hello denominato **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
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
In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **AzureBlobInput** come input e **AzureSqlOutput** come output.

Set di dati di output è attualmente, quali unità hello pianificazione. In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora. pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore. Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello. 

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

**Congratulazioni.** Una data factory di Azure, è stato creato con una pipeline che copia i dati dal database SQL tooAzure di archiviazione Blob di Azure.

## <a name="monitor-pipeline"></a>Monitorare la pipeline
In questo passaggio è utilizzare le sezioni di toomonitor API REST di Data Factory viene generate dalla pipeline hello.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Assicurarsi che hello inizio e fine tempi hello specificato nel seguente comando inizio hello corrispondenza e di fine della pipeline hello. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Eseguire Invoke-Command hello e hello successivo finché non viene visualizzata una sezione in **pronto** stato o **Failed** stato. Quando la sezione hello è nello stato pronto, controllare hello **emp** tabella nel database SQL di Azure per i dati di output di hello. 

Per ogni intervallo di due righe di dati dal file di origine hello sono tabella emp toohello copiati nel database di SQL Azure hello. Pertanto, vedrai 24 nuovi record nella tabella emp hello quando vengono elaborate tutte le sezioni di hello (nello stato Ready). 

## <a name="summary"></a>Riepilogo
In questa esercitazione è stato utilizzato API REST toocreate un Azure data factory toocopy di dati da un database di SQL Azure tooan blob di Azure. Ecco i passaggi di alto livello hello effettuati in questa esercitazione:  

1. Creare un'istanza di Azure **Data Factory**.
2. Creare **servizi collegati**:
   1. Una risorsa di archiviazione di Azure collegati toolink service account di archiviazione di Azure che contiene i dati di input.     
   2. SQL Azure collegato toolink servizio database SQL di Azure che contiene i dati di output di hello. 
3. Creare **set di dati**che descrivono dati di input e dati di output per le pipeline.
4. Creare una **pipeline** con un'attività di copia con BlobSource come origine e SqlSink come sink. 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia. Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.
