---
title: Usare gli endpoint di Azure Machine Learning in Analisi di flusso | Documentazione Microsoft
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
ms.openlocfilehash: d3a46190dd802bf31ea03ef38304d58e6e63b66d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="7abda-103">Integrazione di Machine Learning in Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7abda-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="7abda-104">Analisi di flusso supporta funzioni definite dall'utente che chiamano gli endpoint di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7abda-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="7abda-105">Il supporto dell'API REST per questa funzionalità è illustrato in dettaglio nella [libreria delle API REST di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="7abda-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="7abda-106">Questo articolo fornisce le informazioni supplementari necessarie per la corretta implementazione di questa funzionalità in Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="7abda-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="7abda-107">È stata pubblicata anche un'esercitazione che è disponibile [qui](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7abda-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="7abda-108">Panoramica: Terminologia di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7abda-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="7abda-109">Microsoft Azure Machine Learning fornisce uno strumento di trascinamento collaborativo che consente di compilare, testare e distribuire soluzioni di analisi predittiva ai dati.</span><span class="sxs-lookup"><span data-stu-id="7abda-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="7abda-110">Questo strumento si chiama *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="7abda-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="7abda-111">e viene usato per interagire con le risorse di Machine Learning ed eseguire facilmente la compilazione, il test e l'iterazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="7abda-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="7abda-112">Di seguito sono riportate le risorse e le rispettive definizioni.</span><span class="sxs-lookup"><span data-stu-id="7abda-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="7abda-113">**Area di lavoro**: l' *area di lavoro* è un contenitore che include tutte le altre risorse di Machine Learning per poterle gestire e controllare.</span><span class="sxs-lookup"><span data-stu-id="7abda-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="7abda-114">**Esperimento**: gli *esperimenti* vengono creati dagli esperti di gestione dati per utilizzare i set di dati ed eseguire il training di un modello di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7abda-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="7abda-115">**Endpoint**: gli *endpoint* sono gli oggetti di Azure Machine Learning usati per accettare le funzionalità come input, applicare un modello di apprendimento automatico specificato e restituire un output con punteggio.</span><span class="sxs-lookup"><span data-stu-id="7abda-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="7abda-116">**Servizio Web di assegnazione dei punteggi**: un *servizio Web di assegnazione dei punteggi* è una raccolta di endpoint, come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="7abda-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="7abda-117">Ogni endpoint ha API per l'esecuzione batch e per l'esecuzione sincrona.</span><span class="sxs-lookup"><span data-stu-id="7abda-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="7abda-118">Analisi di flusso usa l'esecuzione sincrona.</span><span class="sxs-lookup"><span data-stu-id="7abda-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="7abda-119">Il servizio specifico è detto [servizio di richiesta/risposta](../machine-learning/machine-learning-consume-web-services.md) in Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="7abda-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="7abda-120">Risorse di Machine Learning necessarie per i processi di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7abda-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="7abda-121">Ai fini dell'elaborazione dei processi di Analisi di flusso, per la corretta esecuzione sono necessari un endpoint di richiesta/risposta, una [chiave API](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md)e una definizione swagger.</span><span class="sxs-lookup"><span data-stu-id="7abda-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="7abda-122">Analisi di flusso ha un endpoint aggiuntivo che crea l'URL per l'endpoint swagger, cerca l'interfaccia e restituisce all'utente una definizione UDF predefinita.</span><span class="sxs-lookup"><span data-stu-id="7abda-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="7abda-123">Configurare una funzione definita dall'utente di Analisi di flusso e di Machine Learning con l'API REST</span><span class="sxs-lookup"><span data-stu-id="7abda-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="7abda-124">Usando le API REST è possibile configurare il processo per chiamare le funzioni di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7abda-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="7abda-125">Attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7abda-125">The steps are as follows:</span></span>

1. <span data-ttu-id="7abda-126">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="7abda-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="7abda-127">Definire un input</span><span class="sxs-lookup"><span data-stu-id="7abda-127">Define an input</span></span>
3. <span data-ttu-id="7abda-128">Definire un output</span><span class="sxs-lookup"><span data-stu-id="7abda-128">Define an output</span></span>
4. <span data-ttu-id="7abda-129">Creare una funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="7abda-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="7abda-130">Scrivere una trasformazione di Analisi di flusso che chiami la funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="7abda-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="7abda-131">Avviare il processo</span><span class="sxs-lookup"><span data-stu-id="7abda-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="7abda-132">Creazione di una funzione definita dall'utente con proprietà di base</span><span class="sxs-lookup"><span data-stu-id="7abda-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="7abda-133">Il codice di esempio seguente crea una funzione definita dall'utente scalare denominata *newudf* che viene associata a un endpoint di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7abda-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="7abda-134">Si noti che l'*endpoint* (URI del servizio) è disponibile nella pagina della Guida dell'API per il servizio scelto e la *chiave API* nella pagina principale dei servizi.</span><span class="sxs-lookup"><span data-stu-id="7abda-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="7abda-135">Corpo della richiesta di esempio:</span><span class="sxs-lookup"><span data-stu-id="7abda-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="7abda-136">Chiamare l'endpoint RetrieveDefaultDefinition per la funzione definita dall'utente predefinita</span><span class="sxs-lookup"><span data-stu-id="7abda-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="7abda-137">Una volta creata la struttura della funzione definita dall'utente, è necessaria la definizione completa della funzione.</span><span class="sxs-lookup"><span data-stu-id="7abda-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="7abda-138">L'endpoint RetreiveDefaultDefinition consente di ottenere la definizione predefinita per una funzione scalare associata a un endpoint di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7abda-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="7abda-139">Per il payload seguente è necessario ottenere la definizione di definizione definita dall'utente predefinita per una funzione scalare associata a un endpoint di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7abda-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="7abda-140">Il payload non specifica l'endpoint effettivo perché è già stato fornito durante la richiesta PUT.</span><span class="sxs-lookup"><span data-stu-id="7abda-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="7abda-141">Analisi di flusso chiama l'endpoint fornito nella richiesta se viene specificato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="7abda-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="7abda-142">In caso contrario, usa quello a cui si è fatto riferimento in origine.</span><span class="sxs-lookup"><span data-stu-id="7abda-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="7abda-143">Qui la funzione definita dall'utente accetta un singolo parametro di stringa (una frase) e restituisce un singolo output di tipo stringa indicante l'etichetta "sentiment" per tale frase.</span><span class="sxs-lookup"><span data-stu-id="7abda-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="7abda-144">Corpo della richiesta di esempio:</span><span class="sxs-lookup"><span data-stu-id="7abda-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="7abda-145">Un output di esempio dovrebbe essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="7abda-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="7abda-146">Inserire la risposta nella funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="7abda-146">Patch UDF with the response</span></span>
<span data-ttu-id="7abda-147">Ora è necessario inserire la risposta precedente nella funzione definita dall'utente, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7abda-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="7abda-148">Corpo della richiesta (output da RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="7abda-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="7abda-149">Implementare una trasformazione di Analisi di flusso per chiamare la funzione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="7abda-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="7abda-150">Cercare ora nella funzione definita dall'utente (denominata qui scoreTweet) ogni evento di input e scrivere una risposta per ogni evento in un output.</span><span class="sxs-lookup"><span data-stu-id="7abda-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="7abda-151">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="7abda-151">Get help</span></span>
<span data-ttu-id="7abda-152">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="7abda-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7abda-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7abda-153">Next steps</span></span>
* [<span data-ttu-id="7abda-154">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7abda-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7abda-155">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7abda-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7abda-156">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7abda-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7abda-157">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7abda-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7abda-158">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="7abda-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
