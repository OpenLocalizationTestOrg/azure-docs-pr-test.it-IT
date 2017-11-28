---
title: "Tipi di nodo di Service Fabric e set di scalabilità di macchine virtuali | Documentazione Microsoft"
description: "Descrive come i tipi di nodo di Service Fabric siano correlati ai set di scalabilità di macchine virtuali e come connettersi in remoto a un'istanza del set di scalabilità di macchine virtuali o a un nodo del cluster."
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
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="e4019-103">Relazione tra i tipi di nodo di Service Fabric e i set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e4019-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="e4019-104">I set di scalabilità di macchine virtuali sono una risorsa di calcolo di Azure che è possibile usare per distribuire e gestire una raccolta di macchine virtuali come set.</span><span class="sxs-lookup"><span data-stu-id="e4019-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="e4019-105">Ogni tipo di nodo definito in un cluster di Service Fabric è configurato come un set di scalabilità di macchine virtuali separato.</span><span class="sxs-lookup"><span data-stu-id="e4019-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="e4019-106">Ogni tipo di nodo può quindi essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse.</span><span class="sxs-lookup"><span data-stu-id="e4019-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="e4019-107">Lo screenshot seguente illustra un cluster con due tipi di nodo: front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="e4019-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="e4019-108">Ogni tipo di nodo ha cinque nodi.</span><span class="sxs-lookup"><span data-stu-id="e4019-108">Each node type has five nodes each.</span></span>

![Screenshot di un cluster con due tipi di nodo][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="e4019-110">Mapping dei set di scalabilità di macchine virtuali ai nodi</span><span class="sxs-lookup"><span data-stu-id="e4019-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="e4019-111">Come si può notare dalla figura precedente, le istanze dei set di scalabilità di macchine virtuali iniziano con l'istanza 0 per poi aumentare.</span><span class="sxs-lookup"><span data-stu-id="e4019-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="e4019-112">La numerazione viene rispecchiata dai nomi.</span><span class="sxs-lookup"><span data-stu-id="e4019-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="e4019-113">Ad esempio, BackEnd_0 è l'istanza 0 del set di scalabilità di macchine virtuali BackEnd.</span><span class="sxs-lookup"><span data-stu-id="e4019-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="e4019-114">Questo particolare set di scalabilità di macchine virtuali ha cinque istanze, denominate BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 e BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="e4019-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="e4019-115">Quando si aumenta un set di scalabilità di macchine virtuali, viene creata una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="e4019-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="e4019-116">La nuova istanza del set di scalabilità di macchine virtuali sarà in genere il nome del set di scalabilità di macchine virtuali + il successivo numero di istanza.</span><span class="sxs-lookup"><span data-stu-id="e4019-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="e4019-117">Nell'esempio sarà BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="e4019-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="e4019-118">Mapping dei servizi di bilanciamento del carico dei set di scalabilità di macchine virtuali a ogni tipo di nodo/set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e4019-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="e4019-119">Se il cluster è stato distribuito dal portale o è stato usato il modello di Resource Manager di esempio fornito, quando si ottiene un elenco di tutte le risorse di un gruppo di risorse, verranno visualizzati i servizi di bilanciamento del carico per ogni set di scalabilità di macchine virtuali o tipo di nodo.</span><span class="sxs-lookup"><span data-stu-id="e4019-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="e4019-120">Il nome sarà simile a: **LB-&lt;nome tipo di nodo&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e4019-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="e4019-121">ad esempio, LB-sfcluster4doc-0, come in questo screenshot:</span><span class="sxs-lookup"><span data-stu-id="e4019-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Risorse][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="e4019-123">Connessione remota a un'istanza di set di scalabilità di macchine virtuali o a un nodo del cluster</span><span class="sxs-lookup"><span data-stu-id="e4019-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="e4019-124">Ogni tipo di nodo definito in un cluster viene configurato come set di scalabilità di macchine virtuali separato.</span><span class="sxs-lookup"><span data-stu-id="e4019-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="e4019-125">I tipi di nodo possono quindi essere aumentati o ridotti in modo indipendente ed essere costituiti da SKU di VM diverse.</span><span class="sxs-lookup"><span data-stu-id="e4019-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="e4019-126">Diversamente dalle VM a istanza singola, le istanze dei set di scalabilità di macchine virtuali non ottengono un proprio indirizzo IP virtuale.</span><span class="sxs-lookup"><span data-stu-id="e4019-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="e4019-127">Può quindi essere difficile cercare un indirizzo IP e una porta da usare per connettersi in remoto a un'istanza specifica.</span><span class="sxs-lookup"><span data-stu-id="e4019-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="e4019-128">Ecco i passaggi che è possibile seguire per trovarli.</span><span class="sxs-lookup"><span data-stu-id="e4019-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="e4019-129">Passaggio 1: Trovare l'indirizzo IP virtuale per il tipo di nodo e quindi le regole NAT in ingresso per RDP</span><span class="sxs-lookup"><span data-stu-id="e4019-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="e4019-130">A questo scopo, è necessario ottenere i valori delle regole NAT in ingresso definiti nell'ambito della definizione di risorse per **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="e4019-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="e4019-131">Nel portale passare al pannello del servizio di bilanciamento del carico e quindi fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="e4019-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![Pannello servizio di bilanciamento del carico][LBBlade]

<span data-ttu-id="e4019-133">In **Impostazioni** fare clic su **Regole NAT in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="e4019-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="e4019-134">Si ottengono così l'indirizzo IP e la porta che è possibile usare per connettersi in remoto alla prima istanza del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e4019-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="e4019-135">Nello screenshot seguente sono **104.42.106.156** e **3389**</span><span class="sxs-lookup"><span data-stu-id="e4019-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![Regole NAT][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="e4019-137">Passaggio 2: Trovare la porta che è possibile usare per connettersi in remoto all'istanza del set di scalabilità di macchine virtuali/nodo specifico</span><span class="sxs-lookup"><span data-stu-id="e4019-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="e4019-138">Nella prima parte di questo documento si è parlato di come venga eseguito il mapping delle istanze dei set di scalabilità di macchine virtuali ai nodi.</span><span class="sxs-lookup"><span data-stu-id="e4019-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="e4019-139">Questa operazione verrà usata per trovare la porta esatta.</span><span class="sxs-lookup"><span data-stu-id="e4019-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="e4019-140">Le porte vengono allocate in ordine crescente nell'istanza del set di scalabilità di macchine virtuali,</span><span class="sxs-lookup"><span data-stu-id="e4019-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="e4019-141">quindi nell'esempio, per il tipo di nodo FrontEnd, le porte per ognuna delle cinque istanze sono le seguenti.</span><span class="sxs-lookup"><span data-stu-id="e4019-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="e4019-142">È ora necessario eseguire lo stesso mapping per l'istanza del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e4019-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="e4019-143">**Istanza del set di scalabilità di macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="e4019-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="e4019-144">**Porta**</span><span class="sxs-lookup"><span data-stu-id="e4019-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="e4019-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="e4019-145">FrontEnd_0</span></span> |<span data-ttu-id="e4019-146">3389</span><span class="sxs-lookup"><span data-stu-id="e4019-146">3389</span></span> |
| <span data-ttu-id="e4019-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="e4019-147">FrontEnd_1</span></span> |<span data-ttu-id="e4019-148">3390</span><span class="sxs-lookup"><span data-stu-id="e4019-148">3390</span></span> |
| <span data-ttu-id="e4019-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="e4019-149">FrontEnd_2</span></span> |<span data-ttu-id="e4019-150">3391</span><span class="sxs-lookup"><span data-stu-id="e4019-150">3391</span></span> |
| <span data-ttu-id="e4019-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="e4019-151">FrontEnd_3</span></span> |<span data-ttu-id="e4019-152">3392</span><span class="sxs-lookup"><span data-stu-id="e4019-152">3392</span></span> |
| <span data-ttu-id="e4019-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="e4019-153">FrontEnd_4</span></span> |<span data-ttu-id="e4019-154">3393</span><span class="sxs-lookup"><span data-stu-id="e4019-154">3393</span></span> |
| <span data-ttu-id="e4019-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="e4019-155">FrontEnd_5</span></span> |<span data-ttu-id="e4019-156">3394</span><span class="sxs-lookup"><span data-stu-id="e4019-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="e4019-157">Passaggio 3: Connettersi in remoto all'istanza specifica del set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e4019-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="e4019-158">Nello screenshot seguente viene usata Connessione Desktop remoto per connettersi a FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="e4019-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="e4019-160">Come modificare i valori dell'intervallo di porte RDP</span><span class="sxs-lookup"><span data-stu-id="e4019-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="e4019-161">Prima della distribuzione cluster</span><span class="sxs-lookup"><span data-stu-id="e4019-161">Before cluster deployment</span></span>
<span data-ttu-id="e4019-162">Quando si configura il cluster usando un modello di Resource Manager, è possibile specificare l'intervallo in **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="e4019-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="e4019-163">Passare alla definizione di risorse per **Microsoft.Network/loadBalancers**,</span><span class="sxs-lookup"><span data-stu-id="e4019-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="e4019-164">in cui si troverà la descrizione per **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="e4019-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="e4019-165">Sostituire i valori *frontendPortRangeStart* e *frontendPortRangeEnd*.</span><span class="sxs-lookup"><span data-stu-id="e4019-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="e4019-167">Dopo la distribuzione cluster</span><span class="sxs-lookup"><span data-stu-id="e4019-167">After cluster deployment</span></span>
<span data-ttu-id="e4019-168">È una procedura un po' più complessa ed è possibile che le VM vengano riciclate.</span><span class="sxs-lookup"><span data-stu-id="e4019-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="e4019-169">Sarà necessario impostare nuovi valori usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4019-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="e4019-170">Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e4019-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="e4019-171">Se non è ancora installato, si consiglia vivamente di seguire la procedura descritta in [Come installare e configurare Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e4019-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="e4019-172">Accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="e4019-172">Sign in to your Azure account.</span></span> <span data-ttu-id="e4019-173">Se per qualche motivo questo comando PowerShell genera un errore, verificare che Azure PowerShell sia installato correttamente.</span><span class="sxs-lookup"><span data-stu-id="e4019-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="e4019-174">Eseguire quanto segue per ottenere i dettagli sul servizio di bilanciamento del carico e visualizzare i valori della descrizione per **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="e4019-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="e4019-175">Impostare *frontendPortRangeEnd* e *frontendPortRangeStart* sui valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="e4019-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="e4019-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e4019-176">Next steps</span></span>
* [<span data-ttu-id="e4019-177">Panoramica della funzionalità "Distribuzione in qualsiasi ambiente" e confronto con i cluster gestiti da Azure</span><span class="sxs-lookup"><span data-stu-id="e4019-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="e4019-178">Sicurezza del cluster</span><span class="sxs-lookup"><span data-stu-id="e4019-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="e4019-179"> Service Fabric SDK e introduzione</span><span class="sxs-lookup"><span data-stu-id="e4019-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
