---
title: Creare la prima data factory (REST) | Documentazione Microsoft
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
ms.openlocfilehash: b0c237667f1f55298df20ab0f525202aa1b42e0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="c53a3-103">Esercitazione: Creare la prima data factory di Azure usando l'API REST di Data Factory</span><span class="sxs-lookup"><span data-stu-id="c53a3-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c53a3-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c53a3-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c53a3-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c53a3-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c53a3-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c53a3-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c53a3-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c53a3-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c53a3-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c53a3-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c53a3-109">API REST</span><span class="sxs-lookup"><span data-stu-id="c53a3-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="c53a3-110">In questo articolo viene usata l'API REST di Data Factory per creare la prima data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-110">In this article, you use Data Factory REST API to create your first Azure data factory.</span></span> <span data-ttu-id="c53a3-111">Per eseguire l'esercitazione usando altri strumenti/SDK, selezionare una delle opzioni dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c53a3-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="c53a3-112">La pipeline in questa esercitazione include un'attività, l'**attività Hive di HDInsight**,</span><span class="sxs-lookup"><span data-stu-id="c53a3-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c53a3-113">che esegue uno script Hive in un cluster Azure HDInsight per trasformare i dati di input e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="c53a3-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="c53a3-114">L'esecuzione della pipeline è pianificata una volta al mese tra le ore di inizio e di fine specificate.</span><span class="sxs-lookup"><span data-stu-id="c53a3-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="c53a3-115">Questo articolo non illustra tutte le API REST.</span><span class="sxs-lookup"><span data-stu-id="c53a3-115">This article does not cover all the REST API.</span></span> <span data-ttu-id="c53a3-116">Per una documentazione completa sull'API REST, vedere [Data Factory REST API Reference](/rest/api/datafactory/) (Informazioni di riferimento sull'API REST di Data Factory).</span><span class="sxs-lookup"><span data-stu-id="c53a3-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="c53a3-117">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="c53a3-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c53a3-118">ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra.</span><span class="sxs-lookup"><span data-stu-id="c53a3-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="c53a3-119">Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c53a3-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c53a3-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c53a3-120">Prerequisites</span></span>
* <span data-ttu-id="c53a3-121">Vedere la [panoramica dell'esercitazione](data-factory-build-your-first-pipeline.md) ed eseguire i passaggi relativi ai **prerequisiti** .</span><span class="sxs-lookup"><span data-stu-id="c53a3-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="c53a3-122">Installare [Curl](https://curl.haxx.se/dlwiz/) nel computer.</span><span class="sxs-lookup"><span data-stu-id="c53a3-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="c53a3-123">Lo strumento CURL viene usato insieme ai comandi REST per creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-123">You use the CURL tool with REST commands to create a data factory.</span></span>
* <span data-ttu-id="c53a3-124">Seguire le istruzioni disponibili in [questo articolo](../azure-resource-manager/resource-group-create-service-principal-portal.md) per:</span><span class="sxs-lookup"><span data-stu-id="c53a3-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="c53a3-125">Creare un'applicazione Web denominata **ADFGetStartedApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="c53a3-126">Ottenere i valori per l'**ID client** e la **chiave privata**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="c53a3-127">Ottenere l' **ID tenant**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="c53a3-128">Assegnare l'applicazione **ADFGetStartedApp** al ruolo **Collaboratore Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-128">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="c53a3-129">Installare [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c53a3-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c53a3-130">Avviare **Azure PowerShell** ed eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c53a3-130">Launch **PowerShell** and run the following command.</span></span> <span data-ttu-id="c53a3-131">Mantenere aperto Azure PowerShell fino alla fine dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-131">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="c53a3-132">Se si chiude e si riapre, sarà necessario eseguire di nuovo questi comandi.</span><span class="sxs-lookup"><span data-stu-id="c53a3-132">If you close and reopen, you need to run the commands again.</span></span>
  1. <span data-ttu-id="c53a3-133">Eseguire **Login-AzureRmAccount** e immettere il nome utente e la password usati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-133">Run **Login-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span></span>
  2. <span data-ttu-id="c53a3-134">Eseguire **Get-AzureRmSubscription** per visualizzare tutte le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="c53a3-134">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span></span>
  3. <span data-ttu-id="c53a3-135">Eseguire **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** per selezionare la sottoscrizione che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="c53a3-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span></span> <span data-ttu-id="c53a3-136">Sostituire **NameOfAzureSubscription** con il nome della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-136">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span></span>
* <span data-ttu-id="c53a3-137">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo questo comando in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c53a3-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="c53a3-138">Per alcuni dei passaggi in questa esercitazione si presuppone l'uso del gruppo di risorse denominato ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="c53a3-138">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="c53a3-139">Se si usa un gruppo di risorse diverso, è necessario usare il nome del gruppo di risorse invece di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-139">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="c53a3-140">Creare le definizioni JSON</span><span class="sxs-lookup"><span data-stu-id="c53a3-140">Create JSON definitions</span></span>
<span data-ttu-id="c53a3-141">Creare i file JSON seguenti nella cartella che include curl.exe.</span><span class="sxs-lookup"><span data-stu-id="c53a3-141">Create following JSON files in the folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="c53a3-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="c53a3-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c53a3-143">Il nome deve essere univoco a livello globale, quindi è consigliabile aggiungere un prefisso/suffisso ad ADFCopyTutorialDF per renderlo univoco.</span><span class="sxs-lookup"><span data-stu-id="c53a3-143">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="c53a3-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="c53a3-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c53a3-145">Sostituire **accountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="c53a3-146">Per informazioni su come ottenere la chiave di accesso alle risorse di archiviazione, vedere le informazioni su come visualizzare, copiare e rigenerare le chiavi di accesso alle risorse di archiviazione in [Gestire l'account di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c53a3-146">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="c53a3-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="c53a3-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="c53a3-148">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="c53a3-148">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="c53a3-149">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c53a3-149">Property</span></span> | <span data-ttu-id="c53a3-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c53a3-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c53a3-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="c53a3-151">ClusterSize</span></span> |<span data-ttu-id="c53a3-152">Dimensioni del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c53a3-152">Size of the HDInsight cluster.</span></span> |
| <span data-ttu-id="c53a3-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="c53a3-153">TimeToLive</span></span> |<span data-ttu-id="c53a3-154">Specifica il tempo di inattività del cluster HDInsight, prima che sia eliminato.</span><span class="sxs-lookup"><span data-stu-id="c53a3-154">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="c53a3-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c53a3-155">linkedServiceName</span></span> |<span data-ttu-id="c53a3-156">Specifica l'account di archiviazione che viene usato per archiviare i log generati da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c53a3-156">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

<span data-ttu-id="c53a3-157">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c53a3-157">Note the following points:</span></span>

* <span data-ttu-id="c53a3-158">Data Factory crea automaticamente un cluster HDInsight **basato su Linux** con il codice JSON precedente.</span><span class="sxs-lookup"><span data-stu-id="c53a3-158">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="c53a3-159">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="c53a3-160">È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="c53a3-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c53a3-161">Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="c53a3-162">Il cluster HDInsight crea un **contenitore predefinito** nell'archivio BLOB specificato nel file JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="c53a3-162">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="c53a3-163">HDInsight non elimina il contenitore quando viene eliminato il cluster.</span><span class="sxs-lookup"><span data-stu-id="c53a3-163">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="c53a3-164">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-164">This behavior is by design.</span></span> <span data-ttu-id="c53a3-165">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che viene elaborata una sezione, a meno che non esista un cluster attivo (**timeToLive**) che viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

    <span data-ttu-id="c53a3-166">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c53a3-167">Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-167">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="c53a3-168">I nomi dei contenitori seguono questo schema: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="c53a3-168">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="c53a3-169">Per eliminare i contenitori nell'archivio BLOB di Azure, usare strumenti come [Microsoft Azure Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="c53a3-170">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="c53a3-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="c53a3-171">inputdataset.json</span></span>

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

<span data-ttu-id="c53a3-172">Il codice JSON definisce un set di dati denominato **AzureBlobInput**, che rappresenta dati di input per un'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-172">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="c53a3-173">Specifica anche che i dati di input si trovano nel contenitore BLOB denominato **adfgetstarted** e nella cartella denominata **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-173">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

<span data-ttu-id="c53a3-174">La tabella seguente fornisce le descrizioni delle proprietà JSON usate nel frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="c53a3-174">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="c53a3-175">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c53a3-175">Property</span></span> | <span data-ttu-id="c53a3-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c53a3-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c53a3-177">type</span><span class="sxs-lookup"><span data-stu-id="c53a3-177">type</span></span> |<span data-ttu-id="c53a3-178">La proprietà type è impostata su AzureBlob perché i dati si trovano nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-178">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="c53a3-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c53a3-179">linkedServiceName</span></span> |<span data-ttu-id="c53a3-180">Fa riferimento all'oggetto StorageLinkedService creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c53a3-180">refers to the StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="c53a3-181">fileName</span><span class="sxs-lookup"><span data-stu-id="c53a3-181">fileName</span></span> |<span data-ttu-id="c53a3-182">Questa proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="c53a3-182">This property is optional.</span></span> <span data-ttu-id="c53a3-183">Se si omette questa proprietà, vengono prelevati tutti i file da folderPath.</span><span class="sxs-lookup"><span data-stu-id="c53a3-183">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="c53a3-184">In tal caso viene elaborato solo il file input.log.</span><span class="sxs-lookup"><span data-stu-id="c53a3-184">In this case, only the input.log is processed.</span></span> |
| <span data-ttu-id="c53a3-185">type</span><span class="sxs-lookup"><span data-stu-id="c53a3-185">type</span></span> |<span data-ttu-id="c53a3-186">I file di log sono in formato testo, quindi viene usato TextFormat.</span><span class="sxs-lookup"><span data-stu-id="c53a3-186">The log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="c53a3-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c53a3-187">columnDelimiter</span></span> |<span data-ttu-id="c53a3-188">Le colonne nei file di log sono delimitate da virgola (,).</span><span class="sxs-lookup"><span data-stu-id="c53a3-188">columns in the log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="c53a3-189">frequenza/intervallo</span><span class="sxs-lookup"><span data-stu-id="c53a3-189">frequency/interval</span></span> |<span data-ttu-id="c53a3-190">La frequenza è impostata su Month e l'intervallo è 1, ciò significa che le sezioni di input sono disponibili con cadenza mensile.</span><span class="sxs-lookup"><span data-stu-id="c53a3-190">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
| <span data-ttu-id="c53a3-191">external</span><span class="sxs-lookup"><span data-stu-id="c53a3-191">external</span></span> |<span data-ttu-id="c53a3-192">Questa proprietà è impostata su true se i dati di input non vengono generati dal servizio Data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-192">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="c53a3-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="c53a3-193">outputdataset.json</span></span>

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

<span data-ttu-id="c53a3-194">Il codice JSON definisce un set di dati denominato **AzureBlobOutput**, che rappresenta dati di output per un'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-194">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="c53a3-195">Specifica anche che i risultati vengono archiviati nel contenitore BLOB denominato **adfgetstarted** e nella cartella denominata **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-195">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="c53a3-196">La sezione **availability** specifica che il set di dati di output viene generato su base mensile.</span><span class="sxs-lookup"><span data-stu-id="c53a3-196">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="c53a3-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="c53a3-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c53a3-198">Sostituire **storageaccountname** con il nome del proprio account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
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

<span data-ttu-id="c53a3-199">Nel frammento di codice JSON si crea una pipeline costituita da una singola attività che usa Hive per elaborare i dati in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c53a3-199">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span></span>

<span data-ttu-id="c53a3-200">Il file di script Hive, **partitionweblogs.hql**, è archiviato nell'account di archiviazione di Azure (specificato da scriptLinkedService, denominato **StorageLinkedService**) e nella cartella **script** nel contenitore **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-200">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

<span data-ttu-id="c53a3-201">La sezione **defines** specifica le impostazioni di runtime che vengono passate allo script Hive come valori di configurazione Hive, ad esempio, ${hiveconf:inputtable}, ${hiveconf:partitionedtable}.</span><span class="sxs-lookup"><span data-stu-id="c53a3-201">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="c53a3-202">Le proprietà **start** ed **end** della pipeline ne specificano il periodo attivo.</span><span class="sxs-lookup"><span data-stu-id="c53a3-202">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

<span data-ttu-id="c53a3-203">Nel codice JSON dell'attività si specifica che lo script Hive viene eseguito sulla risorsa di calcolo specificata da **linkedServiceName** - **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-203">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="c53a3-204">Per informazioni dettagliate sulle proprietà JSON usate nell'esempio precedente, vedere la sezione "Pipeline JSON" dell'articolo [Pipeline e attività in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c53a3-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="c53a3-205">Configurare le variabili globali</span><span class="sxs-lookup"><span data-stu-id="c53a3-205">Set global variables</span></span>
<span data-ttu-id="c53a3-206">In Azure PowerShell eseguire i comandi seguenti dopo avere sostituito i valori con quelli personalizzati:</span><span class="sxs-lookup"><span data-stu-id="c53a3-206">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c53a3-207">Per istruzioni su come ottenere i valori per ID client, segreto client, ID tenant e ID sottoscrizione, vedere la sezione [Prerequisiti](#prerequisites) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
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


## <a name="authenticate-with-aad"></a><span data-ttu-id="c53a3-208">Eseguire l'autenticazione con AAD</span><span class="sxs-lookup"><span data-stu-id="c53a3-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="c53a3-209">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="c53a3-209">Create data factory</span></span>
<span data-ttu-id="c53a3-210">In questo passaggio viene creata un'istanza di Azure Data Factory denominata **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="c53a3-211">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c53a3-212">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="c53a3-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c53a3-213">Ad esempio, un'attività di copia per copiare dati da un archivio dati di origine a uno di destinazione e un'attività Hive HDInsight per eseguire uno script Hive e trasformare i dati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-213">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform data.</span></span> <span data-ttu-id="c53a3-214">Eseguire i comandi seguenti per creare la data factory:</span><span class="sxs-lookup"><span data-stu-id="c53a3-214">Run the following commands to create the data factory:</span></span>

1. <span data-ttu-id="c53a3-215">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-215">Assign the command to variable named **cmd**.</span></span>

    <span data-ttu-id="c53a3-216">Verificare che il nome della data factory specificato qui (ADFCopyTutorialDF) corrisponda al nome specificato in **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-216">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c53a3-217">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-217">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c53a3-218">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-218">View the results.</span></span> <span data-ttu-id="c53a3-219">Se la data factory è stata creata correttamente, in **results** viene visualizzato il codice JSON per la data factory. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c53a3-219">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="c53a3-220">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c53a3-220">Note the following points:</span></span>

* <span data-ttu-id="c53a3-221">È necessario specificare un nome univoco globale per la Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-221">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="c53a3-222">Se nei risultati viene visualizzato l'errore **Il nome "FirstDataFactoryREST" per la data factory non è disponibile**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c53a3-222">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span></span>
  1. <span data-ttu-id="c53a3-223">Modificare il nome, ad esempio nomeutenteFirstDataFactoryREST, nel file **datafactory.json** .</span><span class="sxs-lookup"><span data-stu-id="c53a3-223">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span></span> <span data-ttu-id="c53a3-224">Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere l'argomento [Azure Data Factory - Regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="c53a3-225">Nel primo comando in cui viene assegnato un valore alla variabile **$cmd** sostituire FirstDataFactoryREST con il nuovo nome ed eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="c53a3-225">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span></span>
  3. <span data-ttu-id="c53a3-226">Eseguire i due comandi seguenti per richiamare l'API REST per creare la data factory e stampare i risultati dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-226">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span>
* <span data-ttu-id="c53a3-227">Per creare istanze di data factory, è necessario essere un collaboratore/amministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-227">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="c53a3-228">Il nome della data factory può essere registrato come nome DNS in futuro e quindi divenire visibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="c53a3-228">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="c53a3-229">Se viene visualizzato l'errore "**La sottoscrizione non è registrata per l'uso dello spazio dei nomi Microsoft.DataFactory**", eseguire una di queste operazioni e provare a ripetere la pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="c53a3-229">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="c53a3-230">In Azure PowerShell eseguire questo comando per registrare il provider di Data Factory:</span><span class="sxs-lookup"><span data-stu-id="c53a3-230">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="c53a3-231">Per verificare che il provider di Data Factory sia registrato è possibile eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="c53a3-231">You can run the following command to confirm that the Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="c53a3-232">Accedere usando la sottoscrizione di Azure nel [portale di Azure](https://portal.azure.com) e passare al pannello Data Factory oppure creare un'istanza di Data Factory nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-232">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="c53a3-233">Questa azione registra automaticamente il provider.</span><span class="sxs-lookup"><span data-stu-id="c53a3-233">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="c53a3-234">Prima di creare una pipeline è necessario creare alcune entità di Data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-234">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="c53a3-235">Creare prima di tutto i servizi collegati per collegare archivi dati/servizi di calcolo all'archivio dati, definire i set di dati di input e di output per rappresentare i dati negli archivi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-235">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c53a3-236">Creazione di servizi collegati</span><span class="sxs-lookup"><span data-stu-id="c53a3-236">Create linked services</span></span>
<span data-ttu-id="c53a3-237">In questo passaggio l'account di archiviazione di Azure e un cluster HDInsight su richiesta di Azure vengono collegati alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="c53a3-238">In questo esempio l'account di archiviazione di Azure contiene i dati di input e di output per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-238">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="c53a3-239">Il servizio HDInsight collegato viene usato per eseguire uno script Hive specificato nell'attività della pipeline in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="c53a3-239">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c53a3-240">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c53a3-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="c53a3-241">In questo passaggio l'account di archiviazione di Azure viene collegato alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-241">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="c53a3-242">In questa esercitazione viene usato lo stesso account di archiviazione di Azure per archiviare i dati di input/output e il file di script HQL.</span><span class="sxs-lookup"><span data-stu-id="c53a3-242">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="c53a3-243">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-243">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c53a3-244">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-244">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c53a3-245">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-245">View the results.</span></span> <span data-ttu-id="c53a3-246">Se il servizio collegato è stato creato correttamente, in **results** viene visualizzato il codice JSON per il servizio collegato. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c53a3-246">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="c53a3-247">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c53a3-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="c53a3-248">In questo passaggio viene collegato un cluster HDInsight su richiesta alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-248">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="c53a3-249">Il cluster HDInsight viene creato automaticamente in fase di esecuzione ed eliminato al termine dell'elaborazione, se rimane inattivo per il periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="c53a3-249">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="c53a3-250">È possibile usare il proprio cluster HDInsight anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="c53a3-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c53a3-251">Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="c53a3-252">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-252">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c53a3-253">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-253">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c53a3-254">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-254">View the results.</span></span> <span data-ttu-id="c53a3-255">Se il servizio collegato è stato creato correttamente, in **results** viene visualizzato il codice JSON per il servizio collegato. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c53a3-255">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="c53a3-256">Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="c53a3-256">Create datasets</span></span>
<span data-ttu-id="c53a3-257">In questo passaggio vengono creati set di dati per rappresentare i dati di input e di output per l'elaborazione Hive.</span><span class="sxs-lookup"><span data-stu-id="c53a3-257">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="c53a3-258">I set di dati fanno riferimento all'oggetto **StorageLinkedService** creato in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-258">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="c53a3-259">Il servizio collegato punta a un account di archiviazione di Azure e i set di dati specificano il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="c53a3-259">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="c53a3-260">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="c53a3-260">Create input dataset</span></span>
<span data-ttu-id="c53a3-261">In questo passaggio viene creato il set di dati di input per rappresentare i dati di input archiviati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-261">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="c53a3-262">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-262">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c53a3-263">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-263">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c53a3-264">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-264">View the results.</span></span> <span data-ttu-id="c53a3-265">Se il set di dati è stato creato correttamente, in **results** viene visualizzato il codice JSON per il set di dati. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c53a3-265">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="c53a3-266">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="c53a3-266">Create output dataset</span></span>
<span data-ttu-id="c53a3-267">In questo passaggio viene creato il set di dati di output per rappresentare i dati di output archiviati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-267">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="c53a3-268">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-268">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c53a3-269">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-269">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c53a3-270">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-270">View the results.</span></span> <span data-ttu-id="c53a3-271">Se il set di dati è stato creato correttamente, in **results** viene visualizzato il codice JSON per il set di dati. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c53a3-271">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="c53a3-272">Creare una pipeline</span><span class="sxs-lookup"><span data-stu-id="c53a3-272">Create pipeline</span></span>
<span data-ttu-id="c53a3-273">In questo passaggio viene creata la prima pipeline con un'attività **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="c53a3-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="c53a3-274">La sezione di input è disponibile ogni mese (frequency: Month, interval: 1), la sezione di output viene generata ogni mese e anche la proprietà dell'utilità di pianificazione dell'attività è impostata su una frequenza mensile.</span><span class="sxs-lookup"><span data-stu-id="c53a3-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="c53a3-275">Le impostazioni per il set di dati di output e l'utilità di pianificazione dell'attività devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="c53a3-275">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="c53a3-276">In questo momento la pianificazione è basata sul set di dati di output, quindi è necessario creare un set di dati di output anche se l'attività non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="c53a3-276">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="c53a3-277">Se l'attività non richiede input, è possibile ignorare la creazione del set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="c53a3-277">If the activity doesn't take any input, you can skip creating the input dataset.</span></span>

<span data-ttu-id="c53a3-278">Verificare che il file **input.log** si trovi nella cartella **adfgetstarted/inputdata** nell'archivio BLOB di Azure ed eseguire il comando seguente per distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-278">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="c53a3-279">Dal momento che gli orari di **inizio** e **fine** sono impostati nel passato e **isPaused** è impostato su false, la pipeline (l'attività nella pipeline) viene eseguita immediatamente dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-279">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="c53a3-280">Assegnare il comando alla variabile denominata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-280">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c53a3-281">Eseguire il comando usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-281">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c53a3-282">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="c53a3-282">View the results.</span></span> <span data-ttu-id="c53a3-283">Se il set di dati è stato creato correttamente, in **results** viene visualizzato il codice JSON per il set di dati. In caso contrario, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c53a3-283">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="c53a3-284">La creazione della prima pipeline tramite Azure PowerShell è così completata.</span><span class="sxs-lookup"><span data-stu-id="c53a3-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c53a3-285">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="c53a3-285">Monitor pipeline</span></span>
<span data-ttu-id="c53a3-286">In questo passaggio viene usata l'API REST di Azure Data Factory per monitorare le sezioni prodotte dalla pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-286">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

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
> <span data-ttu-id="c53a3-287">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="c53a3-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c53a3-288">Di conseguenza, prevedere **circa 30 minuti** per l'elaborazione della sezione nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-288">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
>

<span data-ttu-id="c53a3-289">Eseguire il comando Invoke e il comando successivo fino a quando la sezione non avrà stato **Pronto** o **Non riuscito**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-289">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="c53a3-290">Quando lo stato della sezione è **Pronto**, cercare i dati di output nella cartella **partitioneddata** del contenitore adfgetstarted nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="c53a3-290">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="c53a3-291">La creazione di un cluster HDInsight su richiesta di solito richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="c53a3-291">The creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![Dati di output](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="c53a3-293">Il file di input viene eliminato quando la sezione viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="c53a3-293">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="c53a3-294">Per eseguire di nuovo la sezione o ripetere l'esercitazione, caricare quindi il file di input (input.log) nella cartella inputdata del contenitore adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="c53a3-294">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

<span data-ttu-id="c53a3-295">È anche possibile usare il portale di Azure per monitorare le sezioni e risolvere eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="c53a3-295">You can also use Azure portal to monitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="c53a3-296">Per i dettagli, vedere [Creare la prima data factory di Azure usando il portale di Azure/l'editor di Data Factory](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="c53a3-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="c53a3-297">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c53a3-297">Summary</span></span>
<span data-ttu-id="c53a3-298">In questa esercitazione è stata creata un'istanza di Azure Data Factory per elaborare i dati eseguendo lo script Hive in un cluster Hadoop di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c53a3-298">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="c53a3-299">È stato usato l'editor di Data Factory nel portale di Azure per eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c53a3-299">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="c53a3-300">Creare un'istanza di Azure **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c53a3-301">Creare due **servizi collegati**:</span><span class="sxs-lookup"><span data-stu-id="c53a3-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="c53a3-302">**Archiviazione di Azure** per collegare l'archivio BLOB di Azure che contiene i file di input/output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-302">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="c53a3-303">**Azure HDInsight** per collegare un cluster Hadoop di HDInsight alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-303">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="c53a3-304">Azure Data Factory crea un cluster Hadoop di HDInsight JIT per elaborare i dati di input e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="c53a3-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="c53a3-305">Creare due **set di dati**che descrivono i dati di input e di output per l'attività Hive di HDInsight nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="c53a3-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="c53a3-306">Creare una **pipeline** con un'attività **Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c53a3-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c53a3-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c53a3-307">Next steps</span></span>
<span data-ttu-id="c53a3-308">In questo articolo è stata creata una pipeline con un'attività di trasformazione (attività HDInsight) che esegue uno script Hive in un cluster HDInsight su richiesta di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="c53a3-309">Per informazioni su come usare un'attività di copia per copiare i dati da un BLOB di Azure ad Azure SQL, vedere [Esercitazione: Copiare i dati di un BLOB di Azure in Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c53a3-309">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c53a3-310">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c53a3-310">See Also</span></span>
| <span data-ttu-id="c53a3-311">Argomento</span><span class="sxs-lookup"><span data-stu-id="c53a3-311">Topic</span></span> | <span data-ttu-id="c53a3-312">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c53a3-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c53a3-313">Informazioni di riferimento sull'API REST di Data Factory</span><span class="sxs-lookup"><span data-stu-id="c53a3-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="c53a3-314">Vedere la documentazione completa sui cmdlet di Data factory</span><span class="sxs-lookup"><span data-stu-id="c53a3-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="c53a3-315">Pipeline</span><span class="sxs-lookup"><span data-stu-id="c53a3-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c53a3-316">Questo articolo fornisce informazioni sulle pipeline e sulle attività in Azure Data Factory e su come usarle per costruire flussi di lavoro end-to-end basati sui dati per lo scenario o l'azienda.</span><span class="sxs-lookup"><span data-stu-id="c53a3-316">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c53a3-317">Set di dati</span><span class="sxs-lookup"><span data-stu-id="c53a3-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c53a3-318">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c53a3-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c53a3-319">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="c53a3-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c53a3-320">Questo articolo descrive gli aspetti di pianificazione ed esecuzione del modello applicativo di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c53a3-320">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c53a3-321">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="c53a3-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c53a3-322">Questo articolo descrive come monitorare, gestire ed eseguire il debug delle pipeline usando l'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="c53a3-322">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
