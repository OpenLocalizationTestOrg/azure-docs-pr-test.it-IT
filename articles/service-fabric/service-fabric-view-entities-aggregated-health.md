---
title: "aaaHow tooview Azure Service Fabric entità aggregato di integrità | Documenti Microsoft"
description: "Viene descritto come tooquery, visualizzare e valutare l'integrità di entità Azure Service Fabric aggregato, tramite query sull'integrità e le query generali."
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
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="1e567-103">Come visualizzare i report sull'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1e567-103">View Service Fabric health reports</span></span>
<span data-ttu-id="1e567-104">Azure Service Fabric introduce un [modello di integrità](service-fabric-health-introduction.md) con entità di integrità per le quali i componenti di sistema e i watchdog possono creare report sulle condizioni locali sottoposte a monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="1e567-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="1e567-105">Hello [archivio integrità](service-fabric-health-introduction.md#health-store) aggrega tutti toodetermine di dati di integrità se le entità siano integri.</span><span class="sxs-lookup"><span data-stu-id="1e567-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="1e567-106">cluster Hello viene popolato automaticamente con i rapporti di stati inviati dai componenti di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="1e567-107">Leggere informazioni, vedere [tootroubleshoot report l'integrità di sistema utilizzare](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="1e567-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="1e567-108">Infrastruttura del servizio sono disponibili più modi tooget hello aggregato integrità di entità hello:</span><span class="sxs-lookup"><span data-stu-id="1e567-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="1e567-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) o altri strumenti di visualizzazione</span><span class="sxs-lookup"><span data-stu-id="1e567-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="1e567-110">Query di integrità (tramite PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="1e567-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="1e567-111">Generale query che restituiscono un elenco di entità che dispongono di integrità come una delle proprietà di hello (tramite PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="1e567-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="1e567-112">toodemonstrate queste opzioni, consente l'utilizzo di un cluster locale con cinque nodi e hello [fabric: / applicazione WordCount](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="1e567-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="1e567-113">Hello **fabric: / WordCount** applicazione contiene due servizi predefiniti, un servizio con stato di tipo `WordCountServiceType`e un servizio senza stato di tipo `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="1e567-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="1e567-114">In seguito alla modifica hello `ApplicationManifest.xml` toorequire sette repliche di destinazione per i servizi con stato hello e una partizione.</span><span class="sxs-lookup"><span data-stu-id="1e567-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="1e567-115">Poiché sono presenti solo cinque nodi nel cluster hello, i componenti di sistema hello report un avviso sulla partizione di servizio hello perché è inferiore al conteggio di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

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

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="1e567-116">Integrità in Esplora Infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="1e567-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="1e567-117">Service Fabric Explorer fornisce una visualizzazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="1e567-118">Nell'immagine hello riportata di seguito, è possibile vedere che:</span><span class="sxs-lookup"><span data-stu-id="1e567-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="1e567-119">applicazione Hello **fabric: / WordCount** è rosso (errore) perché dispone di un evento di errore segnalato da **MyWatchdog** per la proprietà hello **disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="1e567-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="1e567-120">Uno dei servizi di questa applicazione, **fabric:/WordCount/WordCountService** è di colore giallo (condizione di avviso).</span><span class="sxs-lookup"><span data-stu-id="1e567-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="1e567-121">servizio Hello è configurato con le sette repliche e cluster hello include cinque nodi, in modo non è possibile inserire due repicas.</span><span class="sxs-lookup"><span data-stu-id="1e567-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="1e567-122">Sebbene non illustrato di seguito, partizione del servizio hello è giallo a causa di un report di sistema da `System.FM` che informa che `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="1e567-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="1e567-123">i trigger di partizione giallo Hello hello servizio giallo.</span><span class="sxs-lookup"><span data-stu-id="1e567-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="1e567-124">cluster Hello è rosso a causa di un'applicazione hello rosso.</span><span class="sxs-lookup"><span data-stu-id="1e567-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="1e567-125">valutazione Hello utilizza criteri predefiniti dal manifesto del cluster hello e manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e567-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="1e567-126">Questi sono criteri rigorosi e non tollerano errori.</span><span class="sxs-lookup"><span data-stu-id="1e567-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="1e567-127">Visualizzazione del cluster di hello di Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="1e567-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Visualizzazione del cluster di hello di Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="1e567-129">Ulteriori informazioni su [Esplora Infrastruttura di servizi](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1e567-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="1e567-130">Query relative all’integrità</span><span class="sxs-lookup"><span data-stu-id="1e567-130">Health queries</span></span>
<span data-ttu-id="1e567-131">Service Fabric espone una query sull'integrità per ogni hello supportato [tipi di entità](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="1e567-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="1e567-132">Sono accessibili mediante API, utilizzando i metodi di hello [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), i cmdlet di PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="1e567-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="1e567-133">Queste query restituiscono informazioni di stato completo sull'entità hello: hello aggregati lo stato di integrità, gli eventi di integrità di entità, gli stati di integrità figlio (se applicabile), non integro valutazioni (quando l'entità hello non integro) e le statistiche di integrità di elementi figlio (quando applicabile).</span><span class="sxs-lookup"><span data-stu-id="1e567-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="1e567-134">Un'entità di integrità viene restituita quando viene compilata completamente nell'archivio integrità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="1e567-135">entità Hello deve essere attivo (non eliminata) e dispone di un report di sistema.</span><span class="sxs-lookup"><span data-stu-id="1e567-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="1e567-136">Le entità padre nella catena della gerarchia hello devono inoltre disporre di report del sistema.</span><span class="sxs-lookup"><span data-stu-id="1e567-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="1e567-137">Se una di queste condizioni non vengono soddisfatti, integrità hello query restituiscono un [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) con [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` che mostra perché non vengono restituite entità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="1e567-138">Identificatore dell'entità hello, che dipende dal tipo di entità hello deve passare query sull'integrità Hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="1e567-139">le query Hello accettano parametri dei criteri di integrità facoltativi.</span><span class="sxs-lookup"><span data-stu-id="1e567-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="1e567-140">Se non è stato specificato alcun criterio di integrità, hello [criteri di integrità](service-fabric-health-introduction.md#health-policies) dal manifesto del cluster o l'applicazione hello vengono utilizzati per la valutazione.</span><span class="sxs-lookup"><span data-stu-id="1e567-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="1e567-141">Se i manifesti hello non contengono una definizione di criteri di integrità, criteri di integrità hello predefiniti vengono utilizzati per la valutazione.</span><span class="sxs-lookup"><span data-stu-id="1e567-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="1e567-142">criteri di integrità Hello predefinito non essere in grado di tollerare eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="1e567-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="1e567-143">le query Hello accettano anche i filtri per la restituzione solo elementi figlio parziali o eventi: hello quelli che rispettano hello i filtri specificati.</span><span class="sxs-lookup"><span data-stu-id="1e567-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="1e567-144">Un altro filtro consente di escludere le statistiche di hello elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="1e567-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="1e567-145">i filtri di output di Hello vengono applicati sul lato server hello, pertanto le dimensioni di risposta messaggio hello sono ridotto.</span><span class="sxs-lookup"><span data-stu-id="1e567-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="1e567-146">Si consiglia di utilizzare i filtri di output di hello toolimit hello dati restituito, anziché applicano filtri sul lato client hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="1e567-147">L'integrità di un'entità contiene quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1e567-147">An entity's health contains:</span></span>

* <span data-ttu-id="1e567-148">Hello lo stato di integrità aggregato dell'entità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="1e567-149">Calcolato dall'archivio integrità hello basato su rapporti di integrità di entità, gli stati di integrità figlio (se applicabile) e criteri di integrità.</span><span class="sxs-lookup"><span data-stu-id="1e567-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="1e567-150">Per altre informazioni, vedere [valutazione dell'integrità dell'entità](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="1e567-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="1e567-151">eventi di integrità Hello nell'entità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="1e567-152">raccolta di Hello degli stati di integrità di tutti gli elementi figlio per le entità hello possono avere elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="1e567-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="1e567-153">gli stati di integrità Hello contengono gli identificatori di entità e hello stato di integrità aggregato.</span><span class="sxs-lookup"><span data-stu-id="1e567-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="1e567-154">tooget stato completo per un elemento figlio, chiamare integrità query hello per tipo di entità figlio hello e passare identificatore figlio hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="1e567-155">le valutazioni di tipo non integro Hello toohello tale punto del report che attivata stato hello dell'entità di hello, se l'entità hello non è integro.</span><span class="sxs-lookup"><span data-stu-id="1e567-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="1e567-156">valutazioni Hello sono ricorsivi, contenente valutazioni dell'integrità hello figli che ha attivato lo stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="1e567-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="1e567-157">Un watchdog ha segnalato ad esempio un errore in una replica.</span><span class="sxs-lookup"><span data-stu-id="1e567-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="1e567-158">integrità applicazione Hello viene illustrata una versione di valutazione non integro scadenza tooan servizio di tipo non integro. servizio di Hello è danneggiato a causa di partizione tooa in errore. partizione di Hello è danneggiato a causa di replica tooa in errore. non è integro scadenza rapporto di stato di errore watchdog toohello replica Hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="1e567-159">statistiche di integrità Hello per tutti i tipi di elementi figlio di entità hello che hanno elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="1e567-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="1e567-160">Ad esempio, l'integrità del cluster Mostra hello il numero totale di applicazioni, servizi, partizioni, le repliche e distribuiti entità cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="1e567-161">Stato servizio Mostra numero totale di hello di partizioni e repliche in hello servizio specificato.</span><span class="sxs-lookup"><span data-stu-id="1e567-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="1e567-162">Get cluster health</span><span class="sxs-lookup"><span data-stu-id="1e567-162">Get cluster health</span></span>
<span data-ttu-id="1e567-163">Restituisce l'integrità di entità cluster hello hello e contiene hello gli stati di integrità delle applicazioni e i nodi (elementi figlio del cluster hello).</span><span class="sxs-lookup"><span data-stu-id="1e567-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="1e567-164">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-164">Input:</span></span>

* <span data-ttu-id="1e567-165">Criteri di integrità del cluster [facoltativo] hello utilizzato nodi hello tooevaluate e gli eventi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="1e567-166">Mappa criteri di integrità dell'applicazione di hello [facoltativo], con i criteri di integrità hello utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="1e567-167">[Facoltativo] Filtri per eventi, i nodi e le applicazioni che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-168">Tutti gli eventi, i nodi e le applicazioni sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="1e567-169">[Facoltativo] Filtrare le statistiche di integrità tooexclude.</span><span class="sxs-lookup"><span data-stu-id="1e567-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="1e567-170">[Facoltativo] Filtrare tooinclude fabric: / statistiche di integrità del sistema in hello delle statistiche di integrità.</span><span class="sxs-lookup"><span data-stu-id="1e567-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="1e567-171">Questo campo è applicabile solo quando non sono escluse le statistiche di integrità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="1e567-172">Per impostazione predefinita, le statistiche di integrità hello includono solo le statistiche per le applicazioni utente e non un'applicazione hello del sistema.</span><span class="sxs-lookup"><span data-stu-id="1e567-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-173">API</span><span class="sxs-lookup"><span data-stu-id="1e567-173">API</span></span>
<span data-ttu-id="1e567-174">tooget integrità del cluster, creare un `FabricClient` chiamata hello e [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) metodo relativo **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="1e567-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="1e567-175">Hello chiamata seguente ottiene l'integrità del cluster hello:</span><span class="sxs-lookup"><span data-stu-id="1e567-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="1e567-176">Hello codice seguente ottiene l'integrità del cluster hello utilizzando un criterio di integrità del cluster personalizzato e i filtri per i nodi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e567-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="1e567-177">Specifica che le statistiche di integrità hello includono infrastruttura hello: / statistiche di sistema.</span><span class="sxs-lookup"><span data-stu-id="1e567-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="1e567-178">Crea [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), che contiene informazioni di input hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="1e567-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-179">PowerShell</span></span>
<span data-ttu-id="1e567-180">integrità del cluster hello tooget cmdlet Hello è [Get ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="1e567-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="1e567-181">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="1e567-182">Hello stato del cluster hello è cinque nodi, l'applicazione di sistema hello e fabric: / WordCount configurato come descritto.</span><span class="sxs-lookup"><span data-stu-id="1e567-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="1e567-183">Hello cmdlet seguente ottiene l'integrità del cluster tramite criteri di integrità predefinito.</span><span class="sxs-lookup"><span data-stu-id="1e567-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="1e567-184">Hello stato di integrità aggregato è avviso, in quanto hello fabric: / applicazione WordCount è in avviso.</span><span class="sxs-lookup"><span data-stu-id="1e567-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="1e567-185">Si noti come valutazioni integro hello forniscono dettagli sulle condizioni di hello che ha attivato integrità hello aggregato.</span><span class="sxs-lookup"><span data-stu-id="1e567-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

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

<span data-ttu-id="1e567-186">Hello cmdlet di PowerShell seguente ottiene hello integrità del cluster hello utilizzando un criterio di applicazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1e567-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="1e567-187">Filtra i risultati tooget solo le applicazioni e i nodi in errore o avviso.</span><span class="sxs-lookup"><span data-stu-id="1e567-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="1e567-188">Di conseguenza, non vengono restituiti nodi, perché sono tutti integri.</span><span class="sxs-lookup"><span data-stu-id="1e567-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="1e567-189">Solo hello fabric: / applicazione WordCount rispetta filtro applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="1e567-190">Poiché i criteri personalizzati di hello specificano tooconsider avvisi come errori per l'infrastruttura di hello: / applicazione WordCount, un'applicazione hello viene valutata come in errore e pertanto è hello cluster.</span><span class="sxs-lookup"><span data-stu-id="1e567-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

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

### <a name="rest"></a><span data-ttu-id="1e567-191">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-191">REST</span></span>
<span data-ttu-id="1e567-192">È possibile ottenere l'integrità del cluster con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="1e567-193">Get node health</span><span class="sxs-lookup"><span data-stu-id="1e567-193">Get node health</span></span>
<span data-ttu-id="1e567-194">Restituisce hello integrità di un'entità del nodo e contiene gli eventi di integrità hello segnalati nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="1e567-195">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-195">Input:</span></span>

* <span data-ttu-id="1e567-196">Nome del nodo hello [obbligatorio] che identifica il nodo hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="1e567-197">Impostazioni dei criteri di integrità del cluster [facoltativo] hello utilizzato tooevaluate integrità.</span><span class="sxs-lookup"><span data-stu-id="1e567-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="1e567-198">[Facoltativo] Filtri per gli eventi che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-199">Tutti gli eventi sono di integrità aggregato dell'entità di hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-200">API</span><span class="sxs-lookup"><span data-stu-id="1e567-200">API</span></span>
<span data-ttu-id="1e567-201">integrità del nodo tooget tramite hello API, creare un `FabricClient` chiamata hello e [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) metodo relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="1e567-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="1e567-202">Hello codice seguente ottiene integrità del nodo per il nome di nodo specificato hello hello:</span><span class="sxs-lookup"><span data-stu-id="1e567-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="1e567-203">Hello codice seguente ottiene integrità del nodo hello per hello specificato nome di nodo e passa nel filtro di eventi e criteri personalizzati tramite [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="1e567-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="1e567-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-204">PowerShell</span></span>
<span data-ttu-id="1e567-205">integrità del nodo hello tooget cmdlet Hello è [Get ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="1e567-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="1e567-206">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="1e567-207">Hello seguente cmdlet Ottiene l'integrità del nodo hello tramite criteri di integrità predefinito:</span><span class="sxs-lookup"><span data-stu-id="1e567-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

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

<span data-ttu-id="1e567-208">Hello cmdlet seguente ottiene hello integrità di tutti i nodi nel cluster hello:</span><span class="sxs-lookup"><span data-stu-id="1e567-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

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

### <a name="rest"></a><span data-ttu-id="1e567-209">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-209">REST</span></span>
<span data-ttu-id="1e567-210">È possibile ottenere l'integrità del nodo con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="1e567-211">Ottieni lo stato dell'integrità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1e567-211">Get application health</span></span>
<span data-ttu-id="1e567-212">Restituisce hello integrità di un'entità di applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e567-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="1e567-213">Contiene gli stati di integrità hello di un'applicazione hello distribuito e gli elementi figlio del servizio.</span><span class="sxs-lookup"><span data-stu-id="1e567-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="1e567-214">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-214">Input:</span></span>

* <span data-ttu-id="1e567-215">Hello [obbligatorio] nome dell'applicazione (URI) che identifica un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="1e567-216">Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="1e567-217">[Facoltativo] Filtri per gli eventi, servizi e applicazioni distribuite che specificano le voci che sono di interesse e devono essere restituiti nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-218">Tutti gli eventi, servizi e applicazioni distribuite sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="1e567-219">[Facoltativo] Filtrare le statistiche di integrità hello tooexclude.</span><span class="sxs-lookup"><span data-stu-id="1e567-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="1e567-220">Se non specificato, le statistiche di integrità hello includono hello ok, avviso e il numero di errore per tutti gli elementi figlio dell'applicazione: servizi, partizioni e repliche, le applicazioni distribuite e distribuiti i pacchetti del servizio.</span><span class="sxs-lookup"><span data-stu-id="1e567-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-221">API</span><span class="sxs-lookup"><span data-stu-id="1e567-221">API</span></span>
<span data-ttu-id="1e567-222">integrità applicazione tooget, creare un `FabricClient` chiamata hello e [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) metodo relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="1e567-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="1e567-223">Hello codice seguente ottiene lo stato di applicazioni hello per nome dell'applicazione specificato hello (URI):</span><span class="sxs-lookup"><span data-stu-id="1e567-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="1e567-224">Hello codice seguente ottiene integrità applicazione hello per nome dell'applicazione specificato hello (URI), con i filtri e i criteri personalizzati specificati tramite [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="1e567-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="1e567-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-225">PowerShell</span></span>
<span data-ttu-id="1e567-226">l'integrità dell'applicazione Hello cmdlet tooget hello è [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="1e567-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="1e567-227">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="1e567-228">il cmdlet seguente Hello restituisce integrità hello di hello **fabric: / WordCount** applicazione:</span><span class="sxs-lookup"><span data-stu-id="1e567-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

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

<span data-ttu-id="1e567-229">Hello seguendo i passaggi di cmdlet di PowerShell nei criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1e567-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="1e567-230">Filtra anche gli elementi figlio e gli eventi.</span><span class="sxs-lookup"><span data-stu-id="1e567-230">It also filters children and events.</span></span>

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

### <a name="rest"></a><span data-ttu-id="1e567-231">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-231">REST</span></span>
<span data-ttu-id="1e567-232">È possibile ottenere l'integrità dell'applicazione con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="1e567-233">Get service health</span><span class="sxs-lookup"><span data-stu-id="1e567-233">Get service health</span></span>
<span data-ttu-id="1e567-234">Restituisce hello integrità di un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="1e567-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="1e567-235">Contiene gli stati di integrità di hello partizione.</span><span class="sxs-lookup"><span data-stu-id="1e567-235">It contains hello partition health states.</span></span> <span data-ttu-id="1e567-236">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-236">Input:</span></span>

* <span data-ttu-id="1e567-237">Hello [obbligatorio] nome del servizio (URI) che identifica il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="1e567-238">Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="1e567-239">[Facoltativo] Filtri per gli eventi e le partizioni che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-240">Tutti gli eventi e le partizioni sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="1e567-241">[Facoltativo] Filtrare le statistiche di integrità tooexclude.</span><span class="sxs-lookup"><span data-stu-id="1e567-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="1e567-242">Se non specificato, hello hello Mostra le statistiche di integrità ok, avviso e errore numero per tutte le partizioni e repliche del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-243">API</span><span class="sxs-lookup"><span data-stu-id="1e567-243">API</span></span>
<span data-ttu-id="1e567-244">integrità del servizio tooget attraverso hello API, creare un `FabricClient` chiamata hello e [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) metodo relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="1e567-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="1e567-245">Hello seguente esempio ottiene hello integrità di un servizio con il nome di servizio specifico (URI):</span><span class="sxs-lookup"><span data-stu-id="1e567-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="1e567-246">il codice seguente Hello Ottiene hello dell'integrità del servizio per nome del servizio specificato hello (URI), specificando i filtri e i criteri personalizzati tramite [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="1e567-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="1e567-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-247">PowerShell</span></span>
<span data-ttu-id="1e567-248">Hello cmdlet tooget hello servizio integrità è [Get ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="1e567-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="1e567-249">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="1e567-250">Hello seguente cmdlet Ottiene integrità servizio hello tramite criteri di integrità predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1e567-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

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

### <a name="rest"></a><span data-ttu-id="1e567-251">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-251">REST</span></span>
<span data-ttu-id="1e567-252">È possibile ottenere l'integrità del servizio con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="1e567-253">Get partition health</span><span class="sxs-lookup"><span data-stu-id="1e567-253">Get partition health</span></span>
<span data-ttu-id="1e567-254">Restituisce hello integrità di un'entità di partizione.</span><span class="sxs-lookup"><span data-stu-id="1e567-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="1e567-255">Contiene gli stati di integrità replica hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-255">It contains hello replica health states.</span></span> <span data-ttu-id="1e567-256">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-256">Input:</span></span>

* <span data-ttu-id="1e567-257">Partizione hello [obbligatorio] ID (GUID) che identifica la partizione hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="1e567-258">Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="1e567-259">[Facoltativo] Filtri per gli eventi e le repliche che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-260">Tutti gli eventi e le repliche sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="1e567-261">[Facoltativo] Filtrare le statistiche di integrità tooexclude.</span><span class="sxs-lookup"><span data-stu-id="1e567-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="1e567-262">Se non specificato, le statistiche di integrità hello mostrano il numero di repliche ok, avviso ed errore stati.</span><span class="sxs-lookup"><span data-stu-id="1e567-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-263">API</span><span class="sxs-lookup"><span data-stu-id="1e567-263">API</span></span>
<span data-ttu-id="1e567-264">integrità della partizione tooget tramite hello API, creare un `FabricClient` chiamata hello e [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) metodo relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="1e567-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="1e567-265">parametri facoltativi toospecify, creare [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="1e567-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="1e567-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-266">PowerShell</span></span>
<span data-ttu-id="1e567-267">integrità della partizione hello tooget cmdlet Hello è [Get ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="1e567-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="1e567-268">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="1e567-269">Hello seguente ottiene integrità hello per tutte le partizioni di hello **fabric: / WordCount/WordCountService** servizio ed esclude quelli gli stati di integrità di replica:</span><span class="sxs-lookup"><span data-stu-id="1e567-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="rest"></a><span data-ttu-id="1e567-270">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-270">REST</span></span>
<span data-ttu-id="1e567-271">È possibile ottenere l'integrità della partizione con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="1e567-272">Get replica health</span><span class="sxs-lookup"><span data-stu-id="1e567-272">Get replica health</span></span>
<span data-ttu-id="1e567-273">Restituisce l'integrità di hello di una replica del servizio con stato o un'istanza del servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="1e567-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="1e567-274">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-274">Input:</span></span>

* <span data-ttu-id="1e567-275">Hello [obbligatorio] ID (GUID) e replica ID partizione che identifica hello replica.</span><span class="sxs-lookup"><span data-stu-id="1e567-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="1e567-276">Parametri dei criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="1e567-277">[Facoltativo] Filtri per gli eventi che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-278">Tutti gli eventi sono di integrità aggregato dell'entità di hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-279">API</span><span class="sxs-lookup"><span data-stu-id="1e567-279">API</span></span>
<span data-ttu-id="1e567-280">integrità della replica hello tooget tramite hello API, creare un `FabricClient` chiamata hello e [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) metodo relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="1e567-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="1e567-281">Utilizzare parametri avanzati toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="1e567-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="1e567-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-282">PowerShell</span></span>
<span data-ttu-id="1e567-283">integrità della replica hello tooget cmdlet Hello è [Get ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="1e567-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="1e567-284">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="1e567-285">Hello cmdlet seguente ottiene hello integrità della replica primaria di hello per tutte le partizioni del servizio hello:</span><span class="sxs-lookup"><span data-stu-id="1e567-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

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

### <a name="rest"></a><span data-ttu-id="1e567-286">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-286">REST</span></span>
<span data-ttu-id="1e567-287">È possibile ottenere l'integrità della replica con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="1e567-288">Ottieni lo stato dell'integrità delle applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="1e567-288">Get deployed application health</span></span>
<span data-ttu-id="1e567-289">Restituisce hello integrità di un'applicazione distribuita in un'entità del nodo.</span><span class="sxs-lookup"><span data-stu-id="1e567-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="1e567-290">Contiene gli stati di integrità pacchetto servizio hello distribuito.</span><span class="sxs-lookup"><span data-stu-id="1e567-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="1e567-291">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-291">Input:</span></span>

* <span data-ttu-id="1e567-292">Nome dell'applicazione hello [obbligatorio] (URI) e il nome di nodo (stringa) che identificano hello applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="1e567-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="1e567-293">Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="1e567-294">[Facoltativo] Filtri per gli eventi e i pacchetti del servizio distribuiti che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-295">Tutti gli eventi e i pacchetti del servizio distribuito sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="1e567-296">[Facoltativo] Filtrare le statistiche di integrità tooexclude.</span><span class="sxs-lookup"><span data-stu-id="1e567-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="1e567-297">Se non specificato, le statistiche di integrità hello mostrano il numero di hello di pacchetti del servizio distribuiti negli Stati di integrità ok, avviso e di errore.</span><span class="sxs-lookup"><span data-stu-id="1e567-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-298">API</span><span class="sxs-lookup"><span data-stu-id="1e567-298">API</span></span>
<span data-ttu-id="1e567-299">integrità hello tooget di un'applicazione distribuita in un nodo tramite hello API, creare un `FabricClient` chiamata hello e [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) metodo relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="1e567-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="1e567-300">Utilizzare parametri facoltativi toospecify, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="1e567-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="1e567-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-301">PowerShell</span></span>
<span data-ttu-id="1e567-302">è Hello integrità dell'applicazione hello distribuito cmdlet tooget [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="1e567-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="1e567-303">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="1e567-304">toofind out in cui viene distribuita un'applicazione, eseguire [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ed esaminerà hello distribuiti gli elementi figlio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e567-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="1e567-305">il cmdlet seguente Hello Ottiene integrità hello di hello **fabric: / WordCount** applicazione distribuita in **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="1e567-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="1e567-306">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-306">REST</span></span>
<span data-ttu-id="1e567-307">È possibile ottenere l'integrità dell'applicazione distribuita con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="1e567-308">Get deployed service package health</span><span class="sxs-lookup"><span data-stu-id="1e567-308">Get deployed service package health</span></span>
<span data-ttu-id="1e567-309">Restituisce hello integrità di un'entità di pacchetto del servizio distribuito.</span><span class="sxs-lookup"><span data-stu-id="1e567-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="1e567-310">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-310">Input:</span></span>

* <span data-ttu-id="1e567-311">Nome dell'applicazione hello [obbligatorio] (URI), il nome di nodo (stringa) e nome del manifesto del servizio (string) che identificano hello distribuiti pacchetto del servizio.</span><span class="sxs-lookup"><span data-stu-id="1e567-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="1e567-312">Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="1e567-313">[Facoltativo] Filtri per gli eventi che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori).</span><span class="sxs-lookup"><span data-stu-id="1e567-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="1e567-314">Tutti gli eventi sono di integrità aggregato dell'entità di hello tooevaluate utilizzato, indipendentemente dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-315">API</span><span class="sxs-lookup"><span data-stu-id="1e567-315">API</span></span>
<span data-ttu-id="1e567-316">integrità hello tooget di un pacchetto del servizio distribuito tramite hello API, creare un `FabricClient` chiamata hello e [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) metodo relativo HealthManager.</span><span class="sxs-lookup"><span data-stu-id="1e567-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="1e567-317">Utilizzare parametri facoltativi toospecify, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="1e567-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="1e567-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-318">PowerShell</span></span>
<span data-ttu-id="1e567-319">è Hello integrità del pacchetto del servizio distribuito hello tooget cmdlet [Get ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="1e567-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="1e567-320">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="1e567-321">toosee in cui viene distribuita un'applicazione, eseguire [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ed esaminare le applicazioni distribuita hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="1e567-322">toosee i pacchetti del servizio in un'applicazione, cercare nella hello distribuito gli elementi figlio del pacchetto di servizio in hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span><span class="sxs-lookup"><span data-stu-id="1e567-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="1e567-323">il cmdlet seguente Hello Ottiene integrità hello di hello **WordCountServicePkg** pacchetto del servizio di hello **fabric: / WordCount** applicazione distribuita in **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="1e567-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="1e567-324">entità Hello è **System.Hosting** report per l'attivazione del pacchetto di servizio e del punto di ingresso e tipo di servizio di registrazione corretta.</span><span class="sxs-lookup"><span data-stu-id="1e567-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="1e567-325">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-325">REST</span></span>
<span data-ttu-id="1e567-326">È possibile ottenere l'integrità del pacchetto del servizio distribuito con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="1e567-327">Query sul blocco di integrità</span><span class="sxs-lookup"><span data-stu-id="1e567-327">Health chunk queries</span></span>
<span data-ttu-id="1e567-328">query di blocchi sull'integrità Hello può restituire gli elementi figlio di un cluster a più livelli (ricorsivo), per i filtri di input.</span><span class="sxs-lookup"><span data-stu-id="1e567-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="1e567-329">Supporta i filtri avanzati che consentono una notevole flessibilità nella scelta di elementi figlio di hello toobe restituito.</span><span class="sxs-lookup"><span data-stu-id="1e567-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="1e567-330">i filtri di Hello possono specificare gli elementi figlio da un identificatore univoco hello o altri identificatori di gruppo e/o gli stati di integrità.</span><span class="sxs-lookup"><span data-stu-id="1e567-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="1e567-331">Per impostazione predefinita, non è incluso, come i comandi toohealth anziché sempre includono gli elementi figlio di primo livello elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="1e567-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="1e567-332">Hello [query sull'integrità](service-fabric-view-entities-aggregated-health.md#health-queries) restituiti elementi figlio di primo livello solo di hello specificato entità per i filtri necessari.</span><span class="sxs-lookup"><span data-stu-id="1e567-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="1e567-333">tooget hello figli dei figli di hello, è necessario chiamare integrità altre API per ogni entità di interesse.</span><span class="sxs-lookup"><span data-stu-id="1e567-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="1e567-334">Analogamente, dello stato di hello tooget di entità specifico, è necessario chiamare uno stato API per ogni entità desiderata.</span><span class="sxs-lookup"><span data-stu-id="1e567-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="1e567-335">Hello blocco query filtro avanzato consente toorequest più elementi di interesse in un'unica query, riducendo al minimo la dimensione dei messaggi hello e numero di hello di messaggi.</span><span class="sxs-lookup"><span data-stu-id="1e567-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="1e567-336">il valore di Hello di query di blocco hello è che è possibile ottenere lo stato di integrità per più cluster le entità (potenzialmente tutti i cluster entità a partire dalla radice obbligatorio) in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="1e567-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="1e567-337">È possibile esprimere query sull'integrità complesse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1e567-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="1e567-338">Restituzione solo delle applicazioni con errore e inclusione di tutti i servizi con avviso o errore per queste applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e567-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="1e567-339">Per i servizi restituiti, inclusione di tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="1e567-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="1e567-340">Restituire solo hello dello stato di quattro applicazioni, specificato con i relativi nomi.</span><span class="sxs-lookup"><span data-stu-id="1e567-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="1e567-341">Restituire solo hello dello stato di applicazioni di un tipo di applicazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="1e567-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="1e567-342">Restituzione di tutte le entità distribuite su un nodo.</span><span class="sxs-lookup"><span data-stu-id="1e567-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="1e567-343">Restituisce tutte le applicazioni, tutte le applicazioni distribuite nel nodo specificato hello e tutti i pacchetti hello distribuito servizio su tale nodo.</span><span class="sxs-lookup"><span data-stu-id="1e567-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="1e567-344">Restituzione di tutte le repliche con errore.</span><span class="sxs-lookup"><span data-stu-id="1e567-344">Return all replicas in error.</span></span> <span data-ttu-id="1e567-345">Vengono restituiti tutti i servizi, le applicazioni e le partizioni e le sole repliche con errore.</span><span class="sxs-lookup"><span data-stu-id="1e567-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="1e567-346">Restituzione di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e567-346">Return all applications.</span></span> <span data-ttu-id="1e567-347">Per un servizio specificato, inclusione di tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="1e567-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="1e567-348">Attualmente, query di blocco integrità hello viene esposta solo per entità di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="1e567-349">Restituisce un blocco di integrità del cluster che contiene:</span><span class="sxs-lookup"><span data-stu-id="1e567-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="1e567-350">stato di integrità aggregato cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="1e567-351">Hello integrità stato blocco elenco di nodi che rispettano i filtri di input.</span><span class="sxs-lookup"><span data-stu-id="1e567-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="1e567-352">Hello integrità stato blocco elenco di applicazioni che rispettano i filtri di input.</span><span class="sxs-lookup"><span data-stu-id="1e567-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="1e567-353">Ogni blocco di stato di integrità dell'applicazione contiene un elenco di blocco con tutti i servizi che rispettano i filtri di input e un elenco di blocco con tutte le applicazioni distribuite che rispettano i filtri di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="1e567-354">Uguale per gli elementi figlio hello dei servizi e applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="1e567-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="1e567-355">In questo modo, tutte le entità nel cluster hello possono essere potenzialmente restituite se richiesto, in modo gerarchico.</span><span class="sxs-lookup"><span data-stu-id="1e567-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="1e567-356">Query sul blocco di integrità del cluster</span><span class="sxs-lookup"><span data-stu-id="1e567-356">Cluster health chunk query</span></span>
<span data-ttu-id="1e567-357">Restituisce l'integrità di entità cluster hello hello e contiene blocchi di stato di integrità gerarchica hello di figli obbligatori.</span><span class="sxs-lookup"><span data-stu-id="1e567-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="1e567-358">Input:</span><span class="sxs-lookup"><span data-stu-id="1e567-358">Input:</span></span>

* <span data-ttu-id="1e567-359">Criteri di integrità del cluster [facoltativo] hello utilizzato nodi hello tooevaluate e gli eventi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="1e567-360">Mappa criteri di integrità dell'applicazione di hello [facoltativo], con i criteri di integrità hello utilizzato Criteri di manifesto dell'applicazione hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="1e567-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="1e567-361">[Facoltativo] Filtri per i nodi e le applicazioni che specificano le voci di interesse e devono essere restituite nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="1e567-362">i filtri di Hello sono entità tooan specifico/gruppo di entità o entità tooall applicabile a tale livello.</span><span class="sxs-lookup"><span data-stu-id="1e567-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="1e567-363">elenco di Hello dei filtri può contenere un filtro generale e/o i filtri per le entità con granularità fine toofine identificatori specifici restituiti dalla query hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="1e567-364">Se vuoto, gli elementi figlio hello non vengono restituiti per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1e567-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="1e567-365">Ulteriori informazioni sui filtri hello [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="1e567-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="1e567-366">in modo ricorsivo di Hello applicazione filtri possono specificare i filtri avanzati per gli elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="1e567-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="1e567-367">il risultato di blocco Hello include elementi figlio di hello che rispettano i filtri di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="1e567-368">Attualmente, hello blocco restituiti valutazioni non integro o eventi di entità.</span><span class="sxs-lookup"><span data-stu-id="1e567-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="1e567-369">Informazioni aggiuntive possono essere ottenuti utilizzando query di integrità del cluster esistente hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="1e567-370">API</span><span class="sxs-lookup"><span data-stu-id="1e567-370">API</span></span>
<span data-ttu-id="1e567-371">integrità del cluster tooget blocco, creare un `FabricClient` chiamata hello e [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) metodo relativo **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="1e567-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="1e567-372">È possibile passare [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe criteri di integrità e filtri avanzati.</span><span class="sxs-lookup"><span data-stu-id="1e567-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="1e567-373">Hello codice seguente ottiene il blocco di integrità del cluster con i filtri avanzati.</span><span class="sxs-lookup"><span data-stu-id="1e567-373">hello following code gets cluster health chunk with advanced filters.</span></span>

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

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="1e567-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e567-374">PowerShell</span></span>
<span data-ttu-id="1e567-375">integrità del cluster hello tooget cmdlet Hello è [Get ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="1e567-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="1e567-376">In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e567-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="1e567-377">Hello codice seguente ottiene i nodi solo se sono in errore, ad eccezione di un nodo specifico, deve sempre essere restituito.</span><span class="sxs-lookup"><span data-stu-id="1e567-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
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

<span data-ttu-id="1e567-378">Hello seguente cmdlet Ottiene il blocco di cluster con i filtri di applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e567-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

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

<span data-ttu-id="1e567-379">Hello cmdlet seguente restituisce entità tutti distribuite in un nodo.</span><span class="sxs-lookup"><span data-stu-id="1e567-379">hello following cmdlet returns all deployed entities on a node.</span></span>

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

### <a name="rest"></a><span data-ttu-id="1e567-380">REST</span><span class="sxs-lookup"><span data-stu-id="1e567-380">REST</span></span>
<span data-ttu-id="1e567-381">È possibile ottenere il blocco di integrità del cluster con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) che include criteri di integrità e i filtri avanzati descritti nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="1e567-382">Query generali</span><span class="sxs-lookup"><span data-stu-id="1e567-382">General queries</span></span>
<span data-ttu-id="1e567-383">Le query generali restituiscono l'elenco delle entità di Service Fabric di un tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="1e567-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="1e567-384">Gli oggetti vengono esposti tramite API hello (tramite metodi hello sulla **FabricClient.QueryManager**), i cmdlet di PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="1e567-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="1e567-385">Queste query aggregano sottoquery da più componenti.</span><span class="sxs-lookup"><span data-stu-id="1e567-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="1e567-386">Uno di essi è hello [archivio integrità](service-fabric-health-introduction.md#health-store), che popola hello aggregato dello stato di integrità per ogni risultato della query.</span><span class="sxs-lookup"><span data-stu-id="1e567-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="1e567-387">Le query generale restituiscono hello aggregato di stato di integrità di entità hello e non contengono dati di integrità avanzati.</span><span class="sxs-lookup"><span data-stu-id="1e567-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="1e567-388">Se un'entità non è integra, è possibile giungere a integrità query tooget tutte le informazioni di integrità, inclusi gli eventi, gli stati di integrità figlio e valutazioni non integro.</span><span class="sxs-lookup"><span data-stu-id="1e567-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="1e567-389">Se le query generale restituiscono uno stato sconosciuto per un'entità, è possibile che tale archivio integrità hello non dispone di dati completo sull'entità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="1e567-390">È inoltre possibile che un archivio di integrità toohello sottoquery non è riuscito (ad esempio, si è verificato un errore di comunicazione o dell'archivio integrità hello è stata limitata).</span><span class="sxs-lookup"><span data-stu-id="1e567-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="1e567-391">Follow-up con una query di integrità per entità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="1e567-392">Se la sottoquery hello ha rilevato errori temporanei, ad esempio problemi di rete, questa query follow-up può essere completata.</span><span class="sxs-lookup"><span data-stu-id="1e567-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="1e567-393">Può anche fornire ulteriori dettagli dall'archivio integrità hello sui motivi per cui non è esposta entità hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="1e567-394">le query che contengono Hello **HealthState** per le entità sono:</span><span class="sxs-lookup"><span data-stu-id="1e567-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="1e567-395">Elenco di nodi: restituisce i nodi di elenco hello in cluster hello (paginato).</span><span class="sxs-lookup"><span data-stu-id="1e567-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="1e567-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="1e567-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="1e567-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="1e567-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="1e567-398">Elenco di applicazioni: elenco di hello restituisce delle applicazioni in cluster hello (paginata).</span><span class="sxs-lookup"><span data-stu-id="1e567-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="1e567-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="1e567-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="1e567-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="1e567-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="1e567-401">Elenco di servizio: elenco di hello restituisce dei servizi in un'applicazione (paginata).</span><span class="sxs-lookup"><span data-stu-id="1e567-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="1e567-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="1e567-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="1e567-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="1e567-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="1e567-404">Elenco partizioni: elenco di hello restituisce delle partizioni in un servizio (paginata).</span><span class="sxs-lookup"><span data-stu-id="1e567-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="1e567-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="1e567-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="1e567-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="1e567-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="1e567-407">Elenco di replica: elenco di hello restituisce delle repliche in una partizione (paginata).</span><span class="sxs-lookup"><span data-stu-id="1e567-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="1e567-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="1e567-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="1e567-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="1e567-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="1e567-410">Elenco di applicazioni distribuite: elenco di hello restituisce delle applicazioni distribuite in un nodo.</span><span class="sxs-lookup"><span data-stu-id="1e567-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="1e567-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="1e567-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="1e567-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="1e567-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="1e567-413">Elenco dei pacchetti del servizio distribuito: elenco di hello restituisce dei pacchetti del servizio in un'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="1e567-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="1e567-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="1e567-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="1e567-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="1e567-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="1e567-416">Alcune delle query hello restituiscono risultati di paging.</span><span class="sxs-lookup"><span data-stu-id="1e567-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="1e567-417">Hello delle query viene restituito un elenco derivato da [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="1e567-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="1e567-418">Se i risultati di hello un messaggio non corrispondono, viene restituita solo una pagina e un ContinuationToken che tiene traccia di punto di interruzione di enumerazione.</span><span class="sxs-lookup"><span data-stu-id="1e567-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="1e567-419">Continuare toocall hello stessa query e passare il token di continuazione hello dal hello precedente query tooget successivo dei risultati.</span><span class="sxs-lookup"><span data-stu-id="1e567-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="1e567-420">esempi</span><span class="sxs-lookup"><span data-stu-id="1e567-420">Examples</span></span>
<span data-ttu-id="1e567-421">Hello codice seguente ottiene applicazioni non integre hello cluster hello:</span><span class="sxs-lookup"><span data-stu-id="1e567-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="1e567-422">il cmdlet seguente Hello Ottiene i dettagli dell'applicazione hello per l'infrastruttura di hello: / applicazione WordCount.</span><span class="sxs-lookup"><span data-stu-id="1e567-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="1e567-423">Lo stato di integrità è di tipo avviso.</span><span class="sxs-lookup"><span data-stu-id="1e567-423">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="1e567-424">Hello seguente ottiene servizi hello con uno stato di errore:</span><span class="sxs-lookup"><span data-stu-id="1e567-424">hello following cmdlet gets hello services with a health state of error:</span></span>

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

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="1e567-425">Aggiornamenti del cluster e dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1e567-425">Cluster and application upgrades</span></span>
<span data-ttu-id="1e567-426">Durante un aggiornamento monitorato del cluster hello e dell'applicazione, Service Fabric Controlla integrità tooensure che tutto ciò che resta integro.</span><span class="sxs-lookup"><span data-stu-id="1e567-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="1e567-427">Se un'entità non è integra valutato usando i criteri di integrità configurato, l'aggiornamento di hello Applica azione successiva hello toodetermine di criteri specifici per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1e567-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="1e567-428">aggiornamento Hello sia interazione dell'utente tooallow sospesa (come correggere le condizioni di errore o la modifica dei criteri) oppure potrebbe automaticamente il rollback toohello precedente versione funzionante.</span><span class="sxs-lookup"><span data-stu-id="1e567-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="1e567-429">Durante un *cluster* esegue l'aggiornamento, è possibile ottenere lo stato di aggiornamento cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="1e567-430">stato di aggiornamento Hello include le valutazioni non integro, non è integro cluster hello toowhat quale punto.</span><span class="sxs-lookup"><span data-stu-id="1e567-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="1e567-431">Se l'aggiornamento di hello viene eseguito il rollback a causa di problemi di toohealth, lo stato dell'aggiornamento hello memorizza motivi non integro ultimo hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="1e567-432">Queste informazioni consente agli amministratori di analizzare la causa dell'errore dopo l'aggiornamento di hello rollback o l'arresto.</span><span class="sxs-lookup"><span data-stu-id="1e567-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="1e567-433">Analogamente, durante un *applicazione* esegue l'aggiornamento, tutte le valutazioni integro sono contenute in stato di aggiornamento dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="1e567-434">Hello seguito è riportato lo stato di aggiornamento dell'applicazione hello per un'infrastruttura modificata: / applicazione WordCount.</span><span class="sxs-lookup"><span data-stu-id="1e567-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="1e567-435">Un watchdog ha segnalato un errore in una delle repliche.</span><span class="sxs-lookup"><span data-stu-id="1e567-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="1e567-436">è in corso l'aggiornamento di Hello in quanto i controlli di integrità hello non viene rispettati.</span><span class="sxs-lookup"><span data-stu-id="1e567-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

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

<span data-ttu-id="1e567-437">Altre informazioni su hello [aggiornamento dell'applicazione di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="1e567-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="1e567-438">Utilizzare tootroubleshoot valutazioni di integrità</span><span class="sxs-lookup"><span data-stu-id="1e567-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="1e567-439">Ogni volta che si verifica un problema con il cluster hello o un'applicazione, esaminare toopinpoint di integrità del cluster o l'applicazione hello qual è il problema.</span><span class="sxs-lookup"><span data-stu-id="1e567-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="1e567-440">valutazioni integro Hello forniscono dettagli sulle quali stato non integro corrente hello attivate.</span><span class="sxs-lookup"><span data-stu-id="1e567-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="1e567-441">Se necessario, è possibile scorrere verso il basso causa radice di elementi figlio non integri entità tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="1e567-442">Si consideri, ad esempio, un'applicazione non integra a causa di un errore segnalato in una delle relative repliche.</span><span class="sxs-lookup"><span data-stu-id="1e567-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="1e567-443">Hello cmdlet di Powershell seguente mostra le valutazioni di tipo non integro hello:</span><span class="sxs-lookup"><span data-stu-id="1e567-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

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

<span data-ttu-id="1e567-444">È possibile esaminare hello replica tooget ulteriori informazioni:</span><span class="sxs-lookup"><span data-stu-id="1e567-444">You can look at hello replica tooget more information:</span></span>

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
> <span data-ttu-id="1e567-445">Hello valutazioni problematico mostra hello autorità entità hello è valutata toocurrent lo stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="1e567-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="1e567-446">Potrebbero essere presenti più altri eventi che attivano questo stato, ma non risulteranno in valutazioni hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="1e567-447">tooget ulteriori informazioni, drill-down hello integrità entità toofigure out tutti i report non integro hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1e567-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1e567-448">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e567-448">Next steps</span></span>
[<span data-ttu-id="1e567-449">Utilizzare tootroubleshoot rapporti di integrità sistema</span><span class="sxs-lookup"><span data-stu-id="1e567-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="1e567-450">Aggiungere report sull'integrità di Service Fabric personalizzati</span><span class="sxs-lookup"><span data-stu-id="1e567-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="1e567-451">Come tooreport e controllo del servizio integrità</span><span class="sxs-lookup"><span data-stu-id="1e567-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="1e567-452">Monitorare e diagnosticare servizi in locale</span><span class="sxs-lookup"><span data-stu-id="1e567-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="1e567-453">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="1e567-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
