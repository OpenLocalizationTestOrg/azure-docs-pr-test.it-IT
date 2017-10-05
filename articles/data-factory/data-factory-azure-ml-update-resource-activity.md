---
title: Aggiornare i modelli di Machine Learning con Azure Data Factory | Documentazione Microsoft
description: Illustra come creare pipeline predittive usando Data factory di Azure e Azure Machine Learning
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="01b31-103">Aggiornamento dei modelli di Azure Machine Learning con Attività della risorsa di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="01b31-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="01b31-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="01b31-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="01b31-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="01b31-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="01b31-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="01b31-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="01b31-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="01b31-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="01b31-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="01b31-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="01b31-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="01b31-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="01b31-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="01b31-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="01b31-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="01b31-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="01b31-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="01b31-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="01b31-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="01b31-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="01b31-114">Questo articolo integra la versione principale di Azure Data Factory: articolo di integrazione di Azure Machine Learning: [Creare pipeline predittive tramite Azure Machine Learning e Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="01b31-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="01b31-115">Se ancora non è stato fatto, consultare l'articolo principale prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="01b31-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="01b31-116">Panoramica</span><span class="sxs-lookup"><span data-stu-id="01b31-116">Overview</span></span>
<span data-ttu-id="01b31-117">Nel corso del tempo è necessario ripetere il training dei modelli predittivi negli esperimenti di assegnazione dei punteggi di Azure ML usando nuovi set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="01b31-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="01b31-118">Una volta ripetuto il training, aggiornare il servizio Web di assegnazione dei punteggi con il modello ML di cui è stato ripetuto il training.</span><span class="sxs-lookup"><span data-stu-id="01b31-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="01b31-119">Questa è la procedura tipica per abilitare la ripetizione del training e l'aggiornamento dei modelli di Azure ML tramite i servizi Web:</span><span class="sxs-lookup"><span data-stu-id="01b31-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="01b31-120">Creare un esperimento in [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="01b31-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="01b31-121">Quando si è soddisfatti del modello, usare Azure ML Studio per pubblicare i servizi Web sia per l'**esperimento di training** che per l'**esperimento predittivo** o di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="01b31-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="01b31-122">La tabella seguente descrive i servizi Web usati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="01b31-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="01b31-123">Per altre informazioni, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](../machine-learning/machine-learning-retrain-models-programmatically.md) .</span><span class="sxs-lookup"><span data-stu-id="01b31-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="01b31-124">**Servizio Web di training**: riceve dati di training e produce modelli sottoposti a training.</span><span class="sxs-lookup"><span data-stu-id="01b31-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="01b31-125">L'output della ripetizione del training è un file con estensione ilearner in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="01b31-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="01b31-126">L' **endpoint predefinito** viene creato automaticamente quando si pubblica l'esperimento di training come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="01b31-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="01b31-127">È possibile creare altri endpoint ma l'esempio usa solo l'endpoint predefinito.</span><span class="sxs-lookup"><span data-stu-id="01b31-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="01b31-128">**Servizio Web di assegnazione dei punteggi**: riceve esempi di dati non etichettati ed esegue previsioni.</span><span class="sxs-lookup"><span data-stu-id="01b31-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="01b31-129">L'output della stima può avere diversi formati, ad esempio un file con estensione csv o righe in un database SQL di Azure, a seconda della configurazione dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="01b31-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="01b31-130">L'endpoint predefinito viene creato automaticamente quando si pubblica l'esperimento predittivo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="01b31-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="01b31-131">L'immagine seguente illustra la relazione tra gli endpoint di training e di assegnazione dei punteggi in Azure ML.</span><span class="sxs-lookup"><span data-stu-id="01b31-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVIZI WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="01b31-133">È possibile richiamare il **training web service** tramite il **Attività di esecuzione batch di Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="01b31-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="01b31-134">Richiamare il servizio Web di training è la stessa operazione che si esegue per richiamare un servizio Web di Azure ML, il servizio Web di assegnazione dei punteggi, per la valutazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="01b31-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="01b31-135">Le sezioni precedenti descrivono in dettaglio come richiamare un servizio Web di Azure ML da una pipeline di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01b31-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="01b31-136">È possibile richiamare il **scoring web service** tramite il **Attività della risorsa di aggiornamento di Azure ML** per aggiornare il servizio Web con il nuovo modello sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="01b31-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="01b31-137">Gli esempi seguenti forniscono definizioni dei servizi collegati:</span><span class="sxs-lookup"><span data-stu-id="01b31-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="01b31-138">Il servizio Web di assegnazione dei punteggi è un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="01b31-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="01b31-139">Se il servizio Web di assegnazione dei punteggi è un **servizio Web classico**, creare il secondo **endpoint non predefinito e aggiornabile** usando il [portale di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="01b31-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="01b31-140">Per la procedura, vedere l'articolo [Creare endpoint](../machine-learning/machine-learning-create-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="01b31-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="01b31-141">Dopo aver creato l'endpoint aggiornabile non predefinito, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="01b31-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="01b31-142">Fare clic su **ESECUZIONE BATCH** per ottenere il valore dell'URI per la proprietà JSON **mlEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="01b31-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="01b31-143">Fare clic su **AGGIORNA RISORSA** per ottenere il valore dell'URI per la proprietà JSON **updateResourceEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="01b31-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="01b31-144">La chiave API si trova nell'angolo in basso a destra della pagina dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="01b31-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![Endpoint aggiornabile](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="01b31-146">L'esempio seguente fornisce una definizione JSON di esempio per il servizio collegato AzureML.</span><span class="sxs-lookup"><span data-stu-id="01b31-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="01b31-147">Il servizio collegato usa il valore apiKey per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="01b31-147">The linked service uses the apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="01b31-148">Il servizio di assegnazione dei punteggi è un servizio Web di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01b31-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="01b31-149">Se il servizio Web è il nuovo tipo di servizio Web che espone un endpoint di Azure Resource Manager, non è necessario aggiungere il secondo endpoint **non predefinito**.</span><span class="sxs-lookup"><span data-stu-id="01b31-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="01b31-150">Il formato del valore **updateResourceEndpoint** nel servizio collegato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="01b31-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="01b31-151">È possibile ottenere i valori per i segnaposti nell'URL quando si eseguono query nel servizio Web nel portale di [Azure Machine Learning Web Services](https://services.azureml.net/) (Servizi Web Microsoft Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="01b31-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="01b31-152">Il nuovo tipo di endpoint di risorse di aggiornamento richiede un token AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="01b31-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="01b31-153">Specificare **servicePrincipalId** e **servicePrincipalKey** nel servizio collegato AzureML.</span><span class="sxs-lookup"><span data-stu-id="01b31-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="01b31-154">Vedere [Come creare un'entità servizio e assegnare autorizzazioni per gestire una risorsa di Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="01b31-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="01b31-155">Ecco una definizione di esempio del servizio collegato AzureML:</span><span class="sxs-lookup"><span data-stu-id="01b31-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="01b31-156">Lo scenario seguente fornisce altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="01b31-156">The following scenario provides more details.</span></span> <span data-ttu-id="01b31-157">Include un esempio per la ripetizione del training e l'aggiornamento dei modelli di Azure ML da una pipeline di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01b31-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="01b31-158">Scenario: ripetizione del training e aggiornamento di un modello di Azure ML</span><span class="sxs-lookup"><span data-stu-id="01b31-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="01b31-159">Questa sezione include una pipeline di esempio che usa **Attività di esecuzione batch di Azure ML** per ripetere il training di un modello.</span><span class="sxs-lookup"><span data-stu-id="01b31-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="01b31-160">La pipeline usa anche **Attività della risorsa di aggiornamento di Azure ML** per aggiornare il modello nel servizio Web di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="01b31-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="01b31-161">La sezione include anche frammenti di codice JSON per tutti i servizi collegati, i set di dati e la pipeline usati nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="01b31-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="01b31-162">Ecco la vista diagramma della pipeline di esempio.</span><span class="sxs-lookup"><span data-stu-id="01b31-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="01b31-163">Come si può vedere, Attività di esecuzione batch di Azure ML accetta l'input di training e genera un output di training (file iLearner).</span><span class="sxs-lookup"><span data-stu-id="01b31-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="01b31-164">Attività della risorsa di aggiornamento di Azure ML accetta questo output di training e aggiorna il modello nell'endpoint di servizio Web di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="01b31-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="01b31-165">Attività della risorsa di aggiornamento non produce un output.</span><span class="sxs-lookup"><span data-stu-id="01b31-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="01b31-166">placeholderBlob è solo un set di dati di output fittizio richiesto dal servizio Data factory di Azure per eseguire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="01b31-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![Diagramma della pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="01b31-168">Servizio collegato di archiviazione BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="01b31-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="01b31-169">Archiviazione di Azure include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="01b31-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="01b31-170">Dati di training.</span><span class="sxs-lookup"><span data-stu-id="01b31-170">training data.</span></span> <span data-ttu-id="01b31-171">Dati di input per il servizio Web di training di Azure ML.</span><span class="sxs-lookup"><span data-stu-id="01b31-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="01b31-172">File iLearner.</span><span class="sxs-lookup"><span data-stu-id="01b31-172">iLearner file.</span></span> <span data-ttu-id="01b31-173">Output del servizio Web di training di Azure ML.</span><span class="sxs-lookup"><span data-stu-id="01b31-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="01b31-174">È anche l'input per Attività della risorsa di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="01b31-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="01b31-175">Ecco la definizione JSON di esempio del servizio collegato:</span><span class="sxs-lookup"><span data-stu-id="01b31-175">Here is the sample JSON definition of the linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="01b31-176">Set di dati di input di training:</span><span class="sxs-lookup"><span data-stu-id="01b31-176">Training input dataset:</span></span>
<span data-ttu-id="01b31-177">Il set di dati seguente rappresenta i dati di training di input per il servizio Web di training di Azure ML.</span><span class="sxs-lookup"><span data-stu-id="01b31-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="01b31-178">Attività di esecuzione batch di Azure ML accetta questo set di dati come input.</span><span class="sxs-lookup"><span data-stu-id="01b31-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="01b31-179">Set di dati di output di training:</span><span class="sxs-lookup"><span data-stu-id="01b31-179">Training output dataset:</span></span>
<span data-ttu-id="01b31-180">Il set di dati seguente rappresenta il file iLearner di output del servizio Web di training di Azure ML.</span><span class="sxs-lookup"><span data-stu-id="01b31-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="01b31-181">Attività di esecuzione batch di Azure ML genera questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="01b31-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="01b31-182">Questo set di dati è anche l'input per Attività della risorsa di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="01b31-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="01b31-183">Servizio collegato per l'endpoint di training di Azure ML</span><span class="sxs-lookup"><span data-stu-id="01b31-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="01b31-184">Il frammento di codice JSON seguente definisce un servizio collegato di Azure Machine Learning che punta all'endpoint predefinito del servizio Web di training.</span><span class="sxs-lookup"><span data-stu-id="01b31-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="01b31-185">In **Azure ML Studio** eseguire queste operazioni per ottenere i valori per **mlEndpoint** e **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="01b31-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="01b31-186">Fare clic su **SERVIZI WEB** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="01b31-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="01b31-187">Fare clic su **servizio Web di training** nell'elenco dei servizi Web.</span><span class="sxs-lookup"><span data-stu-id="01b31-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="01b31-188">Fare clic su Copia accanto alla casella di testo **Chiave API** .</span><span class="sxs-lookup"><span data-stu-id="01b31-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="01b31-189">Incollare la chiave dagli Appunti nell'editor JSON di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01b31-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="01b31-190">In **Azure ML Studio** fare clic sul collegamento **ESECUZIONE BATCH**.</span><span class="sxs-lookup"><span data-stu-id="01b31-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="01b31-191">Copiare il valore di **Request URI** (URI della richiesta) dalla sezione **Richiesta** e incollarlo nell'editor JSON di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01b31-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="01b31-192">Servizio collegato per l'endpoint di assegnazione dei punteggi aggiornabile di Azure ML:</span><span class="sxs-lookup"><span data-stu-id="01b31-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="01b31-193">Il frammento di codice JSON seguente definisce un servizio collegato di Azure Machine Learning che punta all'endpoint aggiornabile non predefinito del servizio Web di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="01b31-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="01b31-194">Set di dati di output del segnaposto:</span><span class="sxs-lookup"><span data-stu-id="01b31-194">Placeholder output dataset:</span></span>
<span data-ttu-id="01b31-195">Attività della risorsa di aggiornamento di Azure ML non produce un output.</span><span class="sxs-lookup"><span data-stu-id="01b31-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="01b31-196">Tuttavia, Azure Data Factory richiede un set di dati di output per gestire la pianificazione di una pipeline,</span><span class="sxs-lookup"><span data-stu-id="01b31-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="01b31-197">quindi in questo esempio viene usato un set di dati segnaposto fittizio.</span><span class="sxs-lookup"><span data-stu-id="01b31-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="01b31-198">Pipeline</span><span class="sxs-lookup"><span data-stu-id="01b31-198">Pipeline</span></span>
<span data-ttu-id="01b31-199">La pipeline include due attività: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="01b31-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="01b31-200">Attività di esecuzione batch di Azure ML accetta i dati di training come input e genera il file con estensione iLearner come output.</span><span class="sxs-lookup"><span data-stu-id="01b31-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="01b31-201">L'attività richiama il servizio Web di training, l'esperimento di training esposto come servizio Web, con i dati di training di input e riceve il file iLearner dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="01b31-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="01b31-202">placeholderBlob è solo un set di dati di output fittizio richiesto dal servizio Data factory di Azure per eseguire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="01b31-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![Diagramma della pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
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
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
