---
title: aaaVisualizing il cluster usando Service Fabric Explorer | Documenti Microsoft
description: "Service Fabric Explorer è uno strumento basato sul Web per analizzare e gestire nodi e applicazioni cloud in un cluster di Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="21b0b-103">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="21b0b-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="21b0b-104">Service Fabric Explorer è uno strumento basato sul web per analizzare e gestire applicazioni e nodi in un cluster di Service Fabric di Azure.</span><span class="sxs-lookup"><span data-stu-id="21b0b-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="21b0b-105">Service Fabric Explorer è ospitato direttamente all'interno di cluster hello, pertanto è sempre disponibile, indipendentemente dal fatto in cui il cluster è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="21b0b-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="21b0b-106">Esercitazione video</span><span class="sxs-lookup"><span data-stu-id="21b0b-106">Video tutorial</span></span>

<span data-ttu-id="21b0b-107">toolearn come toouse Service Fabric Explorer, guardare hello seguente video Microsoft Virtual Academy:</span><span class="sxs-lookup"><span data-stu-id="21b0b-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="21b0b-108">Connettersi tooService Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="21b0b-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="21b0b-109">Se si sono seguite le istruzioni di hello troppo[preparare l'ambiente di sviluppo](service-fabric-get-started.md), è possibile avviare Service Fabric Explorer sul cluster locale passando toohttp://localhost:19080 / Explorer.</span><span class="sxs-lookup"><span data-stu-id="21b0b-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="21b0b-110">Comprendere il layout di Service Fabric Explorer hello</span><span class="sxs-lookup"><span data-stu-id="21b0b-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="21b0b-111">È possibile spostarsi Service Fabric Explorer con struttura ad albero hello a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="21b0b-112">Nella radice dell'albero di hello hello dashboard cluster hello viene fornita una panoramica del cluster, incluso un riepilogo dell'applicazione e l'integrità del nodo.</span><span class="sxs-lookup"><span data-stu-id="21b0b-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Dashboard del cluster di Service Fabric Explorer][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="21b0b-114">Visualizzare il layout del cluster hello</span><span class="sxs-lookup"><span data-stu-id="21b0b-114">View hello cluster's layout</span></span>
<span data-ttu-id="21b0b-115">I nodi in un cluster di Service Fabric sono posizionati in una griglia bidimensionale di domini di errore e domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="21b0b-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="21b0b-116">Questa posizione assicura che le applicazioni rimangano disponibili in presenza di hello di errori hardware e gli aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21b0b-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="21b0b-117">È possibile visualizzare il layout cluster corrente hello utilizzando hello cluster mappa.</span><span class="sxs-lookup"><span data-stu-id="21b0b-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Mappa del cluster di Service Fabric Explorer][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="21b0b-119">Visualizzare applicazioni e servizi</span><span class="sxs-lookup"><span data-stu-id="21b0b-119">View applications and services</span></span>
<span data-ttu-id="21b0b-120">cluster Hello contiene due sottoalberi: uno per applicazioni e un altro per i nodi.</span><span class="sxs-lookup"><span data-stu-id="21b0b-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="21b0b-121">È possibile utilizzare hello applicazione vista toonavigate tramite la gerarchia logica dell'infrastruttura servizio: le applicazioni, servizi, partizioni e repliche.</span><span class="sxs-lookup"><span data-stu-id="21b0b-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="21b0b-122">Nel seguente esempio hello hello applicazione **MyApp** è costituito da due servizi, **MyStatefulService** e **WebService**.</span><span class="sxs-lookup"><span data-stu-id="21b0b-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="21b0b-123">Poiché **MyStatefulService** è con stato, include una partizione con una replica primaria e due repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="21b0b-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="21b0b-124">Al contrario, il WebSvcService è senza stato e contiene una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="21b0b-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Visualizzazione delle applicazioni di Service Fabric Explorer][sfx-application-tree]

<span data-ttu-id="21b0b-126">Ogni livello della struttura ad albero hello riquadro principale hello Mostra le informazioni pertinenti elemento hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="21b0b-127">Ad esempio, è possibile visualizzare lo stato di integrità hello e la versione per un determinato servizio.</span><span class="sxs-lookup"><span data-stu-id="21b0b-127">For example, you can see hello health status and version for a particular service.</span></span>

![Riquadro essentials di Service Fabric Explorer][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="21b0b-129">Visualizzare i nodi del cluster hello</span><span class="sxs-lookup"><span data-stu-id="21b0b-129">View hello cluster's nodes</span></span>
<span data-ttu-id="21b0b-130">visualizzazione del nodo Hello Mostra struttura fisica di hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="21b0b-131">Per un determinato nodo, è possibile esaminare le applicazioni con il codice distribuito in quel nodo.</span><span class="sxs-lookup"><span data-stu-id="21b0b-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="21b0b-132">In particolare, è possibile visualizzare le repliche attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="21b0b-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="21b0b-133">Azioni</span><span class="sxs-lookup"><span data-stu-id="21b0b-133">Actions</span></span>
<span data-ttu-id="21b0b-134">Service Fabric Explorer offre un modo rapido di tooinvoke azioni sui nodi, applicazioni e servizi all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="21b0b-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="21b0b-135">Ad esempio, toodelete un'istanza dell'applicazione, scegliere un'applicazione hello dalla struttura ad albero hello hello sinistra, quindi **azioni** > **Elimina applicazione**.</span><span class="sxs-lookup"><span data-stu-id="21b0b-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Eliminazione di un'applicazione in Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="21b0b-137">È possibile eseguire hello stesse azioni facendo clic su elemento tooeach successivo di hello i puntini di sospensione.</span><span class="sxs-lookup"><span data-stu-id="21b0b-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="21b0b-138">Hello nella tabella seguente sono elencate le azioni di hello disponibili per ogni entità:</span><span class="sxs-lookup"><span data-stu-id="21b0b-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="21b0b-139">**Entità**</span><span class="sxs-lookup"><span data-stu-id="21b0b-139">**Entity**</span></span> | <span data-ttu-id="21b0b-140">**Azione**</span><span class="sxs-lookup"><span data-stu-id="21b0b-140">**Action**</span></span> | <span data-ttu-id="21b0b-141">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="21b0b-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21b0b-142">Tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="21b0b-142">Application type</span></span> |<span data-ttu-id="21b0b-143">Annullare il provisioning del tipo</span><span class="sxs-lookup"><span data-stu-id="21b0b-143">Unprovision type</span></span> |<span data-ttu-id="21b0b-144">Rimuove il pacchetto di applicazione hello dall'archivio di immagini del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="21b0b-145">Richiede tutte le applicazioni di tale tipo di toobe rimossa prima.</span><span class="sxs-lookup"><span data-stu-id="21b0b-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="21b0b-146">Applicazione</span><span class="sxs-lookup"><span data-stu-id="21b0b-146">Application</span></span> |<span data-ttu-id="21b0b-147">Elimina applicazione</span><span class="sxs-lookup"><span data-stu-id="21b0b-147">Delete Application</span></span> |<span data-ttu-id="21b0b-148">Eliminare un'applicazione hello, inclusi tutti i relativi servizi e il relativo stato (se presente).</span><span class="sxs-lookup"><span data-stu-id="21b0b-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="21b0b-149">Service</span><span class="sxs-lookup"><span data-stu-id="21b0b-149">Service</span></span> |<span data-ttu-id="21b0b-150">Eliminare il servizio</span><span class="sxs-lookup"><span data-stu-id="21b0b-150">Delete Service</span></span> |<span data-ttu-id="21b0b-151">Eliminare il servizio hello e del relativo stato (se presente).</span><span class="sxs-lookup"><span data-stu-id="21b0b-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="21b0b-152">Nodo</span><span class="sxs-lookup"><span data-stu-id="21b0b-152">Node</span></span> |<span data-ttu-id="21b0b-153">Activate</span><span class="sxs-lookup"><span data-stu-id="21b0b-153">Activate</span></span> |<span data-ttu-id="21b0b-154">Attivare un nodo di hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-154">Activate hello node.</span></span> |
| <span data-ttu-id="21b0b-155">Nodo</span><span class="sxs-lookup"><span data-stu-id="21b0b-155">Node</span></span> | <span data-ttu-id="21b0b-156">Disattivare (sospendere)</span><span class="sxs-lookup"><span data-stu-id="21b0b-156">Deactivate (pause)</span></span> | <span data-ttu-id="21b0b-157">Sospendi nodo hello nello stato corrente.</span><span class="sxs-lookup"><span data-stu-id="21b0b-157">Pause hello node in its current state.</span></span> <span data-ttu-id="21b0b-158">Servizi continuino toorun ma Service Fabric non in modo proattivo spostare nulla su o off, a meno che non è necessario tooprevent un'interruzione del servizio o un'incoerenza dei dati.</span><span class="sxs-lookup"><span data-stu-id="21b0b-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="21b0b-159">Questa azione è in genere utilizzate tooenable debug dei servizi in un nodo specifico di tooensure che non passano durante il controllo.</span><span class="sxs-lookup"><span data-stu-id="21b0b-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="21b0b-160">Nodo</span><span class="sxs-lookup"><span data-stu-id="21b0b-160">Node</span></span> | <span data-ttu-id="21b0b-161">Disattivare (riavviare)</span><span class="sxs-lookup"><span data-stu-id="21b0b-161">Deactivate (restart)</span></span> | <span data-ttu-id="21b0b-162">Spostare tutti i servizi in memoria all'esterno di un nodo e chiudere i servizi permanenti in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="21b0b-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="21b0b-163">In genere utilizzato quando i processi host hello o toobe necessità computer riavviato.</span><span class="sxs-lookup"><span data-stu-id="21b0b-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="21b0b-164">Nodo</span><span class="sxs-lookup"><span data-stu-id="21b0b-164">Node</span></span> | <span data-ttu-id="21b0b-165">Disattivare (rimuovere i dati)</span><span class="sxs-lookup"><span data-stu-id="21b0b-165">Deactivate (remove data)</span></span> | <span data-ttu-id="21b0b-166">Chiudere tutti i servizi in esecuzione nel nodo di hello dopo la creazione di repliche riserva sufficienti.</span><span class="sxs-lookup"><span data-stu-id="21b0b-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="21b0b-167">Questa azione viene in genere usata quando un nodo (o almeno lo spazio di archiviazione correlato) viene reso improduttivo in modo permanente.</span><span class="sxs-lookup"><span data-stu-id="21b0b-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="21b0b-168">Nodo</span><span class="sxs-lookup"><span data-stu-id="21b0b-168">Node</span></span> | <span data-ttu-id="21b0b-169">Rimuovere lo stato del nodo</span><span class="sxs-lookup"><span data-stu-id="21b0b-169">Remove node state</span></span> | <span data-ttu-id="21b0b-170">Rimuovere conoscenza delle repliche di un nodo dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="21b0b-171">Questa azione viene in genere usata quando un nodo che ha già avuto esito negativo viene ritenuto non recuperabile.</span><span class="sxs-lookup"><span data-stu-id="21b0b-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="21b0b-172">Nodo</span><span class="sxs-lookup"><span data-stu-id="21b0b-172">Node</span></span> | <span data-ttu-id="21b0b-173">Riavvia</span><span class="sxs-lookup"><span data-stu-id="21b0b-173">Restart</span></span> | <span data-ttu-id="21b0b-174">Riavviare il nodo hello per simulare un errore di nodo.</span><span class="sxs-lookup"><span data-stu-id="21b0b-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="21b0b-175">Altre informazioni sono disponibili [qui](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="21b0b-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="21b0b-176">Poiché molte azioni sono distruttive, potrebbe essere richiesto tooconfirm lo scopo previsto prima che venga completato l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="21b0b-177">Ogni azione che può essere eseguita tramite Service Fabric Explorer può essere eseguite anche tramite PowerShell o un'API REST, tooenable automazione.</span><span class="sxs-lookup"><span data-stu-id="21b0b-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="21b0b-178">È anche possibile utilizzare le istanze dell'applicazione di Service Fabric Explorer toocreate per un tipo di applicazione specificata e la versione.</span><span class="sxs-lookup"><span data-stu-id="21b0b-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="21b0b-179">Scegliere il tipo di applicazione hello nella visualizzazione ad albero di hello, quindi fare clic su hello **Crea istanza app** versione toohello successivo collegamento desiderato nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Creazione di un'istanza dell'applicazione in Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="21b0b-181">Non è attualmente possibile impostare parametri per le istanze dell'applicazione create mediante Service Fabric Explorer,</span><span class="sxs-lookup"><span data-stu-id="21b0b-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="21b0b-182">per le quali vengono usati valori di parametro predefiniti.</span><span class="sxs-lookup"><span data-stu-id="21b0b-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="21b0b-183">Connettere il cluster di Service Fabric remoto tooa</span><span class="sxs-lookup"><span data-stu-id="21b0b-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="21b0b-184">Se si conosce l'endpoint del cluster hello e si dispone di autorizzazioni sufficienti per accedere Service Fabric Explorer da qualsiasi browser.</span><span class="sxs-lookup"><span data-stu-id="21b0b-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="21b0b-185">Infatti, Service Fabric Explorer è semplicemente un altro servizio che viene eseguito nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="21b0b-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="21b0b-186">Individuare l'endpoint di Service Fabric Explorer hello per un cluster remoto</span><span class="sxs-lookup"><span data-stu-id="21b0b-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="21b0b-187">tooreach Service Fabric Explorer per un determinato cluster, puntare il browser per:</span><span class="sxs-lookup"><span data-stu-id="21b0b-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="21b0b-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="21b0b-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="21b0b-189">Per i cluster di Azure, l'URL completo hello disponibile anche nel riquadro di essentials cluster hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="21b0b-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="21b0b-190">Connettere il cluster protetto di tooa</span><span class="sxs-lookup"><span data-stu-id="21b0b-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="21b0b-191">È possibile controllare client accesso tooyour cluster di Service Fabric con certificati o tramite Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="21b0b-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="21b0b-192">Se si tenta di tooconnect tooService Fabric Explorer in un cluster protetto, quindi a seconda della configurazione del cluster hello si essere toopresent richiesto un certificato client oppure accedi con Azure ad.</span><span class="sxs-lookup"><span data-stu-id="21b0b-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21b0b-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21b0b-193">Next steps</span></span>
* [<span data-ttu-id="21b0b-194">Panoramica di Testabilità</span><span class="sxs-lookup"><span data-stu-id="21b0b-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="21b0b-195">Gestione delle applicazioni di Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21b0b-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="21b0b-196">Distribuzione di un'applicazione di Infrastruttura di servizi mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="21b0b-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
