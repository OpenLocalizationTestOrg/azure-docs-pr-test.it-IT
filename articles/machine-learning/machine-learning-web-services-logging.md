---
title: Registrazione per i servizi Web di Machine Learning | Documentazione Microsoft
description: Informazioni su come abilitare la registrazione per i servizi Web di Machine Learning. La registrazione fornisce informazioni aggiuntive per risolvere i problemi relativi alle API.
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
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="6802e-104">Abilitare la registrazione per i servizi Web di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6802e-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="6802e-105">Questo documento include informazioni sulla capacità di registrazione dei servizi Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6802e-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="6802e-106">La registrazione offre informazioni aggiuntive per la risoluzione dei problemi delle API di Machine Learning, non soltanto un semplice codice di errore e un messaggio.</span><span class="sxs-lookup"><span data-stu-id="6802e-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="6802e-107">Come abilitare la registrazione per un servizio Web</span><span class="sxs-lookup"><span data-stu-id="6802e-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="6802e-108">La registrazione viene abilitata nel portale dei [servizi Web di Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="6802e-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="6802e-109">Accedere al portale dei servizi Web di Azure Machine Learning all'indirizzo [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="6802e-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="6802e-110">Per un servizio Web classico, è possibile anche accedere al portale facendo clic su **New Web Services Experience** (Nuovi servizi Web) nella pagina dei servizi Web di Machine Learning in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="6802e-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Collegamento New Web Services Experience](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="6802e-112">Nella barra dei menu superiore fare clic su **Servizi Web** per un nuovo servizio Web oppure su **Classic Web Services** (Servizi Web classici) per un servizio Web classico.</span><span class="sxs-lookup"><span data-stu-id="6802e-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selezione di servizi Web nuovi o classici](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="6802e-114">Per un nuovo servizio Web, fare clic sul nome del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="6802e-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="6802e-115">Per un servizio Web classico, fare clic sul nome del servizio Web e nella pagina successiva fare clic sull'endpoint appropriato.</span><span class="sxs-lookup"><span data-stu-id="6802e-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="6802e-116">Nella barra dei menu superiore fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="6802e-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="6802e-117">Impostare l'opzione **Abilita registrazione** su *Errore*, per registrare solo gli errori, o su *Tutti*, per la registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="6802e-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Selezione del livello di registrazione](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="6802e-119">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6802e-119">Click **Save**.</span></span>

7. <span data-ttu-id="6802e-120">Per i servizi Web classici, creare il contenitore **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="6802e-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="6802e-121">Tutti i registri dei servizi Web vengono mantenuti in un contenitore BLOB denominato **ml-diagnostics** nell'account di archiviazione associato al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="6802e-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="6802e-122">Per i nuovi servizi Web, questo contenitore viene creato la prima volta in cui si accede al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="6802e-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="6802e-123">Per i servizi Web classici, è necessario creare il contenitore se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="6802e-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="6802e-124">Nel [portale di Azure](https://portal.azure.com) accedere all'account di archiviazione associato al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="6802e-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="6802e-125">In **Servizio BLOB** fare clic su **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="6802e-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="6802e-126">Se il contenitore **ml-diagnostics** non esiste, fare clic su **+ Contenitore**, assegnare al contenitore il nome "ml-diagnostics" e selezionare il **Tipo di accesso** "BLOB".</span><span class="sxs-lookup"><span data-stu-id="6802e-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="6802e-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6802e-127">Click **OK**.</span></span>

      ![Selezione del livello di registrazione](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="6802e-129">Per un servizio Web classico, anche il dashboard dei servizi Web in Machine Learning Studio ha un'opzione per abilitare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="6802e-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="6802e-130">Tuttavia, poiché la registrazione ora è gestita tramite il portale dei servizi Web, è necessario abilitarla tramite il portale come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6802e-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="6802e-131">Se la registrazione è già stata abilitata in Studio, nel portale dei servizi Web disabilitare la registrazione e abilitarla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="6802e-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="6802e-132">Effetti dell'abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="6802e-132">The effects of enabling logging</span></span>
<span data-ttu-id="6802e-133">Quando la registrazione è abilitata, tutti i dati di diagnostica e gli errori originati dall'endpoint del servizio Web vengono registrati nel contenitore BLOB **ml-diagnostics** nell'account di archiviazione di Azure collegato all'area di lavoro dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6802e-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="6802e-134">Tale contenitore contiene tutte le informazioni di diagnostica per tutti gli endpoint del servizio Web di tutte le aree di lavoro associate all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6802e-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="6802e-135">I registri possono essere visualizzati tramite uno dei diversi strumenti disponibili per l'esplorazione degli account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6802e-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="6802e-136">Il modo più semplice per visualizzarli è passare all'account di archiviazione nel portale di Azure e fare clic su **Contenitori** e quindi sul contenitore **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="6802e-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="6802e-137">Informazioni dettagliate dei BLOB dei log</span><span class="sxs-lookup"><span data-stu-id="6802e-137">Log blob detail information</span></span>
<span data-ttu-id="6802e-138">Ogni BLOB nel contenitore contiene le informazioni di diagnostica per una delle azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6802e-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="6802e-139">Un'esecuzione del metodo Batch-Execution</span><span class="sxs-lookup"><span data-stu-id="6802e-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="6802e-140">Un'esecuzione del metodo Request-Response</span><span class="sxs-lookup"><span data-stu-id="6802e-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="6802e-141">Inizializzazione di un contenitore Request-Response</span><span class="sxs-lookup"><span data-stu-id="6802e-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="6802e-142">Il nome di ogni BLOB riporta un prefisso nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="6802e-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="6802e-143">Dove _Tipo di log_ corrisponde a uno dei valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="6802e-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="6802e-144">o batch</span><span class="sxs-lookup"><span data-stu-id="6802e-144">batch</span></span>  
* <span data-ttu-id="6802e-145">punteggio/richieste</span><span class="sxs-lookup"><span data-stu-id="6802e-145">score/requests</span></span>  
* <span data-ttu-id="6802e-146">punteggio/init</span><span class="sxs-lookup"><span data-stu-id="6802e-146">score/init</span></span>  

