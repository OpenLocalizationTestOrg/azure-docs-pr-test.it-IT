---
title: Visualizzazione del cluster con Service Fabric Explorer | Microsoft Docs
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
ms.openlocfilehash: 789793a7f50170188d688881a9178546c3074018
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="1153c-103">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1153c-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="1153c-104">Service Fabric Explorer è uno strumento basato sul web per analizzare e gestire applicazioni e nodi in un cluster di Service Fabric di Azure.</span><span class="sxs-lookup"><span data-stu-id="1153c-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="1153c-105">Service Fabric Explorer è ospitato direttamente all'interno del cluster, pertanto è sempre disponibile indipendentemente da dove il cluster sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1153c-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="1153c-106">Esercitazione video</span><span class="sxs-lookup"><span data-stu-id="1153c-106">Video tutorial</span></span>

<span data-ttu-id="1153c-107">Per informazioni sull'uso di Service Fabric Explorer, vedere il video seguente di Microsoft Virtual Academy:</span><span class="sxs-lookup"><span data-stu-id="1153c-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-to-service-fabric-explorer"></a><span data-ttu-id="1153c-108">Connettersi a Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1153c-108">Connect to Service Fabric Explorer</span></span>
<span data-ttu-id="1153c-109">Se si sono seguite le istruzioni per [preparare l'ambiente di sviluppo](service-fabric-get-started.md), è possibile avviare Service Fabric Explorer nel cluster locale andando su http://localhost:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="1153c-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span></span>

## <a name="understand-the-service-fabric-explorer-layout"></a><span data-ttu-id="1153c-110">Comprendere il layout di Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1153c-110">Understand the Service Fabric Explorer layout</span></span>
<span data-ttu-id="1153c-111">È possibile spostarsi all'interno di Service Fabric Explorer seguendo la struttura ad albero a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1153c-111">You can navigate through Service Fabric Explorer by using the tree on the left.</span></span> <span data-ttu-id="1153c-112">Nella radice dell'albero, il dashboard del cluster fornisce una panoramica del cluster, inclusi un riepilogo dell'applicazione e l'integrità del nodo.</span><span class="sxs-lookup"><span data-stu-id="1153c-112">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Dashboard del cluster di Service Fabric Explorer][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a><span data-ttu-id="1153c-114">Visualizzare il layout del cluster</span><span class="sxs-lookup"><span data-stu-id="1153c-114">View the cluster's layout</span></span>
<span data-ttu-id="1153c-115">I nodi in un cluster di Service Fabric sono posizionati in una griglia bidimensionale di domini di errore e domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1153c-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="1153c-116">Questa posizione garantisce la disponibilità delle applicazioni in caso di errori hardware e aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1153c-116">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="1153c-117">È possibile visualizzare la disposizione del cluster corrente mediante la mappa del cluster.</span><span class="sxs-lookup"><span data-stu-id="1153c-117">You can view how the current cluster is laid out by using the cluster map.</span></span>

![Mappa del cluster di Service Fabric Explorer][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="1153c-119">Visualizzare applicazioni e servizi</span><span class="sxs-lookup"><span data-stu-id="1153c-119">View applications and services</span></span>
<span data-ttu-id="1153c-120">Il cluster contiene due sotto-alberi: uno per le applicazioni e un altro per i nodi.</span><span class="sxs-lookup"><span data-stu-id="1153c-120">The cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="1153c-121">È possibile usare la visualizzazione delle applicazioni per spostarsi nella gerarchia logica di Service Fabric: applicazioni, servizi, partizioni e repliche.</span><span class="sxs-lookup"><span data-stu-id="1153c-121">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="1153c-122">Nell'esempio seguente, l'applicazione **MyApp** è costituita da due servizi, **MyStatefulService** e **WebService**.</span><span class="sxs-lookup"><span data-stu-id="1153c-122">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="1153c-123">Poiché **MyStatefulService** è con stato, include una partizione con una replica primaria e due repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="1153c-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="1153c-124">Al contrario, il WebSvcService è senza stato e contiene una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="1153c-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Visualizzazione delle applicazioni di Service Fabric Explorer][sfx-application-tree]

<span data-ttu-id="1153c-126">A ogni livello della struttura ad albero, il riquadro principale mostra informazioni pertinenti all'elemento.</span><span class="sxs-lookup"><span data-stu-id="1153c-126">At each level of the tree, the main pane shows pertinent information about the item.</span></span> <span data-ttu-id="1153c-127">Ad esempio, è possibile visualizzare lo stato di integrità e la versione di un determinato servizio.</span><span class="sxs-lookup"><span data-stu-id="1153c-127">For example, you can see the health status and version for a particular service.</span></span>

![Riquadro essentials di Service Fabric Explorer][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a><span data-ttu-id="1153c-129">Visualizzare i nodi del cluster</span><span class="sxs-lookup"><span data-stu-id="1153c-129">View the cluster's nodes</span></span>
<span data-ttu-id="1153c-130">La visualizzazione dei nodi mostra il layout fisico del cluster.</span><span class="sxs-lookup"><span data-stu-id="1153c-130">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="1153c-131">Per un determinato nodo, è possibile esaminare le applicazioni con il codice distribuito in quel nodo.</span><span class="sxs-lookup"><span data-stu-id="1153c-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="1153c-132">In particolare, è possibile visualizzare le repliche attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1153c-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="1153c-133">Azioni</span><span class="sxs-lookup"><span data-stu-id="1153c-133">Actions</span></span>
<span data-ttu-id="1153c-134">Service Fabric Explorer offre un modo rapido per richiamare le azioni su nodi, applicazioni e servizi all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="1153c-134">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="1153c-135">Ad esempio, per eliminare un'istanza dell'applicazione, è sufficiente scegliere l'applicazione dall'albero a sinistra e quindi scegliere **Azioni** > **Elimina applicazione**.</span><span class="sxs-lookup"><span data-stu-id="1153c-135">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span></span>

![Eliminazione di un'applicazione in Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="1153c-137">È possibile eseguire le stesse azioni facendo clic sui puntini di sospensione accanto a ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="1153c-137">You can perform the same actions by clicking the ellipsis next to each element.</span></span>
>
>

<span data-ttu-id="1153c-138">La tabella seguente elenca le azioni disponibili per ogni entità:</span><span class="sxs-lookup"><span data-stu-id="1153c-138">The following table lists the actions available for each entity:</span></span>

| <span data-ttu-id="1153c-139">**Entità**</span><span class="sxs-lookup"><span data-stu-id="1153c-139">**Entity**</span></span> | <span data-ttu-id="1153c-140">**Azione**</span><span class="sxs-lookup"><span data-stu-id="1153c-140">**Action**</span></span> | <span data-ttu-id="1153c-141">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="1153c-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1153c-142">Tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="1153c-142">Application type</span></span> |<span data-ttu-id="1153c-143">Annullare il provisioning del tipo</span><span class="sxs-lookup"><span data-stu-id="1153c-143">Unprovision type</span></span> |<span data-ttu-id="1153c-144">Rimuove il pacchetto dell'applicazione dall'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="1153c-144">Removes the application package from the cluster's image store.</span></span> <span data-ttu-id="1153c-145">È necessario rimuovere prima tutte le applicazioni di quel tipo.</span><span class="sxs-lookup"><span data-stu-id="1153c-145">Requires all applications of that type to be removed first.</span></span> |
| <span data-ttu-id="1153c-146">Applicazione</span><span class="sxs-lookup"><span data-stu-id="1153c-146">Application</span></span> |<span data-ttu-id="1153c-147">Elimina applicazione</span><span class="sxs-lookup"><span data-stu-id="1153c-147">Delete Application</span></span> |<span data-ttu-id="1153c-148">Eliminare l'applicazione, inclusi tutti i servizi correlati e il relativo stato, se presente.</span><span class="sxs-lookup"><span data-stu-id="1153c-148">Delete the application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="1153c-149">Service</span><span class="sxs-lookup"><span data-stu-id="1153c-149">Service</span></span> |<span data-ttu-id="1153c-150">Eliminare il servizio</span><span class="sxs-lookup"><span data-stu-id="1153c-150">Delete Service</span></span> |<span data-ttu-id="1153c-151">Eliminare il servizio e il relativo stato (se presente).</span><span class="sxs-lookup"><span data-stu-id="1153c-151">Delete the service and its state (if any).</span></span> |
| <span data-ttu-id="1153c-152">Nodo</span><span class="sxs-lookup"><span data-stu-id="1153c-152">Node</span></span> |<span data-ttu-id="1153c-153">Activate</span><span class="sxs-lookup"><span data-stu-id="1153c-153">Activate</span></span> |<span data-ttu-id="1153c-154">Attivare il nodo.</span><span class="sxs-lookup"><span data-stu-id="1153c-154">Activate the node.</span></span> |
| <span data-ttu-id="1153c-155">Nodo</span><span class="sxs-lookup"><span data-stu-id="1153c-155">Node</span></span> | <span data-ttu-id="1153c-156">Disattivare (sospendere)</span><span class="sxs-lookup"><span data-stu-id="1153c-156">Deactivate (pause)</span></span> | <span data-ttu-id="1153c-157">Sospendere il nodo nello stato corrente.</span><span class="sxs-lookup"><span data-stu-id="1153c-157">Pause the node in its current state.</span></span> <span data-ttu-id="1153c-158">I servizi continueranno a essere eseguiti, tuttavia Service Fabric non sposterà in modo proattivo alcun elemento a meno che non sia necessario per impedire un'interruzione o un caso di incoerenza di dati.</span><span class="sxs-lookup"><span data-stu-id="1153c-158">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span></span> <span data-ttu-id="1153c-159">Questa azione viene in genere usata per abilitare i servizi di debug in un nodo specifico in modo da garantire che non si spostino durante l'ispezione.</span><span class="sxs-lookup"><span data-stu-id="1153c-159">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="1153c-160">Nodo</span><span class="sxs-lookup"><span data-stu-id="1153c-160">Node</span></span> | <span data-ttu-id="1153c-161">Disattivare (riavviare)</span><span class="sxs-lookup"><span data-stu-id="1153c-161">Deactivate (restart)</span></span> | <span data-ttu-id="1153c-162">Spostare tutti i servizi in memoria all'esterno di un nodo e chiudere i servizi permanenti in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="1153c-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="1153c-163">Questa azione viene in genere usata quando i processi host o i computer devono essere riavviati.</span><span class="sxs-lookup"><span data-stu-id="1153c-163">Typically used when the host processes or machine need to be restarted.</span></span> | |
| <span data-ttu-id="1153c-164">Nodo</span><span class="sxs-lookup"><span data-stu-id="1153c-164">Node</span></span> | <span data-ttu-id="1153c-165">Disattivare (rimuovere i dati)</span><span class="sxs-lookup"><span data-stu-id="1153c-165">Deactivate (remove data)</span></span> | <span data-ttu-id="1153c-166">Chiudere in modo sicuro tutti i servizi in esecuzione sul nodo dopo la creazione di un numero sufficiente di repliche riserva.</span><span class="sxs-lookup"><span data-stu-id="1153c-166">Safely close all services running on the node after building sufficient spare replicas.</span></span> <span data-ttu-id="1153c-167">Questa azione viene in genere usata quando un nodo (o almeno lo spazio di archiviazione correlato) viene reso improduttivo in modo permanente.</span><span class="sxs-lookup"><span data-stu-id="1153c-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="1153c-168">Nodo</span><span class="sxs-lookup"><span data-stu-id="1153c-168">Node</span></span> | <span data-ttu-id="1153c-169">Rimuovere lo stato del nodo</span><span class="sxs-lookup"><span data-stu-id="1153c-169">Remove node state</span></span> | <span data-ttu-id="1153c-170">Rimuovere le repliche di un nodo dal cluster.</span><span class="sxs-lookup"><span data-stu-id="1153c-170">Remove knowledge of a node's replicas from the cluster.</span></span> <span data-ttu-id="1153c-171">Questa azione viene in genere usata quando un nodo che ha già avuto esito negativo viene ritenuto non recuperabile.</span><span class="sxs-lookup"><span data-stu-id="1153c-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="1153c-172">Nodo</span><span class="sxs-lookup"><span data-stu-id="1153c-172">Node</span></span> | <span data-ttu-id="1153c-173">Riavvia</span><span class="sxs-lookup"><span data-stu-id="1153c-173">Restart</span></span> | <span data-ttu-id="1153c-174">Riavviare il nodo per simularne un errore.</span><span class="sxs-lookup"><span data-stu-id="1153c-174">Simulate a node failure by restarting the node.</span></span> <span data-ttu-id="1153c-175">Altre informazioni sono disponibili [qui](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="1153c-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="1153c-176">Poiché molte azioni sono distruttive, viene richiesto di confermare la finalità prima del completamento dell'azione.</span><span class="sxs-lookup"><span data-stu-id="1153c-176">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="1153c-177">Ogni azione eseguibile con Service Fabric Explorer può essere eseguita anche tramite PowerShell o un'API REST per abilitare l'automazione.</span><span class="sxs-lookup"><span data-stu-id="1153c-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span></span>
>
>

<span data-ttu-id="1153c-178">È inoltre possibile usare Service Fabric Explorer per creare istanze di applicazione per un tipo e una versione dell'applicazione specifici.</span><span class="sxs-lookup"><span data-stu-id="1153c-178">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span></span> <span data-ttu-id="1153c-179">Scegliere il tipo di applicazione nella visualizzazione albero, quindi fare clic sul collegamento **Create app instance** (Crea un'istanza dell'app).</span><span class="sxs-lookup"><span data-stu-id="1153c-179">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span></span>

![Creazione di un'istanza dell'applicazione in Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="1153c-181">Non è attualmente possibile impostare parametri per le istanze dell'applicazione create mediante Service Fabric Explorer,</span><span class="sxs-lookup"><span data-stu-id="1153c-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="1153c-182">per le quali vengono usati valori di parametro predefiniti.</span><span class="sxs-lookup"><span data-stu-id="1153c-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-to-a-remote-service-fabric-cluster"></a><span data-ttu-id="1153c-183">Connettersi a un cluster di Service Fabric remoto</span><span class="sxs-lookup"><span data-stu-id="1153c-183">Connect to a remote Service Fabric cluster</span></span>
<span data-ttu-id="1153c-184">Se si conosce l'endpoint del cluster e si dispone di autorizzazioni sufficienti, è possibile accedere a Service Fabric Explorer da qualsiasi browser.</span><span class="sxs-lookup"><span data-stu-id="1153c-184">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="1153c-185">Service Fabric Explorer è infatti un altro servizio in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="1153c-185">This is because Service Fabric Explorer is just another service that runs in the cluster.</span></span>

### <a name="discover-the-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="1153c-186">Scoprire l'endpoint di Service Fabric Explorer per un cluster remoto</span><span class="sxs-lookup"><span data-stu-id="1153c-186">Discover the Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="1153c-187">Per accedere a Service Fabric Explorer per un determinato cluster, inserire nel browser l'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="1153c-187">To reach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="1153c-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="1153c-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="1153c-189">Per i cluster di Azure, l'URL completo è disponibile anche nel riquadro Essentials del cluster del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1153c-189">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="1153c-190">Connettersi a un cluster sicuro</span><span class="sxs-lookup"><span data-stu-id="1153c-190">Connect to a secure cluster</span></span>
<span data-ttu-id="1153c-191">È possibile controllare l'accesso al cluster di Service Fabric con certificati oppure usando Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="1153c-191">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="1153c-192">Se si prova a connettersi a Service Fabric Explorer in un cluster sicuro, a seconda della configurazione del cluster, è necessario presentare un certificato client oppure eseguire l'accesso con AAD.</span><span class="sxs-lookup"><span data-stu-id="1153c-192">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1153c-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1153c-193">Next steps</span></span>
* [<span data-ttu-id="1153c-194">Panoramica di Testabilità</span><span class="sxs-lookup"><span data-stu-id="1153c-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="1153c-195">Gestione delle applicazioni di Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1153c-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="1153c-196">Distribuzione di un'applicazione di Infrastruttura di servizi mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="1153c-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
