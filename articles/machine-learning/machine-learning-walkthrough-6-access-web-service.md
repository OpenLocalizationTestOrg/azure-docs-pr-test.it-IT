---
title: 'Passaggio 6: Accesso del servizio Web di Machine Learning hello | Documenti Microsoft'
description: 'Passaggio 6 di hello sviluppare una procedura dettagliata soluzione predittiva: accedere a un servizio Web di Azure Machine Learning attivo.'
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
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="8111e-103">Procedura dettagliata passaggio 6: Accedere al servizio web Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="8111e-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="8111e-104">Hello ultimo passaggio della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="8111e-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="8111e-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8111e-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="8111e-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="8111e-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="8111e-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="8111e-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="8111e-108">Eseguire il training e valutare i modelli di hello</span><span class="sxs-lookup"><span data-stu-id="8111e-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="8111e-109">Distribuzione di servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="8111e-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="8111e-110">**Accedere al servizio Web hello**</span><span class="sxs-lookup"><span data-stu-id="8111e-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="8111e-111">Nel passaggio precedente di hello in questa procedura dettagliata sono stati distribuiti un servizio web che utilizza il nostro modello di stima rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="8111e-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="8111e-112">Ora gli utenti sono in grado di toosend dati tooit e ricevano i risultati.</span><span class="sxs-lookup"><span data-stu-id="8111e-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="8111e-113">Hello servizio Web è un servizio web di Azure che può ricevere e restituire dati tramite le API REST in uno dei due modi:</span><span class="sxs-lookup"><span data-stu-id="8111e-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="8111e-114">**Richiesta/risposta** : utente hello invia uno o più righe di carta di credito dati toohello del servizio tramite un protocollo HTTP e hello servizio risponde con uno o più set di risultati.</span><span class="sxs-lookup"><span data-stu-id="8111e-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="8111e-115">**Esecuzione batch** : utente hello archivia uno o più righe di dati di carta di credito in un Azure blob e quindi invia hello blob percorso toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="8111e-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="8111e-116">Archivia i risultati in un altro blob hello e restituisce l'URL del contenitore di hello hello di punteggi servizio Hello che tutti hello righe di dati nel blob di input.</span><span class="sxs-lookup"><span data-stu-id="8111e-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="8111e-117">Hello tooaccess modo rapido e semplice consiste nell'utilizzare un servizio web classica hello [Azure ML richiesta-risposta del servizio Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) o [modello di App di Azure ML Batch esecuzione del servizio Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="8111e-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="8111e-118">I modelli di app Web consentono di compilare un'app Web personalizzata che riconosce i dati di input del servizio Web e i dati da restituire.</span><span class="sxs-lookup"><span data-stu-id="8111e-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="8111e-119">È sufficiente toodo forniscono dati e servizio web di accesso tooyour e modello hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="8111e-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="8111e-120">Per ulteriori informazioni sull'utilizzo di modelli di hello web app, vedere [utilizzo di un servizio Web di Azure Machine Learning con un modello di app web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="8111e-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="8111e-121">È inoltre possibile sviluppare un servizio web di applicazione personalizzata tooaccess hello utilizzando il codice di avvio disponibile per l'utente in R, c# e linguaggi di programmazione Python.</span><span class="sxs-lookup"><span data-stu-id="8111e-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="8111e-122">È possibile trovare informazioni dettagliate in [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="8111e-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

