---
title: Simulare errori nei microservizi di Azure | Documentazione Microsoft
description: Come proteggere i servizi in caso di errori normali e anomali
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
ms.openlocfilehash: 7ec671c23e101d0f7401bd4656fb201111602cad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="simulate-failures-during-service-workloads"></a><span data-ttu-id="3eddf-103">Simulare gli errori durante i carichi di lavoro del servizio</span><span class="sxs-lookup"><span data-stu-id="3eddf-103">Simulate failures during service workloads</span></span>
<span data-ttu-id="3eddf-104">Gli scenari di testabilità in Service Fabric di Azure consentono agli sviluppatori di non preoccuparsi della gestione dei singoli errori.</span><span class="sxs-lookup"><span data-stu-id="3eddf-104">The testability scenarios in Azure Service Fabric enable developers to not worry about dealing with individual faults.</span></span> <span data-ttu-id="3eddf-105">Tuttavia, sono disponibili scenari in cui potrebbe essere necessaria un'interfoliazione esplicita del carico di lavoro client e degli errori.</span><span class="sxs-lookup"><span data-stu-id="3eddf-105">There are scenarios, however, where an explicit interleaving of client workload and failures might be needed.</span></span> <span data-ttu-id="3eddf-106">L'interfoliazione del carico di lavoro client e degli errori garantisce che il servizio stia effettivamente eseguendo un’azione quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="3eddf-106">The interleaving of client workload and faults ensures that the service is actually performing some action when failure happens.</span></span> <span data-ttu-id="3eddf-107">Dato il livello di controllo fornito dalla testabilità, questi errori potrebbero verificarsi in momenti precisi dell'esecuzione del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3eddf-107">Given the level of control that testability provides, these could be at precise points of the workload execution.</span></span> <span data-ttu-id="3eddf-108">L’induzione degli errori in stati diversi nell'applicazione può consentire di individuare bug e migliorare la qualità.</span><span class="sxs-lookup"><span data-stu-id="3eddf-108">This induction of faults at different states in the application can find bugs and improve quality.</span></span>

## <a name="sample-custom-scenario"></a><span data-ttu-id="3eddf-109">Esempio di scenario personalizzato</span><span class="sxs-lookup"><span data-stu-id="3eddf-109">Sample custom scenario</span></span>
<span data-ttu-id="3eddf-110">In questo test viene illustrato uno scenario in cui si verifica l'interfoliazione del carico di lavoro di business con [errori normali e anomali](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span><span class="sxs-lookup"><span data-stu-id="3eddf-110">This test shows a scenario that interleaves the business workload with [graceful and ungraceful failures](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span></span> <span data-ttu-id="3eddf-111">Per ottenere risultati ottimali, gli errori devono essere indotti nel corso delle operazioni del servizio o del calcolo.</span><span class="sxs-lookup"><span data-stu-id="3eddf-111">The faults should be induced in the middle of service operations or compute for best results.</span></span>

<span data-ttu-id="3eddf-112">Esaminiamo in dettaglio un esempio di servizio che espone quattro carichi di lavoro: A, B, C e D. Ognuno corrisponde a un insieme di flussi di lavoro e potrebbe essere calcolo, archiviazione o una combinazione.</span><span class="sxs-lookup"><span data-stu-id="3eddf-112">Let's walk through an example of a service that exposes four workloads: A, B, C, and D. Each corresponds to a set of workflows and could be compute, storage, or a mix.</span></span> <span data-ttu-id="3eddf-113">Per ragioni di semplicità, nel nostro esempio verranno estrapolati i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3eddf-113">For the sake of simplicity, we will abstract out the workloads in our example.</span></span> <span data-ttu-id="3eddf-114">I diversi errori eseguiti in questo esempio sono:</span><span class="sxs-lookup"><span data-stu-id="3eddf-114">The different faults executed in this example are:</span></span>

* <span data-ttu-id="3eddf-115">RestartNode: errore anomalo per simulare un riavvio del computer.</span><span class="sxs-lookup"><span data-stu-id="3eddf-115">RestartNode: Ungraceful fault to simulate a machine restart.</span></span>
* <span data-ttu-id="3eddf-116">RestartDeployedCodePackage: errore anomalo per simulare arresti anomali del processo host del servizio.</span><span class="sxs-lookup"><span data-stu-id="3eddf-116">RestartDeployedCodePackage: Ungraceful fault to simulate service host process crashes.</span></span>
* <span data-ttu-id="3eddf-117">RemoveReplica: errore normale per simulare la rimozione della replica.</span><span class="sxs-lookup"><span data-stu-id="3eddf-117">RemoveReplica: Graceful fault to simulate replica removal.</span></span>
* <span data-ttu-id="3eddf-118">MovePrimary: errore normale per simulare gli spostamenti della replica attivati dal servizio di bilanciamento del carico di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3eddf-118">MovePrimary: Graceful fault to simulate replica moves triggered by the Service Fabric load balancer.</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll.

using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        // Replace these strings with the actual version for your cluster and application.
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
        // Maximum time to wait for a service to stabilize.
        TimeSpan maxServiceStabilizationTime = TimeSpan.FromSeconds(120);

        // How many loops of faults you want to execute.
        uint testLoopCount = 20;
        Random random = new Random();

        for (var i = 0; i < testLoopCount; ++i)
        {
            var workload = SelectRandomValue<ServiceWorkloads>(random);
            // Start the workload.
            var workloadTask = RunWorkloadAsync(workload);

            // While the task is running, induce faults into the service. They can be ungraceful faults like
            // RestartNode and RestartDeployedCodePackage or graceful faults like RemoveReplica or MovePrimary.
            var fault = SelectRandomValue<ServiceFabricFaults>(random);

            // Create a replica selector, which will select a primary replica from the given service to test.
            var replicaSelector = ReplicaSelector.PrimaryOf(PartitionSelector.RandomOf(serviceName));
            // Run the selected random fault.
            await RunFaultAsync(applicationName, fault, replicaSelector, fabricClient);
            // Validate the health and stability of the service.
            await fabricClient.ServiceManager.ValidateServiceAsync(serviceName, maxServiceStabilizationTime);

            // Wait for the workload to finish successfully.
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
        // Note that the faults induced while your service workload is running will
        // fault the primary service. Hence, you will need to reconnect to complete or check
        // the status of the workload.
    }

    private static T SelectRandomValue<T>(Random random)
    {
        Array values = Enum.GetValues(typeof(T));
        T workload = (T)values.GetValue(random.Next(values.Length));
        return workload;
    }
}
```
