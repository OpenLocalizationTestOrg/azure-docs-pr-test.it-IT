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
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="5c601-103">Costo di spostamento dei servizi</span><span class="sxs-lookup"><span data-stu-id="5c601-103">Service movement cost</span></span>
<span data-ttu-id="5c601-104">Un fattore che hello gestione delle risorse Cluster dell'infrastruttura del servizio prende in considerazione durante il tentativo toodetermine quali cluster tooa toomake di modifiche è il costo di hello di tali modifiche.</span><span class="sxs-lookup"><span data-stu-id="5c601-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="5c601-105">il concetto di Hello "costo" verrà scambiato con quanti cluster hello possono essere migliorate.</span><span class="sxs-lookup"><span data-stu-id="5c601-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="5c601-106">Il factoring del costo avviene durante lo spostamento di servizi di bilanciamento del carico, la deframmentazione e altri requisiti.</span><span class="sxs-lookup"><span data-stu-id="5c601-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="5c601-107">obiettivo di Hello è requisiti hello toomeet hello almeno modo dannose o costosa.</span><span class="sxs-lookup"><span data-stu-id="5c601-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="5c601-108">Lo spostamento dei servizi comporta costi, come minimo in termini di tempo della CPU e ampiezza di banda della rete.</span><span class="sxs-lookup"><span data-stu-id="5c601-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="5c601-109">Per i servizi con stati, è necessario copiando hello stato di tali servizi, utilizzo disco e memoria aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="5c601-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="5c601-110">Ridurre il costo di hello di soluzioni che hello gestione delle risorse Cluster di Azure Service Fabric è dotato della contribuisce a garantire che le risorse del cluster di hello non impiegate inutilmente.</span><span class="sxs-lookup"><span data-stu-id="5c601-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="5c601-111">Tuttavia, non si desideri tooignore soluzioni che possono migliorare notevolmente allocazione hello di risorse cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c601-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="5c601-112">Gestione delle risorse Cluster Hello ha due modalità di calcolo dei costi e servirsi mentre tenta di cluster hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="5c601-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="5c601-113">primo meccanismo Hello è semplicemente il conteggio ogni spostamento che renderebbe.</span><span class="sxs-lookup"><span data-stu-id="5c601-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="5c601-114">Se vengono generate due soluzioni con hello stesso bilancia (punteggio), quindi hello gestione delle risorse Cluster preferito hello uno con costo più basso (numero totale degli spostamenti) hello.</span><span class="sxs-lookup"><span data-stu-id="5c601-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="5c601-115">Questa strategia funziona bene.</span><span class="sxs-lookup"><span data-stu-id="5c601-115">This strategy works well.</span></span> <span data-ttu-id="5c601-116">Ma come con i carichi predefiniti o statici, è improbabile che in qualsiasi sistema complesso tutti gli spostamenti siano uguali.</span><span class="sxs-lookup"><span data-stu-id="5c601-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="5c601-117">Alcuni sono probabilmente toobe molto più costoso.</span><span class="sxs-lookup"><span data-stu-id="5c601-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="5c601-118">Impostazione dei costi di spostamento</span><span class="sxs-lookup"><span data-stu-id="5c601-118">Setting Move Costs</span></span> 
<span data-ttu-id="5c601-119">Quando viene creato, è possibile specificare hello costo predefinito dello spostamento di un servizio:</span><span class="sxs-lookup"><span data-stu-id="5c601-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="5c601-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c601-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="5c601-121">C#:</span><span class="sxs-lookup"><span data-stu-id="5c601-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="5c601-122">È anche possibile specificare o aggiornare in modo dinamico MoveCost per un servizio dopo aver creato il servizio hello:</span><span class="sxs-lookup"><span data-stu-id="5c601-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="5c601-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c601-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="5c601-124">C#:</span><span class="sxs-lookup"><span data-stu-id="5c601-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="5c601-125">Specificare in modo dinamico il costo di spostamento su base di replica</span><span class="sxs-lookup"><span data-stu-id="5c601-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="5c601-126">Hello frammenti di codice precedente sono tutti per specificare MoveCost per un intero servizio contemporaneamente dal servizio esterno hello stesso.</span><span class="sxs-lookup"><span data-stu-id="5c601-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="5c601-127">Tuttavia, spostare il costo è più utile è quando cambia costo di spostamento hello di un oggetto servizio specifico per la sua durata.</span><span class="sxs-lookup"><span data-stu-id="5c601-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="5c601-128">Poiché hello servizi probabilmente che hello migliore di come costose sono toomove un determinato momento, è un'API per servizi tooreport i propri singolo spostamento dei costi in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5c601-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="5c601-129">C#:</span><span class="sxs-lookup"><span data-stu-id="5c601-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="5c601-130">Impatto del costo di spostamento</span><span class="sxs-lookup"><span data-stu-id="5c601-130">Impact of move cost</span></span>
<span data-ttu-id="5c601-131">MoveCost ha quattro livelli: Zero, Low, Medium e High.</span><span class="sxs-lookup"><span data-stu-id="5c601-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="5c601-132">MoveCosts sono relativo tooeach altri, ad eccezione di Zero.</span><span class="sxs-lookup"><span data-stu-id="5c601-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="5c601-133">Costo pari a zero spostamento significa che lo spostamento è gratuito e deve non inclusi nel conteggio per il punteggio di hello della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="5c601-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="5c601-134">Impostazione Sposta costo tooHigh *non* garantisce che la replica hello rimane in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="5c601-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="5c601-135"><center>
![Costo di spostamento come fattore da considerare per la selezione delle repliche da spostare][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="5c601-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="5c601-136">MoveCost consente di individuare soluzioni hello che causa hello complessiva di un'interruzione minima del e è ancora che pervengono a bilanciare equivalente tooachieve più semplice.</span><span class="sxs-lookup"><span data-stu-id="5c601-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="5c601-137">Nozione di un servizio di costo può essere di tipo toomany relativo.</span><span class="sxs-lookup"><span data-stu-id="5c601-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="5c601-138">Hello più comuni per il calcolo del costo di spostamento sono fattori:</span><span class="sxs-lookup"><span data-stu-id="5c601-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="5c601-139">quantità di Hello di dati che il servizio di hello è toomove o dello stato.</span><span class="sxs-lookup"><span data-stu-id="5c601-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="5c601-140">costo di Hello di disconnessione dei client.</span><span class="sxs-lookup"><span data-stu-id="5c601-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="5c601-141">Lo spostamento di una replica primaria è in genere più costoso costo hello dello spostamento di una replica secondaria.</span><span class="sxs-lookup"><span data-stu-id="5c601-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="5c601-142">costo di Hello di interrompere un'operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="5c601-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="5c601-143">Alcune operazioni dati hello archiviano livello o operazioni eseguite nella chiamata di risposta tooa client sono dispendiose.</span><span class="sxs-lookup"><span data-stu-id="5c601-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="5c601-144">Dopo un certo punto, non si desidera toostop, se non è necessario.</span><span class="sxs-lookup"><span data-stu-id="5c601-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="5c601-145">In modo durante l'operazione di hello in corso, aumento dei costi di spostamento hello di probabilità hello tooreduce oggetto servizio che si sposta.</span><span class="sxs-lookup"><span data-stu-id="5c601-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="5c601-146">Al termine dell'operazione di hello, impostare hello costo indietro toonormal.</span><span class="sxs-lookup"><span data-stu-id="5c601-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="5c601-147">Abilitazione del costo di spostamento del cluster</span><span class="sxs-lookup"><span data-stu-id="5c601-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="5c601-148">Affinché hello più granulare MoveCosts toobe, prendere in considerazione, MoveCost deve essere abilitata nel cluster.</span><span class="sxs-lookup"><span data-stu-id="5c601-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="5c601-149">Senza questa impostazione, modalità predefinita di hello del conteggio spostamenti viene utilizzata per calcolare MoveCost e MoveCost report vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="5c601-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="5c601-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="5c601-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="5c601-151">mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="5c601-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5c601-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c601-152">Next steps</span></span>
- <span data-ttu-id="5c601-153">Gestore di risorse Cluster dell'infrastruttura del servizio utilizza consumo toomanage metriche e la capacità in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c601-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="5c601-154">ulteriori informazioni sulle metriche toolearn come tooconfigure, archiviazione ed estrazione [consumo delle risorse di gestione e il carico in Service Fabric con le metriche](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5c601-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="5c601-155">toolearn sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, estrarre [bilanciamento del carico del cluster di Service Fabric](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="5c601-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
