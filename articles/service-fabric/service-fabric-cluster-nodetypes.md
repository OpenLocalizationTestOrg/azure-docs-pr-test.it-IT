---
title: "Infrastruttura aaaService tipi di nodo e il set di scalabilità di macchine Virtuali | Documenti Microsoft"
description: "Descrive come tipi di nodo di Service Fabric correlare tooVM set di scalabilità e la modalità di connessione tooremote tooa istanza del Set di scalabilità della macchina virtuale o un nodo del cluster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="417e4-103">relazione Hello tra set di scalabilità di macchine virtuali e i tipi di nodo di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="417e4-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="417e4-104">Set di scalabilità di macchine virtuali sono una risorsa di calcolo di Azure è possibile utilizzare toodeploy e gestire una raccolta di macchine virtuali come un set.</span><span class="sxs-lookup"><span data-stu-id="417e4-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="417e4-105">Ogni tipo di nodo definito in un cluster di Service Fabric è configurato come un set di scalabilità di macchine virtuali separato.</span><span class="sxs-lookup"><span data-stu-id="417e4-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="417e4-106">Ogni tipo di nodo può quindi essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse.</span><span class="sxs-lookup"><span data-stu-id="417e4-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="417e4-107">Hello cattura di schermata seguente viene illustrato un cluster con due tipi di nodo: front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="417e4-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="417e4-108">Ogni tipo di nodo ha cinque nodi.</span><span class="sxs-lookup"><span data-stu-id="417e4-108">Each node type has five nodes each.</span></span>

![Screenshot di un cluster con due tipi di nodo][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="417e4-110">Mapping di Set di scalabilità della macchina virtuale toonodes istanze</span><span class="sxs-lookup"><span data-stu-id="417e4-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="417e4-111">Come si può notare in precedenza, le istanze di Set di scalabilità della macchina virtuale hello avviare dall'istanza 0 e quindi aumenta.</span><span class="sxs-lookup"><span data-stu-id="417e4-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="417e4-112">numerazione Hello viene riflessa nei nomi di hello.</span><span class="sxs-lookup"><span data-stu-id="417e4-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="417e4-113">Ad esempio, BackEnd_0 è istanza 0 del Set di scalabilità della macchina virtuale back-end hello.</span><span class="sxs-lookup"><span data-stu-id="417e4-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="417e4-114">Questo particolare set di scalabilità di macchine virtuali ha cinque istanze, denominate BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 e BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="417e4-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="417e4-115">Quando si aumenta un set di scalabilità di macchine virtuali, viene creata una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="417e4-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="417e4-116">Hello nuovo Set di scalabilità della macchina virtuale Nome istanza corrisponderà in genere il nome di Set di scalabilità della macchina virtuale hello + numero istanza successivo hello.</span><span class="sxs-lookup"><span data-stu-id="417e4-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="417e4-117">Nell'esempio sarà BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="417e4-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="417e4-118">Mapping VM bilanciamento tooeach nodo tipo/VM Set di scalabilità di caricare set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="417e4-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="417e4-119">Se è stato distribuito il cluster dal portale hello o modello di gestione risorse di esempio hello è forniti, quindi quando si ottiene un elenco di tutte le risorse in un gruppo di risorse non è utilizzato verrà visualizzato servizi di bilanciamento del carico hello per ogni tipo di Set di scalabilità della macchina virtuale o di nodo.</span><span class="sxs-lookup"><span data-stu-id="417e4-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="417e4-120">Hello nome sarebbe simile al seguente: **LB -&lt;nome NodeType&gt;**.</span><span class="sxs-lookup"><span data-stu-id="417e4-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="417e4-121">ad esempio, LB-sfcluster4doc-0, come in questo screenshot:</span><span class="sxs-lookup"><span data-stu-id="417e4-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Risorse][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="417e4-123">Istanza di tooa Set di scalabilità della macchina virtuale o un nodo del cluster della connessione remota</span><span class="sxs-lookup"><span data-stu-id="417e4-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="417e4-124">Ogni tipo di nodo definito in un cluster viene configurato come set di scalabilità di macchine virtuali separato.</span><span class="sxs-lookup"><span data-stu-id="417e4-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="417e4-125">È possibile scalare che indica hello tipi di nodo alto o verso il basso in modo indipendente e può essere costituita da diverse SKU di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="417e4-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="417e4-126">A differenza delle macchine virtuali a singola istanza, le istanze di hello Set di scalabilità della macchina virtuale non si ottengono un indirizzo IP virtuale di propri.</span><span class="sxs-lookup"><span data-stu-id="417e4-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="417e4-127">Pertanto può essere un po' difficile quando si cercano un indirizzo IP indirizzo e la porta che è possibile utilizzare tooremote connettersi tooa specifica istanza.</span><span class="sxs-lookup"><span data-stu-id="417e4-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="417e4-128">Di seguito sono hello è possibile attenersi alla procedura toodiscover li.</span><span class="sxs-lookup"><span data-stu-id="417e4-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="417e4-129">Passaggio 1: Trovare l'indirizzo IP virtuale hello per il tipo di nodo hello e quindi le regole NAT in ingresso per RDP</span><span class="sxs-lookup"><span data-stu-id="417e4-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="417e4-130">Nel tooget ordine, è necessario tooget hello NAT in ingresso, le regole i valori che sono stati definiti come parte della definizione di risorsa hello per **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="417e4-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="417e4-131">Nel portale di hello passare pannello del servizio di bilanciamento carico di toohello e quindi **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="417e4-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![Pannello servizio di bilanciamento del carico][LBBlade]

<span data-ttu-id="417e4-133">In **Impostazioni** fare clic su **Regole NAT in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="417e4-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="417e4-134">A questo punto si hello indirizzo IP e porta che è possibile utilizzare tooremote consente di connettono toohello prima istanza del Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="417e4-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="417e4-135">Nella seguente schermata hello è **104.42.106.156** e **3389**</span><span class="sxs-lookup"><span data-stu-id="417e4-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![Regole NAT][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="417e4-137">Passaggio 2: Individuare porta hello che è possibile utilizzare tooremote connettersi toohello specifico Set di scalabilità della macchina virtuale/nodo dell'istanza</span><span class="sxs-lookup"><span data-stu-id="417e4-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="417e4-138">In questo documento, è parlato mapping toohello nodi di istanze di Set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="417e4-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="417e4-139">Si utilizzerà tale toofigure out hello esatta per la porta.</span><span class="sxs-lookup"><span data-stu-id="417e4-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="417e4-140">porte Hello vengono allocate in ordine crescente dell'istanza di hello Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="417e4-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="417e4-141">Pertanto, in questo esempio per il tipo di nodo front-end hello, porte hello per ognuno dei cinque istanze di hello sono seguente hello.</span><span class="sxs-lookup"><span data-stu-id="417e4-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="417e4-142">è ora necessario toodo hello stesso mapping per l'istanza del Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="417e4-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="417e4-143">**Istanza del set di scalabilità di macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="417e4-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="417e4-144">**Porta**</span><span class="sxs-lookup"><span data-stu-id="417e4-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="417e4-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="417e4-145">FrontEnd_0</span></span> |<span data-ttu-id="417e4-146">3389</span><span class="sxs-lookup"><span data-stu-id="417e4-146">3389</span></span> |
| <span data-ttu-id="417e4-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="417e4-147">FrontEnd_1</span></span> |<span data-ttu-id="417e4-148">3390</span><span class="sxs-lookup"><span data-stu-id="417e4-148">3390</span></span> |
| <span data-ttu-id="417e4-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="417e4-149">FrontEnd_2</span></span> |<span data-ttu-id="417e4-150">3391</span><span class="sxs-lookup"><span data-stu-id="417e4-150">3391</span></span> |
| <span data-ttu-id="417e4-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="417e4-151">FrontEnd_3</span></span> |<span data-ttu-id="417e4-152">3392</span><span class="sxs-lookup"><span data-stu-id="417e4-152">3392</span></span> |
| <span data-ttu-id="417e4-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="417e4-153">FrontEnd_4</span></span> |<span data-ttu-id="417e4-154">3393</span><span class="sxs-lookup"><span data-stu-id="417e4-154">3393</span></span> |
| <span data-ttu-id="417e4-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="417e4-155">FrontEnd_5</span></span> |<span data-ttu-id="417e4-156">3394</span><span class="sxs-lookup"><span data-stu-id="417e4-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="417e4-157">Passaggio 3: Toohello specifica istanza di macchina virtuale del Set di scalabilità della connessione remota</span><span class="sxs-lookup"><span data-stu-id="417e4-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="417e4-158">Utilizzare connessione Desktop remoto tooconnect toohello FrontEnd_1 in hello schermata riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="417e4-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="417e4-160">Come valori di intervallo hello toochange porta RDP</span><span class="sxs-lookup"><span data-stu-id="417e4-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="417e4-161">Prima della distribuzione cluster</span><span class="sxs-lookup"><span data-stu-id="417e4-161">Before cluster deployment</span></span>
<span data-ttu-id="417e4-162">Quando si configura il cluster hello utilizzando un modello di gestione delle risorse, è possibile specificare l'intervallo hello in hello **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="417e4-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="417e4-163">Vai a definizione di risorsa toohello **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="417e4-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="417e4-164">In cui si trova descrizione hello per **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="417e4-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="417e4-165">Sostituire hello *valore finale* e *frontendPortRangeEnd* valori.</span><span class="sxs-lookup"><span data-stu-id="417e4-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="417e4-167">Dopo la distribuzione cluster</span><span class="sxs-lookup"><span data-stu-id="417e4-167">After cluster deployment</span></span>
<span data-ttu-id="417e4-168">Questo è un po' più complicata e può comportare nelle macchine virtuali hello recupero riciclate.</span><span class="sxs-lookup"><span data-stu-id="417e4-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="417e4-169">È ora tooset i nuovi valori utilizzando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="417e4-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="417e4-170">Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="417e4-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="417e4-171">Se non è stata eseguita questa operazione prima di, fortemente consigliabile seguire passaggi descritti nella procedura hello [come tooinstall e configurare Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="417e4-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="417e4-172">Accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="417e4-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="417e4-173">Se per qualche motivo questo comando PowerShell genera un errore, verificare che Azure PowerShell sia installato correttamente.</span><span class="sxs-lookup"><span data-stu-id="417e4-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="417e4-174">Eseguire i seguenti dettagli tooget nel servizio di bilanciamento del carico hello e vengono visualizzati valori hello per descrizione hello per **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="417e4-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="417e4-175">Impostare ora *frontendPortRangeEnd* e *valore finale* toohello valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="417e4-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="417e4-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="417e4-176">Next steps</span></span>
* [<span data-ttu-id="417e4-177">Panoramica sulla funzionalità di "In un punto qualsiasi distribuzione" hello e un confronto con i cluster gestito di Azure</span><span class="sxs-lookup"><span data-stu-id="417e4-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="417e4-178">Sicurezza del cluster</span><span class="sxs-lookup"><span data-stu-id="417e4-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="417e4-179"> Service Fabric SDK e introduzione</span><span class="sxs-lookup"><span data-stu-id="417e4-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
