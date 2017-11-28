---
title: aaaLogging per servizi web Machine Learning | Documenti Microsoft
description: Informazioni su come servizi web registrazione tooenable per Machine Learning. Registrazione fornisce informazioni aggiuntive toohelp risolvere hello API.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="f434d-104">Abilitare la registrazione per i servizi Web di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f434d-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="f434d-105">Questo documento vengono fornite informazioni su hello registrazione delle funzionalità di servizi web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f434d-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="f434d-106">Registrazione fornisce informazioni aggiuntive, oltre a un numero di errore e un messaggio, che consentono di risolvere i problemi del toohello chiamate API di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f434d-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="f434d-107">La modalità registrazione tooenable per un servizio Web</span><span class="sxs-lookup"><span data-stu-id="f434d-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="f434d-108">Abilitare la registrazione da hello [servizi Web di Azure Machine Learning](https://services.azureml.net) portale.</span><span class="sxs-lookup"><span data-stu-id="f434d-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="f434d-109">Accedi al portale di servizi Web di Azure Machine Learning toohello all'indirizzo [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f434d-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="f434d-110">Per un servizio web classica, è inoltre possibile ottenere toohello portale facendo **nuova esperienza di servizi Web** nella pagina servizi Web di Machine Learning hello in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f434d-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Collegamento New Web Services Experience](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="f434d-112">Nella barra dei menu superiore hello, fare clic su **servizi Web** per un nuovo servizio web oppure fare clic su **classico servizi Web** per un classico servizio web.</span><span class="sxs-lookup"><span data-stu-id="f434d-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selezione di servizi Web nuovi o classici](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="f434d-114">Per un nuovo servizio web, fare clic sul nome del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="f434d-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="f434d-115">Per un servizio web classica, fare clic sul nome del servizio web di hello e quindi fare clic su endpoint appropriato hello nella pagina successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="f434d-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="f434d-116">Nella barra dei menu superiore hello, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="f434d-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="f434d-117">Set hello **Abilita registrazione** opzione troppo*errore* (toolog solo gli errori) o *tutti* (per la registrazione completa).</span><span class="sxs-lookup"><span data-stu-id="f434d-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Selezione del livello di registrazione](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="f434d-119">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f434d-119">Click **Save**.</span></span>

7. <span data-ttu-id="f434d-120">Per i servizi web classica creare hello **ml diagnostica** contenitore.</span><span class="sxs-lookup"><span data-stu-id="f434d-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="f434d-121">Tutti i log di servizio web vengono conservati in un contenitore blob denominato **ml diagnostica** nell'account di archiviazione hello associato al servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="f434d-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="f434d-122">Per i nuovi servizi web, questo contenitore viene creato hello primo accesso del servizio web di hello.</span><span class="sxs-lookup"><span data-stu-id="f434d-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="f434d-123">Per i servizi web classica, è necessario contenitore hello toocreate se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="f434d-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="f434d-124">In hello [portale di Azure](https://portal.azure.com), visitare toohello account di archiviazione associato al servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="f434d-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="f434d-125">In **Servizio BLOB** fare clic su **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="f434d-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="f434d-126">Se il contenitore di hello **ml diagnostica** non esiste, fare clic su **+ contenitore**, assegnare hello contenitore hello nome "ml diagnostica" e selezionare hello **tipo di accesso** come "Blob".</span><span class="sxs-lookup"><span data-stu-id="f434d-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="f434d-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f434d-127">Click **OK**.</span></span>

      ![Selezione del livello di registrazione](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="f434d-129">Per un servizio web classica, hello del Dashboard di servizi Web in Machine Learning Studio dispone anche di registrazione tooenable commutatore.</span><span class="sxs-lookup"><span data-stu-id="f434d-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="f434d-130">Tuttavia, poiché la registrazione è ora gestita tramite il portale di servizi Web hello, è necessario tooenable registrazione tramite il portale di hello come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f434d-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="f434d-131">Se è già abilitata la registrazione in Studio, nel portale dei servizi Web hello, disabilitare la registrazione e abilitarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="f434d-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="f434d-132">effetti Hello dell'abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="f434d-132">hello effects of enabling logging</span></span>
<span data-ttu-id="f434d-133">Quando è abilitata la registrazione, diagnostica hello ed errori restituiti dall'endpoint del servizio web hello vengono registrate in hello **ml diagnostica** contenitore blob nell'Account di archiviazione Azure hello collegate con area di lavoro dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="f434d-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="f434d-134">Questo contenitore contiene tutte le informazioni di diagnostica di hello per tutti gli endpoint servizio web hello per tutte le aree di lavoro di hello associate a questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f434d-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="f434d-135">Hello registri possono essere visualizzati utilizzando uno dei hello diversi strumenti disponibili tooexplore un Account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f434d-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="f434d-136">Hello più semplice può essere toonavigate toohello account di archiviazione nel portale di Azure hello, fare clic su **contenitori**e quindi fare clic sul contenitore di hello **ml diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="f434d-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="f434d-137">Informazioni dettagliate dei BLOB dei log</span><span class="sxs-lookup"><span data-stu-id="f434d-137">Log blob detail information</span></span>
<span data-ttu-id="f434d-138">Ogni blob nel contenitore hello contiene le informazioni di diagnostica hello esattamente per una delle seguenti azioni hello:</span><span class="sxs-lookup"><span data-stu-id="f434d-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="f434d-139">Un'esecuzione del metodo hello esecuzione Batch</span><span class="sxs-lookup"><span data-stu-id="f434d-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="f434d-140">Un'esecuzione del metodo hello richiesta-risposta</span><span class="sxs-lookup"><span data-stu-id="f434d-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="f434d-141">Inizializzazione di un contenitore Request-Response</span><span class="sxs-lookup"><span data-stu-id="f434d-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="f434d-142">nome Hello di ciascun blob ha un prefisso di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="f434d-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="f434d-143">Dove _tipo Log_ è uno dei seguenti valori hello:</span><span class="sxs-lookup"><span data-stu-id="f434d-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="f434d-144">o batch</span><span class="sxs-lookup"><span data-stu-id="f434d-144">batch</span></span>  
* <span data-ttu-id="f434d-145">punteggio/richieste</span><span class="sxs-lookup"><span data-stu-id="f434d-145">score/requests</span></span>  
* <span data-ttu-id="f434d-146">punteggio/init</span><span class="sxs-lookup"><span data-stu-id="f434d-146">score/init</span></span>  

