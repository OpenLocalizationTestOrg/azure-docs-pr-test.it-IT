---
title: governance delle risorse dell'infrastruttura di servizio per contenitori e i servizi aaaAzure | Documenti Microsoft
description: Azure Service Fabric consente toospecify i limiti delle risorse per i servizi in esecuzione all'interno o esterno contenitori.
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
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="361f8-103">Governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="361f8-103">Resource governance</span></span> 

<span data-ttu-id="361f8-104">Quando si eseguono più servizi hello allo stesso nodo o un cluster, è possibile che un servizio può utilizzare più risorse di memoria destinata altri servizi.</span><span class="sxs-lookup"><span data-stu-id="361f8-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="361f8-105">Problema di cui viene fatto riferimento tooas hello vicino fastidioso è il problema.</span><span class="sxs-lookup"><span data-stu-id="361f8-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="361f8-106">Service Fabric consente le prenotazioni di toospecify developer hello e limitazioni per le risorse del servizio tooguarantee e anche di limitare l'utilizzo di risorse.</span><span class="sxs-lookup"><span data-stu-id="361f8-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="361f8-107">Metriche di governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="361f8-107">Resource governance metrics</span></span> 

<span data-ttu-id="361f8-108">In Service Fabric la governance delle risorse è supportata per [pacchetto del servizio](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="361f8-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="361f8-109">risorse Hello assegnati tooService pacchetto possono essere ulteriormente suddivisi tra pacchetti di codice.</span><span class="sxs-lookup"><span data-stu-id="361f8-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="361f8-110">i limiti delle risorse Hello specificati anche trattarsi di prenotazione hello delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="361f8-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="361f8-111">Service Fabric supporta la specifica di CPU e memoria per pacchetto del servizio mediante due [metriche](service-fabric-cluster-resource-manager-metrics.md) predefinite:</span><span class="sxs-lookup"><span data-stu-id="361f8-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="361f8-112">CPU (nome della metrica `ServiceFabric:/_CpuCores`): un core è un core logico disponibile nel computer host hello e tutti i core in tutti i nodi vengono ponderati hello stesso.</span><span class="sxs-lookup"><span data-stu-id="361f8-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="361f8-113">Memoria (il nome della metrica `ServiceFabric:/_MemoryInMB`): viene eseguito il mapping toophysical memoria disponibile nel computer di hello e memoria viene espressa in megabyte.</span><span class="sxs-lookup"><span data-stu-id="361f8-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="361f8-114">Solo le garanzie di riserva soft sono fornite - runtime hello rifiuta l'apertura del nuovo servizio vengono superate le risorse disponibili pacchetti.</span><span class="sxs-lookup"><span data-stu-id="361f8-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="361f8-115">Tuttavia, se un altro file eseguibile o un contenitore viene posizionato sul nodo hello, che potrebbe violare le garanzie di riserva originale hello.</span><span class="sxs-lookup"><span data-stu-id="361f8-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="361f8-116">Per questi due metriche, hello [gestione delle risorse Cluster](service-fabric-cluster-resource-manager-cluster-description.md) tiene traccia delle relative capacità totale del cluster, carico hello in ogni nodo cluster hello, e le risorse cluster hello rimanenti.</span><span class="sxs-lookup"><span data-stu-id="361f8-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="361f8-117">Questi due metriche sono equivalenti tooany altro utente o una metrica personalizzata e possono utilizzare tutte le funzionalità esistenti:</span><span class="sxs-lookup"><span data-stu-id="361f8-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="361f8-118">Può essere cluster [bilanciato](service-fabric-cluster-resource-manager-balancing.md) in base a metriche toothese due (comportamento predefinito).</span><span class="sxs-lookup"><span data-stu-id="361f8-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="361f8-119">Può essere cluster [deframmentati](service-fabric-cluster-resource-manager-defragmentation-metrics.md) in base a metriche toothese due.</span><span class="sxs-lookup"><span data-stu-id="361f8-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="361f8-120">Quando si [descrive un cluster](service-fabric-cluster-resource-manager-cluster-description.md), è possibile impostare il buffer di capacità per queste due metriche.</span><span class="sxs-lookup"><span data-stu-id="361f8-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="361f8-121">La [creazione di report sul carico dinamico](service-fabric-cluster-resource-manager-metrics.md) non è supportata per queste metriche e i relativi carichi vengono definiti al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="361f8-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="361f8-122">Configurazione del cluster per l'abilitazione della governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="361f8-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="361f8-123">La capacità deve essere definita manualmente in ogni tipo di nodo nel cluster hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="361f8-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="361f8-124">La governance delle risorse è consentita solo per i servizi utente, non per qualsiasi servizio di sistema.</span><span class="sxs-lookup"><span data-stu-id="361f8-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="361f8-125">Quando si specifica la capacità, è necessario lasciare non allocate alcune memorie centrali e parte della memoria per i servizi di sistema.</span><span class="sxs-lookup"><span data-stu-id="361f8-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="361f8-126">Per prestazioni ottimali, hello dopo l'impostazione deve inoltre essere attivata nel manifesto del cluster hello:</span><span class="sxs-lookup"><span data-stu-id="361f8-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="361f8-127">Specifica della governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="361f8-127">Specifying resource governance</span></span> 

<span data-ttu-id="361f8-128">I limiti di governance delle risorse vengono specificati nel manifesto dell'applicazione hello (sezione oggetto ServiceManifestImport) come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="361f8-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
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
  
<span data-ttu-id="361f8-129">In questo esempio, pacchetto del servizio ServicePackageA Ottiene uno dei core nei nodi hello in cui viene inserito.</span><span class="sxs-lookup"><span data-stu-id="361f8-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="361f8-130">Questo pacchetto del servizio contiene due pacchetti di codice (CodeA1 e CodeA2) e specificano hello `CpuShares` parametro.</span><span class="sxs-lookup"><span data-stu-id="361f8-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="361f8-131">percentuale di Hello di CpuShares 512:256 divide core hello tra due pacchetti di codice hello.</span><span class="sxs-lookup"><span data-stu-id="361f8-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="361f8-132">Pertanto, in questo esempio, CodeA1 Ottiene due terzi di un core e CodeA2 Ottiene un terzo di un core e una prenotazione soft garanzia di hello stesso.</span><span class="sxs-lookup"><span data-stu-id="361f8-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="361f8-133">Nel caso in cui CpuShares quando non vengono specificati per i pacchetti di codice, Service Fabric divide core hello in modo uniforme tra essi.</span><span class="sxs-lookup"><span data-stu-id="361f8-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="361f8-134">I limiti di memoria sono assoluti, in modo che entrambi i pacchetti di codice siano limitate too1024 MB di memoria (e una prenotazione soft garanzia di hello stesso).</span><span class="sxs-lookup"><span data-stu-id="361f8-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="361f8-135">Pacchetti di codice (contenitori o processi) non sono in grado di tooallocate più memoria rispetto a questo limite e il tentativo di toodo operazione genera un'eccezione di memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="361f8-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="361f8-136">Per risorse limite imposizione toowork, tutti i pacchetti di codice all'interno di un pacchetto del servizio devono avere i limiti di memoria specificati.</span><span class="sxs-lookup"><span data-stu-id="361f8-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="361f8-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="361f8-137">Next steps</span></span>
* <span data-ttu-id="361f8-138">toolearn più sulla gestione delle risorse Cluster, leggere questo [articolo](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="361f8-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="361f8-139">toolearn più sul modello di applicazione, pacchetti, pacchetti di codice e toothem le corrispondenze tra le repliche di leggere questo [articolo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="361f8-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
