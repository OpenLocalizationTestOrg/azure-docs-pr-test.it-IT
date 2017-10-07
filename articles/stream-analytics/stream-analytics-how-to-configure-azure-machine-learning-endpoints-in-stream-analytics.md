---
title: gli endpoint di Azure Machine Learning aaaUse nel flusso Analitica | Documenti Microsoft
description: Funzioni definite dall'utente di Machine Learning in Analisi di flusso
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="3da5e-103">Integrazione di Machine Learning in Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="3da5e-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="3da5e-104">Flusso Analitica supporta funzioni definite dall'utente che richiamano gli endpoint di Machine Learning tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3da5e-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="3da5e-105">Supporto delle API REST per questa funzionalità è descritta in dettaglio in hello [libreria dell'API REST di flusso Analitica](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="3da5e-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="3da5e-106">Questo articolo fornisce le informazioni supplementari necessarie per la corretta implementazione di questa funzionalità in Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="3da5e-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="3da5e-107">È stata pubblicata anche un'esercitazione che è disponibile [qui](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3da5e-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="3da5e-108">Panoramica: Terminologia di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3da5e-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="3da5e-109">Microsoft Azure Machine Learning fornisce uno strumento di collaborazione, trascinamento e rilascio, è possibile utilizzare toobuild, testare e distribuire soluzioni analitica predittiva sui dati.</span><span class="sxs-lookup"><span data-stu-id="3da5e-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="3da5e-110">Questo strumento viene chiamato hello *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="3da5e-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="3da5e-111">studio Hello è toointeract utilizzati con hello risorse Machine Learning e compilare con facilità, test e alla progettazione di eseguire l'iterazione.</span><span class="sxs-lookup"><span data-stu-id="3da5e-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="3da5e-112">Di seguito sono riportate le risorse e le rispettive definizioni.</span><span class="sxs-lookup"><span data-stu-id="3da5e-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="3da5e-113">**Area di lavoro**: hello *dell'area di lavoro* è un contenitore che include tutte le altre risorse Machine Learning in un contenitore per la gestione e controllo.</span><span class="sxs-lookup"><span data-stu-id="3da5e-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="3da5e-114">**Sperimentazione**: *esperimenti* vengono create dal DataSet tooutilize gli esperti di dati e di eseguire il training di un modello di machine learning.</span><span class="sxs-lookup"><span data-stu-id="3da5e-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="3da5e-115">**Endpoint**: *endpoint* sono hello Azure Machine Learning caratteristiche tootake dell'oggetto utilizzato come input, applicare un modello di apprendimento automatico specificato e restituire l'output con punteggio.</span><span class="sxs-lookup"><span data-stu-id="3da5e-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="3da5e-116">**Servizio Web di assegnazione dei punteggi**: un *servizio Web di assegnazione dei punteggi* è una raccolta di endpoint, come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="3da5e-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="3da5e-117">Ogni endpoint ha API per l'esecuzione batch e per l'esecuzione sincrona.</span><span class="sxs-lookup"><span data-stu-id="3da5e-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="3da5e-118">Analisi di flusso usa l'esecuzione sincrona.</span><span class="sxs-lookup"><span data-stu-id="3da5e-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="3da5e-119">nome del servizio specifico Hello è un [servizio richiesta/risposta](../machine-learning/machine-learning-consume-web-services.md) in Azure ml studio.</span><span class="sxs-lookup"><span data-stu-id="3da5e-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="3da5e-120">Risorse di Machine Learning necessarie per i processi di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="3da5e-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="3da5e-121">Ai fini di hello di Analitica di flusso del processo di elaborazione, un endpoint di tipo richiesta/risposta, un [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), e una definizione swagger tutti necessari per la corretta esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3da5e-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="3da5e-122">Flusso Analitica dispone di un endpoint aggiuntivo che costruisce l'url dell'endpoint swagger hello, Cerca l'interfaccia hello e restituisce un utente di toohello definizione di funzione definita dall'utente predefinito.</span><span class="sxs-lookup"><span data-stu-id="3da5e-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="3da5e-123">Configurare una funzione definita dall'utente di Analisi di flusso e di Machine Learning con l'API REST</span><span class="sxs-lookup"><span data-stu-id="3da5e-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="3da5e-124">Mediante le API REST è possibile configurare le funzioni di linguaggio macchina Azure toocall di processo.</span><span class="sxs-lookup"><span data-stu-id="3da5e-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="3da5e-125">come indicato di seguito sono riportati i passaggi di Hello:</span><span class="sxs-lookup"><span data-stu-id="3da5e-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="3da5e-126">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="3da5e-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="3da5e-127">Definire un input</span><span class="sxs-lookup"><span data-stu-id="3da5e-127">Define an input</span></span>
3. <span data-ttu-id="3da5e-128">Definire un output</span><span class="sxs-lookup"><span data-stu-id="3da5e-128">Define an output</span></span>
4. <span data-ttu-id="3da5e-129">Creare una funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="3da5e-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="3da5e-130">Scrivere una trasformazione di flusso Analitica che chiama hello funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="3da5e-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="3da5e-131">Avviare il processo di hello</span><span class="sxs-lookup"><span data-stu-id="3da5e-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="3da5e-132">Creazione di una funzione definita dall'utente con proprietà di base</span><span class="sxs-lookup"><span data-stu-id="3da5e-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="3da5e-133">Ad esempio, hello codice di esempio seguente viene creata una funzione scalare definita dall'utente denominato *newudf* che associa l'endpoint di Azure Machine Learning tooan.</span><span class="sxs-lookup"><span data-stu-id="3da5e-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="3da5e-134">Si noti che hello *endpoint* (URI del servizio) sono disponibili nella pagina della Guida hello API per hello scelto servizio e hello *apiKey* sono reperibili nella pagina principale di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="3da5e-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="3da5e-135">Corpo della richiesta di esempio:</span><span class="sxs-lookup"><span data-stu-id="3da5e-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="3da5e-136">Chiamare l'endpoint RetrieveDefaultDefinition per la funzione definita dall'utente predefinita</span><span class="sxs-lookup"><span data-stu-id="3da5e-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="3da5e-137">Una volta hello scheletro che funzione definita dall'utente viene creata una definizione completa di hello di hello che funzione definita dall'utente è necessaria.</span><span class="sxs-lookup"><span data-stu-id="3da5e-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="3da5e-138">endpoint RetreiveDefaultDefinition Hello consente di ottenere definizione default hello per una funzione scalare che è l'endpoint di Azure Machine Learning tooan associato.</span><span class="sxs-lookup"><span data-stu-id="3da5e-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="3da5e-139">payload Hello seguente richiede definizione di funzione definita dall'utente tooget hello default per una funzione scalare che è l'endpoint di Azure Machine Learning tooan associato.</span><span class="sxs-lookup"><span data-stu-id="3da5e-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="3da5e-140">Non consente di specificare endpoint effettivo hello perché è già stato specificato durante la richiesta PUT.</span><span class="sxs-lookup"><span data-stu-id="3da5e-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="3da5e-141">Flusso Analitica chiama endpoint hello fornito nella richiesta di hello se viene fornito in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="3da5e-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="3da5e-142">In caso contrario, viene utilizzato hello uno stato a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="3da5e-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="3da5e-143">Di seguito hello accetta definita un'unica stringa parametro (una frase) e restituisce un singolo output di tipo stringa che indica l'etichetta "sentiment" hello per la frase.</span><span class="sxs-lookup"><span data-stu-id="3da5e-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="3da5e-144">Corpo della richiesta di esempio:</span><span class="sxs-lookup"><span data-stu-id="3da5e-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="3da5e-145">Un output di esempio dovrebbe essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="3da5e-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="3da5e-146">Patch di funzione definita dall'utente con risposta hello</span><span class="sxs-lookup"><span data-stu-id="3da5e-146">Patch UDF with hello response</span></span>
<span data-ttu-id="3da5e-147">Ora hello funzione definita dall'utente devono essere aggiornati con risposta precedente hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3da5e-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="3da5e-148">Corpo della richiesta (output da RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="3da5e-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="3da5e-149">Implementare flusso Analitica trasformazione toocall hello funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="3da5e-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="3da5e-150">Ora eseguire una query hello (qui denominata scoreTweet) per ogni evento di input e scrivere una risposta per l'output di tooan tale evento.</span><span class="sxs-lookup"><span data-stu-id="3da5e-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="3da5e-151">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="3da5e-151">Get help</span></span>
<span data-ttu-id="3da5e-152">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3da5e-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3da5e-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3da5e-153">Next steps</span></span>
* [<span data-ttu-id="3da5e-154">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="3da5e-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3da5e-155">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3da5e-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3da5e-156">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3da5e-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3da5e-157">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3da5e-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3da5e-158">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="3da5e-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
