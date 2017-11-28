---
title: test di failover e chaos aaaCreate per microservizi Azure | Documenti Microsoft
description: "Tramite i failover e il test di hello Service Fabric chaos errori tooinduce scenari di test e verificare l'affidabilità di hello dei servizi."
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
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="d490b-103">Scenari di testabilità</span><span class="sxs-lookup"><span data-stu-id="d490b-103">Testability scenarios</span></span>
<span data-ttu-id="d490b-104">Sistemi distribuiti di grandi dimensioni come le infrastrutture cloud sono intrinsecamente inaffidabili.</span><span class="sxs-lookup"><span data-stu-id="d490b-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="d490b-105">Azure Service Fabric fornisce agli sviluppatori hello possibilità toowrite servizi toorun sopra infrastrutture inaffidabili.</span><span class="sxs-lookup"><span data-stu-id="d490b-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="d490b-106">In servizi di alta qualità toowrite ordine, gli sviluppatori devono tooinduce in grado di toobe stabilità di hello tootest tale infrastruttura non affidabile dei servizi.</span><span class="sxs-lookup"><span data-stu-id="d490b-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="d490b-107">Hello errore Analysis Services offre agli sviluppatori di servizi di hello possibilità tooinduce errore azioni tootest in presenza di hello di errori.</span><span class="sxs-lookup"><span data-stu-id="d490b-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="d490b-108">Gli errori simulati indotti, tuttavia, possono arrivare solo fino a un certo punto.</span><span class="sxs-lookup"><span data-stu-id="d490b-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="d490b-109">hello tootake test, inoltre, è possibile utilizzare gli scenari di test hello in Service Fabric: un test chaos e un test di failover.</span><span class="sxs-lookup"><span data-stu-id="d490b-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="d490b-110">Questi scenari simulano continui errori interleaved, sia normale e anomali, in tutto il cluster hello per periodi prolungati di tempo.</span><span class="sxs-lookup"><span data-stu-id="d490b-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="d490b-111">Dopo aver configurato un test con frequenza hello e tipo di errori, può essere avviato tramite l'API c# o PowerShell, gli errori di toogenerate cluster hello e il servizio.</span><span class="sxs-lookup"><span data-stu-id="d490b-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="d490b-112">ChaosTestScenario è sostituito da un Chaos più resiliente, basato su servizi.</span><span class="sxs-lookup"><span data-stu-id="d490b-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="d490b-113">Consultare l'articolo nuovo toohello [controllato Chaos](service-fabric-controlled-chaos.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="d490b-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="d490b-114">Test chaos</span><span class="sxs-lookup"><span data-stu-id="d490b-114">Chaos test</span></span>
<span data-ttu-id="d490b-115">scenario chaos Hello genera errori nel cluster di Service Fabric intera hello.</span><span class="sxs-lookup"><span data-stu-id="d490b-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="d490b-116">scenario di Hello comprime presenza di errori in genere in mesi o anni tooa alcune ore.</span><span class="sxs-lookup"><span data-stu-id="d490b-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="d490b-117">combinazione di Hello di interfoliazione errori con frequenza elevata errore hello trova nei casi in cui vengono persi in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="d490b-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="d490b-118">In tal modo tooa significativo miglioramento nella qualità del codice del servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="d490b-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="d490b-119">Errori simulati in test chaos hello</span><span class="sxs-lookup"><span data-stu-id="d490b-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="d490b-120">Riavvio di un nodo</span><span class="sxs-lookup"><span data-stu-id="d490b-120">Restart a node</span></span>
* <span data-ttu-id="d490b-121">Riavvio di un pacchetto di codice distribuito</span><span class="sxs-lookup"><span data-stu-id="d490b-121">Restart a deployed code package</span></span>
* <span data-ttu-id="d490b-122">Rimozione di una replica</span><span class="sxs-lookup"><span data-stu-id="d490b-122">Remove a replica</span></span>
* <span data-ttu-id="d490b-123">Riavvio di una replica</span><span class="sxs-lookup"><span data-stu-id="d490b-123">Restart a replica</span></span>
* <span data-ttu-id="d490b-124">Spostamento di una replica primaria (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="d490b-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="d490b-125">Spostamento di una replica secondaria (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="d490b-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="d490b-126">esecuzione dei test di chaos Hello più iterazioni di errori e le convalide di cluster per hello periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="d490b-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="d490b-127">tempo di Hello per toostabilize cluster hello e per la convalida toosucceed è anche configurabile.</span><span class="sxs-lookup"><span data-stu-id="d490b-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="d490b-128">scenario di Hello ha esito negativo quando si raggiunge un singolo errore di convalida del cluster.</span><span class="sxs-lookup"><span data-stu-id="d490b-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="d490b-129">Si consideri, ad esempio, che un test imposta toorun per un'ora con un massimo di tre errori simultanei.</span><span class="sxs-lookup"><span data-stu-id="d490b-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="d490b-130">test hello verrà indurre tre errori e quindi convalidare l'integrità del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d490b-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="d490b-131">test hello scorrerà dal passaggio precedente hello fino a quando il cluster hello diventa non integro o passa a un'ora.</span><span class="sxs-lookup"><span data-stu-id="d490b-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="d490b-132">Se il cluster hello diventa non integro in un'iterazione, vale a dire non stabilizzare entro un periodo di tempo configurato, test hello avrà esito negativo con un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="d490b-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="d490b-133">Questa eccezione indica che si è verificato un errore ed è necessaria un'ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="d490b-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="d490b-134">Nella sua forma corrente, motore di generazione di hello di test chaos hello provoca errori solo-safe.</span><span class="sxs-lookup"><span data-stu-id="d490b-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="d490b-135">Ciò significa che in assenza di hello degli errori esterni, una quorum o perdita di dati non verrà mai eseguiti.</span><span class="sxs-lookup"><span data-stu-id="d490b-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="d490b-136">Opzioni di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="d490b-136">Important configuration options</span></span>
* <span data-ttu-id="d490b-137">**TimeToRun**: tempo totale di tale test hello verrà eseguito prima di completare con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="d490b-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="d490b-138">test di Hello può finire in precedenza anziché un errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="d490b-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="d490b-139">**MaxClusterStabilizationTimeout**: quantità massima di tempo toowait per hello cluster toobecome integro prima dell'errore hello test.</span><span class="sxs-lookup"><span data-stu-id="d490b-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="d490b-140">Hello controlli eseguiti sono indica se l'integrità del cluster è OK, l'integrità del servizio è OK, hello dimensioni set di repliche di destinazione viene realizzata per la partizione del servizio hello ed è presente alcuna replica InBuild.</span><span class="sxs-lookup"><span data-stu-id="d490b-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="d490b-141">**MaxConcurrentFaults**: numero massimo di errori simultanei indotti in ogni iterazione.</span><span class="sxs-lookup"><span data-stu-id="d490b-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="d490b-142">salve maggiore hello, hello più aggressiva hello prova, pertanto i failover più complessi e combinazioni di transizione.</span><span class="sxs-lookup"><span data-stu-id="d490b-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="d490b-143">test di Hello garantisce che in assenza di errori esterni non sarà disponibile una quorum o perdita di dati, indipendentemente dalla modalità elevata questa configurazione è.</span><span class="sxs-lookup"><span data-stu-id="d490b-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="d490b-144">**EnableMoveReplicaFaults**: Abilita o disabilita gli errori di hello che causano spostamento hello di hello repliche primarie o secondarie.</span><span class="sxs-lookup"><span data-stu-id="d490b-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="d490b-145">Questi errori sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d490b-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="d490b-146">**WaitTimeBetweenIterations**: quantità di tempo toowait tra le iterazioni, ad esempio dopo un ciclo di convalida corrispondente e gli errori.</span><span class="sxs-lookup"><span data-stu-id="d490b-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="d490b-147">Come i test chaos hello toorun</span><span class="sxs-lookup"><span data-stu-id="d490b-147">How toorun hello chaos test</span></span>
<span data-ttu-id="d490b-148">Esempio C#</span><span class="sxs-lookup"><span data-stu-id="d490b-148">C# sample</span></span>

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

        // hello chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create hello scenario class and execute it asynchronously.
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

<span data-ttu-id="d490b-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d490b-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="d490b-150">Test di failover</span><span class="sxs-lookup"><span data-stu-id="d490b-150">Failover test</span></span>
<span data-ttu-id="d490b-151">scenario di test di failover Hello è una versione di uno scenario di test chaos hello destinato a una partizione di servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="d490b-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="d490b-152">Verifica effetto hello di failover in una partizione di servizio specifico, lasciando al contempo hello altri servizi interessati.</span><span class="sxs-lookup"><span data-stu-id="d490b-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="d490b-153">Una volta che viene configurato con informazioni sulla partizione di destinazione hello e altri parametri, viene eseguito come uno strumento sul lato client che utilizza le API di c# o PowerShell errori toogenerate per una partizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="d490b-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="d490b-154">scenario di Hello iterazione di una sequenza di errori simulati e convalida del servizio mentre la logica di business in esecuzione su hello lato tooprovide un carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d490b-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="d490b-155">Un errore nella convalida del servizio indica un problema necessita di ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="d490b-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="d490b-156">Errori simulati in test di failover hello</span><span class="sxs-lookup"><span data-stu-id="d490b-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="d490b-157">Riavviare un pacchetto di codice distribuito in cui è ospitato partizione hello</span><span class="sxs-lookup"><span data-stu-id="d490b-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="d490b-158">Rimozione di una replica primaria o secondaria o di un'istanza senza stato</span><span class="sxs-lookup"><span data-stu-id="d490b-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="d490b-159">Riavvio di una replica primaria o secondaria (in caso di servizio persistente)</span><span class="sxs-lookup"><span data-stu-id="d490b-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="d490b-160">Spostamento di una replica primaria</span><span class="sxs-lookup"><span data-stu-id="d490b-160">Move a primary replica</span></span>
* <span data-ttu-id="d490b-161">Spostamento di una replica secondaria</span><span class="sxs-lookup"><span data-stu-id="d490b-161">Move a secondary replica</span></span>
* <span data-ttu-id="d490b-162">Riavviare partizione hello</span><span class="sxs-lookup"><span data-stu-id="d490b-162">Restart hello partition</span></span>

<span data-ttu-id="d490b-163">test di failover Hello provoca un errore scelto e quindi viene eseguita la convalida su hello servizio tooensure la stabilità.</span><span class="sxs-lookup"><span data-stu-id="d490b-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="d490b-164">test di failover Hello provoca solo uno di errore in un'ora, invece di toopossible più errori nel test chaos hello.</span><span class="sxs-lookup"><span data-stu-id="d490b-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="d490b-165">Se la partizione di servizio hello non stabilizzarsi entro il timeout configurato di hello dopo ogni errore, il test di hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d490b-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="d490b-166">test di Hello provoca solo gli errori-safe.</span><span class="sxs-lookup"><span data-stu-id="d490b-166">hello test induces only safe faults.</span></span> <span data-ttu-id="d490b-167">In assenza di errori esterni, quindi, non si verifica una perdita di quorum o di dati.</span><span class="sxs-lookup"><span data-stu-id="d490b-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="d490b-168">Opzioni di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="d490b-168">Important configuration options</span></span>
* <span data-ttu-id="d490b-169">**PartitionSelector**: oggetto selettore che specifica una partizione di hello toobe di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d490b-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="d490b-170">**TimeToRun**: tempo totale di tale test hello verrà eseguito prima di terminare.</span><span class="sxs-lookup"><span data-stu-id="d490b-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="d490b-171">**MaxServiceStabilizationTimeout**: quantità massima di tempo toowait per hello cluster toobecome integro prima dell'errore hello test.</span><span class="sxs-lookup"><span data-stu-id="d490b-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="d490b-172">Hello controlli eseguiti sono indica se l'integrità del servizio è OK, hello dimensioni set di repliche di destinazione viene realizzata per tutte le partizioni, ed è presente alcuna replica InBuild.</span><span class="sxs-lookup"><span data-stu-id="d490b-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="d490b-173">**WaitTimeBetweenFaults**: quantità di tempo toowait tra ogni ciclo di convalida e di errore.</span><span class="sxs-lookup"><span data-stu-id="d490b-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="d490b-174">Come i test failover hello toorun</span><span class="sxs-lookup"><span data-stu-id="d490b-174">How toorun hello failover test</span></span>
<span data-ttu-id="d490b-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="d490b-175">**C#**</span></span>

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

        // hello chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create hello scenario class and execute it asynchronously.
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


<span data-ttu-id="d490b-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="d490b-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
