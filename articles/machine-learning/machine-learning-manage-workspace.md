---
title: Gestire un'area di lavoro di Machine Learning | Microsoft Docs
description: Gestione dell'accesso alle aree di lavoro di Azure Machine Learning e distribuzione e gestione dei servizi Web API ML
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 94800f51baf83311c33490cada5f991ff2101da9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="fb54d-103">Gestire un'area di lavoro di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fb54d-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="fb54d-104">Per informazioni sulla gestione dei servizi Web nel portale dei servizi Web di Machine Learning, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="fb54d-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="fb54d-105">È possibile gestire le aree di lavoro di Machine Learning nel portale di Azure o nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="fb54d-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="fb54d-106">Usare il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fb54d-106">Use the Azure portal</span></span>

<span data-ttu-id="fb54d-107">Per gestire un'area di lavoro nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="fb54d-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="fb54d-108">Accedere al [portale di Azure](https://portal.azure.com/) usando un account amministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb54d-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="fb54d-109">Nella casella di ricerca nella parte superiore della pagina immettere "aree di lavoro di Machine Learning" e quindi selezionare **Aree di lavoro di Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="fb54d-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="fb54d-110">Fare clic sull'area di lavoro da gestire.</span><span class="sxs-lookup"><span data-stu-id="fb54d-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="fb54d-111">Oltre alle informazioni e alle opzioni di gestione delle risorse standard disponibili, viene offerta la possibilità di effettuare le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="fb54d-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="fb54d-112">Visualizzare **Proprietà**: questa pagina visualizza informazioni relative all'area di lavoro e alle risorse e consente di modificare la sottoscrizione e il gruppo di risorse a cui è connessa l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="fb54d-113">**Risincronizzare le chiavi di archiviazione**: l'area di lavoro mantiene le chiavi per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fb54d-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="fb54d-114">Se le chiavi vengono modificate nell'account di archiviazione, è possibile fare clic su **Risincronizza le chiavi** per sincronizzarle con l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="fb54d-115">Per gestire i servizi Web associati all'area di lavoro, usare il portale dei servizi Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fb54d-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="fb54d-116">Per informazioni complete, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="fb54d-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="fb54d-117">Per distribuire o gestire nuovi servizi Web è necessario che all'utente sia assegnato un ruolo di collaboratore o di amministratore nella sottoscrizione in cui viene distribuito il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="fb54d-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="fb54d-118">Se si invita un altro utente in un'area di lavoro di Machine Learning, affinché possa distribuire o gestire servizi Web è prima necessario assegnargli un ruolo di collaboratore o di amministratore nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fb54d-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="fb54d-119">Per altre informazioni sull'impostazione delle autorizzazioni di accesso, vedere [Visualizzare le assegnazioni di accesso per utenti e gruppi nel Portale di Azure - Anteprima pubblica](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="fb54d-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="fb54d-120">Usare il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="fb54d-120">Use the Azure classic portal</span></span>

<span data-ttu-id="fb54d-121">Tramite il portale di Azure classico è possibile gestire le aree di lavoro di Machine Learning per:</span><span class="sxs-lookup"><span data-stu-id="fb54d-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="fb54d-122">Monitorare la modalità d'uso dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="fb54d-123">Configurare l'area di lavoro per consentire o negare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="fb54d-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="fb54d-124">Gestire i servizi Web creati nell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="fb54d-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="fb54d-125">Eliminare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-125">Delete the workspace</span></span>

<span data-ttu-id="fb54d-126">Nella scheda Dashboard viene inoltre fornita una panoramica dell'utilizzo dell'area di lavoro e un riepilogo rapido delle informazioni relative all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="fb54d-127">Nella scheda **WEB SERVICES** (SERVIZI WEB) di Azure Machine Learning Studio è possibile aggiungere, aggiornare o eliminare un servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fb54d-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="fb54d-128">Per gestire un'area di lavoro nel portale di Azure classico:</span><span class="sxs-lookup"><span data-stu-id="fb54d-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="fb54d-129">Accedere al [portale di Azure classico](https://manage.windowsazure.com/) usando l'account di Microsoft Azure associato alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb54d-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="fb54d-130">Nel riquadro dei servizi di Microsoft Azure fare clic su **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="fb54d-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="fb54d-131">Fare clic sull'area di lavoro da gestire.</span><span class="sxs-lookup"><span data-stu-id="fb54d-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="fb54d-132">La pagina dell'area di lavoro contiene tre schede:</span><span class="sxs-lookup"><span data-stu-id="fb54d-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="fb54d-133">**DASHBOARD** : permette di visualizzare i dati di utilizzo e le informazioni sull'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="fb54d-134">**CONFIGURE** : permette di gestire l'accesso all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="fb54d-135">**WEB SERVICES** (SERVIZI WEB): permette di gestire i servizi Web pubblicati da questa area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="fb54d-136">Per monitorare la modalità d'uso dell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="fb54d-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="fb54d-137">Fare clic sulla scheda **DASHBOARD** .</span><span class="sxs-lookup"><span data-stu-id="fb54d-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="fb54d-138">Dal dashboard è possibile visualizzare l'utilizzo complessivo dell'area di lavoro e ottenere un riepilogo rapido delle informazioni dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="fb54d-139">Il grafico **COMPUTE** mostra le risorse di calcolo in uso nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="fb54d-140">È possibile modificare la visualizzazione per mostrare i valori relativi o assoluti, nonché cambiare l'intervallo di tempo visualizzato nel grafico.</span><span class="sxs-lookup"><span data-stu-id="fb54d-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="fb54d-141">**Usage overview** mostra l'archiviazione di Azure attualmente in uso nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="fb54d-142">**Quick glance** visualizza un riepilogo delle informazioni dell'area di lavoro e collegamenti utili.</span><span class="sxs-lookup"><span data-stu-id="fb54d-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="fb54d-143">Il link all’ **Accesso a ML Studio** consente di aprire Machine Learning Studio usando l'account Microsoft con cui è stato eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="fb54d-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="fb54d-144">L'account Microsoft usato per accedere al portale di Azure classico per creare un'area di lavoro non è automaticamente autorizzato ad aprire tale area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="fb54d-145">Per aprire un'area di lavoro, è necessario essere connessi con l'account Microsoft definito come proprietario dell'area di lavoro oppure ricevere un invito dal proprietario per partecipare all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="fb54d-146">Per concedere o sospendere l'accesso agli utenti</span><span class="sxs-lookup"><span data-stu-id="fb54d-146">To grant or suspend access for users</span></span>
<span data-ttu-id="fb54d-147">Fare clic sulla scheda **CONFIGURE** .</span><span class="sxs-lookup"><span data-stu-id="fb54d-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="fb54d-148">Dalla scheda di configurazione è possibile:</span><span class="sxs-lookup"><span data-stu-id="fb54d-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="fb54d-149">Sospendere l'accesso all'area di lavoro di Machine Learning facendo clic su DENY.</span><span class="sxs-lookup"><span data-stu-id="fb54d-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="fb54d-150">Gli utenti non saranno più in grado di aprire l'area di lavoro in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fb54d-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="fb54d-151">Per ripristinare l'accesso, fare clic su ALLOW.</span><span class="sxs-lookup"><span data-stu-id="fb54d-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="fb54d-152">Per gestire account aggiuntivi che hanno accesso all'area di lavoro in Machine Learning Studio, fare clic su **Accedi a ML Studio** nella scheda **DASHBOARD** (vedere la nota precedente relativa al comando **Accedi a ML Studio**).</span><span class="sxs-lookup"><span data-stu-id="fb54d-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="fb54d-153">Verrà aperta l'area di lavoro in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fb54d-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="fb54d-154">A questo punto, fare clic sulla scheda **SETTINGS** (IMPOSTAZIONI) e quindi su **USERS** (UTENTI).</span><span class="sxs-lookup"><span data-stu-id="fb54d-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="fb54d-155">È possibile fare clic su **INVITE MORE USERS** (INVITA ALTRI UTENTI) per concedere agli utenti l'accesso all'area di lavoro oppure selezionare un utente e fare clic su **REMOVE** (RIMUOVI).</span><span class="sxs-lookup"><span data-stu-id="fb54d-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="fb54d-156">Per gestire i servizi Web in questa area di lavoro</span><span class="sxs-lookup"><span data-stu-id="fb54d-156">To manage web services in this workspace</span></span>
<span data-ttu-id="fb54d-157">Fare clic sulla scheda **WEB SERVICES** .</span><span class="sxs-lookup"><span data-stu-id="fb54d-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="fb54d-158">Verrà visualizzato un elenco di servizi Web pubblicati da questa area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb54d-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="fb54d-159">Per gestire un servizio Web, fare clic sul nome nell'elenco per aprire la pagina corrispondente.</span><span class="sxs-lookup"><span data-stu-id="fb54d-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="fb54d-160">Per un servizio Web possono essere definiti uno o più endpoint.</span><span class="sxs-lookup"><span data-stu-id="fb54d-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="fb54d-161">È possibile definire altri endpoint oltre a quelli di "Default".</span><span class="sxs-lookup"><span data-stu-id="fb54d-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="fb54d-162">Per aggiungere l'endpoint, fare clic su **Manage Endpoints** (Gestisci endpoint) nella parte inferiore del dashboard per aprire il portale dei servizi Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fb54d-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="fb54d-163">Per eliminare un endpoint, escluso l'endpoint "Default" che non può essere eliminato, fare clic nella casella di controllo all'inizio della riga dell'endpoint e quindi su **DELETE** (ELIMINA).</span><span class="sxs-lookup"><span data-stu-id="fb54d-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="fb54d-164">L'endpoint verrà rimosso dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="fb54d-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="fb54d-165">Se in un'applicazione è in uso l'endpoint di servizio Web quando questo viene eliminato, al successivo tentativo di accesso al servizio da parte dell'applicazione verrà visualizzato un errore .</span><span class="sxs-lookup"><span data-stu-id="fb54d-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="fb54d-166">Fare clic sul nome di un endpoint di servizio Web per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="fb54d-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="fb54d-167">Nel dashboard è possibile visualizzare l'utilizzo complessivo del servizio Web in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="fb54d-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="fb54d-168">È possibile selezionare il periodo da visualizzare dal menu a discesa Periodo in alto a destra dei grafici di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="fb54d-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="fb54d-169">Il dashboard visualizza le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb54d-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="fb54d-170">**Requests Over Time** (Richieste nel tempo) visualizza un grafico con il numero di richieste nel periodo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="fb54d-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="fb54d-171">Può aiutare a identificare se si verificano picchi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="fb54d-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="fb54d-172">**Request-Response Requests** (Richieste richiesta-risposta) visualizza il numero totale di chiamate di richiesta-risposta ricevute dal servizio nel periodo di tempo selezionato e il numero di richieste con errore.</span><span class="sxs-lookup"><span data-stu-id="fb54d-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="fb54d-173">**Average Request-Response Compute Time** (Tempo medio di calcolo richiesta-risposta) visualizza una media del tempo necessario per eseguire le richieste ricevute.</span><span class="sxs-lookup"><span data-stu-id="fb54d-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="fb54d-174">**Batch Requests** (Richieste batch) visualizza il numero totale di richieste batch ricevute dal servizio nel periodo di tempo selezionato e il numero di richieste con errore.</span><span class="sxs-lookup"><span data-stu-id="fb54d-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="fb54d-175">**Average Job Latency** (Latenza processo media) visualizza una media del tempo necessario per eseguire le richieste ricevute.</span><span class="sxs-lookup"><span data-stu-id="fb54d-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="fb54d-176">**Errors** (Errori) visualizza il numero complessivo di errori che si sono verificati nelle chiamate al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="fb54d-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="fb54d-177">**Services Costs** (Costi servizi) visualizza le spese per il piano di fatturazione associato al servizio.</span><span class="sxs-lookup"><span data-stu-id="fb54d-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="fb54d-178">Dalla pagina di configurazione è possibile aggiornare le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb54d-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="fb54d-179">**Description** (Descrizione) consente di immettere una descrizione per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="fb54d-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="fb54d-180">La descrizione è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="fb54d-180">Description is a required field.</span></span>
* <span data-ttu-id="fb54d-181">**Logging** (Registrazione) consente di abilitare o disabilitare la registrazione nell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="fb54d-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="fb54d-182">Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="fb54d-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="fb54d-183">**Enable Sample data** (Abilita dati di esempio) consente di fornire dati di esempio che è possibile usare per testare il servizio di richiesta-risposta.</span><span class="sxs-lookup"><span data-stu-id="fb54d-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="fb54d-184">Se il servizio Web è stato creato in Machine Learning Studio, i dati di esempio vengono prelevati dai dati usati per il training del modello.</span><span class="sxs-lookup"><span data-stu-id="fb54d-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="fb54d-185">Se il servizio è stato creato a livello di codice, i dati vengono ricavati dai dati di esempio forniti come parte del pacchetto JSON.</span><span class="sxs-lookup"><span data-stu-id="fb54d-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

