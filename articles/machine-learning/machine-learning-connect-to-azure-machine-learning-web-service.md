---
title: aaaConnect tooa servizio Web di Machine Learning | Documenti Microsoft
description: Con c# o Python, connettersi tooan servizio Web di Azure Machine Learning usando una chiave di autorizzazione.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="49ca4-103">Connettersi tooan servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="49ca4-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="49ca4-104">Hello esperienza dello sviluppatore Azure Machine Learning è un stime di toomake API del servizio Web dai dati di input in tempo reale o in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="49ca4-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="49ca4-105">Utilizzare le stime di Azure Machine Learning Studio toocreate e distribuire un servizio Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49ca4-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="49ca4-106">toolearn sulla toocreate e distribuire un servizio Web di Machine Learning tramite Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="49ca4-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="49ca4-107">Per un'esercitazione su come toocreate un esperimento di Machine Learning Studio, vedere [l'esperimento prima di creare](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="49ca4-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="49ca4-108">Per informazioni dettagliate su come toodeploy un servizio Web, vedere [distribuire un servizio Web di Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="49ca4-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="49ca4-109">Per ulteriori informazioni su Machine Learning in generale, visitare hello [Centro documentazione di Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="49ca4-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="49ca4-110">Servizio Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="49ca4-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="49ca4-111">Con il servizio Web di Azure Machine Learning hello, un'applicazione esterna comunica con un modello del flusso di lavoro di Machine Learning assegnazione dei punteggi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="49ca4-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="49ca4-112">Una chiamata al servizio Web di Machine Learning restituisce i risultati della stima tooan di applicazione esterna.</span><span class="sxs-lookup"><span data-stu-id="49ca4-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="49ca4-113">una chiamata al servizio Web di Machine Learning toomake, passare una chiave API che viene creata quando si distribuisce una stima.</span><span class="sxs-lookup"><span data-stu-id="49ca4-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="49ca4-114">servizio Web di Machine Learning Hello è basato su REST, una scelta di architettura comune per i progetti di programmazione web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="49ca4-115">Azure Machine Learning dispone di due tipi di servizi:</span><span class="sxs-lookup"><span data-stu-id="49ca4-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="49ca4-116">Il servizio di richiesta-risposta (RR) – una bassa latenza, servizio altamente scalabile che offre un'interfaccia toohello modelli senza stato creato e distribuito da hello Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="49ca4-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="49ca4-117">Servizio esecuzione batch (BES). Un servizio asincrono che valuta un batch di record di dati.</span><span class="sxs-lookup"><span data-stu-id="49ca4-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="49ca4-118">Per altre informazioni sui servizi Web di Machine Learning, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="49ca4-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="49ca4-119">Ottenere una chiave di autorizzazione Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="49ca4-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="49ca4-120">Quando si distribuisce l'esperimento, le chiavi API vengono generate per hello servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="49ca4-121">È possibile recuperare le chiavi di hello da diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="49ca4-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="49ca4-122">Dal portale di servizi Web di Microsoft Azure Machine Learning: hello</span><span class="sxs-lookup"><span data-stu-id="49ca4-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="49ca4-123">Accedi toohello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net) portale.</span><span class="sxs-lookup"><span data-stu-id="49ca4-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="49ca4-124">chiave di hello API tooretrieve per un servizio Web di nuova Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="49ca4-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="49ca4-125">Nel portale di servizi Web di Azure Machine Learning hello, fare clic su **servizi Web** menu in alto hello.</span><span class="sxs-lookup"><span data-stu-id="49ca4-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="49ca4-126">Fare clic su servizio Web hello per cui si desidera chiave hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="49ca4-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="49ca4-127">Scegliere dal menu superiore hello **consumare**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="49ca4-128">Copiare e salvare hello **chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="49ca4-129">chiave di hello API tooretrieve per un servizio Web di classico Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="49ca4-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="49ca4-130">Nel portale di servizi Web di Azure Machine Learning hello, fare clic su **servizi Web classico** menu in alto hello.</span><span class="sxs-lookup"><span data-stu-id="49ca4-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="49ca4-131">Fare clic su servizio Web hello con cui si lavora.</span><span class="sxs-lookup"><span data-stu-id="49ca4-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="49ca4-132">Fare clic su endpoint hello per cui si desidera chiave hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="49ca4-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="49ca4-133">Scegliere dal menu superiore hello **consumare**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="49ca4-134">Copiare e salvare hello **chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="49ca4-135">Servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="49ca4-135">Classic Web service</span></span>
 <span data-ttu-id="49ca4-136">È inoltre possibile recuperare una chiave per un servizio Web classico da Machine Learning Studio o hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="49ca4-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="49ca4-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="49ca4-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="49ca4-138">In Machine Learning Studio, fare clic su **servizi WEB** a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="49ca4-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="49ca4-139">Fare clic su un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-139">Click a Web service.</span></span> <span data-ttu-id="49ca4-140">Hello **chiave API** in hello **DASHBOARD** scheda.</span><span class="sxs-lookup"><span data-stu-id="49ca4-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="49ca4-141">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="49ca4-141">Azure classic portal</span></span>
1. <span data-ttu-id="49ca4-142">Fare clic su **MACHINE LEARNING** a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="49ca4-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="49ca4-143">Fare clic su area di lavoro hello in cui si trova il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="49ca4-144">Fare clic su **WEB SERVICES**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="49ca4-145">Fare clic su un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-145">Click a Web service.</span></span>
5. <span data-ttu-id="49ca4-146">Fare clic su un endpoint.</span><span class="sxs-lookup"><span data-stu-id="49ca4-146">Click an endpoint.</span></span> <span data-ttu-id="49ca4-147">Hello "Chiave API" non è attivo hello in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="49ca4-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="49ca4-148"><a id="connect"></a>La connessione del servizio Web di Machine Learning tooa</span><span class="sxs-lookup"><span data-stu-id="49ca4-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="49ca4-149">È possibile connettersi tooa servizio Web di Machine Learning utilizzando qualsiasi linguaggio di programmazione che supporta la risposta e richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="49ca4-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="49ca4-150">È possibile visualizzare gli esempi in C#, Python e R da una pagina della guida del servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49ca4-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="49ca4-151">**Guida alle API di Machine Learning** Una Guida per l'API di Machine Learning viene creata quando si distribuisce un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="49ca4-152">Vedere [Procedura dettagliata di Azure Machine Learning - Distribuire il servizio Web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="49ca4-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="49ca4-153">Guida di Machine Learning API Hello contiene dettagli su una stima del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="49ca4-154">Fare clic su servizio Web hello con cui si lavora.</span><span class="sxs-lookup"><span data-stu-id="49ca4-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="49ca4-155">Fare clic su endpoint hello per cui si desidera tooview hello pagina della Guida di API.</span><span class="sxs-lookup"><span data-stu-id="49ca4-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="49ca4-156">Scegliere dal menu superiore hello **consumare**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="49ca4-157">Fare clic su **pagina della Guida API** in hello richiesta-risposta o gli endpoint di esecuzione del Batch.</span><span class="sxs-lookup"><span data-stu-id="49ca4-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="49ca4-158">**la Guida di Machine Learning API tooview per un servizio Web nuovo**</span><span class="sxs-lookup"><span data-stu-id="49ca4-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="49ca4-159">Nel portale dei servizi Web Azure Machine Learning hello:</span><span class="sxs-lookup"><span data-stu-id="49ca4-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="49ca4-160">Fare clic su **servizi WEB** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="49ca4-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="49ca4-161">Fare clic su servizio Web hello per cui si desidera chiave hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="49ca4-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="49ca4-162">Fare clic su **consumare** tooget hello URI per la richiesta Reposonse hello e servizi per l'esecuzione Batch e codice di esempio in c#, R e Python.</span><span class="sxs-lookup"><span data-stu-id="49ca4-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="49ca4-163">Fare clic su **Swagger API** tooget Swagger documentazione di base per hello API chiamata da hello specificato gli URI.</span><span class="sxs-lookup"><span data-stu-id="49ca4-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="49ca4-164">Esempio C#</span><span class="sxs-lookup"><span data-stu-id="49ca4-164">C# Sample</span></span>
<span data-ttu-id="49ca4-165">tooconnect tooa servizio Web di Machine Learning, utilizzare un **HttpClient** passando ScoreData.</span><span class="sxs-lookup"><span data-stu-id="49ca4-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="49ca4-166">ScoreData contiene un FeatureVector, un vettore di n-dimensionale delle funzionalità numerico che rappresenta hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="49ca4-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="49ca4-167">Servizio di Machine Learning toohello l'autenticazione con una chiave API.</span><span class="sxs-lookup"><span data-stu-id="49ca4-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="49ca4-168">tooconnect tooa servizio Web di Machine Learning, hello **webapi** è necessario installare il pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="49ca4-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="49ca4-169">**Installare il Nuget Microsoft.AspNet.WebApi.Client in Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="49ca4-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="49ca4-170">Pubblicare il set di dati di hello Download da UCI: 2 per adulti classe dataset servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="49ca4-171">Fare clic su **Strumenti** > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="49ca4-172">Scegliere **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="49ca4-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="49ca4-173">**Nell'esempio di codice hello toorun**</span><span class="sxs-lookup"><span data-stu-id="49ca4-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="49ca4-174">Pubblicare "esempio 1: scaricare set di dati da UCI: adulto 2 classe dataset" esperimento, parte della raccolta di Machine Learning esempio hello.</span><span class="sxs-lookup"><span data-stu-id="49ca4-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="49ca4-175">Assegnare apiKey con chiave hello da un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="49ca4-176">Vedere la sezione precedente **Ottenere una chiave di autorizzazione di Azure Machine Learning** .</span><span class="sxs-lookup"><span data-stu-id="49ca4-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="49ca4-177">Assegnare serviceUri con hello URI della richiesta.</span><span class="sxs-lookup"><span data-stu-id="49ca4-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="49ca4-178">Esempio Python</span><span class="sxs-lookup"><span data-stu-id="49ca4-178">Python Sample</span></span>
<span data-ttu-id="49ca4-179">tooconnect tooa servizio Web di Machine Learning, utilizzare hello **urllib2** libreria passando ScoreData.</span><span class="sxs-lookup"><span data-stu-id="49ca4-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="49ca4-180">ScoreData contiene un FeatureVector, un vettore di n-dimensionale delle funzionalità numerico che rappresenta hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="49ca4-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="49ca4-181">Servizio di Machine Learning toohello l'autenticazione con una chiave API.</span><span class="sxs-lookup"><span data-stu-id="49ca4-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="49ca4-182">**Nell'esempio di codice hello toorun**</span><span class="sxs-lookup"><span data-stu-id="49ca4-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="49ca4-183">Distribuire "esempio 1: scaricare set di dati da UCI: adulto 2 classe dataset" esperimento, parte della raccolta di Machine Learning esempio hello.</span><span class="sxs-lookup"><span data-stu-id="49ca4-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="49ca4-184">Assegnare apiKey con chiave hello da un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="49ca4-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="49ca4-185">Vedere hello **ottenere una chiave di autorizzazione di Azure Machine Learning** sezione parte iniziale di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="49ca4-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="49ca4-186">Assegnare serviceUri con hello URI della richiesta.</span><span class="sxs-lookup"><span data-stu-id="49ca4-186">Assign serviceUri with hello Request URI.</span></span>

