---
title: "Scalabilità a livello di codice di Azure Service Fabric | Documentazione Microsoft"
description: Aumentare o ridurre le istanze di un cluster Service Fabric in Azure a livello di codice in base a trigger personalizzati
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="b3770-103">Aumentare o ridurre le istanze di un cluster di Service Fabric a livello di codice</span><span class="sxs-lookup"><span data-stu-id="b3770-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="b3770-104">Le nozioni di base sulla scalabilità di un cluster Service Fabric in Azure sono trattate nella documentazione sulla [scalabilità del cluster](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="b3770-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="b3770-105">Questo articolo descrive come i cluster Service Fabric sono costruiti su set di scalabilità di macchine virtuali ed è possibile ottenere la scalabilità manualmente o usando regole di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="b3770-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="b3770-106">Vengono esaminati i metodi a livello di codice per il coordinamento delle operazioni di scalabilità in Azure per scenari più avanzati.</span><span class="sxs-lookup"><span data-stu-id="b3770-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="b3770-107">Motivi per eseguire la scalabilità a livello di codice</span><span class="sxs-lookup"><span data-stu-id="b3770-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="b3770-108">In molti scenari, la scalabilità manuale o mediante regole di scalabilità automatica sono soluzioni valide.</span><span class="sxs-lookup"><span data-stu-id="b3770-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="b3770-109">In altri scenari, tuttavia, potrebbero non essere la scelta adatta.</span><span class="sxs-lookup"><span data-stu-id="b3770-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="b3770-110">Alcuni potenziali svantaggi di questi approcci sono:</span><span class="sxs-lookup"><span data-stu-id="b3770-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="b3770-111">La scalabilità manuale richiede l'accesso e la richiesta esplicita delle operazioni di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b3770-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="b3770-112">Questo approccio potrebbe non essere una soluzione valida se le operazioni di scalabilità vengono richieste di frequente oppure in momenti imprevisti.</span><span class="sxs-lookup"><span data-stu-id="b3770-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="b3770-113">Quando le regole di scalabilità automatica rimuovono un'istanza da un set di scalabilità di macchine virtuali, non rimuovono automaticamente le informazioni di questo nodo dal cluster Service Fabric associato, a meno che il tipo di nodo non disponga di un livello di durabilità Silver o Gold.</span><span class="sxs-lookup"><span data-stu-id="b3770-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="b3770-114">Poiché funzionano a livello di set di scalabilità anziché a livello di Service Fabric, le regole di scalabilità automatica possono rimuovere i nodi Service Fabric senza arrestarli in modo normale.</span><span class="sxs-lookup"><span data-stu-id="b3770-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="b3770-115">Questo tipo di rimozione dei nodi lascerà il nodo Service Fabric nello stato "ghost" dopo le operazioni di riduzione delle istanze.</span><span class="sxs-lookup"><span data-stu-id="b3770-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="b3770-116">Un utente o un servizio dovrà pulire periodicamente lo stato del nodo rimosso nel cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3770-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="b3770-117">Si noti che un tipo di nodo con un livello di durabilità Gold o Silver eseguirà automaticamente la pulizia dei nodi rimossi.</span><span class="sxs-lookup"><span data-stu-id="b3770-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="b3770-118">Anche se le regole di scalabilità automatica supportano [molte metriche](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), si tratta comunque di un set limitato.</span><span class="sxs-lookup"><span data-stu-id="b3770-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="b3770-119">Se lo scenario richiede la scalabilità basata su alcune metriche non incluse in questo set, le regole di scalabilità automatica potrebbero non essere una soluzione valida.</span><span class="sxs-lookup"><span data-stu-id="b3770-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="b3770-120">Considerando queste limitazioni, è consigliabile implementare più modelli di scalabilità automatica personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b3770-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="b3770-121">Scalabilità delle API</span><span class="sxs-lookup"><span data-stu-id="b3770-121">Scaling APIs</span></span>
<span data-ttu-id="b3770-122">Esistono API Azure che consentono alle applicazioni di usare a livello di codice i set di scalabilità di macchine virtuali e i cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3770-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="b3770-123">Se le opzioni di scalabilità automatica esistenti non funzionano per lo scenario specifico, queste API consentono di implementare una logica di scalabilità personalizzata.</span><span class="sxs-lookup"><span data-stu-id="b3770-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="b3770-124">Un approccio all'implementazione di questa funzionalità di scalabilità automatica "interna" consiste nell'aggiungere un nuovo servizio senza stato all'applicazione Service Fabric per gestire le operazioni di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b3770-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="b3770-125">All'interno del metodo `RunAsync` del servizio, un set di trigger può determinare se la scalabilità è necessaria, inclusi i parametri di controllo, come la dimensione massima di un cluster e i tempi di raffreddamento della scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b3770-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="b3770-126">L'API usata per le interazioni dei set di scalabilità di macchine virtuali, sia per verificare il numero corrente di istanze di macchine virtuali che per modificarlo, è la [libreria Azure Management Compute Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="b3770-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="b3770-127">La libreria Fluent fornisce un'API facile da usare per l'interazione con i set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b3770-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="b3770-128">Per interagire con il cluster Service Fabric, usare [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="b3770-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="b3770-129">Naturalmente non è necessario che il codice di scalabilità sia in esecuzione come servizio nel cluster di cui modificare la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b3770-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="b3770-130">Sia `IAzure` sia `FabricClient` possono connettersi in remoto alle risorse di Azure associate; il servizio di scalabilità può quindi essere facilmente un'applicazione console o il servizio Windows in esecuzione dall'esterno dell'applicazione Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3770-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="b3770-131">Gestione delle credenziali</span><span class="sxs-lookup"><span data-stu-id="b3770-131">Credential management</span></span>
<span data-ttu-id="b3770-132">Un problema in fase di scrittura di un servizio per gestire la scalabilità è che il servizio deve essere in grado di accedere alle risorse dei set di scalabilità di macchine virtuali senza un accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="b3770-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="b3770-133">L'accesso al cluster Service Fabric è semplice se il servizio di scalabilità sta modificando la propria applicazione Service Fabric, ma sono necessarie le credenziali per accedere al set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b3770-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="b3770-134">Per accedere, è possibile usare un'[entità servizio](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) creata con l'[interfaccia della riga di comando di Azure 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b3770-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="b3770-135">È possibile creare un'entità servizio con i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3770-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="b3770-136">Accedere all'interfaccia della riga di comando di Azure (`az login`) come utente con accesso al set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="b3770-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="b3770-137">Creare l'entità servizio con `az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="b3770-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="b3770-138">Prendere nota di appId (denominato altrove "ID client"), nome, password e tenant per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="b3770-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="b3770-139">Sarà inoltre necessario l'ID sottoscrizione, che può essere visualizzato con `az account list`</span><span class="sxs-lookup"><span data-stu-id="b3770-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="b3770-140">La libreria di calcolo Fluent può eseguire l'accesso usando queste credenziali come indicato di seguito. Si noti che i tipi di Azure fluent principali, ad esempio `IAzure`, sono nel pacchetto [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/):</span><span class="sxs-lookup"><span data-stu-id="b3770-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="b3770-141">Una volta eseguito l'accesso, è possibile eseguire una query del numero di istanze di set di scalabilità tramite `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="b3770-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="b3770-142">Aumento del numero di istanze</span><span class="sxs-lookup"><span data-stu-id="b3770-142">Scaling out</span></span>
<span data-ttu-id="b3770-143">Usando l'SDK di calcolo di Azure Fluent è possibile aggiungere istanze al set di scalabilità di macchine virtuali con poche chiamate.</span><span class="sxs-lookup"><span data-stu-id="b3770-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="b3770-144">In alternativa, le dimensioni del set di scalabilità di macchine virtuali possono essere gestite anche con i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3770-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="b3770-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) consente di recuperare l'oggetto set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b3770-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="b3770-146">La capacità corrente verrà archiviata nella proprietà `.sku.capacity`.</span><span class="sxs-lookup"><span data-stu-id="b3770-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="b3770-147">Dopo avere impostato la capacità sul valore desiderato, il set di scalabilità di macchine virtuali in Azure può essere aggiornato con il comando [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="b3770-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="b3770-148">Quando si aggiunge manualmente un nodo, l'aggiunta di un'istanza del set di scalabilità dovrebbe essere sufficiente per avviare un nuovo nodo Service Fabric in quanto il modello del set di scalabilità include le estensioni per aggiungere automaticamente nuove istanze al cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3770-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="b3770-149">Riduzione</span><span class="sxs-lookup"><span data-stu-id="b3770-149">Scaling in</span></span>

<span data-ttu-id="b3770-150">La riduzione è simile all'aumento del numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="b3770-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="b3770-151">Le modifiche effettive al set di scalabilità di macchine virtuali sono praticamente le stesse.</span><span class="sxs-lookup"><span data-stu-id="b3770-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="b3770-152">Tuttavia, come illustrato in precedenza, Service Fabric pulisce automaticamente solo i nodi rimossi con la durabilità Gold o Silver.</span><span class="sxs-lookup"><span data-stu-id="b3770-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="b3770-153">Pertanto, nel caso di riduzione con la durabilità Bronze, è necessario interagire con il cluster Service Fabric per arrestare il nodo da rimuovere, quindi rimuovere il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="b3770-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="b3770-154">La preparazione del nodo per l'arresto implica la ricerca del nodo da rimuovere, ovvero il nodo aggiunto più di recente, e la relativa disattivazione.</span><span class="sxs-lookup"><span data-stu-id="b3770-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="b3770-155">Per i nodi non di inizializzazione, è possibile trovare i nodi più recenti confrontando il valore `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="b3770-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="b3770-156">Tenere presente che i nodi di *inizializzazione* non seguotno apparentemente sempre la convenzione per cui gli ID di istanza maggiori verranno rimossi per primi.</span><span class="sxs-lookup"><span data-stu-id="b3770-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="b3770-157">Dopo avere individuato il nodo da rimuovere, questo può essere disattivato e rimosso usando la stessa istanza `FabricClient` e l'istanza `IAzure` precedente.</span><span class="sxs-lookup"><span data-stu-id="b3770-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="b3770-158">Anche in questo caso, come per l'aumento del numero di istanze, è possibile usare i cmdlet di PowerShell per modificare la capacità del set di scalabilità di macchine virtuali, se si preferisce un approccio basato sugli script.</span><span class="sxs-lookup"><span data-stu-id="b3770-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="b3770-159">Dopo avere rimosso l'istanza di macchina virtuale, è possibile rimuovere lo stato del nodo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3770-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="b3770-160">Potenziali svantaggi</span><span class="sxs-lookup"><span data-stu-id="b3770-160">Potential drawbacks</span></span>

<span data-ttu-id="b3770-161">Come illustrato nei frammenti di codice precedenti, la creazione di un servizio di scalabilità proprio offre il massimo livello di controllo e personalizzazione sul comportamento di scalabilità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b3770-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="b3770-162">Questa condizione può essere utile negli scenari che richiedono un controllo preciso su quando e come aumentare o ridurre il numero di istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b3770-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="b3770-163">Tuttavia, questo controllo implica un compromesso a livello di complessità del codice.</span><span class="sxs-lookup"><span data-stu-id="b3770-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="b3770-164">Questo approccio richiede un codice di scalabilità proprio, il che non è semplice.</span><span class="sxs-lookup"><span data-stu-id="b3770-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="b3770-165">L'approccio da scegliere per la scalabilità di Service Fabric dipende dallo scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="b3770-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="b3770-166">Se la scalabilità non è comune, la possibilità di aggiungere o rimuovere nodi manualmente è probabilmente sufficiente.</span><span class="sxs-lookup"><span data-stu-id="b3770-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="b3770-167">Per gli scenari più complessi, gli SDK e le regole di scalabilità automatica che espongono la capacità di eseguire la scalabilità a livello di codice offrono alternative molto efficaci.</span><span class="sxs-lookup"><span data-stu-id="b3770-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3770-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3770-168">Next steps</span></span>

<span data-ttu-id="b3770-169">Per iniziare a implementare la logica di scalabilità automatica, acquisire familiarità con i seguenti concetti e le utili API:</span><span class="sxs-lookup"><span data-stu-id="b3770-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="b3770-170">Scalabilità manuale o con regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="b3770-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="b3770-171">[Fluent Azure Management Libraries per .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (utili per l'interazione con i set di scalabilità di macchine virtuali sottostanti del cluster Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="b3770-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="b3770-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (utile per l'interazione con un cluster Service Fabric e i relativi nodi)</span><span class="sxs-lookup"><span data-stu-id="b3770-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
