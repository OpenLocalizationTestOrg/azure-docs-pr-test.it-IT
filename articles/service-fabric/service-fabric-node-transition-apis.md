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
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Sostituendo hello nodo avvio e arresto nodo API con hello nodo transizione API

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>Cosa hello nodo arrestare e avviare le API nodo?

Arresta nodo API Hello (gestito: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) si arresta un nodo di Service Fabric.  Un nodo di Service Fabric è processo, non una macchina virtuale o macchina: hello VM o computer verranno ancora essere in esecuzione.  Per rest hello del documento hello "nodo" implica il nodo di Service Fabric.  L'arresto di un nodo inserisce in un *arrestato* stato in cui non è un membro del cluster hello e non è possibile ospitare servizi, simulando in questo modo un *verso il basso* nodo.  Ciò è utile per l'inserimento di errori in hello sistema tootest l'applicazione.  Avvia nodo API Hello (gestito: [StartNodeAsync()][startnode], PowerShell: [inizio ServiceFabricNode][startnodeps]]) Inverte hello arresta nodo API,  che visualizza lo stato normale hello nodo tooa indietro.

## <a name="why-are-we-replacing-these"></a>Perché si sta procedendo alla relativa sostituzione?

Come descritto in precedenza, un *arrestato* nodo Service Fabric è un nodo intenzionalmente utilizzando hello arrestare API nodo di destinazione.  Oggetto *verso il basso* nodo è un nodo verso il basso per qualsiasi motivo (ad esempio hello VM o computer è disattivato).  Con hello arresta nodo API, sistema hello non espone informazioni toodifferentiate tra *arrestato* nodi e *verso il basso* nodi.

Inoltre, alcuni errori restituiti da queste API non offrono il massimo livello di dettaglio possibile.  Ad esempio, richiamare hello arresta nodo API in un oggetto già *arrestato* nodo verrà restituito l'errore hello *InvalidAddress*.  Questa esperienza poteva essere migliorata.

Inoltre, un nodo è stato arrestato per la durata di hello è "infinita" finché non viene richiamato avviare API nodo hello.  Questa condizione può causare problemi ed essere soggetta a errori.  Ad esempio, abbiamo visto problemi in cui un utente viene richiamato hello arrestare API nodo in un nodo e quindi dimenticato.  In un secondo momento, è poco chiaro se è stato nodo hello *verso il basso* o *arrestato*.


## <a name="introducing-hello-node-transition-apis"></a>Introduzione a hello nodo transizione API

Questi problemi sono stati risolti in un nuovo set di API.  Hello nuova transizione nodo API (gestito: [StartNodeTransitionAsync()][snt]) può essere utilizzato tootransition un tooa nodo Service Fabric *arrestato* stato o tootransition, da un *arrestato* tooa stato normale backup dello stato.  Si noti che hello "Start" nel nome hello di hello API toostarting un nodo non fa riferimento.  Fa riferimento a un'operazione asincrona che sistema hello eseguirà tootransition hello nodo tooeither toobeginning *arrestato* o è stato avviato.

**Utilizzo**

Se hello nodo transizione API non genera un'eccezione quando viene richiamato, sistema hello ha accettato l'operazione asincrona di hello e verrà eseguirlo.  Una chiamata non implica l'operazione di hello è ancora stato completato.  tooget informazioni sullo stato corrente di hello dell'operazione di hello, hello chiamata API di stato di transizione nodo (gestito: [GetNodeTransitionProgressAsync()][gntp]) con il guid di hello utilizzato durante la chiamata di nodo API di transizione per questa operazione.  Hello nodo transizione di stato di avanzamento API restituisce un oggetto NodeTransitionProgress.  La proprietà dell'oggetto stato specifica lo stato corrente di hello dell'operazione di hello.  Se lo stato di hello è "Running" operazione di hello è in esecuzione.  Se viene completata, l'operazione di hello completata senza errori.  Se si è verificato un errore, si è verificato un problema durante l'esecuzione di operazione hello.  stato di eccezione della proprietà di Hello risultato proprietà indicherà quali hello emettere.  Vedere https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate per ulteriori informazioni sulla proprietà State hello e hello "Esempio di utilizzo" sotto per esempi di codice.


**Fatta distinzione tra un nodo arrestato e un nodo verso il basso** se è un nodo *arrestato* utilizzando hello nodo transizione API, output di hello di una query di nodo (gestito: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) indicherà che il nodo presenta un *IsStopped* ha valore true.  Questo è diverso dal valore hello hello *NodeStatus* proprietà, che indicherà *verso il basso*.  Se hello *NodeStatus* proprietà ha un valore *verso il basso*, ma *IsStopped* è false, quindi il nodo hello non è stato arrestato utilizzando l'API di transizione nodo hello ed è  *Verso il basso* a causa di un altro motivo.  Se hello *IsStopped* proprietà è true e hello *NodeStatus* proprietà *verso il basso*, quindi è stato arrestato utilizzando hello nodo transizione API.

Avvio di un *arrestato* nodo utilizzando hello nodo transizione API restituirà, toofunction come membro del cluster hello normale nuovamente.  Hello output di hello nodo query API mostrerà *IsStopped* false, e *NodeStatus* come qualcosa che non è attivo (ad esempio, in alto).


**Durata limitata** quando si utilizza hello nodo transizione API toostop un nodo, uno di hello parametri obbligatori, *stopNodeDurationInSeconds*, rappresenta hello quantità di tempo nel nodo di hello tookeep secondi  *arrestato*.  Questo valore deve essere nell'intervallo, con un minimo di 600 e un massimo di 14400 consentito hello.  Trascorso questo tempo, nodo hello verrà riavviato automaticamente nel backup dello stato automaticamente.  Per un esempio di utilizzo, vedere tooSample 1 di seguito.

> [!WARNING]
> Evitare di utilizzare le API di transizione di nodo e hello nodo arrestare e avviare le API di nodo.  Hello si consiglia di utilizzare troppo hello nodo transizione API.  > Se un nodo è già stato arrestato utilizzando hello arresta nodo API, deve essere avviato prima tramite hello avviare API nodo prima di utilizzare hello > nodo transizione API.

> [!WARNING]
> Non è possibile effettuare chiamate in numerose API di transizione nodo hello stesso nodo in parallelo.  In questo caso, verrà hello nodo transizione API > generare una FabricException con un valore della proprietà ErrorCode di NodeTransitionInProgress.  In presenza di una transizione di nodo in un nodo specifico > stato avviato, è necessario attendere fino a quando l'operazione di hello raggiunge uno stato finale (Completed, Faulted o ForceCancelled) prima di avviare un > nuova transizione su hello stesso nodo.  Sono consentite chiamate a transizioni del nodo in parallelo su nodi diversi.


#### <a name="sample-usage"></a>Esempio di utilizzo


**Esempio 1** -hello seguendo l'esempio utilizza hello nodo transizione API toostop un nodo.

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

**Esempio 2** : hello seguente esempio avvia un *arrestato* nodo.  Usa alcuni metodi di supporto dal primo esempio hello.

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

**Esempio 3** : hello esempio seguente viene illustrato l'utilizzo non corretto.  Questo utilizzo non è corretto perché hello *stopDurationInSeconds* fornisce è maggiore di hello nell'intervallo consentito.  Poiché StartNodeTransitionAsync() avrà esito negativo con un errore irreversibile, non è stato accettato l'operazione di hello e API di stato di avanzamento hello non deve essere chiamato.  Questo esempio utilizza alcuni metodi di supporto dal primo esempio hello.

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

**Esempio 4** : hello esempio seguente mostra informazioni sull'errore hello che verrà restituiti da hello nodo transizione di stato di avanzamento API quando l'operazione di hello iniziata dal nodo transizione API hello viene accettata, ma non riesce in un secondo momento durante l'esecuzione.  In caso di hello, operazione non riesce perché tenta di hello nodo transizione API toostart un nodo che non esiste.  Questo esempio utilizza alcuni metodi di supporto dal primo esempio hello.

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
