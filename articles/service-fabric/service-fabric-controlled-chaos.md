---
title: Eseguire Chaos nei cluster di Service Fabric | Documentazione Microsoft
description: Uso delle API del servizio di fault injection e di analisi del cluster per la gestione di Chaos nel cluster.
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 3b3b93bc9ec5ecdcfc289e5b62e84de6aa4172ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="b359e-103">Eseguire Chaos in ambiente controllato nei cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b359e-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="b359e-104">I sistemi distribuiti di grandi dimensioni come le infrastrutture cloud sono intrinsecamente inaffidabili.</span><span class="sxs-lookup"><span data-stu-id="b359e-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="b359e-105">Azure Service Fabric consente agli sviluppatori di scrivere servizi distribuiti affidabili in un'infrastruttura inaffidabile.</span><span class="sxs-lookup"><span data-stu-id="b359e-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="b359e-106">Per scrivere servizi distribuiti affidabili in un'infrastruttura inaffidabile, gli sviluppatori devono poter testare la stabilità dei servizi quando nell'infrastruttura inaffidabile sottostante si verificano transizioni di stato complesse a causa di errori.</span><span class="sxs-lookup"><span data-stu-id="b359e-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span></span>

<span data-ttu-id="b359e-107">Il [servizio di fault injection e analisi del cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (noto anche come servizio di analisi degli errori) offre agli sviluppatori la possibilità di causare errori per testare i servizi.</span><span class="sxs-lookup"><span data-stu-id="b359e-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span></span> <span data-ttu-id="b359e-108">Questi errori simulati mirati, ad esempio il [riavvio di una partizione](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), consentono di generare le transizioni di stato più comuni.</span><span class="sxs-lookup"><span data-stu-id="b359e-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span></span> <span data-ttu-id="b359e-109">Gli errori simulati mirati sono tuttavia parziali per definizione e quindi possono non coprire i bug che si verificano solo in sequenze di transizioni di stato difficili da prevedere, lunghe e complesse.</span><span class="sxs-lookup"><span data-stu-id="b359e-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="b359e-110">Per un test imparziale, è possibile usare Chaos.</span><span class="sxs-lookup"><span data-stu-id="b359e-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="b359e-111">Chaos simula errori periodici con interfoliazione, normali e anomali, nel cluster per lunghi periodi di tempo.</span><span class="sxs-lookup"><span data-stu-id="b359e-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="b359e-112">Dopo aver configurato Chaos con la frequenza e la tipologia di errori, è possibile avviarlo attraverso le API C# o PowerShell per iniziare a generare errori nel cluster e nei servizi.</span><span class="sxs-lookup"><span data-stu-id="b359e-112">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C# or Powershell API to start generating faults in the cluster and in your services.</span></span> <span data-ttu-id="b359e-113">È possibile configurare Chaos per l'esecuzione per un periodo di tempo specifico (ad esempio per un'ora), dopo il quale Chaos si arresta automaticamente oppure è possibile chiamare l'API StopChaos (C# o PowerShell) per arrestarlo in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="b359e-113">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) to stop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="b359e-114">Nella sua forma attuale, Chaos causa solo errori sicuri, il che implica che in assenza di errori esterni non si verifica mai una perdita del quorum o di dati.</span><span class="sxs-lookup"><span data-stu-id="b359e-114">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="b359e-115">Durante l'esecuzione, Chaos genera eventi diversi che acquisiscono lo stato dell'esecuzione al momento.</span><span class="sxs-lookup"><span data-stu-id="b359e-115">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="b359e-116">Un oggetto ExecutingFaultsEvent contiene ad esempio tutti gli errori eseguiti da Chaos nell'iterazione.</span><span class="sxs-lookup"><span data-stu-id="b359e-116">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span></span> <span data-ttu-id="b359e-117">Un oggetto ValidationFailedEvent contiene i dettagli di un errore di convalida (problemi di integrità o di stabilità) rilevato durante la convalida del cluster.</span><span class="sxs-lookup"><span data-stu-id="b359e-117">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span></span> <span data-ttu-id="b359e-118">È possibile richiamare l'API GetChaosReport (C# or PowerShell) per ottenere il report delle esecuzioni di Chaos.</span><span class="sxs-lookup"><span data-stu-id="b359e-118">You can invoke the GetChaosReport API (C# or Powershell) to get the report of Chaos runs.</span></span> <span data-ttu-id="b359e-119">Gli eventi vengono conservati in un oggetto [Reliable ​Dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), che ha un criterio di troncamento influenzato da due configurazioni: **MaxStoredChaosEventCount** (valore predefinito 25000) e **StoredActionCleanupIntervalInSeconds** (valore predefinito 3600).</span><span class="sxs-lookup"><span data-stu-id="b359e-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="b359e-120">A ogni intervallo indicato da *StoredActionCleanupIntervalInSeconds* Chaos esegue un controllo e tutti gli eventi *MaxStoredChaosEventCount*, escluso il più recente, vengono eliminati dall'oggetto Reliable ​Dictionary.</span><span class="sxs-lookup"><span data-stu-id="b359e-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="b359e-121">Errori indotti da Chaos</span><span class="sxs-lookup"><span data-stu-id="b359e-121">Faults induced in Chaos</span></span>
<span data-ttu-id="b359e-122">Chaos genera errori in tutto il cluster di Service Fabric e comprime in poche ore gli errori riscontrati in mesi o anni.</span><span class="sxs-lookup"><span data-stu-id="b359e-122">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="b359e-123">Grazie alla combinazione di errori con interfoliazione e un'elevata frequenza di errori è possibile trovare casi limite che altrimenti non verrebbero considerati.</span><span class="sxs-lookup"><span data-stu-id="b359e-123">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="b359e-124">Questa applicazione di Chaos consente di ottenere un notevole miglioramento della qualità del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="b359e-124">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="b359e-125">Chaos induce errori delle categorie seguenti:</span><span class="sxs-lookup"><span data-stu-id="b359e-125">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="b359e-126">Riavvio di un nodo</span><span class="sxs-lookup"><span data-stu-id="b359e-126">Restart a node</span></span>
* <span data-ttu-id="b359e-127">Riavvio di un pacchetto di codice distribuito</span><span class="sxs-lookup"><span data-stu-id="b359e-127">Restart a deployed code package</span></span>
* <span data-ttu-id="b359e-128">Rimozione di una replica</span><span class="sxs-lookup"><span data-stu-id="b359e-128">Remove a replica</span></span>
* <span data-ttu-id="b359e-129">Riavvio di una replica</span><span class="sxs-lookup"><span data-stu-id="b359e-129">Restart a replica</span></span>
* <span data-ttu-id="b359e-130">Spostamento di una replica primaria (configurabile)</span><span class="sxs-lookup"><span data-stu-id="b359e-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="b359e-131">Spostamento di una replica secondaria (configurabile)</span><span class="sxs-lookup"><span data-stu-id="b359e-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="b359e-132">Chaos esegue più iterazioni.</span><span class="sxs-lookup"><span data-stu-id="b359e-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="b359e-133">Ogni iterazione consiste in errori e convalide cluster per il periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="b359e-133">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="b359e-134">È possibile configurare anche il tempo impiegato per la stabilizzazione del cluster e il completamento della convalida.</span><span class="sxs-lookup"><span data-stu-id="b359e-134">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="b359e-135">Se viene rilevato un errore di convalida dei cluster, Chaos genera e mantiene un ValidationFailedEvent con il timestamp UTC e i dettagli dell'errore.</span><span class="sxs-lookup"><span data-stu-id="b359e-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span> <span data-ttu-id="b359e-136">Si consideri, ad esempio, un'istanza di Chaos configurata per un'esecuzione della durata di un'ora e con un massimo di tre errori simultanei.</span><span class="sxs-lookup"><span data-stu-id="b359e-136">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="b359e-137">Chaos provoca tre errori, per poi convalidare l'integrità del cluster.</span><span class="sxs-lookup"><span data-stu-id="b359e-137">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="b359e-138">Ripete il passaggio precedente finché non viene esplicitamente interrotto con l'API StopChaosAsync o dopo un'ora.</span><span class="sxs-lookup"><span data-stu-id="b359e-138">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="b359e-139">Se in una qualsiasi iterazione il cluster diventa non integro, ovvero non si stabilizza entro il tempo definito da MaxClusterStabilizationTimeout, Chaos genera un evento ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="b359e-139">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="b359e-140">Questo evento indica che si è verificato un errore e potrebbe richiedersi un'ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="b359e-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="b359e-141">Per ottenere gli errori indotti da Chaos, è possibile usare l'API GetChaosReport (PowerShell o C#).</span><span class="sxs-lookup"><span data-stu-id="b359e-141">To get which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="b359e-142">L'API ottiene il segmento successivo del report di Chaos in base al token di continuazione passato o all'intervallo di tempo passato.</span><span class="sxs-lookup"><span data-stu-id="b359e-142">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span></span> <span data-ttu-id="b359e-143">È possibile specificare ContinuationToken per ottenere il segmento successivo del report di Chaos oppure è possibile specificare l'intervallo di tempo tramite StartTimeUtc ed EndTimeUtc, ma non è possibile specificare sia ContinuationToken che l'intervallo di tempo nella stessa chiamata.</span><span class="sxs-lookup"><span data-stu-id="b359e-143">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span></span> <span data-ttu-id="b359e-144">Quando ci sono più di 100 eventi di Chaos, il report di Chaos viene restituito in segmenti e ogni segmento contiene non più di 100 eventi.</span><span class="sxs-lookup"><span data-stu-id="b359e-144">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="b359e-145">Opzioni di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="b359e-145">Important configuration options</span></span>
* <span data-ttu-id="b359e-146">**TimeToRun**: tempo totale di esecuzione di Chaos prima del completamento con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="b359e-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="b359e-147">È possibile arrestare Chaos prima sia trascorso il tempo di esecuzione indicato da TimeToRun tramite l'API StopChaos.</span><span class="sxs-lookup"><span data-stu-id="b359e-147">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>

* <span data-ttu-id="b359e-148">**MaxClusterStabilizationTimeout**: tempo di attesa massimo perché il cluster diventi integro prima che venga generato un evento ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="b359e-148">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="b359e-149">Questa attesa consiste nel ridurre il carico nel cluster durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="b359e-149">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="b359e-150">I controlli eseguiti sono:</span><span class="sxs-lookup"><span data-stu-id="b359e-150">The checks performed are:</span></span>
  * <span data-ttu-id="b359e-151">Se l'integrità del cluster è OK</span><span class="sxs-lookup"><span data-stu-id="b359e-151">If the cluster health is OK</span></span>
  * <span data-ttu-id="b359e-152">Se l'integrità del servizio è OK</span><span class="sxs-lookup"><span data-stu-id="b359e-152">If the service health is OK</span></span>
  * <span data-ttu-id="b359e-153">Se si ottiene la dimensione di set di replica di destinazione per la partizione di servizio</span><span class="sxs-lookup"><span data-stu-id="b359e-153">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="b359e-154">Che non esistano repliche InBuild</span><span class="sxs-lookup"><span data-stu-id="b359e-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="b359e-155">**MaxConcurrentFaults**: numero massimo di errori simultanei indotti in ogni iterazione.</span><span class="sxs-lookup"><span data-stu-id="b359e-155">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="b359e-156">Maggiore è il numero, più aggressivo è Chaos e più complesse saranno le combinazioni di failover e transizioni di stato a cui viene sottoposto il cluster.</span><span class="sxs-lookup"><span data-stu-id="b359e-156">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="b359e-157">Indipendentemente da quanto è alto il valore di *MaxConcurrentFaults*, Chaos garantisce che in assenza di errori esterni non si verifichi una perdita di quorum o di dati.</span><span class="sxs-lookup"><span data-stu-id="b359e-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="b359e-158">**EnableMoveReplicaFaults**: abilita o disabilita gli errori che causano lo spostamento delle repliche primarie o secondarie.</span><span class="sxs-lookup"><span data-stu-id="b359e-158">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="b359e-159">Questi errori sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b359e-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="b359e-160">**WaitTimeBetweenIterations**: quantità di tempo di attesa tra due iterazioni.</span><span class="sxs-lookup"><span data-stu-id="b359e-160">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span></span> <span data-ttu-id="b359e-161">Indica il tempo durante cui Chaos rimane in pausa dopo l'esecuzione di un ciclo di errori e il completamento della convalida dell'integrità del cluster corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b359e-161">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span></span> <span data-ttu-id="b359e-162">Maggiore è il valore, minore è la frequenza media di inserimento degli errori.</span><span class="sxs-lookup"><span data-stu-id="b359e-162">The higher the value, the lower is the average fault injection rate.</span></span>
* <span data-ttu-id="b359e-163">**WaitTimeBetweenFaults**: quantità di tempo di attesa tra due errori consecutivi in una singola iterazione.</span><span class="sxs-lookup"><span data-stu-id="b359e-163">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="b359e-164">Maggiore è il valore, minore sarà la concorrenza degli errori, ovvero la loro sovrapposizione.</span><span class="sxs-lookup"><span data-stu-id="b359e-164">The higher the value, the lower the concurrency of (or the overlap between) faults.</span></span>
* <span data-ttu-id="b359e-165">**ClusterHealthPolicy**: criteri di integrità del cluster usati per convalidare l'integrità del cluster tra iterazioni di Chaos.</span><span class="sxs-lookup"><span data-stu-id="b359e-165">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span></span> <span data-ttu-id="b359e-166">Se si verifica un errore di integrità del cluster o un'eccezione imprevista durante l'esecuzione dell'errore, Chaos attende 30 minuti prima del successivo controllo di integrità, per fornire al cluster il tempo di recupero.</span><span class="sxs-lookup"><span data-stu-id="b359e-166">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span></span>
* <span data-ttu-id="b359e-167">**Context**: raccolta di coppie chiave-valore di tipo (string, string).</span><span class="sxs-lookup"><span data-stu-id="b359e-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="b359e-168">La mappa può essere usata per registrare le informazioni sull'esecuzione di Chaos.</span><span class="sxs-lookup"><span data-stu-id="b359e-168">The map can be used to record information about the Chaos run.</span></span> <span data-ttu-id="b359e-169">Non possono esserci più di 100 coppie di questo tipo e ogni stringa (chiave o valore) può essere costituita da un massimo di 4095 caratteri.</span><span class="sxs-lookup"><span data-stu-id="b359e-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="b359e-170">Questa mappa viene impostata dalla funzione di avvio dell'esecuzione di Chaos per l'archiviazione facoltativa del contesto dell'esecuzione specifica.</span><span class="sxs-lookup"><span data-stu-id="b359e-170">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="b359e-171">Come eseguire Chaos</span><span class="sxs-lookup"><span data-stu-id="b359e-171">How to run Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in the cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit the loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
