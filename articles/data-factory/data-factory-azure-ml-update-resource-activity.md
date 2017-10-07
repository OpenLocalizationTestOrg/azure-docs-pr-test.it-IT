---
title: i modelli di Machine Learning aaaUpdate utilizzando Data Factory di Azure | Documenti Microsoft
description: Viene descritto come toocreate creare pipeline predittive con Data Factory di Azure e Azure Machine Learning
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
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="20b5f-103">Aggiornamento dei modelli di Azure Machine Learning con Attività della risorsa di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="20b5f-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="20b5f-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="20b5f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="20b5f-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="20b5f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="20b5f-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="20b5f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="20b5f-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="20b5f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="20b5f-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="20b5f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="20b5f-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="20b5f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="20b5f-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="20b5f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="20b5f-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="20b5f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="20b5f-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="20b5f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="20b5f-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="20b5f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="20b5f-114">In questo articolo fa da complemento hello principale Data Factory di Azure - articolo di integrazione di Azure Machine Learning: [creare pipeline predittive con Data Factory di Azure e di Azure Machine Learning](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="20b5f-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="20b5f-115">Se non già stato fatto, esaminare l'articolo principale hello prima di leggere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="20b5f-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="20b5f-116">Panoramica</span><span class="sxs-lookup"><span data-stu-id="20b5f-116">Overview</span></span>
<span data-ttu-id="20b5f-117">Nel corso del tempo, i modelli di previsione hello negli esperimenti di assegnazione dei punteggi di hello Azure ML devono toobe ripetere il training con nuovi set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="20b5f-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="20b5f-118">Dopo avere completato con ripetizione di training, si desidera hello tooupdate punteggio servizio web con hello ripetere il training del modello ML.</span><span class="sxs-lookup"><span data-stu-id="20b5f-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="20b5f-119">Hello passaggi tipici tooenable ripetizione di training e l'aggiornamento di modelli di Azure ML tramite i servizi web sono:</span><span class="sxs-lookup"><span data-stu-id="20b5f-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="20b5f-120">Creare un esperimento in [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="20b5f-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="20b5f-121">Quando si è soddisfatti dei modello hello, utilizzare servizi di Azure ML Studio toopublish web per entrambi hello **esperimento di training** e assegnazione dei punteggi /**esperimento predittiva**.</span><span class="sxs-lookup"><span data-stu-id="20b5f-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="20b5f-122">Hello nella tabella seguente descrive i servizi web hello utilizzati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="20b5f-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="20b5f-123">Per altre informazioni, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](../machine-learning/machine-learning-retrain-models-programmatically.md) .</span><span class="sxs-lookup"><span data-stu-id="20b5f-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="20b5f-124">**Servizio Web di training**: riceve dati di training e produce modelli sottoposti a training.</span><span class="sxs-lookup"><span data-stu-id="20b5f-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="20b5f-125">output di Hello di ripetizione di training hello è un file .ilearner in una risorsa di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="20b5f-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="20b5f-126">Hello **predefinito endpoint** viene creato automaticamente per quando si pubblica la formazione di hello riuscire come servizio web.</span><span class="sxs-lookup"><span data-stu-id="20b5f-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="20b5f-127">È possibile creare più endpoint, ma esempio hello utilizza solo endpoint di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="20b5f-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="20b5f-128">**Servizio Web di assegnazione dei punteggi**: riceve esempi di dati non etichettati ed esegue previsioni.</span><span class="sxs-lookup"><span data-stu-id="20b5f-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="20b5f-129">output di Hello di stima può avere forme diverse, ad esempio un file CSV o le righe in un database di SQL Azure, a seconda della configurazione di hello dell'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="20b5f-130">endpoint predefinito Hello viene creato automaticamente quando si pubblica l'esperimento predittiva di hello come servizio web.</span><span class="sxs-lookup"><span data-stu-id="20b5f-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="20b5f-131">Hello nella figura seguente viene illustrata hello relazione tra set di training e assegnazione dei punteggi di endpoint in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="20b5f-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVIZI WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="20b5f-133">È possibile richiamare hello **training servizio web** utilizzando hello **attività di esecuzione Batch di Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="20b5f-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="20b5f-134">Richiamare il servizio Web di training è la stessa operazione che si esegue per richiamare un servizio Web di Azure ML, il servizio Web di assegnazione dei punteggi, per la valutazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="20b5f-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="20b5f-135">Hello precedente copertura di sezioni, come un servizio web Machine Learning di Azure da una Data Factory di Azure tooinvoke della pipeline in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="20b5f-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="20b5f-136">È possibile richiamare hello **servizio web di punteggio** utilizzando hello **attività della risorsa di Azure ML aggiornamento** servizio web di hello tooupdate con modello sottoposto a training appena hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="20b5f-137">seguono esempi Hello fornisce le definizioni di servizio collegato:</span><span class="sxs-lookup"><span data-stu-id="20b5f-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="20b5f-138">Il servizio Web di assegnazione dei punteggi è un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="20b5f-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="20b5f-139">Se hello servizio web di punteggio è un **servizio web classico**, creare hello secondo **endpoint non predefinito e aggiornabile** utilizzando hello [portale di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="20b5f-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="20b5f-140">Per la procedura, vedere l'articolo [Creare endpoint](../machine-learning/machine-learning-create-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="20b5f-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="20b5f-141">Dopo aver creato endpoint aggiornabile di hello non predefinito, hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="20b5f-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="20b5f-142">Fare clic su **esecuzione BATCH** tooget hello URI valore hello **mlEndpoint** proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="20b5f-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="20b5f-143">Fare clic su **aggiornamento risorsa** tooget hello URI valore per hello del collegamento **updateresourceendpoint ' dal** proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="20b5f-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="20b5f-144">Nella pagina endpoint hello stesso è una chiave API Hello (nell'angolo in basso a destra di hello).</span><span class="sxs-lookup"><span data-stu-id="20b5f-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![Endpoint aggiornabile](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="20b5f-146">Hello di esempio seguente fornisce una definizione JSON di esempio per il servizio di Azure ml collegato hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="20b5f-147">Hello apiKey di hello servizio collegato viene utilizzato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="20b5f-147">hello linked service uses hello apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="20b5f-148">Il servizio di assegnazione dei punteggi è un servizio Web di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="20b5f-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="20b5f-149">Se il servizio web hello è hello nuovo tipo di servizio web che espone un endpoint di gestione risorse di Azure, non è necessario tooadd hello secondo **non predefinito** endpoint.</span><span class="sxs-lookup"><span data-stu-id="20b5f-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="20b5f-150">Hello **updateresourceendpoint ' dal** in hello servizio collegato è del formato hello:</span><span class="sxs-lookup"><span data-stu-id="20b5f-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="20b5f-151">È possibile ottenere valori per i segnaposto hello URL quando si eseguono query del servizio web hello in hello [portale dei servizi Web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="20b5f-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="20b5f-152">Hello nuovo tipo di endpoint di risorsa di aggiornamento richiede un token di Azure ad (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="20b5f-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="20b5f-153">Specificare **servicePrincipalId** e **servicePrincipalKey** nel servizio collegato AzureML.</span><span class="sxs-lookup"><span data-stu-id="20b5f-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="20b5f-154">Vedere [come toocreate entità del servizio e assegnare le autorizzazioni toomanage risorse di Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="20b5f-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="20b5f-155">Ecco una definizione di esempio del servizio collegato AzureML:</span><span class="sxs-lookup"><span data-stu-id="20b5f-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
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

<span data-ttu-id="20b5f-156">Hello nello scenario seguente vengono fornite informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="20b5f-156">hello following scenario provides more details.</span></span> <span data-ttu-id="20b5f-157">Include un esempio per la ripetizione del training e l'aggiornamento dei modelli di Azure ML da una pipeline di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="20b5f-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="20b5f-158">Scenario: ripetizione del training e aggiornamento di un modello di Azure ML</span><span class="sxs-lookup"><span data-stu-id="20b5f-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="20b5f-159">In questa sezione fornisce una pipeline di esempio che utilizza hello **attività esecuzione Batch di Azure ML** tooretrain un modello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="20b5f-160">pipeline di Hello utilizza inoltre hello **attività di Azure ML aggiornamento risorsa** modello hello tooupdate hello punteggio servizio web.</span><span class="sxs-lookup"><span data-stu-id="20b5f-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="20b5f-161">sezione Hello nonché hello di frammenti di codice JSON per tutti i servizi collegati, i set di dati e della pipeline nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="20b5f-162">Di seguito è una vista diagramma hello della pipeline di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="20b5f-163">Come si può notare, hello attività di esecuzione Batch di Azure ML accetta input di training hello e produce un output di training (file iLearner).</span><span class="sxs-lookup"><span data-stu-id="20b5f-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="20b5f-164">Attività della risorsa di Azure ML aggiornamento Hello accetta l'output di training e aggiornamenti hello modello hello punteggio endpoint del servizio web.</span><span class="sxs-lookup"><span data-stu-id="20b5f-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="20b5f-165">Hello attività della risorsa di aggiornamento non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="20b5f-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="20b5f-166">placeholderBlob Hello è solo un set di dati del fittizio output richiesto dalla pipeline di hello toorun di hello Data Factory di Azure del servizio.</span><span class="sxs-lookup"><span data-stu-id="20b5f-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![Diagramma della pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="20b5f-168">Servizio collegato di archiviazione BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="20b5f-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="20b5f-169">Archiviazione di Azure Hello contiene hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="20b5f-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="20b5f-170">Dati di training.</span><span class="sxs-lookup"><span data-stu-id="20b5f-170">training data.</span></span> <span data-ttu-id="20b5f-171">dati di input Hello per servizio web di hello Azure ML training.</span><span class="sxs-lookup"><span data-stu-id="20b5f-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="20b5f-172">File iLearner.</span><span class="sxs-lookup"><span data-stu-id="20b5f-172">iLearner file.</span></span> <span data-ttu-id="20b5f-173">Hello output dal servizio web di hello Azure ML training.</span><span class="sxs-lookup"><span data-stu-id="20b5f-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="20b5f-174">Questo file è inoltre hello input toohello attività di aggiornamento risorsa.</span><span class="sxs-lookup"><span data-stu-id="20b5f-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="20b5f-175">Ecco definizione JSON di esempio hello del servizio collegato hello:</span><span class="sxs-lookup"><span data-stu-id="20b5f-175">Here is hello sample JSON definition of hello linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="20b5f-176">Set di dati di input di training:</span><span class="sxs-lookup"><span data-stu-id="20b5f-176">Training input dataset:</span></span>
<span data-ttu-id="20b5f-177">Hello seguente set di dati rappresenta i dati di training input hello per servizio web di hello Azure ML training.</span><span class="sxs-lookup"><span data-stu-id="20b5f-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="20b5f-178">l'attività di esecuzione Batch di Azure ML Hello accetta questo set di dati come input.</span><span class="sxs-lookup"><span data-stu-id="20b5f-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="20b5f-179">Set di dati di output di training:</span><span class="sxs-lookup"><span data-stu-id="20b5f-179">Training output dataset:</span></span>
<span data-ttu-id="20b5f-180">Hello seguente set di dati rappresenta hello iLearner file di output dal servizio web di hello Azure ML training.</span><span class="sxs-lookup"><span data-stu-id="20b5f-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="20b5f-181">Attività di esecuzione Batch di Azure ML Hello produce questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="20b5f-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="20b5f-182">Questo set di dati è inoltre hello input toohello attività di Azure ML aggiornamento risorsa.</span><span class="sxs-lookup"><span data-stu-id="20b5f-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="20b5f-183">Servizio collegato per l'endpoint di training di Azure ML</span><span class="sxs-lookup"><span data-stu-id="20b5f-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="20b5f-184">Hello frammento di codice JSON seguente definisce un servizio collegato di Azure Machine Learning che fa riferimento a endpoint predefinito toohello del servizio web di training hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

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

<span data-ttu-id="20b5f-185">In **Azure ML Studio**, hello tooget i valori per seguenti **mlEndpoint** e **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="20b5f-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="20b5f-186">Fare clic su **servizi WEB** nel menu di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="20b5f-187">Fare clic su hello **training servizio web** nell'elenco di hello dei servizi web.</span><span class="sxs-lookup"><span data-stu-id="20b5f-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="20b5f-188">Fare clic su Copia Avanti troppo**chiave API** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="20b5f-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="20b5f-189">Incollare la chiave hello negli Appunti hello nell'editor di JSON Factory dati hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="20b5f-190">In hello **Azure ML studio**, fare clic su **esecuzione BATCH** collegamento.</span><span class="sxs-lookup"><span data-stu-id="20b5f-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="20b5f-191">Hello copia **URI della richiesta** da hello **richiesta** sezione e incollarlo nell'editor delle Data Factory JSON hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="20b5f-192">Servizio collegato per l'endpoint di assegnazione dei punteggi aggiornabile di Azure ML:</span><span class="sxs-lookup"><span data-stu-id="20b5f-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="20b5f-193">Hello frammento di codice JSON seguente definisce un servizio collegato di Azure Machine Learning che fa riferimento a endpoint aggiornabile di toohello non predefinito di hello punteggio servizio web.</span><span class="sxs-lookup"><span data-stu-id="20b5f-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="20b5f-194">Set di dati di output del segnaposto:</span><span class="sxs-lookup"><span data-stu-id="20b5f-194">Placeholder output dataset:</span></span>
<span data-ttu-id="20b5f-195">attività di Azure ML aggiornamento risorsa Hello non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="20b5f-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="20b5f-196">Tuttavia, Data Factory di Azure richiede una pianificazione di hello output toodrive set di dati di una pipeline.</span><span class="sxs-lookup"><span data-stu-id="20b5f-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="20b5f-197">quindi in questo esempio viene usato un set di dati segnaposto fittizio.</span><span class="sxs-lookup"><span data-stu-id="20b5f-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="20b5f-198">Pipeline</span><span class="sxs-lookup"><span data-stu-id="20b5f-198">Pipeline</span></span>
<span data-ttu-id="20b5f-199">Hello pipeline dispone di due attività: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="20b5f-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="20b5f-200">l'attività di esecuzione Batch di Azure ML Hello accetta i dati di training hello come input e genera un file iLearner come output.</span><span class="sxs-lookup"><span data-stu-id="20b5f-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="20b5f-201">attività Hello richiama il servizio web di formazione hello (esperimento di training esposta come servizio web) con input hello i dati di training e riceve file ilearner hello dal servizio Web hello.</span><span class="sxs-lookup"><span data-stu-id="20b5f-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="20b5f-202">placeholderBlob Hello è solo un set di dati del fittizio output richiesto dalla pipeline di hello toorun di hello Data Factory di Azure del servizio.</span><span class="sxs-lookup"><span data-stu-id="20b5f-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

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
