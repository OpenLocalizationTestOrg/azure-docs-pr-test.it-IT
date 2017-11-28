---
title: errori aaaSimulate in Azure microservizi | Documenti Microsoft
description: Come tooharden i servizi in caso di errori normale e anomali.
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: 
ms.assetid: 44af01f0-ed73-4c31-8ac0-d9d65b4ad2d6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: 05467e291dfc0f12a021955f8ea540881ec10746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="simulate-failures-during-service-workloads"></a><span data-ttu-id="df777-103">Simulare gli errori durante i carichi di lavoro del servizio</span><span class="sxs-lookup"><span data-stu-id="df777-103">Simulate failures during service workloads</span></span>
<span data-ttu-id="df777-104">scenari di testabilità Hello in Azure Service Fabric consentono agli sviluppatori toonot preoccupare di gestione di errori di singoli.</span><span class="sxs-lookup"><span data-stu-id="df777-104">hello testability scenarios in Azure Service Fabric enable developers toonot worry about dealing with individual faults.</span></span> <span data-ttu-id="df777-105">Tuttavia, sono disponibili scenari in cui potrebbe essere necessaria un'interfoliazione esplicita del carico di lavoro client e degli errori.</span><span class="sxs-lookup"><span data-stu-id="df777-105">There are scenarios, however, where an explicit interleaving of client workload and failures might be needed.</span></span> <span data-ttu-id="df777-106">Hello interfoliazione di errori e di carico di lavoro client garantisce che il servizio hello sta effettivamente eseguendo un'azione quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="df777-106">hello interleaving of client workload and faults ensures that hello service is actually performing some action when failure happens.</span></span> <span data-ttu-id="df777-107">Dato il livello di hello del controllo che fornisce la testabilità, questi potrebbero essere in punti precisi dell'esecuzione del carico di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="df777-107">Given hello level of control that testability provides, these could be at precise points of hello workload execution.</span></span> <span data-ttu-id="df777-108">Questo induzione degli errori in stati diversi in un'applicazione hello può individuare i bug e migliorare la qualità.</span><span class="sxs-lookup"><span data-stu-id="df777-108">This induction of faults at different states in hello application can find bugs and improve quality.</span></span>

## <a name="sample-custom-scenario"></a><span data-ttu-id="df777-109">Esempio di scenario personalizzato</span><span class="sxs-lookup"><span data-stu-id="df777-109">Sample custom scenario</span></span>
<span data-ttu-id="df777-110">Questo test viene illustrato uno scenario che esegue l'interfoliazione hello business del carico di lavoro con [errori normale e anomali](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span><span class="sxs-lookup"><span data-stu-id="df777-110">This test shows a scenario that interleaves hello business workload with [graceful and ungraceful failures](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span></span> <span data-ttu-id="df777-111">devono essere provocati errori Hello interno hello delle operazioni del servizio o di calcolo per ottenere risultati ottimali.</span><span class="sxs-lookup"><span data-stu-id="df777-111">hello faults should be induced in hello middle of service operations or compute for best results.</span></span>

<span data-ttu-id="df777-112">Verrà ora esaminato un esempio di un servizio che espone quattro carichi di lavoro: A, B, C e D. ogni corrisponde tooa set di flussi di lavoro e potrebbe essere di calcolo, archiviazione o una combinazione.</span><span class="sxs-lookup"><span data-stu-id="df777-112">Let's walk through an example of a service that exposes four workloads: A, B, C, and D. Each corresponds tooa set of workflows and could be compute, storage, or a mix.</span></span> <span data-ttu-id="df777-113">Per i migliori risultati hello di semplicità, si verrà astratta carichi di lavoro hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="df777-113">For hello sake of simplicity, we will abstract out hello workloads in our example.</span></span> <span data-ttu-id="df777-114">errori di diversi Hello eseguiti in questo esempio sono:</span><span class="sxs-lookup"><span data-stu-id="df777-114">hello different faults executed in this example are:</span></span>

* <span data-ttu-id="df777-115">RestartNode: Errore anomali toosimulate una macchina riavviare.</span><span class="sxs-lookup"><span data-stu-id="df777-115">RestartNode: Ungraceful fault toosimulate a machine restart.</span></span>
* <span data-ttu-id="df777-116">RestartDeployedCodePackage: Processo host del servizio errore anomali toosimulate arresti anomali.</span><span class="sxs-lookup"><span data-stu-id="df777-116">RestartDeployedCodePackage: Ungraceful fault toosimulate service host process crashes.</span></span>
* <span data-ttu-id="df777-117">RemoveReplica: Rimozione di replica errore normale toosimulate.</span><span class="sxs-lookup"><span data-stu-id="df777-117">RemoveReplica: Graceful fault toosimulate replica removal.</span></span>
* <span data-ttu-id="df777-118">MovePrimary: Replica toosimulate errore normale Sposta attivate dal servizio di bilanciamento del carico hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="df777-118">MovePrimary: Graceful fault toosimulate replica moves triggered by hello Service Fabric load balancer.</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll.

using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        // Replace these strings with hello actual version for your cluster and application.
        string clusterConnection = "localhost:19000";
        Uri applicationName = new Uri("fabric:/samples/PersistentToDoListApp");
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Workload Test...");
        try
        {
            RunTestAsync(clusterConnection, applicationName, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Workload Test failed: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Workload Test completed successfully.");
        return 0;
    }

    public enum ServiceWorkloads
    {
        A,
        B,
        C,
        D
    }

    public enum ServiceFabricFaults
    {
        RestartNode,
        RestartCodePackage,
        RemoveReplica,
        MovePrimary,
    }

    public static async Task RunTestAsync(string clusterConnection, Uri applicationName, Uri serviceName)
    {
        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);
        // Maximum time toowait for a service toostabilize.
        TimeSpan maxServiceStabilizationTime = TimeSpan.FromSeconds(120);

        // How many loops of faults you want tooexecute.
        uint testLoopCount = 20;
        Random random = new Random();

        for (var i = 0; i < testLoopCount; ++i)
        {
            var workload = SelectRandomValue<ServiceWorkloads>(random);
            // Start hello workload.
            var workloadTask = RunWorkloadAsync(workload);

            // While hello task is running, induce faults into hello service. They can be ungraceful faults like
            // RestartNode and RestartDeployedCodePackage or graceful faults like RemoveReplica or MovePrimary.
            var fault = SelectRandomValue<ServiceFabricFaults>(random);

            // Create a replica selector, which will select a primary replica from hello given service tootest.
            var replicaSelector = ReplicaSelector.PrimaryOf(PartitionSelector.RandomOf(serviceName));
            // Run hello selected random fault.
            await RunFaultAsync(applicationName, fault, replicaSelector, fabricClient);
            // Validate hello health and stability of hello service.
            await fabricClient.ServiceManager.ValidateServiceAsync(serviceName, maxServiceStabilizationTime);

            // Wait for hello workload toofinish successfully.
            await workloadTask;
        }
    }

    private static async Task RunFaultAsync(Uri applicationName, ServiceFabricFaults fault, ReplicaSelector selector, FabricClient client)
    {
        switch (fault)
        {
            case ServiceFabricFaults.RestartNode:
                await client.ClusterManager.RestartNodeAsync(selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RestartCodePackage:
                await client.ApplicationManager.RestartDeployedCodePackageAsync(applicationName, selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RemoveReplica:
                await client.ServiceManager.RemoveReplicaAsync(selector, CompletionMode.Verify, false);
                break;
            case ServiceFabricFaults.MovePrimary:
                await client.ServiceManager.MovePrimaryAsync(selector.PartitionSelector);
                break;
        }
    }

    private static Task RunWorkloadAsync(ServiceWorkloads workload)
    {
        throw new NotImplementedException();
        // This is where you trigger and complete your service workload.
        // Note that hello faults induced while your service workload is running will
        // fault hello primary service. Hence, you will need tooreconnect toocomplete or check
        // hello status of hello workload.
    }

    private static T SelectRandomValue<T>(Random random)
    {
        Array values = Enum.GetValues(typeof(T));
        T workload = (T)values.GetValue(random.Next(values.Length));
        return workload;
    }
}
```
