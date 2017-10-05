---
title: Come usare un servizio Web di Azure Machine Learning | Microsoft Docs
description: "Dopo la pubblicazione di un servizio di Machine Learning, è possibile usare il servizio Web RESTFul che viene reso disponibile come servizio di richiesta-risposta o come un servizio di esecuzione del batch."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: eec9f637b4b2306ab4a888dbd5ef5b9a021bcac5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-consume-an-azure-machine-learning-web-service"></a><span data-ttu-id="eceaa-103">Come usare un servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="eceaa-103">How to consume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="eceaa-104">Dopo aver distribuito un modello predittivo di Azure Machine Learning come servizio Web, è possibile usare un'API REST per inviare dati e ottenere stime.</span><span class="sxs-lookup"><span data-stu-id="eceaa-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API to send it data and get predictions.</span></span> <span data-ttu-id="eceaa-105">È possibile inviare i dati in tempo reale o in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="eceaa-105">You can send the data in real-time or in batch mode.</span></span>

<span data-ttu-id="eceaa-106">Per informazioni su come creare e distribuire un servizio Web di Machine Learning tramite Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="eceaa-106">You can find more information about how to create and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="eceaa-107">Per un'esercitazione su come creare un esperimento in Machine Learning Studio, vedere l'articolo su come [creare il primo esperimento](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="eceaa-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="eceaa-108">Per dettagli su come distribuire un servizio Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="eceaa-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="eceaa-109">Per altre informazioni su Machine Learning in generale, accedere alla [Documentazione su Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="eceaa-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="eceaa-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="eceaa-110">Overview</span></span>
<span data-ttu-id="eceaa-111">Con il servizio Web di Azure Machine Learning, un'applicazione esterna comunica con un modello di valutazione del flusso di lavoro di Machine Learning in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="eceaa-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="eceaa-112">Una chiamata al servizio Web di Machine Learning restituisce i risultati della stima a un'applicazione esterna.</span><span class="sxs-lookup"><span data-stu-id="eceaa-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="eceaa-113">Per effettuare una chiamata al servizio Web di Machine Learning, passare una chiave API creata quando si distribuisce una stima.</span><span class="sxs-lookup"><span data-stu-id="eceaa-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="eceaa-114">Il servizio Web di Machine Learning è basato su REST, una scelta di architettura diffusa per progetti di programmazione Web.</span><span class="sxs-lookup"><span data-stu-id="eceaa-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="eceaa-115">Azure Machine Learning dispone di due tipi di servizi:</span><span class="sxs-lookup"><span data-stu-id="eceaa-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="eceaa-116">Servizio di richiesta-risposta (RRS). Un servizio a latenza bassa e altamente scalabile che offre un'interfaccia ai modelli senza stato creati e distribuiti da Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="eceaa-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="eceaa-117">Servizio esecuzione batch (BES). Un servizio asincrono che valuta un batch di record di dati.</span><span class="sxs-lookup"><span data-stu-id="eceaa-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="eceaa-118">Per altre informazioni sui servizi Web di Machine Learning, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="eceaa-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="eceaa-119">Ottenere una chiave di autorizzazione Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="eceaa-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="eceaa-120">Quando si distribuisce l'esperimento, vengono generate le chiavi API per il servizio Web,</span><span class="sxs-lookup"><span data-stu-id="eceaa-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="eceaa-121">recuperabili da diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="eceaa-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="eceaa-122">Dal portale dei servizi Web di Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="eceaa-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="eceaa-123">Accedere al portale dei [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="eceaa-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="eceaa-124">Per recuperare la chiave API per un nuovo servizio Web Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="eceaa-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="eceaa-125">Nel portale Servizi Web di Machine Learning di Azure, fare clic sul menu **Web Services** (Servizi Web) nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="eceaa-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="eceaa-126">Selezionare il servizio Web per il quale si desidera recuperare la chiave.</span><span class="sxs-lookup"><span data-stu-id="eceaa-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="eceaa-127">Nel menu in alto fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="eceaa-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="eceaa-128">Copiare e salvare la **Chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="eceaa-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="eceaa-129">Per recuperare la chiave API per un nuovo servizio Web Machine Learning di tipo classico:</span><span class="sxs-lookup"><span data-stu-id="eceaa-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="eceaa-130">Nel portale Servizi Web di Machine Learning di Azure, fare clic sul menu **Classic Web Services** (Servizi Web classici) nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="eceaa-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="eceaa-131">Fare clic sul servizio Web in uso.</span><span class="sxs-lookup"><span data-stu-id="eceaa-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="eceaa-132">Selezionare l'endpoint per il quale si desidera recuperare la chiave.</span><span class="sxs-lookup"><span data-stu-id="eceaa-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="eceaa-133">Nel menu in alto fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="eceaa-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="eceaa-134">Copiare e salvare la **Chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="eceaa-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="eceaa-135">Servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="eceaa-135">Classic Web service</span></span>
 <span data-ttu-id="eceaa-136">La chiave di un servizio Web di tipo classico può essere recuperata anche da Machine Learning Studio o dal portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="eceaa-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="eceaa-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="eceaa-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="eceaa-138">In Machine Learning Studio fare clic su **WEB SERVICES** (Servizi Web) a sinistra.</span><span class="sxs-lookup"><span data-stu-id="eceaa-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="eceaa-139">Fare clic su un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="eceaa-139">Click a Web service.</span></span> <span data-ttu-id="eceaa-140">La **chiave API** si trova nella scheda **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="eceaa-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="eceaa-141">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="eceaa-141">Azure classic portal</span></span>
1. <span data-ttu-id="eceaa-142">Fare clic su **MACHINE LEARNING** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="eceaa-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="eceaa-143">Fare clic sull'area di lavoro in cui si trova il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="eceaa-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="eceaa-144">Fare clic su **WEB SERVICES**.</span><span class="sxs-lookup"><span data-stu-id="eceaa-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="eceaa-145">Fare clic su un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="eceaa-145">Click a Web service.</span></span>
5. <span data-ttu-id="eceaa-146">Fare clic su un endpoint.</span><span class="sxs-lookup"><span data-stu-id="eceaa-146">Click an endpoint.</span></span> <span data-ttu-id="eceaa-147">La "CHIAVE API" si trova in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="eceaa-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="eceaa-148"><a id="connect"></a>Connettersi a un servizio Web di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="eceaa-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="eceaa-149">È possibile connettersi a un servizio Web di Machine Learning usando qualsiasi linguaggio di programmazione che supporta la risposta e la richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="eceaa-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="eceaa-150">È possibile visualizzare gli esempi in C#, Python e R da una pagina della guida del servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="eceaa-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="eceaa-151">**Guida alle API di Machine Learning** Una Guida per l'API di Machine Learning viene creata quando si distribuisce un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="eceaa-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="eceaa-152">Vedere [Procedura dettagliata di Azure Machine Learning - Distribuire il servizio Web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="eceaa-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="eceaa-153">La Guida per l'API di Machine Learning contiene i dettagli su un servizio Web di stima.</span><span class="sxs-lookup"><span data-stu-id="eceaa-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="eceaa-154">Fare clic sul servizio Web in uso.</span><span class="sxs-lookup"><span data-stu-id="eceaa-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="eceaa-155">Selezionare l'endpoint per il quale si desidera visualizzare la pagina della guida alle API.</span><span class="sxs-lookup"><span data-stu-id="eceaa-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="eceaa-156">Nel menu in alto fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="eceaa-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="eceaa-157">Fare clic sulla pagina della **guida alle API** negli endpoint Request-Response o Esecuzione batch.</span><span class="sxs-lookup"><span data-stu-id="eceaa-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="eceaa-158">**Per visualizzare la guida alle API di Machine Learning per un nuovo servizio Web**</span><span class="sxs-lookup"><span data-stu-id="eceaa-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="eceaa-159">Nel portale dei servizi Web di Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="eceaa-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="eceaa-160">Fare clic su **WEB SERVICES** (Servizi Web) nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="eceaa-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="eceaa-161">Selezionare il servizio Web per il quale si desidera recuperare la chiave.</span><span class="sxs-lookup"><span data-stu-id="eceaa-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="eceaa-162">Fare clic su **Consume** (Uso) per ottenere l'URI per i servizi Richiesta/Risposta ed Esecuzione in batch, nonché il codice di esempio in C#, R e Python.</span><span class="sxs-lookup"><span data-stu-id="eceaa-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="eceaa-163">Fare clic su **Swagger API** (API Swagger) per ottenere la documentazione basata su Swagger per le API chiamate dagli URI specificati.</span><span class="sxs-lookup"><span data-stu-id="eceaa-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="eceaa-164">Esempio C#</span><span class="sxs-lookup"><span data-stu-id="eceaa-164">C# Sample</span></span>
<span data-ttu-id="eceaa-165">Per connettersi a un servizio Web di Machine Learning, usare un **HttpClient** che passa ScoreData.</span><span class="sxs-lookup"><span data-stu-id="eceaa-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="eceaa-166">ScoreData contiene FeatureVector, un vettore n-dimensionale di funzioni numeriche che rappresentano ScoreData.</span><span class="sxs-lookup"><span data-stu-id="eceaa-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="eceaa-167">Effettuare l'autenticazione al servizio di Machine Learning con una chiave API.</span><span class="sxs-lookup"><span data-stu-id="eceaa-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="eceaa-168">Per connettersi a un servizio Web di Machine Learning, è necessario installare il pacchetto NuGet **Microsoft.AspNet.WebApi.Client** .</span><span class="sxs-lookup"><span data-stu-id="eceaa-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="eceaa-169">**Installare il Nuget Microsoft.AspNet.WebApi.Client in Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="eceaa-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="eceaa-170">Pubblicare il set di dati di download dal servizio Web UCI: Adult 2 class dataset.</span><span class="sxs-lookup"><span data-stu-id="eceaa-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="eceaa-171">Fare clic su **Strumenti** > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="eceaa-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="eceaa-172">Scegliere **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="eceaa-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="eceaa-173">**Per eseguire l'esempio di codice**</span><span class="sxs-lookup"><span data-stu-id="eceaa-173">**To run the code sample**</span></span>

1. <span data-ttu-id="eceaa-174">Pubblicare l'esperimento "Sample 1: Download dataset from UCI: Adult 2 class dataset", che fa parte della raccolta di esempi di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="eceaa-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="eceaa-175">Assegnare ad apiKey la chiave di un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="eceaa-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="eceaa-176">Vedere la sezione precedente **Ottenere una chiave di autorizzazione di Azure Machine Learning** .</span><span class="sxs-lookup"><span data-stu-id="eceaa-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="eceaa-177">Assegnare l'URI del servizio con l'URI della richiesta.</span><span class="sxs-lookup"><span data-stu-id="eceaa-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="eceaa-178">Esempio Python</span><span class="sxs-lookup"><span data-stu-id="eceaa-178">Python Sample</span></span>
<span data-ttu-id="eceaa-179">Per connettersi a un servizio Web di Machine Learning, usare la libreria **urllib2** con ScoreData.</span><span class="sxs-lookup"><span data-stu-id="eceaa-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="eceaa-180">ScoreData contiene FeatureVector, un vettore n-dimensionale di funzioni numeriche che rappresentano ScoreData.</span><span class="sxs-lookup"><span data-stu-id="eceaa-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="eceaa-181">Effettuare l'autenticazione al servizio di Machine Learning con una chiave API.</span><span class="sxs-lookup"><span data-stu-id="eceaa-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="eceaa-182">**Per eseguire l'esempio di codice**</span><span class="sxs-lookup"><span data-stu-id="eceaa-182">**To run the code sample**</span></span>

1. <span data-ttu-id="eceaa-183">Distribuire l'esperimento "Sample 1: Download dataset from UCI: Adult 2 class dataset", che fa parte della raccolta di esempi di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="eceaa-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="eceaa-184">Assegnare ad apiKey la chiave di un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="eceaa-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="eceaa-185">Vedere la sezione **Ottenere una chiave di autorizzazione Azure Machine Learning** all'inizio di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="eceaa-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="eceaa-186">Assegnare l'URI del servizio con l'URI della richiesta.</span><span class="sxs-lookup"><span data-stu-id="eceaa-186">Assign serviceUri with the Request URI.</span></span>

