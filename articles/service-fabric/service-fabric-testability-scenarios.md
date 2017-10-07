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
# <a name="testability-scenarios"></a>Scenari di testabilità
Sistemi distribuiti di grandi dimensioni come le infrastrutture cloud sono intrinsecamente inaffidabili. Azure Service Fabric fornisce agli sviluppatori hello possibilità toowrite servizi toorun sopra infrastrutture inaffidabili. In servizi di alta qualità toowrite ordine, gli sviluppatori devono tooinduce in grado di toobe stabilità di hello tootest tale infrastruttura non affidabile dei servizi.

Hello errore Analysis Services offre agli sviluppatori di servizi di hello possibilità tooinduce errore azioni tootest in presenza di hello di errori. Gli errori simulati indotti, tuttavia, possono arrivare solo fino a un certo punto. hello tootake test, inoltre, è possibile utilizzare gli scenari di test hello in Service Fabric: un test chaos e un test di failover. Questi scenari simulano continui errori interleaved, sia normale e anomali, in tutto il cluster hello per periodi prolungati di tempo. Dopo aver configurato un test con frequenza hello e tipo di errori, può essere avviato tramite l'API c# o PowerShell, gli errori di toogenerate cluster hello e il servizio.

> [!WARNING]
> ChaosTestScenario è sostituito da un Chaos più resiliente, basato su servizi. Consultare l'articolo nuovo toohello [controllato Chaos](service-fabric-controlled-chaos.md) per altri dettagli.
> 
> 

## <a name="chaos-test"></a>Test chaos
scenario chaos Hello genera errori nel cluster di Service Fabric intera hello. scenario di Hello comprime presenza di errori in genere in mesi o anni tooa alcune ore. combinazione di Hello di interfoliazione errori con frequenza elevata errore hello trova nei casi in cui vengono persi in caso contrario. In tal modo tooa significativo miglioramento nella qualità del codice del servizio hello hello.

### <a name="faults-simulated-in-hello-chaos-test"></a>Errori simulati in test chaos hello
* Riavvio di un nodo
* Riavvio di un pacchetto di codice distribuito
* Rimozione di una replica
* Riavvio di una replica
* Spostamento di una replica primaria (facoltativo)
* Spostamento di una replica secondaria (facoltativo)

esecuzione dei test di chaos Hello più iterazioni di errori e le convalide di cluster per hello periodo di tempo specificato. tempo di Hello per toostabilize cluster hello e per la convalida toosucceed è anche configurabile. scenario di Hello ha esito negativo quando si raggiunge un singolo errore di convalida del cluster.

Si consideri, ad esempio, che un test imposta toorun per un'ora con un massimo di tre errori simultanei. test hello verrà indurre tre errori e quindi convalidare l'integrità del cluster hello. test hello scorrerà dal passaggio precedente hello fino a quando il cluster hello diventa non integro o passa a un'ora. Se il cluster hello diventa non integro in un'iterazione, vale a dire non stabilizzare entro un periodo di tempo configurato, test hello avrà esito negativo con un'eccezione. Questa eccezione indica che si è verificato un errore ed è necessaria un'ulteriore analisi.

Nella sua forma corrente, motore di generazione di hello di test chaos hello provoca errori solo-safe. Ciò significa che in assenza di hello degli errori esterni, una quorum o perdita di dati non verrà mai eseguiti.

### <a name="important-configuration-options"></a>Opzioni di configurazione importanti
* **TimeToRun**: tempo totale di tale test hello verrà eseguito prima di completare con esito positivo. test di Hello può finire in precedenza anziché un errore di convalida.
* **MaxClusterStabilizationTimeout**: quantità massima di tempo toowait per hello cluster toobecome integro prima dell'errore hello test. Hello controlli eseguiti sono indica se l'integrità del cluster è OK, l'integrità del servizio è OK, hello dimensioni set di repliche di destinazione viene realizzata per la partizione del servizio hello ed è presente alcuna replica InBuild.
* **MaxConcurrentFaults**: numero massimo di errori simultanei indotti in ogni iterazione. salve maggiore hello, hello più aggressiva hello prova, pertanto i failover più complessi e combinazioni di transizione. test di Hello garantisce che in assenza di errori esterni non sarà disponibile una quorum o perdita di dati, indipendentemente dalla modalità elevata questa configurazione è.
* **EnableMoveReplicaFaults**: Abilita o disabilita gli errori di hello che causano spostamento hello di hello repliche primarie o secondarie. Questi errori sono disabilitati per impostazione predefinita.
* **WaitTimeBetweenIterations**: quantità di tempo toowait tra le iterazioni, ad esempio dopo un ciclo di convalida corrispondente e gli errori.

### <a name="how-toorun-hello-chaos-test"></a>Come i test chaos hello toorun
Esempio C#

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

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Test di failover
scenario di test di failover Hello è una versione di uno scenario di test chaos hello destinato a una partizione di servizio specifico. Verifica effetto hello di failover in una partizione di servizio specifico, lasciando al contempo hello altri servizi interessati. Una volta che viene configurato con informazioni sulla partizione di destinazione hello e altri parametri, viene eseguito come uno strumento sul lato client che utilizza le API di c# o PowerShell errori toogenerate per una partizione del servizio. scenario di Hello iterazione di una sequenza di errori simulati e convalida del servizio mentre la logica di business in esecuzione su hello lato tooprovide un carico di lavoro. Un errore nella convalida del servizio indica un problema necessita di ulteriore analisi.

### <a name="faults-simulated-in-hello-failover-test"></a>Errori simulati in test di failover hello
* Riavviare un pacchetto di codice distribuito in cui è ospitato partizione hello
* Rimozione di una replica primaria o secondaria o di un'istanza senza stato
* Riavvio di una replica primaria o secondaria (in caso di servizio persistente)
* Spostamento di una replica primaria
* Spostamento di una replica secondaria
* Riavviare partizione hello

test di failover Hello provoca un errore scelto e quindi viene eseguita la convalida su hello servizio tooensure la stabilità. test di failover Hello provoca solo uno di errore in un'ora, invece di toopossible più errori nel test chaos hello. Se la partizione di servizio hello non stabilizzarsi entro il timeout configurato di hello dopo ogni errore, il test di hello ha esito negativo. test di Hello provoca solo gli errori-safe. In assenza di errori esterni, quindi, non si verifica una perdita di quorum o di dati.

### <a name="important-configuration-options"></a>Opzioni di configurazione importanti
* **PartitionSelector**: oggetto selettore che specifica una partizione di hello toobe di destinazione.
* **TimeToRun**: tempo totale di tale test hello verrà eseguito prima di terminare.
* **MaxServiceStabilizationTimeout**: quantità massima di tempo toowait per hello cluster toobecome integro prima dell'errore hello test. Hello controlli eseguiti sono indica se l'integrità del servizio è OK, hello dimensioni set di repliche di destinazione viene realizzata per tutte le partizioni, ed è presente alcuna replica InBuild.
* **WaitTimeBetweenFaults**: quantità di tempo toowait tra ogni ciclo di convalida e di errore.

### <a name="how-toorun-hello-failover-test"></a>Come i test failover hello toorun
**C#**

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


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
