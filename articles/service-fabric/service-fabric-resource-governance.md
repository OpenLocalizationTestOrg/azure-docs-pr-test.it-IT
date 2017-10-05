---
title: Governance delle risorse di Azure Service Fabric per contenitori e i servizi | Microsoft Docs
description: Azure Service Fabric consente di specificare limiti di risorse per i servizi in esecuzione all'interno o all'esterno di contenitori.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88d44953ad83f9e7401fd087a39842e4a3790124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="resource-governance"></a><span data-ttu-id="8089f-103">Governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="8089f-103">Resource governance</span></span> 

<span data-ttu-id="8089f-104">Quando si eseguono più servizi sullo stesso nodo o cluster, è possibile che uno di essi consumi molte risorse a scapito degli altri.</span><span class="sxs-lookup"><span data-stu-id="8089f-104">When running multiple services on the same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="8089f-105">Questo problema prende il nome di noisy neighbor effect.</span><span class="sxs-lookup"><span data-stu-id="8089f-105">This problem is referred to as the noisy-neighbor problem.</span></span> <span data-ttu-id="8089f-106">Service Fabric consente allo sviluppatore di specificare prenotazioni e limiti per servizio in modo da garantire le risorse e limitarne l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="8089f-106">Service Fabric allows the developer to specify reservations and limits per service to guarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="8089f-107">Metriche di governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="8089f-107">Resource governance metrics</span></span> 

<span data-ttu-id="8089f-108">In Service Fabric la governance delle risorse è supportata per [pacchetto del servizio](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="8089f-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="8089f-109">Le risorse assegnate a un pacchetto del servizio possono essere ulteriormente divise tra pacchetti di codice.</span><span class="sxs-lookup"><span data-stu-id="8089f-109">The resources that are assigned to Service Package can be further divided between code packages.</span></span> <span data-ttu-id="8089f-110">I limiti di risorse specificati implicano anche la prenotazione delle stesse.</span><span class="sxs-lookup"><span data-stu-id="8089f-110">The resource limits specified also mean the reservation of the resources.</span></span> <span data-ttu-id="8089f-111">Service Fabric supporta la specifica di CPU e memoria per pacchetto del servizio mediante due [metriche](service-fabric-cluster-resource-manager-metrics.md) predefinite:</span><span class="sxs-lookup"><span data-stu-id="8089f-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="8089f-112">CPU (nome della metrica `ServiceFabric:/_CpuCores`): una memoria centrale è una memoria centrale logica disponibile nel computer host. Tutte le memorie centrali in tutti i nodi vengono ponderate nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="8089f-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on the host machine, and all cores across all nodes are weighted the same.</span></span>
* <span data-ttu-id="8089f-113">Memoria (nome della metrica `ServiceFabric:/_MemoryInMB`): la memoria viene espressa in megabyte ed esegue il mapping alla memoria fisica disponibile nel computer.</span><span class="sxs-lookup"><span data-stu-id="8089f-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps to physical memory that is available on the machine.</span></span>

<span data-ttu-id="8089f-114">Vengono fornite solo garanzie di prenotazione flessibile: il runtime rifiuta l'apertura di nuovi pacchetti del servizio se vengono superate le risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="8089f-114">Only soft reservation guarantees are provided - the runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="8089f-115">Tuttavia, se nel nodo viene posizionato un altro file eseguibile o un contenitore, tale elemento può superare le garanzie di prenotazione originali.</span><span class="sxs-lookup"><span data-stu-id="8089f-115">However, if another executable or container is placed on the node, that may violate the original reservation guarantees.</span></span>

<span data-ttu-id="8089f-116">Per queste due metriche, [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) rileva la capacità totale del cluster, il carico presente su ciascun nodo e le restanti risorse del cluster.</span><span class="sxs-lookup"><span data-stu-id="8089f-116">For these two metrics, the [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, the load on each node in the cluster, and, remaining resources in the cluster.</span></span> <span data-ttu-id="8089f-117">Queste due metriche sono equivalenti a qualsiasi altra metrica dell'utente o personalizzata e possono essere usate con tutte le funzionalità esistenti:</span><span class="sxs-lookup"><span data-stu-id="8089f-117">These two metrics are equivalent to any other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="8089f-118">Il cluster può essere [bilanciato](service-fabric-cluster-resource-manager-balancing.md) in base a queste due metriche (comportamento predefinito).</span><span class="sxs-lookup"><span data-stu-id="8089f-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according to these two metrics (default behavior).</span></span>
* <span data-ttu-id="8089f-119">Il cluster può essere [deframmentato](service-fabric-cluster-resource-manager-defragmentation-metrics.md) in base a queste due metriche.</span><span class="sxs-lookup"><span data-stu-id="8089f-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according to these two metrics.</span></span>
* <span data-ttu-id="8089f-120">Quando si [descrive un cluster](service-fabric-cluster-resource-manager-cluster-description.md), è possibile impostare il buffer di capacità per queste due metriche.</span><span class="sxs-lookup"><span data-stu-id="8089f-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="8089f-121">La [creazione di report sul carico dinamico](service-fabric-cluster-resource-manager-metrics.md) non è supportata per queste metriche e i relativi carichi vengono definiti al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="8089f-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="8089f-122">Configurazione del cluster per l'abilitazione della governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="8089f-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="8089f-123">È necessario definire manualmente la capacità in ogni tipo di nodo del cluster nel modo indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8089f-123">Capacity should be defined manually in each node type in the cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="8089f-124">La governance delle risorse è consentita solo per i servizi utente, non per qualsiasi servizio di sistema.</span><span class="sxs-lookup"><span data-stu-id="8089f-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="8089f-125">Quando si specifica la capacità, è necessario lasciare non allocate alcune memorie centrali e parte della memoria per i servizi di sistema.</span><span class="sxs-lookup"><span data-stu-id="8089f-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="8089f-126">Per ottenere prestazioni ottimali, nel manifesto del cluster è necessario attivare anche l'impostazione seguente:</span><span class="sxs-lookup"><span data-stu-id="8089f-126">For optimal performance, the following setting should also be turned on in the cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="8089f-127">Specifica della governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="8089f-127">Specifying resource governance</span></span> 

<span data-ttu-id="8089f-128">I limiti di governance delle risorse vengono specificati nel manifesto dell'applicazione (sezione ServiceManifestImport) come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8089f-128">Resource governance limits are specified in the application manifest (ServiceManifestImport section) as shown in the following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has the number of CPU cores defined, but doesn't have the MemoryInMB defined.
  In this case, Service Fabric will sum the limits on code packages and uses the sum as 
  the overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="8089f-129">In questo esempio il pacchetto del servizio ServicePackageA ottiene una memoria centrale sui nodi in cui è posizionato.</span><span class="sxs-lookup"><span data-stu-id="8089f-129">In this example, service package ServicePackageA gets one core on the nodes where it is placed.</span></span> <span data-ttu-id="8089f-130">Il pacchetto del servizio contiene due pacchetti di codice, CodeA1 e CodeA2, che specificano entrambi il parametro `CpuShares`.</span><span class="sxs-lookup"><span data-stu-id="8089f-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify the `CpuShares` parameter.</span></span> <span data-ttu-id="8089f-131">La proporzione CpuShares 512:256 divide la memoria centrale tra i due pacchetti di codice.</span><span class="sxs-lookup"><span data-stu-id="8089f-131">The proportion of CpuShares 512:256  divides the core across the two code packages.</span></span> <span data-ttu-id="8089f-132">Di conseguenza, in questo esempio CodeA1 ottiene due terzi di una memoria centrale e CodeA2 ne ottiene un terzo, oltre a una prenotazione con garanzia flessibile sulla stessa.</span><span class="sxs-lookup"><span data-stu-id="8089f-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="8089f-133">Nel caso in cui CpuShares non sia specificato per i pacchetti di codice, Service Fabric divide le memorie centrali in parti uguali tra di essi.</span><span class="sxs-lookup"><span data-stu-id="8089f-133">In case when CpuShares are not specified for code packages, Service Fabric divides the cores equally among them.</span></span>

<span data-ttu-id="8089f-134">I limiti di memoria sono assoluti, motivo per cui i pacchetti di codice sono limitati a 1024 MB di memoria, con prenotazione a garanzia flessibile.</span><span class="sxs-lookup"><span data-stu-id="8089f-134">Memory limits are absolute, so both code packages are limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="8089f-135">I pacchetti di codice (contenitori o pacchetti) non sono in grado di allocare una quantità di memoria superiore a questo limite. Un'operazione di questo tipo genererebbe un'eccezione di memoria esaurita.</span><span class="sxs-lookup"><span data-stu-id="8089f-135">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="8089f-136">Perché l'imposizione di un limite di risorse funzioni, è necessario che tutti i pacchetti di codice inclusi in un pacchetto del servizio abbiano limiti di memoria specificati.</span><span class="sxs-lookup"><span data-stu-id="8089f-136">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8089f-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8089f-137">Next steps</span></span>
* <span data-ttu-id="8089f-138">Per altre informazioni su Cluster Resource Manager, leggere questo [articolo](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8089f-138">To learn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="8089f-139">Per altre informazioni sul modello dell'applicazione, i pacchetti del servizio e i pacchetti di codice, nonché sul mapping delle repliche a tali elementi, leggere questo [articolo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="8089f-139">To learn more about application model, service packages, code packages and how replicas map to them read this [article](service-fabric-application-model.md).</span></span>
