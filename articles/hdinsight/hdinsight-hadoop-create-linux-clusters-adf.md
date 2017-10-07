---
title: cluster di Hadoop su richiesta utilizzando Data Factory - Azure HDInsight aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate cluster su richiesta Hadoop in HDInsight mediante la Data Factory di Azure.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Creare cluster Hadoop on demand in HDInsight con Azure Data Factory
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Azure Data Factory](../data-factory/data-factory-introduction.md) è un servizio di integrazione di dati basato su cloud che Orchestra e automatizza lo spostamento di hello e trasformazione dei dati. È possibile creare un tooprocess just-in-time di cluster HDInsight Hadoop una sezione di dati di input ed eliminare cluster hello termine dell'elaborazione hello. Alcuni dei vantaggi di hello dell'utilizzo di un cluster HDInsight Hadoop su richiesta sono:

- Si pagare solo per il processo ora hello è in esecuzione hello del cluster HDInsight Hadoop (più un tempo di inattività configurabile breve). la fatturazione per i cluster HDInsight Hello è proporzionale al minuto, sia che si utilizzi o non. Quando si utilizza un servizio collegato di HDInsight su richiesta in Data Factory, i cluster hello vengono creati su richiesta. E i cluster hello vengono eliminati automaticamente quando vengono completati i processi di hello. Pertanto, si paga solo per il processo di hello esegue ora e tempo di inattività breve hello (impostazione di time-to-live).
- È possibile creare un flusso di lavoro usando una pipeline di Data Factory. Ad esempio, è possibile disporre hello pipeline toocopy di dati da un tooan di SQL Server on-premise archiviazione blob di Azure, dati hello processo eseguendo uno script Hive e uno script Pig in un cluster HDInsight Hadoop su richiesta. Copiare quindi hello risultato dati tooan Azure SQL Data Warehouse per tooconsume applicazioni di Business Intelligence.
- È possibile pianificare hello del flusso di lavoro toorun periodicamente (oraria, giornaliera, settimanale, mensile, ecc.).

In Azure Data Factory, una data factory può includere una o più pipeline di dati. Una pipeline di dati include una o più attività. Esistono due tipi di attività: [attività di spostamento dei dati](../data-factory/data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](../data-factory/data-factory-data-transformation-activities.md). Utilizzare dati toomove di attività (attualmente solo attività di copia) lo spostamento di dati da un archivio dati di origine dati archivio tooa destinazione. Utilizzare i dati o il processo tootransform attività di trasformazione dati. Attività Hive di HDInsight è una delle attività di trasformazione hello è supportata da Data Factory. Utilizzare l'attività di trasformazione Hive hello in questa esercitazione.

È possibile configurare un toouse attività hive cluster HDInsight Hadoop personale o un cluster HDInsight Hadoop su richiesta. In questa esercitazione, hello attività Hive nella pipeline di hello data factory è toouse configurato un cluster di HDInsight su richiesta. Pertanto, quando viene eseguita attività hello tooprocess una sezione di dati, ecco cosa succede:

1. -In-time tooprocess hello suddividere viene creato automaticamente un cluster HDInsight Hadoop.  
2. dati di input Hello viene elaborati eseguendo uno script HiveQL nel cluster hello.
3. cluster HDInsight Hadoop Hello viene eliminato dopo l'elaborazione di hello e cluster hello è inattivo per hello configurato di tempo (impostazione timeToLive). Se è disponibile per l'elaborazione con il tempo di inattività timeToLive sezione di dati successiva hello, hello dello stesso cluster è sezione hello tooprocess utilizzato.  

In questa esercitazione, hello script HiveQL associato all'attività hive hello esegue hello seguenti azioni:

1. Crea una tabella esterna che riferimenti hello dati di log web non elaborato archiviati in una risorsa di archiviazione Blob di Azure.
2. Dati non elaborati hello di partizioni per anno e mese.
3. Archivi hello dati partizionati in hello archiviazione blob di Azure.

In questa esercitazione, hello script HiveQL associato all'attività hive hello crea una tabella esterna che riferimenti hello dati di registro non elaborati web archiviati in hello archiviazione Blob di Azure. Di seguito sono le righe di esempio hello per ogni mese nel file di input hello.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

le partizioni di script HiveQL Hello hello dati non elaborati per anno e mese. Vengono create tre cartelle di output in base all'input precedente hello. Ogni cartella contiene un file con le voci di ogni mese.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Per un elenco delle attività di trasformazione di dati di Data Factory in attività tooHive aggiunta, vedere [trasformare e analizzare l'utilizzo di Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Attualmente, da Azure Data Factory è possibile creare solo cluster HDInsight versione 3.2.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare hello istruzioni in questo articolo, è necessario disporre di hello seguenti elementi:

* [Sottoscrizione di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Preparare un account di archiviazione
È possibile utilizzare gli account di archiviazione toothree in questo scenario:

- account di archiviazione predefinito per il cluster HDInsight hello
- account di archiviazione per i dati di input hello
- account di archiviazione per i dati di output di hello

esercitazione di hello toosimplify, utilizzare un account tooserve hello tre scopi di archiviazione. script di esempio Hello Azure PowerShell riportati in questa sezione vengono eseguite hello seguenti attività:

1. Accedi tooAzure.
2. Creare un gruppo di risorse di Azure.
3. Creare un account di archiviazione di Azure.
4. Creare un contenitore Blob nell'account di archiviazione hello
5. Copiare hello contenitore Blob di due file toohello seguenti:

   * File di dati di input: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * Script HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Entrambi i file vengono archiviati in un contenitore BLOB pubblico.


**tooprepare hello archiviazione e copiare hello file tramite Azure PowerShell:**
> [!IMPORTANT]
> Specificare i nomi per il gruppo di risorse di Azure hello e hello account di archiviazione Azure che verrà creato dallo script hello.
> Annotare **nome gruppo di risorse**, **nome account di archiviazione**, e **chiave account di archiviazione** restituite dallo script hello. È necessario nella sezione successiva hello.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Per assistenza con script di PowerShell hello, vedere [hello tramite Azure PowerShell con l'archiviazione di Azure](../storage/common/storage-powershell-guide-full.md). Se si desidera toouse CLI di Azure, vedere hello [appendice](#appendix) sezione per hello script CLI di Azure.

**tooexamine hello storage account e hello contenuto**

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **gruppi di risorse** hello riquadro a sinistra.
3. Fare doppio clic sul nome del gruppo di risorse hello che è stato creato nello script di PowerShell. Se si dispone di un numero eccessivo di gruppi di risorse elencati, utilizzare il filtro di hello.
4. In hello **risorse** riquadro, si deve essere presente una risorsa elencata, a meno che il gruppo di risorse hello è condividere con altri progetti. Questa risorsa è l'account di archiviazione hello con nome hello specificato in precedenza. Fare clic su nome account di archiviazione hello.
5. Fare clic su hello **BLOB** riquadri.
6. Fare clic su hello **adfgetstarted** contenitore. Vengono visualizzate due cartelle: **inputdata** e **script**.
7. Aprire la cartella hello e controllare i file nelle cartelle hello hello. cartella script hello contiene file di script HiveQL hello inputdata Hello contiene file input.log hello con dati di input.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Creare una data factory usando un modello di Resource Manager
Con account di archiviazione hello, dati di input hello e hello script HiveQL preparato, si è pronti toocreate una data factory di Azure. Esistono diversi metodi per creare un'istanza di Data Factory. In questa esercitazione creerai una data factory tramite la distribuzione di un modello di gestione risorse di Azure tramite hello portale di Azure. È possibile distribuire un modello di Resource Manager anche con l'[interfaccia della riga di comando di Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) e [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Per altri metodi di creazione di un'istanza di Data Factory, vedere [l'esercitazione per creare la prima istanza di Data Factory](../data-factory/data-factory-build-your-first-pipeline.md).

1. Fare clic su hello seguente immagine toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello. modello Hello si trova in https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json. Vedere hello [entità Data Factory nel modello hello](#data-factory-entities-in-the-template) sezione per informazioni dettagliate sulle entità definite nel modello di hello. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Selezionare **Usa esistente** opzione per hello **gruppo di risorse** , impostazione e il nome di hello selezionare hello del gruppo di risorse creato nel passaggio precedente di hello (tramite script di PowerShell).
3. Immettere un nome per data factory di hello (**nome della Data Factory**). Il nome deve essere univoco a livello globale.
4. Immettere hello **nome account di archiviazione** e **chiave account di archiviazione** annotate nel passaggio precedente hello.
5. Selezionare **accetto le condizioni toohello** indicati sopra la a **termini e condizioni**.
6. Selezionare **toodashboard Pin** opzione.
6. Fare clic su **Acquista/Crea**. Viene visualizzato un riquadro nel Dashboard chiamato hello **distribuzione del modello di distribuzione**. Attendere hello **gruppo di risorse** apre pannello per il gruppo di risorse. È anche possibile fare clic su riquadro hello denominato come il pannello di gruppo di risorse gruppo nome tooopen hello risorsa.
6. Fare clic su gruppo di risorse di hello riquadro tooopen hello pannello della risorsa gruppo hello non è già aperto. Ora verrà visualizzata una risorsa di ulteriori dati factory inoltre toohello archiviazione account risorsa indicata.
7. Fare clic sul nome di una factory di dati hello (valore specificato per hello **nome della Data Factory** parametro).
8. Nel Pannello di Data Factory hello, fare clic su hello **diagramma** riquadro. Hello è illustrata un'attività con un set di dati di input e un set di dati di output:

    ![Diagramma della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    i nomi di Hello vengono definiti nel modello di gestione risorse di hello.
9. Fare doppio clic su **AzureBlobOutput**.
10. In hello **recenti aggiornato sezioni**, verrà visualizzata un'unica sezione. Se è stato hello **In corso**, attendere fino a quando non è stato modificato anche**pronto**. In genere richiede circa **20 minuti** toocreate un cluster HDInsight.

### <a name="check-hello-data-factory-output"></a>Controllare l'output di hello data factory

1. Utilizzare hello stessa procedura in hello ultima sessione toocheck hello contenitori del contenitore adfgetstarted hello. Esistono due nuovi contenitori inoltre troppo**adfgetsarted**:

   * Un contenitore con nome che segue il modello di hello: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Questo contenitore è il contenitore predefinito hello per il cluster HDInsight hello.
   * adfjobs: questo contenitore è il contenitore di hello hello ADF dei log dei processi.

     output di Hello data factory viene archiviato **afgetstarted** come configurato nel modello di gestione risorse di hello.
2. Fare clic su **adfgetstarted**.
3. Fare doppio clic su **partitioneddata**. Viene visualizzato un **anno = 2014** cartella perché tutti i log web hello data nell'anno 2014.

    ![Output della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Se il drill-down elenco hello, verrà visualizzato tre cartelle relativi a gennaio, febbraio e marzo. È presente un log per ogni mese.

    ![Output della pipeline attività Hive di HDInsight on demand in Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Entità di modello hello Factory di dati
Ecco come modello di gestione risorse per una data factory di primo livello hello simile:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Definire una data factory
È consigliabile definire una data factory nel modello di gestione risorse di hello come illustrato nel seguente esempio hello:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
dataFactoryName Hello è il nome di hello di hello data factory che è specificare quando si distribuisce il modello di hello. Factory di dati è attualmente supportata solo in aree geografiche di Stati Uniti orientali, Stati Uniti occidentali e Nord Europa hello.

### <a name="defining-entities-within-hello-data-factory"></a>Definizione di entità all'interno di data factory di hello
Hello entità Data Factory seguenti vengono definite nel modello JSON hello:

* [Servizio collegato Archiviazione di Azure](#azure-storage-linked-service)
* [Servizio collegato su richiesta HDInsight](#hdinsight-on-demand-linked-service)
* [Set di dati di input del BLOB di Azure](#azure-blob-input-dataset)
* [Set di dati di output del BLOB di Azure](#azure-blob-output-dataset)
* [Pipeline di dati con un'attività di copia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
Archiviazione di Azure Hello collegato collegamenti al servizio la data factory toohello account di archiviazione di Azure. In questa esercitazione, hello stesso account di archiviazione viene utilizzato come account di archiviazione di hello predefinito HDInsight, archiviazione di dati di input e archiviazione dei dati di output. Di conseguenza, si definisce un solo servizio collegato Archiviazione di Azure. Nella definizione di servizio collegato hello, specificare il nome di hello e chiave dell'account di archiviazione di Azure. Vedere [servizio collegato di archiviazione di Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Hello **connectionString** utilizza hello parametri storageAccountName e storageAccountKey. Si specificano valori per questi parametri durante la distribuzione del modello di hello.  

#### <a name="hdinsight-on-demand-linked-service"></a>Servizio collegato su richiesta HDInsight
In hello HDInsight su richiesta collegato definizione del servizio, si specificano valori per parametri di configurazione che vengono utilizzati da toocreate servizio Data Factory di hello un HDInsight Hadoop cluster in fase di esecuzione. Vedere [servizi collegati di calcolo](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) articolo per informazioni dettagliate su JSON proprietà utilizzate toodefine un servizio collegato di HDInsight su richiesta.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Si noti hello seguenti punti:

* Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente.
* Hello cluster HDInsight Hadoop viene creato in hello stessa regione dell'account di archiviazione hello.
* Hello preavviso *timeToLive* impostazione. data factory di Hello Elimina automaticamente i cluster hello dopo cluster hello è un periodo di inattività per 30 minuti.
* Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato di HDInsight su richiesta, un cluster HDInsight viene creato ogni volta che una sezione deve toobe elaborati a meno che non vi è un cluster esistente in tempo reale (**timeToLive**) e viene eliminata quando viene eseguita un'elaborazione hello.

Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

> [!IMPORTANT]
> Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.

#### <a name="azure-blob-input-dataset"></a>Set di dati di input del BLOB di Azure
Nella definizione di set di dati input hello, specificare nomi di hello del contenitore blob, cartelle e file che contiene i dati di input hello. Vedere [proprietà set di dati Blob di Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

Si noti hello impostazioni specifiche nella definizione JSON hello seguenti:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Set di dati di output del BLOB di Azure
Nella definizione di set di dati di output hello, specificare nomi hello del contenitore blob e di cartella che contiene i dati di output di hello. Vedere [proprietà set di dati Blob di Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

folderPath Hello specifica hello toohello cartella che contiene i dati di output di hello:

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Hello [disponibilità dataset](../data-factory/data-factory-create-datasets.md#dataset-availability) impostazione è come segue:

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

In Data Factory di Azure, l'output della pipeline di set di dati disponibilità unità hello. In questo esempio hello sezione viene prodotta mensile hello ultimo giorno del mese (EndOfInterval). Per altre informazioni, vedere [Pianificazione ed esecuzione con Data factory](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Data Pipeline
Viene definita una pipeline che trasforma i dati eseguendo lo script Hive in un cluster HDInsight di Azure su richiesta. Vedere [JSON di Pipeline](../data-factory/data-factory-create-pipelines.md#pipeline-json) per le descrizioni degli elementi usati di JSON toodefine una pipeline in questo esempio.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
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
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

pipeline di Hello contiene un'attività, attività HDInsightHive. Poiché sia la data di inizio che la data di fine sono nel mese di gennaio 2016, vengono elaboratori i dati per un solo mese (una sezione). Entrambi *avviare* e *fine* dell'attività hello presentano una data già trascorsa, pertanto hello Data Factory elabora i dati per mese hello immediatamente. Se una data futura fine hello è data factory di hello crea un'altra sezione al momento di hello. Per altre informazioni, vedere [Pianificazione ed esecuzione con Data factory](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Pulire esercitazione hello

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>Eliminare i contenitori di blob hello creati dal cluster HDInsight su richiesta
Con il servizio collegato di HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che una sezione deve toobe elaborati a meno che non vi è un cluster in tempo reale esistente (timeToLive); e hello cluster viene eliminato quando viene eseguita l'elaborazione di hello. Per ogni cluster, Azure Data Factory crea un contenitore blob nell'archiviazione blob di Azure utilizzato come account di archiviazione predefinito hello per cluster hello hello. Anche se il cluster HDInsight è stato eliminato, contenitore di archiviazione blob di hello predefinito e account di archiviazione hello associato non vengono eliminati. Questo comportamento dipende dalla progettazione. Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Eliminare hello **adfjobs** e **adfyourdatafactoryname-linkedservicename-datetimestamp** cartelle. contenitore adfjobs Hello contiene i registri dei processi da Azure Data Factory.

### <a name="delete-hello-resource-group"></a>Eliminare il gruppo di risorse hello
[Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) è usato toodeploy, gestire e monitorare la soluzione come gruppo.  Se si elimina un gruppo di risorse, tutti i componenti di hello all'interno di hello gruppo.  

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **gruppi di risorse** hello riquadro a sinistra.
3. Fare clic su nome gruppo di risorse hello che è stato creato nello script di PowerShell. Se si dispone di un numero eccessivo di gruppi di risorse elencati, utilizzare il filtro di hello. Gruppo di risorse hello viene aperto in un nuovo pannello.
4. In hello **risorse** riquadro, si hanno account di archiviazione predefinito hello e hello data factory elencati, a meno che il gruppo di risorse hello è condividere con altri progetti.
5. Fare clic su **eliminare** nella parte superiore di hello del pannello hello. In questo modo Elimina l'account di archiviazione hello e dati hello archiviati nell'account di archiviazione hello.
6. Immettere l'eliminazione del tooconfirm nome gruppo di risorse hello e quindi fare clic su **eliminare**.

Nel caso in cui non si desidera account di archiviazione hello toodelete quando si elimina il gruppo di risorse hello, prendere in considerazione hello seguente architettura separando i dati di business hello dall'account di archiviazione predefinito hello. In questo caso, si dispone di un gruppo di risorse per account di archiviazione hello con i dati aziendali hello e hello altro gruppo di risorse per account di archiviazione predefinito hello HDInsight collegato hello e servizio data factory. Quando si elimina il gruppo di risorse secondo hello, non influisce sulla account di archiviazione di dati business hello. toodo in modo:

* Aggiungere hello seguente gruppo di risorse di primo livello toohello insieme hello Microsoft.DataFactory/datafactories risorse nel modello di gestione risorse. Viene creato un account di archiviazione:

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Aggiungere un nuovo servizio collegato punto toohello nuovo account di archiviazione:

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Configurare il servizio ondemand collegato di HDInsight hello con un dependsOn aggiuntive e un additionalLinkedServiceNames:

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come toouse su richiesta toocreate Data Factory di Azure HDInsight cluster tooprocess processi Hive. tooread più:

* [Esercitazione di Hadoop: Introduzione all'uso di Hadoop basato su Linux in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Documentazione relativa a HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Documentazione di Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Appendice

### <a name="azure-cli-script"></a>Script dell'interfaccia della riga di comando di Azure
È possibile utilizzare l'interfaccia CLI di Azure anziché utilizzare l'esercitazione di Azure PowerShell toodo hello. toouse CLI di Azure, installare innanzitutto CLI di Azure in base alle hello attenendosi alle istruzioni:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Utilizzare l'archiviazione di Azure CLI tooprepare hello e copiare i file hello

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

nome di contenitore Hello *adfgetstarted*. Mantenerlo invariato, In caso contrario è necessario un modello di gestione risorse di tooupdate hello. Per assistenza con questo script CLI, vedere [Using hello CLI di Azure con l'archiviazione di Azure](../storage/common/storage-azure-cli.md).
