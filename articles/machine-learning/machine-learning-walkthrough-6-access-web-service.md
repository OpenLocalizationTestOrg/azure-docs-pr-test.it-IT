---
title: 'Passaggio 6: Accedere al servizio Web di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 6 della procedura dettagliata Sviluppare una soluzione predittiva: Accedere a un servizio Web attivo di Azure Machine Learning.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="a8913-103">Passaggio 6 della procedura dettagliata: Accedere al servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a8913-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="a8913-104">Questo è l'ultimo passaggio della procedura dettagliata [Sviluppare una soluzione di analisi predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a8913-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="a8913-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a8913-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="a8913-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="a8913-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="a8913-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="a8913-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a8913-108">Eseguire il training e valutare i modelli</span><span class="sxs-lookup"><span data-stu-id="a8913-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="a8913-109">Distribuire il servizio Web</span><span class="sxs-lookup"><span data-stu-id="a8913-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="a8913-110">**Accedere al servizio Web**</span><span class="sxs-lookup"><span data-stu-id="a8913-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="a8913-111">Nel passaggio precedente di questa procedura dettagliata è stato distribuito un servizio Web che utilizza il modello di previsione del rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="a8913-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="a8913-112">Ora gli utenti sono in grado di inviare dati al servizio e ricevere risultati.</span><span class="sxs-lookup"><span data-stu-id="a8913-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="a8913-113">Questo è un servizio Web di Azure che può ricevere e restituire dati tramite le API REST in due modi:</span><span class="sxs-lookup"><span data-stu-id="a8913-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="a8913-114">**Richiesta/risposta** : l'utente invia uno o più set di dati di credito al servizio usando un protocollo HTTP e il servizio risponde con uno o più set di risultati.</span><span class="sxs-lookup"><span data-stu-id="a8913-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="a8913-115">**Esecuzione batch** : l'utente archivia una o più righe di dati di credito in un BLOB di Azure e invia il percorso del BLOB al servizio.</span><span class="sxs-lookup"><span data-stu-id="a8913-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="a8913-116">Il servizio assegna un punteggio a tutte le righe di dati del BLOB di input, archivia i risultati in un altro BLOB e restituisce l'URL di quel contenitore.</span><span class="sxs-lookup"><span data-stu-id="a8913-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="a8913-117">È il modo più rapido e semplice per accedere a un servizio Web classico tramite il [modello di app Web di richiesta-risposta di Azure Machine Learning ](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) o il [modello di app Web di esecuzione batch di Azure Machine Learning](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="a8913-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="a8913-118">I modelli di app Web consentono di compilare un'app Web personalizzata che riconosce i dati di input del servizio Web e i dati da restituire.</span><span class="sxs-lookup"><span data-stu-id="a8913-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="a8913-119">È sufficiente concedere l'accesso al proprio servizio Web e ai dati e il modello farà il resto.</span><span class="sxs-lookup"><span data-stu-id="a8913-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="a8913-120">Per altre informazioni sull'utilizzo di modelli di app Web, vedere [Utilizzare un servizio Web di Azure Machine Learning con un modello di app Web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="a8913-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="a8913-121">È possibile sviluppare anche un'applicazione personalizzata per accedere al servizio Web utilizzando il codice di avvio fornito automaticamente nei linguaggi di programmazione R, C# e Python.</span><span class="sxs-lookup"><span data-stu-id="a8913-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="a8913-122">Per informazioni complete, vedere [Come usare un servizio Web di Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="a8913-122">You can find complete details in [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

