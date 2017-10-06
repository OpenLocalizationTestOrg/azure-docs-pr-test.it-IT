---
title: un'area di lavoro di Machine Learning aaaManage | Documenti Microsoft
description: Gestire aree di lavoro di accesso tooAzure Machine Learning, distribuire e gestire i servizi web API ML
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
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="d47e5-103">Gestire un'area di lavoro di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d47e5-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="d47e5-104">Per informazioni sulla gestione dei servizi Web nel portale di servizi Web di Machine Learning hello, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d47e5-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="d47e5-105">È possibile gestire le aree di lavoro di Machine Learning nel portale di Azure entrambi hello o hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="d47e5-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="d47e5-106">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d47e5-106">Use hello Azure portal</span></span>

<span data-ttu-id="d47e5-107">toomanage un'area di lavoro hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="d47e5-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="d47e5-108">Accedi toohello [portale di Azure](https://portal.azure.com/) utilizzando un account di amministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d47e5-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="d47e5-109">Nella casella di ricerca hello nella parte superiore di hello di hello pagina, immettere "di machine learning aree di lavoro" e quindi selezionare **Machine Learning aree di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="d47e5-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="d47e5-110">Fare clic su area di lavoro hello desiderato toomanage.</span><span class="sxs-lookup"><span data-stu-id="d47e5-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="d47e5-111">Inoltre le informazioni di gestione risorse standard toohello e le opzioni disponibili, è possibile:</span><span class="sxs-lookup"><span data-stu-id="d47e5-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="d47e5-112">Visualizzazione **proprietà** : questa pagina consente di visualizzare informazioni su area di lavoro e risorse hello e sottoscrizione hello e gruppo di risorse collegato con l'area di lavoro, è possibile modificare.</span><span class="sxs-lookup"><span data-stu-id="d47e5-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="d47e5-113">**Risincronizzazione di archiviazione chiavi** -area di lavoro hello gestisce l'account di archiviazione chiavi toohello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="d47e5-114">Se i tasti di modifica degli account di archiviazione hello, quindi è possibile fare clic su **Resync chiavi** chiavi hello toosynchronize con area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="d47e5-115">servizi web di hello toomanage associati a questa area di lavoro, usare il portale di servizi Web di Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="d47e5-116">Vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md) per informazioni complete.</span><span class="sxs-lookup"><span data-stu-id="d47e5-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="d47e5-117">toodeploy o gestire i nuovi servizi web, è necessario disporre di un collaboratore o il ruolo di amministratore nel servizio web di hello sottoscrizione toowhich hello viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="d47e5-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="d47e5-118">Se si invita a un'altra macchina di tooa utente apprendimento dell'area di lavoro, è necessario assegnare loro ruolo di collaboratore o amministratore tooa sottoscrizione hello prima di poter distribuire o gestire i servizi web.</span><span class="sxs-lookup"><span data-stu-id="d47e5-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="d47e5-119">Per ulteriori informazioni sull'impostazione delle autorizzazioni di accesso, vedere [visualizzare le assegnazioni di accesso per utenti e gruppi nel portale di Azure - anteprima pubblica di hello](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="d47e5-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="d47e5-120">Utilizzare hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="d47e5-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="d47e5-121">Usa hello portale di Azure classico, è possibile gestire le aree di lavoro di Machine Learning per:</span><span class="sxs-lookup"><span data-stu-id="d47e5-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="d47e5-122">Monitorare l'utilizzo dell'area di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="d47e5-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="d47e5-123">Configurare hello dell'area di lavoro tooallow o negare l'accesso</span><span class="sxs-lookup"><span data-stu-id="d47e5-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="d47e5-124">Gestire i servizi Web creati nell'area di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="d47e5-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="d47e5-125">Elimina area di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="d47e5-125">Delete hello workspace</span></span>

<span data-ttu-id="d47e5-126">Inoltre, nella scheda dashboard hello fornisce una panoramica dell'uso dell'area di lavoro e una rapida panoramica delle informazioni dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d47e5-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="d47e5-127">In Azure Machine Learning Studio, su hello **servizi WEB** scheda, è possibile aggiungere, aggiornare o eliminare un servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d47e5-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="d47e5-128">area di lavoro nel portale di Azure classico hello toomanage:</span><span class="sxs-lookup"><span data-stu-id="d47e5-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="d47e5-129">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) utilizzo di Microsoft Azure account, utilizzare account hello associato hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d47e5-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="d47e5-130">Nel Pannello di servizi di Microsoft Azure hello, fare clic su **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="d47e5-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="d47e5-131">Fare clic su area di lavoro hello desiderato toomanage.</span><span class="sxs-lookup"><span data-stu-id="d47e5-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="d47e5-132">Nella pagina dell'area di lavoro Hello sono presenti tre schede:</span><span class="sxs-lookup"><span data-stu-id="d47e5-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="d47e5-133">**DASHBOARD** -consente l'utilizzo dell'area di lavoro tooview e informazioni</span><span class="sxs-lookup"><span data-stu-id="d47e5-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="d47e5-134">**Configura** -permette l'area di lavoro toohello toomanage access</span><span class="sxs-lookup"><span data-stu-id="d47e5-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="d47e5-135">**SERVIZI WEB** -consente i servizi Web toomanage che sono stati pubblicati dall'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d47e5-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="d47e5-136">utilizzo dell'area di lavoro hello toomonitor</span><span class="sxs-lookup"><span data-stu-id="d47e5-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="d47e5-137">Fare clic su hello **DASHBOARD** scheda.</span><span class="sxs-lookup"><span data-stu-id="d47e5-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="d47e5-138">Dal dashboard di hello, è possibile visualizzare l'utilizzo complessivo dell'area di lavoro e ottenere un riepilogo rapido delle informazioni dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d47e5-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="d47e5-139">Hello **calcolo** grafico mostra le risorse di calcolo hello in uso dall'area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="d47e5-140">È possibile modificare toodisplay visualizzazione hello relativo o assoluto valori ed è possibile modificare l'intervallo di tempo hello hello grafico visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d47e5-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="d47e5-141">**Panoramica sull'utilizzo** Visualizza l'archiviazione di Azure in uso dall'area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="d47e5-142">**Quick glance** visualizza un riepilogo delle informazioni dell'area di lavoro e collegamenti utili.</span><span class="sxs-lookup"><span data-stu-id="d47e5-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="d47e5-143">Hello **Accedi tooML Studio** collegamento consente di aprire Machine Learning Studio usando l'Account Microsoft è stato eseguito l'accesso in hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="d47e5-144">Hello Account Microsoft usato toosign in toohello toocreate portale Azure classico un'area di lavoro dispone automaticamente dell'autorizzazione tooopen area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d47e5-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="d47e5-145">tooopen un'area di lavoro, è necessario essere connessi con Account Microsoft che è stato definito come proprietario di hello dell'area di lavoro hello toohello oppure è necessario un invito dall'area di lavoro di hello proprietario toojoin hello tooreceive.</span><span class="sxs-lookup"><span data-stu-id="d47e5-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="d47e5-146">toogrant o sospendere l'accesso per gli utenti</span><span class="sxs-lookup"><span data-stu-id="d47e5-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="d47e5-147">Fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="d47e5-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="d47e5-148">Dalla scheda Configurazione hello è possibile:</span><span class="sxs-lookup"><span data-stu-id="d47e5-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="d47e5-149">Sospensione dell'area di lavoro di accesso toohello Machine Learning facendo clic su Nega.</span><span class="sxs-lookup"><span data-stu-id="d47e5-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="d47e5-150">Gli utenti non saranno in grado di tooopen dell'area di lavoro hello in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d47e5-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="d47e5-151">toorestore accedere, fare clic su Consenti.</span><span class="sxs-lookup"><span data-stu-id="d47e5-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="d47e5-152">toomanage altri account che dispongono di accesso dell'area di lavoro toohello in Machine Learning Studio, fare clic su **Accedi tooML Studio** in hello **DASHBOARD** scheda (vedere la nota che precedono hello relative  **Sign-in tooML Studio**).</span><span class="sxs-lookup"><span data-stu-id="d47e5-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="d47e5-153">Verrà visualizzata l'area di lavoro hello in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d47e5-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="d47e5-154">Da qui, fare clic su hello **impostazioni** scheda e quindi **utenti**.</span><span class="sxs-lookup"><span data-stu-id="d47e5-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="d47e5-155">È possibile fare clic su **INVITARE utenti più** toogive utenti accedere toohello area di lavoro, oppure selezionare un utente e fare clic su **rimuovere**.</span><span class="sxs-lookup"><span data-stu-id="d47e5-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="d47e5-156">servizi web toomanage nell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="d47e5-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="d47e5-157">Fare clic su hello **servizi WEB** scheda.</span><span class="sxs-lookup"><span data-stu-id="d47e5-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="d47e5-158">Verrà visualizzato un elenco di servizi Web pubblicati da questa area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d47e5-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="d47e5-159">toomanage un servizio web, fare clic su nome hello nella pagina del servizio Web di hello elenco tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="d47e5-160">Per un servizio Web possono essere definiti uno o più endpoint.</span><span class="sxs-lookup"><span data-stu-id="d47e5-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="d47e5-161">È possibile definire più endpoint nell'endpoint "Default" toohello di addizione.</span><span class="sxs-lookup"><span data-stu-id="d47e5-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="d47e5-162">tooadd hello endpoint, fare clic su **gestire endpoint** nella parte inferiore di hello del portale di servizi Web di Azure Machine Learning di hello dashboard tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="d47e5-163">toodelete un endpoint (è possibile eliminare endpoint "Predefinita" hello), fare clic sulla casella di controllo hello all'inizio di hello della riga di endpoint hello e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="d47e5-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="d47e5-164">Per rimuovere endpoint hello dal servizio Web hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d47e5-165">Se un'applicazione sta utilizzando l'endpoint del servizio web hello quando viene eliminato l'endpoint di hello, un'applicazione hello riceverà hello un errore successivo tentativo servizio hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d47e5-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="d47e5-166">Fare clic sul nome di un tooopen di endpoint servizio Web hello è.</span><span class="sxs-lookup"><span data-stu-id="d47e5-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="d47e5-167">Dal dashboard di hello, è possibile visualizzare l'utilizzo complessivo del servizio Web in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="d47e5-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="d47e5-168">È possibile selezionare tooview periodo hello dal menu a discesa periodo hello in alto a destra hello di grafici relativi all'utilizzo di hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="d47e5-169">dashboard di Hello Mostra hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d47e5-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="d47e5-170">**Le richieste nel tempo** Visualizza un grafico di passaggio del numero di hello di richieste su hello periodo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="d47e5-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="d47e5-171">Può aiutare a identificare se si verificano picchi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="d47e5-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="d47e5-172">**Le richieste di richiesta-risposta** Visualizza hello il numero totale di chiamate richiesta-risposta ricevuta dal servizio hello hello periodo di tempo selezionato e quanti di essi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="d47e5-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="d47e5-173">**Tempo medio di richiesta-risposta calcolo** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.</span><span class="sxs-lookup"><span data-stu-id="d47e5-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="d47e5-174">**Batch di richieste** hello Visualizza il numero totale di servizio hello richieste Batch ha ricevuto tramite hello periodo di tempo selezionato e quanti di essi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="d47e5-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="d47e5-175">**Processo latenza media** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.</span><span class="sxs-lookup"><span data-stu-id="d47e5-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="d47e5-176">**Errori** Visualizza hello aggregazione del numero di errori che si sono verificati nel servizio web toohello di chiamate.</span><span class="sxs-lookup"><span data-stu-id="d47e5-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="d47e5-177">**I costi dei servizi** hello spese per il piano di fatturazione hello associato hello servizio vengono visualizzate.</span><span class="sxs-lookup"><span data-stu-id="d47e5-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="d47e5-178">Dalla pagina Configura hello, è possibile aggiornare hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d47e5-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="d47e5-179">**Descrizione** consente tooenter una descrizione per il servizio Web hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="d47e5-180">La descrizione è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d47e5-180">Description is a required field.</span></span>
* <span data-ttu-id="d47e5-181">**Registrazione** consente errore tooenable o disabilitare la registrazione su endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="d47e5-182">Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="d47e5-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="d47e5-183">**Abilita dati di esempio** consente tooprovide dati di esempio che è possibile utilizzare il servizio di richiesta-risposta hello tootest.</span><span class="sxs-lookup"><span data-stu-id="d47e5-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="d47e5-184">Se si crea servizio web hello in Machine Learning Studio, i dati di esempio hello viene recuperati dal dati hello il tootrain utilizzato il modello.</span><span class="sxs-lookup"><span data-stu-id="d47e5-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="d47e5-185">Se è stato creato a livello di codice servizio hello, dati hello viene eseguiti da dati di esempio hello forniti come parte del pacchetto di hello JSON.</span><span class="sxs-lookup"><span data-stu-id="d47e5-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

