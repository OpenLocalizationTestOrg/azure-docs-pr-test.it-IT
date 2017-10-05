---
title: Avviare e arrestare nodi di cluster per testare microservizi di Azure | Documentazione Microsoft
description: Informazioni su come usare la tecnologia fault injection per testare un'applicazione di Service Fabric avviando e arrestando nodi di cluster.
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
ms.openlocfilehash: 850fbc0c74811ec942292da64064dec867cd1b9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replacing-the-start-node-and-stop-node-apis-with-the-node-transition-api"></a><span data-ttu-id="48df4-103">Sostituzione dell'API di avvio del nodo e dell'API di arresto del nodo con l'API di transizione del nodo</span><span class="sxs-lookup"><span data-stu-id="48df4-103">Replacing the Start Node and Stop node APIs with the Node Transition API</span></span>

## <a name="what-do-the-stop-node-and-start-node-apis-do"></a><span data-ttu-id="48df4-104">Come funzionano le API di avvio del nodo e di arresto del nodo?</span><span class="sxs-lookup"><span data-stu-id="48df4-104">What do the Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="48df4-105">L'API di avvio del nodo (gestita: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) arresta un nodo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48df4-105">The Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="48df4-106">Un nodo di Service Fabric è un processo, non una VM o macchina; la VM o la macchina sarà comunque in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="48df4-106">A Service Fabric node is process, not a VM or machine – the VM or machine will still be running.</span></span>  <span data-ttu-id="48df4-107">Nel resto del documento, "nodo" indica il nodo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48df4-107">For the rest of the document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="48df4-108">L'arresto di un nodo inserisce il nodo in uno stato *arrestato*, in cui non è un membro del cluster e non può ospitare servizi, simulando in questo modo un nodo *inattivo*.</span><span class="sxs-lookup"><span data-stu-id="48df4-108">Stopping a node puts it into a *stopped* state where it is not a member of the cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="48df4-109">Questa condizione è utile per l'inserimento di errori nel sistema per testare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48df4-109">This is useful for injecting faults into the system to test your application.</span></span>  <span data-ttu-id="48df4-110">L'API di avvio del nodo (gestita: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) inverte l'API di arresto del nodo riportando il nodo a uno stato normale.</span><span class="sxs-lookup"><span data-stu-id="48df4-110">The Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses the Stop Node API,  which brings the node back to a normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="48df4-111">Perché si sta procedendo alla relativa sostituzione?</span><span class="sxs-lookup"><span data-stu-id="48df4-111">Why are we replacing these?</span></span>

<span data-ttu-id="48df4-112">Come descritto in precedenza, un nodo *arrestato* di Service Fabric è un nodo di destinazione scelto intenzionalmente usando l'API di arresto del nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using the Stop Node API.</span></span>  <span data-ttu-id="48df4-113">Un nodo *inattivo* è un nodo che non è attivo per qualsiasi altro motivo, ad esempio, la VM o la macchina è disattivata.</span><span class="sxs-lookup"><span data-stu-id="48df4-113">A *down* node is a node that is down for any other reason (e.g. the VM or machine is off).</span></span>  <span data-ttu-id="48df4-114">Con l'API di arresto del nodo, il sistema non espone le informazioni per distinguere i nodi *arrestati* e i nodi *inattivi*.</span><span class="sxs-lookup"><span data-stu-id="48df4-114">With the Stop Node API, the system does not expose information to differentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="48df4-115">Inoltre, alcuni errori restituiti da queste API non offrono il massimo livello di dettaglio possibile.</span><span class="sxs-lookup"><span data-stu-id="48df4-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="48df4-116">Ad esempio, se si chiama l'API di arresto del nodo su un nodo già *arrestato* verrà restituito l'errore *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="48df4-116">For example, invoking the Stop Node API on an already *stopped* node will return the error *InvalidAddress*.</span></span>  <span data-ttu-id="48df4-117">Questa esperienza poteva essere migliorata.</span><span class="sxs-lookup"><span data-stu-id="48df4-117">This experience could be improved.</span></span>

<span data-ttu-id="48df4-118">Inoltre, la durata per cui un nodo viene arrestato è "infinita" finché non viene richiamata l'API di avvio del nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-118">Also, the duration a node is stopped for is “infinite” until the Start Node API is invoked.</span></span>  <span data-ttu-id="48df4-119">Questa condizione può causare problemi ed essere soggetta a errori.</span><span class="sxs-lookup"><span data-stu-id="48df4-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="48df4-120">Ad esempio, si sono verificati problemi in cui un utente ha richiama l'API di avvio del nodo su un nodo e successivamente ha dimenticato di avere eseguito questa operazione.</span><span class="sxs-lookup"><span data-stu-id="48df4-120">For example, we’ve seen problems where a user invoked the Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="48df4-121">In seguito non è stato chiaro se il nodo era *inattivo* o *arrestato*.</span><span class="sxs-lookup"><span data-stu-id="48df4-121">Later, it was unclear if the node was *down* or *stopped*.</span></span>


## <a name="introducing-the-node-transition-apis"></a><span data-ttu-id="48df4-122">Introduzione alle API di transizione del nodo</span><span class="sxs-lookup"><span data-stu-id="48df4-122">Introducing the Node Transition APIs</span></span>

<span data-ttu-id="48df4-123">Questi problemi sono stati risolti in un nuovo set di API.</span><span class="sxs-lookup"><span data-stu-id="48df4-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="48df4-124">La nuova API di transizione del nodo (gestito: [StartNodeTransitionAsync()][snt]) può essere usata per la transizione di un nodo di Service Fabric a uno stato *arrestato* o per eseguire la transizione da uno stato *arrestato* a uno stato attivo normale.</span><span class="sxs-lookup"><span data-stu-id="48df4-124">The new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used to transition a Service Fabric node to a *stopped* state, or to transition it from a *stopped* state to a normal up state.</span></span>  <span data-ttu-id="48df4-125">Si noti che "Start" nel nome dell'API non fa riferimento all'avvio di un nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-125">Please note that the “Start” in the name of the API does not refer to starting a node.</span></span>  <span data-ttu-id="48df4-126">Fa riferimento all'avvio di un'operazione asincrona che verrà eseguita dal sistema per la transizione del nodo nello stato *arrestato* o avviato.</span><span class="sxs-lookup"><span data-stu-id="48df4-126">It refers to beginning an asynchronous operation that the system will execute to transition the node to either *stopped* or started state.</span></span>

<span data-ttu-id="48df4-127">**Utilizzo**</span><span class="sxs-lookup"><span data-stu-id="48df4-127">**Usage**</span></span>

<span data-ttu-id="48df4-128">Se l'API di transizione del nodo non genera un'eccezione quando viene richiamata, il sistema ha accettato l'operazione asincrona e la eseguirà.</span><span class="sxs-lookup"><span data-stu-id="48df4-128">If the Node Transition API does not throw an exception when invoked, then the system has accepted the asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="48df4-129">Una chiamata eseguita correttamente non implica che l'operazione sia stata completata.</span><span class="sxs-lookup"><span data-stu-id="48df4-129">A successful call does not imply the operation is finished yet.</span></span>  <span data-ttu-id="48df4-130">Per ottenere informazioni sullo stato corrente dell'operazione, chiamare l'API di avanzamento della transizione del nodo (gestito: [GetNodeTransitionProgressAsync()][gntp]) con il GUID usato per chiamare l'API di transizione di nodo per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="48df4-130">To get information about the current state of the operation, call the Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with the guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="48df4-131">L'API di avanzamento della transizione del nodo restituisce un oggetto NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="48df4-131">The Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="48df4-132">La proprietà State dell'oggetto specifica lo stato corrente dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="48df4-132">This object’s State property specifies the current state of the operation.</span></span>  <span data-ttu-id="48df4-133">Se lo stato è "in esecuzione", l'operazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="48df4-133">If the state is “Running” then the operation is executing.</span></span>  <span data-ttu-id="48df4-134">Se lo stato è completato, l'operazione è stata completata senza errori.</span><span class="sxs-lookup"><span data-stu-id="48df4-134">If it is Completed, the operation finished without error.</span></span>  <span data-ttu-id="48df4-135">Se lo stato indica un errore, si è verificato un problema in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="48df4-135">If it is Faulted, there was a problem executing the operation.</span></span>  <span data-ttu-id="48df4-136">La proprietà Exception della proprietà Result indicherà il problema riscontrato.</span><span class="sxs-lookup"><span data-stu-id="48df4-136">The Result property’s Exception property will indicate what the issue was.</span></span>  <span data-ttu-id="48df4-137">Per altre informazioni sulla proprietà State e la sezione "Esempio di utilizzo" per esempi di codice, vedere https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate.</span><span class="sxs-lookup"><span data-stu-id="48df4-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about the State property, and the “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="48df4-138">**Differenze tra un nodo arrestato e un nodo inattivo** Se un nodo è stato *arrestato* usando l'API di transizione del nodo, l'output di una query del nodo (gestito: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) indicherà il valore true della proprietà *IsStopped* per questo nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using the Node Transition API, the output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="48df4-139">Si noti che questo valore è diverso dal valore della proprietà *NodeStatus* che indicherà lo stato *inattivo*.</span><span class="sxs-lookup"><span data-stu-id="48df4-139">Note this is different from the value of the *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="48df4-140">Se la proprietà *NodeStatus* ha il valore *inattivo*, ma *IsStopped* restituisce false, il nodo non è stato arrestato usando l'API di transizione del nodo ed è *inattivo* per un altro motivo.</span><span class="sxs-lookup"><span data-stu-id="48df4-140">If the *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then the node was not stopped using the Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="48df4-141">Se il valore della proprietà *IsStopped* è true e la proprietà *NodeStatus* indica lo stato *inattivo*, il nodo è stato arrestato usando l'API di transizione del nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-141">If the *IsStopped* property is true, and the *NodeStatus* property is *Down*, then it was stopped using the Node Transition API.</span></span>

<span data-ttu-id="48df4-142">L'avvio di un nodo *arrestato* usando l'API di transizione del nodo ne ripristina il funzionamento come membro normale del cluster.</span><span class="sxs-lookup"><span data-stu-id="48df4-142">Starting a *stopped* node using the Node Transition API will return it to function as a normal member of the cluster again.</span></span>  <span data-ttu-id="48df4-143">L'output dell'API di query del nodo indicherà *IsStopped* come false e *NodeStatus* indicherà un valore che non è inattivo, ad esempio, attivo.</span><span class="sxs-lookup"><span data-stu-id="48df4-143">The output of the node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="48df4-144">**Durata limitata** quando si usa l'API di transizione di nodo per arrestare un nodo, uno dei parametri obbligatori, *stopNodeDurationInSeconds*, rappresenta il tempo in secondi per cui il nodo viene mantenuto *arrestato*.</span><span class="sxs-lookup"><span data-stu-id="48df4-144">**Limited Duration** When using the Node Transition API to stop a node, one of the required parameters, *stopNodeDurationInSeconds*, represents the amount of time in seconds to keep the node *stopped*.</span></span>  <span data-ttu-id="48df4-145">Questo valore deve essere compreso nell'intervallo consentito, che include un minimo di 600 secondi e un massimo di 14.400 secondi.</span><span class="sxs-lookup"><span data-stu-id="48df4-145">This value must be in the allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="48df4-146">Al termine di questo periodo, il nodo verrà riavviato automaticamente in uno stato attivo.</span><span class="sxs-lookup"><span data-stu-id="48df4-146">After this time expires, the node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="48df4-147">Fare riferimento all'esempio 1 di seguito per un esempio di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="48df4-147">Refer to Sample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="48df4-148">Non combinare le API di transizione del nodo e le API di avvio del nodo e di arresto del nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-148">Avoid mixing Node Transition APIs and the Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="48df4-149">È consigliabile usare solo l'API di transizione del nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-149">The recommendation is to  use the Node Transition API only.</span></span>  <span data-ttu-id="48df4-150">Se un nodo è già stato arrestato usando l'API di arresto del nodo, è necessario avviarlo usando l'API di avvio del nodo prima di usare le API di transizioni del nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-150">> If a node has been already been stopped using the Stop Node API, it should be started using the Start Node API first before using the > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="48df4-151">Non è possibile eseguire più chiamate API di transizione del nodo in parallelo nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-151">Multiple Node Transition APIs calls cannot be made on the same node in parallel.</span></span>  <span data-ttu-id="48df4-152">In questo caso, l'API di transizione del nodo  genererà un FabricException con un valore NodeTransitionInProgress della proprietà ErrorCode.</span><span class="sxs-lookup"><span data-stu-id="48df4-152">In such a situation, the Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="48df4-153">Dopo avere avviato una transizione del nodo in un nodo specifico, è necessario attendere fino a quando l'operazione raggiunge uno stato finale (completato, con errore e annullamento forzato) prima di avviare una nuova transizione nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-153">Once a node transition on a specific node has  > been started, you should wait until the operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on the same node.</span></span>  <span data-ttu-id="48df4-154">Sono consentite chiamate a transizioni del nodo in parallelo su nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="48df4-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="48df4-155">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="48df4-155">Sample Usage</span></span>


<span data-ttu-id="48df4-156">**Esempio 1**: l'esempio seguente usa l'API di transizione del nodo per arrestare un nodo.</span><span class="sxs-lookup"><span data-stu-id="48df4-156">**Sample 1** - The following sample uses the Node Transition API to stop a node.</span></span>

```csharp
        // Helper function to get information about a node
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
                        // Inspect the progress object's Result.Exception.HResult to get the error code.
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
            // Uses the GetNodeListAsync() API to get information about the target node
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
                    // Invoke StartNodeTransitionAsync with the NodeStopDescription from above, which will stop the target node.  Retry transient errors.
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

<span data-ttu-id="48df4-157">**Esempio 2**: l'esempio seguente avvia un nodo *arrestato*.</span><span class="sxs-lookup"><span data-stu-id="48df4-157">**Sample 2** - The following sample starts a *stopped* node.</span></span>  <span data-ttu-id="48df4-158">Vengono usati alcuni metodi di supporto dal primo esempio.</span><span class="sxs-lookup"><span data-stu-id="48df4-158">It uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses the GetNodeListAsync() API to get information about the target node
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
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
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

<span data-ttu-id="48df4-159">**Esempio 3**: l'esempio seguente illustra un uso non corretto.</span><span class="sxs-lookup"><span data-stu-id="48df4-159">**Sample 3** - The following sample shows incorrect usage.</span></span>  <span data-ttu-id="48df4-160">Questo uso non è corretto perché il valore *stopDurationInSeconds* fornito è maggiore dell'intervallo consentito.</span><span class="sxs-lookup"><span data-stu-id="48df4-160">This usage is incorrect because the *stopDurationInSeconds* it provides is greater than the allowed range.</span></span>  <span data-ttu-id="48df4-161">Poiché StartNodeTransitionAsync() genererà un errore irreversibile, l'operazione non è stata accettata e l'API di avanzamento non deve essere chiamata.</span><span class="sxs-lookup"><span data-stu-id="48df4-161">Since StartNodeTransitionAsync() will fail with a fatal error, the operation was not accepted, and the progress API should not be called.</span></span>  <span data-ttu-id="48df4-162">Questo esempio usa alcuni metodi di supporto dal primo esempio.</span><span class="sxs-lookup"><span data-stu-id="48df4-162">This sample uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds to demonstrate error
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

<span data-ttu-id="48df4-163">**Esempio 4**: l'esempio seguente mostra le informazioni sull'errore che verranno restituite dall'API di avanzamento della transizione del nodo quando l'operazione avviata dall'API di transizione del nodo viene accettata, ma si verifica un errore successivamente in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="48df4-163">**Sample 4** - The following sample shows the error information that will be returned from the Node Transition Progress API when the operation initiated by the Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="48df4-164">In questo caso l'errore si verifica perché l'API di transizione del nodo tenta di avviare un nodo che non esiste.</span><span class="sxs-lookup"><span data-stu-id="48df4-164">In the case, it fails because the Node Transition API attempts to start a node that does not exist.</span></span>  <span data-ttu-id="48df4-165">Questo esempio usa alcuni metodi di supporto dal primo esempio.</span><span class="sxs-lookup"><span data-stu-id="48df4-165">This sample uses some helper methods from the first sample.</span></span>

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
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
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

            // Now call StartNodeTransitionProgressAsync() until the desired state is reached.  In this case, it will end up in the Faulted state since the node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect the progress object's Result.Exception.HResult to get the error code.
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
