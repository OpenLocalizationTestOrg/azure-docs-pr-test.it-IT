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
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="7992f-103">Esercitazione: Creare la prima data factory di Azure usando l'API REST di Data Factory</span><span class="sxs-lookup"><span data-stu-id="7992f-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7992f-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7992f-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="7992f-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7992f-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="7992f-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7992f-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="7992f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7992f-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="7992f-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7992f-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="7992f-109">API REST</span><span class="sxs-lookup"><span data-stu-id="7992f-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="7992f-110">In questo articolo, utilizzare API REST di Data Factory toocreate prima data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="7992f-111">esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="7992f-112">pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7992f-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="7992f-113">Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input.</span><span class="sxs-lookup"><span data-stu-id="7992f-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="7992f-114">pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="7992f-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="7992f-115">In questo articolo non copre tutti hello API REST.</span><span class="sxs-lookup"><span data-stu-id="7992f-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="7992f-116">Per una documentazione completa sull'API REST, vedere [Data Factory REST API Reference](/rest/api/datafactory/) (Informazioni di riferimento sull'API REST di Data Factory).</span><span class="sxs-lookup"><span data-stu-id="7992f-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="7992f-117">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="7992f-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="7992f-118">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="7992f-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="7992f-119">Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="7992f-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7992f-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7992f-120">Prerequisites</span></span>
* <span data-ttu-id="7992f-121">Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="7992f-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="7992f-122">Installare [Curl](https://curl.haxx.se/dlwiz/) nel computer.</span><span class="sxs-lookup"><span data-stu-id="7992f-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="7992f-123">Lo strumento di CURL hello con altri comandi toocreate una data factory.</span><span class="sxs-lookup"><span data-stu-id="7992f-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="7992f-124">Seguire le istruzioni disponibili in [questo articolo](../azure-resource-manager/resource-group-create-service-principal-portal.md) per:</span><span class="sxs-lookup"><span data-stu-id="7992f-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="7992f-125">Creare un'applicazione Web denominata **ADFGetStartedApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7992f-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="7992f-126">Ottenere i valori per l'**ID client** e la **chiave privata**.</span><span class="sxs-lookup"><span data-stu-id="7992f-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="7992f-127">Ottenere l' **ID tenant**.</span><span class="sxs-lookup"><span data-stu-id="7992f-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="7992f-128">Assegnare hello **ADFGetStartedApp** applicazione toohello **Data Factory collaboratore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="7992f-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="7992f-129">Installare [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7992f-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="7992f-130">Avviare **PowerShell** e hello esecuzione comando seguente.</span><span class="sxs-lookup"><span data-stu-id="7992f-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="7992f-131">Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7992f-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="7992f-132">Se si chiude e riapre, è necessario comandi hello toorun nuovamente.</span><span class="sxs-lookup"><span data-stu-id="7992f-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="7992f-133">Eseguire **accesso AzureRmAccount** e immettere nome utente hello e la password usati toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="7992f-134">Eseguire **Get AzureRmSubscription** tooview tutti hello sottoscrizioni per questo account.</span><span class="sxs-lookup"><span data-stu-id="7992f-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="7992f-135">Eseguire **AzureRmSubscription di Get - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** sottoscrizione hello tooselect da toowork con.</span><span class="sxs-lookup"><span data-stu-id="7992f-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="7992f-136">Sostituire **NameOfAzureSubscription** con nome hello della sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="7992f-137">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando in hello PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="7992f-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="7992f-138">Alcuni dei passaggi di hello in questa esercitazione si supponga di utilizza il gruppo di risorse di hello denominato ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="7992f-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="7992f-139">Se si utilizza un gruppo di risorse diverso, è necessario il nome hello toouse del gruppo di risorse al posto di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7992f-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="7992f-140">Creare le definizioni JSON</span><span class="sxs-lookup"><span data-stu-id="7992f-140">Create JSON definitions</span></span>
<span data-ttu-id="7992f-141">Creare i seguenti file JSON nella cartella hello curl.exe in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="7992f-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="7992f-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="7992f-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7992f-143">Nome deve essere globalmente univoco, pertanto è consigliabile toomake ADFCopyTutorialDF tooprefix/suffisso è un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="7992f-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="7992f-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="7992f-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7992f-145">Sostituire **accountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="7992f-146">toolearn come accedere a tooget lo spazio di archiviazione della chiave, vedere informazioni come tooview, copiare e rigenerare archiviazione accedere alle chiavi in hello [gestire account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7992f-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="7992f-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="7992f-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="7992f-148">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="7992f-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="7992f-149">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7992f-149">Property</span></span> | <span data-ttu-id="7992f-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7992f-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7992f-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="7992f-151">ClusterSize</span></span> |<span data-ttu-id="7992f-152">Dimensioni del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="7992f-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="7992f-153">TimeToLive</span></span> |<span data-ttu-id="7992f-154">Specifica il tempo di inattività hello per il cluster HDInsight hello, prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="7992f-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="7992f-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7992f-155">linkedServiceName</span></span> |<span data-ttu-id="7992f-156">Specifica l'account di archiviazione hello toostore utilizzati hello registri generati da HDInsight</span><span class="sxs-lookup"><span data-stu-id="7992f-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="7992f-157">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="7992f-157">Note hello following points:</span></span>

* <span data-ttu-id="7992f-158">Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello sopra JSON.</span><span class="sxs-lookup"><span data-stu-id="7992f-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="7992f-159">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="7992f-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="7992f-160">È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="7992f-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="7992f-161">Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="7992f-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="7992f-162">Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="7992f-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="7992f-163">HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="7992f-164">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="7992f-164">This behavior is by design.</span></span> <span data-ttu-id="7992f-165">Con il servizio collegato di HDInsight su richiesta, un cluster HDInsight viene creato ogni volta che viene elaborata una sezione a meno che non vi è un cluster esistente in tempo reale (**timeToLive**) e viene eliminata quando viene eseguita un'elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="7992f-166">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="7992f-167">Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7992f-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="7992f-168">i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="7992f-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="7992f-169">Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="7992f-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="7992f-170">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="7992f-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="7992f-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="7992f-171">inputdataset.json</span></span>

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

<span data-ttu-id="7992f-172">Hello JSON definisce un set di dati denominato **AzureBlobInput**, che rappresenta i dati di input per un'attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="7992f-173">Inoltre, specifica che i dati di input hello si trovano nel contenitore di blob hello chiamato **adfgetstarted** e cartella hello denominata **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="7992f-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="7992f-174">Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="7992f-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="7992f-175">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7992f-175">Property</span></span> | <span data-ttu-id="7992f-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7992f-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7992f-177">type</span><span class="sxs-lookup"><span data-stu-id="7992f-177">type</span></span> |<span data-ttu-id="7992f-178">proprietà tipo Hello è impostato tooAzureBlob perché risiedono dati nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="7992f-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7992f-179">linkedServiceName</span></span> |<span data-ttu-id="7992f-180">si riferisce toohello StorageLinkedService creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7992f-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="7992f-181">fileName</span><span class="sxs-lookup"><span data-stu-id="7992f-181">fileName</span></span> |<span data-ttu-id="7992f-182">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="7992f-182">This property is optional.</span></span> <span data-ttu-id="7992f-183">Se si omette questa proprietà, vengono selezionati tutti i file hello folderPath hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="7992f-184">In questo caso, viene elaborato solo hello input.log.</span><span class="sxs-lookup"><span data-stu-id="7992f-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="7992f-185">type</span><span class="sxs-lookup"><span data-stu-id="7992f-185">type</span></span> |<span data-ttu-id="7992f-186">file di log Hello sono in formato testo, permette di usare TextFormat.</span><span class="sxs-lookup"><span data-stu-id="7992f-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="7992f-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="7992f-187">columnDelimiter</span></span> |<span data-ttu-id="7992f-188">nei file di log hello colonne sono delimitate da una virgola ()</span><span class="sxs-lookup"><span data-stu-id="7992f-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="7992f-189">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="7992f-189">frequency/interval</span></span> |<span data-ttu-id="7992f-190">frequenza impostata tooMonth e l'intervallo è 1, che significa che le sezioni di input hello sono disponibili ogni mese.</span><span class="sxs-lookup"><span data-stu-id="7992f-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="7992f-191">external</span><span class="sxs-lookup"><span data-stu-id="7992f-191">external</span></span> |<span data-ttu-id="7992f-192">Questa proprietà è impostata tootrue se i dati di input hello non viene generati dal servizio Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="7992f-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="7992f-193">outputdataset.json</span></span>

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

<span data-ttu-id="7992f-194">Hello JSON definisce un set di dati denominato **AzureBlobOutput**, che rappresenta i dati di output per un'attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="7992f-195">Inoltre, specifica che i risultati di hello vengono archiviati nel contenitore blob hello chiamato **adfgetstarted** e cartella hello denominata **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="7992f-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="7992f-196">Hello **disponibilità** sezione specifica di tale set di dati di output di hello viene prodotto su base mensile.</span><span class="sxs-lookup"><span data-stu-id="7992f-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="7992f-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="7992f-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7992f-198">Sostituire **storageaccountname** con il nome del proprio account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
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

<span data-ttu-id="7992f-199">Nel frammento di codice JSON hello, si sta creando una pipeline che è costituito da una singola attività che utilizza dati tooprocess Hive in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7992f-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="7992f-200">file di script Hive Hello, **partitionweblogs.hql**, viene archiviato nell'account di archiviazione Azure hello (specificato da scriptLinkedService hello, chiamato **StorageLinkedService**) e in **script**  cartella nel contenitore hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="7992f-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="7992f-201">Hello **definisce** sezione specifica le impostazioni di runtime script hive toohello passati come valori di configurazione di Hive (ad esempio ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="7992f-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="7992f-202">Hello **avviare** e **fine** le proprietà della pipeline hello specifica periodo attivo di hello della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="7992f-203">In formato JSON dell'attività hello, specificare tale script Hive hello viene eseguito sul calcolo hello specificato da hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="7992f-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="7992f-204">Vedere la sezione "JSON di Pipeline" in [pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md) per dettagli sulle proprietà JSON utilizzato in hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="7992f-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="7992f-205">Configurare le variabili globali</span><span class="sxs-lookup"><span data-stu-id="7992f-205">Set global variables</span></span>
<span data-ttu-id="7992f-206">In Azure PowerShell, eseguire hello seguenti comandi dopo la sostituzione di valori hello con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="7992f-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7992f-207">Per istruzioni su come ottenere i valori per ID client, segreto client, ID tenant e ID sottoscrizione, vedere la sezione [Prerequisiti](#prerequisites) .</span><span class="sxs-lookup"><span data-stu-id="7992f-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
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


## <a name="authenticate-with-aad"></a><span data-ttu-id="7992f-208">Eseguire l'autenticazione con AAD</span><span class="sxs-lookup"><span data-stu-id="7992f-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="7992f-209">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="7992f-209">Create data factory</span></span>
<span data-ttu-id="7992f-210">In questo passaggio viene creata un'istanza di Azure Data Factory denominata **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="7992f-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="7992f-211">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="7992f-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="7992f-212">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="7992f-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="7992f-213">Ad esempio, un'attività di copia toocopy i dati da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform di dati di script Hive.</span><span class="sxs-lookup"><span data-stu-id="7992f-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="7992f-214">Eseguire hello data factory di comandi toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7992f-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="7992f-215">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7992f-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="7992f-216">Verificare che nome hello di hello data factory specificato (ADFCopyTutorialDF) corrispondenze hello nome specificato in hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="7992f-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7992f-217">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7992f-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7992f-218">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-218">View hello results.</span></span> <span data-ttu-id="7992f-219">Se hello data factory è stata creata correttamente, viene visualizzato hello JSON per data factory di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="7992f-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="7992f-220">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="7992f-220">Note hello following points:</span></span>

* <span data-ttu-id="7992f-221">nome Hello di hello Azure Data Factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="7992f-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="7992f-222">Se viene visualizzato l'errore hello nei risultati: **"FirstDataFactoryREST" nome della Data factory non è disponibile**, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7992f-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="7992f-223">Modifica il nome hello (ad esempio, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span><span class="sxs-lookup"><span data-stu-id="7992f-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="7992f-224">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="7992f-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="7992f-225">Nel primo comando hello in hello **$cmd** variabile viene assegnato un valore, sostituire FirstDataFactoryREST con nome hello ed eseguire il comando di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="7992f-226">Eseguire hello due comandi successivi tooinvoke hello API REST toocreate hello data factory e stampa hello risultati dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="7992f-227">le istanze di Data Factory toocreate, è necessario toobe un amministratore o un collaboratore di hello sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="7992f-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="7992f-228">nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="7992f-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="7992f-229">Se viene visualizzato l'errore hello: "**questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory**", effettuare una delle seguenti hello e riprovare:</span><span class="sxs-lookup"><span data-stu-id="7992f-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="7992f-230">In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory:</span><span class="sxs-lookup"><span data-stu-id="7992f-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="7992f-231">È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è stato registrato:</span><span class="sxs-lookup"><span data-stu-id="7992f-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="7992f-232">Account di accesso tramite hello sottoscrizione di Azure in hello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="7992f-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="7992f-233">Questa azione registra automaticamente i provider di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="7992f-234">Prima di creare una pipeline, è necessario toocreate alcune entità Data Factory prima.</span><span class="sxs-lookup"><span data-stu-id="7992f-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="7992f-235">Creare innanzitutto i dati di servizi collegati toolink archivi/calcola tooyour dati archiviano, definiscono l'input e output dati toorepresent set di dati in archivi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="7992f-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="7992f-236">Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="7992f-236">Create linked services</span></span>
<span data-ttu-id="7992f-237">In questo passaggio è collegare l'account di archiviazione di Azure e una factory del dati tooyour cluster Azure HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="7992f-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="7992f-238">contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="7992f-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="7992f-239">servizio collegato di HDInsight Hello è toorun usato uno script Hive specificato nell'attività hello della pipeline hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="7992f-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="7992f-240">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7992f-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="7992f-241">In questo passaggio si collega la data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="7992f-242">In questa esercitazione, si utilizza hello stesso account di archiviazione di Azure i dati di input/output toostore e hello HQL file di script.</span><span class="sxs-lookup"><span data-stu-id="7992f-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="7992f-243">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7992f-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7992f-244">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7992f-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7992f-245">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-245">View hello results.</span></span> <span data-ttu-id="7992f-246">Se collegato hello servizio è stato creato correttamente, hello JSON per il servizio collegato hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="7992f-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="7992f-247">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7992f-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="7992f-248">In questo passaggio si collega una factory del dati tooyour cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="7992f-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="7992f-249">cluster HDInsight Hello viene automaticamente creato in fase di esecuzione ed eliminato al termine per l'elaborazione e inattività per l'intervallo di tempo specificato hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="7992f-250">È possibile usare il proprio cluster HDInsight anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="7992f-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="7992f-251">Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="7992f-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="7992f-252">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7992f-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7992f-253">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7992f-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7992f-254">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-254">View hello results.</span></span> <span data-ttu-id="7992f-255">Se collegato hello servizio è stato creato correttamente, hello JSON per il servizio collegato hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="7992f-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="7992f-256">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="7992f-256">Create datasets</span></span>
<span data-ttu-id="7992f-257">In questo passaggio creare set di dati toorepresent hello input e output dei dati per l'elaborazione Hive.</span><span class="sxs-lookup"><span data-stu-id="7992f-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="7992f-258">Questi set di dati di riferimento toohello **StorageLinkedService** creata precedentemente in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7992f-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="7992f-259">Hello tooan punti di servizio collegato account di archiviazione di Azure e i set di dati specificare contenitore, cartella, nome del file nell'archiviazione hello che contiene l'input e output di dati.</span><span class="sxs-lookup"><span data-stu-id="7992f-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="7992f-260">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="7992f-260">Create input dataset</span></span>
<span data-ttu-id="7992f-261">In questo passaggio è creare hello set di dati input toorepresent dati di input memorizzati nell'archiviazione Blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="7992f-262">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7992f-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7992f-263">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7992f-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7992f-264">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-264">View hello results.</span></span> <span data-ttu-id="7992f-265">Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="7992f-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="7992f-266">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="7992f-266">Create output dataset</span></span>
<span data-ttu-id="7992f-267">In questo passaggio è creare hello output dataset toorepresent output dei dati archiviati in archiviazione Blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="7992f-268">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7992f-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7992f-269">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7992f-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7992f-270">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-270">View hello results.</span></span> <span data-ttu-id="7992f-271">Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="7992f-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="7992f-272">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="7992f-272">Create pipeline</span></span>
<span data-ttu-id="7992f-273">In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="7992f-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="7992f-274">Sezione di input è disponibile ogni mese (frequenza: mese, intervallo: 1), sezione di output viene prodotta ogni mese e hello dell'utilità di pianificazione per l'attività hello viene anche impostata toomonthly.</span><span class="sxs-lookup"><span data-stu-id="7992f-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="7992f-275">le impostazioni di Hello per set di dati output hello e utilità di pianificazione attività hello devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="7992f-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="7992f-276">Set di dati di output è attualmente, quali unità hello pianificazione, pertanto è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="7992f-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="7992f-277">Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione.</span><span class="sxs-lookup"><span data-stu-id="7992f-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="7992f-278">Assicurarsi di visualizzare hello **input.log** file hello **adfgetstarted/inputdata** cartella hello archiviazione blob di Azure e hello fase della pipeline hello toodeploy dei comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="7992f-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="7992f-279">Poiché hello **avviare** e **fine** volte in cui vengono impostate in hello precedente e **isPaused** è toofalse set, pipeline hello esecuzioni (attività nella pipeline hello) immediatamente dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7992f-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="7992f-280">Assegnare toovariable comando hello denominato **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7992f-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7992f-281">Eseguire il comando hello utilizzando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7992f-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7992f-282">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-282">View hello results.</span></span> <span data-ttu-id="7992f-283">Se il set di dati hello è stato creato correttamente, viene visualizzato hello JSON per set di dati di hello in hello **risultati**; in caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="7992f-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="7992f-284">La creazione della prima pipeline tramite Azure PowerShell è così completata.</span><span class="sxs-lookup"><span data-stu-id="7992f-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="7992f-285">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="7992f-285">Monitor pipeline</span></span>
<span data-ttu-id="7992f-286">In questo passaggio è utilizzare le sezioni di toomonitor API REST di Data Factory viene generate dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

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
> <span data-ttu-id="7992f-287">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="7992f-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="7992f-288">Pertanto, prevedere hello pipeline tootake **circa 30 minuti** tooprocess hello sezione.</span><span class="sxs-lookup"><span data-stu-id="7992f-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="7992f-289">Eseguire Invoke-Command hello e hello successivo finché non viene visualizzata la sezione hello in **pronto** stato o **Failed** stato.</span><span class="sxs-lookup"><span data-stu-id="7992f-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="7992f-290">Quando la sezione hello è nello stato pronto, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.</span><span class="sxs-lookup"><span data-stu-id="7992f-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="7992f-291">creazione di Hello di un cluster di HDInsight su richiesta richiede in genere del tempo.</span><span class="sxs-lookup"><span data-stu-id="7992f-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![Dati di output](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="7992f-293">file di input Hello eliminato quando la sezione hello viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="7992f-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="7992f-294">Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.</span><span class="sxs-lookup"><span data-stu-id="7992f-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="7992f-295">È inoltre possibile utilizzare le sezioni toomonitor portale Azure e risolvere eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="7992f-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="7992f-296">Per i dettagli, vedere [Creare la prima data factory di Azure usando il portale di Azure/l'editor di Data Factory](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="7992f-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="7992f-297">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7992f-297">Summary</span></span>
<span data-ttu-id="7992f-298">In questa esercitazione, creato un Azure factory tooprocess dati tramite l'esecuzione di script Hive in un cluster di HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="7992f-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="7992f-299">È stato utilizzato hello Editor delle Data Factory in hello toodo portale Azure hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7992f-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="7992f-300">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="7992f-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="7992f-301">Creare due **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="7992f-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="7992f-302">**Archiviazione di Azure** collegati toolink servizio di archiviazione blob di Azure che contiene una data factory toohello di file di input/output.</span><span class="sxs-lookup"><span data-stu-id="7992f-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="7992f-303">**Azure HDInsight** toolink servizio collegato su richiesta di una factory del dati toohello cluster HDInsight Hadoop su richiesta.</span><span class="sxs-lookup"><span data-stu-id="7992f-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="7992f-304">Data Factory di Azure crea un HDInsight Hadoop dati di input tooprocess just-in-time di cluster e generare dati di output.</span><span class="sxs-lookup"><span data-stu-id="7992f-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="7992f-305">Creare due **set di dati**, che descrivono i dati di input e outpui per l'attività Hive di HDInsight nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="7992f-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="7992f-306">Creare una **pipeline** con un'attività **Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7992f-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7992f-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7992f-307">Next steps</span></span>
<span data-ttu-id="7992f-308">In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta di Azure.</span><span class="sxs-lookup"><span data-stu-id="7992f-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="7992f-309">toosee toouse un dati toocopy attività di copia da un tooAzure Blob di Azure SQL, vedere [esercitazione: copiare i dati da un tooAzure Blob di Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7992f-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7992f-310">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7992f-310">See Also</span></span>
| <span data-ttu-id="7992f-311">Argomento</span><span class="sxs-lookup"><span data-stu-id="7992f-311">Topic</span></span> | <span data-ttu-id="7992f-312">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7992f-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="7992f-313">Informazioni di riferimento sull'API REST di Data Factory</span><span class="sxs-lookup"><span data-stu-id="7992f-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="7992f-314">Vedere la documentazione completa sui cmdlet di Data factory</span><span class="sxs-lookup"><span data-stu-id="7992f-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="7992f-315">Pipeline</span><span class="sxs-lookup"><span data-stu-id="7992f-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="7992f-316">In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="7992f-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="7992f-317">Set di dati</span><span class="sxs-lookup"><span data-stu-id="7992f-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="7992f-318">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7992f-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="7992f-319">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="7992f-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="7992f-320">Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7992f-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="7992f-321">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="7992f-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="7992f-322">In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App.</span><span class="sxs-lookup"><span data-stu-id="7992f-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
