---
title: "Scalabilità a livello di codice dell'infrastruttura di servizio aaaAzure | Documenti Microsoft"
description: "Scalabilità di un cluster di Azure Service Fabric in o out in base a livello di programmazione di trigger toocustom"
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
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="2c5de-103">Aumentare o ridurre le istanze di un cluster di Service Fabric a livello di codice</span><span class="sxs-lookup"><span data-stu-id="2c5de-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="2c5de-104">Le nozioni di base sulla scalabilità di un cluster Service Fabric in Azure sono trattate nella documentazione sulla [scalabilità del cluster](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="2c5de-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="2c5de-105">Questo articolo descrive come i cluster Service Fabric sono costruiti su set di scalabilità di macchine virtuali ed è possibile ottenere la scalabilità manualmente o usando regole di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="2c5de-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="2c5de-106">Vengono esaminati i metodi a livello di codice per il coordinamento delle operazioni di scalabilità in Azure per scenari più avanzati.</span><span class="sxs-lookup"><span data-stu-id="2c5de-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="2c5de-107">Motivi per eseguire la scalabilità a livello di codice</span><span class="sxs-lookup"><span data-stu-id="2c5de-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="2c5de-108">In molti scenari, la scalabilità manuale o mediante regole di scalabilità automatica sono soluzioni valide.</span><span class="sxs-lookup"><span data-stu-id="2c5de-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="2c5de-109">In altri scenari, tuttavia, possono non essere hello adatta a destra.</span><span class="sxs-lookup"><span data-stu-id="2c5de-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="2c5de-110">Approcci di potenziali svantaggi toothese includono:</span><span class="sxs-lookup"><span data-stu-id="2c5de-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="2c5de-111">Ridimensionamento manuale richiede toolog in e, in modo esplicito, le operazioni di ridimensionamento richiesta.</span><span class="sxs-lookup"><span data-stu-id="2c5de-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="2c5de-112">Questo approccio potrebbe non essere una soluzione valida se le operazioni di scalabilità vengono richieste di frequente oppure in momenti imprevisti.</span><span class="sxs-lookup"><span data-stu-id="2c5de-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="2c5de-113">Quando le regole di scalabilità automatica consente di rimuovere un'istanza di un set di scalabilità della macchina virtuale, essi non vengono rimossi automaticamente conoscenza di tale nodo dal cluster di Service Fabric hello associato, a meno che il tipo di nodo hello ha un livello di durabilità di Silver o oro.</span><span class="sxs-lookup"><span data-stu-id="2c5de-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="2c5de-114">Poiché le regole di scalabilità automatica funzionano su larga scala hello impostare il livello (anziché a livello di Service Fabric hello), le regole di scalabilità automatica è possono rimuovere i nodi di Service Fabric senza arresto li.</span><span class="sxs-lookup"><span data-stu-id="2c5de-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="2c5de-115">Questo tipo di rimozione dei nodi lascerà il nodo Service Fabric nello stato "ghost" dopo le operazioni di riduzione delle istanze.</span><span class="sxs-lookup"><span data-stu-id="2c5de-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="2c5de-116">Una persona (o un servizio) sarebbe necessario tooperiodically pulire lo stato del nodo rimosso in cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="2c5de-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="2c5de-117">Si noti che un tipo di nodo con un livello di durabilità Gold o Silver eseguirà automaticamente la pulizia dei nodi rimossi.</span><span class="sxs-lookup"><span data-stu-id="2c5de-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="2c5de-118">Anche se le regole di scalabilità automatica supportano [molte metriche](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), si tratta comunque di un set limitato.</span><span class="sxs-lookup"><span data-stu-id="2c5de-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="2c5de-119">Se lo scenario richiede la scalabilità basata su alcune metriche non incluse in questo set, le regole di scalabilità automatica potrebbero non essere una soluzione valida.</span><span class="sxs-lookup"><span data-stu-id="2c5de-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="2c5de-120">In base a queste limitazioni, è preferibile tooimplement più automatico scalabilità modelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2c5de-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="2c5de-121">Scalabilità delle API</span><span class="sxs-lookup"><span data-stu-id="2c5de-121">Scaling APIs</span></span>
<span data-ttu-id="2c5de-122">Le API di Azure esistono in questo modo il lavoro tooprogrammatically applicazioni con set di scalabilità di macchine virtuali e i cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2c5de-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="2c5de-123">Se le opzioni di scalabilità automatica esistenti non funzionano per lo scenario, queste API rendono possibili tooimplement logica di ridimensionamento personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2c5de-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="2c5de-124">Un approccio tooimplementing questo 'home-reso' scalabilità automatica funzionalità è tooadd un nuovo servizio senza stato toohello Service Fabric applicazione toomanage operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="2c5de-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="2c5de-125">All'interno del servizio hello `RunAsync` metodo, un set di trigger consente di determinare se la scalabilità è necessario (inclusi i parametri come la dimensione massima di un cluster di controllo e scalabilità cooldowns).</span><span class="sxs-lookup"><span data-stu-id="2c5de-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="2c5de-126">Hello API utilizzata per le interazioni di set di scalabilità macchina virtuale (numero corrente di hello entrambi toocheck di istanze di macchine virtuali e toomodify è) è hello [libreria di gestione di Azure calcolo fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="2c5de-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="2c5de-127">libreria di calcolo di Microsoft Office fluent Hello fornisce un'API da utilizzare per l'interazione con il set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2c5de-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="2c5de-128">Utilizzare toointeract con i cluster di Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="2c5de-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="2c5de-129">Naturalmente, hello scalabilità codice non deve necessariamente toorun come servizio in toobe cluster hello in scala.</span><span class="sxs-lookup"><span data-stu-id="2c5de-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="2c5de-130">Entrambi `IAzure` e `FabricClient` possibile connettersi in modalità remota, le risorse di Azure tootheir associata in modo hello scalabilità servizio potrebbe essere facilmente un'applicazione console o il servizio Windows in esecuzione da un'applicazione hello di fuori dell'infrastruttura di servizio.</span><span class="sxs-lookup"><span data-stu-id="2c5de-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="2c5de-131">Gestione delle credenziali</span><span class="sxs-lookup"><span data-stu-id="2c5de-131">Credential management</span></span>
<span data-ttu-id="2c5de-132">Una sfida di scrittura di un servizio di toohandle ridimensionamento è che il servizio di hello deve essere in grado di tooaccess risorse set scala della macchina virtuale senza un account di accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="2c5de-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="2c5de-133">L'accesso a Service Fabric hello cluster è facile se hello scalabilità servizio sta modificando l'applicazione di Service Fabric, ma le credenziali sono necessarie tooaccess hello set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="2c5de-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="2c5de-134">toolog in, è possibile utilizzare un [dell'entità servizio](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) creato con hello [CLI di Azure 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2c5de-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="2c5de-135">È possibile creare un'entità servizio con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2c5de-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="2c5de-136">Accedi toohello CLI di Azure (`az login`) come utente con scalabilità di macchine virtuali toohello di accesso set</span><span class="sxs-lookup"><span data-stu-id="2c5de-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="2c5de-137">Creare l'entità con il servizio hello`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="2c5de-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="2c5de-138">Prendere nota del appId hello (chiamato altrove 'ID client'), nome, password e tenant per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="2c5de-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="2c5de-139">Sarà inoltre necessario l'ID sottoscrizione, che può essere visualizzato con `az account list`</span><span class="sxs-lookup"><span data-stu-id="2c5de-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="2c5de-140">Hello calcolo fluent libreria può effettuare l'accesso utilizzando queste credenziali come indicato di seguito (si noti che i tipi Azure intuitiva di base come `IAzure` in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span><span class="sxs-lookup"><span data-stu-id="2c5de-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="2c5de-141">Una volta eseguito l'accesso, è possibile eseguire una query del numero di istanze di set di scalabilità tramite `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="2c5de-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="2c5de-142">Aumento del numero di istanze</span><span class="sxs-lookup"><span data-stu-id="2c5de-142">Scaling out</span></span>
<span data-ttu-id="2c5de-143">Utilizzando Microsoft Office fluent hello calcolo di Azure SDK, è possono aggiungere istanze di scalabilità della macchina virtuale toohello impostata con pochi chiamate-</span><span class="sxs-lookup"><span data-stu-id="2c5de-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="2c5de-144">In alternativa, le dimensioni del set di scalabilità di macchine virtuali possono essere gestite anche con i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c5de-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="2c5de-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)recuperare l'oggetto set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2c5de-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="2c5de-146">la capacità corrente Hello verrà archiviata in hello `.sku.capacity` proprietà.</span><span class="sxs-lookup"><span data-stu-id="2c5de-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="2c5de-147">Dopo la modifica di hello capacità toohello valore desiderato, scalabilità della macchina virtuale hello impostato in Azure possono essere aggiornati con hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.</span><span class="sxs-lookup"><span data-stu-id="2c5de-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="2c5de-148">Come quando si aggiunge manualmente un nodo, l'aggiunta di una scala di imposta l'istanza deve essere tutti toostart necessari che include un nuovo nodo di Service Fabric poiché il modello di set di scalabilità di hello estensioni tooautomatically aggiungere nuovo cluster di Service Fabric toohello istanze.</span><span class="sxs-lookup"><span data-stu-id="2c5de-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="2c5de-149">Riduzione</span><span class="sxs-lookup"><span data-stu-id="2c5de-149">Scaling in</span></span>

<span data-ttu-id="2c5de-150">La scalabilità è simile tooscaling out. set di scalabilità della macchina virtuale effettivo Hello le modifiche sono praticamente hello stesso.</span><span class="sxs-lookup"><span data-stu-id="2c5de-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="2c5de-151">Tuttavia, come illustrato in precedenza, Service Fabric pulisce automaticamente solo i nodi rimossi con la durabilità Gold o Silver.</span><span class="sxs-lookup"><span data-stu-id="2c5de-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="2c5de-152">Pertanto, in caso di hello bronzo durabilità, scala aggiuntivo è necessario toointeract con hello Service Fabric cluster tooshut toobe nodo hello rimosso verso il basso e quindi tooremove il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="2c5de-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="2c5de-153">Preparazione nodo hello per arresto riguarda la ricerca hello nodo toobe rimosso (nodo aggiunto più di recente hello) e disattivarlo.</span><span class="sxs-lookup"><span data-stu-id="2c5de-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="2c5de-154">Per i nodi non di inizializzazione, è possibile trovare i nodi più recenti confrontando il valore `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="2c5de-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="2c5de-155">Tenere presente che *valore di inizializzazione* nodi non sembrano tooalways seguono la convenzione di hello che gli ID istanza maggiore verranno rimosse per prime.</span><span class="sxs-lookup"><span data-stu-id="2c5de-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="2c5de-156">Una volta trovata hello nodo toobe rimosso, può essere disattivata e rimosso utilizzando hello stesso `FabricClient` istanza e hello `IAzure` istanza precedenti.</span><span class="sxs-lookup"><span data-stu-id="2c5de-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
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

<span data-ttu-id="2c5de-157">Anche in questo caso, come per l'aumento del numero di istanze, è possibile usare i cmdlet di PowerShell per modificare la capacità del set di scalabilità di macchine virtuali, se si preferisce un approccio basato sugli script.</span><span class="sxs-lookup"><span data-stu-id="2c5de-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="2c5de-158">Una volta che viene rimossa l'istanza di macchina virtuale di hello, è possibile rimuovere lo stato del nodo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2c5de-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="2c5de-159">Potenziali svantaggi</span><span class="sxs-lookup"><span data-stu-id="2c5de-159">Potential drawbacks</span></span>

<span data-ttu-id="2c5de-160">Come illustrato nel hello frammenti di codice precedente, la creazione di un proprio servizio scalabilità fornisce elevato hello di controllo e personalizzazione tramite l'applicazione della scala.</span><span class="sxs-lookup"><span data-stu-id="2c5de-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="2c5de-161">Questa condizione può essere utile negli scenari che richiedono un controllo preciso su quando e come aumentare o ridurre il numero di istanze dell'applicazione. Tuttavia, questo controllo implica un compromesso a livello di complessità del codice.</span><span class="sxs-lookup"><span data-stu-id="2c5de-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="2c5de-162">Questo approccio, è pertanto necessario tooown scalabilità codice, non è semplice.</span><span class="sxs-lookup"><span data-stu-id="2c5de-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="2c5de-163">L'approccio da scegliere per la scalabilità di Service Fabric dipende dallo scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="2c5de-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="2c5de-164">Se il ridimensionamento è insolito, hello possibilità tooadd o rimuovere i nodi è manualmente sia sufficiente.</span><span class="sxs-lookup"><span data-stu-id="2c5de-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="2c5de-165">Per scenari più complessi, le regole di scalabilità automatica e SDK esposizione a livello di codice hello possibilità tooscale offrono potenti alternative.</span><span class="sxs-lookup"><span data-stu-id="2c5de-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c5de-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c5de-166">Next steps</span></span>

<span data-ttu-id="2c5de-167">tooget iniziato a implementare la logica di ridimensionamento automatico, acquisire familiarità con hello seguenti concetti e le API utili:</span><span class="sxs-lookup"><span data-stu-id="2c5de-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="2c5de-168">Scalabilità manuale o con regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="2c5de-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="2c5de-169">[Fluent Azure Management Libraries per .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (utili per l'interazione con i set di scalabilità di macchine virtuali sottostanti del cluster Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="2c5de-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="2c5de-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (utile per l'interazione con un cluster Service Fabric e i relativi nodi)</span><span class="sxs-lookup"><span data-stu-id="2c5de-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
