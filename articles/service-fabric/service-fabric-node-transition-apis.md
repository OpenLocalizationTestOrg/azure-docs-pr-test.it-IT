---
title: aaaStart e arrestare tootest di nodi di cluster Azure microservizi | Documenti Microsoft
description: Informazioni su come toouse fault tootest attacco intrusivo nel codice un'applicazione di Service Fabric per avvio e arresto di nodi del cluster.
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="2a425-103">Sostituendo hello nodo avvio e arresto nodo API con hello nodo transizione API</span><span class="sxs-lookup"><span data-stu-id="2a425-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="2a425-104">Cosa hello nodo arrestare e avviare le API nodo?</span><span class="sxs-lookup"><span data-stu-id="2a425-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="2a425-105">Arresta nodo API Hello (gestito: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) si arresta un nodo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2a425-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="2a425-106">Un nodo di Service Fabric è processo, non una macchina virtuale o macchina: hello VM o computer verranno ancora essere in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a425-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="2a425-107">Per rest hello del documento hello "nodo" implica il nodo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2a425-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="2a425-108">L'arresto di un nodo inserisce in un *arrestato* stato in cui non è un membro del cluster hello e non è possibile ospitare servizi, simulando in questo modo un *verso il basso* nodo.</span><span class="sxs-lookup"><span data-stu-id="2a425-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="2a425-109">Ciò è utile per l'inserimento di errori in hello sistema tootest l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a425-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="2a425-110">Avvia nodo API Hello (gestito: [StartNodeAsync()][startnode], PowerShell: [inizio ServiceFabricNode][startnodeps]]) Inverte hello arresta nodo API,  che visualizza lo stato normale hello nodo tooa indietro.</span><span class="sxs-lookup"><span data-stu-id="2a425-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="2a425-111">Perché si sta procedendo alla relativa sostituzione?</span><span class="sxs-lookup"><span data-stu-id="2a425-111">Why are we replacing these?</span></span>

<span data-ttu-id="2a425-112">Come descritto in precedenza, un *arrestato* nodo Service Fabric è un nodo intenzionalmente utilizzando hello arrestare API nodo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2a425-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="2a425-113">Oggetto *verso il basso* nodo è un nodo verso il basso per qualsiasi motivo (ad esempio hello VM o computer è disattivato).</span><span class="sxs-lookup"><span data-stu-id="2a425-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="2a425-114">Con hello arresta nodo API, sistema hello non espone informazioni toodifferentiate tra *arrestato* nodi e *verso il basso* nodi.</span><span class="sxs-lookup"><span data-stu-id="2a425-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="2a425-115">Inoltre, alcuni errori restituiti da queste API non offrono il massimo livello di dettaglio possibile.</span><span class="sxs-lookup"><span data-stu-id="2a425-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="2a425-116">Ad esempio, richiamare hello arresta nodo API in un oggetto già *arrestato* nodo verrà restituito l'errore hello *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="2a425-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="2a425-117">Questa esperienza poteva essere migliorata.</span><span class="sxs-lookup"><span data-stu-id="2a425-117">This experience could be improved.</span></span>

<span data-ttu-id="2a425-118">Inoltre, un nodo è stato arrestato per la durata di hello è "infinita" finché non viene richiamato avviare API nodo hello.</span><span class="sxs-lookup"><span data-stu-id="2a425-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="2a425-119">Questa condizione può causare problemi ed essere soggetta a errori.</span><span class="sxs-lookup"><span data-stu-id="2a425-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="2a425-120">Ad esempio, abbiamo visto problemi in cui un utente viene richiamato hello arrestare API nodo in un nodo e quindi dimenticato.</span><span class="sxs-lookup"><span data-stu-id="2a425-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="2a425-121">In un secondo momento, è poco chiaro se è stato nodo hello *verso il basso* o *arrestato*.</span><span class="sxs-lookup"><span data-stu-id="2a425-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="2a425-122">Introduzione a hello nodo transizione API</span><span class="sxs-lookup"><span data-stu-id="2a425-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="2a425-123">Questi problemi sono stati risolti in un nuovo set di API.</span><span class="sxs-lookup"><span data-stu-id="2a425-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="2a425-124">Hello nuova transizione nodo API (gestito: [StartNodeTransitionAsync()][snt]) può essere utilizzato tootransition un tooa nodo Service Fabric *arrestato* stato o tootransition, da un *arrestato* tooa stato normale backup dello stato.</span><span class="sxs-lookup"><span data-stu-id="2a425-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="2a425-125">Si noti che hello "Start" nel nome hello di hello API toostarting un nodo non fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="2a425-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="2a425-126">Fa riferimento a un'operazione asincrona che sistema hello eseguirà tootransition hello nodo tooeither toobeginning *arrestato* o è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="2a425-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="2a425-127">**Utilizzo**</span><span class="sxs-lookup"><span data-stu-id="2a425-127">**Usage**</span></span>

<span data-ttu-id="2a425-128">Se hello nodo transizione API non genera un'eccezione quando viene richiamato, sistema hello ha accettato l'operazione asincrona di hello e verrà eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="2a425-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="2a425-129">Una chiamata non implica l'operazione di hello è ancora stato completato.</span><span class="sxs-lookup"><span data-stu-id="2a425-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="2a425-130">tooget informazioni sullo stato corrente di hello dell'operazione di hello, hello chiamata API di stato di transizione nodo (gestito: [GetNodeTransitionProgressAsync()][gntp]) con il guid di hello utilizzato durante la chiamata di nodo API di transizione per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="2a425-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="2a425-131">Hello nodo transizione di stato di avanzamento API restituisce un oggetto NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="2a425-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="2a425-132">La proprietà dell'oggetto stato specifica lo stato corrente di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="2a425-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="2a425-133">Se lo stato di hello è "Running" operazione di hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a425-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="2a425-134">Se viene completata, l'operazione di hello completata senza errori.</span><span class="sxs-lookup"><span data-stu-id="2a425-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="2a425-135">Se si è verificato un errore, si è verificato un problema durante l'esecuzione di operazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a425-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="2a425-136">stato di eccezione della proprietà di Hello risultato proprietà indicherà quali hello emettere.</span><span class="sxs-lookup"><span data-stu-id="2a425-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="2a425-137">Vedere https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate per ulteriori informazioni sulla proprietà State hello e hello "Esempio di utilizzo" sotto per esempi di codice.</span><span class="sxs-lookup"><span data-stu-id="2a425-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="2a425-138">**Fatta distinzione tra un nodo arrestato e un nodo verso il basso** se è un nodo *arrestato* utilizzando hello nodo transizione API, output di hello di una query di nodo (gestito: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) indicherà che il nodo presenta un *IsStopped* ha valore true.</span><span class="sxs-lookup"><span data-stu-id="2a425-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="2a425-139">Questo è diverso dal valore hello hello *NodeStatus* proprietà, che indicherà *verso il basso*.</span><span class="sxs-lookup"><span data-stu-id="2a425-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="2a425-140">Se hello *NodeStatus* proprietà ha un valore *verso il basso*, ma *IsStopped* è false, quindi il nodo hello non è stato arrestato utilizzando l'API di transizione nodo hello ed è  *Verso il basso* a causa di un altro motivo.</span><span class="sxs-lookup"><span data-stu-id="2a425-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="2a425-141">Se hello *IsStopped* proprietà è true e hello *NodeStatus* proprietà *verso il basso*, quindi è stato arrestato utilizzando hello nodo transizione API.</span><span class="sxs-lookup"><span data-stu-id="2a425-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="2a425-142">Avvio di un *arrestato* nodo utilizzando hello nodo transizione API restituirà, toofunction come membro del cluster hello normale nuovamente.</span><span class="sxs-lookup"><span data-stu-id="2a425-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="2a425-143">Hello output di hello nodo query API mostrerà *IsStopped* false, e *NodeStatus* come qualcosa che non è attivo (ad esempio, in alto).</span><span class="sxs-lookup"><span data-stu-id="2a425-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="2a425-144">**Durata limitata** quando si utilizza hello nodo transizione API toostop un nodo, uno di hello parametri obbligatori, *stopNodeDurationInSeconds*, rappresenta hello quantità di tempo nel nodo di hello tookeep secondi  *arrestato*.</span><span class="sxs-lookup"><span data-stu-id="2a425-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="2a425-145">Questo valore deve essere nell'intervallo, con un minimo di 600 e un massimo di 14400 consentito hello.</span><span class="sxs-lookup"><span data-stu-id="2a425-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="2a425-146">Trascorso questo tempo, nodo hello verrà riavviato automaticamente nel backup dello stato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2a425-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="2a425-147">Per un esempio di utilizzo, vedere tooSample 1 di seguito.</span><span class="sxs-lookup"><span data-stu-id="2a425-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="2a425-148">Evitare di utilizzare le API di transizione di nodo e hello nodo arrestare e avviare le API di nodo.</span><span class="sxs-lookup"><span data-stu-id="2a425-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="2a425-149">Hello si consiglia di utilizzare troppo hello nodo transizione API.</span><span class="sxs-lookup"><span data-stu-id="2a425-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="2a425-150">> Se un nodo è già stato arrestato utilizzando hello arresta nodo API, deve essere avviato prima tramite hello avviare API nodo prima di utilizzare hello > nodo transizione API.</span><span class="sxs-lookup"><span data-stu-id="2a425-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="2a425-151">Non è possibile effettuare chiamate in numerose API di transizione nodo hello stesso nodo in parallelo.</span><span class="sxs-lookup"><span data-stu-id="2a425-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="2a425-152">In questo caso, verrà hello nodo transizione API > generare una FabricException con un valore della proprietà ErrorCode di NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="2a425-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="2a425-153">In presenza di una transizione di nodo in un nodo specifico > stato avviato, è necessario attendere fino a quando l'operazione di hello raggiunge uno stato finale (Completed, Faulted o ForceCancelled) prima di avviare un > nuova transizione su hello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="2a425-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="2a425-154">Sono consentite chiamate a transizioni del nodo in parallelo su nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="2a425-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="2a425-155">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="2a425-155">Sample Usage</span></span>


<span data-ttu-id="2a425-156">**Esempio 1** -hello seguendo l'esempio utilizza hello nodo transizione API toostop un nodo.</span><span class="sxs-lookup"><span data-stu-id="2a425-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="2a425-157">**Esempio 2** : hello seguente esempio avvia un *arrestato* nodo.</span><span class="sxs-lookup"><span data-stu-id="2a425-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="2a425-158">Usa alcuni metodi di supporto dal primo esempio hello.</span><span class="sxs-lookup"><span data-stu-id="2a425-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="2a425-159">**Esempio 3** : hello esempio seguente viene illustrato l'utilizzo non corretto.</span><span class="sxs-lookup"><span data-stu-id="2a425-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="2a425-160">Questo utilizzo non è corretto perché hello *stopDurationInSeconds* fornisce è maggiore di hello nell'intervallo consentito.</span><span class="sxs-lookup"><span data-stu-id="2a425-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="2a425-161">Poiché StartNodeTransitionAsync() avrà esito negativo con un errore irreversibile, non è stato accettato l'operazione di hello e API di stato di avanzamento hello non deve essere chiamato.</span><span class="sxs-lookup"><span data-stu-id="2a425-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="2a425-162">Questo esempio utilizza alcuni metodi di supporto dal primo esempio hello.</span><span class="sxs-lookup"><span data-stu-id="2a425-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="2a425-163">**Esempio 4** : hello esempio seguente mostra informazioni sull'errore hello che verrà restituiti da hello nodo transizione di stato di avanzamento API quando l'operazione di hello iniziata dal nodo transizione API hello viene accettata, ma non riesce in un secondo momento durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a425-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="2a425-164">In caso di hello, operazione non riesce perché tenta di hello nodo transizione API toostart un nodo che non esiste.</span><span class="sxs-lookup"><span data-stu-id="2a425-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="2a425-165">Questo esempio utilizza alcuni metodi di supporto dal primo esempio hello.</span><span class="sxs-lookup"><span data-stu-id="2a425-165">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
