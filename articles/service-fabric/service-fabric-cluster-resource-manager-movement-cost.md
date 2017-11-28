---
title: Cluster Resource Manager di Service Fabric - Costo dello spostamento | Microsoft Docs
description: Panoramica del costo di spostamento per i servizi di Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5de07c259d1d327d0211338c2911804445dd6b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="3c1c3-103">Costo di spostamento dei servizi</span><span class="sxs-lookup"><span data-stu-id="3c1c3-103">Service movement cost</span></span>
<span data-ttu-id="3c1c3-104">Un fattore preso in considerazione da Cluster Resource Manager di Service Fabric nel tentativo di determinare le modifiche da apportare a un cluster è il costo di tali modifiche.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span></span> <span data-ttu-id="3c1c3-105">Il concetto di "costo" viene compensato sulla base di quanto il cluster può essere migliorato.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-105">The notion of "cost" is traded off against how much the cluster can be improved.</span></span> <span data-ttu-id="3c1c3-106">Il factoring del costo avviene durante lo spostamento di servizi di bilanciamento del carico, la deframmentazione e altri requisiti.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="3c1c3-107">L'obiettivo è soddisfare i requisiti nel modo meno problematico o costoso.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-107">The goal is to meet the requirements in the least disruptive or expensive way.</span></span> 

<span data-ttu-id="3c1c3-108">Lo spostamento dei servizi comporta costi, come minimo in termini di tempo della CPU e ampiezza di banda della rete.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="3c1c3-109">Per i servizi con stato, è necessario copiare lo stato di tali servizi, consumando disco e memoria aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="3c1c3-110">La riduzione del costo delle soluzioni offerta da Cluster Resource Manager di Azure Service Fabric contribuisce a garantire che le risorse del cluster non vengono usate inutilmente.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="3c1c3-111">Ma non bisogna neppure ignorare le soluzioni in grado di migliorare significativamente l'allocazione delle risorse del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="3c1c3-112">Cluster Resource Manager prevede due modalità di calcolo dei costi e del relativo contenimento quando tenta di gestire il cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span></span> <span data-ttu-id="3c1c3-113">Il primo meccanismo è semplicemente il conteggio ogni spostamento che verrebbe eseguito.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-113">The first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="3c1c3-114">Se due soluzioni vengono generate in modo bilanciato, ovvero con un punteggio analogo, Cluster Resource Manager sceglie quella con il costo minore (numero totale degli spostamenti).</span><span class="sxs-lookup"><span data-stu-id="3c1c3-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="3c1c3-115">Questa strategia funziona bene.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-115">This strategy works well.</span></span> <span data-ttu-id="3c1c3-116">Ma come con i carichi predefiniti o statici, è improbabile che in qualsiasi sistema complesso tutti gli spostamenti siano uguali.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="3c1c3-117">Alcuni possono risultare molto più costosi.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-117">Some are likely to be much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="3c1c3-118">Impostazione dei costi di spostamento</span><span class="sxs-lookup"><span data-stu-id="3c1c3-118">Setting Move Costs</span></span> 
<span data-ttu-id="3c1c3-119">È possibile specificare il costo predefinito degli spostamenti di un servizio al momento della creazione:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-119">You can specify the default move cost for a service when it is created:</span></span>

<span data-ttu-id="3c1c3-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="3c1c3-121">C#:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up the rest of the ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="3c1c3-122">È anche possibile specificare o aggiornare in modo dinamico MoveCost per un servizio dopo averlo creato:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span></span> 

<span data-ttu-id="3c1c3-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="3c1c3-124">C#:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="3c1c3-125">Specificare in modo dinamico il costo di spostamento su base di replica</span><span class="sxs-lookup"><span data-stu-id="3c1c3-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="3c1c3-126">I precedenti frammenti di codice sono tutti per la specifica di MoveCost contemporaneamente per un intero servizio all'esterno del servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span></span> <span data-ttu-id="3c1c3-127">Tuttavia, il costo di spostamento è maggiormente utile quando questo cambia per un servizio specifico durante la sua durata.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="3c1c3-128">Poiché i servizi stessi sono a conoscenza del costo del loro spostamento in un determinato momento, è disponibile un'API per i servizi che notifica i singoli costi di spostamento in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span></span> 

<span data-ttu-id="3c1c3-129">C#:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="3c1c3-130">Impatto del costo di spostamento</span><span class="sxs-lookup"><span data-stu-id="3c1c3-130">Impact of move cost</span></span>
<span data-ttu-id="3c1c3-131">MoveCost ha quattro livelli: Zero, Low, Medium e High.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="3c1c3-132">Ad eccezione del livello Zero, tali livelli sono correlati.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-132">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="3c1c3-133">Se un costo di spostamento è di livello Zero, significa che lo spostamento è gratuito e non deve influire sul punteggio della soluzione.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-133">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="3c1c3-134">L'impostazione del costo di spostamento su High *non* garantisce che la replica rimanga in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="3c1c3-135"><center>
![Costo di spostamento come fattore da considerare per la selezione delle repliche da spostare][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="3c1c3-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="3c1c3-136">MoveCost consente di trovare le soluzioni che causano un'interruzione complessivamente minima e che sono più facili da realizzare garantendo allo stesso tempo un bilanciamento equivalente.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="3c1c3-137">Il concetto di costo di un servizio può essere correlato a molti aspetti.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-137">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="3c1c3-138">I fattori più comuni per il calcolo del costo di spostamento sono:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-138">The most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="3c1c3-139">La quantità di stato o dati che il servizio deve spostare.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-139">The amount of state or data that the service has to move.</span></span>
- <span data-ttu-id="3c1c3-140">Il costo di disconnessione dei client.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-140">The cost of disconnection of clients.</span></span> <span data-ttu-id="3c1c3-141">Lo spostamento di una replica primaria è solitamente più costoso dello spostamento di una replica secondaria.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span></span>
- <span data-ttu-id="3c1c3-142">Il costo di interruzione di un'operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-142">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="3c1c3-143">Alcune operazioni a livello di archivio dati o operazioni eseguite in risposta a una chiamata del client sono costose.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-143">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="3c1c3-144">Dopo un certo punto è preferibile non arrestarle se non è indispensabile.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-144">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="3c1c3-145">Durante l'esecuzione dell'operazione, aumentare il costo di spostamento di questo oggetto del servizio per ridurre la probabilità che si sposti.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="3c1c3-146">Al termine dell'operazione, reimpostare il costo sul valore normale.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-146">When the operation is done, you set the cost back to normal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="3c1c3-147">Abilitazione del costo di spostamento del cluster</span><span class="sxs-lookup"><span data-stu-id="3c1c3-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="3c1c3-148">Per considerare il MoveCosts più granulare, è necessario abilitare MoveCost nel cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="3c1c3-149">Senza questa impostazione, viene usata la modalità predefinita per conteggio degli spostamenti per calcolare MoveCost e i report di MoveCost vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="3c1c3-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="3c1c3-151">mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="3c1c3-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="3c1c3-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c1c3-152">Next steps</span></span>
- <span data-ttu-id="3c1c3-153">Cluster Resource Manger di Service Fabric usa le repliche per gestire il consumo e la capacità del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1c3-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="3c1c3-154">Per altre informazioni sulle metriche e sulla relativa configurazione, consultare [Gestione dell'utilizzo delle risorse e del carico in Service Fabric con le metriche](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3c1c3-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="3c1c3-155">Per informazioni sul modo in cui Cluster Resource Manager gestisce e bilancia il carico nel cluster, vedere [Bilanciamento del carico nel cluster di Service Fabric](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="3c1c3-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
