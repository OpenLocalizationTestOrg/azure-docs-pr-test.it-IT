---
title: Creare pipeline di dati predittive tramite Azure Data Factory | Microsoft Docs
description: Illustra come creare pipeline predittive usando Data factory di Azure e Azure Machine Learning
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="d007e-103">Creare pipeline predittive tramite Azure Machine Learning e Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d007e-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="d007e-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="d007e-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="d007e-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="d007e-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="d007e-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="d007e-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="d007e-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="d007e-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="d007e-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="d007e-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="d007e-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d007e-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="d007e-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d007e-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="d007e-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="d007e-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="d007e-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d007e-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="d007e-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="d007e-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="d007e-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d007e-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="d007e-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d007e-115">Azure Machine Learning</span></span>
<span data-ttu-id="d007e-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) consente di compilare, testare e distribuire soluzioni di analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="d007e-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="d007e-117">Da un punto di vista generale, questo avviene in tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="d007e-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="d007e-118">**Creare un esperimento di training**.</span><span class="sxs-lookup"><span data-stu-id="d007e-118">**Create a training experiment**.</span></span> <span data-ttu-id="d007e-119">Questo passaggio deve essere eseguito con Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="d007e-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="d007e-120">Azure ML Studio è un ambiente di sviluppo visivo di collaborazione usato per eseguire il training e il test di un modello di analisi predittiva usando dati di training.</span><span class="sxs-lookup"><span data-stu-id="d007e-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="d007e-121">**Convertirlo in un esperimento predittivo**.</span><span class="sxs-lookup"><span data-stu-id="d007e-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="d007e-122">Dopo aver eseguito il training del modello con i dati esistenti, preparare e semplificare l'esperimento di assegnazione dei punteggi quando si è pronti a usarlo per valutare nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="d007e-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="d007e-123">**Distribuirlo come servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="d007e-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="d007e-124">È possibile pubblicare l'esperimento di assegnazione dei punteggi come servizio Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="d007e-125">È possibile inviare dati al modello tramite l'endpoint di questo servizio Web e ricevere le stime dei risultati dal modello.</span><span class="sxs-lookup"><span data-stu-id="d007e-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="d007e-126">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="d007e-126">Azure Data Factory</span></span>
<span data-ttu-id="d007e-127">Data factory è un servizio di integrazione dei dati basato sul cloud che permette di automatizzare lo **spostamento** e la **trasformazione** dei dati.</span><span class="sxs-lookup"><span data-stu-id="d007e-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="d007e-128">È possibile creare soluzioni di integrazione dei dati usando Azure Data Factory che può inserire dati da diversi archivi dati, trasformare/elaborare i dati e pubblicare i dati risultanti negli archivi dati.</span><span class="sxs-lookup"><span data-stu-id="d007e-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="d007e-129">Il servizio Data Factory consente di creare pipeline di dati che spostano e trasformano i dati e quindi di eseguire le pipeline in base a una pianificazione specificata (ogni ora, ogni giorno, ogni settimana e così via).</span><span class="sxs-lookup"><span data-stu-id="d007e-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="d007e-130">Offre anche viste avanzate per visualizzare la derivazione e le dipendenze tra le pipeline di dati e monitorare tutte le pipeline di dati da una singola visualizzazione unificata per individuare facilmente i problemi e configurare avvisi di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="d007e-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="d007e-131">Per una rapida introduzione al servizio Azure Data Factory, vedere gli articoli [Introduzione al servizio Azure Data Factory](data-factory-introduction.md) e [Creare la prima pipeline](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="d007e-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="d007e-132">Data Factory e Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d007e-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="d007e-133">Azure Data Factory consente di creare facilmente pipeline che usano un servizio Web pubblicato di [Azure Machine Learning][azure-machine-learning] per l'analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="d007e-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="d007e-134">Con **Attività di esecuzione batch** in una pipeline di Data factory di Azure è possibile richiamare un servizio Web di Azure ML per eseguire stime dei dati in batch.</span><span class="sxs-lookup"><span data-stu-id="d007e-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="d007e-135">Per altre informazioni, vedere la sezione [Richiamo di un servizio Web di Azure ML tramite Attività di esecuzione batch](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) .</span><span class="sxs-lookup"><span data-stu-id="d007e-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="d007e-136">Nel corso del tempo è necessario ripetere il training dei modelli predittivi negli esperimenti di assegnazione dei punteggi di Azure ML usando nuovi set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="d007e-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="d007e-137">È possibile ripetere il training di un modello di Azure ML da una pipeline di Data factory seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d007e-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="d007e-138">Pubblicare l'esperimento di training, non l'esperimento predittivo, come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="d007e-139">Eseguire questo passaggio in Azure ML Studio come è stato fatto per esporre l'esperimento predittivo come servizio Web nello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="d007e-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="d007e-140">Usare Attività di esecuzione batch di Azure ML per richiamare il servizio Web per l'esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="d007e-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="d007e-141">In sostanza, è possibile usare Attività di esecuzione batch di Azure ML per richiamare sia il servizio Web di training che il servizio Web di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="d007e-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="d007e-142">Al termine della ripetizione del training, aggiornare il servizio Web di assegnazione dei punteggi, ovvero l'esperimento predittivo esposto come servizio Web, con il modello appena sottoposto a training usando l'**Attività della risorsa di aggiornamento di Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="d007e-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="d007e-143">Per informazioni dettagliate, vedere l'articolo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Aggiornamento dei modelli con Attività della risorsa di aggiornamento).</span><span class="sxs-lookup"><span data-stu-id="d007e-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="d007e-144">Richiamo di un servizio Web tramite Attività di esecuzione batch</span><span class="sxs-lookup"><span data-stu-id="d007e-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="d007e-145">È possibile usare Data factory di Azure per gestire l'elaborazione e lo spostamento dei dati e quindi effettuare un'esecuzione batch tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d007e-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="d007e-146">Ecco i passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="d007e-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="d007e-147">Creare un servizio collegato di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d007e-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="d007e-148">Sono necessari i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="d007e-148">You need the following values:</span></span>

   1. <span data-ttu-id="d007e-149">**URI della richiesta** per l’API di esecuzione batch.</span><span class="sxs-lookup"><span data-stu-id="d007e-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="d007e-150">È possibile trovare l'URI della richiesta facendo clic sul collegamento **ESECUZIONE BATCH** nella pagina dei servizi Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="d007e-151">**API key** per il servizio Web di Azure Machine Learning pubblicato.</span><span class="sxs-lookup"><span data-stu-id="d007e-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="d007e-152">È possibile trovare la chiave API facendo clic sul servizio Web pubblicato.</span><span class="sxs-lookup"><span data-stu-id="d007e-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="d007e-153">Usare l'attività **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="d007e-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Dashboard di Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Batch URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="d007e-156">Scenario: Esperimenti di uso degli input/output del servizio Web che fanno riferimento ai dati presenti nell'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d007e-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="d007e-157">Il questo scenario il servizio Web Azure Machine Learning esegue stime usando dati provenienti da un file dell'archiviazione BLOB di Azure e archivia i risultati nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="d007e-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="d007e-158">Il frammento di codice JSON seguente definisce una pipeline di Data factory con un'attività AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="d007e-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="d007e-159">L'attività include il set di dati **DecisionTreeInputBlob** come input e il set di dati **DecisionTreeResultBlob** come output.</span><span class="sxs-lookup"><span data-stu-id="d007e-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="d007e-160">Il set di dati **DecisionTreeInputBlob** viene passato come input al servizio Web usando la proprietà JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="d007e-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="d007e-161">Il set di dati **DecisionTreeResultBlob** viene passato come output al servizio Web usando la proprietà JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="d007e-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d007e-162">Se il servizio Web accetta più input, usare la proprietà **webServiceInputs** invece di **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="d007e-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="d007e-163">Vedere la sezione [Il servizio Web richiede più input](#web-service-requires-multiple-inputs) per un esempio di uso della proprietà webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="d007e-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="d007e-164">I set di dati a cui fanno riferimento le proprietà **webServiceInput**/**webServiceInputs** e **webServiceOutputs** (in **typeProperties**) devono essere inclusi anche negli **input** e **output** dell'attività.</span><span class="sxs-lookup"><span data-stu-id="d007e-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="d007e-165">Nell'esperimento di Machine Learning di Azure,le porte e i parametri globali di input e output del servizio Web hanno nomi predefiniti ("input1", "input2") che è possibile personalizzare.</span><span class="sxs-lookup"><span data-stu-id="d007e-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="d007e-166">I nomi scelti per le impostazioni webServiceInputs, webServiceOutputs e globalParameters devono corrispondere esattamente ai nomi negli esperimenti.</span><span class="sxs-lookup"><span data-stu-id="d007e-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="d007e-167">Per verificare il mapping previsto, è possibile visualizzare il payload della richiesta di esempio nella pagina della Guida relativa all'esecuzione in batch per l'endpoint di Machine Learning di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="d007e-168">Possono essere passati come parametri per il servizio Web solo input e output dell'attività AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="d007e-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="d007e-169">Nel precedente snippet JSON, ad esempio, DecisionTreeInputBlob è un input per l'attività AzureMLBatchExecution e viene passato come input al servizio Web tramite il parametro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="d007e-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="d007e-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="d007e-170">Example</span></span>
<span data-ttu-id="d007e-171">Questo esempio usa Archiviazione di Azure per archiviare i dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="d007e-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="d007e-172">Prima di procedere con questo esempio, è consigliabile eseguire l'esercitazione relativa alla [creazione della prima pipeline con Data Factory][adf-build-1st-pipeline].</span><span class="sxs-lookup"><span data-stu-id="d007e-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="d007e-173">Usare l'editor di Data Factory per creare elementi di Data Factory, come servizi collegati, set di dati e pipeline, in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="d007e-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="d007e-174">Creare un **servizio collegato** per **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d007e-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="d007e-175">Se i file di input e output si trovano in account di archiviazione diversi, sono necessari due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="d007e-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="d007e-176">Di seguito è fornito un esempio JSON:</span><span class="sxs-lookup"><span data-stu-id="d007e-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="d007e-177">Creare il **set di dati** di **input** di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d007e-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="d007e-178">A differenza di altri set di dati di Data Factory, questi devono includere entrambi i valori **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="d007e-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="d007e-179">È possibile usare il partizionamento per fare in modo che ogni esecuzione di batch (ogni sezione di dati) elabori o produca file di input e di output univoci.</span><span class="sxs-lookup"><span data-stu-id="d007e-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="d007e-180">Può essere necessario includere alcune attività upstream per trasformare il file di input in formato CSV e inserirlo nell'account di archiviazione per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="d007e-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="d007e-181">In tal caso, non è necessario includere le impostazioni **external** ed **externalData** illustrate nell'esempio seguente e DecisionTreeInputBlob sarà il set di dati di output di un'attività diversa.</span><span class="sxs-lookup"><span data-stu-id="d007e-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    <span data-ttu-id="d007e-182">Il file con estensione csv di input deve avere una riga di intestazione di colonna.</span><span class="sxs-lookup"><span data-stu-id="d007e-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="d007e-183">Se si usa l'**attività di copia** per creare/spostare il file CSV nell'archivio BLOB, è consigliabile impostare la proprietà **blobWriterAddHeader** del sink su **true**.</span><span class="sxs-lookup"><span data-stu-id="d007e-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="d007e-184">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d007e-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="d007e-185">Se il file CSV non ha la riga di intestazione, potrebbe essere visualizzato un messaggio di errore analogo al seguente: **Errore nell'attività: Errore di lettura della stringa. Token imprevisto: StartObject. Percorso '', riga 1, posizione 1**.</span><span class="sxs-lookup"><span data-stu-id="d007e-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="d007e-186">Creare il **set di dati** di **output** di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d007e-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="d007e-187">In questo esempio il file di output usa il partizionamento per creare un percorso di output univoco per l'esecuzione di ciascuna sezione.</span><span class="sxs-lookup"><span data-stu-id="d007e-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="d007e-188">Senza il partizionamento l'attività sovrascriverà il file.</span><span class="sxs-lookup"><span data-stu-id="d007e-188">Without the partitioning, the activity would overwrite the file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="d007e-189">Creare un **servizio collegato** di tipo **AzureMLLinkedService** che fornisce la chiave API e un modello di URL per l'esecuzione batch.</span><span class="sxs-lookup"><span data-stu-id="d007e-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="d007e-190">Creare infine una pipeline contenente un'attività **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="d007e-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="d007e-191">In fase di esecuzione la pipeline segue questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d007e-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="d007e-192">Ottiene il percorso del file di input dal set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="d007e-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="d007e-193">Richiama l'API di esecuzione batch di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d007e-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="d007e-194">Copia l'output di esecuzione batch nel BLOB specificato nel set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="d007e-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d007e-195">L'attività AzureMLBatchExecution può avere zero o più input e uno o più output.</span><span class="sxs-lookup"><span data-stu-id="d007e-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="d007e-196">Per la data e l'ora di **inizio** e di **fine** è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="d007e-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="d007e-197">ad esempio 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="d007e-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="d007e-198">Se non si specifica un valore per la proprietà **Inizio + 48 ore** ".</span><span class="sxs-lookup"><span data-stu-id="d007e-198">The **end** time is optional.</span></span> <span data-ttu-id="d007e-199">Se non si specifica alcun valore per la proprietà **end**, il valore verrà calcolato come "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="d007e-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="d007e-200">Per eseguire la pipeline illimitatamente, specificare **9999-09-09** come valore per la proprietà **end**.</span><span class="sxs-lookup"><span data-stu-id="d007e-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="d007e-201">Per informazioni dettagliate sulle proprietà JSON, vedere [Informazioni di riferimento sugli script JSON di Data Factory](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d007e-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d007e-202">La specifica dell'input per l'attività AzureMLBatchExecution è opzionale.</span><span class="sxs-lookup"><span data-stu-id="d007e-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="d007e-203">Scenario: Esperimenti di uso dei moduli Reader e Writer per fare riferimento ai dati in diversi archivi</span><span class="sxs-lookup"><span data-stu-id="d007e-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="d007e-204">Un altro scenario comune durante la creazione di esperimenti di Azure ML è quello relativo all'uso dei moduli Reader e Writer.</span><span class="sxs-lookup"><span data-stu-id="d007e-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="d007e-205">Il modulo Reader consente di caricare i dati in un esperimento, mentre il modulo Writer consente di salvare i dati derivanti dagli esperimenti.</span><span class="sxs-lookup"><span data-stu-id="d007e-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="d007e-206">Per informazioni dettagliate sui moduli Reader e Writer, vedere gli argomenti [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) in MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="d007e-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="d007e-207">Quando si usano i moduli Reader e Writer, è consigliabile usare un parametro del servizio Web per ciascuna proprietà di tali moduli.</span><span class="sxs-lookup"><span data-stu-id="d007e-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="d007e-208">Questi parametri Web consentono di configurare i valori durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="d007e-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="d007e-209">Ad esempio, è possibile creare un esperimento con un modulo Reader che usa un database SQL di Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d007e-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="d007e-210">Dopo aver distribuito il servizio Web, si desidera consentire ai consumer del servizio Web di specificare un altro server SQL di Azure denominato YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d007e-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="d007e-211">È possibile usare un parametro del servizio Web per consentire la configurazione di questo valore.</span><span class="sxs-lookup"><span data-stu-id="d007e-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="d007e-212">L'input e l'output del servizio Web sono diversi dai parametri del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="d007e-213">Nel primo scenario è stato illustrato come è possibile specificare un input e un output per un servizio Web Azure ML.</span><span class="sxs-lookup"><span data-stu-id="d007e-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="d007e-214">In questo scenario si passano i parametri per un servizio Web corrispondenti alle proprietà dei moduli Reader e Writer.</span><span class="sxs-lookup"><span data-stu-id="d007e-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="d007e-215">Viene preso in esame uno scenario relativo all'uso dei parametri del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="d007e-216">È stato distribuito un servizio Web di Azure Machine Learning che usa un modulo Reader per leggere i dati da una delle origini dati di Azure Machine Learning supportate, ad esempio un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="d007e-217">Dopo l'esecuzione batch, i risultati vengono scritti usando un modulo Writer (database SQL di Azure).</span><span class="sxs-lookup"><span data-stu-id="d007e-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="d007e-218">Negli esperimenti non sono definiti input e output del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="d007e-219">In questo caso, è consigliabile configurare i parametri del servizio Web rilevanti per i moduli Reader e Writer.</span><span class="sxs-lookup"><span data-stu-id="d007e-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="d007e-220">Ciò consente la configurazione dei moduli Reader e Writer quando si usa l'attività AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="d007e-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="d007e-221">Specificare i parametri del servizio Web nella sezione **globalParameters** del codice JSON dell'attività come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d007e-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="d007e-222">È anche possibile usare le [funzioni di Data factory](data-factory-functions-variables.md) per passare i valori per i parametri del servizio Web, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d007e-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="d007e-223">I parametri del servizio Web applicano la distinzione tra maiuscole e minuscole. È quindi necessario assicurarsi che i nomi specificati nel file JSON dell'attività corrispondano ai nomi esposti dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="d007e-224">Uso di un modulo Reader per leggere dati da più file del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d007e-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="d007e-225">Le pipeline di Big Data, con attività come Pig e Hive, possono generare uno o più file di output senza estensioni.</span><span class="sxs-lookup"><span data-stu-id="d007e-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="d007e-226">Ad esempio, quando si specifica una tabella Hive esterna, i dati per tale tabella possono essere archiviati nell'archiviazione BLOB di Azure con il nome 000000_0.</span><span class="sxs-lookup"><span data-stu-id="d007e-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="d007e-227">È possibile usare il modulo Reader in un esperimento per la lettura di più file e usare questi ultimi per creare delle stime.</span><span class="sxs-lookup"><span data-stu-id="d007e-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="d007e-228">Quando si usa il modulo Reader in un esperimento di Azure Machine Learning, è possibile specificare il BLOB di Azure come input.</span><span class="sxs-lookup"><span data-stu-id="d007e-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="d007e-229">I file nell'archivio BLOB di Azure possono essere file di output, ad esempio 000000_0, generati da uno script Pig e Hive in esecuzione in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d007e-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="d007e-230">Il modulo Reader consente di leggere i file, senza estensioni, configurando la voce **Path to container, directory or blob**(Percorso del contenitore, della directory o del BLOB).</span><span class="sxs-lookup"><span data-stu-id="d007e-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="d007e-231">La parte relativa al **percorso del contenitore** punta al contenitore, mentre **directory o BLOB** punta alla cartella che contiene i file, come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="d007e-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="d007e-232">L'asterisco (\*) **specifica che tutti i file nel contenitore o nella cartella, ovvero data/aggregateddata/year=2014/month-6/\***, vengono letti come parte dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="d007e-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Proprietà del Blob Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="d007e-234">Esempio</span><span class="sxs-lookup"><span data-stu-id="d007e-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="d007e-235">Pipeline con l'attività AzureMLBatchExecution con parametri del servizio Web</span><span class="sxs-lookup"><span data-stu-id="d007e-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
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
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="d007e-236">Nell'esempio JSON precedente:</span><span class="sxs-lookup"><span data-stu-id="d007e-236">In the above JSON example:</span></span>

* <span data-ttu-id="d007e-237">Il servizio Web Azure Machine Learning distribuito usa un modulo Reader e un modulo Writer per leggere e scrivere i dati da e in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="d007e-238">Il servizio Web espone i quattro parametri seguenti: Database server name, Database name, Server user account name e Server user account password.</span><span class="sxs-lookup"><span data-stu-id="d007e-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="d007e-239">Per la data e l'ora di **inizio** e di **fine** è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="d007e-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="d007e-240">ad esempio 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="d007e-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="d007e-241">Se non si specifica un valore per la proprietà **Inizio + 48 ore** ".</span><span class="sxs-lookup"><span data-stu-id="d007e-241">The **end** time is optional.</span></span> <span data-ttu-id="d007e-242">Se non si specifica alcun valore per la proprietà **end**, il valore verrà calcolato come "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="d007e-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="d007e-243">Per eseguire la pipeline illimitatamente, specificare **9999-09-09** come valore per la proprietà **end**.</span><span class="sxs-lookup"><span data-stu-id="d007e-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="d007e-244">Per informazioni dettagliate sulle proprietà JSON, vedere [Informazioni di riferimento sugli script JSON di Data Factory](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d007e-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="d007e-245">Altri scenari</span><span class="sxs-lookup"><span data-stu-id="d007e-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="d007e-246">Il servizio Web richiede più input</span><span class="sxs-lookup"><span data-stu-id="d007e-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="d007e-247">Se il servizio Web accetta più input, usare la proprietà **webServiceInputs** invece di **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="d007e-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="d007e-248">Includere anche i set di dati a cui **webServiceInputs** fa riferimento negli **input** dell'attività.</span><span class="sxs-lookup"><span data-stu-id="d007e-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="d007e-249">Nell'esperimento di Machine Learning di Azure,le porte e i parametri globali di input e output del servizio Web hanno nomi predefiniti ("input1", "input2") che è possibile personalizzare.</span><span class="sxs-lookup"><span data-stu-id="d007e-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="d007e-250">I nomi scelti per le impostazioni webServiceInputs, webServiceOutputs e globalParameters devono corrispondere esattamente ai nomi negli esperimenti.</span><span class="sxs-lookup"><span data-stu-id="d007e-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="d007e-251">Per verificare il mapping previsto, è possibile visualizzare il payload della richiesta di esempio nella pagina della Guida relativa all'esecuzione in batch per l'endpoint di Machine Learning di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="d007e-252">Servizio Web non richiede un input</span><span class="sxs-lookup"><span data-stu-id="d007e-252">Web Service does not require an input</span></span>
<span data-ttu-id="d007e-253">I servizi Web per l'esecuzione batch di Azure ML possono essere usati per eseguire flussi di lavoro, ad esempio script R o Python, che possono non richiedere alcun input.</span><span class="sxs-lookup"><span data-stu-id="d007e-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="d007e-254">In alternativa, l'esperimento può essere configurato con un modulo Reader che non espone proprietà GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="d007e-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="d007e-255">In tal caso l'attività AzureMLBatchExecution verrà configurata come segue:</span><span class="sxs-lookup"><span data-stu-id="d007e-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="d007e-256">Servizio Web non richiede un input/output</span><span class="sxs-lookup"><span data-stu-id="d007e-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="d007e-257">Il servizio Web per l'esecuzione batch di Azure ML può non disporre di alcun output del servizio Web configurato.</span><span class="sxs-lookup"><span data-stu-id="d007e-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="d007e-258">In questo esempio non sono disponibili input o output del servizio Web, né alcuna proprietà GlobalParameters configurata.</span><span class="sxs-lookup"><span data-stu-id="d007e-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="d007e-259">È ancora presente un output configurato nell'attività stessa, ma non viene fornito come webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="d007e-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="d007e-260">Il servizio Web usa moduli Reader e Writer e l'attività viene eseguita solo quando le altre attività hanno avuto esito positivo</span><span class="sxs-lookup"><span data-stu-id="d007e-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="d007e-261">I moduli Reader e Writer del servizio Web di Azure ML possono essere configurati per l'esecuzione con o senza proprietà GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="d007e-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="d007e-262">Tuttavia, è possibile incorporare chiamate al servizio in una pipeline che usa le dipendenze del set di dati per richiamare il servizio solo dopo il completamento di alcune operazioni di elaborazione upstream.</span><span class="sxs-lookup"><span data-stu-id="d007e-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="d007e-263">Si possono anche attivare altre azioni dopo il completamento dell'esecuzione batch usando questo approccio.</span><span class="sxs-lookup"><span data-stu-id="d007e-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="d007e-264">In tal caso è possibile esprimere le dipendenze tramite gli input e gli output dell'attività, senza denominarli input o output del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="d007e-265">Ecco i **punti chiave** :</span><span class="sxs-lookup"><span data-stu-id="d007e-265">The **takeaways** are:</span></span>

* <span data-ttu-id="d007e-266">Se l'endpoint dell'esperimento usa la proprietà webServiceInput, questa è rappresentata da un set di dati del BLOB ed è inclusa negli input dell'attività e nella proprietà webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="d007e-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="d007e-267">In caso contrario, la proprietà webServiceInput viene omessa.</span><span class="sxs-lookup"><span data-stu-id="d007e-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="d007e-268">Se l'endpoint dell'esperimento usa le proprietà webServiceOutputs, queste sono rappresentate da un set di dati del BLOB e sono incluse negli output dell'attività e nella proprietà webServiceOutputs.</span><span class="sxs-lookup"><span data-stu-id="d007e-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="d007e-269">Il mapping degli output dell'attività e di webServiceOutputs viene eseguito in base al nome di ogni output nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="d007e-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="d007e-270">In caso contrario, la proprietà webServiceOutputs viene omessa.</span><span class="sxs-lookup"><span data-stu-id="d007e-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="d007e-271">Se l'endpoint dell'esperimento espone le proprietà globalParameters, vengono assegnate alla proprietà globalParameters dell'attività come coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="d007e-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="d007e-272">In caso contrario, la proprietà globalParameters viene omessa.</span><span class="sxs-lookup"><span data-stu-id="d007e-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="d007e-273">Le chiavi distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="d007e-273">The keys are case-sensitive.</span></span> <span data-ttu-id="d007e-274">[funzioni di Data factory di Azure](data-factory-functions-variables.md) possono essere usate nei valori.</span><span class="sxs-lookup"><span data-stu-id="d007e-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="d007e-275">Nelle proprietà di input e output delle dell'attività possono essere inclusi set di dati aggiuntivi, senza che vi si faccia riferimento nella sezione typeProperties dell'attività.</span><span class="sxs-lookup"><span data-stu-id="d007e-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="d007e-276">Questi set di dati regolano l'esecuzione tramite le dipendenze delle sezioni, ma in caso contrario vengono ignorati dall'attività AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="d007e-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="d007e-277">Aggiornamento dei modelli con Attività della risorsa di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="d007e-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="d007e-278">Al termine della ripetizione del training, aggiornare il servizio Web di assegnazione dei punteggi, ovvero l'esperimento predittivo esposto come servizio Web, con il modello appena sottoposto a training usando l'**Attività della risorsa di aggiornamento di Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="d007e-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="d007e-279">Per informazioni dettagliate, vedere l'articolo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Aggiornamento dei modelli con Attività della risorsa di aggiornamento).</span><span class="sxs-lookup"><span data-stu-id="d007e-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="d007e-280">Moduli Reader e Writer </span><span class="sxs-lookup"><span data-stu-id="d007e-280">Reader and Writer Modules</span></span>
<span data-ttu-id="d007e-281">Uno scenario comune per l'uso dei parametri del servizio Web è costituito dai reader e dai writer SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="d007e-282">Il modulo Reader viene usato per caricare i dati in un esperimento dai servizi di gestione dati all'esterno di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d007e-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="d007e-283">Il modulo Writer viene usato per salvare i dati degli esperimenti in servizi di gestione dati all'esterno di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d007e-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="d007e-284">Per informazioni dettagliate sui BLOB di Azure o sui moduli Reader e Writer SQL di Azure, vedere gli argomenti [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) in MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="d007e-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="d007e-285">L'esempio della sezione precedente usa un reader e un writer di BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="d007e-286">Questa sezione illustra l'uso di un reader e un writer SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d007e-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d007e-287">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="d007e-287">Frequently asked questions</span></span>
<span data-ttu-id="d007e-288">**D:** Ho più file generati dalle pipeline di Big Data.</span><span class="sxs-lookup"><span data-stu-id="d007e-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="d007e-289">Posso usare l'attività AzureMLBatchExecution per lavorare con tali file?</span><span class="sxs-lookup"><span data-stu-id="d007e-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="d007e-290">**R:** Sì.</span><span class="sxs-lookup"><span data-stu-id="d007e-290">**A:** Yes.</span></span> <span data-ttu-id="d007e-291">Per informazioni dettagliate, vedere la sezione **Uso di un modulo Reader per leggere dati da più file del BLOB di Azure** .</span><span class="sxs-lookup"><span data-stu-id="d007e-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="d007e-292">Attività di assegnazione dei punteggi di batch di Azure ML</span><span class="sxs-lookup"><span data-stu-id="d007e-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="d007e-293">Se si sta usando l'attività **AzureMLBatchScoring** per l'integrazione con Azure Machine Learning, si consiglia di passare alla più recente attività **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="d007e-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="d007e-294">L'attività AzureMLBatchExecution è stata introdotta nella versione di Azure SDK e Azure PowerShell di agosto 2015.</span><span class="sxs-lookup"><span data-stu-id="d007e-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="d007e-295">Se si vuole continuare a usare l'attività AzureMLBatchScoring, continuare a leggere questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d007e-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="d007e-296">Attività di assegnazione dei punteggi di batch di Azure ML che usa Archiviazione di Azure per l'input/output</span><span class="sxs-lookup"><span data-stu-id="d007e-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="d007e-297">Parametri del servizio Web</span><span class="sxs-lookup"><span data-stu-id="d007e-297">Web Service Parameters</span></span>
<span data-ttu-id="d007e-298">Per specificare i valori per i parametri del servizio Web, aggiungere una sezione **typeProperties** alla sezione **AzureMLBatchScoringActivity** nel file JSON della pipeline, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d007e-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="d007e-299">È anche possibile usare le [funzioni di Data factory](data-factory-functions-variables.md) per passare i valori per i parametri del servizio Web, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d007e-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="d007e-300">I parametri del servizio Web applicano la distinzione tra maiuscole e minuscole. È quindi necessario assicurarsi che i nomi specificati nel file JSON dell'attività corrispondano ai nomi esposti dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d007e-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="d007e-301">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d007e-301">See Also</span></span>
* [<span data-ttu-id="d007e-302">Post di blog di Azure: Guida introduttiva a Data Factory di Azure e ad Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d007e-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
