---
title: aaaService gestione delle risorse dell'infrastruttura Cluster - criteri di posizionamento | Documenti Microsoft
description: Panoramica su altre politiche e regole per i servizi di Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="03862-103">Criteri di posizionamento per i servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="03862-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="03862-104">Criteri di posizionamento sono regole aggiuntive che possono essere utilizzati toogovern posizione del servizio in alcuni scenari specifici, meno comuni.</span><span class="sxs-lookup"><span data-stu-id="03862-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="03862-105">Alcuni esempi di questi scenari sono:</span><span class="sxs-lookup"><span data-stu-id="03862-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="03862-106">Il cluster di Service Fabric si estende nelle distanze geografiche, come più data center locali o in diverse aree di Azure</span><span class="sxs-lookup"><span data-stu-id="03862-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="03862-107">L'ambiente si estende su più aree di controllo di natura geopolitica o legale o un altro caso in cui si dispone dei limiti dei criteri è necessario tooenforce</span><span class="sxs-lookup"><span data-stu-id="03862-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="03862-108">Vi sono considerazioni sulle prestazioni o latenza comunicazioni scadenza toolarge distanze o l'utilizzo di collegamenti di rete lenta o meno affidabile</span><span class="sxs-lookup"><span data-stu-id="03862-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="03862-109">È necessario tookeep determinati carichi di lavoro con condivisione percorso come sforzo, con altri carichi di lavoro o in prossimità toocustomers</span><span class="sxs-lookup"><span data-stu-id="03862-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="03862-110">La maggior parte di questi requisiti si allineano ai layout fisico di hello del cluster di hello, rappresentati come hello domini di errore del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="03862-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="03862-111">Hello avanzata dei criteri di posizionamento che consentono di risolvere che questi scenari sono:</span><span class="sxs-lookup"><span data-stu-id="03862-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="03862-112">Domini non validi</span><span class="sxs-lookup"><span data-stu-id="03862-112">Invalid domains</span></span>
2. <span data-ttu-id="03862-113">Domini obbligatori</span><span class="sxs-lookup"><span data-stu-id="03862-113">Required domains</span></span>
3. <span data-ttu-id="03862-114">Domini preferiti</span><span class="sxs-lookup"><span data-stu-id="03862-114">Preferred domains</span></span>
4. <span data-ttu-id="03862-115">Divieto di compressione della replica</span><span class="sxs-lookup"><span data-stu-id="03862-115">Disallowing replica packing</span></span>

<span data-ttu-id="03862-116">La maggior parte dei seguenti controlli hello è stato possibile configurare le proprietà di nodo e i vincoli di posizionamento, ma alcune sono più complesse.</span><span class="sxs-lookup"><span data-stu-id="03862-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="03862-117">toomake cose più semplici, hello gestione delle risorse Cluster dell'infrastruttura del servizio fornisce questi criteri di posizionamento aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="03862-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="03862-118">I criteri di posizionamento sono configurati in una base all'istanza singola del servizio.</span><span class="sxs-lookup"><span data-stu-id="03862-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="03862-119">Possono anche essere aggiornati in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="03862-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="03862-120">Specifica di domini non validi</span><span class="sxs-lookup"><span data-stu-id="03862-120">Specifying invalid domains</span></span>
<span data-ttu-id="03862-121">Hello **InvalidDomain** toospecify che un particolare dominio di errore non è valido per uno specifico servizio consentono criteri di selezione.</span><span class="sxs-lookup"><span data-stu-id="03862-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="03862-122">Questo criterio garantisce che un particolare servizio non sia mai eseguito in una determinata area, ad esempio per motivi geopolitici o criteri aziendali.</span><span class="sxs-lookup"><span data-stu-id="03862-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="03862-123">È possibile specificare più domini non validi tramite criteri separati.</span><span class="sxs-lookup"><span data-stu-id="03862-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="03862-124"><center>
![Esempio di dominio non valido][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="03862-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="03862-125">Codice:</span><span class="sxs-lookup"><span data-stu-id="03862-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="03862-126">Powershell:</span><span class="sxs-lookup"><span data-stu-id="03862-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="03862-127">Specifica dei domini obbligatori</span><span class="sxs-lookup"><span data-stu-id="03862-127">Specifying required domains</span></span>
<span data-ttu-id="03862-128">Hello necessari criteri di posizionamento di dominio richiedono che il servizio di hello è presente solo nel dominio specificato hello.</span><span class="sxs-lookup"><span data-stu-id="03862-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="03862-129">È possibile specificare più domini richiesti tramite criteri separati.</span><span class="sxs-lookup"><span data-stu-id="03862-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="03862-130"><center>
![Esempio di dominio obbligatorio][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="03862-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="03862-131">Codice:</span><span class="sxs-lookup"><span data-stu-id="03862-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="03862-132">Powershell:</span><span class="sxs-lookup"><span data-stu-id="03862-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="03862-133">Specificare un dominio preferito per le repliche primarie hello di un servizio con stato</span><span class="sxs-lookup"><span data-stu-id="03862-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="03862-134">Dominio primario preferito Hello specifica hello errore dominio tooplace hello primario.</span><span class="sxs-lookup"><span data-stu-id="03862-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="03862-135">Hello primario finisce in questo dominio quando tutto è integro.</span><span class="sxs-lookup"><span data-stu-id="03862-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="03862-136">Se il dominio hello o la replica primaria hello ha esito negativo o viene chiuso, hello primario Sposta toosome altra posizione, idealmente in hello nello stesso dominio.</span><span class="sxs-lookup"><span data-stu-id="03862-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="03862-137">Se non è il nuovo percorso nel dominio preferito hello, hello gestione delle risorse Cluster passa nuovamente dominio preferito toohello appena possibile.</span><span class="sxs-lookup"><span data-stu-id="03862-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="03862-138">Naturalmente questa impostazione è adatta solo ai servizi con stati.</span><span class="sxs-lookup"><span data-stu-id="03862-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="03862-139">Questo criterio è particolarmente utile in cluster distribuiti tra più data center o aree di Azure, ma hanno dei data center che preferiscono la collocazione in una determinata posizione.</span><span class="sxs-lookup"><span data-stu-id="03862-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="03862-140">Conservazione primari chiudere tootheir utenti o altri servizi consente di fornire una latenza più bassa, in particolare per le letture, che sono gestite da componenti primari, per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="03862-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="03862-141"><center>
![Failover e domini primari preferiti][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="03862-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="03862-142">Powershell:</span><span class="sxs-lookup"><span data-stu-id="03862-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="03862-143">Necessità di distribuzione della replica e divieto di compressione</span><span class="sxs-lookup"><span data-stu-id="03862-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="03862-144">Le repliche sono _normalmente_ distribuiti in domini di errore e di aggiornamento quando hello cluster è integro.</span><span class="sxs-lookup"><span data-stu-id="03862-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="03862-145">Tuttavia, vi sono casi in cui più di una replica per una determinata partizione rischia di essere temporaneamente compressa in un singolo dominio.</span><span class="sxs-lookup"><span data-stu-id="03862-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="03862-146">Ad esempio, supponiamo che tale cluster hello dispone di nove nodi in tre domini di errore, fd: / 0, fd: / 1 e fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="03862-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="03862-147">Si supponga anche che il servizio disponga di tre repliche.</span><span class="sxs-lookup"><span data-stu-id="03862-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="03862-148">Si supponga che hello nodi che sono stati utilizzati per le repliche in fd: / 1 e fd: / 2 si è arrestato.</span><span class="sxs-lookup"><span data-stu-id="03862-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="03862-149">In genere hello gestione delle risorse Cluster preferisce altri nodi in tali domini di errore stesso.</span><span class="sxs-lookup"><span data-stu-id="03862-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="03862-150">In questo caso, si supponga che a causa di problemi toocapacity nessuno di hello altri nodi in tali domini sono valide.</span><span class="sxs-lookup"><span data-stu-id="03862-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="03862-151">Se Gestione delle risorse Cluster hello compilazioni sostituzioni per tali repliche, avrebbe toochoose nodi in fd: / 0.</span><span class="sxs-lookup"><span data-stu-id="03862-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="03862-152">Tuttavia, in questo _che_ crea una situazione in cui viene violata hello vincolo di dominio di errore.</span><span class="sxs-lookup"><span data-stu-id="03862-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="03862-153">Compressione aumenta repliche probabilità hello che hello set di repliche intero Impossibile inattività o persi.</span><span class="sxs-lookup"><span data-stu-id="03862-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="03862-154">Per altre informazioni sui vincoli e sulle priorità dei vincoli in generale, vedere [questo argomento](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="03862-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="03862-155">Se viene visualizzato un messaggio di integrità come "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", allora si verifica questa condizione o una condizione simile.</span><span class="sxs-lookup"><span data-stu-id="03862-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="03862-156">In genere solo una o due repliche vengono compresse insieme temporaneamente.</span><span class="sxs-lookup"><span data-stu-id="03862-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="03862-157">Finché sono presenti meno di un quorum di repliche in un dominio specifico, si è sicuri.</span><span class="sxs-lookup"><span data-stu-id="03862-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="03862-158">Compressione rara, ma può verificarsi, e in genere, queste situazioni sono temporanee poiché i nodi di hello tornare.</span><span class="sxs-lookup"><span data-stu-id="03862-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="03862-159">Se i nodi di hello rimanere verso il basso e hello gestione delle risorse Cluster deve toobuild sostituzioni, in genere sono disponibili altri nodi in domini di errore ideale di hello.</span><span class="sxs-lookup"><span data-stu-id="03862-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="03862-160">Alcuni carichi di lavoro preferiscono sempre con numero di destinazione hello di repliche, anche se essi vengono compressi in un minor numero di domini.</span><span class="sxs-lookup"><span data-stu-id="03862-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="03862-161">Questi carichi di lavoro puntano contro la presenza di errori di dominio permanenti totali e simultanei e in genere sono in grado di ripristinare lo stato locale.</span><span class="sxs-lookup"><span data-stu-id="03862-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="03862-162">Altri carichi di lavoro invece richiede tempi di inattività hello precedenti a correttezza rischio o perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="03862-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="03862-163">La maggior parte dei carichi di lavoro di produzione viene eseguita con più di tre repliche, più di tre domini di errore e numerosi nodi validi per ogni dominio di errore.</span><span class="sxs-lookup"><span data-stu-id="03862-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="03862-164">Per questo motivo, hello predefinito che consente la compressione di dominio per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="03862-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="03862-165">comportamento predefinito di Hello consente normale di bilanciamento del carico e failover toohandle questi casi estremi, anche se ciò significa che la compressione dominio temporaneo.</span><span class="sxs-lookup"><span data-stu-id="03862-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="03862-166">Se si desidera toodisable tale compressione per un determinato carico di lavoro, è possibile specificare hello `RequireDomainDistribution` criteri sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="03862-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="03862-167">Quando questo criterio è impostato, hello gestione delle risorse Cluster non garantisce alcun due repliche da hello stessa partizione eseguiti in hello stesso errore o di dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="03862-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="03862-168">Codice:</span><span class="sxs-lookup"><span data-stu-id="03862-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="03862-169">Powershell:</span><span class="sxs-lookup"><span data-stu-id="03862-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="03862-170">A questo punto, sarebbe possibile toouse possibili queste configurazioni per i servizi in un cluster che non è stato geograficamente occupate?</span><span class="sxs-lookup"><span data-stu-id="03862-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="03862-171">È possibile, ma non ce n'è motivo.</span><span class="sxs-lookup"><span data-stu-id="03862-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="03862-172">Hello configurazioni di dominio richiesto non valido e Preferiti devono essere evitate a meno che non li richiedono scenari hello.</span><span class="sxs-lookup"><span data-stu-id="03862-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="03862-173">Può non essere qualsiasi tooforce tootry senso toorun un determinato carico di lavoro in un singolo rack tooprefer alcuni segmenti del cluster locale rispetto a un altro.</span><span class="sxs-lookup"><span data-stu-id="03862-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="03862-174">È necessario distribuire diverse configurazioni hardware tra i domini di errore e gestirle tramite normali vincoli di posizionamento e proprietà dei nodi.</span><span class="sxs-lookup"><span data-stu-id="03862-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03862-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03862-175">Next steps</span></span>
- <span data-ttu-id="03862-176">Per altre informazioni sulla configurazione dei servizi, [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="03862-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
