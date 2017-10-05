---
title: "Come visualizzare l'integrità aggregata delle entità di Azure Service Fabric | Microsoft Docs"
description: "Descrive come eseguire una query dell'integrità aggregata delle entità di Azure Service Fabric, come visualizzarla e come valutarla con query di integrità e query generali."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: b97972b1bdc28a17fb9c3a0e997738f5bd0b5d15
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="22aa2-103">Come visualizzare i report sull'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="22aa2-103">View Service Fabric health reports</span></span>
<span data-ttu-id="22aa2-104">Azure Service Fabric introduce un [modello di integrità](service-fabric-health-introduction.md) con entità di integrità per le quali i componenti di sistema e i watchdog possono creare report sulle condizioni locali sottoposte a monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="22aa2-105">L' [archivio integrità](service-fabric-health-introduction.md#health-store) aggrega tutti i dati di integrità per determinare se le entità sono integre.</span><span class="sxs-lookup"><span data-stu-id="22aa2-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="22aa2-106">Il cluster viene popolato automaticamente con report sull'integrità inviati dai componenti di sistema.</span><span class="sxs-lookup"><span data-stu-id="22aa2-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="22aa2-107">Per altre informazioni, vedere [Usare i report sull'integrità del sistema per la risoluzione dei problemi](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="22aa2-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="22aa2-108">Service Fabric offre diversi modi per ottenere l'integrità aggregata delle entità:</span><span class="sxs-lookup"><span data-stu-id="22aa2-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="22aa2-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) o altri strumenti di visualizzazione</span><span class="sxs-lookup"><span data-stu-id="22aa2-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="22aa2-110">Query di integrità (tramite PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="22aa2-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="22aa2-111">Query generali che restituiscono un elenco di entità per le quali l'integrità costituisce una proprietà (tramite PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="22aa2-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="22aa2-112">Per illustrare queste opzioni, si userà un cluster locale con cinque nodi e l'[applicazione fabric:/WordCount](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="22aa2-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="22aa2-113">L'applicazione **fabric:/WordCount** contiene due servizi predefiniti, un servizio con stato di tipo `WordCountServiceType` e un servizio senza stato di tipo `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="22aa2-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="22aa2-114">L'oggetto `ApplicationManifest.xml` è stato modificato per richiedere sette repliche di destinazione per il servizio con stato e una partizione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="22aa2-115">Poiché ci sono solo cinque nodi nel cluster, i componenti di sistema segnalano un avviso nella partizione del servizio perché è al di sotto del numero previsto.</span><span class="sxs-lookup"><span data-stu-id="22aa2-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="22aa2-116">Integrità in Esplora Infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="22aa2-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="22aa2-117">Esplora Infrastruttura di servizi fornisce una panoramica visiva del cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="22aa2-118">Nell'immagine seguente è possibile osservare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="22aa2-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="22aa2-119">L'applicazione **fabric:/WordCount** è di colore rosso (condizione di errore), perché per questa applicazione è stato segnalato un evento di errore da **MyWatchdog** per la proprietà **Availability**.</span><span class="sxs-lookup"><span data-stu-id="22aa2-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="22aa2-120">Uno dei servizi di questa applicazione, **fabric:/WordCount/WordCountService** è di colore giallo (condizione di avviso).</span><span class="sxs-lookup"><span data-stu-id="22aa2-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="22aa2-121">Il servizio è configurato con sette repliche e il cluster ha cinque nodi, quindi due repliche non possono essere posizionate.</span><span class="sxs-lookup"><span data-stu-id="22aa2-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="22aa2-122">Anche se qui non è illustrata, la partizione del servizio è di colore giallo a causa di un report di sistema di `System.FM` che indica `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="22aa2-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="22aa2-123">La partizione gialla avvia il servizio giallo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="22aa2-124">Il cluster è di colore rosso perché è rossa anche l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="22aa2-125">La valutazione usa criteri predefiniti del manifesto del cluster dal manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="22aa2-126">Questi sono criteri rigorosi e non tollerano errori.</span><span class="sxs-lookup"><span data-stu-id="22aa2-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="22aa2-127">Visualizzazione del cluster con Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="22aa2-127">View of the cluster with Service Fabric Explorer:</span></span>

![Visualizzazione del cluster con Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="22aa2-129">Ulteriori informazioni su [Esplora Infrastruttura di servizi](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="22aa2-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="22aa2-130">Query relative all’integrità</span><span class="sxs-lookup"><span data-stu-id="22aa2-130">Health queries</span></span>
<span data-ttu-id="22aa2-131">Infrastruttura di servizi espone le query relative all’integrità per ognuno dei [tipi di entità](service-fabric-health-introduction.md#health-entities-and-hierarchy)supportati.</span><span class="sxs-lookup"><span data-stu-id="22aa2-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="22aa2-132">È possibile accedervi tramite l'API, usando i metodi in [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), i cmdlet di PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="22aa2-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="22aa2-133">Queste query restituiscono informazioni complete sull'integrità per l'entità, come lo stato aggregato dell'integrità, gli eventi di integrità dell'entità, gli stati di integrità degli elementi figlio, se applicabili, le valutazioni di non integrità (quando l'entità non è integra) e le statistiche sull'integrità degli elementi figlio, quando applicabili.</span><span class="sxs-lookup"><span data-stu-id="22aa2-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="22aa2-134">Un'entità integra viene restituita quando è popolata completamente nell'archivio integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="22aa2-135">L'entità deve essere attiva (non eliminata) e avere un report di sistema.</span><span class="sxs-lookup"><span data-stu-id="22aa2-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="22aa2-136">Anche le entità padre nella catena della gerarchia devono avere report di sistema.</span><span class="sxs-lookup"><span data-stu-id="22aa2-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="22aa2-137">Se una di queste condizioni non viene soddisfatta, le query relative all'integrità restituiscono un oggetto [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) con [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` che illustra il motivo per cui l'entità non viene restituita.</span><span class="sxs-lookup"><span data-stu-id="22aa2-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="22aa2-138">Le query di integrità richiedono il passaggio nell'identificatore dell'entità, che dipende dal tipo di entità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="22aa2-139">Le query accettano parametri dei criteri di integrità facoltativi.</span><span class="sxs-lookup"><span data-stu-id="22aa2-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="22aa2-140">Se non sono specificati, per la valutazione vengono usati i [criteri di integrità](service-fabric-health-introduction.md#health-policies) dal manifesto del cluster o dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="22aa2-141">Se i manifesti non contengono una definizione per i criteri di integrità, per la valutazione vengono usati i criteri di integrità predefiniti.</span><span class="sxs-lookup"><span data-stu-id="22aa2-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="22aa2-142">I criteri di integrità predefiniti non tollerano errori.</span><span class="sxs-lookup"><span data-stu-id="22aa2-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="22aa2-143">Le query accettano anche filtri per restituire solo elementi figlio o eventi parziali, quelli che rispettano i filtri specificati.</span><span class="sxs-lookup"><span data-stu-id="22aa2-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="22aa2-144">Un altro filtro consente di escludere le statistiche relative agli elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="22aa2-145">Sul lato server vengono applicati i filtri di output, in modo che la dimensione della risposta al messaggio venga ridotta.</span><span class="sxs-lookup"><span data-stu-id="22aa2-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="22aa2-146">È consigliabile usare i filtri di output per limitare i dati restituiti, invece di applicare filtri sul lato client.</span><span class="sxs-lookup"><span data-stu-id="22aa2-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="22aa2-147">L'integrità di un'entità contiene quanto segue:</span><span class="sxs-lookup"><span data-stu-id="22aa2-147">An entity's health contains:</span></span>

* <span data-ttu-id="22aa2-148">Lo stato di integrità aggregato dell'entità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="22aa2-149">Viene calcolato dall'archivio integrità in base ai report sull'integrità dell'entità, gli stati di integrità degli elementi figlio, se applicabili, e i criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="22aa2-150">Per altre informazioni, vedere [valutazione dell'integrità dell'entità](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="22aa2-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="22aa2-151">Gli eventi di integrità dell'entità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-151">The health events on the entity.</span></span>
* <span data-ttu-id="22aa2-152">La raccolta degli stati di integrità di tutti gli elementi figlio per le entità che possono avere elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="22aa2-153">Gli stati di integrità contengono l'identificatore dell'entità e lo stato di integrità aggregato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="22aa2-154">Per ottenere l'integrità completa per un elemento figlio, chiamare l'integrità di query per il tipo di entità figlio e passare l'identificatore dell'elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="22aa2-155">Le valutazioni non integre che puntano al report che ha attivato lo stato dell'entità, se l'entità non è integra.</span><span class="sxs-lookup"><span data-stu-id="22aa2-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="22aa2-156">Le valutazioni sono ricorsive e contengono le valutazioni di integrità degli elementi figlio che hanno attivato lo stato di integrità corrente.</span><span class="sxs-lookup"><span data-stu-id="22aa2-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="22aa2-157">Un watchdog ha segnalato ad esempio un errore in una replica.</span><span class="sxs-lookup"><span data-stu-id="22aa2-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="22aa2-158">L'integrità dell'applicazione presenta una valutazione di non integrità a causa di un servizio non integro. Il servizio non è integro a causa di un errore di una partizione. La partizione non è integra a causa di un errore di una replica. La replica non è integra a causa del report di integrità di errore del watchdog.</span><span class="sxs-lookup"><span data-stu-id="22aa2-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="22aa2-159">Le statistiche di integrità per tutti i tipi figlio delle entità che hanno elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="22aa2-160">L'integrità del cluster mostra ad esempio il numero totale di applicazioni, servizi, partizioni, repliche ed entità distribuite nel cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="22aa2-161">L'integrità del servizio mostra il numero totale di partizioni e repliche nel servizio specificato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="22aa2-162">Get cluster health</span><span class="sxs-lookup"><span data-stu-id="22aa2-162">Get cluster health</span></span>
<span data-ttu-id="22aa2-163">Restituisce l'integrità dell'entità cluster e contiene gli stati di integrità di applicazioni e nodi, elementi figlio del cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="22aa2-164">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-164">Input:</span></span>

* <span data-ttu-id="22aa2-165">[Facoltativo] Criteri di integrità del cluster usati per valutare i nodi e gli eventi del cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="22aa2-166">[Facoltativo] Mappa dei criteri di integrità dell'applicazione con criteri di integrità usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="22aa2-167">[Facoltativo] Filtri per eventi, nodi e applicazioni che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-168">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi, i nodi e le applicazioni, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="22aa2-169">[Facoltativo] Filtrare per escludere le statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="22aa2-170">[Facoltativo] Filtrare per includere le statistiche di integrità di fabric:/System.</span><span class="sxs-lookup"><span data-stu-id="22aa2-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="22aa2-171">Applicabile solo quando le statistiche di integrità non sono escluse.</span><span class="sxs-lookup"><span data-stu-id="22aa2-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="22aa2-172">Per impostazione predefinita, le statistiche di integrità includono solo le statistiche per le applicazioni utente e non per l'applicazione System.</span><span class="sxs-lookup"><span data-stu-id="22aa2-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-173">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-173">API</span></span>
<span data-ttu-id="22aa2-174">Per ottenere l'integrità del cluster, creare un oggetto `FabricClient` e chiamare il metodo [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) sul relativo **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="22aa2-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="22aa2-175">La chiamata seguente permette di ottenere l'integrità del cluster:</span><span class="sxs-lookup"><span data-stu-id="22aa2-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="22aa2-176">Il codice seguente permette di ottenere l'integrità del cluster usando criteri di integrità del cluster personalizzati e filtri per nodi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="22aa2-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="22aa2-177">Specifica che le statistiche di integrità includono le statistiche di fabric:/System.</span><span class="sxs-lookup"><span data-stu-id="22aa2-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="22aa2-178">Crea un oggetto [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), che contiene le informazioni di input.</span><span class="sxs-lookup"><span data-stu-id="22aa2-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="22aa2-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-179">PowerShell</span></span>
<span data-ttu-id="22aa2-180">Il cmdlet per ottenere l'integrità del cluster è [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="22aa2-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="22aa2-181">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="22aa2-182">Lo stato del cluster è costituito da cinque nodi, dall'applicazione di sistema e da fabric:/WordCount, configurati come descritto.</span><span class="sxs-lookup"><span data-stu-id="22aa2-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="22aa2-183">I cmdlet seguenti ottengono l'integrità del cluster con criteri di integrità predefiniti.</span><span class="sxs-lookup"><span data-stu-id="22aa2-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="22aa2-184">Lo stato di integrità aggregato è di tipo avviso, perché per l'applicazione fabric:/WordCount è stato generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="22aa2-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="22aa2-185">Notare come le valutazioni non integre forniscano dettagli sulle condizioni che hanno attivato lo stato di integrità aggregato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="22aa2-186">Il cmdlet PowerShell seguente ottiene lo stato di integrità del cluster con i criteri dell'applicazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="22aa2-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="22aa2-187">Filtra i risultati per ottenere solo le applicazioni e i nodi con stato di errore o avviso.</span><span class="sxs-lookup"><span data-stu-id="22aa2-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="22aa2-188">Di conseguenza, non vengono restituiti nodi, perché sono tutti integri.</span><span class="sxs-lookup"><span data-stu-id="22aa2-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="22aa2-189">Solo l'applicazione fabric:/WordCount rispetta il filtro delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="22aa2-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="22aa2-190">Poiché i criteri personalizzati specificano di considerare gli avvisi come errori per l'applicazione fabric:/WordCount, questa viene valutata in stato di errore e lo stesso accade per il cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="22aa2-191">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-191">REST</span></span>
<span data-ttu-id="22aa2-192">Per ottenere l'integrità di un cluster è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="22aa2-193">Get node health</span><span class="sxs-lookup"><span data-stu-id="22aa2-193">Get node health</span></span>
<span data-ttu-id="22aa2-194">Restituisce l'integrità di un'entità nodo e contiene gli eventi di integrità segnalati sul nodo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="22aa2-195">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-195">Input:</span></span>

* <span data-ttu-id="22aa2-196">[Obbligatorio] Nome del nodo che identifica il nodo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="22aa2-197">[Facoltativo] Impostazioni dei criteri di integrità usate per valutare l'integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="22aa2-198">[Facoltativo] Filtri per gli eventi che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-199">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-200">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-200">API</span></span>
<span data-ttu-id="22aa2-201">Per ottenere l'integrità del nodo tramite l'API, creare un oggetto `FabricClient` e chiamare il metodo [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) sul relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="22aa2-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="22aa2-202">Il codice seguente permette di ottenere l'integrità del nodo per il nome del nodo specificato:</span><span class="sxs-lookup"><span data-stu-id="22aa2-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="22aa2-203">Il codice seguente permette di ottenere l'integrità del nodo per il nome del nodo specificato e passa un filtro eventi e criteri personalizzati tramite [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="22aa2-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="22aa2-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-204">PowerShell</span></span>
<span data-ttu-id="22aa2-205">Il cmdlet per ottenere l'integrità del nodo è [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="22aa2-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="22aa2-206">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="22aa2-207">I cmdlet seguenti ottengono l'integrità del nodo con criteri di integrità predefiniti:</span><span class="sxs-lookup"><span data-stu-id="22aa2-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="22aa2-208">Il cmdlet seguente ottiene lo stato di tutti i nodi del cluster:</span><span class="sxs-lookup"><span data-stu-id="22aa2-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="22aa2-209">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-209">REST</span></span>
<span data-ttu-id="22aa2-210">Per ottenere l'integrità di un nodo è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="22aa2-211">Ottieni lo stato dell'integrità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="22aa2-211">Get application health</span></span>
<span data-ttu-id="22aa2-212">Restituisce lo stato di un'entità applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-212">Returns the health of an application entity.</span></span> <span data-ttu-id="22aa2-213">Contiene gli stati di integrità dell'applicazione distribuita e gli elementi figlio del servizio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="22aa2-214">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-214">Input:</span></span>

* <span data-ttu-id="22aa2-215">[Obbligatorio] Nome dell'applicazione (URI) che identifica l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="22aa2-216">[Facoltativo] Criteri di integrità dell'applicazione usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="22aa2-217">[Facoltativo] Filtri per eventi, servizi e applicazioni distribuite che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-218">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi, i servizi e le applicazioni distribuite, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="22aa2-219">[Facoltativo] Filtrare per escludere le statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="22aa2-220">Se non specificato, le statistiche di integrità includono il numero di stati ok, di avviso e di errore per tutti gli elementi figlio dell'applicazione: servizi, partizioni, repliche, applicazioni distribuite e pacchetti del servizio distribuiti.</span><span class="sxs-lookup"><span data-stu-id="22aa2-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-221">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-221">API</span></span>
<span data-ttu-id="22aa2-222">Per ottenere l'integrità dell'applicazione, creare un oggetto `FabricClient` e chiamare il metodo [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) sul relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="22aa2-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="22aa2-223">Il codice seguente permette di ottenere l'integrità dell'applicazione per il nome dell'applicazione (URI) specificato:</span><span class="sxs-lookup"><span data-stu-id="22aa2-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="22aa2-224">Il codice seguente permette di ottenere l'integrità dell'applicazione per il nome dell'applicazione (URI) specificato, con filtri e criteri personalizzati specificati tramite [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="22aa2-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="22aa2-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-225">PowerShell</span></span>
<span data-ttu-id="22aa2-226">Il cmdlet per ottenere l'integrità dell'applicazione è [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="22aa2-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="22aa2-227">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="22aa2-228">Il cmdlet seguente restituisce l'integrità dell'applicazione **fabric:/WordCount** :</span><span class="sxs-lookup"><span data-stu-id="22aa2-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="22aa2-229">Il cmdlet PowerShell seguente passa i criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="22aa2-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="22aa2-230">Filtra anche gli elementi figlio e gli eventi.</span><span class="sxs-lookup"><span data-stu-id="22aa2-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="22aa2-231">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-231">REST</span></span>
<span data-ttu-id="22aa2-232">Per ottenere l'integrità di un'applicazione è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="22aa2-233">Get service health</span><span class="sxs-lookup"><span data-stu-id="22aa2-233">Get service health</span></span>
<span data-ttu-id="22aa2-234">Restituisce lo stato di un'entità di servizio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-234">Returns the health of a service entity.</span></span> <span data-ttu-id="22aa2-235">Contiene gli stati di integrità della partizione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-235">It contains the partition health states.</span></span> <span data-ttu-id="22aa2-236">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-236">Input:</span></span>

* <span data-ttu-id="22aa2-237">[Obbligatorio] Nome del servizio (URI) che identifica il servizio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="22aa2-238">[Facoltativo] Criteri di integrità dell'applicazione usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="22aa2-239">[Facoltativo] Filtri per eventi e partizioni che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-240">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi e tutte le partizioni, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="22aa2-241">[Facoltativo] Filtrare per escludere le statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="22aa2-242">Se non specificato, le statistiche di integrità mostrano il numero di stati ok, di avviso e di errore per tutte le partizioni e le repliche del servizio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-243">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-243">API</span></span>
<span data-ttu-id="22aa2-244">Per ottenere l'integrità del servizio tramite l'API, creare un oggetto `FabricClient` e chiamare il metodo [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) sul relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="22aa2-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="22aa2-245">L'esempio seguente ottiene l'integrità di un servizio con il nome di servizio (URI) specificato:</span><span class="sxs-lookup"><span data-stu-id="22aa2-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="22aa2-246">Il codice seguente permette di ottenere l'integrità del servizio per il nome del servizio (URI) specificato, con filtri e criteri personalizzati specificati tramite [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="22aa2-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="22aa2-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-247">PowerShell</span></span>
<span data-ttu-id="22aa2-248">Il cmdlet per ottenere l'integrità del servizio è [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="22aa2-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="22aa2-249">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="22aa2-250">Il cmdlet seguente ottiene l'integrità del servizio usando i criteri di integrità predefiniti:</span><span class="sxs-lookup"><span data-stu-id="22aa2-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="22aa2-251">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-251">REST</span></span>
<span data-ttu-id="22aa2-252">Per ottenere l'integrità di un servizio è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="22aa2-253">Get partition health</span><span class="sxs-lookup"><span data-stu-id="22aa2-253">Get partition health</span></span>
<span data-ttu-id="22aa2-254">Restituisce lo stato di un'entità partizione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="22aa2-255">Contiene gli stati di integrità della replica.</span><span class="sxs-lookup"><span data-stu-id="22aa2-255">It contains the replica health states.</span></span> <span data-ttu-id="22aa2-256">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-256">Input:</span></span>

* <span data-ttu-id="22aa2-257">[Obbligatorio] ID partizione (GUID) che identifica la partizione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="22aa2-258">[Facoltativo] Criteri di integrità dell'applicazione usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="22aa2-259">[Facoltativo] Filtri per eventi e repliche che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-260">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi e tutte le repliche, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="22aa2-261">[Facoltativo] Filtrare per escludere le statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="22aa2-262">Se non specificato, le statistiche di integrità mostrano il numero di repliche con stati ok, di avviso e di errore.</span><span class="sxs-lookup"><span data-stu-id="22aa2-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-263">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-263">API</span></span>
<span data-ttu-id="22aa2-264">Per ottenere l'integrità della partizione tramite l'API, creare un oggetto `FabricClient` e chiamare il metodo [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) sul relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="22aa2-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="22aa2-265">Per specificare parametri facoltativi, creare [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="22aa2-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="22aa2-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-266">PowerShell</span></span>
<span data-ttu-id="22aa2-267">Il cmdlet per ottenere l'integrità della partizione è [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="22aa2-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="22aa2-268">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="22aa2-269">Il cmdlet seguente ottiene l'integrità di tutte le partizioni del servizio **fabric:/WordCount/WordCountService** ed esclude tramite filtro gli stati di integrità delle repliche:</span><span class="sxs-lookup"><span data-stu-id="22aa2-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="22aa2-270">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-270">REST</span></span>
<span data-ttu-id="22aa2-271">Per ottenere l'integrità di una partizione è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="22aa2-272">Get replica health</span><span class="sxs-lookup"><span data-stu-id="22aa2-272">Get replica health</span></span>
<span data-ttu-id="22aa2-273">Restituisce l'integrità di una replica di un servizio con stato o di un'istanza di un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="22aa2-274">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-274">Input:</span></span>

* <span data-ttu-id="22aa2-275">[Obbligatorio] ID partizione (GUID) e ID replica che identifica la replica.</span><span class="sxs-lookup"><span data-stu-id="22aa2-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="22aa2-276">[Facoltativo] Parametri dei criteri di integrità dell'applicazione usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="22aa2-277">[Facoltativo] Filtri per gli eventi che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-278">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-279">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-279">API</span></span>
<span data-ttu-id="22aa2-280">Per ottenere l'integrità della replica tramite l'API, creare un oggetto `FabricClient` e chiamare il metodo [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) sul relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="22aa2-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="22aa2-281">Per specificare parametri avanzati, usare [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="22aa2-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="22aa2-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-282">PowerShell</span></span>
<span data-ttu-id="22aa2-283">Il cmdlet per ottenere l'integrità della replica è [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="22aa2-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="22aa2-284">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="22aa2-285">Il cmdlet seguente ottiene l'integrità della replica primaria per tutte le partizioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="22aa2-286">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-286">REST</span></span>
<span data-ttu-id="22aa2-287">Per ottenere l'integrità di una replica è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="22aa2-288">Ottieni lo stato dell'integrità delle applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="22aa2-288">Get deployed application health</span></span>
<span data-ttu-id="22aa2-289">Restituisce l’integrità di un’applicazione distribuita in un’entità nodo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="22aa2-290">Contiene gli stati di integrità del pacchetto di servizi distribuito.</span><span class="sxs-lookup"><span data-stu-id="22aa2-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="22aa2-291">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-291">Input:</span></span>

* <span data-ttu-id="22aa2-292">[Obbligatorio] Nome dell'applicazione (URI) e nome del nodo (stringa) che identificano l'applicazione distribuita</span><span class="sxs-lookup"><span data-stu-id="22aa2-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="22aa2-293">[Facoltativo] Criteri di integrità dell'applicazione usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="22aa2-294">[Facoltativo] Filtri per eventi e pacchetti di servizi distribuiti che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-295">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi e i pacchetti di servizi distribuiti, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="22aa2-296">[Facoltativo] Filtrare per escludere le statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="22aa2-297">Se non specificato, le statistiche di integrità mostrano il numero di pacchetti del servizio distribuiti con stati di integrità ok, di avviso e di errore.</span><span class="sxs-lookup"><span data-stu-id="22aa2-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-298">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-298">API</span></span>
<span data-ttu-id="22aa2-299">Per ottenere l'integrità di un'applicazione distribuita in un nodo tramite l'API, creare un oggetto `FabricClient` e chiamare il metodo [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) sul relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="22aa2-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="22aa2-300">Per specificare parametri facoltativi, usare [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="22aa2-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="22aa2-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-301">PowerShell</span></span>
<span data-ttu-id="22aa2-302">Il cmdlet per ottenere l'integrità dell'applicazione distribuita è [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="22aa2-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="22aa2-303">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="22aa2-304">Per sapere dove viene distribuita un'applicazione, eseguire [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e osservare gli elementi figlio dell'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="22aa2-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="22aa2-305">Il cmdlet seguente ottiene l'integrità dell'applicazione **fabric:/WordCount** distribuita nel nodo **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="22aa2-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="22aa2-306">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-306">REST</span></span>
<span data-ttu-id="22aa2-307">Per ottenere l'integrità di un'applicazione distribuita è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="22aa2-308">Get deployed service package health</span><span class="sxs-lookup"><span data-stu-id="22aa2-308">Get deployed service package health</span></span>
<span data-ttu-id="22aa2-309">Restituisce lo stato di un'entità di pacchetto di servizi distribuito.</span><span class="sxs-lookup"><span data-stu-id="22aa2-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="22aa2-310">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-310">Input:</span></span>

* <span data-ttu-id="22aa2-311">[Obbligatorio] Nome dell'applicazione (URI), nome del nodo (stringa) e nome del manifesto del servizio (stringa) che identificano il pacchetto di servizi distribuito.</span><span class="sxs-lookup"><span data-stu-id="22aa2-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="22aa2-312">[Facoltativo] Criteri di integrità dell'applicazione usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="22aa2-313">[Facoltativo] Filtri per gli eventi che specificano le voci di interesse che devono essere restituite nel risultato (ad esempio, solo gli errori o avvisi ed errori).</span><span class="sxs-lookup"><span data-stu-id="22aa2-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="22aa2-314">Per valutare l'integrità aggregata dell'entità, vengono usati tutti gli eventi, indipendentemente dal filtro.</span><span class="sxs-lookup"><span data-stu-id="22aa2-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-315">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-315">API</span></span>
<span data-ttu-id="22aa2-316">Per ottenere l'integrità di un pacchetto del servizio distribuito tramite l'API, creare un oggetto `FabricClient` e chiamare il metodo [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) sul relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="22aa2-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="22aa2-317">Per specificare parametri facoltativi, usare [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="22aa2-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="22aa2-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-318">PowerShell</span></span>
<span data-ttu-id="22aa2-319">Il cmdlet per ottenere l'integrità del pacchetto del servizio distribuito è [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="22aa2-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="22aa2-320">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="22aa2-321">Per verificare dove viene distribuita un'applicazione, eseguire [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e osservare le applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="22aa2-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="22aa2-322">Per verificare quali pacchetti di servizi sono contenuti in un'applicazione, esaminare gli elementi figlio del pacchetto del servizio distribuito nell'output di [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="22aa2-323">Il cmdlet seguente permette di ottenere l'integrità del pacchetto del servizio **WordCountServicePkg** dell'applicazione **fabric:/WordCount** distribuita in **Node2**.</span><span class="sxs-lookup"><span data-stu-id="22aa2-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="22aa2-324">L'entità include report **System.Hosting** per l'attivazione corretta del pacchetto del servizio e del punto di ingresso, nonché per la registrazione corretta del tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="22aa2-325">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-325">REST</span></span>
<span data-ttu-id="22aa2-326">Per ottenere l'integrità di un pacchetto del servizio distribuito è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="22aa2-327">Query sul blocco di integrità</span><span class="sxs-lookup"><span data-stu-id="22aa2-327">Health chunk queries</span></span>
<span data-ttu-id="22aa2-328">Le query sul blocco di integrità possono restituire gli elementi figlio di un cluster a più livelli (in modo ricorsivo) per ogni filtro di input.</span><span class="sxs-lookup"><span data-stu-id="22aa2-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="22aa2-329">Supporta i filtri avanzati che consentono una notevole flessibilità nella scelta degli elementi figlio da restituire.</span><span class="sxs-lookup"><span data-stu-id="22aa2-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="22aa2-330">I filtri consentono di specificare gli elementi figlio in base a un identificatore univoco o ad altri identificatori di gruppo e/o stati di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="22aa2-331">Per impostazione predefinita, non sono inclusi elementi figlio, a differenza dei comandi relativi all'integrità che includono sempre gli elementi figlio di primo livello.</span><span class="sxs-lookup"><span data-stu-id="22aa2-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="22aa2-332">Le [query sull'integrità](service-fabric-view-entities-aggregated-health.md#health-queries) restituiscono solo gli elementi figlio di primo livello dell'entità specificata per ogni filtro necessario.</span><span class="sxs-lookup"><span data-stu-id="22aa2-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="22aa2-333">Per ottenere gli elementi figlio di un elemento figlio, è necessario chiamare API di integrità aggiuntive per ogni entità di interesse.</span><span class="sxs-lookup"><span data-stu-id="22aa2-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="22aa2-334">Analogamente, per ottenere l'integrità di entità specifiche, è necessario chiamare un'API di integrità per ogni entità di interesse.</span><span class="sxs-lookup"><span data-stu-id="22aa2-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="22aa2-335">I filtri avanzati per le query sui blocchi consentono di richiedere più elementi di interesse in una sola query, riducendo al minimo le dimensioni del messaggio e il numero di messaggi.</span><span class="sxs-lookup"><span data-stu-id="22aa2-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="22aa2-336">Il vantaggio delle query sui blocchi sta nella possibilità di ottenere lo stato dell'integrità per più entità cluster, potenzialmente tutte le entità cluster a partire dalla radice richiesta, in una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="22aa2-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="22aa2-337">È possibile esprimere query sull'integrità complesse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="22aa2-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="22aa2-338">Restituzione solo delle applicazioni con errore e inclusione di tutti i servizi con avviso o errore per queste applicazioni.</span><span class="sxs-lookup"><span data-stu-id="22aa2-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="22aa2-339">Per i servizi restituiti, inclusione di tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="22aa2-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="22aa2-340">Restituzione solo dell'integrità di quattro applicazioni, specificate in base ai rispettivi nomi.</span><span class="sxs-lookup"><span data-stu-id="22aa2-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="22aa2-341">Restituzione solo dell'integrità delle applicazioni con un tipo di applicazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="22aa2-342">Restituzione di tutte le entità distribuite su un nodo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="22aa2-343">Restituisce tutte le applicazioni, tutte le applicazioni distribuite nel nodo specificato e tutti i pacchetti di servizio distribuiti nel nodo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="22aa2-344">Restituzione di tutte le repliche con errore.</span><span class="sxs-lookup"><span data-stu-id="22aa2-344">Return all replicas in error.</span></span> <span data-ttu-id="22aa2-345">Vengono restituiti tutti i servizi, le applicazioni e le partizioni e le sole repliche con errore.</span><span class="sxs-lookup"><span data-stu-id="22aa2-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="22aa2-346">Restituzione di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="22aa2-346">Return all applications.</span></span> <span data-ttu-id="22aa2-347">Per un servizio specificato, inclusione di tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="22aa2-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="22aa2-348">La query sul blocco di integrità è attualmente esposta solo per l'entità del cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="22aa2-349">Restituisce un blocco di integrità del cluster che contiene:</span><span class="sxs-lookup"><span data-stu-id="22aa2-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="22aa2-350">Lo stato di integrità aggregato del cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="22aa2-351">L'elenco del blocco dello stato di integrità dei nodi che rispettano i filtri di input.</span><span class="sxs-lookup"><span data-stu-id="22aa2-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="22aa2-352">L'elenco del blocco dello stato di integrità delle applicazioni che rispettano i filtri di input.</span><span class="sxs-lookup"><span data-stu-id="22aa2-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="22aa2-353">Ogni blocco dello stato di integrità dell'applicazione contiene un elenco di blocchi con tutti i servizi che rispettano i filtri di input e un elenco di blocchi con tutte le applicazioni distribuite che rispettano i filtri.</span><span class="sxs-lookup"><span data-stu-id="22aa2-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="22aa2-354">Lo stesso vale per gli elementi figlio dei servizi e delle applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="22aa2-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="22aa2-355">In questo modo, tutte le entità nel cluster possono essere potenzialmente restituite se richiesto, in modo gerarchico.</span><span class="sxs-lookup"><span data-stu-id="22aa2-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="22aa2-356">Query sul blocco di integrità del cluster</span><span class="sxs-lookup"><span data-stu-id="22aa2-356">Cluster health chunk query</span></span>
<span data-ttu-id="22aa2-357">Restituisce l'integrità dell'entità cluster e contiene blocchi di stato dell'integrità gerarchici degli elementi figlio necessari.</span><span class="sxs-lookup"><span data-stu-id="22aa2-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="22aa2-358">Input:</span><span class="sxs-lookup"><span data-stu-id="22aa2-358">Input:</span></span>

* <span data-ttu-id="22aa2-359">[Facoltativo] Criteri di integrità del cluster usati per valutare i nodi e gli eventi del cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="22aa2-360">[Facoltativo] Mappa dei criteri di integrità dell'applicazione con criteri di integrità usati per sostituire i criteri del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="22aa2-361">[Facoltativo] Filtri per i nodi e per le applicazioni che specificano le voci di interesse e da restituire nel risultato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="22aa2-362">I filtri sono specifici per un'entità/un gruppo di entità o sono applicabili a tutte le entità a tale livello.</span><span class="sxs-lookup"><span data-stu-id="22aa2-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="22aa2-363">L'elenco di filtri può contenere un filtro generale e/o filtri per identificatori specifici per entità dettagliate restituite dalla query.</span><span class="sxs-lookup"><span data-stu-id="22aa2-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="22aa2-364">Se l'elenco è vuoto, gli elementi figlio non vengono restituiti per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="22aa2-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="22aa2-365">Per altre informazioni sui filtri, vedere [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="22aa2-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="22aa2-366">I filtri dell'applicazione possono specificare in modo ricorsivo filtri avanzati per gli elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="22aa2-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="22aa2-367">I risultati del blocco includono gli elementi figlio che rispettano i filtri.</span><span class="sxs-lookup"><span data-stu-id="22aa2-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="22aa2-368">Analogamente, la query sul blocco non restituisce valutazioni non integre o eventi dell'entità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="22aa2-369">Tali informazioni aggiuntive possono essere ottenute usando la query sull'integrità del cluster esistente.</span><span class="sxs-lookup"><span data-stu-id="22aa2-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="22aa2-370">API</span><span class="sxs-lookup"><span data-stu-id="22aa2-370">API</span></span>
<span data-ttu-id="22aa2-371">Per ottenere il blocco di integrità del cluster, creare un oggetto `FabricClient` e chiamare il metodo [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) sul relativo **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="22aa2-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="22aa2-372">È possibile passare [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) per descrivere i criteri di integrità e i filtri avanzati.</span><span class="sxs-lookup"><span data-stu-id="22aa2-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="22aa2-373">Il codice seguente permette di ottenere il blocco di integrità del cluster con filtri avanzati.</span><span class="sxs-lookup"><span data-stu-id="22aa2-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="22aa2-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa2-374">PowerShell</span></span>
<span data-ttu-id="22aa2-375">Il cmdlet per ottenere l'integrità del cluster è [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="22aa2-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="22aa2-376">Connettersi prima di tutto al cluster con il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="22aa2-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="22aa2-377">Il codice seguente permette di ottenere solo i nodi in stato di errore, eccetto un nodo specifico che deve essere restituito sempre.</span><span class="sxs-lookup"><span data-stu-id="22aa2-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="22aa2-378">Il cmdlet seguente permette di ottenere il blocco di cluster con filtri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22aa2-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="22aa2-379">Il cmdlet seguente restituisce tutte le entità distribuite su un nodo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="22aa2-380">REST</span><span class="sxs-lookup"><span data-stu-id="22aa2-380">REST</span></span>
<span data-ttu-id="22aa2-381">Per ottenere il blocco di integrità di un cluster è possibile usare una [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) o una [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) che nel corpo include la descrizione di criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="22aa2-382">Query generali</span><span class="sxs-lookup"><span data-stu-id="22aa2-382">General queries</span></span>
<span data-ttu-id="22aa2-383">Le query generali restituiscono l'elenco delle entità di Service Fabric di un tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="22aa2-384">Le query vengono esposte tramite l'API con i metodi in **FabricClient.QueryManager**, tramite i cmdlet di PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="22aa2-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="22aa2-385">Queste query aggregano sottoquery da più componenti.</span><span class="sxs-lookup"><span data-stu-id="22aa2-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="22aa2-386">Uno di questi è l' [archivio integrità](service-fabric-health-introduction.md#health-store), che popola lo stato di integrità aggregato per ogni risultato della query.</span><span class="sxs-lookup"><span data-stu-id="22aa2-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="22aa2-387">Le query generali restituiscono lo stato di integrità aggregato dell'entità e non contengono i dati di integrità complessi.</span><span class="sxs-lookup"><span data-stu-id="22aa2-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="22aa2-388">Se un'entità non è integra, è possibile procedere con query di integrità per ottenere tutte le informazioni di integrità, come gli eventi, gli stati di integrità degli elementi figlio e le valutazioni non integre.</span><span class="sxs-lookup"><span data-stu-id="22aa2-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="22aa2-389">Se le query generali restituiscono uno stato di integrità sconosciuto per un'entità, è possibile che l'archivio integrità non abbia dati completi sull'entità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="22aa2-390">È anche possibile che una sottoquery nell'archivio integrità non sia riuscita, ad esempio, si è verificato un errore di comunicazione o l'archivio integrità è stato limitato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="22aa2-391">Procedere con una query di integrità per l'entità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="22aa2-392">Se la sottoquery ha rilevato errori temporanei, ad esempio problemi di rete, questa query di completamento può riuscire.</span><span class="sxs-lookup"><span data-stu-id="22aa2-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="22aa2-393">Può anche fornire altri dettagli dall'archivio integrità sui motivi che impediscono l'esposizione dell'entità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="22aa2-394">Di seguito sono elencate le query che contengono **HealthState** per le entità:</span><span class="sxs-lookup"><span data-stu-id="22aa2-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="22aa2-395">Elenco dei nodi: restituisce i nodi elencati nel cluster (di paging).</span><span class="sxs-lookup"><span data-stu-id="22aa2-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="22aa2-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="22aa2-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="22aa2-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="22aa2-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="22aa2-398">Elenco delle applicazioni: restituisce l'elenco di applicazioni nel cluster (di paging).</span><span class="sxs-lookup"><span data-stu-id="22aa2-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="22aa2-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="22aa2-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="22aa2-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="22aa2-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="22aa2-401">Elenco dei servizi: restituisce l'elenco dei servizi in un'applicazione (di paging).</span><span class="sxs-lookup"><span data-stu-id="22aa2-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="22aa2-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="22aa2-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="22aa2-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="22aa2-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="22aa2-404">Elenco delle partizioni: restituisce l'elenco delle partizioni in un servizio (di paging).</span><span class="sxs-lookup"><span data-stu-id="22aa2-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="22aa2-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="22aa2-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="22aa2-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="22aa2-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="22aa2-407">Elenco delle repliche: restituisce l'elenco delle repliche in una partizione (di paging).</span><span class="sxs-lookup"><span data-stu-id="22aa2-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="22aa2-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="22aa2-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="22aa2-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="22aa2-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="22aa2-410">Elenco delle applicazioni distribuite: restituisce l'elenco delle applicazioni distribuite in un nodo.</span><span class="sxs-lookup"><span data-stu-id="22aa2-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="22aa2-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="22aa2-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="22aa2-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="22aa2-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="22aa2-413">Elenco dei pacchetti di servizi distribuiti: restituisce l'elenco dei pacchetti di servizi in un'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="22aa2-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="22aa2-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="22aa2-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="22aa2-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="22aa2-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="22aa2-416">Alcune query restituiscono risultati di paging.</span><span class="sxs-lookup"><span data-stu-id="22aa2-416">Some of the queries return paged results.</span></span> <span data-ttu-id="22aa2-417">Queste query restituiscono un elenco derivato da [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="22aa2-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="22aa2-418">Se questi risultati non corrispondono a un messaggio, viene restituita solo una pagina e un ContinuationToken che tiene traccia del punto in cui l'enumerazione è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="22aa2-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="22aa2-419">Continuare a chiamare la stessa query e passare il token di continuazione dalla query precedente per ottenere i risultati successivi.</span><span class="sxs-lookup"><span data-stu-id="22aa2-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="22aa2-420">Esempi</span><span class="sxs-lookup"><span data-stu-id="22aa2-420">Examples</span></span>
<span data-ttu-id="22aa2-421">Il codice seguente permette di ottenere le applicazioni non integre nel cluster:</span><span class="sxs-lookup"><span data-stu-id="22aa2-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="22aa2-422">Il cmdlet seguente ottiene i dettagli dell'applicazione per l'applicazione fabric:/WordCount.</span><span class="sxs-lookup"><span data-stu-id="22aa2-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="22aa2-423">Lo stato di integrità è di tipo avviso.</span><span class="sxs-lookup"><span data-stu-id="22aa2-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="22aa2-424">Il cmdlet seguente ottiene i servizi con stato di integrità di errore:</span><span class="sxs-lookup"><span data-stu-id="22aa2-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="22aa2-425">Aggiornamenti del cluster e dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="22aa2-425">Cluster and application upgrades</span></span>
<span data-ttu-id="22aa2-426">Durante un aggiornamento monitorato del cluster e dell'applicazione, Service Fabric controlla l'integrità per garantire che lo stato sia integro e che rimanga tale.</span><span class="sxs-lookup"><span data-stu-id="22aa2-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="22aa2-427">Se un'entità non è integra ed è stata valutata con i criteri di integrità configurati, l'aggiornamento applica criteri specifici dell'aggiornamento per determinare l'azione successiva.</span><span class="sxs-lookup"><span data-stu-id="22aa2-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="22aa2-428">L'aggiornamento può essere sospeso per consentire l'interazione dell'utente, ad esempio per correggere le condizioni di errore o modificare i criteri, oppure può eseguire automaticamente il ripristino dello stato precedente di una versione funzionante.</span><span class="sxs-lookup"><span data-stu-id="22aa2-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="22aa2-429">Durante un aggiornamento del *cluster* è possibile ottenerne lo stato di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="22aa2-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="22aa2-430">Quest'ultimo include valutazioni di non integrità, che puntano agli elementi non integri nel cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="22aa2-431">Se viene eseguito il rollback dell'aggiornamento a causa di problemi di integrità, lo stato di aggiornamento memorizza le cause di non integrità più recenti.</span><span class="sxs-lookup"><span data-stu-id="22aa2-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="22aa2-432">Queste informazioni consentono agli amministratori di analizzare la causa dell'errore dopo il rollback o l'arresto dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="22aa2-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="22aa2-433">Analogamente, durante l'aggiornamento di un' *applicazione* , lo stato di aggiornamento dell'applicazione stessa include le eventuali valutazioni di non integrità.</span><span class="sxs-lookup"><span data-stu-id="22aa2-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="22aa2-434">Di seguito viene illustrato lo stato di aggiornamento dell’applicazione per un’applicazione fabric:/WordCount modificata.</span><span class="sxs-lookup"><span data-stu-id="22aa2-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="22aa2-435">Un watchdog ha segnalato un errore in una delle repliche.</span><span class="sxs-lookup"><span data-stu-id="22aa2-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="22aa2-436">Viene eseguito il rollback dell’aggiornamento poiché le verifiche dell’integrità non sono rispettate.</span><span class="sxs-lookup"><span data-stu-id="22aa2-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="22aa2-437">Per altre informazioni, vedere [Aggiornamento di un'applicazione di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="22aa2-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="22aa2-438">Usare le valutazioni dell'integrità per risolvere i problemi</span><span class="sxs-lookup"><span data-stu-id="22aa2-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="22aa2-439">Ogni volta che si verifica un problema in cluster o in un'applicazione, osservare l'integrità del cluster o dell'applicazione per individuare il problema riscontrato.</span><span class="sxs-lookup"><span data-stu-id="22aa2-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="22aa2-440">Le valutazioni di non integrità includono dettagli sulle cause che hanno attivato lo stato di non integrità corrente.</span><span class="sxs-lookup"><span data-stu-id="22aa2-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="22aa2-441">È possibile eseguire il drill-down delle entità figlio non integre per identificare la causa radice.</span><span class="sxs-lookup"><span data-stu-id="22aa2-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="22aa2-442">Si consideri, ad esempio, un'applicazione non integra a causa di un errore segnalato in una delle relative repliche.</span><span class="sxs-lookup"><span data-stu-id="22aa2-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="22aa2-443">Il cmdlet di Powershell seguente mostra le valutazioni di non integrità:</span><span class="sxs-lookup"><span data-stu-id="22aa2-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="22aa2-444">È possibile esaminare la replica per ottenere altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="22aa2-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="22aa2-445">Le valutazioni non integre mostrano il primo motivo per cui l'entità restituisce lo stato di integrità corrente.</span><span class="sxs-lookup"><span data-stu-id="22aa2-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="22aa2-446">Lo stato potrebbe essere attivato da vari altri eventi, che però non devono riflettersi nelle valutazioni.</span><span class="sxs-lookup"><span data-stu-id="22aa2-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="22aa2-447">Per ottenere altre informazioni, è necessario eseguire il drill-down nelle entità di integrità per trovare tutti i report non integri nel cluster.</span><span class="sxs-lookup"><span data-stu-id="22aa2-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="22aa2-448">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22aa2-448">Next steps</span></span>
[<span data-ttu-id="22aa2-449">Usare i report sull'integrità del sistema per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="22aa2-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="22aa2-450">Aggiungere report sull'integrità di Service Fabric personalizzati</span><span class="sxs-lookup"><span data-stu-id="22aa2-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="22aa2-451">Creare report e verificare l'integrità dei servizi</span><span class="sxs-lookup"><span data-stu-id="22aa2-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="22aa2-452">Monitorare e diagnosticare servizi in locale</span><span class="sxs-lookup"><span data-stu-id="22aa2-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="22aa2-453">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="22aa2-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
