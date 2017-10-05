---
title: Creare test di failover e CHAOS per i microservizi di Azure | Documentazione Microsoft
description: "Utilizzando i test chaos dell'infrastruttura di servizi e gli scenari dei test di failover per provocare gli errori e verificare l'affidabilità dei servizi."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="dec70-103">Scenari di testabilità</span><span class="sxs-lookup"><span data-stu-id="dec70-103">Testability scenarios</span></span>
<span data-ttu-id="dec70-104">Sistemi distribuiti di grandi dimensioni come le infrastrutture cloud sono intrinsecamente inaffidabili.</span><span class="sxs-lookup"><span data-stu-id="dec70-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="dec70-105">Azure Service Fabric offre agli sviluppatori la possibilità di scrivere servizi destinati ad essere eseguiti in infrastrutture inaffidabili.</span><span class="sxs-lookup"><span data-stu-id="dec70-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="dec70-106">Per scrivere servizi di qualità elevata, gli sviluppatori devono essere in grado di mettere alla prova un'infrastruttura inaffidabile in modo da testarne la stabilità dei servizi.</span><span class="sxs-lookup"><span data-stu-id="dec70-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="dec70-107">Il servizio di analisi degli errori offre agli sviluppatori la possibilità di causare azioni di errore e testare i servizi in presenza di errori.</span><span class="sxs-lookup"><span data-stu-id="dec70-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="dec70-108">Gli errori simulati indotti, tuttavia, possono arrivare solo fino a un certo punto.</span><span class="sxs-lookup"><span data-stu-id="dec70-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="dec70-109">Per spingere il test oltre, è possibile usare gli scenari di testi disponibili in Service Fabric: test di chaos e test di failover.</span><span class="sxs-lookup"><span data-stu-id="dec70-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="dec70-110">Questi scenari simulano in tutto il cluster continui errori interfoliati, normali e anomali, per lunghi periodi di tempo.</span><span class="sxs-lookup"><span data-stu-id="dec70-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="dec70-111">Dopo la configurazione con la frequenza e il tipo di errori, il test può essere avviato tramite le API C# o PowerShell, allo scopo di generare errori nel cluster e nel servizio.</span><span class="sxs-lookup"><span data-stu-id="dec70-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="dec70-112">ChaosTestScenario è sostituito da un Chaos più resiliente, basato su servizi.</span><span class="sxs-lookup"><span data-stu-id="dec70-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="dec70-113">Consultare il nuovo articolo [Chaos in ambiente controllato](service-fabric-controlled-chaos.md) per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="dec70-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="dec70-114">Test chaos</span><span class="sxs-lookup"><span data-stu-id="dec70-114">Chaos test</span></span>
<span data-ttu-id="dec70-115">Lo scenario chaos genera errori nell’intero cluster dell’infrastruttura di servizi.</span><span class="sxs-lookup"><span data-stu-id="dec70-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="dec70-116">Lo scenario comprime in alcune ore gli errori che in genere si osservano in mesi o anni.</span><span class="sxs-lookup"><span data-stu-id="dec70-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="dec70-117">La combinazione di errori interfoliati con un'elevata frequenza di errori consente di trovare casi limite che altrimenti non verrebbero considerati.</span><span class="sxs-lookup"><span data-stu-id="dec70-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="dec70-118">In tal modo è possibile ottenere un notevole miglioramento della qualità del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="dec70-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="dec70-119">Errori simulati nel test chaos</span><span class="sxs-lookup"><span data-stu-id="dec70-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="dec70-120">Riavvio di un nodo</span><span class="sxs-lookup"><span data-stu-id="dec70-120">Restart a node</span></span>
* <span data-ttu-id="dec70-121">Riavvio di un pacchetto di codice distribuito</span><span class="sxs-lookup"><span data-stu-id="dec70-121">Restart a deployed code package</span></span>
* <span data-ttu-id="dec70-122">Rimozione di una replica</span><span class="sxs-lookup"><span data-stu-id="dec70-122">Remove a replica</span></span>
* <span data-ttu-id="dec70-123">Riavvio di una replica</span><span class="sxs-lookup"><span data-stu-id="dec70-123">Restart a replica</span></span>
* <span data-ttu-id="dec70-124">Spostamento di una replica primaria (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="dec70-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="dec70-125">Spostamento di una replica secondaria (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="dec70-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="dec70-126">Il test chaos esegue più iterazioni di errori e di convalide cluster per il periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="dec70-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="dec70-127">È possibile configurare anche il tempo impiegato per la stabilizzazione del cluster e il completamento della convalida.</span><span class="sxs-lookup"><span data-stu-id="dec70-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="dec70-128">Lo scenario ha esito negativo anche se si verifica un singolo errore nella convalida del cluster.</span><span class="sxs-lookup"><span data-stu-id="dec70-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="dec70-129">Si consideri, ad esempio, un test configurato per un'esecuzione della durata di un'ora e con un massimo di tre errori simultanei.</span><span class="sxs-lookup"><span data-stu-id="dec70-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="dec70-130">Il test provocherà tre errori e quindi convaliderà l'integrità del cluster.</span><span class="sxs-lookup"><span data-stu-id="dec70-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="dec70-131">Il test ripeterà il passaggio precedente fino a quando non sarà trascorsa un'ora o lo stato del cluster diventerà non integro.</span><span class="sxs-lookup"><span data-stu-id="dec70-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="dec70-132">Se in una qualsiasi iterazione il cluster diventa non integro, ovvero non si stabilizza entro un tempo configurato, il test avrà esito negativo con un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="dec70-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="dec70-133">Questa eccezione indica che si è verificato un errore ed è necessaria un'ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="dec70-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="dec70-134">Nella forma attuale, il motore di generazione di errori del test Chaos provoca solo errori sicuri.</span><span class="sxs-lookup"><span data-stu-id="dec70-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="dec70-135">In assenza di errori esterni, quindi, non si verifica mai una perdita di quorum o di dati.</span><span class="sxs-lookup"><span data-stu-id="dec70-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="dec70-136">Opzioni di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="dec70-136">Important configuration options</span></span>
* <span data-ttu-id="dec70-137">**TimeToRun**: tempo totale per il quale il test verrà eseguito prima del completamento con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="dec70-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="dec70-138">Il test può essere completato in anticipo anziché produrre un errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="dec70-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="dec70-139">**MaxClusterStabilizationTimeout**: tempo di attesa massimo perché il cluster diventi integro prima che ne venga dichiarato l'esito negativo.</span><span class="sxs-lookup"><span data-stu-id="dec70-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="dec70-140">I controlli eseguiti verificano che il cluster e il servizio siano integri, che la dimensione del set di repliche di destinazione sia stata raggiunta per la partizione di servizio e che non siano presenti repliche InBuild.</span><span class="sxs-lookup"><span data-stu-id="dec70-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="dec70-141">**MaxConcurrentFaults**: numero massimo di errori simultanei indotti in ogni iterazione.</span><span class="sxs-lookup"><span data-stu-id="dec70-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="dec70-142">Maggiore è il numero, più aggressivo è il test e più complesse saranno le combinazioni di failover e transizioni.</span><span class="sxs-lookup"><span data-stu-id="dec70-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="dec70-143">Il test garantisce che in assenza di errori esterni non si verificherà una perdita di quorum o di dati, a prescindere da quanto è elevata la configurazione.</span><span class="sxs-lookup"><span data-stu-id="dec70-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="dec70-144">**EnableMoveReplicaFaults**: abilita o disabilita gli errori che causano lo spostamento delle repliche primarie o secondarie.</span><span class="sxs-lookup"><span data-stu-id="dec70-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="dec70-145">Questi errori sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dec70-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="dec70-146">**WaitTimeBetweenIterations**: quantità di tempo di attesa tra due iterazioni, ad esempio dopo un ciclo di errori e la convalida corrispondente.</span><span class="sxs-lookup"><span data-stu-id="dec70-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="dec70-147">Come eseguire il test chaos</span><span class="sxs-lookup"><span data-stu-id="dec70-147">How to run the chaos test</span></span>
<span data-ttu-id="dec70-148">Esempio C#</span><span class="sxs-lookup"><span data-stu-id="dec70-148">C# sample</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // The chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create the scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

<span data-ttu-id="dec70-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dec70-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="dec70-150">Test di failover</span><span class="sxs-lookup"><span data-stu-id="dec70-150">Failover test</span></span>
<span data-ttu-id="dec70-151">Lo scenario di test di failover è una versione dello scenario di test chaos destinata a una specifica partizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="dec70-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="dec70-152">Verifica l'effetto del failover in una specifica partizione di servizio senza interessare gli altri servizi.</span><span class="sxs-lookup"><span data-stu-id="dec70-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="dec70-153">Una volta configurato con informazioni sulla partizione di destinazione e altri parametri, il test viene eseguito come strumento lato client che usa API C# o PowerShell per generare errori per una partizione di servizio.</span><span class="sxs-lookup"><span data-stu-id="dec70-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="dec70-154">Lo scenario ripete una sequenza di errori simulati e test di convalida del servizio, mentre viene eseguita la logica di business per fornire un carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="dec70-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="dec70-155">Un errore nella convalida del servizio indica un problema necessita di ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="dec70-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="dec70-156">Errori simulati nel test di failover</span><span class="sxs-lookup"><span data-stu-id="dec70-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="dec70-157">Riavvio di un pacchetto di codice distribuito in cui è ospitata la partizione</span><span class="sxs-lookup"><span data-stu-id="dec70-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="dec70-158">Rimozione di una replica primaria o secondaria o di un'istanza senza stato</span><span class="sxs-lookup"><span data-stu-id="dec70-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="dec70-159">Riavvio di una replica primaria o secondaria (in caso di servizio persistente)</span><span class="sxs-lookup"><span data-stu-id="dec70-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="dec70-160">Spostamento di una replica primaria</span><span class="sxs-lookup"><span data-stu-id="dec70-160">Move a primary replica</span></span>
* <span data-ttu-id="dec70-161">Spostamento di una replica secondaria</span><span class="sxs-lookup"><span data-stu-id="dec70-161">Move a secondary replica</span></span>
* <span data-ttu-id="dec70-162">Riavvio della partizione</span><span class="sxs-lookup"><span data-stu-id="dec70-162">Restart the partition</span></span>

<span data-ttu-id="dec70-163">Il test di failover provoca un errore scelto e quindi esegue la convalida del servizio per garantirne la stabilità.</span><span class="sxs-lookup"><span data-stu-id="dec70-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="dec70-164">Il test di failover provoca un solo errore per volta, anziché i possibili errori multipli generati dal test chaos.</span><span class="sxs-lookup"><span data-stu-id="dec70-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="dec70-165">Se dopo ogni errore la partizione di servizio non si stabilizza entro il timeout configurato, il test ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="dec70-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="dec70-166">Il test provoca solo errori sicuri.</span><span class="sxs-lookup"><span data-stu-id="dec70-166">The test induces only safe faults.</span></span> <span data-ttu-id="dec70-167">In assenza di errori esterni, quindi, non si verifica una perdita di quorum o di dati.</span><span class="sxs-lookup"><span data-stu-id="dec70-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="dec70-168">Opzioni di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="dec70-168">Important configuration options</span></span>
* <span data-ttu-id="dec70-169">**PartitionSelector**: oggetto selettore che specifica la partizione che deve essere impostata come destinazione.</span><span class="sxs-lookup"><span data-stu-id="dec70-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="dec70-170">**TimeToRun**: tempo totale per il quale il test verrà eseguito prima del completamento.</span><span class="sxs-lookup"><span data-stu-id="dec70-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="dec70-171">**MaxServiceStabilizationTimeout**: tempo di attesa massimo perché il cluster diventi integro prima che ne venga dichiarato l'esito negativo.</span><span class="sxs-lookup"><span data-stu-id="dec70-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="dec70-172">I controlli eseguiti verificano che il cluster sia integro, che la dimensione del set di repliche di destinazione sia stata raggiunta per tutte le partizioni e che non siano presenti repliche InBuild.</span><span class="sxs-lookup"><span data-stu-id="dec70-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="dec70-173">**WaitTimeBetweenFaults**: tempo di attesa tra ogni ciclo di errore e di convalida.</span><span class="sxs-lookup"><span data-stu-id="dec70-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="dec70-174">Come eseguire il test di failover</span><span class="sxs-lookup"><span data-stu-id="dec70-174">How to run the failover test</span></span>
<span data-ttu-id="dec70-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="dec70-175">**C#**</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // The chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create the scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


<span data-ttu-id="dec70-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="dec70-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
