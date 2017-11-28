---
title: pipeline di dati predittivi aaaCreate utilizzando Data Factory di Azure | Documenti Microsoft
description: Viene descritto come toocreate creare pipeline predittive con Data Factory di Azure e Azure Machine Learning
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
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="c43a7-103">Creare pipeline predittive tramite Azure Machine Learning e Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c43a7-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="c43a7-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="c43a7-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="c43a7-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="c43a7-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="c43a7-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="c43a7-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="c43a7-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="c43a7-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="c43a7-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="c43a7-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="c43a7-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c43a7-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="c43a7-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c43a7-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="c43a7-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="c43a7-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="c43a7-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c43a7-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="c43a7-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="c43a7-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="c43a7-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="c43a7-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="c43a7-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c43a7-115">Azure Machine Learning</span></span>
<span data-ttu-id="c43a7-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) Abilita è toobuild, testare e distribuire soluzioni analitica predittiva.</span><span class="sxs-lookup"><span data-stu-id="c43a7-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="c43a7-117">Da un punto di vista generale, questo avviene in tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="c43a7-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="c43a7-118">**Creare un esperimento di training**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-118">**Create a training experiment**.</span></span> <span data-ttu-id="c43a7-119">Eseguire questo passaggio utilizzando hello Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="c43a7-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="c43a7-120">Machine Learning studio di Hello è un ambiente di sviluppo visivo collaborativo utilizzare tootrain e testare un modello predittivo analitica utilizzando i dati di training.</span><span class="sxs-lookup"><span data-stu-id="c43a7-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="c43a7-121">**Convertirlo esperimento predittiva tooa**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="c43a7-122">Una volta il modello è stato eseguito con i dati esistenti e si è pronti toouse è tooscore nuovi dati, la preparazione e semplificare l'esperimento di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="c43a7-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="c43a7-123">**Distribuirlo come servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="c43a7-124">È possibile pubblicare l'esperimento di assegnazione dei punteggi come servizio Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c43a7-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="c43a7-125">È possibile modello di dati tooyour tramite questo punto finale del servizio web di inviare e ricevere le stime di risultato da modello hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="c43a7-126">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="c43a7-126">Azure Data Factory</span></span>
<span data-ttu-id="c43a7-127">Data Factory è un servizio di integrazione di dati basato su cloud che Orchestra e automatizza hello **spostamento** e **trasformazione** dei dati.</span><span class="sxs-lookup"><span data-stu-id="c43a7-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="c43a7-128">È possibile creare soluzioni di integrazione dati utilizzando Data Factory di Azure che possono inserire dati da diversi archivi dati, dati hello/processo di trasformazione e pubblicare archivi dati toohello di hello risultato dati.</span><span class="sxs-lookup"><span data-stu-id="c43a7-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="c43a7-129">Servizio Data Factory consente una pipeline di dati toocreate spostano e trasformare i dati e quindi eseguirla le pipeline hello in una pianificazione specifica (oraria, giornaliera, settimanale e così via).</span><span class="sxs-lookup"><span data-stu-id="c43a7-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="c43a7-130">Offre inoltre le dipendenze tra le pipeline di dati e la derivazione di visualizzazioni dettagliate toodisplay hello e monitorare tutte le pipeline di dati da un problemi di individuare tooeasily singola vista unificata e gli avvisi di monitoraggio del programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="c43a7-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="c43a7-131">Vedere [tooAzure introduzione Data Factory](data-factory-introduction.md) e [compilare le pipeline prima](data-factory-build-your-first-pipeline.md) tooquickly articoli introduzione hello servizio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c43a7-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="c43a7-132">Data Factory e Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c43a7-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="c43a7-133">Azure consente di Data Factory è tooeasily creare pipeline che utilizzano un report pubblicato [Azure Machine Learning] [ azure-machine-learning] web service per analitica predittiva.</span><span class="sxs-lookup"><span data-stu-id="c43a7-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="c43a7-134">Utilizzo di hello **attività di esecuzione Batch** in una pipeline di Data Factory di Azure, è possibile richiamare un toomake stime di Azure ML web service sui dati hello in batch.</span><span class="sxs-lookup"><span data-stu-id="c43a7-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="c43a7-135">Vedere [richiamando un Azure ML servizio web utilizzando hello attività di esecuzione Batch](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="c43a7-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="c43a7-136">Nel corso del tempo, i modelli di previsione hello negli esperimenti di assegnazione dei punteggi di hello Azure ML devono toobe ripetere il training con nuovi set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="c43a7-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="c43a7-137">È possibile ripetere il training un modello da una pipeline di Data Factory di Azure ML effettuando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c43a7-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="c43a7-138">Pubblicare l'esperimento di training hello (non predittiva esperimento) come un servizio web.</span><span class="sxs-lookup"><span data-stu-id="c43a7-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="c43a7-139">Eseguire questo passaggio in Azure Machine Learning Studio hello come esperimento predittiva tooexpose come un servizio web nello scenario precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="c43a7-140">Usa servizio web per esperimento di training hello hello attività di esecuzione Batch di Azure ML tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="c43a7-141">In pratica, è possibile utilizzare hello esecuzione Batch di Azure ML attività tooinvoke training servizio web e il servizio web di punteggio.</span><span class="sxs-lookup"><span data-stu-id="c43a7-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="c43a7-142">Dopo avere completato con ripetizione di training, aggiornare il punteggio di servizio web (esperimento predittiva esposta come servizio web) con il modello appena eseguito il training di hello utilizzando hello hello **attività risorse di Azure ML aggiornare**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="c43a7-143">Per informazioni dettagliate, vedere l'articolo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Aggiornamento dei modelli con Attività della risorsa di aggiornamento).</span><span class="sxs-lookup"><span data-stu-id="c43a7-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="c43a7-144">Richiamo di un servizio Web tramite Attività di esecuzione batch</span><span class="sxs-lookup"><span data-stu-id="c43a7-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="c43a7-145">Utilizzare l'elaborazione e lo spostamento dei dati di Azure Data Factory tooorchestrate e quindi eseguire esecuzione batch utilizzando Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c43a7-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="c43a7-146">Ecco i passaggi di livello superiore di hello:</span><span class="sxs-lookup"><span data-stu-id="c43a7-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="c43a7-147">Creare un servizio collegato di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c43a7-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="c43a7-148">È necessario hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="c43a7-148">You need hello following values:</span></span>

   1. <span data-ttu-id="c43a7-149">**URI della richiesta** per hello API esecuzione Batch.</span><span class="sxs-lookup"><span data-stu-id="c43a7-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="c43a7-150">È possibile trovare l'URI della richiesta di hello facendo hello **esecuzione BATCH** collegamento nella pagina servizi web di hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="c43a7-151">**Chiave API** per hello pubblicato il servizio web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c43a7-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="c43a7-152">È possibile trovare la chiave API hello facendo clic sul servizio web hello che è stata pubblicata.</span><span class="sxs-lookup"><span data-stu-id="c43a7-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="c43a7-153">Hello utilizzare **AzureMLBatchExecution** attività.</span><span class="sxs-lookup"><span data-stu-id="c43a7-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Dashboard di Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Batch URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="c43a7-156">Scenario: Esperimenti con Web servizio degli input/output che fanno riferimento toodata nell'archiviazione Blob di Azure</span><span class="sxs-lookup"><span data-stu-id="c43a7-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="c43a7-157">In questo scenario, hello servizio Web di Azure Machine Learning esegue le stime utilizzando i dati da un file in una risorsa di archiviazione blob di Azure e archivia i risultati della stima hello nell'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="c43a7-158">Hello JSON seguente definisce una pipeline di Data Factory con un'attività AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="c43a7-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="c43a7-159">attività Hello dispone di set di dati hello **DecisionTreeInputBlob** come input e **DecisionTreeResultBlob** come output di hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="c43a7-160">Hello **DecisionTreeInputBlob** viene passato come un servizio web di input toohello da utilizzando hello **WebServiceInputActivity** proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="c43a7-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="c43a7-161">Hello **DecisionTreeResultBlob** viene passato come un servizio Web toohello di output da utilizzando hello **webserviceoutputs della** proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="c43a7-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c43a7-162">Se il servizio web hello accetta più input, utilizzare hello **webServiceInputs** proprietà anziché **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="c43a7-163">Vedere hello [servizio Web richiede più input](#web-service-requires-multiple-inputs) sezione per un esempio di utilizzo di proprietà webServiceInputs hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="c43a7-164">Set di dati che fanno riferimento hello **webServiceInput**/**webServiceInputs** e **webserviceoutputs della** proprietà (in  **typeProperties**) deve essere incluso anche in attività hello **input** e **restituisce**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="c43a7-165">Nell'esperimento di Machine Learning di Azure,le porte e i parametri globali di input e output del servizio Web hanno nomi predefiniti ("input1", "input2") che è possibile personalizzare.</span><span class="sxs-lookup"><span data-stu-id="c43a7-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="c43a7-166">nomi di Hello che è usare per webServiceInputs e webserviceoutputs della globalparameters della impostazioni devono corrispondere esattamente nomi hello negli esperimenti hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="c43a7-167">È possibile visualizzare i payload di richiesta di esempio hello nella hello Help esecuzione Batch per il mapping di Azure ML endpoint tooverify hello previsto.</span><span class="sxs-lookup"><span data-stu-id="c43a7-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
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
> <span data-ttu-id="c43a7-168">Solo input e output dell'attività AzureMLBatchExecution hello possono essere passati come parametri toohello servizio Web.</span><span class="sxs-lookup"><span data-stu-id="c43a7-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="c43a7-169">Ad esempio, in hello sopra frammento di codice JSON, DecisionTreeInputBlob è un input toohello AzureMLBatchExecution attività, che viene passato come un input toohello servizio Web tramite un parametro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="c43a7-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="c43a7-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="c43a7-170">Example</span></span>
<span data-ttu-id="c43a7-171">Toohold di archiviazione di Azure viene utilizzato questo esempio sia hello dati di input e outpui.</span><span class="sxs-lookup"><span data-stu-id="c43a7-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="c43a7-172">È consigliabile eseguire hello [compilare le pipeline prima con Data Factory] [ adf-build-1st-pipeline] esercitazione prima di passare attraverso questo esempio.</span><span class="sxs-lookup"><span data-stu-id="c43a7-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="c43a7-173">In questo esempio, utilizzare hello Editor delle Data Factory toocreate gli elementi Data Factory (servizi collegati, i set di dati, pipeline).</span><span class="sxs-lookup"><span data-stu-id="c43a7-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="c43a7-174">Creare un **servizio collegato** per **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="c43a7-175">Se hello i file di input e outpui sono in diversi account di archiviazione, è necessario due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="c43a7-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="c43a7-176">Di seguito è fornito un esempio JSON:</span><span class="sxs-lookup"><span data-stu-id="c43a7-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="c43a7-177">Creare hello **input** Data Factory di Azure **dataset**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="c43a7-178">A differenza di altri set di dati di Data Factory, questi devono includere entrambi i valori **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="c43a7-179">È possibile utilizzare toocause partizionamento ogni tooprocess (ogni sezione di dati) di esecuzione batch o produrre input univoco e i file di output.</span><span class="sxs-lookup"><span data-stu-id="c43a7-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="c43a7-180">Potrebbe essere necessario tooinclude alcuni hello tootransform attività upstream di input in formato CSV hello e inserirlo nell'account di archiviazione hello per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="c43a7-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="c43a7-181">In tal caso, è necessario includere non hello **esterno** e **externalData** impostazioni mostrate nell'hello seguente esempio, il DecisionTreeInputBlob sarebbe e il set di dati di hello output di un'attività diversa.</span><span class="sxs-lookup"><span data-stu-id="c43a7-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="c43a7-182">Il file di input csv deve includere una riga dell'intestazione di colonna hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="c43a7-183">Se si utilizza hello **attività di copia** toocreate o spostare hello csv nell'archiviazione blob di hello, è necessario impostare proprietà di sink hello **blobWriterAddHeader** troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="c43a7-184">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c43a7-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="c43a7-185">Se il file csv hello non dispone di intestazione hello, si può vedere hello il seguente errore: **errore nell'attività: errore durante la lettura di stringa. Token imprevisto: StartObject. Percorso '', riga 1, posizione 1**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="c43a7-186">Creare hello **output** Data Factory di Azure **dataset**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="c43a7-187">L'esempio Usa partizionamento toocreate un percorso di output univoca per ogni esecuzione della sezione.</span><span class="sxs-lookup"><span data-stu-id="c43a7-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="c43a7-188">Senza il partizionamento hello, attività hello sovrascriverebbe il file hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

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
4. <span data-ttu-id="c43a7-189">Creare un **servizio collegato** di tipo: **nell'oggetto AzureMLLinkedService**, fornendo la chiave API hello e modello di URL di esecuzione batch.</span><span class="sxs-lookup"><span data-stu-id="c43a7-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="c43a7-190">Creare infine una pipeline contenente un'attività **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="c43a7-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="c43a7-191">In fase di esecuzione della pipeline esegue hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c43a7-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="c43a7-192">Ottiene il percorso di hello hello del file di input da input set di dati.</span><span class="sxs-lookup"><span data-stu-id="c43a7-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="c43a7-193">Richiama l'esecuzione di batch di Azure Machine Learning hello API</span><span class="sxs-lookup"><span data-stu-id="c43a7-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="c43a7-194">Copie hello blob toohello output esecuzione di batch specificato con il set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="c43a7-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c43a7-195">L'attività AzureMLBatchExecution può avere zero o più input e uno o più output.</span><span class="sxs-lookup"><span data-stu-id="c43a7-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="c43a7-196">Per la data e l'ora di **inizio** e di **fine** è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c43a7-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c43a7-197">ad esempio 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c43a7-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="c43a7-198">Hello **fine** ora è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c43a7-198">hello **end** time is optional.</span></span> <span data-ttu-id="c43a7-199">Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore.**"</span><span class="sxs-lookup"><span data-stu-id="c43a7-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="c43a7-200">specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.</span><span class="sxs-lookup"><span data-stu-id="c43a7-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="c43a7-201">Per informazioni dettagliate sulle proprietà JSON, vedere [Informazioni di riferimento sugli script JSON di Data Factory](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c43a7-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c43a7-202">Input per l'attività AzureMLBatchExecution hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c43a7-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="c43a7-203">Scenario: Esperimenti con i moduli di lettura/scrittura toorefer toodata in vari archivi</span><span class="sxs-lookup"><span data-stu-id="c43a7-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="c43a7-204">Un altro scenario comune quando si creano gli esperimenti di Azure ML è toouse moduli di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="c43a7-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="c43a7-205">modulo del lettore Hello è tooload utilizzati dati in un esperimento e modulo di scrittura hello è toosave dati dei propri esperimenti.</span><span class="sxs-lookup"><span data-stu-id="c43a7-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="c43a7-206">Per informazioni dettagliate sui moduli Reader e Writer, vedere gli argomenti [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) in MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="c43a7-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="c43a7-207">Quando si utilizzano moduli di lettura e scrittura hello, è buona norma toouse un parametro del servizio Web per ogni proprietà di questi moduli di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="c43a7-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="c43a7-208">Questi parametri web consentono i valori hello tooconfigure durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="c43a7-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="c43a7-209">Ad esempio, è possibile creare un esperimento con un modulo Reader che usa un database SQL di Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c43a7-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="c43a7-210">Dopo la distribuzione di servizio web hello, si desidera consumer hello tooenable di hello web servizio toospecify YYY.database.windows.net chiamato un altro Server di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c43a7-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="c43a7-211">È possibile utilizzare un tooallow di parametro del servizio Web toobe questo valore configurato.</span><span class="sxs-lookup"><span data-stu-id="c43a7-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="c43a7-212">L'input e l'output del servizio Web sono diversi dai parametri del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="c43a7-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="c43a7-213">Nel primo scenario hello, è stato illustrato come un input e output può essere specificati per un servizio Web di Azure ML.</span><span class="sxs-lookup"><span data-stu-id="c43a7-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="c43a7-214">In questo scenario, passare i parametri per un servizio Web corrispondenti tooproperties dei moduli di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="c43a7-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="c43a7-215">Viene preso in esame uno scenario relativo all'uso dei parametri del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="c43a7-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="c43a7-216">Si dispone di un servizio web Azure Machine Learning distribuito che usa un dati tooread modulo del lettore da una delle origini dati hello è supportate da Azure Machine Learning (ad esempio: Database SQL di Azure).</span><span class="sxs-lookup"><span data-stu-id="c43a7-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="c43a7-217">Una volta eseguita, l'esecuzione batch hello risultati hello vengono scritti utilizzando un modulo di scrittura (Database SQL di Azure).</span><span class="sxs-lookup"><span data-stu-id="c43a7-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="c43a7-218">Nessun input del servizio web e output vengono definiti negli esperimenti hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="c43a7-219">In questo caso, si consiglia di configurare i parametri del servizio web rilevanti per i moduli di lettura e scrittura hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="c43a7-220">Questa configurazione consente ai moduli toobe configurato quando si utilizza l'attività AzureMLBatchExecution hello hello lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="c43a7-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="c43a7-221">Specificare i parametri di servizio Web in hello **globalparameters della** sezione in formato JSON dell'attività hello come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c43a7-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="c43a7-222">È inoltre possibile utilizzare [funzioni di Data Factory](data-factory-functions-variables.md) per passare i valori per hello parametri del servizio Web come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c43a7-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="c43a7-223">parametri del servizio Web Hello tra maiuscole e minuscole, verificare che i nomi di hello specificati nell'attività hello JSON corrispondano hello quelli esposti dal servizio Web hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="c43a7-224">Utilizzo di un dati tooread modulo del lettore da più file in Blob di Azure</span><span class="sxs-lookup"><span data-stu-id="c43a7-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="c43a7-225">Le pipeline di Big Data, con attività come Pig e Hive, possono generare uno o più file di output senza estensioni.</span><span class="sxs-lookup"><span data-stu-id="c43a7-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="c43a7-226">Ad esempio, quando si specifica una tabella Hive esterna, hello dati per una tabella Hive esterna hello possono essere archiviati nell'archiviazione blob di Azure con hello seguente nome 000000_0.</span><span class="sxs-lookup"><span data-stu-id="c43a7-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="c43a7-227">È possibile utilizzare più file di modulo del lettore hello in un esperimento di tooread e utilizzarli per le stime.</span><span class="sxs-lookup"><span data-stu-id="c43a7-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="c43a7-228">Quando si Usa modulo del lettore hello in un esperimento di Azure Machine Learning, è possibile specificare i Blob di Azure come input.</span><span class="sxs-lookup"><span data-stu-id="c43a7-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="c43a7-229">file Hello hello archiviazione blob di Azure possono essere file di output di hello (esempio: 000000_0) che vengono generati da uno script Pig e Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c43a7-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="c43a7-230">Hello modulo del lettore consente tooread file (con nessuna estensione) configurando hello **toocontainer percorso, directory/blob**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="c43a7-231">Hello **percorso toocontainer** punti toohello contenitore e **directory/blob** punta toofolder che contiene i file hello, come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="c43a7-232">Hello asterisco, ovvero \*) **specifica che tutti i file nella cartella/contenitore hello di hello (vale a dire dati/aggregateddata/anno = mese/2014-6 /\*)** vengono lette come parte dell'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Proprietà del Blob Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="c43a7-234">Esempio</span><span class="sxs-lookup"><span data-stu-id="c43a7-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="c43a7-235">Pipeline con l'attività AzureMLBatchExecution con parametri del servizio Web</span><span class="sxs-lookup"><span data-stu-id="c43a7-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="c43a7-236">In hello esempio JSON precedente:</span><span class="sxs-lookup"><span data-stu-id="c43a7-236">In hello above JSON example:</span></span>

* <span data-ttu-id="c43a7-237">Hello distribuito Azure Machine Learning Web servizio utilizza un lettore e un writer modulo tooread/scrittura di dati da / tooan Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="c43a7-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="c43a7-238">Questo servizio Web espone hello seguenti quattro parametri: nome del server, nome del Database, nome Server dell'account utente e password dell'account utente Server di Database.</span><span class="sxs-lookup"><span data-stu-id="c43a7-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="c43a7-239">Per la data e l'ora di **inizio** e di **fine** è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c43a7-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c43a7-240">ad esempio 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c43a7-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="c43a7-241">Hello **fine** ora è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c43a7-241">hello **end** time is optional.</span></span> <span data-ttu-id="c43a7-242">Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore.**"</span><span class="sxs-lookup"><span data-stu-id="c43a7-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="c43a7-243">specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.</span><span class="sxs-lookup"><span data-stu-id="c43a7-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="c43a7-244">Per informazioni dettagliate sulle proprietà JSON, vedere [Informazioni di riferimento sugli script JSON di Data Factory](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c43a7-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="c43a7-245">Altri scenari</span><span class="sxs-lookup"><span data-stu-id="c43a7-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="c43a7-246">Il servizio Web richiede più input</span><span class="sxs-lookup"><span data-stu-id="c43a7-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="c43a7-247">Se il servizio web hello accetta più input, utilizzare hello **webServiceInputs** proprietà anziché **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="c43a7-248">Set di dati che fanno riferimento hello **webServiceInputs** deve essere incluso anche in attività hello **input**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="c43a7-249">Nell'esperimento di Machine Learning di Azure,le porte e i parametri globali di input e output del servizio Web hanno nomi predefiniti ("input1", "input2") che è possibile personalizzare.</span><span class="sxs-lookup"><span data-stu-id="c43a7-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="c43a7-250">nomi di Hello che è usare per webServiceInputs e webserviceoutputs della globalparameters della impostazioni devono corrispondere esattamente nomi hello negli esperimenti hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="c43a7-251">È possibile visualizzare i payload di richiesta di esempio hello nella hello Help esecuzione Batch per il mapping di Azure ML endpoint tooverify hello previsto.</span><span class="sxs-lookup"><span data-stu-id="c43a7-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="c43a7-252">Servizio Web non richiede un input</span><span class="sxs-lookup"><span data-stu-id="c43a7-252">Web Service does not require an input</span></span>
<span data-ttu-id="c43a7-253">Servizi web di esecuzione batch di Azure ML può essere utilizzato toorun flussi di lavoro, ad esempio R o script Python, che non richieda alcun input.</span><span class="sxs-lookup"><span data-stu-id="c43a7-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="c43a7-254">In alternativa, esperimento hello può essere configurato con un modulo del lettore che espongono qualsiasi globalparameters della.</span><span class="sxs-lookup"><span data-stu-id="c43a7-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="c43a7-255">In tal caso, hello AzureMLBatchExecution attività sarà configurata come segue:</span><span class="sxs-lookup"><span data-stu-id="c43a7-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="c43a7-256">Servizio Web non richiede un input/output</span><span class="sxs-lookup"><span data-stu-id="c43a7-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="c43a7-257">servizio web di esecuzione batch di Azure ML Hello potrebbe non avere alcun output di servizio Web configurato.</span><span class="sxs-lookup"><span data-stu-id="c43a7-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="c43a7-258">In questo esempio non sono disponibili input o output del servizio Web, né alcuna proprietà GlobalParameters configurata.</span><span class="sxs-lookup"><span data-stu-id="c43a7-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="c43a7-259">È ancora un output configurato nella attività hello stessa, ma non viene fornito come un webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="c43a7-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="c43a7-260">Web Service utilizza lettori e writer e attività di hello viene eseguito solo dopo che altre attività hanno avuto esito positivo</span><span class="sxs-lookup"><span data-stu-id="c43a7-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="c43a7-261">Hello Azure ML web reader e writer moduli del servizio potrebbero essere configurato toorun con o senza alcun globalparameters della.</span><span class="sxs-lookup"><span data-stu-id="c43a7-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="c43a7-262">Tuttavia, è consigliabile tooembed servizio viene chiamata in una pipeline che utilizza il servizio hello tooinvoke dipendenze di set di dati solo se alcune operazioni di elaborazione a monte è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c43a7-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="c43a7-263">È inoltre possibile attivare un'altra azione dopo il completamento dell'esecuzione di batch hello utilizzando questo approccio.</span><span class="sxs-lookup"><span data-stu-id="c43a7-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="c43a7-264">In tal caso, è possibile esprimere le dipendenze di hello mediante attività input e output, senza il nome di uno di essi come servizio Web input o output.</span><span class="sxs-lookup"><span data-stu-id="c43a7-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="c43a7-265">Hello **informazioni chiave** sono:</span><span class="sxs-lookup"><span data-stu-id="c43a7-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="c43a7-266">Se l'endpoint esperimento utilizza un WebServiceInputActivity: è rappresentato da un set di dati blob ed è incluso in input dell'attività hello e proprietà WebServiceInputActivity hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="c43a7-267">In caso contrario, proprietà WebServiceInputActivity hello viene omesso.</span><span class="sxs-lookup"><span data-stu-id="c43a7-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="c43a7-268">Se l'endpoint esperimento utilizza webServiceOutput(s): essi sono rappresentate dal set di dati blob e sono inclusi negli output di hello attività e nella proprietà webserviceoutputs della hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="c43a7-269">output attività Hello e webserviceoutputs della viene eseguito il mapping dal nome hello di ogni output nell'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="c43a7-270">In caso contrario, proprietà webserviceoutputs della hello viene omesso.</span><span class="sxs-lookup"><span data-stu-id="c43a7-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="c43a7-271">Se l'endpoint esperimento espone globalParameter(s), essi vengono fornite nella proprietà globalparameters della attività di hello come coppie di chiavi, valore.</span><span class="sxs-lookup"><span data-stu-id="c43a7-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="c43a7-272">In caso contrario, proprietà globalparameters della hello viene omesso.</span><span class="sxs-lookup"><span data-stu-id="c43a7-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="c43a7-273">le chiavi di Hello maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c43a7-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="c43a7-274">[Funzioni di Azure Data Factory](data-factory-functions-variables.md) può essere utilizzata nei valori hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="c43a7-275">Set di dati aggiuntivi possono essere incluse nelle proprietà di input e output di attività hello, senza hello attività typeProperties cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="c43a7-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="c43a7-276">Questi set di dati determinano l'esecuzione di dipendenze di sezione ma in caso contrario vengono ignorate dal hello AzureMLBatchExecution attività.</span><span class="sxs-lookup"><span data-stu-id="c43a7-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="c43a7-277">Aggiornamento dei modelli con Attività della risorsa di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="c43a7-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="c43a7-278">Dopo avere completato con ripetizione di training, aggiornare il punteggio di servizio web (esperimento predittiva esposta come servizio web) con il modello appena eseguito il training di hello utilizzando hello hello **attività risorse di Azure ML aggiornare**.</span><span class="sxs-lookup"><span data-stu-id="c43a7-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="c43a7-279">Per informazioni dettagliate, vedere l'articolo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Aggiornamento dei modelli con Attività della risorsa di aggiornamento).</span><span class="sxs-lookup"><span data-stu-id="c43a7-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="c43a7-280">Moduli Reader e Writer </span><span class="sxs-lookup"><span data-stu-id="c43a7-280">Reader and Writer Modules</span></span>
<span data-ttu-id="c43a7-281">Uno scenario comune per l'utilizzo di parametri del servizio Web è utilizzare hello di Azure SQL reader e writer.</span><span class="sxs-lookup"><span data-stu-id="c43a7-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="c43a7-282">modulo del lettore Hello è tooload utilizzati dati in un esperimento dai servizi di gestione dati all'esterno di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c43a7-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="c43a7-283">modulo di scrittura Hello è toosave dati dei propri esperimenti in servizi di gestione dati all'esterno di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c43a7-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="c43a7-284">Per informazioni dettagliate sui BLOB di Azure o sui moduli Reader e Writer SQL di Azure, vedere gli argomenti [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) in MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="c43a7-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="c43a7-285">esempio Hello nella sezione precedente hello utilizzato lettura Blob di Azure hello e agente di scrittura Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="c43a7-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="c43a7-286">Questa sezione illustra l'uso di un reader e un writer SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="c43a7-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="c43a7-287">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="c43a7-287">Frequently asked questions</span></span>
<span data-ttu-id="c43a7-288">**D:** Ho più file generati dalle pipeline di Big Data.</span><span class="sxs-lookup"><span data-stu-id="c43a7-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="c43a7-289">È possibile utilizzare toowork AzureMLBatchExecution attività hello in tutti i file hello?</span><span class="sxs-lookup"><span data-stu-id="c43a7-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="c43a7-290">**R:** Sì.</span><span class="sxs-lookup"><span data-stu-id="c43a7-290">**A:** Yes.</span></span> <span data-ttu-id="c43a7-291">Vedere hello **utilizzando un dati tooread modulo del lettore da più file in Blob di Azure** sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="c43a7-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="c43a7-292">Attività di assegnazione dei punteggi di batch di Azure ML</span><span class="sxs-lookup"><span data-stu-id="c43a7-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="c43a7-293">Se si utilizza hello **AzureMLBatchScoring** toointegrate di attività con Azure Machine Learning, è consigliabile utilizzare più recente hello **AzureMLBatchExecution** attività.</span><span class="sxs-lookup"><span data-stu-id="c43a7-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="c43a7-294">Hello AzureMLBatchExecution attività è stata introdotta nella versione di agosto 2015 di Azure SDK e di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="c43a7-295">Se si desidera toocontinue utilizzando attività AzureMLBatchScoring hello, continuare a leggere questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c43a7-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="c43a7-296">Attività di assegnazione dei punteggi di batch di Azure ML che usa Archiviazione di Azure per l'input/output</span><span class="sxs-lookup"><span data-stu-id="c43a7-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="c43a7-297">Parametri del servizio Web</span><span class="sxs-lookup"><span data-stu-id="c43a7-297">Web Service Parameters</span></span>
<span data-ttu-id="c43a7-298">toospecify valori per parametri del servizio Web, aggiungere un **typeProperties** sezione toohello **AzureMLBatchScoringActivty** sezione nella pipeline hello JSON, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c43a7-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="c43a7-299">È inoltre possibile utilizzare [funzioni di Data Factory](data-factory-functions-variables.md) per passare i valori per hello parametri del servizio Web come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c43a7-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="c43a7-300">parametri del servizio Web Hello tra maiuscole e minuscole, verificare che i nomi di hello specificati nell'attività hello JSON corrispondano hello quelli esposti dal servizio Web hello.</span><span class="sxs-lookup"><span data-stu-id="c43a7-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="c43a7-301">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c43a7-301">See Also</span></span>
* [<span data-ttu-id="c43a7-302">Post di blog di Azure: Guida introduttiva a Data Factory di Azure e ad Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c43a7-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
